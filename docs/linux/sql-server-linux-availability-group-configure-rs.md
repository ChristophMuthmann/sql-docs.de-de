---
title: "Verfügbarkeitsgruppe für schreibgeschützte mit horizontaler Skalierung für SQL Server on Linux konfigurieren | Microsoft Docs"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 06/14/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: cf249ff8e6d2e82d1cf413bdec0272e3796b72cb
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---

# <a name="configure-read-scale-out-availability-group-for-sql-server-on-linux"></a>Konfigurieren von schreibgeschützten verfügbarkeitsgruppe mit horizontaler Skalierung für SQL Server on Linux

Sie können eine verfügbarkeitsgruppe für schreibgeschützte mit horizontaler Skalierung für SQL Server on Linux konfigurieren. Es gibt zwei Architekturen für Verfügbarkeitsgruppen. Ein *hohe Verfügbarkeit* Architektur verwendet einen Cluster-Manager, um die Geschäftskontinuität bereitstellen. Diese Architektur kann auch schreibgeschützte mit horizontaler Skalierung Replikate enthalten. Um die hohe Verfügbarkeit-Architektur zu erstellen, finden Sie unter [Konfigurieren von Always On-verfügbarkeitsgruppe für SQL Server on Linux](sql-server-linux-availability-group-configure-ha.md).

Dieses Dokument wird erläutert, wie zum Erstellen einer *Lesen mit horizontaler Skalierung* verfügbarkeitsgruppe ohne einen Cluster-Manager. Diese Architektur bietet nur read horizontale Skalierung nur. Es bietet keine hohen Verfügbarkeit.

[!INCLUDE [Create prerequisites](../includes/ss-linux-cluster-availability-group-create-prereq.md)]

## <a name="create-the-availability-group"></a>Erstellen der verfügbarkeitsgruppe.

Erstellen Sie die Verfügbarkeitsgruppe. Set `CLUSTER_TYPE = NONE`. Darüber hinaus legen Sie jedes Replikat mit `FAILOVER_MODE = NONE`. Clientanwendungen, die Ausführung der Analyse oder reporting Arbeitslasten können direkt eine Verbindung herstellen, auf die sekundären Datenbanken. Sie können auch eine schreibgeschützte Routingliste erstellen. Verbindungen mit dem primären Replikat vorwärts lesen verbindungsanforderungen an jede der sekundären Replikate aus der Routingliste in Roundrobin-Prinzip.

Das folgende Transact-SQL-Skript erstellt ein verfügbarkeitsgruppennamens `ag1`. Das Skript konfiguriert die verfügbarkeitsgruppenreplikaten mit `SEEDING_MODE = AUTOMATIC`. Diese Einstellung bewirkt, dass SQL Server zum Erstellen automatisch der Datenbank in jeder sekundären Serverinstanz ein, nachdem er mit der verfügbarkeitsgruppe hinzugefügt wurde. Aktualisieren Sie das folgende Skript für Ihre Umgebung. Ersetzen Sie die `**<node1>**` und `**<node2>**` Werte mit den Namen der SQL Server-Instanzen, die die Replikate hosten. Ersetzen Sie die `**<5022>**` mit dem Port, die Sie für den Endpunkt festlegen. Führen Sie die folgende Transact-SQL, auf dem primären SQL Server-Replikat:

```Transact-SQL
CREATE AVAILABILITY GROUP [ag1]
    WITH (CLUSTER_TYPE = NONE)
    FOR REPLICA ON
        N'**<node1>**' WITH (
            ENDPOINT_URL = N'tcp://**<node1>:**<5022>**',
            AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
            FAILOVER_MODE = MANUAL,
            SEEDING_MODE = AUTOMATIC,
                    SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL)
            ),
        N'**<node2>**' WITH ( 
            ENDPOINT_URL = N'tcp://**<node2>**:**<5022>**', 
            AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
            FAILOVER_MODE = MANUAL,
            SEEDING_MODE = AUTOMATIC,
            SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL)
            );
        
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

### <a name="join-secondary-sql-servers-to-the-availability-group"></a>Verknüpfen der sekundären SQL-Server mit der verfügbarkeitsgruppe

Die folgende Transact-SQL-Skript verknüpft einen Server mit einer verfügbarkeitsgruppe namens `ag1`. Aktualisieren Sie das Skript für Ihre Umgebung. Führen Sie auf jedem sekundären Replikat für die SQL Server die folgende Transact-SQL, um die verfügbarkeitsgruppe zu verknüpfen.

```Transact-SQL
ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = NONE);
         
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

[!INCLUDE [Create Post](../includes/ss-linux-cluster-availability-group-create-post.md)]

Dies ist keine Konfiguration mit hoher Verfügbarkeit, wenn Sie hohen Verfügbarkeit benötigen, befolgen Sie die Anweisungen unter [Konfigurieren von Always On-Verfügbarkeitsgruppe für SQL Server on Linux](sql-server-linux-availability-group-configure-ha.md). Insbesondere erstellen Sie die verfügbarkeitsgruppe mit `CLUSTER_TYPE=WSFC` (in Windows) oder `CLUSTER_TYPE=EXTERNAL` (in Linux) und integrieren mit einem Cluster-Manager - wsfc-unter Windows oder Schrittmacher unter Linux.

## <a name="connect-to-read-only-secondary-replicas"></a>Herstellen einer Verbindung mit schreibgeschützten sekundären Replikaten

Es gibt zwei Möglichkeiten, mit der schreibgeschützten sekundären Replikaten herstellen. Direktes Verbinden mit SQL Server-Instanz, die das sekundäre Replikat hostet und die Datenbanken Abfragen, oder sie können schreibgeschütztes routing. Schreibgeschütztes routing erfordert einen Listener.

[Lesbare sekundäre Replikate](../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)

[Schreibgeschütztes routing](../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md#ConnectToSecondary)

## <a name="fail-over-primary-replica-on-read-scale-out-availability-group"></a>Führen Sie ein Failover der primären Replikat für schreibgeschützten verfügbarkeitsgruppe mit horizontaler Skalierung

Jede verfügbarkeitsgruppe über nur ein primäres Replikat verfügt. Das primäre Replikat ermöglicht liest und schreibt. Zum Ändern, welches Replikat die primäre ist, können Sie ein Failover ausführen. In einer verfügbarkeitsgruppe für hohe Verfügbarkeit automatisiert werden die Cluster-Manager in den Failovervorgang. In einer schreibgeschützten verfügbarkeitsgruppe mit horizontaler Skalierung erfolgt während des Failovervorgangs manuell. Es gibt zwei Möglichkeiten, die das primäre Replikat in einer schreibgeschützten Skalierung verfügbarkeitsgruppe ein Failover aus.

- Erzwungenes manuelles Failover mit Datenverlust

- Manuell ein Failover ohne Datenverlust

### <a name="forced-fail-over-with-data-loss"></a>Erzwungenes Failover ohne Datenverlust

Verwenden Sie diese Methode, wenn das primäre Replikat nicht verfügbar ist und nicht wiederhergestellt werden kann. Sie finden weitere Informationen zu erzwungenes Failover ohne Datenverlust an [Ausführen eines erzwungenen manuellen Failovers](../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md).

So erzwingen Fehler über mit Datenverlust, Herstellen einer Verbindung mit der SQL-Instanz, die das sekundäre Zielreplikat hostet, und führen:
```Transact-SQL
ALTER AVAILABILITY GROUP [ag1] FORCE_FAILOVER_ALLOW_DATA_LOSS;
```

### <a name="manual-fail-over-without-data-loss"></a>Manuell ein Failover ohne Datenverlust

Verwenden Sie diese Methode, wenn das primäre Replikat verfügbar ist, jedoch müssen Sie vorübergehend oder dauerhaft, ändern Sie die Konfiguration, und ändern Sie die SQL Server-Instanz, der als Host das primäre Replikat. Vor dem Ausstellen von fehlerhaften manuelle Failover, stellen Sie sicher, dass das sekundäre Zielreplikat so, dass kein Datenverlust auf dem neuesten Stand ist. 

Die folgenden Schritte beschreiben, wie Sie manuell ein Failover ohne Datenverlust ausführen:

1. Stellen Sie das Ziel sekundäres Replikat synchronem Commit.

   ```Transact-SQL
   ALTER AVAILABILITY GROUP [ag1] MODIFY REPLICA ON N'**<node2>*' WITH (AVAILABILITY_MODE = SYNCHRONOUS_COMMIT);
   ```
1. Update `required_synchronized_secondaries_to_commit`auf 1.

   Diese Einstellung wird sichergestellt, dass jeder aktiven Transaktion ein Commit ausgeführt wurde, auf dem primären Replikat und mindestens ein synchrones sekundäres Replikat ist. Die verfügbarkeitsgruppe ist bereit für das Failover, wenn die Synchronization_state_desc synchronisiert wird und die Sequence_number für sowohl primären und sekundären Zielreplikat. Führen Sie diese Abfrage zu überprüfen:

   ```Transact-SQL
   SELECT ag.name, 
      drs.database_id, 
      drs.group_id, 
      drs.replica_id, 
      drs.synchronization_state_desc, 
      ag.sequence_number
   FROM sys.dm_hadr_database_replica_states drs, sys.availability_groups ag
   WHERE drs.group_id = ag.group_id; 
   ```

1. Herabstufen von das primäre Replikat zum sekundären Replikat. Nachdem das primäre Replikat herabgestuft wird, ist es schreibgeschützt. Führen Sie diesen Befehl für die SQL-Instanz hostet das primäre Replikat, um die Rolle auf sekundäre Datenbank zu aktualisieren:

   ```Transact-SQL
   ALTER AVAILABILITY GROUP [ag1] SET (ROLE = SECONDARY); 
   ```

1. Stufen Sie das sekundäre Zielreplikat zum primären. 

   ```Transact-SQL
   ALTER AVAILABILITY GROUP distributedag FORCE_FAILOVER_ALLOW_DATA_LOSS; 
   ```  

   > [!NOTE] 
   > So löschen Sie eine Verfügbarkeit Gruppe verwenden [DROP AVAILABILITY GROUP](https://docs.microsoft.com/en-us/sql/t-sql/statements/drop-availability-group-transact-sql). Für eine verfügbarkeitsgruppe mit CLUSTER_TYPE NONE oder extern erstellt wurden muss der Befehl für alle Replikate Teil der verfügbarkeitsgruppe ausgeführt werden.

## <a name="next-steps"></a>Nächste Schritte

[Konfigurieren der verteilten verfügbarkeitsgruppe](..\database-engine\availability-groups\windows\distributed-availability-groups-always-on-availability-groups.md)

[Weitere Informationen zu Verfügbarkeitsgruppen](..\database-engine\availability-groups\windows\overview-of-always-on-availability-groups-sql-server.md)



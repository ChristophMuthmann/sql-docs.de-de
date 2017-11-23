---
title: "Skalieren von Lesevorgängen verfügbarkeitsgruppe für SQL Server on Linux konfigurieren | Microsoft Docs"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 10/20/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 
ms.workload: Inactive
ms.openlocfilehash: bd3fa34a4fbfe40dfe184f7d5cf0e1f64372c8f2
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="configure-read-scale-availability-group-for-sql-server-on-linux"></a>Konfigurieren Sie Skalieren von Lesevorgängen verfügbarkeitsgruppe für SQL Server on Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Sie können eine verfügbarkeitsgruppe Skalieren von Lesevorgängen für SQL Server on Linux konfigurieren. Es gibt zwei Architekturen für Verfügbarkeitsgruppen. Ein *hohe Verfügbarkeit* Architektur verwendet einen Cluster-Manager, um die Geschäftskontinuität bereitstellen. Diese Architektur kann auch Skalieren von Lesevorgängen Replikate enthalten. Um die hohe Verfügbarkeit-Architektur zu erstellen, finden Sie unter [Konfigurieren von Always On-verfügbarkeitsgruppe für SQL Server on Linux](sql-server-linux-availability-group-configure-ha.md).

Dieses Dokument wird erläutert, wie zum Erstellen einer *Skalieren von Lesevorgängen* verfügbarkeitsgruppe ohne einen Cluster-Manager. Diese Architektur bietet nur lesen-Skalierung. Es bietet keine hohen Verfügbarkeit.

[!INCLUDE [Create prerequisites](../includes/ss-linux-cluster-availability-group-create-prereq.md)]

## <a name="create-the-availability-group"></a>Erstellen der verfügbarkeitsgruppe.

Erstellen Sie die Verfügbarkeitsgruppe. Set `CLUSTER_TYPE = NONE`. Darüber hinaus legen Sie jedes Replikat mit `FAILOVER_MODE = NONE`. Clientanwendungen, die Ausführung der Analyse oder reporting Arbeitslasten können direkt eine Verbindung herstellen, auf die sekundären Datenbanken. Sie können auch eine schreibgeschützte Routingliste erstellen. Verbindungen mit dem primären Replikat vorwärts lesen verbindungsanforderungen an jede der sekundären Replikate aus der Routingliste in Roundrobin-Prinzip.

Das folgende Transact-SQL-Skript erstellt ein verfügbarkeitsgruppennamens `ag1`. Das Skript konfiguriert die verfügbarkeitsgruppenreplikaten mit `SEEDING_MODE = AUTOMATIC`. Diese Einstellung bewirkt, dass SQL Server zum Erstellen automatisch der Datenbank in jeder sekundären Serverinstanz ein, nachdem er mit der verfügbarkeitsgruppe hinzugefügt wurde. Aktualisieren Sie das folgende Skript für Ihre Umgebung. Ersetzen Sie die `**<node1>**` und `**<node2>**` Werte mit den Namen der SQL Server-Instanzen, die die Replikate hosten. Ersetzen Sie die `**<5022>**` mit dem Port, die Sie für den Endpunkt festlegen. Führen Sie die folgende Transact-SQL, auf dem primären SQL Server-Replikat:

```SQL
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

```SQL
ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = NONE);
         
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

[!INCLUDE [Create Post](../includes/ss-linux-cluster-availability-group-create-post.md)]

Dies ist keine Konfiguration mit hoher Verfügbarkeit, wenn Sie hohen Verfügbarkeit benötigen, befolgen Sie die Anweisungen unter [Konfigurieren von Always On-Verfügbarkeitsgruppe für SQL Server on Linux](sql-server-linux-availability-group-configure-ha.md). Insbesondere erstellen Sie die verfügbarkeitsgruppe mit `CLUSTER_TYPE=WSFC` (in Windows) oder `CLUSTER_TYPE=EXTERNAL` (in Linux) und integrieren mit einem Cluster-Manager - wsfc-unter Windows oder Schrittmacher unter Linux.

## <a name="connect-to-read-only-secondary-replicas"></a>Herstellen einer Verbindung mit schreibgeschützten sekundären Replikaten

Es gibt zwei Möglichkeiten, mit der schreibgeschützten sekundären Replikaten herstellen. Direktes Verbinden mit SQL Server-Instanz, die das sekundäre Replikat hostet und die Datenbanken Abfragen, oder sie können schreibgeschütztes routing. Schreibgeschütztes routing erfordert einen Listener.

[Lesbare sekundäre Replikate](../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)

[Schreibgeschütztes routing](../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md#ConnectToSecondary)

## <a name="fail-over-primary-replica-on-read-scale-availability-group"></a>Führen Sie ein Failover der primären Replikat für verfügbarkeitsgruppe Skalieren von Lesevorgängen

[!INCLUDE[Force Failover](../includes/ss-force-failover-read-scale-out.md)]

## <a name="next-steps"></a>Nächste Schritte

[Konfigurieren verteilter Verfügbarkeitsgruppen](..\database-engine\availability-groups\windows\distributed-availability-groups-always-on-availability-groups.md)

[Weitere Informationen zu Verfügbarkeitsgruppen](..\database-engine\availability-groups\windows\overview-of-always-on-availability-groups-sql-server.md)

[Ausführen eines erzwungenen manuellen Failovers](../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md).


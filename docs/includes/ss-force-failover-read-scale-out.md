---
title: "Erzwingen, dass SQL Server-Failover für die verfügbarkeitsgruppe"
description: "Erzwingen Sie ein Failover für die Verfügbarkeitsgruppe mit Clustertyp None"
services: 
author: MikeRayMSFT
ms.service: 
ms.topic: include
ms.date: 02/05/2018
ms.author: mikeray
ms.custom: include file
ms.openlocfilehash: 10a2af2cb5bc9e98605a3ee988439e3c3be60c1e
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
Jede AG über nur ein primäres Replikat verfügt. Das primäre Replikat lässt Lese- und Schreibvorgänge zu. Zum Ändern, welches Replikat ein Primärschlüssel ist, können Sie ein Failover ausführen. In einer Verfügbarkeitsgruppe für hohe Verfügbarkeit automatisiert die Cluster-Manager während des Failovervorgangs. In einer Verfügbarkeitsgruppe mit Clustertyp NONE erfolgt während des Failovervorgangs manuell. 

Es gibt zwei Möglichkeiten, die das primäre Replikat in einer Verfügbarkeitsgruppe ein Failover mit Clustertyp NONE:

- Erzwungenes Manuelles Failover ohne Datenverlust
- Manuelles Failover ohne Datenverlust

### <a name="forced-manual-failover-with-data-loss"></a>Erzwungenes Manuelles Failover ohne Datenverlust

Verwenden Sie diese Methode, wenn das primäre Replikat ist nicht verfügbar und kann nicht wiederhergestellt werden. 

Verbinden Sie zum Erzwingen eines Failovers mit Verlust von Daten, SQL Server-Instanz, die das sekundäre Zielreplikat und das Ausführen hostet:

```SQL
ALTER AVAILABILITY GROUP [ag1] FORCE_FAILOVER_ALLOW_DATA_LOSS;
```

### <a name="manual-failover-without-data-loss"></a>Manuelles Failover ohne Datenverlust

Verwenden Sie diese Methode, wenn das primäre Replikat verfügbar ist. Dabei müssen Sie allerdings vorübergehend oder dauerhaft die Konfiguration ändern und die SQL Server-Instanz ändern, die das primäre Replikat hostet. Bevor Sie das manuelle Failover ausgeben, stellen Sie sicher, dass das sekundäre Zielreplikat um potenzielle Datenverluste zu vermeiden auf dem neuesten Stand ist. 

Um manuell ein Failover ohne Datenverlust ausführen:

1. Stellen Sie das sekundäre Zielreplikat `SYNCHRONOUS_COMMIT`.

   ```SQL
   ALTER AVAILABILITY GROUP [ag1] 
        MODIFY REPLICA ON N'<node2>' 
        WITH (AVAILABILITY_MODE = SYNCHRONOUS_COMMIT);
   ```

2. Führen Sie die folgende Abfrage aus, um zu ermitteln, dass aktive Transaktionen auf dem primären Replikat und mindestens ein sekundäres Replikat ausgeführt werden: 

   ```SQL
   SELECT ag.name, 
      drs.database_id, 
      drs.group_id, 
      drs.replica_id, 
      drs.synchronization_state_desc, 
      ag.sequence_number
   FROM sys.dm_hadr_database_replica_states drs, sys.availability_groups ag
   WHERE drs.group_id = ag.group_id; 
   ```

   Das sekundäre Replikat wird synchronisiert, wenn `synchronization_state_desc` `SYNCHRONIZED` ist.

3. Update `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` auf 1.

   Das folgende Skript legt `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` auf 1 auf einer Verfügbarkeitsgruppe mit dem Namen `ag1`. Bevor Sie das folgende Skript ausführen, ersetzen Sie `ag1` durch den Namen der Verfügbarkeitsgruppe:

   ```SQL
   ALTER AVAILABILITY GROUP [ag1] 
        SET REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT = 1;
   ```

   Diese Einstellung wird sichergestellt, dass jeder aktiven Transaktion ein Commit ausgeführt wurde, auf dem primären Replikat und mindestens ein sekundäres Replikat ist. 

4. Herabstufen von das primäre Replikat an ein sekundäres Replikat. Nachdem das primäre Replikat herabgestuft wird, ist es schreibgeschützt. Führen Sie diesen Befehl für die SQL Server-Instanz, die zum Aktualisieren der Rolle, die das primäre Replikat hostet `SECONDARY`:

   ```SQL
   ALTER AVAILABILITY GROUP [ag1] 
        SET (ROLE = SECONDARY); 
   ```

5. Stufen Sie das sekundäre Zielreplikat höher ein als das Primäre. 

   ```SQL
   ALTER AVAILABILITY GROUP ag1 FORCE_FAILOVER_ALLOW_DATA_LOSS; 
   ```  

   > [!NOTE] 
   > Verwenden Sie zum Löschen einer AG [DROP AVAILABILITY GROUP](https://docs.microsoft.com/en-us/sql/t-sql/statements/drop-availability-group-transact-sql). Geben Sie für eine Verfügbarkeitsgruppe mit Cluster erstellt keine oder extern, der Befehl muss auf allen Replikaten, die Teil der Verfügbarkeitsgruppe ausgeführt werden.
---
title: Betrieb der verfügbarkeitsgruppe SQL Server on Linux | Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 03/01/2018
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: ''
ms.workload: Inactive
ms.openlocfilehash: 3242b0be9b907244f6e6809946bb38118592ec3c
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="operate-always-on-availability-groups-on-linux"></a>Betreiben Sie Always On-Verfügbarkeitsgruppen unter Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

## <a name="upgrade-availability-group"></a>Aktualisieren der verfügbarkeitsgruppe.

Überprüfen Sie vor dem upgrade von einer verfügbarkeitsgruppe die Muster und Praktiken zur [Upgrade von Verfügbarkeitsgruppen-replikatsinstanzen](../database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances.md).

In den folgenden Abschnitten wird erläutert, wie ein paralleles Upgrade mit SQL Server-Instanzen unter Linux mit Verfügbarkeitsgruppen ausführen. 

### <a name="upgrade-steps-on-linux"></a>Aktualisieren Sie die Schritte unter Linux

Wenn Replikate der verfügbarkeitsgruppe für Instanzen von SQL Server unter Linux sind, ist der Clustertyp der verfügbarkeitsgruppe entweder `EXTERNAL` oder `NONE`. Eine verfügbarkeitsgruppe, die von einem Cluster-Manager verwaltet wird, neben Windows Server-Failovercluster (WSFC ist) `EXTERNAL`. Schrittmacher mit Corosync ist ein Beispiel für einen externen Cluster-Manager. Eine verfügbarkeitsgruppe mit keine Cluster-Manager verfügt Clustertyp `NONE` die Aktualisierung hier beschriebenen Schritte sind spezifisch für Verfügbarkeitsgruppen von Clustertyp `EXTERNAL` oder `NONE`.

Die Reihenfolge, die Instanzen aktualisiert, hängt ist ihrer Rolle Sekundär und davon, ob sie den synchronen bzw. asynchronen Replikate hosten. Aktualisieren Sie die Instanzen von SQL Server, die zuerst asynchronen sekundären Replikate hosten. Aktualisieren Sie dann die Instanzen, die synchronen sekundären Replikate hosten. 

   >[!NOTE]
   >Wenn eine verfügbarkeitsgruppe nur asynchrone verfügt Replikate, um Datenverluste zu vermeiden ändern ein Replikat, synchrone, und warten Sie, bis er synchronisiert wird. Aktualisieren Sie dann dieses Replikat aus.
   
Bevor Sie beginnen, müssen Sie jede Datenbank sichern.

1. Beenden Sie die Ressource auf dem Knoten, der das sekundäre Replikat als Ziel für Upgrade hostet.
   
   Beenden Sie vor dem Ausführen von Upgrade-Befehls, die Ressource, damit der Cluster nicht werden überwacht und sie unnötig fehl. Im folgenden Beispiel wird eine standorteinschränkung für den Knoten, der sich ergeben, wird für die Ressource beendet werden soll. Update `ag_cluster-master` mit dem Ressourcennamen und `nodeName1` mit dem Knoten, der das Ziel für das Upgrade Replikat hostet.

   ```bash
   pcs constraint location ag_cluster-master avoids nodeName1
   ```

1. Aktualisieren Sie SQL Server, auf dem sekundären Replikat.

   Das folgende Beispiel-Upgrades `mssql-server` und `mssql-server-ha` Pakete.

   ```bash
   sudo yum update mssql-server
   sudo yum update mssql-server-ha
   ```
1. Die standorteinschränkung zu entfernen.

   Beenden Sie vor dem Ausführen von Upgrade-Befehls, die Ressource, damit der Cluster nicht werden überwacht und sie unnötig fehl. Im folgenden Beispiel wird eine standorteinschränkung für den Knoten, der sich ergeben, wird für die Ressource beendet werden soll. Update `ag_cluster-master` mit dem Ressourcennamen und `nodeName1` mit dem Knoten, der das Ziel für das Upgrade Replikat hostet.

   ```bash
   pcs constraint remove location-ag_cluster-master-rhel1--INFINITY
   ```
   Stellen Sie als bewährte Methode sicher die Ressource wird gestartet (mit `pcs status` Befehl) und das sekundäre Replikat ist verbunden und Zustand "synchronisiert" nach dem Upgrade.

1. Nachdem alle sekundären Replikate aktualisiert werden, ein manuelles Failover zu einem synchronen sekundären Replikate.

   Für Verfügbarkeitsgruppen mit `EXTERNAL` cluster-Typ, verwenden Sie die Verwaltungstools fehlschlagen Over; Verfügbarkeitsgruppen mit `NONE` Clustertyp sollten Transact-SQL verwenden, um Failover auszuführen. 
   Im folgenden Beispiel wird ein Failover einer verfügbarkeitsgruppe mit die Verwaltungstools. Ersetzen Sie `<targetReplicaName>` durch den Namen des synchronen sekundären Replikats, das primäre werden soll:

   ```bash
   sudo pcs resource move ag_cluster-master <targetReplicaName> --master  
   ``` 
   
   >[!IMPORTANT]
   >Die folgenden Schritte gelten nur für Verfügbarkeitsgruppen, die nicht über einen Manager verfügen.

   Wenn der Cluster Verfügbarkeit Gruppentyp ist `NONE`manuell ein Failover. Führen Sie die folgenden Schritte wie folgt aus:

      A. Der folgende Befehl legt das primäre Replikat zum sekundären Replikat. Ersetzen Sie `AG1` durch den Namen der verfügbarkeitsgruppe. Führen Sie den Transact-SQL-Befehl für die Instanz von SQL Server hostet, die das primäre Replikat.

      ```transact-sql
      ALTER AVAILABILITY GROUP [ag1] SET (ROLE = SECONDARY);
      ```

      B. Der folgende Befehl legt ein sekundäres Replikat zum primären. Führen den folgenden Transact-SQL-Befehl auf der Zielinstanz von SQL Server - Instanz hostet, die das synchrone sekundäre Replikat.

      ```transact-sql
      ALTER AVAILABILITY GROUP [ag1] FAILOVER;
      ```

1. Aktualisieren Sie nach einem Failover SQL Server auf dem alten primären Replikat durch Wiederholen der vorherigen Prozedur ein.

   Das folgende Beispiel-Upgrades `mssql-server` und `mssql-server-ha` Pakete.

   ```bash
   # add constraint for the resource to stop on the upgraded node
   # replace 'nodename2' with the name of the cluster node targeted for upgrade
   pcs constraint location ag_cluster-master avoids nodeName2
   sudo yum update mssql-server
   sudo yum update mssql-server-ha
   ```
   
   ```bash
   # upgrade mssql-server and mssql-server-ha packages
   sudo yum update mssql-server
   sudo yum update mssql-server-ha
   ```

   ```bash
   # remove the constraint; make sure the resource is started and replica is connected and synchronized
   pcs constraint remove location-ag_cluster-master-rhel1--INFINITY
   ```

1. Bereinigen Sie für eine Verfügbarkeitsgruppen mit einem externen Cluster-Manager - wobei Clustertyp extern ist die standorteinschränkung, die durch das manuelle Failover verursacht wurde. 

   ```bash
   sudo pcs constraint remove cli-prefer-ag_cluster-master  
   ```

1. Fortsetzen der datenverschiebung für die aktualisierten sekundären Replikat - das frühere primäre Replikat. Dieser Schritt ist erforderlich, wenn eine höhere Version Instanz von SQL Server Protokollblöcke auf eine niedrigere Version-Instanz in einer verfügbarkeitsgruppe übertragen wird. Führen Sie den folgenden Befehl auf dem neuen sekundären Replikat (das frühere primäre Replikat).

   ```transact-sql
   ALTER DATABASE database_name SET HADR RESUME;
   ```

Nach dem Upgrade alle Server, können Sie ein Failback auszuführen. Führen Sie ein Failover zurück auf den ursprünglichen primären -, falls erforderlich. 

## <a name="drop-an-availability-group"></a>Löschen einer verfügbarkeitsgruppe

Führen Sie zum Löschen einer verfügbarkeitsgruppe [DROP AVAILABILITY GROUP](../t-sql/statements/drop-availability-group-transact-sql.md). Wenn der Clustertyp ist `EXTERNAL` oder `NONE` führen Sie den Befehl für jede Instanz von SQL Server, die ein Replikat hostet. Z. B. zum Löschen einer verfügbarkeitsgruppe namens `group_name` führen Sie den folgenden Befehl:

   ```transact-sql
   DROP AVAILABILITY GROUP group_name
   ```
 

## <a name="next-steps"></a>Nächste Schritte

[Konfigurieren Sie Red Hat Enterprise Linux-Cluster für SQL Server-Verfügbarkeitsgruppe Clusterressourcen](sql-server-linux-availability-group-cluster-rhel.md)

[Konfigurieren von SUSE Linux Enterprise Server-Cluster für Clusterressourcen für SQL Server-Verfügbarkeitsgruppe](sql-server-linux-availability-group-cluster-sles.md)

[Konfigurieren Sie Ubuntu-Cluster für SQL Server-Verfügbarkeitsgruppe Clusterressourcen](sql-server-linux-availability-group-cluster-ubuntu.md)

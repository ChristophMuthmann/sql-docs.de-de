---
title: "Betrieb der verfügbarkeitsgruppe SQL Server on Linux | Microsoft Docs"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 07/20/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: 07a50a59c320d7abb58c725c717393f8751b337d
ms.contentlocale: de-de
ms.lasthandoff: 08/28/2017

---
# <a name="operate-ha-availability-group-for-sql-server-on-linux"></a>Betreiben Sie HA-verfügbarkeitsgruppe für SQL Server on Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

## <a name="failover"></a>Führen Sie ein Failover der verfügbarkeitsgruppe.

Verwenden Sie die Verwaltungstools für ein Failover einer verfügbarkeitsgruppe, die von einer externen Cluster-Manager verwaltet werden. Verwenden Sie beispielsweise, wenn eine Lösung Schrittmacher verwendet, um ein Linux-Cluster zu verwalten, `pcs` ein manuelles Failover für RHEL oder Ubuntu ausführen. Verwenden Sie für SLES `crm`. 

> [!IMPORTANT]
> Unter normalen Betrieb wird kein Failover mit Transact-SQL oder SQL Server-Verwaltungstools wie SSMS oder PowerShell. Wenn `CLUSTER_TYPE = EXTERNAL`, der einzige zulässige Wert für `FAILOVER_MODE` ist `EXTERNAL`. Mit diesen Einstellungen werden alle manuell oder automatisch failoveraktionen vom externen Cluster-Manager ausgeführt. 

### <a name="manual-failover-examples"></a>Beispiele für manuelles failover

Ein manuelles Failover der verfügbarkeitsgruppe mit die externe Verwaltungstools. Initiieren Sie unter normalen Betrieb Failover mit Transact-SQL nicht. Wenn die externe Verwaltungstools nicht reagieren, können Sie die verfügbarkeitsgruppe für ein Failover erzwingen. Anweisungen, um das manuelle Failover erzwingen, finden Sie unter [manuell verschoben werden soll, wenn der Cluster-Tools nicht reaktionsfähig sind](#forceManual).

Schließen Sie das manuelle Failover in zwei Schritten. 

1. Verschieben Sie die verfügbarkeitsgruppenressource aus dem Clusterknoten, der die Ressourcen auf einem neuen Knoten besitzt.

   Der Cluster-Manager verschiebt die verfügbarkeitsgruppenressource und fügt eine Einschränkung Speicherort. Diese Einschränkung wird die Ressource zur Ausführung auf den neuen Knoten konfiguriert. Sie müssen diese Einschränkung entfernen, um die verschoben werden, entweder manuell oder automatisch in der Zukunft Failover.

2. Die standorteinschränkung zu entfernen.

#### <a name="1-manually-fail-over"></a>1. Ausführen des manuellen Failovers

Um manuell ein Failover einer verfügbarkeitsgruppe Ressource "Group" mit dem Namen *Ag_cluster* auf Clusterknoten mit dem Namen *nodeName2*, führen Sie die entsprechenden Befehl für den Verteilungspunkt:

- **RHEL/Ubuntu-Beispiel**

   ```bash
   sudo pcs resource move ag_cluster-master nodeName2 --master
   ```

- **SLES-Beispiel**

   ```bash
   crm resource migrate ag_cluster nodeName2
   ```



>[!IMPORTANT]
>Nachdem Sie manuell ein Failover einer Ressource aus, müssen Sie eine standorteinschränkung entfernen, die während des Verschiebens automatisch hinzugefügt wird.

#### <a name="2-remove-the-location-constraint"></a>2. Entfernen der Speicherorteinschränkung

Während einer manuellen Verschiebung der `pcs` Befehl `move` oder `crm` Befehl `migrate` Fügt eine standorteinschränkung für die Ressource auf dem neuen Zielknoten abgelegt werden soll. Um die neue Einschränkung anzuzeigen, führen Sie den folgenden Befehl nach dem Verschieben der Ressource aus:

- **RHEL/Ubuntu-Beispiel**

   ```bash
   sudo pcs constraint --full
   ```

- **SLES-Beispiel**

   ```bash
   crm config show
   ```

Sie müssen die Speicherorteinschränkung entfernen, damit zukünftige Verschiebungen, einschließlich manuelles Failover, erfolgreich sind. 

Führen Sie den folgenden Befehl aus, um die Beschränkung zu entfernen. 

- **RHEL/Ubuntu-Beispiel**

   In diesem Beispiel `ag_cluster-master` ist der Name der Ressource, die verschoben wurde. 

   ```bash
   sudo pcs resource clear ag_cluster-master 
   ```

- **SLES-Beispiel**

   In diesem Beispiel `ag_cluster` ist der Name der Ressource, die verschoben wurde. 

   ```bash
   crm resource clear ag_cluster
   ```

Alternativ können Sie den folgenden Befehl ausführen, um die Speicherorteinschränkung zu entfernen.  

- **RHEL/Ubuntu-Beispiel**

   Im folgenden Befehl ist `cli-prefer-ag_cluster-master` die ID der Einschränkung, die entfernt werden muss. `sudo pcs constraint --full` gibt diese ID zurück. 

   ```bash
   sudo pcs constraint remove cli-prefer-ag_cluster-master  
   ```
- **SLES-Beispiel**

   In den folgenden Befehl `cli-prefer-ms-ag_cluster` ist die ID der Einschränkung. `crm config show` gibt diese ID zurück. 
   
   ```bash
   crm configure
   delete cli-prefer-ms-ag_cluster 
   commit
   ```

>[!NOTE]
>Das automatische Failover fügt keine Speicherorteinschränkung hinzu, also ist keine Bereinigung notwendig. 

Weitere Informationen:
- [Red Hat - Managing Cluster Resources (Red Hat – Verwalten von Clusterressourcen)](http://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Configuring_the_Red_Hat_High_Availability_Add-On_with_Pacemaker/ch-manageresource-HAAR.html)
- [Schrittmacher - Ressourcen manuell verschieben](http://clusterlabs.org/doc/en-US/Pacemaker/1.1-pcs/html/Clusters_from_Scratch/_move_resources_manually.html)
 [SLES Administratorhandbuch - Ressourcen](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.troubleshooting.resource) 
 

### <a name="forceManual"></a>Bei der Cluster-Tools nicht reaktionsfähig sind manuell verschieben 

In Extremfällen, wenn ein Benutzer die Verwaltungstools verwenden kann, für die Interaktion mit dem Cluster (d. h. der Cluster ist nicht mehr reagiert, Clusterverwaltungsprogrammen haben ein fehlerhaftes Verhalten), die Benutzer möglicherweise manuell - Failover unter Umgehung des externen Cluster-Managers. Dies wird nicht empfohlen, für die normalen Vorgänge und sollte verwendet werden, in Fällen Cluster ausgeführt wird, die failoveraktion mit den Verwaltungstools Cluster auszuführen.

Gehen folgendermaßen Sie vor, um das Failover von SQL Server-Tools, bei einem Failover der verfügbarkeitsgruppe mit Cluster-Verwaltungstools können nicht:

1. Stellen Sie sicher, dass die verfügbarkeitsgruppenressource nicht mehr vom Cluster verwaltet wird. 

      - Fehler beim Festlegen der Ressourcenanbieters in den nicht verwalteten Modus. Dies signalisiert der Resource-Agent beendet die ressourcenüberwachung und Verwaltung. Beispiel: 
      
      ```bash
      sudo pcs resource unmanage <**resourceName**>
      ```

      - Löschen Sie die Ressource, schlägt der Versuch, den ressourcenmodus in den nicht verwalteten Modus festzulegen. Beispiel:

      ```bash
      sudo pcs resource delete <**resourceName**>
      ```

      >[!NOTE]
      >Wenn Sie eine Ressource löschen löscht es auch alle zugehörigen Einschränkungen. 

1. Der Kontext Sitzungsvariablen manuell festlegen `external_cluster`.

   ```Transact-SQL
   EXEC sp_set_session_context @key = N'external_cluster', @value = N'yes';
   ```

1. Ein Failover der verfügbarkeitsgruppe mit Transact-SQL. Im Beispiel unten ersetzen `<**MyAg**>` mit dem Namen der verfügbarkeitsgruppe. Herstellen einer Verbindung mit der Instanz von SQL Server, die das sekundäre Zielreplikat hostet, und führen Sie den folgenden Befehl aus:

   ```Transact-SQL
   ALTER AVAILABILITY GROUP <**MyAg**> FAILOVER;
   ```

1. Starten Sie Cluster ressourcenüberwachung und Verwaltung. Führen Sie den folgenden Befehl aus:

   ```bash
   sudo pcs resource manage <**resourceName**>
   sudo pcs resource cleanup <**resourceName**>
   ```

## <a name="database-level-monitoring-and-failover-trigger"></a>Ebene Überwachung und Failover Trigger auf Datenbankebene

Für `CLUSTER_TYPE=EXTERNAL`, die Failover-Semantik Trigger unterscheiden sich im Vergleich zu WSFC. Wenn die verfügbarkeitsgruppe auf einer Instanz von SQL Server in einem WSFC ist, sich im Übergang von `ONLINE` Status für die Datenbank bewirkt, die Integrität der verfügbarkeitsgruppe dass um einen Fehler zu melden. Dies wird signalisieren, dass den Cluster-Manager eine failoveraktion ausgelöst wird. SQL Server-Instanz kann nicht unter Linux mit dem Cluster kommunizieren. Überwachen der Integrität der Datenbank erfolgt "Außenseite in". Wenn Benutzer, für die Datenbank auf Failover Überwachung und Failover angemeldet (durch Festlegen der Option `DB_FAILOVER=ON` beim Erstellen der verfügbarkeitsgruppe), der Cluster wird überprüft, ob der Datenbankstatus ist `ONLINE` jedes Mal, wenn bei der Ausführung einer Aktion überwachen. Der Cluster fragt den Status im `sys.databases`. Für sämtliche Staaten unterscheidet `ONLINE`, löst einen Failover automatisch (wenn automatisches Failover-Bedingungen erfüllt sind). Die tatsächliche Zeit des Failovers hängt von der Häufigkeit der Überwachung Aktion sowie den Status einer Datenbank in sys.databases aktualisiert wird.

## <a name="upgrade-availability-group"></a>Aktualisieren der verfügbarkeitsgruppe.

Überprüfen Sie die bewährten Methoden an, vor dem upgrade von einer verfügbarkeitsgruppe [Upgrade von Verfügbarkeitsgruppen-replikatsinstanzen](../database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances.md).

In den folgenden Abschnitten wird erläutert, wie ein paralleles Upgrade mit SQL Server-Instanzen unter Linux mit Verfügbarkeitsgruppen ausführen. 

### <a name="upgrade-steps-on-linux"></a>Aktualisieren Sie die Schritte unter Linux

Wenn Replikate der verfügbarkeitsgruppe für Instanzen von SQL Server unter Linux sind, ist der Clustertyp der verfügbarkeitsgruppe entweder `EXTERNAL` oder `NONE`. Eine verfügbarkeitsgruppe, die von einem Cluster-Manager verwaltet wird, neben Windows Server-Failovercluster (WSFC ist) `EXTERNAL`. Schrittmacher mit Corosync ist ein Beispiel für einen externen Cluster-Manager. Eine verfügbarkeitsgruppe mit keine Cluster-Manager verfügt Clustertyp `NONE` die Aktualisierung hier beschriebenen Schritte sind spezifisch für Verfügbarkeitsgruppen von Clustertyp `EXTERNAL` oder `NONE`.

1. Bevor Sie beginnen, Sichern Sie jede Datenbank.
2. Aktualisieren von SQL Server-Instanzen, sekundäre Replikate gehostet.

    A. Aktualisieren Sie zuerst die asynchronen sekundären Replikate.

    B. Aktualisieren Sie die synchrone sekundäre Replikate.

   >[!NOTE]
   >Wenn eine verfügbarkeitsgruppe nur asynchrone verfügt wird Replikate - um Datenverluste zu vermeiden. ändern ein Replikat, synchrone und warten, bis er synchronisiert wird. Aktualisieren Sie dann dieses Replikat aus.
   
   b. 1. Beenden Sie die Ressource auf dem Knoten, der das sekundäre Replikat als Ziel für Upgrade hostet
   
   Beenden Sie vor dem Ausführen von Upgrade-Befehls, die Ressource, damit der Cluster nicht werden überwacht und sie unnötig fehl. Im folgenden Beispiel wird eine standorteinschränkung für den Knoten, der sich ergeben, wird für die Ressource beendet werden soll. Update `ag_cluster-master` mit dem Ressourcennamen und `nodeName1` mit dem Knoten, der das Ziel für das Upgrade Replikat hostet.

   ```bash
   pcs constraint location ag_cluster-master avoids nodeName1
   ```
   b. 2. Upgrade von SQL Server auf dem sekundären Replikat

   Das folgende Beispiel-Upgrades `mssql-server` und `mssql-server-ha` Pakete.

   ```bash
   sudo yum update mssql-server
   sudo yum update mssql-server-ha
   ```
   b. 3. Entfernen der Speicherorteinschränkung

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

1. Aktualisieren Sie SQL Server auf dem alten primären Replikat durch Wiederholen der Schritte b. 1-b. 3 oben beschriebene Prozedur, nach dem Failover.

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

1. Für eine Verfügbarkeitsgruppen mit einem externen-Cluster ist Manager – Geben Sie den Cluster, auf dem EXTERNEN und Bereinigung der standorteinschränkung, die durch das manuelle Failover verursacht wurde. 

   ```bash
   sudo pcs constraint remove cli-prefer-ag_cluster-master  
   ```

1. Fortsetzen der datenverschiebung für die aktualisierten sekundären Replikat - das frühere primäre Replikat. Dies ist erforderlich, wenn eine höhere Version Instanz von SQL Server Protokollblöcke auf eine niedrigere Version-Instanz in einer verfügbarkeitsgruppe übertragen wird. Führen Sie den folgenden Befehl auf dem neuen sekundären Replikat (das frühere primäre Replikat).

   ```transact-sql
   ALTER DATABASE database_name SET HADR RESUME;
   ```

Nach dem Upgrade alle Server, können Sie das Failback - ein Failover zurück auf den ursprünglichen primären -, falls erforderlich. 

## <a name="drop-an-availability-group"></a>Löschen einer verfügbarkeitsgruppe

Führen Sie zum Löschen einer verfügbarkeitsgruppe [DROP AVAILABILITY GROUP](../t-sql/statements/drop-availability-group-transact-sql.md). Wenn der Clustertyp ist `EXTERNAL` oder `NONE` führen Sie den Befehl für jede Instanz von SQL Server, die ein Replikat hostet. Z. B. zum Löschen einer verfügbarkeitsgruppe namens `group_name` führen Sie den folgenden Befehl:

   ```transact-sql
   DROP AVAILABILITY GROUP group_name
   ```
 

## <a name="next-steps"></a>Nächste Schritte

[Konfigurieren Sie Red Hat Enterprise Linux-Cluster für SQL Server-Verfügbarkeitsgruppe Clusterressourcen](sql-server-linux-availability-group-cluster-rhel.md)

[Konfigurieren von SUSE Linux Enterprise Server-Cluster für Clusterressourcen für SQL Server-Verfügbarkeitsgruppe](sql-server-linux-availability-group-cluster-sles.md)

[Konfigurieren Sie Ubuntu-Cluster für SQL Server-Verfügbarkeitsgruppe Clusterressourcen](sql-server-linux-availability-group-cluster-ubuntu.md)


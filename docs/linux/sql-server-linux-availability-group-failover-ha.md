---
title: Verwalten von verfügbarkeitsgruppenfailover - SQL Server on Linux | Microsoft Docs
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
ms.openlocfilehash: 83cb4a3493534c568a44e7f2ec478cf6ca7df9e2
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="always-on-availability-group-failover-on-linux"></a>Failover von AlwaysOn-Verfügbarkeitsgruppe unter Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Im Kontext einer verfügbarkeitsgruppe (AG) sind die primäre und sekundäre Rolle von verfügbarkeitsreplikaten normalerweise austauschbar, in einem Prozess wird als Failover bezeichnet. Failover können in drei Formen auftreten: automatisches Failover (ohne Datenverlust), geplantes manuelles Failover (ohne Datenverlust) und erzwungenes manuelles Failover (mit möglichem Datenverlust), welches in der Regel *erzwungenes Failover*genannt wird. Beim automatischen und geplanten manuellen Failover bleiben alle Daten erhalten. Eine Verfügbarkeitsgruppe führt ein Failover auf der Ebene des verfügbarkeitsreplikats. D. h. Failover eine Verfügbarkeitsgruppe auf eines ihrer sekundären Replikate (das aktuelle failoverziel). 

Hintergrundinformationen zum Failover finden Sie unter [Failover und failovermodi](../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md).

## <a name="failover"></a>Manuelles failover

Verwenden Sie die Verwaltungstools für ein Failover einer Verfügbarkeitsgruppe, die von einer externen Cluster-Manager verwaltet werden. Verwenden Sie beispielsweise, wenn eine Lösung Schrittmacher verwendet, um ein Linux-Cluster zu verwalten, `pcs` ein manuelles Failover für RHEL oder Ubuntu ausführen. Verwenden Sie für SLES `crm`. 

> [!IMPORTANT]
> Unter normalen Betrieb wird kein Failover mit Transact-SQL oder SQL Server-Verwaltungstools wie SSMS oder PowerShell. Wenn `CLUSTER_TYPE = EXTERNAL`, der einzige zulässige Wert für `FAILOVER_MODE` ist `EXTERNAL`. Mit diesen Einstellungen werden alle manuell oder automatisch failoveraktionen vom externen Cluster-Manager ausgeführt. Anweisungen, um Failover mit potenziellem Datenverlust zu erzwingen, finden Sie unter [erzwungenen Failovers](#forceFailover).

### <a name="a-namemanualfailovermanual-failover-steps"></a><a name="manualFailover">Manuelles Failover-Schritte

Zum Ausführen eines Failovers muss das sekundäre Replikat, das das primäre Replikat synchron sein. Wenn ein sekundäres Replikat asynchron, ist [Ändern des Verfügbarkeitsmodus](../database-engine/availability-groups/windows/change-the-availability-mode-of-an-availability-replica-sql-server.md).

Ein manuelles Failover in zwei Schritten.

   Erstens[ Ausführen des manuellen der Tabulatortaste verschieben AG Ressource](#manualMove) aus dem Clusterknoten, der die Ressourcen auf einem neuen Knoten besitzt.

   Der Cluster führt ein Failover aus der AG-Ressource und fügt eine Einschränkung Speicherort. Diese Einschränkung wird die Ressource zur Ausführung auf den neuen Knoten konfiguriert. Entfernen Sie diese Einschränkung, um ein Failover in der Zukunft ausgeführt werden.

   Zweitens [entfernen Sie die standorteinschränkung](#removeLocConstraint).

#### <a name="a-namemanualmovestep-1-manually-fail-over-by-moving-availability-group-resource"></a><a name="manualMove">Schritt 1. Ausführen des manuellen der Tabulatortaste verschieben die Verfügbarkeit der Ressource "Group"

Um manuell ein Failover einer AG-Ressource mit dem Namen *Ag_cluster* auf Clusterknoten mit dem Namen *nodeName2*, führen Sie den entsprechenden Befehl für den Verteilungspunkt:

- **RHEL/Ubuntu-Beispiel**

   ```bash
   sudo pcs resource move ag_cluster-master nodeName2 --master
   ```

- **SLES-Beispiel**

   ```bash
   crm resource migrate ag_cluster nodeName2
   ```

>[!IMPORTANT]
>Nachdem Sie manuell ein Failover einer Ressource aus, müssen Sie eine standorteinschränkung entfernen, die automatisch hinzugefügt wird.

#### <a name="a-nameremovelocconstraint-step-2-remove-the-location-constraint"></a><a name="removeLocConstraint"> Schritt 2. Entfernen der Speicherorteinschränkung

Während eines manuellen Failovers der `pcs` Befehl `move` oder `crm` Befehl `migrate` Fügt eine standorteinschränkung für die Ressource auf dem neuen Zielknoten abgelegt werden soll. Um die neue Einschränkung anzuzeigen, führen Sie den folgenden Befehl nach dem Verschieben der Ressource aus:

- **RHEL/Ubuntu-Beispiel**

   ```bash
   sudo pcs constraint --full
   ```

- **SLES-Beispiel**

   ```bash
   crm config show
   ```

Entfernen Sie die standorteinschränkung, damit zukünftige - einschließlich Automatisches Failover - Failover erfolgreich ausgeführt werden. 

Um die Einschränkung zu entfernen, führen Sie den folgenden Befehl ein: 

- **RHEL/Ubuntu-Beispiel**

   In diesem Beispiel `ag_cluster-master` ist der Name der Ressource, die ein Failover ausgeführt. 

   ```bash
   sudo pcs resource clear ag_cluster-master 
   ```

- **SLES-Beispiel**

   In diesem Beispiel `ag_cluster` ist der Name der Ressource, die ein Failover ausgeführt. 

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
 
## <a name="forceFailover"></a> Erzwingen Sie ein failover 

Ein erzwungenes Failover dient ausschließlich zur Wiederherstellung im Notfall. In diesem Fall kann nicht mit Clusterverwaltungsprogrammen Failover, weil das primäre Datencenter ausfällt. Wenn Sie ein Failover auf ein nicht synchronisiertes sekundäres Replikat erzwingen, ist Datenverlust möglich. Erzwingen Sie Failover nur, wenn Sie Dienst sofort wiederherstellen müssen, die Verfügbarkeitsgruppe auf das Risiko des Datenverlustes in Kauf zu nehmen.

Wenn Sie die Verwaltungstools verwenden können, für die Interaktion mit dem Cluster – z. B. wenn der Cluster auf einen Notfall zurückzuführen im primären Datencenter nicht reagiert, müssen Sie möglicherweise Erzwingen eines Failovers, den externen Cluster-Manager zu umgehen. Diese Prozedur wird für regelmäßige Vorgänge nicht empfohlen, da es birgt das Risiko von Datenverlusten. Verwenden Sie diese Option, wenn Sie nicht die Verwaltungstools für die failoveraktion ausgeführt. Dieses Verfahren ist funktionell ähnelt [Ausführen eines erzwungenen manuellen Failovers](../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md) auf einer AG in Windows.
 
Dieser Vorgang für das Erzwingen eines Failovers ist spezifisch für SQL Server on Linux.

1. Stellen Sie sicher, dass die AG-Ressource nicht mehr vom Cluster verwaltet wird. 

      - Legen Sie die Ressource in den nicht verwalteten Modus auf dem Ziel-Clusterknoten. Mit diesem Befehl signalisiert den Resource-Agent beenden ressourcenüberwachung und Verwaltung. Beispiel: 
      
      ```bash
      sudo pcs resource unmanage <resourceName>
      ```

      - Löschen Sie die Ressource, schlägt der Versuch, den ressourcenmodus in den nicht verwalteten Modus festzulegen. Beispiel:

      ```bash
      sudo pcs resource delete <resourceName>
      ```

      >[!NOTE]
      >Wenn Sie eine Ressource löschen, löscht es auch alle zugehörigen Einschränkungen. 

1. Legen Sie auf der Instanz von SQL Server, die das sekundäre Replikat hostet, den Kontext Sitzungsvariablen `external_cluster`.

   ```Transact-SQL
   EXEC sp_set_session_context @key = N'external_cluster', @value = N'yes';
   ```

1. Ein Failover der Verfügbarkeitsgruppe mit Transact-SQL. Ersetzen Sie im folgenden Beispiel `<MyAg>` durch den Namen der Verfügbarkeitsgruppe. Herstellen einer Verbindung mit der Instanz von SQL Server, die das sekundäre Zielreplikat hostet, und führen Sie den folgenden Befehl aus:

   ```Transact-SQL
   ALTER AVAILABILITY GROUP <MyAg> FORCE_FAILOVER_ALLOW_DATA_LOSS;
   ```

1.  Schalten Sie nach einem erzwungenen Failover der Verfügbarkeitsgruppe in einen fehlerfreien Zustand vor dem Neustarten der Cluster ressourcenüberwachung und Verwaltung oder Neuerstellen der AG-Ressource. Überprüfen Sie die [wichtige Aufgaben nach einem erzwungenen Failover](../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md#FollowUp).

1.  Starten Sie entweder Cluster ressourcenüberwachung und Verwaltung:

   Um die Cluster ressourcenüberwachung und Verwaltung neu zu starten, führen Sie den folgenden Befehl ein:

   ```bash
   sudo pcs resource manage <resourceName>
   sudo pcs resource cleanup <resourceName>
   ```

   Wenn Sie die Clusterressource gelöscht, neu erstellen. Die Clusterressource neu erstellen möchten, befolgen Sie die Anweisungen unter [erstellen verfügbarkeitsgruppenressource](sql-server-linux-availability-group-cluster-rhel.md#create-availability-group-resource).

>[!Important]
>Verwenden Sie nicht die vorherigen Schritte für Notfallwiederherstellungsverfahren, da sie Datenverluste riskieren. Ändern Sie stattdessen das asynchrone Replikat, synchrone und die Buildanweisungen für [normalen Manuelles Failover](#manualFailover).

## <a name="database-level-monitoring-and-failover-trigger"></a>Ebene Überwachung und Failover Trigger auf Datenbankebene

Für `CLUSTER_TYPE=EXTERNAL`, die Failover-Semantik Trigger unterscheiden sich im Vergleich zu WSFC. Wenn die Verfügbarkeitsgruppe auf einer Instanz von SQL Server in einem WSFC ist, sich im Übergang von `ONLINE` Status für die Datenbank bewirkt, die Integrität AG dass, um einen Fehler zu melden. Der Cluster-Manager löst als Antwort eine failoveraktion aus. SQL Server-Instanz kann nicht unter Linux mit dem Cluster kommunizieren. Eine Überwachung steht für Datenbankzustand erfolgt *außen*. Wenn Benutzer, für die Datenbank auf Failover Überwachung und Failover angemeldet (durch Festlegen der Option `DB_FAILOVER=ON` beim Erstellen der Verfügbarkeitsgruppe), der Cluster wird überprüft, ob der Datenbankstatus ist `ONLINE` jedes Mal, wenn sie eine Überwachung Aktion ausgeführt wird. Der Cluster fragt den Status im `sys.databases`. Für sämtliche Staaten unterscheidet `ONLINE`, löst einen Failover automatisch (wenn automatisches Failover-Bedingungen erfüllt sind). Die tatsächliche Zeit des Failovers hängt von der Häufigkeit der Überwachung Aktion sowie den Status einer Datenbank in sys.databases aktualisiert wird.

Automatisches Failover erfordert mindestens ein synchrones Replikat.

## <a name="next-steps"></a>Nächste Schritte

[Konfigurieren Sie Red Hat Enterprise Linux-Cluster für SQL Server-Verfügbarkeitsgruppe Clusterressourcen](sql-server-linux-availability-group-cluster-rhel.md)

[Konfigurieren von SUSE Linux Enterprise Server-Cluster für Clusterressourcen für SQL Server-Verfügbarkeitsgruppe](sql-server-linux-availability-group-cluster-sles.md)

[Konfigurieren Sie Ubuntu-Cluster für SQL Server-Verfügbarkeitsgruppe Clusterressourcen](sql-server-linux-availability-group-cluster-ubuntu.md)

---
title: "Erstellen einer Verfügbarkeitsgruppe (SQL Server PowerShell) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: availability-groups
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Availability Groups [SQL Server], creating
ms.assetid: bc69a7df-20fa-41e1-9301-11317c5270d2
caps.latest.revision: "41"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fa48b9e58bc8ab005359a2af97f8e8f77cd4cf62
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="create-an-availability-group-sql-server-powershell"></a>Erstellen einer Verfügbarkeitsgruppe (SQL Server PowerShell)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] In diesem Thema wird beschrieben, wie PowerShell-Cmdlets zum Erstellen und Konfigurieren einer Always On-Verfügbarkeitsgruppe mithilfe von PowerShell in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] verwendet werden. Eine *Verfügbarkeitsgruppe* definiert einen Satz von Benutzerdatenbanken, für die als eine einzelne Einheit ein Failover ausgeführt wird, sowie einen Satz von Failoverpartnern, die als *Verfügbarkeitsreplikate*bezeichnet werden und das Failover unterstützen.  
  
> [!NOTE]  
>  Eine Einführung zu Verfügbarkeitsgruppen finden Sie unter [Übersicht über Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](~/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)verwendet werden.  
  
-   **Vorbereitungen:**  
  
     [Voraussetzungen, Einschränkungen und Empfehlungen](#PrerequisitesRestrictions)  
  
     [Security](#Security)  
  
     [Zusammenfassung von Tasks und entsprechenden PowerShell-Cmdlets](#SummaryPSStatements)  
  
     [So richten Sie den SQL Server PowerShell-Anbieter ein und verwenden ihn](#PsProviderLinks)  
  
-   **Erstellen und Konfigurieren einer Verfügbarkeitsgruppe mit:**  [Verwenden von PowerShell zum Erstellen und Konfigurieren einer Verfügbarkeitsgruppe](#PowerShellProcedure)  
  
-   **Beispiele:**  [Verwenden von PowerShell zum Erstellen einer Verfügbarkeitsgruppe](#ExampleConfigureGroup)  
  
-   [Verwandte Aufgaben](#RelatedTasks)  
  
-   [Verwandte Inhalte](#RelatedContent)  
  
> [!NOTE]  
>  Als Alternative zur Verwendung von PowerShell-Cmdlets können Sie den Assistenten zum Erstellen einer Verfügbarkeitsgruppe oder [!INCLUDE[tsql](../../../includes/tsql-md.md)]verwenden. Weitere Informationen finden Sie unter [Verwenden des Dialogfelds „Neue Verfügbarkeitsgruppe“ &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md) oder [Erstellen einer Verfügbarkeitsgruppe &#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md)verwendet werden.  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
 Es wird dringend empfohlen, dass Sie diesen Abschnitt lesen, bevor Sie versuchen, Ihre erste Verfügbarkeitsgruppe zu erstellen.  
  
###  <a name="PrerequisitesRestrictions"></a> Voraussetzungen, Einschränkungen und Empfehlungen  
  
-   Überprüfen Sie vor dem Erstellen einer Verfügbarkeitsgruppe, ob sich die Hostinstanzen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] jeweils auf verschiedenen WSFC-Knoten (Windows Server-Failoverclustering) eines einzelnen WSFC-Failoverclusters befinden. Stellen Sie auch sicher, dass die Serverinstanzen die anderen Serverinstanzvoraussetzungen erfüllen, dass alle anderen [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]-Anforderungen erfüllt sind und dass Sie die Empfehlungen berücksichtigen. Für weitere Informationen empfehlen wir Ihnen dringend [Voraussetzungen, Einschränkungen und Empfehlungen für Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](~/database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die Mitgliedschaft in der festen Serverrolle **sysadmin** und die CREATE AVAILABILITY GROUP-Serverberechtigung, ALTER ANY AVAILABILITY GROUP-Berechtigung oder CONTROL SERVER-Berechtigung.  
  
###  <a name="SummaryPSStatements"></a> Zusammenfassung von Tasks und entsprechenden PowerShell-Cmdlets  
 In der folgenden Tabelle sind die grundlegenden Tasks für die Konfiguration einer Verfügbarkeitsgruppe aufgeführt, und es sind die Tasks angegeben, die von PowerShell-Cmdlets unterstützt werden. Die [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] -Tasks müssen in der Reihenfolge ausgeführt werden, in der sie in der Tabelle dargestellt sind.  
  
|Task|PowerShell-Cmdlets (falls verfügbar) oder Transact-SQL-Anweisung|Wo der Task auszuführen ist**\***|  
|----------|--------------------------------------------------------------------|---------------------------------|  
|Erstellen eines Datenbankspiegelungs-Endpunkts (einmal pro [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Instanz)|**New-SqlHadrEndPoint**|Führen Sie diesen Task auf jeder Serverinstanz aus, auf der der Datenbankspiegelungs-Endpunkt fehlt.<br /><br /> Hinweis: Verwenden Sie **Set-SqlHadrEndpoint**, um einen vorhandenen Datenbankspiegelungs-Endpunkt zu ändern.|  
|Erstellen der Verfügbarkeitsgruppe|Verwenden Sie zuerst das Cmdlet **New-SqlAvailabilityReplica** mit dem **-AsTemplate** -Parameter, um ein In-Memory-Verfügbarkeitsreplikatobjekt für jedes der beiden Verfügbarkeitsreplikate zu erstellen, die Sie in die Verfügbarkeitsgruppe einschließen möchten.<br /><br /> Erstellen Sie dann die Verfügbarkeitsgruppe, indem Sie das Cmdlet **New-SqlAvailabilityGroup** ausführen und auf Ihre Verfügbarkeitsreplikatobjekte verweisen.|Führen Sie diesen Task auf der Serverinstanz aus, auf der das anfängliche primäre Replikat gehostet werden soll.|  
|Verknüpfen eines sekundären Replikats mit einer Verfügbarkeitsgruppe|**Join-SqlAvailabilityGroup**|Führen Sie diesen Task auf jeder Serverinstanz aus, auf der ein sekundäres Replikat gehostet wird.|  
|Vorbereiten der sekundären Datenbank|**Backup-SqlDatabase** und **Restore-SqlDatabase**|Erstellen Sie Sicherungen auf der Serverinstanz, auf der das primäre Replikat gehostet wird.<br /><br /> Stellen Sie mit dem Wiederherstellungsparameter **NoRecovery** Sicherungen auf jeder Serverinstanz wieder her, auf der ein sekundäres Replikat gehostet wird. Wenn sich die Dateipfade zwischen den Computern unterscheiden, die das primäre Replikat und das sekundäre Zielreplikat hosten, verwenden Sie ebenfalls den Wiederherstellungsparameter **RelocateFile** .|  
|Starten der Datensynchronisierung durch Hinzufügen der einzelnen sekundären Datenbanken zur Verfügbarkeitsgruppe|**Add-SqlAvailabilityDatabase**|Führen Sie diesen Task auf jeder Serverinstanz aus, auf der ein sekundäres Replikat gehostet wird.|  
  
 \*Zur Ausführung eines bestimmten Tasks wechseln Sie mit**cd**in das Verzeichnis der angegebenen Serverinstanz(en).  
  
###  <a name="PsProviderLinks"></a> So richten Sie den SQL Server PowerShell-Anbieter ein und verwenden ihn  
  
-   [SQL Server PowerShell-Anbieter](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
-   [Aufrufen der SQL Server PowerShell-Hilfe](../../../relational-databases/scripting/get-help-sql-server-powershell.md)  
  
##  <a name="PowerShellProcedure"></a> Verwenden von PowerShell zum Erstellen und Konfigurieren einer Verfügbarkeitsgruppe  
  
> [!NOTE]  
>  Um die Syntax und ein Beispiel für ein bestimmtes Cmdlet anzuzeigen, verwenden Sie das **Get-Help** -Cmdlet in der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell-Umgebung. Weitere Informationen finden Sie unter [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md).  
  
1.  Wechseln Sie mit**cd**in das Verzeichnis der Serverinstanz, die das primäre Replikat hosten soll.  
  
2.  Erstellen Sie für das primäre Replikat ein Verfügbarkeitsreplikatobjekt im Arbeitsspeicher.  
  
3.  Erstellen Sie für jedes der sekundären Replikate ein Verfügbarkeitsreplikatobjekt im Arbeitsspeicher.  
  
4.  Erstellen Sie die Verfügbarkeitsgruppe.  
  
    > [!NOTE]  
    >  Die maximale Länge eines Verfügbarkeitsgruppennamens beträgt 128 Zeichen.  
  
5.  Verknüpfen Sie das neue sekundäre Replikat mit der Verfügbarkeitsgruppe. Weitere Informationen finden Sie unter [Verknüpfen eines sekundären Replikats mit einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-replica-to-an-availability-group-sql-server.md)mit einer Always On-Verfügbarkeitsgruppe verknüpft wird.  
  
6.  Erstellen Sie für jede Datenbank in der Verfügbarkeitsgruppe eine sekundäre Datenbank, indem Sie letzte Sicherungen der primären Datenbank mit RESTORE WITH NORECOVERY wiederherstellen.  
  
7.  Verknüpfen Sie alle neuen sekundären Datenbanken mit der Verfügbarkeitsgruppe. Weitere Informationen finden Sie unter [Verknüpfen eines sekundären Replikats mit einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-replica-to-an-availability-group-sql-server.md)verwendet werden.  
  
8.  Verwenden Sie optional den **dir** -Befehl von Windows, um den Inhalt der neuen Verfügbarkeitsgruppe zu überprüfen.  
  
> [!NOTE]  
>  Wenn die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Dienstkonten der Serverinstanzen unter unterschiedlichen Domänenbenutzerkonten ausgeführt werden, erstellen Sie auf jeder Serverinstanz eine Anmeldung für die andere Serverinstanz, und gewähren Sie dieser Anmeldung eine CONNECT-Berechtigung zum Zugreifen auf den lokalen Datenbankspiegelungs-Endpunkt.  
  
##  <a name="ExampleConfigureGroup"></a> Beispiel: Verwenden von PowerShell zum Erstellen einer Verfügbarkeitsgruppe  
 Im folgenden PowerShell-Beispiel wird eine einfache Verfügbarkeitsgruppe mit dem Namen `MyAG` erstellt und konfiguriert, die über zwei Verfügbarkeitsreplikate und eine Verfügbarkeitsdatenbank verfügt. Beispiel:  
  
1.  Sichert `MyDatabase` und das dazugehörige Transaktionsprotokoll.  
  
2.  Stellt `MyDatabase` und das dazugehörige Transaktionsprotokoll mithilfe der **-NoRecovery** -Option wieder her.  
  
3.  Erstellt eine speicherinterne Darstellung des primären Replikats, die von der lokalen Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (mit dem Namen `PrimaryComputer\Instance`) gehostet wird.  
  
4.  Erstellt eine speicherinterne Darstellung des sekundären Replikats, die von einer Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (mit dem Namen `SecondaryComputer\Instance`) gehostet wird.  
  
5.  Erstellt eine Verfügbarkeitsgruppe mit dem Namen `MyAG`.  
  
6.  Verknüpft das sekundäre Replikat mit der Verfügbarkeitsgruppe.  
  
7.  Verknüpft die sekundäre Datenbank mit der Verfügbarkeitsgruppe.  
  
```  
# Backup my database and its log on the primary  
Backup-SqlDatabase `  
    -Database "MyDatabase" `  
    -BackupFile "\\share\backups\MyDatabase.bak" `  
    -ServerInstance "PrimaryComputer\Instance"  
  
Backup-SqlDatabase `  
    -Database "MyDatabase" `  
    -BackupFile "\\share\backups\MyDatabase.log" `  
    -ServerInstance "PrimaryComputer\Instance" `  
    -BackupAction Log   
  
# Restore the database and log on the secondary (using NO RECOVERY)  
Restore-SqlDatabase `  
    -Database "MyDatabase" `  
    -BackupFile "\\share\backups\MyDatabase.bak" `  
    -ServerInstance "SecondaryComputer\Instance" `  
    -NoRecovery  
  
Restore-SqlDatabase `  
    -Database "MyDatabase" `  
    -BackupFile "\\share\backups\MyDatabase.log" `  
    -ServerInstance "SecondaryComputer\Instance" `  
    -RestoreAction Log `  
    -NoRecovery  
  
# Create an in-memory representation of the primary replica.  
$primaryReplica = New-SqlAvailabilityReplica `  
    -Name "PrimaryComputer\Instance" `  
    -EndpointURL "TCP://PrimaryComputer.domain.com:5022" `  
    -AvailabilityMode "SynchronousCommit" `  
    -FailoverMode "Automatic" `  
    -Version 12 `  
    -AsTemplate  
  
# Create an in-memory representation of the secondary replica.  
$secondaryReplica = New-SqlAvailabilityReplica `  
    -Name "SecondaryComputer\Instance" `  
    -EndpointURL "TCP://SecondaryComputer.domain.com:5022" `  
    -AvailabilityMode "SynchronousCommit" `  
    -FailoverMode "Automatic" `  
    -Version 12 `  
    -AsTemplate  
  
# Create the availability group  
New-SqlAvailabilityGroup `  
    -Name "MyAG" `  
    -Path "SQLSERVER:\SQL\PrimaryComputer\Instance" `  
    -AvailabilityReplica @($primaryReplica,$secondaryReplica) `  
    -Database "MyDatabase"  
  
# Join the secondary replica to the availability group.  
Join-SqlAvailabilityGroup -Path "SQLSERVER:\SQL\SecondaryComputer\Instance" -Name "MyAG"  
  
# Join the secondary database to the availability group.  
Add-SqlAvailabilityDatabase -Path "SQLSERVER:\SQL\SecondaryComputer\Instance\AvailabilityGroups\MyAG" -Database "MyDatabase"  
```  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
 **So konfigurieren Sie eine Serverinstanz für Always On-Verfügbarkeitsgruppen**  
  
-   [Aktivieren und Deaktivieren von Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](~/database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)  
  
-   [Erstellen eines Datenbankspiegelungs-Endpunkts für Always On-Verfügbarkeitsgruppen &#40;SQL Server PowerShell&#41;](~/database-engine/availability-groups/windows/database-mirroring-always-on-availability-groups-powershell.md)  
  
 **So konfigurieren Sie Verfügbarkeitsgruppen- und Replikateigenschaften**  
  
-   [Ändern des Verfügbarkeitsmodus eines Verfügbarkeitsreplikats &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-availability-mode-of-an-availability-replica-sql-server.md)  
  
-   [Ändern des Failovermodus eines Verfügbarkeitsreplikats &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-failover-mode-of-an-availability-replica-sql-server.md)  
  
-   [Erstellen oder Konfigurieren eines Verfügbarkeitsgruppenlisteners &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [Konfigurieren der flexiblen Failoverrichtlinie zum Steuern der Bedingungen für ein automatisches Failover &#40;Always On-Verfügbarkeitsgruppen&#41;](~/database-engine/availability-groups/windows/configure-flexible-automatic-failover-policy.md)  
  
-   [Angeben der Endpunkt-URL beim Hinzufügen oder Ändern eines Verfügbarkeitsreplikats &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
-   [Konfigurieren der Sicherung auf Verfügbarkeitsreplikaten &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)  
  
-   [Konfigurieren des schreibgeschützten Zugriffs auf ein Verfügbarkeitsreplikat &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [Konfigurieren des schreibgeschützten Routing für eine Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
-   [Ändern des Sitzungstimeouts für ein Verfügbarkeitsreplikat &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-session-timeout-period-for-an-availability-replica-sql-server.md)  
  
 **So schließen Sie die Konfiguration von Verfügbarkeitsgruppen ab**  
  
-   [Verknüpfen eines sekundären Replikats mit einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [Manuelles Vorbereiten einer sekundären Datenbank auf eine Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   [Verknüpfen einer sekundären Datenbank mit einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [Erstellen oder Konfigurieren eines Verfügbarkeitsgruppenlisteners &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
 **Alternative Möglichkeiten zum Erstellen einer Verfügbarkeitsgruppe**  
  
-   [Verwenden des Assistenten für Verfügbarkeitsgruppen &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Verwenden des Dialogfelds Neue Verfügbarkeitsgruppe &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [Erstellen einer Verfügbarkeitsgruppe &#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md)  
  
 **So beheben Sie Probleme für die Always On-Verfügbarkeitsgruppenkonfiguration**  
  
-   [Problembehandlung für die Always On-Verfügbarkeitsgruppenkonfiguration &#40;SQL Server&#41;](~/database-engine/availability-groups/windows/troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
-   [Problembehandlung bei einem fehlgeschlagenen Vorgang zum Hinzufügen einer Datei &#40;Always On-Verfügbarkeitsgruppen&#41;](~/database-engine/availability-groups/windows/troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)  
  
##  <a name="RelatedContent"></a> Verwandte Inhalte  
  
-   **Blogs:**  
  
     [Always On – HADRON Learning Series: Worker Pool Usage for HADRON Enabled Databases (Always On – HADRON-Lernreihe: Nutzung des Arbeitsthreadpools für HADRON-fähige Datenbanken)](http://blogs.msdn.com/b/psssql/archive/2012/05/17/Always%20On-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx)  
  
     [Konfigurieren von Always On mit SQL Server PowerShell](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/03/configuring-alwayson-with-sql-server-powershell/)  
  
     [SQL Server Always On Team Blogs: The official SQL Server Always On Team Blog (SQL Server Always On-Teamblogs: Der offizielle SQL Server Always On-Teamblog)](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
     [CSS SQL Server-Technikblogs](http://blogs.msdn.com/b/psssql/)  
  
-   **Videos:**  
  
     [Microsoft SQL Server Codename „Denali“ Always On-Reihe, Teil 1:Introducing the Next Generation High Availability Solution (Einführung in die nächste Generation von Lösungen mit hoher Verfügbarkeit)](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)  
  
     [Microsoft SQL Server Codename „Denali“ Always On-Reihe, Teil 2: Building a Mission-Critical High Availability Solution Using Always On (Erstellen einer unternehmenswichtigen Lösung für hohe Verfügbarkeit mit Always On)](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
-   **Whitepaper:**  
  
     [Microsoft SQL Server AlwaysOn-Lösungshandbuch zu hoher Verfügbarkeit und Notfallwiederherstellung](http://go.microsoft.com/fwlink/?LinkId=227600)  
  
     [Microsoft-Whitepapers für SQL Server 2012](http://msdn.microsoft.com/library/hh403491.aspx)  
  
     [Whitepapers des SQL Server-Kundenberatungsteams](http://sqlcat.com/)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Der Datenbankspiegelungs-Endpunkt &#40;SQL Server&#41;](../../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [Übersicht über Always On-Verfügbarkeitsgruppen (SQL Server)](~/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  








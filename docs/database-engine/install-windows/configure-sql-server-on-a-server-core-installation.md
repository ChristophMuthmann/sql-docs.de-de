---
title: "Konfigurieren von SQL Server in einer Server Core-Installation | Microsoft Docs"
ms.custom: ""
ms.date: "08/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "setup-install"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "IsHadrEnabled-Servereigenschaft"
  - "Server Core-Installation [SQL Server]"
ms.assetid: ed6e5e94-4b8d-422a-a17e-61b05a4df903
caps.latest.revision: 14
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 14
---
# Konfigurieren von SQL Server in einer Server Core-Installation
  Dieses Thema enthält Details zum Konfigurieren von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] für eine Server Core-Installation von [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1. Sehen Sie sich folgende Abschnitte an:  
  
-   [Konfigurieren und Verwalten von Server Core unter Windows Server](../../database-engine/install-windows/configure-sql-server-on-a-server-core-installation.md#BKMK_ConfigureWindows)  
  
-   [Installieren von SQL Server-Updates](../../database-engine/install-windows/configure-sql-server-on-a-server-core-installation.md#BKMK_InstallSQLUpdates)  
  
-   [Starten/Beenden des SQL Server-Diensts](../../database-engine/install-windows/configure-sql-server-on-a-server-core-installation.md#BKMK_StartStopServices)  
  
-   [AlwaysOn-Verfügbarkeitsgruppen aktivieren](../../database-engine/install-windows/configure-sql-server-on-a-server-core-installation.md#BKMK_EnableAlwaysON)  
  
-   [Konfigurieren von Remotezugriff von SQL Server, der auf Server Core ausgeführt wird](../../database-engine/install-windows/configure-sql-server-on-a-server-core-installation.md#BKMK_ConfigureRemoteAccess)  
  
-   [SQL Server Profiler](../../database-engine/install-windows/configure-sql-server-on-a-server-core-installation.md#BKMK_Profiler)  
  
-   [SQL Server-Überwachung](../../database-engine/install-windows/configure-sql-server-on-a-server-core-installation.md#BKMK_Auditing)  
  
-   [Befehlszeilen-Hilfsprogramme](../../database-engine/install-windows/configure-sql-server-on-a-server-core-installation.md#BKMK_CMD)  
  
-   [Verwenden von Tools zur Problembehandlung](../../database-engine/install-windows/configure-sql-server-on-a-server-core-installation.md#BKMK_troubleshoot)  
  
##  <a name="BKMK_ConfigureWindows"></a> Konfigurieren und Verwalten von Server Core unter Windows Server  
 Der Abschnitt enthält Verweise auf die Themen zur Konfiguration und Verwaltung einer Server Core-Installation.  
  
 Nicht alle Funktionen von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] werden im Server Core-Modus unterstützt.  Einige dieser Funktionen können auf einem Clientcomputer oder anderen Server, der nicht Server Core ausführt, installiert und mit den auf Server Core installierten Datenbankmoduldiensten verbunden werden.  
  
 Weitere Informationen zur Remotekonfiguration und -verwaltung einer Server Core-Installation finden Sie in den folgenden Themen:  
  
-   [Windows Server 2008 R2: Best Practices für die Server Core-Bereitstellungen](http://go.microsoft.com/fwlink/?LinkID=245957) (http://go.microsoft.com/fwlink/?LinkID=245957)  
  
-   [Configuring a Server Core installation: Overview](http://go.microsoft.com/fwlink/?LinkId=245958) (Konfigurieren einer Server Core-Installation: Übersicht) (http://go.microsoft.com/fwlink/?LinkId=245958)  
  
-   [Configuring a Server Core installation of Windows Server 2008 R2 with Sconfig.cmd](http://go.microsoft.com/fwlink/?LinkId=245959) (Konfigurieren einer Server Core-Installation von Windows Server 2008 R2 mit Sconfig.cmd) (http://go.microsoft.com/fwlink/?LinkId=245959)  
  
-   [Installing a server role on a server running a Server Core installation of Windows Server 2008 R2: Overview](http://go.microsoft.com/fwlink/?LinkId=245960) (Installieren einer Serverrolle auf einem Server mit einer Server Core-Installation von Windows Server 2008 R2: Übersicht) (http://go.microsoft.com/fwlink/?LinkId=245960)  
  
-   [Installing Windows Features on a server running a Server Core installation of Windows Server 2008 R2: Overview](http://go.microsoft.com/fwlink/?LinkId=245961) (Installieren von Windows Features auf einem Server mit einer Server Core-Installation von Windows Server 2008 R2: Übersicht) (http://go.microsoft.com/fwlink/?LinkId=245961)  
  
-   [Managing a Server Core installation: Overview](http://go.microsoft.com/fwlink/?LinkId=245962) (Verwalten einer Server Core-Installation: Übersicht) (http://go.microsoft.com/fwlink/?LinkId=245962)  
  
-   [Administering a Server Core installation: Overview](http://go.microsoft.com/fwlink/?LinkId=245963) (Verwalten einer Server Core-Installation als Administrator: Übersicht) (http://go.microsoft.com/fwlink/?LinkId=245963)  
  
##  <a name="BKMK_InstallSQLUpdates"></a> Installieren von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Updates  
 Dieser Abschnitt enthält Informationen zum Installieren von Updates für [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] auf einem Windows Server Core-Computer. Es empfiehlt sich, dass Kunden neue [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Updates zeitnah bewerten und installieren, um sicherzustellen, dass Systeme mit den letzten Sicherheitsupdates aktualisiert wurden. Weitere Informationen zum Installieren von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] auf einem Windows Server Core-Computer finden Sie unter [Installieren von SQL Server 2016 unter Server Core](../../database-engine/install-windows/install-sql-server-2016-on-server-core.md).  
  
 Es gibt zwei Szenarien für die Installation von Produktupdates:  
  
-   [Installieren von Updates für SQL Server 2016 während einer neuen Installation](../../database-engine/install-windows/configure-sql-server-on-a-server-core-installation.md#bkmk_NewInstall)  
  
-   [Installieren von Updates für SQL Server 2016, nachdem es bereits installiert wurde](../../database-engine/install-windows/configure-sql-server-on-a-server-core-installation.md#bkmk_alreadyInstall)  
  
###  <a name="bkmk_NewInstall"></a> Installieren von Updates für [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] während einer neuen Installation  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Setup unterstützt nur Installationen über die Eingabeaufforderung auf dem Server Core-Betriebssystem. Weitere Informationen finden Sie unter [Installieren von SQL Server 2016 über die Eingabeaufforderung](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md).  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Setup integriert die neuesten Produktupdates in die Installation des Hauptprodukts, sodass das Hauptprodukt und geeignete Updates gleichzeitig installiert werden.  
  
 Nachdem Setup die neuesten Versionen der anwendbaren Updates gefunden hat, lädt es diese herunter und integriert sie in den aktuellen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Installationsvorgang. Das Produktupdate kann ein kumulatives Update, Service Pack oder Service Pack plus kumulatives Update einziehen.  
  
 Geben Sie die Parameter UpdateEnabled und UpdateSource an, um die neuesten Produktupdates in die Installation des Hauptprodukts einzuschließen. Sehen Sie sich folgendes Beispiel an, um Produktupdates während des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Setups zu aktivieren:  
  
```tsql  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,Replication /INSTANCENAME=MSSQLSERVER /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="<StrongPassword>" /SQLSYSADMINACCOUNTS="<DomainName\UserName>" /AGTSVCACCOUNT="NT AUTHORITY\Network Service" /UpdateEnabled=True /UpdateSource=”<SourcePath>” /IACCEPTSQLSERVERLICENSETERMS  
```  
  
###  <a name="bkmk_alreadyInstall"></a> Installieren von Updates für [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], nachdem es bereits installiert wurde.  
 Auf einer installierten Instanz von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] empfiehlt es sich, dass Sie die letzten Sicherheitsupdates und wichtige Updates einschließlich allgemeiner Verteilungsversionen (GDRs) und Service Packs (SPS) anwenden. Einzelne kumulative Updates und Sicherheitsupdates sollten nach Bedarf übernommen werden. Werten Sie das Update aus; und wenn es benötigt wird, übernehmen Sie es.  
  
 Anwenden eines Updates über eine Eingabeaufforderung. Dabei wird <Paketname> mit dem Namen des Updatepakets ersetzt:  
  
-   Aktualisieren Sie eine einzelne [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz und alle freigegebenen Komponenten. Sie können die Instanz entweder mit dem InstanceName-Parameter oder dem InstanceID-Parameter angeben.  
  
    ```  
    <package_name>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch /InstanceName=MyInstance  
    ```  
  
-   Aktualisieren Sie nur freigegebene [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Komponenten:  
  
    ```  
    <package_name>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch  
    ```  
  
-   Aktualisieren Sie alle Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf dem Computer und alle freigegebenen Komponenten:  
  
    ```  
    <package_name>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch /AllInstances  
    ```  
  
##  <a name="BKMK_StartStopServices"></a> Starten/Beenden des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Diensts  
 Mithilfe der [sqlservr](../../tools/sqlservr-application.md)-Anwendung können Sie die Ausführung einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz von der Eingabeaufforderung aus starten, beenden, anhalten und fortsetzen.  
  
 Sie können auch Net Services verwenden, um die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Dienste zu starten und zu beenden.  
  
##  <a name="BKMK_EnableAlwaysON"></a> AlwaysOn-Verfügbarkeitsgruppen aktivieren  
 Die Aktivierung von AlwaysOn-Verfügbarkeitsgruppen ist eine Voraussetzung dafür, dass eine Serverinstanz Verfügbarkeitsgruppen als Lösung für hohe Verfügbarkeit und Notfallwiederherstellung verwenden kann. Weitere Informationen zum Verwalten der AlwaysOn-Verfügbarkeitsgruppen finden Sie unter [Aktivieren und Deaktivieren von AlwaysOn-Verfügbarkeitsgruppen (SQL Server)](../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md).  
  
### Remoteverwenden von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfigurations-Manager  
 Diese Schritte müssen auf einem PC mit [!INCLUDE[win7](../../includes/win7-md.md)]-Clientversion oder höher oder einem anderen Server ausgeführt werden, auf dem die grafische Shell für Server installiert ist (d.h. eine vollständige Installation von [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] oder einer [!INCLUDE[win8srv](../../includes/win8srv-md.md)]-Installation mit aktivierter grafischer Shell für Server).  
  
1.  Öffnen Sie die Computerverwaltung. Um die Computerverwaltung zu öffnen, gehen Sie wie folgt vor:  
  
    1.  Unter [!INCLUDE[win7](../../includes/win7-md.md)], Windows Server 2008 oder [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]:  
  
        1.  Klicken Sie auf Start, Alle Programme, Verwaltungstools und Computerverwaltung.  
  
        2.  Klicken Sie auf Start und Ausführen, geben Sie COMPMGMT.MSC ein, und klicken Sie dann auf OK.  
  
    2.  Unter [!INCLUDE[win8srv](../../includes/win8srv-md.md)] mit aktivierter grafischer Shell für Server:  
  
        1.  Bewegen Sie die Maus in die untere linke Ecke des Bildschirms, und klicken Sie mit der rechten Maustaste, wenn die Startüberlagerung angezeigt wird.  
  
        2.  Wählen Sie im Kontextmenü Computerverwaltung.  
  
2.  Klicken Sie in der Konsolenstruktur mit der rechten Maustaste auf Computerverwaltung, und klicken Sie dann auf Verbindung mit anderem Computer herstellen.  
  
3.  Geben Sie im Dialogfeld Computer auswählen den Namen des Server Core-Computers ein, den Sie verwalten möchten, oder klicken Sie auf Durchsuchen, um ihn zu suchen, und klicken Sie dann auf OK.  
  
4.  Klicken Sie in der Konsolenstruktur unter Computerverwaltung des Server Core-Computers auf Dienste und Anwendungen.  
  
5.  Doppelklicken Sie auf -Konfigurations-Manager [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
6.  Klicken Sie im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfigurations-Manager auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Dienste und mit der rechten Maustaste auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (\<Instanzname>), wobei \<Instanzname> der Name einer lokalen Serverinstanz ist, für die Sie Always On-Verfügbarkeitsgruppen aktivieren möchten, und klicken Sie auf „Eigenschaften“.  
  
7.  Wählen Sie die Registerkarte Hohe Verfügbarkeit (immer aktiviert) aus.  
  
8.  Überprüfen Sie, ob das Feld Name des Windows-Failoverclusters den Namen des lokalen Failoverclusterknoten enthält. Wenn dieses Feld leer ist, unterstützt diese Serverinstanz AlwaysOn-Verfügbarkeitsgruppen aktuell nicht. Der lokale Computer ist kein Clusterknoten, der WSFC-Cluster wurde geschlossen oder diese Edition von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] unterstützt keine AlwaysOn-Verfügbarkeitsgruppen.  
  
9. Aktivieren Sie das Kontrollkästchen AlwaysOn-Verfügbarkeitsgruppen aktivieren, und klicken Sie auf OK.  
  
10. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager speichert die Änderung. Dann müssen Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst manuell neu starten. Dies ermöglicht die Auswahl einer für die Geschäftsanforderungen optimalen Neustartzeit. Wenn der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst neu gestartet wird, wird AlwaysOn aktiviert, und die IsHadrEnabled-Servereigenschaft wird auf 1 festgelegt.  
  
> [!NOTE]  
>  -   Sie benötigen die entsprechenden Benutzerberechtigungen, oder Ihnen muss die entsprechende Autorität auf dem Zielcomputer delegiert worden sein, damit Sie eine Verbindung zu diesem Computer herstellen können.  
> -   Der Name des Computers, den Sie verwalten, wird in Klammern neben Computerverwaltung in der Konsolenstruktur angezeigt.  
  
### Verwenden von PowerShell-Cmdlets zur Aktivierung von AlwaysOn-Verfügbarkeitsgruppen  
 Das PowerShell-Cmdlet, Enable-SqlAlwaysOn, wird verwendet, um AlwaysOn-Verfügbarkeitsgruppen auf einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zu aktivieren. Wenn AlwaysOn-Verfügbarkeitsgruppen aktiviert werden, während der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Dienst ausgeführt wird, muss der Datenbankmoduldienst neu gestartet werden, damit die Änderungen abgeschlossen werden. Sofern Sie nicht den -Force-Parameter angeben, wird vom Cmdlet eine Bestätigung zum erneuten Starten des Diensts angefordert. Bei einem Abbruch wird kein Vorgang ausgeführt.  
  
 Zum Ausführen dieses Cmdlets benötigen Sie Administratorberechtigungen.  
  
 Sie können eine der folgenden Syntaxangaben verwenden, um AlwaysOn-Verfügbarkeitsgruppen für eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zu aktivieren:  
  
```  
Enable-SqlAlwaysOn [-Path <string>] [-Credential <PSCredential>] [-Force] [-NoServiceRestart] [-Confirm] [-WhatIf] [<Commom Parameters>]  
```  
  
```  
Enable-SqlAlwaysOn -InputObject <Server> [-Credential <PSCredential>] [-Force] [-NoServiceRestart] [-Confirm] [-WhatIf] [<Commom Parameters>]  
```  
  
```  
Enable-SqlAlwaysOn [-ServerInstance <string>] [-Credential <PSCredential>] [-Force] [-NoServiceRestart] [-Confirm] [-WhatIf] [<Commom Parameters>]  
```  
  
 Der folgende PowerShell-Befehl aktiviert AlwaysOn-Verfügbarkeitsgruppen auf einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Computer\Instanz):  
  
```  
Enable-SqlAlwaysOn -Path SQLSERVER:\SQL\Machine\Instance  
```  
  
##  <a name="BKMK_ConfigureRemoteAccess"></a> Konfigurieren von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Remotezugriff bei einer Server Core-Installation  
 Führen Sie die unten beschriebenen Aktionen aus, um den Remotezugriff auf eine [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] -Instanz zu konfigurieren, die auf [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] Server Core SP1 ausgeführt wird.  
  
### Aktivieren Sie Remoteverbindungen auf der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Um Remoteverbindungen zu aktivieren, verwenden Sie SQLCMD.exe lokal, und führen Sie die folgenden Anweisungen für die Server Core-Instanz aus:  
  
-   `EXEC sys.sp_configure N'remote access', N'1'`  
  
     `GO`  
  
-   `RECONFIGURE WITH OVERRIDE`  
  
     `GO`  
  
### Aktivieren und Starten des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Browserdiensts  
 Standardmäßig ist der Browserdienst deaktiviert.  Wenn er auf einer auf Server Core ausgeführten Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deaktiviert ist, führen Sie den folgenden Befehl von der Befehlszeile aus, um ihn zu aktivieren:  
  
 `sc config SQLBROWSER start= auto`  
  
 Nachdem er aktiviert wurde, führen Sie den folgenden Befehl von der Befehlszeile aus, um den Dienst zu starten:  
  
 `net start SQLBROWSER`  
  
### Erstellen von Ausnahmen von Windows-Firewall  
 Um Ausnahmen für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Zugriff in der Windows-Firewall zu erstellen, führen Sie die in [Konfigurieren der Windows-Firewall für den SQL Server-Zugriff](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md) angegebenen Schritte aus.  
  
### Aktivieren von TCP/IP auf der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Das TCP/IP-Protokoll kann durch Windows PowerShell für eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz auf Server Core aktiviert werden. Führen Sie die folgenden Schritte aus:  
  
1.  Starten Sie den Task-Manager auf dem Computer, der Windows Server 2008 R2 Server Core SP1 ausführt.  
  
2.  Klicken Sie auf der Registerkarte **Anwendungen** auf **Neuer Task**.  
  
3.  Geben Sie im Dialogfeld **Neuen Task erstellen** in das Feld **Öffnen** den Wert **sqlps.exe** ein, und klicken Sie auf **OK**. Dadurch wird das Fenster **Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell** geöffnet.  
  
4.  Führen Sie im Fenster **Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell** das folgende Skript aus, um das TCP/IP-Protokoll zu aktivieren:  
  
```  
$smo = 'Microsoft.SqlServer.Management.Smo.'  
$wmi = new-object ($smo + 'Wmi.ManagedComputer')  
# Enable the TCP protocol on the default instance.  If the instance is named, replace MSSQLSERVER with the instance name in the following line.  
$uri = "ManagedComputer[@Name='" + (get-item env:\computername).Value + "']/ServerInstance[@Name='MSSQLSERVER']/ServerProtocol[@Name='Tcp']"  
$Tcp = $wmi.GetSmoObject($uri)  
$Tcp.IsEnabled = $true  
$Tcp.Alter()  
$Tcp  
```  
  
##  <a name="BKMK_Profiler"></a> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler  
 Starten Sie [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] auf einem Remotecomputer, und wählen Sie im Menü Datei die Option Neue Ablaufverfolgung aus. Die Anwendung zeigt das Dialogfeld Verbindung mit Server herstellen an, in dem Sie die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf dem Server Core-Computer angeben können, mit der eine Verbindung hergestellt werden soll. Weitere Informationen finden Sie unter [Start SQL Server Profiler](../../tools/sql-server-profiler/start-sql-server-profiler.md).  
  
 Weitere Informationen zu den Berechtigungen, die zum Ausführen von [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] erforderlich sind, finden Sie unter [Erforderliche Berechtigungen zum Ausführen von SQL Server Profiler](../../tools/sql-server-profiler/permissions-required-to-run-sql-server-profiler.md).  
  
 Weitere Informationen zu [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] finden Sie unter [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md).  
  
##  <a name="BKMK_Auditing"></a> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Überwachung  
 Sie können [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)] remote verwenden, um eine Überwachung zu definieren. Nachdem die Überwachung erstellt und aktiviert wurde, empfängt das Ziel die Einträge. Weitere Informationen zum Erstellen und Verwalten von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Überwachungen finden Sie unter [SQL Server Audit &#40;Datenbankmodul&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  
  
##  <a name="BKMK_CMD"></a> Befehlszeilen-Hilfsprogramme  
 Sie können die folgenden Eingabeaufforderungs-Hilfsprogramme verwenden, mit denen Sie für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Vorgänge auf einem Server Core-Computer ein Skript erstellen können. Die folgende Tabelle enthält eine Liste der Eingabeaufforderung-Hilfsprogramme, die im Lieferumfang von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] für Server Core enthalten sind.  
  
|**Hilfsprogramm**|**Beschreibung**|**Installiert in**|  
|-----------------|---------------------|----------------------|  
|[bcp (Hilfsprogramm)](../../tools/bcp-utility.md)|Wird verwendet, um Daten in einem benutzerdefinierten Format zwischen einer [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz und einer Datendatei zu kopieren.|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[dtexec (Hilfsprogramm)](../../integration-services/packages/dtexec-utility.md)|Wird verwendet, um ein [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Paket zu konfigurieren und auszuführen.|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]DTS\Binn|  
|[dtutil (Hilfsprogramm)](../../integration-services/dtutil-utility.md)|Wird für die Verwaltung von SSIS-Paketen verwendet.|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]DTS\Binn|  
|[osql (Hilfsprogramm)](../../tools/osql-utility.md)|Ermöglicht es Ihnen, [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen, Systemprozeduren und Skriptdateien an der Eingabeaufforderung einzugeben.|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqlagent90 (Anwendung)](../../tools/sqlagent90-application.md)|Wird verwendet, um den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent von der Eingabeaufforderung zu starten.|\<Laufwerk>:\Programme\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\<*Instanzname*>\MSSQL\Binn|  
|[sqlcmd (Hilfsprogramm)](../../tools/sqlcmd-utility.md)|Ermöglicht es Ihnen, [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen, Systemprozeduren und Skriptdateien an der Eingabeaufforderung einzugeben.|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[SQLdiag (Hilfsprogramm)](../../tools/sqldiag-utility.md)|Wird zum Sammeln von Diagnoseinformationen für den [!INCLUDE[msCoName](../../includes/msconame-md.md)]-Kundenservice und -support verwendet.|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqlmaint (Hilfsprogramm)](../../tools/sqlmaint-utility.md)|Wird verwendet, um Datenbank-Wartungspläne auszuführen, die in früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erstellt wurden.|\<Laufwerk>:\Programme\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL13.MSSQLSERVER\MSSQL\Binn|  
|[sqlps (Hilfsprogramm)](../../tools/sqlps-utility.md)|Wird zum Ausführen von PowerShell-Befehlen und -Skripts verwendet. Lädt und registriert den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell-Anbieter sowie cmdlets.|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqlservr (Anwendung)](../../tools/sqlservr-application.md)|Wird verwendet, um eine Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] zur Problembehandlung von der Eingabeaufforderung aus zu starten und zu beenden.|\<Laufwerk>:\Programme\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL13.MSSQLSERVER\MSSQL\Binn|  
  
##  <a name="BKMK_troubleshoot"></a> Verwenden von Tools zur Problembehandlung  
 Mit dem Hilfsprogramm [SQLdiag](../../tools/sqldiag-utility.md) können Sie Protokolle und Datendateien von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und anderen Servertypen sammeln. Dies kann hilfreich sein, um Server für eine gewisse Zeit zu überwachen oder bestimmte Serverprobleme zu behandeln. SQLdiag dient dazu, das Sammeln von Diagnoseinformationen für Microsoft Support Services zu beschleunigen und zu vereinfachen.  
  
 Sie können das Hilfsprogramm in der Administrator-Eingabeaufforderung auf Server Core mit der Syntax starten, die im Thema [SQLdiag Utility](../../tools/sqldiag-utility.md)angegeben ist.  
  
## Siehe auch  
 [Installieren von SQL Server 2016 unter Server Core](../../database-engine/install-windows/install-sql-server-2016-on-server-core.md)   
 [Themen zu Vorgehensweisen für die Installation](../Topic/Installation%20How-to%20Topics.md)  
  
  
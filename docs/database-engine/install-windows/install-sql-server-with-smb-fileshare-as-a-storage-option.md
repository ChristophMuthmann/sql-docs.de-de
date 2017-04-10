---
title: "Installieren von SQL Server mit SMB-Dateifreigabe als Speicheroption | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "setup-install"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8b7810b2-637e-46a3-9fe1-d055898ba639
caps.latest.revision: 23
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 23
---
# Installieren von SQL Server mit SMB-Dateifreigabe als Speicheroption
  Ab [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] können Systemdatenbanken (master, model, msdb und tempdb) sowie [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Benutzerdatenbanken mit dem SMB-Dateiserver (Server Message Block) als Speicheroption installiert werden. Dies gilt sowohl für eigenständige [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]- als auch für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Failoverclusterinstallationen (FCI).  
  
> [!NOTE]  
>  Filestream auf einer SMB-Dateifreigabe wird derzeit nicht unterstützt.  
  
## Überlegungen zur Installation  
  
### SMB-Dateifreigabeformate:  
 Beim Angeben der SMB-Dateifreigabe werden die folgenden UNC-Pfadformate (Universal Naming Convention) für eigenständige und FCI-Datenbanken unterstützt:  
  
-   \\\Servername\Freigabename\  
  
-   \\\Servername\Freigabename  
  
 Weitere Informationen zu UNC (Universal Naming Convention) finden Sie unter [UNC](http://go.microsoft.com/fwlink/?LinkId=245534) (http://go.microsoft.com/fwlink/?LinkId=245534).  
  
 Der UNC-Loopbackpfad (ein UNC-Pfad, dessen Servername "localhost" oder "127.0.0.1" lautet bzw. dem Namen des lokalen Computers entspricht) wird nicht unterstützt. Darüber hinaus wird ein Sonderfall, bei dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] den Dateiservercluster verwendet, der auf demselben Knoten gehostet wird, auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird, ebenfalls nicht unterstützt. Um diese Situation zu vermeiden, wird empfohlen, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] - und Dateiservercluster auf getrennten Windows-Clustern zu erstellen.  
  
 Folgende UNC-Pfadformate werden nicht unterstützt:  
  
-   Loopbackpfad, z. B. „\\\localhost\\..\“ oder „\\\127.0.0.1\\...\“  
  
-   Administrative Freigaben, z. B. „\\\servername\x$“  
  
-   Weitere UNC-Pfadformate, wie „\\\\\?\x:\“  
  
-   Zugeordnete Netzlaufwerke.  
  
### Unterstützte DDL-Anweisungen(Data Definition Language, Datendefinitionssprache)  
 SMB-Dateifreigaben werden von den folgenden [!INCLUDE[tsql](../../includes/tsql-md.md)]-DDL-Anweisungen und gespeicherten Datenbankmodul-Prozeduren unterstützt:  
  
1.  [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)  
  
2.  [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
  
3.  [RESTORE &#40;Transact-SQL&#41;](../Topic/RESTORE%20\(Transact-SQL\).md)  
  
4.  [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)  
  
5.  [sp_attach_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-attach-db-transact-sql.md)  
  
6.  [sp_attach_single_file_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-attach-single-file-db-transact-sql.md)  
  
### Installationsoptionen  
  
-   Legen Sie den Parameter „Datenstammverzeichnis“ in der Setup-Benutzeroberfläche auf der Seite „Datenbankmodulkonfiguration“ auf der Registerkarte „Datenverzeichnisse“ auf „\\\fileserver1\share1\“ fest.  
  
-   Geben Sie „/INSTALLSQLDATADIR“ bei der Installation über die Eingabeaufforderung als „\\\fileserver1\share1\“ an.  
  
     Die folgende Beispielsyntax zeigt, wie Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mithilfe der SMB-Dateifreigabeoption auf einem eigenständigen Server installieren:  
  
    ```  
    Setup.exe /q /ACTION=Install /FEATURES=SQL /INSTANCENAME=MSSQLSERVER /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="<StrongPassword>" /SQLSYSADMINACCOUNTS="<DomainName\UserName>" /AGTSVCACCOUNT="<DomainName\UserName>" /AGTSVCPASSWORD="<StrongPassword>" /INSTALLSQLDATADIR="\\FileServer\Share1\" /IACCEPTSQLSERVERLICENSETERMS  
    ```  
  
     So installieren Sie eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Failoverclusterinstanz mit einem einzelnen Knoten mit der Standardinstanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] und [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]:  
  
    ```  
    setup.exe /q /ACTION=InstallFailoverCluster /InstanceName=MSSQLSERVER /INDICATEPROGRESS /ASSYSADMINACCOUNTS="<DomainName\UserName>" /ASDATADIR=<Drive>:\OLAP\Data /ASLOGDIR=<Drive>:\OLAP\Log /ASBACKUPDIR=<Drive>:\OLAP\Backup /ASCONFIGDIR=<Drive>:\OLAP\Config /ASTEMPDIR=<Drive>:\OLAP\Temp /FAILOVERCLUSTERDISKS="<Cluster Disk Resource Name - for example, 'Disk S:'" /FAILOVERCLUSTERNETWORKNAME="<Insert Network Name>" /FAILOVERCLUSTERIPADDRESSES="IPv4;xx.xxx.xx.xx;Cluster Network;xxx.xxx.xxx.x" /FAILOVERCLUSTERGROUP="MSSQLSERVER" /Features=AS,SQL /ASSVCACCOUNT="<DomainName\UserName>" /ASSVCPASSWORD="xxxxxxxxxxx" /AGTSVCACCOUNT="<DomainName\UserName>" /AGTSVCPASSWORD="xxxxxxxxxxx" /INSTALLSQLDATADIR="\\FileServer\Share1\" /SQLCOLLATION="SQL_Latin1_General_CP1_CS_AS" /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="xxxxxxxxxxx" /SQLSYSADMINACCOUNTS="<DomainName\UserName> /IACCEPTSQLSERVERLICENSETERMS  
    ```  
  
     Weitere Informationen zur Verwendung verschiedener Optionen für Befehlszeilenparameter in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] finden Sie unter [Installieren von SQL Server 2016 von der Eingabeaufforderung](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md).  
  
## Überlegungen zum Betriebssystem (SMB-Protokoll oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])  
 Jedes Windows-Betriebssystem verfügt über eine eigene SMB-Protokollversion, die gegenüber [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] transparent ist. Sie können die Vorteile der verschiedenen SMB-Protokollversionen in Bezug auf [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]vergleichen.  
  
|Betriebssystem|SMB2-Protokollversion|Vorteile für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|----------------------|---------------------------|-------------------------------------------|  
|[!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] SP 2|2.0|Verbesserte Leistung gegenüber SMB-Vorgängerversionen.<br /><br /> Dauerhaftigkeit zur einfacheren Wiederherstellung nach vorübergehenden Netzwerkstörungen.|  
|[!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP 1, einschließlich Server Core|2.1|Unterstützung eines höheren MTU-Werts, der für umfangreiche Datenübertragungen wie SQL-Sicherungs- und -Wiederherstellungsvorgänge vorteilhaft ist. Diese Funktion muss vom Benutzer aktiviert werden. Ausführliche Informationen zum Aktivieren dieser Funktion finden Sie unter [Neues in SMB](http://go.microsoft.com/fwlink/?LinkID=237319) (http://go.microsoft.com/fwlink/?LinkID=237319).<br /><br /> Signifikante Leistungsverbesserungen besonders für SQL-OLTP-Arbeitsauslastungen. Diese Leistungsverbesserungen erfordern die Anwendung eines Hotfixes. Weitere Informationen zum Hotfix finden Sie [hier](http://go.microsoft.com/fwlink/?LinkId=237320) (http://go.microsoft.com/fwlink/?LinkId=237320).|  
|[!INCLUDE[win8srv](../../includes/win8srv-md.md)], einschließlich Server Core|3.0|Unterstützung für transparentes Failover von Dateifreigaben – ohne Ausfallzeiten und Administratoreingriffe seitens SQL-DBA oder Dateiserveradministratoren in Dateiserver-Clusterkonfigurationen.<br /><br /> Unterstützung für die E/A über mehrere Netzwerkschnittstellen gleichzeitig sowie Toleranz für Netzwerkschnittstellenfehler.<br /><br /> Unterstützung für Netzwerkschnittstellen mit RDMA-Funktionen.<br /><br /> Weitere Informationen zu diesen Funktionen sowie zu Server Message Block finden Sie in der [Übersicht zu Server Message Block](http://go.microsoft.com/fwlink/?LinkId=253174) (http://go.microsoft.com/fwlink/?LinkId=253174).<br /><br /> Unterstützung für Dateiserver mit horizontaler Skalierung mit kontinuierlicher Verfügbarkeit.|  
|[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2, einschließlich Server Core|3.2|Unterstützung für transparentes Failover von Dateifreigaben – ohne Ausfallzeiten und Administratoreingriffe seitens SQL-DBA oder Dateiserveradministratoren in Dateiserver-Clusterkonfigurationen.<br /><br /> Unterstützung für E/A über mehrere Netzwerkschnittstellen gleichzeitig sowie Toleranz für Netzwerkschnittstellenfehler, unter Verwendung von SMB Multichannel.<br /><br /> Unterstützung für Netzwerkschnittstellen mit RDMA-Funktionen, unter Verwendung von SMB Direct.<br /><br /> Weitere Informationen zu diesen Funktionen sowie zu Server Message Block finden Sie in der [Übersicht zu Server Message Block](http://go.microsoft.com/fwlink/?LinkId=253174) (http://go.microsoft.com/fwlink/?LinkId=253174).<br /><br /> Unterstützung für Dateiserver mit horizontaler Skalierung mit kontinuierlicher Verfügbarkeit.<br /><br /> Optimiert für kleine wahlfreie Lese-/Schreib-E/A-Vorgänge, wie sie für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-OLTP üblich sind.<br /><br /> Maximale Übertragungseinheit (Maximum Transmission Unit, MTU) ist standardmäßig aktiviert; hierdurch wird bei umfassenden sequenziellen Übertragungen wie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Data Warehouse- und Datenbanksicherungen und -wiederherstellungen die Leistung wesentlich verbessert.|  
  
## Sicherheitsüberlegungen  
  
-   Das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienstkonto und das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienstkonto sollten über FULL CONTROL-Freigabeberechtigungen und NTFS-Berechtigungen für die SMB-Freigabeordner verfügen. Das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Dienstkonto kann ein Domänen- oder Systemkonto sein, wenn ein SMB-Dateiserver verwendet wird. Weitere Informationen zu Freigabe- und NTFS-Berechtigungen finden Sie unter [Freigabe- und NTFS-Berechtigungen auf einem Dateiserver](http://go.microsoft.com/fwlink/?LinkId=245535) (http://go.microsoft.com/fwlink/?LinkId=245535).  
  
    > [!NOTE]  
    >  Die FULL CONTROL-Freigabeberechtigungen und die NTFS-Berechtigungen in den SMB-Freigabeordnern sollten wie folgt beschränkt werden: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Dienstkonto, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent-Dienstkonto und Windows-Benutzer mit admin-Serverrollen.  
  
     Es wird empfohlen, das Domänenkonto als [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Dienstkonto zu verwenden. Wenn das Systemkonto als Dienstkonto verwendet wird, gewähren Sie die Berechtigungen für das Computerkonto im folgenden Format: *<Domänenname>***\\***<Computername>***$**.  
  
    > [!NOTE]  
    >  Beim [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Setup ist es erforderlich, das Domänenkonto als Dienstkonto anzugeben, wenn die SMB-Dateifreigabe als Speicheroption festgelegt wird. Bei der SMB-Dateifreigabe kann das Systemkonto erst nach der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Installation als Dienstkonto angegeben werden.  
    >   
    >  Virtuelle Konten können nicht gegenüber einem Remotestandort authentifiziert werden. Alle virtuellen Konten verwenden die Berechtigung des Computerkontos. Geben Sie das Computerkonto im Format *<Domänenname>***\\***<Computername>***$** an.  
  
-   Das für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Installation verwendete Konto sollte über FULL CONTROL-Berechtigungen für den als Datenverzeichnis verwendeten SMB-Dateifreigabeorder oder andere beim Cluster-Setup verwendete Datenordner (Benutzerdatenbankverzeichnis, Benutzerdatenbank-Protokollverzeichnis, TempDB-Verzeichnis, TempDB-Protokollverzeichnis, Sicherungsverzeichnis) verfügen.  
  
-   Dem Konto, das für die Installation von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet wird, müssen SeSecurityPrivilege-Berechtigungen auf dem SMB-Dateiserver zugewiesen werden. Diese Berechtigung weisen Sie zu, indem Sie die Konsole "Lokale Sicherheitsrichtlinie" auf dem Dateiserver verwenden, um der Richtlinie zum Verwalten von Überwachungs- und Sicherheitsprotokollen das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Setupkonto hinzuzufügen. Diese Einstellung ist in der Konsole "Lokale Sicherheitsrichtlinie" im Abschnitt Zuweisen von Benutzerrechten unter Lokale Richtlinien verfügbar.  
  
## Bekannte Probleme  
  
-   Nachdem Sie eine [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]-Datenbank getrennt haben, die sich auf einem dem Netzwerk zugeordneten Speichermedium befindet, könnte ein Problem mit der Datenbankberechtigung auftreten, wenn Sie versuchen, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank erneut anzufügen. Das Problem wird in [diesem KB-Artikel](http://go.microsoft.com/fwlink/?LinkId=237321) (http://go.microsoft.com/fwlink/?LinkId=237321) beschrieben. Wie Sie dieses Problem umgehen, erfahren Sie im KB-Artikel im Abschnitt **Weitere Informationen** .  
  
-   Wenn die SMB-Dateifreigabe als Speicheroption für eine gruppierte Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet wird, kann das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Failovercluster-Diagnoseprotokoll standardmäßig nicht in die Dateifreigabe geschrieben werden, da die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Ressourcen-DLL keine Lese-/Schreibberechtigung für die Dateifreigabe hat. Führen Sie eine der folgenden Aktionen aus, um diesen Fehler zu beheben:  
  
    1.  Erteilen Sie allen Computerobjekten im Cluster Lese-/Schreibberechtigungen für die Dateifreigabe.  
  
    2.  Legen Sie als Speicherort für die Diagnoseprotokolle einen lokalen Dateipfad fest. Sehen Sie sich folgendes Beispiel an:  
  
        ```sql  
        ALTER SERVER CONFIGURATION  
        SET DIAGNOSTICS LOG PATH = 'C:\logs';  
        ```  
  
## Siehe auch  
 [Planen einer SQL Server-Installation](../../sql-server/install/planning-a-sql-server-installation.md)   
 [Konfigurieren von Windows-Dienstkonten und -Berechtigungen](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)  
  
  
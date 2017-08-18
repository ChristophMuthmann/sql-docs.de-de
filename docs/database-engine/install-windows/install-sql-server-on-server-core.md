---
title: Installieren von SQL Server 2016 unter Server Core | Microsoft-Dokumentation
ms.custom: 
ms.date: 11/10/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1dd294cc-5b69-4d0c-9005-3e307b75678b
caps.latest.revision: 43
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 043a3dbcfcdfe75e77e8d50bd9698a05fbbf02c4
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="install-sql-server-on-server-core"></a>Installieren von SQL Server unter Server Core
  Sie können [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in einer Server Core-Installation installieren. Dieses Thema enthält setupspezifische Details zum Installieren von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] auf Server Core.  
  
 Die Server Core-Installationsoption stellt eine minimale Umgebung zum Ausführen von bestimmten Serverrollen bereit. Dies hilft, Wartung und Verwaltungsanforderungen und die Angriffsfläche für jene Serverrollen zu reduzieren. Weitere Informationen zur Server Core-Installation finden Sie unter [Installieren von Server Core](https://technet.microsoft.com/en-us/windows-server-docs/get-started/getting-started-with-server-core). Weitere Informationen zur Implementierung von Server Core unter [!INCLUDE[win8srv](../../includes/win8srv-md.md)]finden Sie unter [Server Core für Windows Server 2012](http://msdn.microsoft.com/library/hh846323\(VS.85\).aspx) (http://msdn.microsoft.com/library/hh846323(VS.85).aspx).  
  
 Eine Liste der aktuell unterstützten Betriebssysteme finden Sie unter [Hardware- und Softwareanforderungen für die Installation von SQL Server](https://docs.microsoft.com/en-us/sql/sql-server/install/hardware-and-software-requirements-for-installing-sql-server).

## <a name="prerequisites"></a>Erforderliche Komponenten  
  
|Anforderung|So führen Sie die Installation durch|  
|-----------------|--------------------|  
|[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4.6.1 |Für alle Editionen von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] (außer [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]) installiert Setup das [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4.6.1 Server Core-Profil. SQL Server Setup installiert dieses automatisch, wenn es nicht bereits installiert ist. Durch die Installation ist ein Neustart erforderlich. Sie können [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] installieren, bevor Sie Setup ausführen, um einen Neustart zu verhindern.|  
|Windows Installer 4.5|Im Lieferumfang der Server Core-Installation enthalten.|  
|Windows PowerShell|Im Lieferumfang der Server Core-Installation enthalten.|  
|Java Runtime |Um PolyBase verwenden zu können, müssen Sie die entsprechende Java Runtime installieren. Weitere Informationen finden Sie im [PolyBase-Installation](../../relational-databases/polybase/polybase-installation.md).|
  
##  <a name="BK_SupportedFeatures"></a> Unterstützte Funktionen  
 In der folgenden Tabelle finden Sie die Funktionen, die in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] bei einer Server Core-Installation unterstützt werden.  
  
|Funktion|Unterstützt|Zusätzliche Informationen|  
|-------------|---------------|----------------------------|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] -Dienste|ja||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Replikation|ja||  
|Volltextsuche|ja||  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|ja||  
|[!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)]|ja||  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|Nein||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Data Tools (SSDT)|Nein||  
|Konnektivität der Clienttools|ja||  
|Integration Services-Server|ja|Weitere Informationen zum neuen Integration Services-Server und dessen Features in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]finden Sie unter [Integration Services (SSIS)-Server](https://msdn.microsoft.com/library/bb522534.aspx).|  
|Clienttools-Abwärtskompatibilität|Nein||  
|Clienttools SDK|Nein||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Onlinedokumentation|Nein||  
|Verwaltungstools - Einfach|Ausschließlich remote|Die Installation dieser Funktionen unter Server Core wird nicht unterstützt. Diese Komponenten können auf einem anderen Server installiert werden, der nicht Server Core ist und nicht mit den auf Server Core installierten [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Diensten verbunden ist.|  
|Verwaltungstools - Vollständig|Ausschließlich remote|Die Installation dieser Funktionen unter Server Core wird nicht unterstützt. Diese Komponenten können auf einem anderen Server installiert werden, der nicht Server Core ist und nicht mit den auf Server Core installierten [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Diensten verbunden ist.|  
|Distributed Replay Controller|Nein||  
|Distributed Replay Client|Ausschließlich remote|Die Installation dieser Funktionen unter Server Core wird nicht unterstützt. Diese Komponenten können auf einem anderen Server installiert werden, der nicht Server Core ist und nicht mit den auf Server Core installierten [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Diensten verbunden ist.|  
|SQL Client Connectivity SDK|ja||  
|Microsoft Sync Framework|ja|Microsoft Sync Framework ist im Installationspaket von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] nicht enthalten. Sie können die geeignete Sync Framework-Version aus dem [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=221788) (http://go.microsoft.com/fwlink/?LinkId=221788) herunterladen und auf einem Computer mit der Server Core-Installation installieren.|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]|Nein||  
|[!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)]|Nein||  
  
## <a name="supported-scenarios"></a>Unterstützte Szenarios  
 In der folgenden Tabelle wird die Matrix unterstützter Szenarios zum Installieren von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] auf einer Server Core-Installation veranschaulicht.  
  
|||  
|-|-|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Editionen|Alle [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 64-Bit-Editionen*|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Sprache|Alle Sprachen|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Sprache auf Betriebssystem Sprache/Gebietsschema (Kombination)|ENG [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf JPN (Japanisch) Windows<br /><br /> ENG [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf GER (Deutsch) Windows<br /><br /> ENG [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf CHS (Chinesisch-China) Windows<br /><br /> ENG [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf ARA (Arabisch (SA)) Windows<br /><br /> ENG [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf THA (Thai) Windows<br /><br /> ENG [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf TRK (Türkisch) Windows<br /><br /> ENG [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf pt-PT (Portugiesisch Portugal) Windows<br /><br /> ENG [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf ENG (Englisch) Windows|  
|Windows-Edition|[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation|  
  
## <a name="upgrade"></a>Upgrade 
 In Server Core-Installationen werden Upgrades von [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] auf [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] unterstützt.  
  
## <a name="install"></a>Install  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] unterstützt kein Setup mit dem Installations-Assistenten unter dem Server Core-Betriebssystem. Beim Installieren unter Server Core unterstützt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Setup mithilfe des /Q-Parameters den vollständigen stillen Modus oder mithilfe des /QS-Parameters den einfachen stillen Modus. Weitere Informationen finden Sie unter [Installieren von SQL Server 2016 über die Eingabeaufforderung](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md).  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] kann nicht parallel mit früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf einem Computer installiert werden, auf dem [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] Server Core SP1 oder [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Server Core ausgeführt wird.  
  
 Unabhängig von der Installationsmethode ist es erforderlich, dass Sie den Softwarelizenzbedingungen als Einzelperson oder im Auftrag einer juristischen Person zustimmen, sofern die Verwendung der Software in keiner separaten Vereinbarung geregelt ist, z. B. einem [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Volumenlizenzvertrag oder einem Vertrag eines Drittanbieters mit einem ISV oder OEM.  
  
 Die Lizenzbedingungen werden in der Setup-Benutzeroberfläche angezeigt, damit Sie diese lesen und akzeptieren können. Unbeaufsichtigte Installationen (mit dem /Q-Parameter oder /QS-Parameter) müssen den /IACCEPTSQLSERVERLICENSETERMS-Parameter enthalten. Sie können die Lizenzbedingungen unter [Microsoft-Software-Lizenzbedingungen](http://go.microsoft.com/fwlink/?LinkId=148209)in einer separaten Kopie lesen.  
  
> [!NOTE]  
>  Abhängig davon, wie Sie die Software erworben haben (z. B. durch [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Volumenlizenzierung), unterliegt die Verwendung der Software möglicherweise zusätzlichen Bestimmungen.  
  
 Um bestimmte Funktionen zu installieren, verwenden Sie den /FEATURES-Parameter, und geben Sie die übergeordnete Funktion oder die Funktionswerte an. Weitere Informationen zu Funktionsparametern und ihrer Verwendung finden Sie in den folgenden Abschnitten.  
  
### <a name="feature-parameters"></a>Funktionsparameter  
  
|Funktionsparameter|Beschreibung|  
|-----------------------|-----------------|  
|SQLENGINE|Installiert nur [!INCLUDE[ssDE](../../includes/ssde-md.md)].|  
|-Replikation|Installiert die Replikationskomponente und das [!INCLUDE[ssDE](../../includes/ssde-md.md)].|  
|FULLTEXT|Installiert die FullText-Komponente und das [!INCLUDE[ssDE](../../includes/ssde-md.md)].|  
|AS|Installiert alle [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Komponenten.|  
|IS|Installiert alle [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Komponenten.|  
|CONN|Installiert die Konnektivitätskomponenten.| 
|ADVANCEDANALYTICS |Installiert R Services und erfordert das Datenbankmodul. Unbeaufsichtigte Installationen erfordern den Parameter /IACCEPTROPENLICENSETERMS.  |


 Vergleichen Sie die folgenden Beispiele für die Verwendung von Funktionsparametern:  
  
|Parameter und Werte|Beschreibung|  
|--------------------------|-----------------|  
|/FEATURES=SQLEngine|Installiert nur [!INCLUDE[ssDE](../../includes/ssde-md.md)].|  
|/FEATURES=SQLEngine,FullText|Installiert das [!INCLUDE[ssDE](../../includes/ssde-md.md)] und Volltext.|  
|/FEATURES=SQLEngine,Conn|Installiert [!INCLUDE[ssDE](../../includes/ssde-md.md)] und die Konnektivitätskomponenten.|  
|/FEATURES=SQLEngine,AS,IS,Conn|Installiert [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]und die Konnektivitätskomponenten.|  
|/FEATURES=SQLENGINE,ADVANCEDANALYTICS /IACCEPTROPENLICENSETERMS |Installiert das  [!INCLUDE[ssDE](../../includes/ssde-md.md)] und [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)].|  

  
### <a name="installation-options"></a>Installationsoptionen  
 Beim Installieren von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] unter einem Server Core-Betriebssystem unterstützt das Setup die folgenden Installationsoptionen:  
  
1.  **Installation über die Befehlszeile**  
  
     Um bestimmte Funktionen über die Befehlszeilen-Installationsoption zu installieren, verwenden Sie den /FEATURES-Parameter und geben die übergeordnete Funktion oder die Funktionswerte an. Nachfolgend wird gezeigt, wie die Parameter in der Befehlszeile verwendet werden:  
  
    ```  
    Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,Replication /INSTANCENAME=MSSQLSERVER /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="<StrongPassword>" /SQLSYSADMINACCOUNTS="<DomainName\UserName>" /AGTSVCACCOUNT="NT AUTHORITY\Network Service" /TCPENABLED=1 /IACCEPTSQLSERVERLICENSETERMS  
    ```  
  
2.  **Installation über die Konfigurationsdatei**  
  
     Setup unterstützt die Verwendung der Konfigurationsdatei nur über die Eingabeaufforderung. Die Konfigurationsdatei ist eine Textdatei mit der grundlegenden Struktur eines Parameters (Name/Wert-Paar) und einem beschreibenden Kommentar. Die an der Eingabeaufforderung angegebene Konfigurationsdatei sollte die Dateinamenerweiterung .INI haben. Nachfolgend finden Sie einige Beispiele für ConfigurationFile.INI:  
  
    - Installieren von [!INCLUDE[ssDE](../../includes/ssde-md.md)]. 
    
    Im folgenden Beispiel wird gezeigt, wie eine neue eigenständige Instanz, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)] einschließt, installiert wird:  
  
        ```  
        ; SQL Server Configuration File  
        [OPTIONS]  
  
        ; Specifies a Setup work flow, like INSTALL, UNINSTALL, or UPGRADE. This is a required parameter.   
  
        ACTION="Install"  
  
        ; Specifies features to install, uninstall, or upgrade. The lists of features include SQLEngine, FullText, Replication, AS, IS, and Conn.   
  
        FEATURES=SQLENGINE  
  
        ; Specify a default or named instance. MSSQLSERVER is the default instance for non-Express editions and SQLExpress for Express editions. This parameter is required when installing the ssNoVersion Database Engine, and Analysis Services (AS).  
  
        INSTANCENAME="MSSQLSERVER"  
  
        ; Specify the Instance ID for the ssNoVersion features you have specified. ssNoVersion directory structure, registry structure, and service names will incorporate the instance ID of the ssNoVersion instance.   
  
        INSTANCEID="MSSQLSERVER"  
  
        ; Account for ssNoVersion service: Domain\User or system account.   
  
        SQLSVCACCOUNT="NT Service\MSSQLSERVER"  
  
        ; Windows account(s) to provision as ssNoVersion system administrators.   
  
        SQLSYSADMINACCOUNTS="\<DomainName\UserName>"  
  
        ; Accept the License agreement to continue with Installation  
  
        IAcceptSQLServerLicenseTerms="True"  
  
        ```  
  
    -   Installieren von Konnektivitätskomponenten Im folgenden Beispiel wird gezeigt, wie die Konnektivitätskomponenten installiert werden:  
  
        ```  
        ; SQL Server Configuration File  
        [OPTIONS]  
  
        ; Specifies a Setup work flow, like INSTALL, UNINSTALL, or UPGRADE. This is a required parameter.   
  
        ACTION="Install"  
  
        ; Specifies features to install, uninstall, or upgrade. The lists of features include SQLEngine, FullText, Replication, AS, IS, and Conn.   
  
        FEATURES=Conn  
  
        ; Specifies acceptance of License Terms  
  
        IAcceptSQLServerLicenseTerms="True  
  
        ```  
  
    -   Installieren aller unterstützten Funktionen  
  
        Im folgenden Beispiel wird gezeigt, wie alle unterstützten Funktionen von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] unter Server Core installiert werden:  
  
        ```  
        ; SQL Server Configuration File  
        [OPTIONS]  
        ; Specifies a Setup work flow, like INSTALL, UNINSTALL, or UPGRADE. This is a required parameter.   
  
        ACTION="Install"  
  
        ; Specifies features to install, uninstall, or upgrade. The lists of features include SQLEngine, FullText, Replication, AS, IS, and Conn.   
  
        FEATURES=SQLENGINE,FullText,Replication,AS,IS,Conn  
  
        ; Specify a default or named instance. MSSQLSERVER is the default instance for non-Express editions and SQLExpress for Express editions. This parameter is required when installing the ssNoVersion Database Engine (SQL), or Analysis Services (AS).  
  
        INSTANCENAME="MSSQLSERVER"  
  
        ; Specify the Instance ID for the ssNoVersion features you have specified. ssNoVersion directory structure, registry structure, and service names will incorporate the instance ID of the ssNoVersion instance.   
  
        INSTANCEID="MSSQLSERVER"  
  
        ; Account for ssNoVersion service: Domain\User or system account.   
  
        SQLSVCACCOUNT="NT Service\MSSQLSERVER"  
  
        ; Windows account(s) to provision as ssNoVersion system administrators.   
  
        SQLSYSADMINACCOUNTS="\<DomainName\UserName>"  
  
        ; The name of the account that the Analysis Services service runs under.   
  
        ASSVCACCOUNT= "NT Service\MSSQLServerOLAPService"  
  
        ; Specifies the list of administrator accounts that need to be provisioned.   
  
        ASSYSADMINACCOUNTS="\<DomainName\UserName>"  
  
        ; Specifies the server mode of the Analysis Services instance. Valid values are MULTIDIMENSIONAL, POWERPIVOT or TABULAR. ASSERVERMODE is case-sensitive. All values must be expressed in upper case.   
  
        ASSERVERMODE="MULTIDIMENSIONAL"  
  
        ; Optional value, which specifies the state of the TCP protocol for the ssNoVersion service. Supported values are: 0 to disable the TCP protocol, and 1 to enable the TCP protocol.  
  
        TCPENABLED=1  
  
        ;Specifies acceptance of License Terms  
  
        IAcceptSQLServerLicenseTerms="True"  
        ```  
  
     Nachfolgend wird gezeigt, wie Sie das Setup mithilfe einer benutzerdefinierten bzw. der Standardkonfigurationsdatei starten.  
  
    -   Starten von Setup mithilfe einer benutzerdefinierten Konfigurationsdatei:  
  
         Angeben der Konfigurationsdatei an der Eingabeaufforderung:  
  
        ```  
        Setup.exe /QS /ConfigurationFile=MyConfigurationFile.INI  
        ```  
  
         Angeben von Kennwörtern an der Eingabeaufforderung und nicht in der Konfigurationsdatei:  
  
        ```  
        Setup.exe /QS /SQLSVCPASSWORD="************" /ASSVCPASSWORD="************"  /ConfigurationFile=MyConfigurationFile.INI  
        ```  
  
    -   Starten von Setup mithilfe der Standardkonfigurationsdatei DefaultSetup.ini:  
  
         Wenn sich die Datei „DefaultSetup.ini“ in den Ordnern „\x86“ und „\x64“ auf der Stammebene der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Quellmedien befindet, öffnen Sie die Datei „DefaultSetup.ini“, und fügen Sie der Datei den Parameter *Features* hinzu.  
  
         Wenn die Datei DefaultSetup.ini nicht vorhanden ist, können Sie sie erstellen und sie in die Ordner \x86 und \x64 auf der Stammebene der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Quellmedien kopieren.  
  
## <a name="configure-remote-access-of-includessnoversionincludesssnoversion-mdmd-on-server-core"></a>Konfigurieren von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Remotezugriff in Server Core  
 Führen Sie die unten beschriebenen Aktionen aus, um den Remotezugriff auf eine [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] -Instanz zu konfigurieren, die auf einer Server Core-Installation von [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 oder [!INCLUDE[win8srv](../../includes/win8srv-md.md)]ausgeführt wird.  
  
### <a name="enable-remote-connections-on-the-instance-of-includessnoversionincludesssnoversion-mdmd"></a>Aktivieren von Remoteverbindungen auf der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  

Um Remoteverbindungen zu aktivieren, verwenden Sie SQLCMD.exe lokal, und führen Sie die folgenden Anweisungen für die Server Core-Instanz aus:  

   ```Transact-SQL
   EXEC sys.sp_configure N'remote access', N'1'  
   GO
   RECONFIGURE WITH OVERRIDE
   GO
   ```  
  
### <a name="enable-and-start-the-includessnoversionincludesssnoversion-mdmd-browser-service"></a>Aktivieren und Starten des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] browser service  
 Standardmäßig ist der Browserdienst deaktiviert.  Wenn er auf einer auf Server Core ausgeführten Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deaktiviert ist, führen Sie den folgenden Befehl von der Befehlszeile aus, um ihn zu aktivieren:  
  
 `sc config SQLBROWSER start= auto`  
  
 Nachdem er aktiviert wurde, führen Sie den folgenden Befehl von der Befehlszeile aus, um den Dienst zu starten:  
  
 `net start SQLBROWSER`  
  
### <a name="create-exceptions-in-windows-firewall"></a>Erstellen von Ausnahmen von Windows-Firewall  
 Um Ausnahmen für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Zugriff in der Windows-Firewall zu erstellen, führen Sie die in [Konfigurieren der Windows-Firewall für den SQL Server-Zugriff](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)angegebenen Schritte aus.  
  
### <a name="enable-tcpip-on-the-instance-of-includessnoversionincludesssnoversion-mdmd"></a>Aktivieren von TCP/IP auf der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Das TCP/IP-Protokoll kann durch Windows PowerShell für eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz auf Server Core aktiviert werden. Führen Sie die folgenden Schritte aus:  
  
1.  Starten Sie den Task-Manager auf dem Computer, auf dem [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] Server Core SP1 oder [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Server Core ausgeführt wird.  
  
2.  Klicken Sie auf der Registerkarte **Anwendungen** auf **Neuer Task**.  
  
3.  Geben Sie im Dialogfeld **Neuen Task erstellen** in das Feld **Öffnen** den Wert **sqlps.exe** ein, und klicken Sie auf **OK**. Dadurch wird das Fenster **[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell** geöffnet.  
  
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
  
## <a name="uninstall"></a>Deinstallieren

 Nachdem Sie sich an einem Computer angemeldet haben, auf dem Server Core ausgeführt wird, sehen Sie eine beschränkte Desktopumgebung mit einer Administratoreingabeaufforderung. Sie können diese Eingabeaufforderung verwenden, um die Deinstallation von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] zu starten. Um eine Instanz von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]zu deinstallieren, starten Sie die Deinstallation im vollständigen stillen Modus mit dem /Q-Parameter oder im stillen einfachen Modus mit dem /QS-Parameter von der Eingabeaufforderung aus. Der /QS-Parameter zeigt den Status durch die Benutzeroberfläche an, akzeptiert jedoch keine Eingabe. /Q gibt an, dass Setup ohne Benutzeroberfläche in einem stillen Modus ausgeführt wird.  
  
 So deinstallieren Sie eine vorhandene Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
```  
Setup.exe /Q /Action=Uninstall /FEATURES=SQLEngine,AS,IS /INSTANCENAME=MSSQLSERVER  
```  
  
 Um eine benannte Instanz zu entfernen, geben Sie den Namen der Instanz an und nicht wie im vorhergehenden Beispiel `MSSQLSERVER`.  
  
## <a name="start-a-new-command-prompt"></a>Starten einer neuen Eingabeaufforderung

Wenn Sie die Eingabeaufforderung unbeabsichtigt schließen, können Sie eine neue Eingabeaufforderung starten, indem Sie folgende Schritte ausführen:  
 
1.  Drücken Sie STRG+UMSCHALT+ESC, um Task-Manager anzuzeigen.  
2.  Klicken Sie auf der Registerkarte **Anwendungen** auf **Neuer Task**.  
3.  Geben Sie im Dialogfeld **Neuen Task erstellen** im Feld **Öffnen** den Wert **cmd** ein, und [!INCLUDE[clickOK](../../includes/clickok-md.md)].  
  
## <a name="see-also"></a>Siehe auch  
 [Installieren von SQL Server 2016 mithilfe einer Konfigurationsdatei](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md)   
 [Installieren von SQL Server 2016 über die Eingabeaufforderung](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)   
 [Von den SQL Server 2016-Editionen unterstützte Funktionen](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)   
 [Installation von Server Core](http://technet.microsoft.com/windows-server-docs/get-started/getting-started-with-server-core)   
 [Konfigurieren einer Server Core-Installation von Windows Server 2016 R2 mit sconfig.cmd](http://technet.microsoft.com/windows-server-docs/get-started/sconfig-on-ws2016)   
 [Failovercluster-Cmdlets in Windows PowerShell](http://technet.microsoft.com/itpro/powershell/windows/failover-clusters/index)   

  
  



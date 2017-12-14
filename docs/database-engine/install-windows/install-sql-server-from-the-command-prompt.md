---
title: Installieren von SQL Server von der Eingabeaufforderung | Microsoft-Dokumentation
ms.custom: 
ms.date: 09/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: sql
ms.technology: server-general
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- installing SQL Server, command prompt
- installation scripts [SQL Server]
- maintenance scripts [SQL Server]
- REMOVENODE property
- components [SQL Server], removing
- command prompt [SQL Server], SQL Server installations
- ASACCOUNT parameter
- failover clustering [SQL Server], installing
- master database [SQL Server], rebuilding
- SQLCOLLATION parameter
- clusters [SQL Server], installing
- unattended installations [SQL Server]
- modifying collations
- AGTPASSWORD parameter
- USESYSDB parameter
- RSPASSWORD parameter
- AUTOSTART parameter
- ASPASSWORD parameter
- stand-alone installations [SQL Server]
- SAMPLEDATABASESERVER parameter
- adding components
- SAPWD parameter
- scripts [SQL Server], uninstallations
- remote installations [SQL Server]
- components [SQL Server], installing
- TARGETCOMPUTER parameter
- REMOVENODE parameter
- REINSTALLMODE parameter
- scripts [SQL Server], maintenance
- rebuilding registry
- SQLPASSWORD parameter
- rebuilding databases
- IP property
- PIDKEY parameter
- RSCONFIGURATION parameter
- ADDLOCAL parameter
- Setup [SQL Server], command prompt
- REBUILDDATABASE parameter
- SECURITYMODE parameter
- REMOVE property
- DISABLENETWORKPROTOCOLS parameter
- INSTALLDATADIR parameter
- REMOVE parameter
- removing components
- SQLACCOUNT parameter
- parameters [SQL Server], SQL Server installations
- UPGRADE parameter
- shortcuts [SQL Server]
- updating components
- removing SQL Server
- clustered instance of SQL Server
- INSTALLSQLDATADIR parameter
- RSACCOUNT parameter
- ADMINPASSWORD parameter
- GROUP property
- ERRORREPORTING property
- uninstallation scripts [SQL Server]
- AGTACCOUNT parameter
- SAVESYSDB parameter
- INSTALLVS parameter
- INSTANCENAME parameter
- scripts [SQL Server], installations
- rebuilding database, master
- uninstalling SQL Server
- ASCOLLATION parameter
- .ini files
- ADDNODE parameter
- command line installations [SQL Server]
- VS parameter
- INSTALLASDATADIR parameter
- INSTALLSQLDIR parameter
- nodes [Faillover Clustering], command prompt
- INSTALLSQLSHAREDDIR parameter
ms.assetid: df40c888-691c-4962-a420-78a57852364d
caps.latest.revision: "255"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.openlocfilehash: cf7f4a160fe33cad667f1b469ee6178835d0c384
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="install-sql-server-from-the-command-prompt"></a>Installieren von SQL Server von der Eingabeaufforderung
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Bevor Sie die Installation von SQL Server durchführen, lesen Sie das Thema [Planen einer SQL Server-Installation](../../sql-server/install/planning-a-sql-server-installation.md).  
  
 Wenn Sie eine neue Instanz von SQL Server mithilfe der Eingabeaufforderung installieren, können Sie angeben, welche Funktionen installiert und wie diese konfiguriert werden sollen. Sie können auch angeben, ob eine automatische, Standard- oder vollständige Interaktion mit der Setupbenutzeroberfläche erfolgen soll.  
  
> **HINWEIS:** Wenn Sie über die Eingabeaufforderung installieren, unterstützt SQL Server mithilfe des /Q-Parameters den vollständigen stillen Modus oder mithilfe des /QS-Parameters den einfachen stillen Modus. Mithilfe des /QS-Schalters wird nur der Fortschritt angezeigt, es sind jedoch keine Eingaben möglich. Außerdem werden beim Auftreten von Fehlern keine Fehlermeldungen angezeigt. Der /QS-Parameter wird nur unterstützt, wenn /Action=install angegeben wurde.  
  
 Unabhängig von der Installationsmethode ist es erforderlich, dass Sie den Softwarelizenzbedingungen als Einzelperson oder im Auftrag einer juristischen Person zustimmen, sofern die Verwendung der Software in keiner separaten Vereinbarung geregelt ist, z. B. einem Microsoft-Volumenlizenzvertrag oder einem Vertrag eines Drittanbieters mit einem ISV oder OEM.  
  
 Die Lizenzbedingungen werden in der Setup-Benutzeroberfläche angezeigt, damit Sie diese lesen und akzeptieren können. Unbeaufsichtigte Installationen (mit dem /Q-Parameter oder /QS-Parameter) müssen den /IACCEPTSQLSERVERLICENSETERMS-Parameter enthalten. Sie können die Lizenzbedingungen unter [Microsoft-Software-Lizenzbedingungen](http://go.microsoft.com/fwlink/?LinkId=148209)in einer separaten Kopie lesen.  
  
> **HINWEIS:** Abhängig davon, wie Sie die Software erworben haben (z.B. durch Microsoft-Volumenlizenzierung), unterliegt die Verwendung der Software möglicherweise zusätzlichen Bestimmungen.  
  
 Die Installation über die Eingabeaufforderung wird in den folgenden Szenarien unterstützt:  
  
-   Installieren, Aktualisieren oder Entfernen einer Instanz sowie freigegebener Komponenten von SQL Server auf einem lokalen Computer mit der Syntax und den Parametern, die in der Eingabeaufforderung angegeben werden.  
  
-   Installieren, Aktualisieren oder Entfernen einer Failoverclusterinstanz.  
  
-   Upgraden von einer SQL Server-Edition zu einer anderen Edition von SQL Server  
  
-   Installieren einer Instanz von SQL Server auf einem lokalen Computer mithilfe der Syntax und der Parameter, die in einer Konfigurationsdatei angegeben sind. Mit dieser Methode können Sie eine Installationskonfiguration auf mehrere Computer kopieren oder mehrere Knoten einer Failoverclusterinstallation installieren.  
  
 Wenn Sie SQL Server mithilfe der Eingabeaufforderung installieren, geben Sie die Setupparameter für die Installation als Teil der Installationssyntax in der Eingabeaufforderung ein.  
  
> **HINWEIS:** Bei lokalen Installationen müssen Sie das Setup als Administrator ausführen. Wenn Sie SQL Server von einer Remotefreigabe installieren, müssen Sie ein Domänenkonto verwenden, das Lese- und Ausführungsberechtigungen auf der Remotefreigabe hat. Bei Failoverclusterinstallationen müssen Sie lokaler Administrator sein und über Berechtigungen verfügen, sich als Dienst anzumelden und auf allen Failoverclusterknoten als Teil des Betriebssystems zu agieren.  
  
##  <a name="ProperUse"></a> Richtige Verwendung von Setupparametern  
 Entwickeln Sie anhand der folgenden Richtlinien Installationsbefehle mit der richtigen Syntax:  
  
-   /PARAMETER  
  
-   /PARAMETER=true/false  
  
-   /PARAMETER=1/0 für boolesche Typen  
  
-   /PARAMETER="wert" für einwertige Parameter. Es wird die Verwendung doppelter Anführungszeichen empfohlen. Diese sind jedoch nur dann erforderlich, wenn der Wert ein Leerzeichen enthält.  
  
-   /PARAMETER="wert1" "wert2" "wert3" für mehrwertige Parameter. Es wird die Verwendung doppelter Anführungszeichen empfohlen. Diese sind jedoch nur dann erforderlich, wenn der Wert ein Leerzeichen enthält.  
  
 **Ausnahmen:**  
  
-   Der mehrwertige Parameter /FEATURES, dessen Format /FEATURES=AS,RS,IS lautet. Er enthält keine Leerzeichen und ist durch Kommas getrennt.  
  
 **Beispiele:**  
  
-   /INSTANCEDIR=c:\Pfad wird unterstützt.  
  
-   /INSTANCEDIR="c:\Pfad" wird unterstützt.  
  
> [!NOTE]  
>  -   Wenn Sie bei der Installation von SQL Server für INSTANCEDIR und SQLUSERDBDIR denselben Verzeichnispfad angeben, starten der SQL Server-Agent und die Volltextsuche aufgrund fehlender Berechtigungen nicht.  
>   
>      Die relationalen Serverwerte unterstützen die zusätzlichen abschließenden umgekehrten Schrägstrichformate (umgekehrter Schrägstrich oder zwei umgekehrte Schrägstriche) für den Pfad.  
> -   "/PID", der Wert für diesen Parameter sollte in doppelte Anführungszeichen eingeschlossen werden.  
  
## <a name="sql-server-parameters"></a>SQL Server-Parameter  
 In den folgenden Abschnitten finden Sie Parameter, mit denen Befehlszeilen-Installationsskripts für Installations-, Update- und Reparaturszenarien entwickelt werden können.  
  
 Die für eine SQL Server-Komponente aufgeführten Parameter sind für diese Komponente spezifisch. Bei der Installation von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]sind SQL Server-Agent- und SQL Server-Browser-Parameter anwendbar.  
  
-   [Installationsparameter](#Install)  
  
-   [SysPrep-Parameter](#SysPrep)  
  
-   [Upgradeparameter](#Upgrade)  
  
-   [Reparaturparameter](#Repair)  
  
-   [Parameter für die Neuerstellung einer Systemdatenbank](#Rebuild)  
  
-   [Deinstallationsparameter](#Uninstall)  
  
-   [Failoverclusterparameter](#ClusterInstall)  
  
-   [Dienstkontenparameter](#Accounts)  
  
-   [Funktionsparameter](#Feature)  
  
-   [Rollenparameter](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md#RoleParameters)  
  
-   [Steuern des Failoververhaltens mithilfe des Parameters /FAILOVERCLUSTERROLLOWNERSHIP](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md#RollOwnership)  
  
-   [Instanz-ID- oder InstanceID-Konfiguration](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md#InstanceID) 
  
##  <a name="Install"></a> Installationsparameter  
 Entwickeln Sie mit den in der folgenden Tabelle aufgeführten Parametern Befehlszeilenskripts für die Installation.  
  
|SQL Server-Komponente|Parameter|Description|  
|-----------------------------------------|---------------|-----------------|  
|SQL Server-Setupsteuerelement|/ACTION<br /><br /> **Erforderlich**|Erforderlich, um den Installationsworkflow anzugeben.<br /><br /> Unterstützte Werte: **Install**.|  
|SQL Server-Setupsteuerelement|/IACCEPTSQLSERVERLICENSETERMS<br /><br /> **Nur erforderlich, wenn der /Q-Parameter oder der /QS-Parameter für die unbeaufsichtigte Installation angegeben wird.**|Erforderlich, um das Einverständnis mit den Lizenzbedingungen zu erklären.|  
|SQL Server-Setupsteuerelement|/IACCEPTROPENLICENSETERMS <br /><br /> **Nur erforderlich, wenn der Parameter /Q oder /QS für unbeaufsichtigte Installationen angegeben wird, die entweder R-Dienste (in der Datenbank) oder Microsoft R Server einschließen.**|Erforderlich, um das Einverständnis mit den Lizenzbedingungen zu erklären.| 
|SQL Server-Setupsteuerelement|/ENU<br /><br /> **Optional**|Verwenden Sie diesen Parameter, um die englische Version von SQL Server unter einem lokalisierten Betriebssystem zu installieren, wenn die Installationsmedien sowohl Language Packs für Englisch als auch für die Sprache des Betriebssystems enthalten.|  
|SQL Server-Setupsteuerelement|/UpdateEnabled<br /><br /> **Optional**|Geben Sie an, ob das SQL Server-Setup Produktupdates ermitteln und einschließen soll. Gültige Werte sind True und False oder 1 und 0. Standardmäßig schließt das SQL Server-Setup alle gefundenen Updates ein.|  
|SQL Server-Setupsteuerelement|/UpdateSource<br /><br /> **Optional**|Geben Sie an, wo Produktupdates vom SQL Server-Setup abgerufen werden sollen. Gültige Werte sind „MU“ für die Suche in [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update, ein gültiger Ordnerpfad, ein relativer Pfad wie „.\MyUpdates“ oder eine UNC-Freigabe. Das SQL Server-Setup durchsucht standardmäßig [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update oder einen Windows Update-Dienst über Windows Server Update Services.|  
|SQL Server-Setupsteuerelement|/CONFIGURATIONFILE<br /><br /> **Optional**|Gibt die zu verwendende [ConfigurationFile](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md) an.|  
|SQL Server-Setupsteuerelement|/ERRORREPORTING<br /><br /> **Optional**|Hat in SQL Server 2016 keine Auswirkungen. <br/><br/> Informationen dazu, wie Feedback zu Fehlern an Microsoft gesendet wird, finden Sie unter [Konfigurieren von SQL Server 2016 zum Senden von Feedback an Microsoft](http://support.microsoft.com/kb/3153756). <br/><br/>In älteren Versionen wird damit die Fehlerberichterstattung für SQL Server angegeben.<br /><br /> Weitere Informationen finden Sie in den [Datenschutzbestimmungen für den Microsoft-Fehlerberichterstattungsdienst](http://go.microsoft.com/fwlink/?LinkID=72173).<br /><br /> Unterstützte Werte:<br /><br /> 0 = deaktiviert<br /><br /> 1 = aktiviert|  
|SQL Server-Setupsteuerelement|/FEATURES<br /><br /> - Oder -<br /><br /> /ROLE<br /><br /> **Erforderlich**|Gibt die zu installierenden Komponenten an.<br /><br /> Wählen Sie **/FEATURES** aus, um einzelne zu installierende SQL Server-Komponenten anzugeben. Weitere Informationen finden Sie in den [Funktionsparameter](#Feature) .<br /><br /> Wählen Sie **/ROLE** , um eine Setuprolle anzugeben. Durch Setuprollen wird SQL Server in einer vorherbestimmten Konfiguration installiert.|  
|SQL Server-Setupsteuerelement|/HELP, H, ?<br /><br /> **Optional**|Zeigt die Verwendungsoptionen für Installationsparameter an.|  
|SQL Server-Setupsteuerelement|/INDICATEPROGRESS<br /><br /> **Optional**|Gibt an, dass die ausführliche Setupprotokolldatei an die Konsole weitergeleitet wird.|  
|SQL Server-Setupsteuerelement|/INSTALLSHAREDDIR<br /><br /> **Optional**|Gibt ein nicht standardmäßiges Installationsverzeichnis für freigegebene 64-Bit-Komponenten an.<br /><br /> Das Standardverzeichnis lautet „%Program Files%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server“.<br /><br /> Eine Festlegung auf „%Program Files(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server“ ist nicht möglich.|  
|SQL Server-Setupsteuerelement|/INSTALLSHAREDWOWDIR<br /><br /> **Optional**|Gibt ein nicht standardmäßiges Installationsverzeichnis für freigegebene 32-Bit-Komponenten an. Wird nur auf 64-Bit-Systemen unterstützt.<br /><br /> Das Standardverzeichnis lautet „%Program Files(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server“.<br /><br /> Eine Festlegung auf „%Program Files%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server“ ist nicht möglich.|  
|SQL Server-Setupsteuerelement|/INSTANCEDIR<br /><br /> **Optional**|Gibt ein nicht standardmäßiges Installationsverzeichnis für instanzspezifische Komponenten an.|  
|SQL Server-Setupsteuerelement|/INSTANCEID<br /><br /> **Optional**|Gibt einen nicht standardmäßigen Wert für eine [InstanceID](#InstanceID)an.|  
|SQL Server-Setupsteuerelement|/INSTANCENAME<br /><br /> **Erforderlich**|Gibt den Namen einer SQL Server-Instanz an.<br /><br /> Weitere Informationen finden Sie unter [Instance Configuration](http://msdn.microsoft.com/library/5bf822fc-6dec-4806-a153-e200af28e9a5).|  
|PolyBase|/PBENGSVCACCOUNT<br /><br /> **Optional**|Gibt das Konto für den Moduldienst an. Der Standardwert ist **NT Authority\NETWORK SERVICE**.|  
|PolyBase|/PBDMSSVCPASSWORD<br /><br /> **Optional**|Gibt das Kennwort für das Moduldienstkonto an.|  
|PolyBase|/PBENGSVCSTARTUPTYPE<br /><br /> **Optional**|Gibt den Startmodus für den PolyBase-Moduldienst an: Automatisch (Standard), Deaktiviert und Manuell.|  
|PolyBase|/PBPORTRANGE<br /><br /> **Optional**|Gibt einen Portbereich für PolyBase-Dienste mit mindestens sechs Ports an. Beispiel:<br /><br /> `/PBPORTRANGE=16450-16460`|  
|PolyBase|/PBSCALEOUT<br /><br /> **Optional**|Gibt an, ob die SQL Server-Instanz als Teil einer PolyBase-Erweiterungsgruppe aus Computeknoten verwendet wird. Unterstützte Werte: **True**, **False**|  
|SQL Server-Setupsteuerelement|/PID<br /><br /> **Optional**|Gibt den Product Key für die Edition von SQL Server an. Wenn dieser Parameter nicht angegeben wird, wird Evaluation verwendet.|  
|SQL Server-Setupsteuerelement|/Q<br /><br /> **Optional**|Gibt an, dass Setup ohne Benutzeroberfläche in einem stillen Modus ausgeführt wird. Dies wird für unbeaufsichtigte Installationen verwendet.|  
|SQL Server-Setupsteuerelement|/QS<br /><br /> **Optional**|Gibt an, dass Setup ausgeführt wird. Zudem wird der Fortschritt über die Benutzeroberfläche angezeigt. Es ist jedoch keine Eingabe möglich, und es werden keine Fehlermeldungen angezeigt.|  
|SQL Server-Setupsteuerelement|/UIMODE<br /><br /> **Optional**|Gibt an, ob während des Setups nur die Mindestanzahl von Dialogfeldern angezeigt wird.<br /><br /> **/UIMode** kann nur mit dem **/ACTION=INSTALL** -Parameter und dem **UPGRADE** -Parameter angegeben werden. Unterstützte Werte:<br /><br /> **/UIMODE=Normal** ist die Standardeinstellung für andere Editionen als Express-Editionen und zeigt alle Setupdialogfelder für die ausgewählten Funktionen an.<br /><br /> **/UIMODE=AutoAdvance** ist die Standardeinstellung für Express-Editionen und überspringt alle unwesentlichen Dialogfelder.<br /><br /> <br /><br /> Beachten Sie, dass **UIMODE** bei Kombination mit anderen Parametern überschrieben wird. Wenn **/UIMODE=AutoAdvance** und **/ADDCURRENTUSERASSQLADMIN=FALSE** beispielsweise zusammen angegeben werden, wird das bereitstellende Dialogfeld nicht automatisch mit dem Namen des aktuellen Benutzers aufgefüllt.<br /><br /> Die **UIMode** -Einstellung kann nicht mit dem **/Q** -Parameter oder dem **/QS** -Parameter verwendet werden.|  
|SQL Server-Setupsteuerelement|/SQMREPORTING<br /><br /> **Optional**|Hat in SQL Server 2016 keine Auswirkungen. <br/><br/>Informationen dazu, wie Feedback zu Fehlern an Microsoft gesendet wird, finden Sie unter [Konfigurieren von SQL Server 2016 zum Senden von Feedback an Microsoft](http://support.microsoft.com/kb/3153756). <br/><br/>In älteren Versionen wird damit die Erstellung von Funktionsverwendungsberichten für SQL Server angegeben.<br /><br />Unterstützte Werte:<br /><br /> 0 = deaktiviert<br /><br /> 1 = aktiviert|  
|SQL Server-Setupsteuerelement|/HIDECONSOLE<br /><br /> **Optional**|Gibt an, dass das Konsolenfenster ausgeblendet oder geschlossen ist.|  
|SQL Server-Agent|/AGTSVCACCOUNT<br /><br /> **Erforderlich**|Gibt das Konto für den SQL Server-Agent-Dienst an.|  
|SQL Server-Agent|/AGTSVCPASSWORD<br /><br /> [Erforderlich](#Accounts)|Gibt das Kennwort für das SQL Server-Agent-Dienstkonto an.|  
|SQL Server-Agent|/AGTSVCSTARTUPTYPE<br /><br /> **Optional**|Gibt den [Startmodus](#Accounts) für den SQL Server-Agent-Dienst an.<br /><br /> Unterstützte Werte:<br /><br /> **Automatisch**<br /><br /> **Deaktiviert**<br /><br /> **Manuell**|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASBACKUPDIR<br /><br /> **Optional**|Gibt das Verzeichnis für Sicherungsdateien von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] an. Standardwerte:<br /><br /> Für den WOW-Modus auf 64-Bit-Systemen: %Program Files(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Backup<br /><br /> Für alle anderen Installationen: %Program Files%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Backup|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASCOLLATION<br /><br /> **Optional**|Legt die Sortierungseinstellung für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]fest.<br /><br /> Standardwert: **Latin1_General_CI_AS**|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASCONFIGDIR<br /><br /> **Optional**|Gibt das Verzeichnis für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Konfigurationsdateien an. Standardwerte:<br /><br /> Für den WOW-Modus auf 64-Bit-Systemen: %Program Files(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Config<br /><br /> Für alle anderen Installationen: %Program Files%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Config|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASDATADIR<br /><br /> **Optional**|Gibt das Verzeichnis für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datendateien an. Standardwerte:<br /><br /> Für den WOW-Modus auf 64-Bit-Systemen: %Program Files(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Data<br /><br /> Für alle anderen Installationen: %Program Files%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Data|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASLOGDIR<br /><br /> **Optional**|Gibt das Verzeichnis für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Protokolldateien an. Standardwerte:<br /><br /> Für den WOW-Modus auf 64-Bit-Systemen: %Program Files(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Log<br /><br /> Für alle anderen Installationen: %Program Files%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Log|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSERVERMODE<br /><br /> **Optional**|Gibt den Modus der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz an. Gültige Werte sind MULTIDIMENSIONAL, POWERPIVOT oder TABULAR. Bei**ASSERVERMODE** wird die Groß- und Kleinschreibung berücksichtigt. Alle Werte müssen in Großbuchstaben angegeben werden. Weitere Informationen zu gültigen Werten finden Sie unter [Installieren von Analysis Services](../../analysis-services/instances/install-windows/install-analysis-services.md).|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSVCACCOUNT<br /><br /> **Erforderlich**|Gibt das Konto für den [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Dienst an.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSVCPASSWORD<br /><br /> [Erforderlich](#Accounts)|Gibt das Kennwort für den [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Dienst an.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSVCSTARTUPTYPE<br /><br /> **Optional**|Gibt den [Startmodus](#Accounts) für den [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Dienst an. Unterstützte Werte:<br /><br /> **Automatisch**<br /><br /> **Deaktiviert**<br /><br /> **Manuell**|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSYSADMINACCOUNTS<br /><br /> **Erforderlich**|Gibt die Administratoranmeldeinformationen für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]an.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASTEMPDIR<br /><br /> **Optional**|Gibt das Verzeichnis für temporäre [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Dateien an. Standardwerte:<br /><br /> Für den WOW-Modus auf 64-Bit-Systemen: %Program Files(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server \\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Temp<br /><br /> Für alle anderen Installationen: %Program Files%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Temp|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASPROVIDERMSOLAP<br /><br /> **Optional**|Gibt an, ob der MSOLAP-Anbieter innerhalb von Prozessen ausgeführt werden kann.<br /><br /> Standardwert: 1=aktiviert|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/FARMACCOUNT<br /><br /> **Für SPI_AS_NewFarm erforderlich**|Gibt ein Domänenbenutzerkonto zum Ausführen von Diensten der SharePoint-Zentraladministration und anderen wichtigen Diensten in einer Farm an.<br /><br /> Dieser Parameter wird nur für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanzen verwendet, die über /ROLE = SPI_AS_NEWFARM installiert werden.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/FARMPASSWORD<br /><br /> **Für SPI_AS_NewFarm erforderlich**|Gibt ein Kennwort für das Farmkonto an.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/PASSPHRASE<br /><br /> **Für SPI_AS_NewFarm erforderlich**|Gibt eine Passphrase an, die verwendet wird, um einer SharePoint-Farm zusätzliche Anwendungsserver oder Web-Front-End-Server hinzuzufügen.<br /><br /> Dieser Parameter wird nur für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanzen verwendet, die über /ROLE = SPI_AS_NEWFARM installiert werden.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/FARMADMINIPORT<br /><br /> **Für SPI_AS_NewFarm erforderlich**|Gibt einen Port an, der für die Verbindung mit einer Webanwendung für die SharePoint-Zentraladministration verwendet wird.<br /><br /> Dieser Parameter wird nur für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanzen verwendet, die über /ROLE = SPI_AS_NEWFARM installiert werden.|  
|SQL Server-Browser|/BROWSERSVCSTARTUPTYPE<br /><br /> **Optional**|Gibt den [Startmodus](#Accounts) für den SQL Server-Browserdienst an. Unterstützte Werte:<br /><br /> **Automatisch**<br /><br /> **Deaktiviert**<br /><br /> **Manuell**|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/ENABLERANU<br /><br /> **Optional**|Aktiviert die "Ausführen als"-Anmeldeinformationen von [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] -Installationen.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/INSTALLSQLDATADIR<br /><br /> **Optional**|Gibt das Datenverzeichnis für SQL Server-Datendateien an. Standardwerte:<br /><br /> Für den WOW-Modus auf 64-Bit-Systemen: %Program Files(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<br /><br /> Für alle anderen Installationen: %Program Files%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SAPWD<br /><br /> **Erforderlich, wenn /SECURITYMODE=SQL**|Gibt das Kennwort für das Systemadministratorkonto von SQL Server an.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SECURITYMODE<br /><br /> **Optional**|Gibt den Sicherheitsmodus für SQL Server an.<br /><br /> Wenn dieser Parameter nicht angegeben wird, kann die Authentifizierung nur über Windows erfolgen.<br /><br /> Unterstützter Wert: **SQL**|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLBACKUPDIR<br /><br /> **Optional**|Gibt das Verzeichnis für Sicherungsdateien an.<br /><br /> Standardwert: \<InstallSQLDataDir>\ \<SQLInstanceID>\MSSQL\Backup|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLCOLLATION<br /><br /> **Optional**|Legt die Sortierungseinstellungen für SQL Server fest.<br /><br /> Der Standardwert basiert auf dem Gebietsschema des Windows-Betriebssystems. Weitere Informationen finden Sie unter [Sortierungseinstellungen im Setup-Programm](http://msdn.microsoft.com/library/ms143508%28v=sql.105%29.aspx).|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/ADDCURRENTUSERASSQLADMIN<br /><br /> **Optional**|Fügt der festen Serverrolle**sysadmin** von SQL Server den aktuellen Benutzer hinzu. Der /ADDCURRENTUSERASSQLADMIN-Parameter kann beim Installieren von Express-Editionen oder bei Verwendung von /Role=ALLFeatures_WithDefaults eingesetzt werden. Weitere Informationen finden Sie unten unter „/ROLE“.<br /><br /> Die Verwendung von /ADDCURRENTUSERASSQLADMIN ist optional, aber /ADDCURRENTUSERASSQLADMIN oder /SQLSYSADMINACCOUNTS ist erforderlich. Standardwerte:<br /><br /> **True** für Editionen von [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]<br /><br /> **False** für alle anderen Editionen|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCACCOUNT<br /><br /> **Erforderlich**|Gibt das Startkonto für den SQL Server-Dienst an.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCPASSWORD<br /><br /> [Erforderlich](#Accounts)|Gibt das Kennwort für SQLSVCACCOUNT an.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCSTARTUPTYPE<br /><br /> **Optional**|Gibt den [Startmodus](#Accounts) für den SQL Server-Dienst an. Unterstützte Werte:<br /><br /> **Automatisch**<br /><br /> **Deaktiviert**<br /><br /> **Manuell**|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSYSADMINACCOUNTS<br /><br /> **Erforderlich**|Verwenden Sie diesen Parameter, um Anmeldenamen für Mitglieder der sysadmin-Rolle bereitzustellen.<br /><br /> Für andere SQL Server-Editionen als [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]ist /SQLSYSADMINACCOUNTS erforderlich. Für Editionen von [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]ist die Verwendung von /SQLSYSADMINACCOUNTS optional; /SQLSYSADMINACCOUNTS oder /ADDCURRENTUSERASSQLADMIN ist jedoch erforderlich.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBDIR<br /><br /> **Optional**|Gibt die Verzeichnisse für tempdb-Datendateien an. Wenn Sie mehr als ein Verzeichnis angeben, trennen Sie die Verzeichnisse mit einem Leerzeichen. Wenn mehrere Verzeichnisse angegeben sind, werden die tempdb-Datendateien auf die Verzeichnisse im Rahmen eines Roundrobinverfahrens verteilt.<br /><br /> Standardwert: \<InstallSQLDataDir>\ \<SQLInstanceID>\MSSQL\Data(System Data Directory)<br /><br /> HINWEIS: Dieser Parameter wird dem RebuildDatabase-Szenario ebenfalls hinzugefügt.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGDIR<br /><br /> **Optional**|Gibt das Verzeichnis für die tempdb-Protokolldatei an.<br /><br /> Standardwert: \<InstallSQLDataDir>\ \<SQLInstanceID>\MSSQL\Data(System Data Directory)<br /><br /> HINWEIS: Dieser Parameter wird dem RebuildDatabase-Szenario ebenfalls hinzugefügt.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILECOUNT<br /><br /> **Optional**|Gibt die Anzahl von tempdb-Datendateien an, die von Setup hinzugefügt werden sollen. Dieser Wert kann bis zur Anzahl der Kerne heraufgesetzt werden. Standardwert:<br /><br /> 1 für [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]<br /><br /> 8 oder die Anzahl von Kernen, je nachdem, welcher Wert für alle anderen Editionen niedriger ist<br /><br /> **\*\* Wichtig \*\*** Die primäre Datenbankdatei für tempdb ist immer noch „tempdb.mdf“. Die zusätzlichen tempdb-Dateien werden nach dem Muster „tempdb_mssql_#.ndf“ benannt, wobei „#“ eine eindeutige Zahl für jede zusätzliche tempdb-Datenbankdatei darstellt, die beim Setup erstellt wurde. Diese Namenskonvention dient dazu, die Dateinamen eindeutig zu machen. Beim Deinstallieren einer Instanz von SQL Server werden die Dateien gelöscht, die der Namenskonvention „tempdb_mssql_#.ndf“ folgen. Verwenden Sie die Namenskonvention „tempdb_mssql_*.ndf“ nicht für andere Datenbankdateien.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILESIZE<br /><br /> **Optional**|In [!INCLUDE[SQL VERSION](../../includes/sssql15-md.md)] eingeführt. Gibt die Anfangsgröße jeder tempdb-Datendatei an.<br/><br/>Standard = 4 MB für [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], 8 MB für alle anderen Editionen<br/><br/>Min = (4 oder 8 MB)<br/><br/>Max = 1024 MB (262.144 MB für [!INCLUDE[SQL VERSION](../../includes/sssqlv14-md.md)])|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILEGROWTH<br /><br /> **Optional**|Gibt das Dateivergrößerungsinkrement jeder tempdb-Datendatei in MB an. Der Wert 0 zeigt an, dass die automatische Vergrößerung deaktiviert ist und kein zusätzlicher Platz zulässig ist. Das Setup ermöglicht eine Größe von bis zu 1024 MB.<br /><br /> Standardwert: 64 Zulässiger Bereich: Min = 0, Max = 1024|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGFILESIZE<br /><br /> **Optional**|In [!INCLUDE[SQL VERSION](../../includes/sssql15-md.md)] eingeführt. Gibt die Anfangsgröße einer tempdb-Protokolldatei in MB an.<br/><br/>Standard = 4 MB für [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], 8 MB für alle anderen Editionen<br/><br/>Min = (4 oder 8 MB)<br/><br/>Max = 1024 MB (262.144 MB für [!INCLUDE[SQL VERSION](../../includes/sssqlv14-md.md)])|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGFILEGROWTH<br /><br /> **Optional**|Gibt das Dateivergrößerungsinkrement jeder tempdb-Datendatei in MB an. Der Wert 0 zeigt an, dass die automatische Vergrößerung deaktiviert ist und kein zusätzlicher Platz zulässig ist. Das Setup ermöglicht eine Größe von bis zu 1024 MB.<br /><br /> Standardwert: 64 Zulässiger Bereich: Min = 0, Max = 1024|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLUSERDBDIR<br /><br /> **Optional**|Gibt das Verzeichnis für die Datendateien der Benutzerdatenbanken an.<br /><br /> Standardwert: \<InstallSQLDataDir>\ \<SQLInstanceID>\MSSQL\Data|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCINSTANTFILEINIT<br /><br /> **Optional**|Aktiviert die sofortige Dateiinitialisierung für das SQL Server-Dienstkonto. Überlegungen zu Sicherheit und Leistung finden Sie unter [Sofortige Datenbankdateiinitialisierung](../../relational-databases/databases/database-instant-file-initialization.md).<br /><br /> Standardwert: „False“<br /><br /> Optionaler Wert: „True“|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLUSERDBLOGDIR<br /><br /> **Optional**|Gibt das Verzeichnis für die Protokolldateien der Benutzerdatenbanken an.<br /><br /> Standardwert: \<InstallSQLDataDir>\ \<SQLInstanceID>\MSSQL\Data|  
|FILESTREAM|/FILESTREAMLEVEL<br /><br /> **Optional**|Gibt die Zugriffsebene für die FILESTREAM-Funktion an. Unterstützte Werte:<br /><br /> 0 = FILESTREAM-Unterstützung für diese Instanz deaktivieren. (Standardwert)<br /><br /> 1 = FILESTREAM für den [!INCLUDE[tsql](../../includes/tsql-md.md)] -Zugriff aktivieren.<br /><br /> 2 = FILESTREAM für den [!INCLUDE[tsql](../../includes/tsql-md.md)] - und E/A-Streamingzugriff auf Datei aktivieren. (Nicht gültig für Clusterszenarien)<br /><br /> 3 = Streamingzugriff von Remoteclients auf FILESTREAM-Daten zulassen.|  
|FILESTREAM|/FILESTREAMSHARENAME<br /><br /> **Optional**<br /><br /> **Erforderlich, wenn FILESTREAMLEVEL größer als 1 ist.**|Gibt den Namen der Windows-Freigabe an, in der die FILESTREAM-Daten gespeichert werden.|  
|SQL Server-Volltext|/FTSVCACCOUNT<br /><br /> **Optional**|Gibt das Konto für den Volltextfilter-Startprogrammdienst an.<br /><br /> Dieser Parameter wird in [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]ignoriert. Mithilfe der ServiceSID wird die Kommunikation zwischen SQL Server und dem Volltextfilter-Daemon gesichert. Wenn die Werte nicht bereitgestellt werden, wird der Volltextfilter-Startprogrammdienst deaktiviert. Sie müssen den SQL Server-Dienstkontroll-Manager verwenden, um das Dienstkonto zu ändern und die Volltextfunktion zu aktivieren.<br /><br /> Standardwert: Lokales Dienstkonto|  
|SQL Server-Volltext|/FTSVCPASSWORD<br /><br /> **Optional**|Gibt das Kennwort für den Volltextfilter-Startprogrammdienst an.<br /><br /> Dieser Parameter wird in [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]ignoriert.|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCACCOUNT<br /><br /> **Erforderlich**|Gibt das Konto für [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]an.<br /><br /> Der Standardwert ist: „NT Authority\NETWORK SERVICE“.|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCPASSWORD<br /><br /> [Erforderlich](#Accounts)|Gibt das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Kennwort an.|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCStartupType<br /><br /> **Optional**|Gibt den [Startmodus](#Accounts) für den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst an.|  
|SQL Server-Netzwerkkonfiguration|/NPENABLED<br /><br /> **Optional**|Gibt den Status des Named Pipes-Protokolls für den SQL Server-Dienst an. Unterstützte Werte:<br /><br /> 0 = Named Pipes-Protokoll deaktivieren<br /><br /> 1 = Named Pipes-Protokoll aktivieren|  
|SQL Server-Netzwerkkonfiguration|/TCPENABLED<br /><br /> **Optional**|Gibt den Status des TCP-Protokolls für den SQL Server-Dienst an. Unterstützte Werte:<br /><br /> 0 = TCP-Protokoll deaktivieren<br /><br /> 1 = TCP-Protokoll aktivieren|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSINSTALLMODE<br /><br /> **Optional**|Gibt den Installationsmodus für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]an. Unterstützte Werte:<br /><br /> **SharePointFilesOnlyMode**<br /><br /> **DefaultNativeMode**<br /><br /> **FilesOnlyMode**<br /><br /> <br /><br /> Hinweis: Wenn die Installation SQL Server[!INCLUDE[ssDE](../../includes/ssde-md.md)]umfasst, wird RSINSTALLMODE standardmäßig auf DefaultNativeMode festgelegt.<br /><br /> Wenn die Installation SQL Server[!INCLUDE[ssDE](../../includes/ssde-md.md)]nicht umfasst, wird RSINSTALLMODE standardmäßig auf FilesOnlyMode festgelegt.<br /><br /> Wenn Sie DefaultNativeMode auswählen, die Installation jedoch nicht SQL Server[!INCLUDE[ssDE](../../includes/ssde-md.md)]umfasst, wird die RSINSTALLMODE-Einstellung von der Installation automatisch in FilesOnlyMode geändert.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCACCOUNT<br /><br /> **Erforderlich**|Gibt das Startkonto für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]an.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCPASSWORD<br /><br /> [Erforderlich](#Accounts)|Gibt das Kennwort für das Startkonto für den [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienst an.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCStartupType<br /><br /> **Optional**|Gibt den [Startmodus](#Accounts) für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]an.|  
|R Services (In-Database)|MRCACHEDIRECTORY|Verwenden Sie diesen Parameter, um das Cacheverzeichnis für Microsoft R Open und Microsoft R Server-Komponenten wie in [diesem Abschnitt](https://msdn.microsoft.com/library/mt695942.aspx)beschrieben anzugeben. Diese Einstellung wird normalerweise verwendet, wenn Sie SQL Server R Services über die Befehlszeile eines Computers ohne Internetzugriff installieren.|  
  
###### <a name="sample-syntax"></a>Beispielsyntax:  
 So installieren Sie eine neue, eigenständige Instanz mit den Komponenten [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], Replikation und Volltextsuche und aktivieren die schnelle Dateiinitialisierung für [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. 
  
```  
  
Setup.exe /q /ACTION=Install /FEATURES=SQL /INSTANCENAME=MSSQLSERVER /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="<StrongPassword>" /SQLSYSADMINACCOUNTS="<DomainName\UserName>" /AGTSVCACCOUNT="NT AUTHORITY\Network Service" /SQLSVCINSTANTFILEINIT="True" /IACCEPTSQLSERVERLICENSETERMS  
  
```  
  
##  <a name="SysPrep"></a> SysPrep-Parameter  
 Weitere Informationen zu SQL Server SysPrep finden Sie unter  
  
 [Installieren von SQL Server 2016 mit SysPrep](../../database-engine/install-windows/install-sql-server-using-sysprep.md). 
  
#### <a name="prepare-image-parameters"></a>Parameter für die Imagevorbereitung  
 Verwenden Sie die Parameter in der folgenden Tabelle, um Befehlszeilenskripts zur Vorbereitung einer Instanz von SQL Server zu entwickeln, ohne sie zu konfigurieren. 
  
|SQL Server-Komponente|Parameter|Description|  
|-----------------------------------------|---------------|-----------------|  
|SQL Server-Setupsteuerelement|/ACTION<br /><br /> **Erforderlich**|Erforderlich, um den Installationsworkflow anzugeben.<br /><br /> Unterstützte Werte: **PrepareImage**|  
|SQL Server-Setupsteuerelement|/IACCEPTSQLSERVERLICENSETERMS<br /><br /> **Nur erforderlich, wenn der /Q-Parameter oder der /QS-Parameter für die unbeaufsichtigte Installation angegeben wird.**|Erforderlich, um das Einverständnis mit den Lizenzbedingungen zu erklären.|  
|SQL Server-Setupsteuerelement|/ENU<br /><br /> **Optional**|Verwenden Sie diesen Parameter, um die englische Version von SQL Server unter einem lokalisierten Betriebssystem zu installieren, wenn die Installationsmedien sowohl Language Packs für Englisch als auch für die Sprache des Betriebssystems enthalten.|  
|SQL Server-Setupsteuerelement|/UpdateEnabled<br /><br /> **Optional**|Geben Sie an, ob das SQL Server-Setup Produktupdates ermitteln und einschließen soll. Gültige Werte sind True und False oder 1 und 0. Standardmäßig schließt das SQL Server-Setup alle gefundenen Updates ein.|  
|SQL Server-Setupsteuerelement|/UpdateSource<br /><br /> **Optional**|Geben Sie an, wo Produktupdates vom SQL Server-Setup abgerufen werden sollen. Gültige Werte sind „MU“ für die Suche in [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update, ein gültiger Ordnerpfad, ein relativer Pfad wie „.\MyUpdates“ oder eine UNC-Freigabe. Das SQL Server-Setup durchsucht standardmäßig [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update oder einen Windows Update-Dienst über Windows Server Update Services.|  
|SQL Server-Setupsteuerelement|/CONFIGURATIONFILE<br /><br /> **Optional**|Gibt die zu verwendende [ConfigurationFile](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md) an.|  
|SQL Server-Setupsteuerelement|/FEATURES<br /><br /> **Erforderlich**|Gibt zu installierende [Komponenten](#Feature) an.<br /><br /> Unterstützte Werte sind SQLEngine, Replication, FullText, DQ, AS, AS_SPI, RS, RS_SHP, RS_SHPWFE, DQC, Conn, IS, BC, SDK, DREPLAY_CTLR, DREPLAY_CLT, SNAC_SDK, SQLODBC, SQLODBC_SDK, LocalDB, MDS, POLYBASE|  
|SQL Server-Setupsteuerelement|/HELP, H, ?<br /><br /> **Optional**|Zeigt die Verwendungsoptionen für Installationsparameter an.|  
|SQL Server-Setupsteuerelement|/HIDECONSOLE<br /><br /> **Optional**|Gibt an, dass das Konsolenfenster ausgeblendet oder geschlossen ist.|  
|SQL Server-Setupsteuerelement|/INDICATEPROGRESS<br /><br /> **Optional**|Gibt an, dass die ausführliche Setupprotokolldatei an die Konsole weitergeleitet wird.|  
|SQL Server-Setupsteuerelement|/INSTALLSHAREDDIR<br /><br /> **Optional**|Gibt ein nicht standardmäßiges Installationsverzeichnis für freigegebene 64-Bit-Komponenten an.<br /><br /> Das Standardverzeichnis lautet „%Program Files%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server“.<br /><br /> Eine Festlegung auf „%Program Files(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server“ ist nicht möglich.|  
|SQL Server-Setupsteuerelement|/INSTANCEDIR<br /><br /> **Optional**|Gibt ein nicht standardmäßiges Installationsverzeichnis für instanzspezifische Komponenten an.|  
|SQL Server-Setupsteuerelement|/INSTANCEID<br /><br /> Vor dem kumulativen Update 2 (Januar 2013) für [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Service Pack 1 **Erforderlich**<br /><br /> Ab dem kumulativen Update 2 für [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Service Pack 1 **Erforderlich** für Instanzfunktionen.|Gibt eine InstanceID für die Instanz an, die vorbereitet ist.|  
|PolyBase|/PBENGSVCACCOUNT<br /><br /> **Optional**|Gibt das Konto für den Moduldienst an. Der Standardwert ist **NT Authority\NETWORK SERVICE**.|  
|PolyBase|/PBDMSSVCPASSWORD<br /><br /> **Optional**|Gibt das Kennwort für das Moduldienstkonto an.|  
|PolyBase|/PBENGSVCSTARTUPTYPE<br /><br /> **Optional**|Gibt den Startmodus für den PolyBase-Moduldienst an: Automatisch (Standard), Deaktiviert und Manuell.|  
|PolyBase|/PBPORTRANGE<br /><br /> **Optional**|Gibt einen Portbereich für PolyBase-Dienste mit mindestens sechs Ports an. Beispiel:<br /><br /> `/PBPORTRANGE=16450-16460`|  
|PolyBase|/PBSCALEOUT<br /><br /> **Optional**|Gibt an, ob die SQL Server-Instanz als Teil einer PolyBase-Erweiterungsgruppe aus Computeknoten verwendet wird. Unterstützte Werte: **True**, **False**|  
|SQL Server-Setupsteuerelement|/Q<br /><br /> **Optional**|Gibt an, dass Setup ohne Benutzeroberfläche in einem stillen Modus ausgeführt wird. Dies wird für unbeaufsichtigte Installationen verwendet.|  
|SQL Server-Setupsteuerelement|/QS<br /><br /> **Optional**|Gibt an, dass Setup ausgeführt wird. Zudem wird der Fortschritt über die Benutzeroberfläche angezeigt. Es ist jedoch keine Eingabe möglich, und es werden keine Fehlermeldungen angezeigt.|  
  
###### <a name="sample-syntax"></a>Beispielsyntax:  
 So bereiten Sie eine neue eigenständige Instanz mit den Komponenten für [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], die Replikation und die Volltextsuche sowie [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]vor 
  
```  
Setup.exe /q /ACTION=PrepareImage /FEATURES=SQL,RS /InstanceID =<MYINST> /IACCEPTSQLSERVERLICENSETERMS  
```  
  
#### <a name="complete-image-parameters"></a>Parameter für den Imageabschluss  
 Verwenden Sie die Parameter in der folgenden Tabelle, um Befehlszeilenskripts zum Abschließen und Konfigurieren einer vorbereiteten Instanz von SQL Server zu entwickeln. 
  
|SQL Server-Komponente|Parameter|Description|  
|-----------------------------------------|---------------|-----------------|  
|SQL Server-Setupsteuerelement|/ACTION<br /><br /> **Erforderlich**|Erforderlich, um den Installationsworkflow anzugeben.<br /><br /> Unterstützte Werte: **CompleteImage**|  
|SQL Server-Setupsteuerelement|/IACCEPTSQLSERVERLICENSETERMS<br /><br /> **Nur erforderlich, wenn der /Q-Parameter oder der /QS-Parameter für die unbeaufsichtigte Installation angegeben wird.**|Erforderlich, um das Einverständnis mit den Lizenzbedingungen zu erklären.|  
|SQL Server-Setupsteuerelement|/ENU<br /><br /> **Optional**|Verwenden Sie diesen Parameter, um die englische Version von SQL Server unter einem lokalisierten Betriebssystem zu installieren, wenn die Installationsmedien sowohl Language Packs für Englisch als auch für die Sprache des Betriebssystems enthalten.|  
|SQL Server-Setupsteuerelement|/CONFIGURATIONFILE<br /><br /> **Optional**|Gibt die zu verwendende [ConfigurationFile](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md) an.|  
|SQL Server-Setupsteuerelement|/ERRORREPORTING<br /><br /> **Optional**|Hat in SQL Server 2016 keine Auswirkungen. <br/><br/>Informationen dazu, wie Feedback zu Fehlern an Microsoft gesendet wird, finden Sie unter [Konfigurieren von SQL Server 2016 zum Senden von Feedback an Microsoft](http://support.microsoft.com/kb/3153756). <br/><br/>In älteren Versionen wird damit die Fehlerberichterstattung für SQL Server angegeben.<br /><br /> Weitere Informationen finden Sie in den [Datenschutzbestimmungen für den Microsoft-Fehlerberichterstattungsdienst](http://go.microsoft.com/fwlink/?LinkID=72173). Unterstützte Werte:<br /><br /> 1 = aktiviert<br /><br /> 0 = deaktiviert|  
|SQL Server-Setupsteuerelement|/HELP, H, ?<br /><br /> **Optional**|Zeigt die Verwendungsoptionen für Installationsparameter an.|  
|SQL Server-Setupsteuerelement|/INDICATEPROGRESS<br /><br /> **Optional**|Gibt an, dass die ausführliche Setupprotokolldatei an die Konsole weitergeleitet wird.|  
|SQL Server-Setupsteuerelement|/INSTANCEID<br /><br /> Vor dem kumulativen Update 2 (Januar 2013) für [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Service Pack 1 **Erforderlich**<br /><br /> Ab dem kumulativen Update 2 für [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Service Pack 1 **Optional**|Verwenden Sie die Instanz-ID, die während des Schritts zur Imagevorbereitung angegeben wurde.<br /><br /> Unterstützte Werte: InstanceID einer vorbereiteten Instanz.|  
|SQL Server-Setupsteuerelement|/INSTANCENAME<br /><br /> Vor dem kumulativen Update 2 (Januar 2013) für [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Service Pack 1 **Erforderlich**<br /><br /> Ab dem kumulativen Update 2 für [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Service Pack 1 **Optional**|Gibt einen SQL Server-Instanznamen für die Instanz an, die abgeschlossen wird<br /><br /> Weitere Informationen finden Sie unter [Instance Configuration](http://msdn.microsoft.com/library/5bf822fc-6dec-4806-a153-e200af28e9a5).|  
|PolyBase|/PBENGSVCACCOUNT<br /><br /> **Optional**|Gibt das Konto für den Moduldienst an. Der Standardwert ist **NT Authority\NETWORK SERVICE**.|  
|PolyBase|/PBDMSSVCPASSWORD<br /><br /> **Optional**|Gibt das Kennwort für das Moduldienstkonto an.|  
|PolyBase|/PBENGSVCSTARTUPTYPE<br /><br /> **Optional**|Gibt den Startmodus für den PolyBase-Moduldienst an: Automatisch (Standard), Deaktiviert und Manuell.|  
|PolyBase|/PBPORTRANGE<br /><br /> **Optional**|Gibt einen Portbereich für PolyBase-Dienste mit mindestens sechs Ports an. Beispiel:<br /><br /> `/PBPORTRANGE=16450-16460`|  
|PolyBase|/PBSCALEOUT<br /><br /> **Optional**|Gibt an, ob die SQL Server-Instanz als Teil einer PolyBase-Erweiterungsgruppe aus Computeknoten verwendet wird. Unterstützte Werte: **True**, **False**|  
|SQL Server-Setupsteuerelement|/PID<br /><br /> **Optional**|Gibt den Product Key für die Edition von SQL Server an. Wenn dieser Parameter nicht angegeben wird, wird Evaluation verwendet.<br /><br /> Hinweis: Wenn Sie SQL Server Express, SQL Server Express with Tools oder SQL Server Express with Advanced Services installieren, ist die PID vordefiniert.|  
|SQL Server-Setupsteuerelement|/Q<br /><br /> **Optional**|Gibt an, dass Setup ohne Benutzeroberfläche in einem stillen Modus ausgeführt wird. Dies wird für unbeaufsichtigte Installationen verwendet.|  
|SQL Server-Setupsteuerelement|/QS<br /><br /> **Optional**|Gibt an, dass Setup ausgeführt wird. Zudem wird der Fortschritt über die Benutzeroberfläche angezeigt. Es ist jedoch keine Eingabe möglich, und es werden keine Fehlermeldungen angezeigt.|  
|SQL Server-Setupsteuerelement|/SQMREPORTING<br /><br /> **Optional**|Hat in SQL Server 2016 keine Auswirkungen. <br/><br/>Informationen dazu, wie Feedback zu Fehlern an Microsoft gesendet wird, finden Sie unter [Konfigurieren von SQL Server 2016 zum Senden von Feedback an Microsoft](http://support.microsoft.com/kb/3153756). <br/><br/>In älteren Versionen wird damit die Erstellung von Funktionsverwendungsberichten für SQL Server angegeben.<br /><br />Unterstützte Werte:<br /><br /> 0 = deaktiviert<br /><br /> 1 = aktiviert|  
|SQL Server-Setupsteuerelement|/HIDECONSOLE<br /><br /> **Optional**|Gibt an, dass das Konsolenfenster ausgeblendet oder geschlossen ist.|  
|SQL Server-Agent|/AGTSVCACCOUNT<br /><br /> **Erforderlich**|Gibt das Konto für den SQL Server-Agent-Dienst an.|  
|SQL Server-Agent|/AGTSVCPASSWORD<br /><br /> [Erforderlich](#Accounts)|Gibt das Kennwort für das SQL Server-Agent-Dienstkonto an.|  
|SQL Server-Agent|/AGTSVCSTARTUPTYPE<br /><br /> **Optional**|Gibt den [Startmodus](#Accounts) für den SQL Server-Agent-Dienst an. Unterstützte Werte:<br /><br /> **Automatisch**<br /><br /> **Deaktiviert**<br /><br /> **Manuell**|  
|SQL Server-Browser|/BROWSERSVCSTARTUPTYPE<br /><br /> **Optional**|Gibt den [Startmodus](#Accounts) für den SQL Server-Browserdienst an. Unterstützte Werte:<br /><br /> **Automatisch**<br /><br /> **Deaktiviert**<br /><br /> **Manuell**|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/ENABLERANU<br /><br /> **Optional**|Aktiviert „run-as“-Anmeldeinformationen für SQL Server Express-Installationen.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/INSTALLSQLDATADIR<br /><br /> **Optional**|Gibt das Datenverzeichnis für SQL Server-Datendateien an. Standardwerte:<br /><br /> Für den WOW-Modus auf 64-Bit-Systemen: %Program Files(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<br /><br /> Für alle anderen Installationen: %Program Files%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SAPWD<br /><br /> **Erforderlich, wenn /SECURITYMODE=SQL**|Gibt das Kennwort für das Systemadministratorkonto von SQL Server an.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SECURITYMODE<br /><br /> **Optional**|Gibt den Sicherheitsmodus für SQL Server an.<br /><br /> Wenn dieser Parameter nicht angegeben wird, kann die Authentifizierung nur über Windows erfolgen.<br /><br /> Unterstützter Wert: **SQL**|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLBACKUPDIR<br /><br /> **Optional**|Gibt das Verzeichnis für Sicherungsdateien an.<br /><br /> Standardwert:<br /><br /> \<InstallSQLDataDir>\ \<SQLInstanceID>\MSSQL\Backup|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLCOLLATION<br /><br /> **Optional**|Legt die Sortierungseinstellungen für SQL Server fest.<br /><br /> Der Standardwert basiert auf dem Gebietsschema des Windows-Betriebssystems. Weitere Informationen finden Sie unter [Sortierungseinstellungen im Setup-Programm](http://msdn.microsoft.com/library/ms143508%28v=sql.105%29.aspx).|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCACCOUNT<br /><br /> **Erforderlich**|Gibt das Startkonto für den SQL Server-Dienst an.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCPASSWORD<br /><br /> [Erforderlich](#Accounts)|Gibt das Kennwort für SQLSVCACCOUNT an.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCSTARTUPTYPE<br /><br /> **Optional**|Gibt den [Startmodus](#Accounts) für den SQL Server-Dienst an. Unterstützte Werte:<br /><br /> **Automatisch**<br /><br /> **Deaktiviert**<br /><br /> **Manuell**|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSYSADMINACCOUNTS<br /><br /> **Erforderlich**|Verwenden Sie diesen Parameter, um Anmeldenamen für Mitglieder der sysadmin-Rolle bereitzustellen.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBDIR<br /><br /> **Optional**|Gibt die Verzeichnisse für tempdb-Datendateien an. Wenn Sie mehr als ein Verzeichnis angeben, trennen Sie die Verzeichnisse mit einem Leerzeichen. Wenn mehrere Verzeichnisse angegeben sind, werden die tempdb-Datendateien auf die Verzeichnisse im Rahmen eines Roundrobinverfahrens verteilt.<br /><br /> Standardwert: \<InstallSQLDataDir>\ \<SQLInstanceID>\MSSQL\Data(System Data Directory)<br /><br /> HINWEIS: Dieser Parameter wird dem RebuildDatabase-Szenario ebenfalls hinzugefügt.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGDIR<br /><br /> **Optional**|Gibt das Verzeichnis für die tempdb-Protokolldatei an.<br /><br /> Standardwert: \<InstallSQLDataDir>\ \<SQLInstanceID>\MSSQL\Data(System Data Directory)<br /><br /> HINWEIS: Dieser Parameter wird dem RebuildDatabase-Szenario ebenfalls hinzugefügt.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILESIZE<br /><br /> **Optional**|In [!INCLUDE[SQL VERSION](../../includes/sssql15-md.md)] eingeführt. Gibt die Anfangsgröße jeder tempdb-Datendatei an.<br/><br/>Standard = 4 MB für [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], 8 MB für alle anderen Editionen<br/><br/>Min = (4 oder 8 MB)<br/><br/>Max = 1024 MB (262.144 MB für [!INCLUDE[SQL VERSION](../../includes/sssqlv14-md.md)])|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILEGROWTH<br /><br /> **Optional**|Gibt das Dateivergrößerungsinkrement jeder tempdb-Datendatei in MB an. Der Wert 0 zeigt an, dass die automatische Vergrößerung deaktiviert ist und kein zusätzlicher Platz zulässig ist. Das Setup ermöglicht eine Größe von bis zu 1024 MB.<br /><br /> Standardwert: 64<br /><br /> Zulässiger Bereich: Min = 0, Max = 1024|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGFILESIZE<br /><br /> **Optional**|Gibt die Anfangsgröße einer tempdb-Protokolldatei in MB an. Das Setup ermöglicht eine Größe von bis zu 1024 MB.<br /><br /> Standardwert:<br /><br /> 4 für [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]<br /><br /> 8 für alle anderen Editionen<br /><br /> Zulässiger Bereich: Min = Standardwert (4 oder 8), Max = 1024|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGFILEGROWTH<br /><br /> **Optional**|In [!INCLUDE[SQL VERSION](../../includes/sssql15-md.md)] eingeführt. Gibt die Anfangsgröße einer tempdb-Protokolldatei in MB an.<br/><br/>Standard = 4 MB für [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], 8 MB für alle anderen Editionen<br/><br/>Min = (4 oder 8 MB)<br/><br/>Max = 1024 MB (262.144 MB für [!INCLUDE[SQL VERSION](../../includes/sssqlv14-md.md)])|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILECOUNT<br /><br /> **Optional**|Gibt die Anzahl von tempdb-Datendateien an, die von Setup hinzugefügt werden sollen. Dieser Wert kann bis zur Anzahl der Kerne heraufgesetzt werden. Standardwert:<br /><br /> 1 für [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]<br /><br /> 8 oder die Anzahl von Kernen, je nachdem, welcher Wert für alle anderen Editionen niedriger ist<br /><br /> **\*\* Wichtig \*\*** Die primäre Datenbankdatei für tempdb ist immer noch „tempdb.mdf“. Die zusätzlichen tempdb-Dateien werden nach dem Muster „tempdb_mssql_#.ndf“ benannt, wobei „#“ eine eindeutige Zahl für jede zusätzliche tempdb-Datenbankdatei darstellt, die beim Setup erstellt wurde. Diese Namenskonvention dient dazu, die Dateinamen eindeutig zu machen. Beim Deinstallieren einer Instanz von SQL Server werden die Dateien gelöscht, die der Namenskonvention „tempdb_mssql_#.ndf“ folgen. Verwenden Sie die Namenskonvention „tempdb_mssql_\*.ndf“ nicht für andere Datenbankdateien.<br /><br /> **\*\* Warnung \*\*** [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]wird für die Konfiguration dieses Parameters nicht unterstützt. Setup installiert nur 1 Tempdb-Datendatei.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLUSERDBDIR<br /><br /> **Optional**|Gibt das Verzeichnis für die Datendateien der Benutzerdatenbanken an.<br /><br /> Standardwert: \<InstallSQLDataDir>\ \<SQLInstanceID>\MSSQL\Data|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLUSERDBLOGDIR<br /><br /> **Optional**|Gibt das Verzeichnis für die Protokolldateien der Benutzerdatenbanken an.<br /><br /> Standardwert: \<InstallSQLDataDir>\ \<SQLInstanceID>\MSSQL\Data|  
|FILESTREAM|/FILESTREAMLEVEL<br /><br /> **Optional**|Gibt die Zugriffsebene für die FILESTREAM-Funktion an. Unterstützte Werte:<br /><br /> 0 = FILESTREAM-Unterstützung für diese Instanz deaktivieren. (Standardwert)<br /><br /> 1 = FILESTREAM für den [!INCLUDE[tsql](../../includes/tsql-md.md)] -Zugriff aktivieren.<br /><br /> 2 = FILESTREAM für den [!INCLUDE[tsql](../../includes/tsql-md.md)] - und E/A-Streamingzugriff auf Datei aktivieren. (Nicht gültig für Clusterszenarien)<br /><br /> 3 = Streamingzugriff von Remoteclients auf FILESTREAM-Daten zulassen.|  
|FILESTREAM|/FILESTREAMSHARENAME<br /><br /> **Optional**<br /><br /> **Erforderlich, wenn FILESTREAMLEVEL größer als 1 ist.**|Gibt den Namen der Windows-Freigabe an, in der die FILESTREAM-Daten gespeichert werden.|  
|SQL Server-Volltext|/FTSVCACCOUNT<br /><br /> **Optional**|Gibt das Konto für den Volltextfilter-Startprogrammdienst an.<br /><br /> Dieser Parameter wird in [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]ignoriert. Mithilfe der ServiceSID wird die Kommunikation zwischen SQL Server und dem Volltextfilter-Daemon gesichert. Wenn die Werte nicht bereitgestellt werden, wird der Volltextfilter-Startprogrammdienst deaktiviert. Sie müssen den SQL Server-Dienstkontroll-Manager verwenden, um das Dienstkonto zu ändern und die Volltextfunktion zu aktivieren.<br /><br /> Standardwert: Lokales Dienstkonto|  
|SQL Server-Volltext|/FTSVCPASSWORD<br /><br /> **Optional**|Gibt das Kennwort für den Volltextfilter-Startprogrammdienst an.<br /><br /> Dieser Parameter wird in [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]ignoriert.|  
|SQL Server-Netzwerkkonfiguration|/NPENABLED<br /><br /> **Optional**|Gibt den Status des Named Pipes-Protokolls für den SQL Server-Dienst an. Unterstützte Werte:<br /><br /> 0 = Named Pipes-Protokoll deaktivieren<br /><br /> 1 = Named Pipes-Protokoll aktivieren|  
|SQL Server-Netzwerkkonfiguration|/TCPENABLED<br /><br /> **Optional**|Gibt den Status des TCP-Protokolls für den SQL Server-Dienst an. Unterstützte Werte:<br /><br /> 0 = TCP-Protokoll deaktivieren<br /><br /> 1 = TCP-Protokoll aktivieren|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSINSTALLMODE<br /><br /> **Optional**|Gibt den Installationsmodus für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]an.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCACCOUNT<br /><br /> **Erforderlich**|Gibt das Startkonto für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]an.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCPASSWORD<br /><br /> [Erforderlich](#Accounts)|Gibt das Kennwort für das Startkonto für den [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienst an.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCStartupType<br /><br /> **Optional**|Gibt den [Startmodus](#Accounts) für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]an.|  
  
###### <a name="sample-syntax"></a>Beispielsyntax:  
 So schließen Sie eine vorbereitete, eigenständige Instanz ab, die die Komponenten für das [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]-Datenbankmodul, die Replikation und die Volltextsuche einschließt. 
  
```  
  
setup.exe /q /ACTION=CompleteImage /INSTANCENAME=MYNEWINST /INSTANCEID=<MYINST> /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="<StrongPassword>" /SQLSYSADMINACCOUNTS="<DomainName\UserName>" /AGTSVCACCOUNT="NT AUTHORITY\Network Service" /IACCEPTSQLSERVERLICENSETERMS  
  
```  
  
##  <a name="Upgrade"></a> Upgradeparameter  
 Entwickeln Sie mit den in der folgenden Tabelle aufgeführten Parametern Befehlszeilenskripts für Upgrades. 
  
|SQL Server-Komponente|Parameter|Description|  
|-----------------------------------------|---------------|-----------------|  
|SQL Server-Setupsteuerelement|/ACTION<br /><br /> **Erforderlich**|Erforderlich, um den Installationsworkflow anzugeben. Unterstützte Werte:<br /><br /> **Upgrade**<br /><br /> **EditionUpgrade**<br /><br /> <br /><br /> Der **EditionUpgrade** -Wert wird verwendet, um für eine vorhandene Edition von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ein Upgrade auf eine andere Edition auszuführen. Weitere Informationen zu unterstützten Versions- und Editionsupgrades finden Sie unter [Supported Version and Edition Upgrades](../../database-engine/install-windows/supported-version-and-edition-upgrades.md).|  
|SQL Server-Setupsteuerelement|/IACCEPTSQLSERVERLICENSETERMS<br /><br /> **Nur erforderlich, wenn der /Q-Parameter oder der /QS-Parameter für die unbeaufsichtigte Installation angegeben wird.**|Erforderlich, um das Einverständnis mit den Lizenzbedingungen zu erklären.|  
|SQL Server-Setupsteuerelement|/ENU<br /><br /> **Optional**|Verwenden Sie diesen Parameter, um die englische Version von SQL Server unter einem lokalisierten Betriebssystem zu installieren, wenn die Installationsmedien sowohl Language Packs für Englisch als auch für die Sprache des Betriebssystems enthalten.|  
|SQL Server-Setupsteuerelement|/*UpdateEnabled*<br /><br /> **Optional**|Geben Sie an, ob das SQL Server-Setup Produktupdates ermitteln und einschließen soll. Gültige Werte sind True und False oder 1 und 0. Standardmäßig schließt das SQL Server-Setup alle gefundenen Updates ein.|  
|SQL Server-Setupsteuerelement|/*UpdateSource*<br /><br /> **Optional**|Geben Sie an, wo Produktupdates vom SQL Server-Setup abgerufen werden sollen. Gültige Werte sind „MU“ für die Suche in [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update, ein gültiger Ordnerpfad, ein relativer Pfad wie „.\MyUpdates“ oder eine UNC-Freigabe. Das SQL Server-Setup durchsucht standardmäßig [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update oder einen Windows Update-Dienst über Windows Server Update Services.|  
|SQL Server-Setupsteuerelement|/CONFIGURATIONFILE<br /><br /> **Optional**|Gibt die zu verwendende [ConfigurationFile](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md) an.|  
|SQL Server-Setupsteuerelement|/ERRORREPORTING<br /><br /> **Optional**|Hat in SQL Server 2016 keine Auswirkungen. <br/><br/>Informationen dazu, wie Feedback zu Fehlern an Microsoft gesendet wird, finden Sie unter [Konfigurieren von SQL Server 2016 zum Senden von Feedback an Microsoft](http://support.microsoft.com/kb/3153756). <br/><br/>In älteren Versionen wird damit die Fehlerberichterstattung für SQL Server angegeben.<br /><br /> Weitere Informationen finden Sie in den [Datenschutzbestimmungen für den Microsoft-Fehlerberichterstattungsdienst](http://go.microsoft.com/fwlink/?LinkID=72173). Unterstützte Werte:<br /><br /> 1 = aktiviert<br /><br /> 0 = deaktiviert|  
|SQL Server-Setupsteuerelement|/HELP, H, ?<br /><br /> **Optional**|Zeigt die Verwendungsoptionen für die Parameter an.|  
|SQL Server-Setupsteuerelement|/INDICATEPROGRESS<br /><br /> **Optional**|Gibt an, dass die ausführliche Setupprotokolldatei an die Konsole weitergeleitet wird.|  
|SQL Server-Setupsteuerelement|/ INSTANCEDIR<br /><br /> **Optional**|Gibt ein nicht standardmäßiges Installationsverzeichnis für freigegebene Komponenten an.|  
|SQL Server-Setupsteuerelement|/INSTANCEID<br /><br /> **Erforderlich für Upgrades von [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]** oder höher aktualisieren.<br /><br /> **Optional für das Upgrade von [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]**|Gibt einen nicht standardmäßigen Wert für eine [InstanceID](#InstanceID)an.|  
|SQL Server-Setupsteuerelement|/INSTANCENAME<br /><br /> **Erforderlich**|Gibt den Namen einer SQL Server-Instanz an.<br /><br /> Weitere Informationen finden Sie unter [Instance Configuration](http://msdn.microsoft.com/library/5bf822fc-6dec-4806-a153-e200af28e9a5).|  
|SQL Server-Setupsteuerelement|/PID<br /><br /> **Optional**|Gibt den Product Key für die Edition von SQL Server an. Wenn dieser Parameter nicht angegeben wird, wird Evaluation verwendet.|  
|SQL Server-Setupsteuerelement|/Q<br /><br /> **Optional**|Gibt an, dass Setup ohne Benutzeroberfläche in einem stillen Modus ausgeführt wird. Dies wird für unbeaufsichtigte Installationen verwendet.|  
|SQL Server-Setupsteuerelement|/UIMODE<br /><br /> **Optional**|Gibt an, ob während des Setups nur die Mindestanzahl von Dialogfeldern angezeigt wird. <br />                **/UIMode** kann nur mit dem **/ACTION=INSTALL** -Parameter und dem **UPGRADE** -Parameter angegeben werden. Unterstützte Werte:<br /><br /> **/UIMODE=Normal** ist die Standardeinstellung für andere Editionen als Express-Editionen und zeigt alle Setupdialogfelder für die ausgewählten Funktionen an.<br /><br /> **/UIMODE=AutoAdvance** ist die Standardeinstellung für Express-Editionen und überspringt alle unwesentlichen Dialogfelder.<br /><br /> Beachten Sie, dass die **UIMode** -Einstellung nicht mit dem **/Q** -Parameter oder dem **/QS** -Parameter verwendet werden kann.|  
|SQL Server-Setupsteuerelement|/SQMREPORTING<br /><br /> **Optional**|Hat in SQL Server 2016 keine Auswirkungen. <br/><br/>Informationen dazu, wie Feedback zu Fehlern an Microsoft gesendet wird, finden Sie unter [Konfigurieren von SQL Server 2016 zum Senden von Feedback an Microsoft](http://support.microsoft.com/kb/3153756). <br/><br/>In älteren Versionen wird damit die Erstellung von Funktionsverwendungsberichten für SQL Server angegeben.<br /><br />Unterstützte Werte:<br /><br /> 1 = aktiviert<br /><br /> 0 = deaktiviert|  
|SQL Server-Setupsteuerelement|/HIDECONSOLE<br /><br /> **Optional**|Gibt an, dass das Konsolenfenster ausgeblendet oder geschlossen ist.|  
|SQL Server-Browserdienst|/BROWSERSVCSTARTUPTYPE<br /><br /> **Optional**|Gibt den [Startmodus](#Accounts) für den SQL Server-Browserdienst an. Unterstützte Werte:<br /><br /> **Automatisch**<br /><br /> **Deaktiviert**<br /><br /> **Manuell**|  
|SQL Server-Volltext|/FTUPGRADEOPTION<br /><br /> **Optional**|Gibt die Upgradeoption für den Volltextkatalog an. Unterstützte Werte:<br /><br /> **REBUILD**<br /><br /> **RESET**<br /><br /> **IMPORT**|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCACCOUNT<br /><br /> **Erforderlich**|Gibt das Konto für [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]an.<br /><br /> Der Standardwert ist: „NT Authority\NETWORK SERVICE“.|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCPASSWORD<br /><br /> [Erforderlich](#Accounts)|Gibt das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Kennwort an.|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCStartupType<br /><br /> **Optional**|Gibt den [Startmodus](#Accounts) für den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst an.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSUPGRADEDATABASEACCOUNT<br /><br /> **Optional**|Die Eigenschaft wird nur verwendet, wenn ein Upgrade eines Berichtsserver im SharePoint-Modus der Version 2008 R2 oder früher ausgeführt wird. Weitere Upgradevorgänge werden für Berichtsserver ausgeführt, die die ältere Architektur des SharePoint-Modus verwenden, die in SQL Server 2012 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]geändert wurde. Wenn diese Option in der Befehlszeileninstallation nicht eingeschlossen ist, wird das Standarddienstkonto für die alte Instanz des Berichtsservers verwendet. Wenn diese Eigenschaft verwendet wird, geben Sie mithilfe der **/RSUPGRADEPASSWORD** -Eigenschaft das Kennwort für das Konto an.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSUPGRADEPASSWORD<br /><br /> **Optional**|Kennwort des vorhandenen Berichtsserver-Dienstkontos.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/ALLOWUPGRADEFORSSRSSHAREPOINTMODE|Der Schalter ist erforderlich, wenn Sie eine Installation des SharePoint-Modus aktualisieren, die auf der Architektur für den gemeinsamen SharePoint-Dienst basiert. Der Schalter wird nicht benötigt, um nicht freigegebene Dienstversionen von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]zu aktualisieren.|  
  
###### <a name="sample-syntax"></a>Beispielsyntax:  
 So upgraden Sie eine vorhandene Instanz oder einen Failoverclusterknoten von einer früheren SQL Server-Version  
  
```  
Setup.exe /q /ACTION=upgrade /INSTANCEID = <INSTANCEID>/INSTANCENAME=MSSQLSERVER /RSUPGRADEDATABASEACCOUNT="<Provide a SQL Server logon account that can connect to the report server during upgrade>" /RSUPGRADEPASSWORD="<Provide a password for the report server upgrade account>" /ISSVCAccount="NT Authority\Network Service" /IACCEPTSQLSERVERLICENSETERMS  
```  
  
##  <a name="Repair"></a> Reparaturparameter  
 Entwickeln Sie mit den in der folgenden Tabelle aufgeführten Parametern Befehlszeilenskripts für die Reparatur. 
  
|SQL Server-Komponente|Parameter|Description|  
|-----------------------------------------|---------------|-----------------|  
|SQL Server-Setupsteuerelement|/ACTION<br /><br /> **Erforderlich**|Erforderlich, um den Reparaturworkflow anzugeben.<br /><br /> Unterstützte Werte: **Repair**|  
|SQL Server-Setupsteuerelement|/ENU<br /><br /> **Optional**|Verwenden Sie diesen Parameter, um die englische Version von SQL Server unter einem lokalisierten Betriebssystem zu installieren, wenn die Installationsmedien sowohl Language Packs für Englisch als auch für die Sprache des Betriebssystems enthalten.|  
|SQL Server-Setupsteuerelement|/FEATURES<br /><br /> **Erforderlich**|Gibt die [Komponenten](#Feature) für die Reparatur an.|  
|SQL Server-Setupsteuerelement|/INSTANCENAME<br /><br /> **Erforderlich**|Gibt den Namen einer SQL Server-Instanz an.<br /><br /> Weitere Informationen finden Sie unter [Instance Configuration](http://msdn.microsoft.com/library/5bf822fc-6dec-4806-a153-e200af28e9a5).|  
|PolyBase|/PBENGSVCACCOUNT<br /><br /> **Optional**|Gibt das Konto für den Moduldienst an. Der Standardwert ist **NT Authority\NETWORK SERVICE**.|  
|PolyBase|/PBDMSSVCPASSWORD<br /><br /> **Optional**|Gibt das Kennwort für das Moduldienstkonto an.|  
|PolyBase|/PBENGSVCSTARTUPTYPE<br /><br /> **Optional**|Gibt den Startmodus für den PolyBase-Moduldienst an: Automatisch (Standard), Deaktiviert und Manuell.|  
|PolyBase|/PBPORTRANGE<br /><br /> **Optional**|Gibt einen Portbereich für PolyBase-Dienste mit mindestens sechs Ports an. Beispiel:<br /><br /> `/PBPORTRANGE=16450-16460`|  
|PolyBase|/PBSCALEOUT<br /><br /> **Optional**|Gibt an, ob die SQL Server-Instanz als Teil einer PolyBase-Erweiterungsgruppe aus Computeknoten verwendet wird. Unterstützte Werte: **True**, **False**|  
|SQL Server-Setupsteuerelement|/Q<br /><br /> **Optional**|Gibt an, dass Setup ohne Benutzeroberfläche in einem stillen Modus ausgeführt wird. Dies wird für unbeaufsichtigte Installationen verwendet.|  
|SQL Server-Setupsteuerelement|/HIDECONSOLE<br /><br /> **Optional**|Gibt an, dass das Konsolenfenster ausgeblendet oder geschlossen ist.|  
  
###### <a name="sample-syntax"></a>Beispielsyntax:  
 Reparieren einer Instanz und von freigegebenen Komponenten. 
  
```  
Setup.exe /q /ACTION=Repair /INSTANCENAME=<instancename>  
```  
  
##  <a name="Rebuild"></a> Parameter für die Neuerstellung einer Systemdatenbank  
 Verwenden Sie die in der folgenden Tabelle aufgeführten Parameter, um Befehlszeilenskripts zur Neuerstellung der Systemdatenbanken master, model, msdb und tempdb zu entwickeln. Weitere Informationen finden Sie unter [Neuerstellen von Systemdatenbanken](../../relational-databases/databases/rebuild-system-databases.md). 
  
|SQL Server-Komponente|Parameter|Description|  
|-----------------------------------------|---------------|-----------------|  
|SQL Server-Setupsteuerelement|/ACTION<br /><br /> **Erforderlich**|Erforderlich, um den Workflow für das erneute Erstellen der Datenbank anzugeben.<br /><br /> Unterstützte Werte: **Rebuilddatabase**|  
|SQL Server-Setupsteuerelement|/INSTANCENAME<br /><br /> **Erforderlich**|Gibt den Namen einer SQL Server-Instanz an.<br /><br /> Weitere Informationen finden Sie unter [Instance Configuration](http://msdn.microsoft.com/library/5bf822fc-6dec-4806-a153-e200af28e9a5).|  
|SQL Server-Setupsteuerelement|/Q<br /><br /> **Optional**|Gibt an, dass Setup ohne Benutzeroberfläche in einem stillen Modus ausgeführt wird. Dies wird für unbeaufsichtigte Installationen verwendet.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLCOLLATION<br /><br /> **Optional**|Gibt eine neue Sortierung auf Serverebene an.<br /><br /> Der Standardwert basiert auf dem Gebietsschema des Windows-Betriebssystems. Weitere Informationen finden Sie unter [Sortierungseinstellungen im Setup-Programm](http://msdn.microsoft.com/library/ms143508%28v=sql.105%29.aspx).|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SAPWD<br /><br /> **Erforderlich, wenn bei der Installation der Instanz /SECURITYMODE=SQL angegeben wurde.**|Gibt das Kennwort für das SQL-SA-Konto an.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSYSADMINACCOUNTS<br /><br /> **Erforderlich**|Verwenden Sie diesen Parameter, um Anmeldenamen für Mitglieder der sysadmin-Rolle bereitzustellen.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBDIR<br /><br /> **Optional**|Gibt die Verzeichnisse für tempdb-Datendateien an. Wenn Sie mehr als ein Verzeichnis angeben, trennen Sie die Verzeichnisse mit einem Leerzeichen. Wenn mehrere Verzeichnisse angegeben sind, werden die tempdb-Datendateien auf die Verzeichnisse im Rahmen eines Roundrobinverfahrens verteilt.<br /><br /> Standardwert: \<InstallSQLDataDir>\ \<SQLInstanceID>\MSSQL\Data(System Data Directory)<br /><br /> HINWEIS: Dieser Parameter wird dem RebuildDatabase-Szenario ebenfalls hinzugefügt.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGDIR<br /><br /> **Optional**|Gibt das Verzeichnis für die tempdb-Protokolldatei an.<br /><br /> Standardwert: \<InstallSQLDataDir>\ \<SQLInstanceID>\MSSQL\Data(System Data Directory)<br /><br /> HINWEIS: Dieser Parameter wird dem RebuildDatabase-Szenario ebenfalls hinzugefügt.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILECOUNT<br /><br /> **Optional**|Gibt die Anzahl von tempdb-Datendateien an, die von Setup hinzugefügt werden sollen. Dieser Wert kann bis zur Anzahl der Kerne heraufgesetzt werden. Standardwert:<br /><br /> 1 für [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]<br /><br /> 8 oder die Anzahl von Kernen, je nachdem, welcher Wert für alle anderen Editionen niedriger ist<br /><br /> **\*\* Wichtig \*\*** Die primäre Datenbankdatei für tempdb ist immer noch „tempdb.mdf“. Die zusätzlichen tempdb-Dateien werden nach dem Muster „tempdb_mssql_#.ndf“ benannt, wobei „#“ eine eindeutige Zahl für jede zusätzliche tempdb-Datenbankdatei darstellt, die beim Setup erstellt wurde. Diese Namenskonvention dient dazu, die Dateinamen eindeutig zu machen. Beim Deinstallieren einer Instanz von SQL Server werden die Dateien gelöscht, die der Namenskonvention „tempdb_mssql_#.ndf“ folgen. Verwenden Sie die Namenskonvention „tempdb_mssql_\*.ndf“ nicht für andere Datenbankdateien.<br /><br /> **\*\* Warnung \*\*** [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]wird für die Konfiguration dieses Parameters nicht unterstützt. Setup installiert nur 1 Tempdb-Datendatei.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILESIZE<br /><br /> **Optional**|In [!INCLUDE[SQL VERSION](../../includes/sssql15-md.md)] eingeführt. Gibt die Anfangsgröße jeder tempdb-Datendatei an.<br/><br/>Standard = 4 MB für [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], 8 MB für alle anderen Editionen<br/><br/>Min = (4 oder 8 MB)<br/><br/>Max = 1024 MB (262.144 MB für [!INCLUDE[SQL VERSION](../../includes/sssqlv14-md.md)])|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILEGROWTH<br /><br /> **Optional**|Gibt das Dateivergrößerungsinkrement jeder tempdb-Datendatei in MB an. Der Wert 0 zeigt an, dass die automatische Vergrößerung deaktiviert ist und kein zusätzlicher Platz zulässig ist. Das Setup ermöglicht eine Größe von bis zu 1024 MB.<br /><br /> Standardwert: 64<br /><br /> Zulässiger Bereich: Min = 0, Max = 1024|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGFILESIZE<br /><br /> **Optional**|Gibt die Anfangsgröße einer tempdb-Protokolldatei in MB an. Das Setup ermöglicht eine Größe von bis zu 1024 MB. Standardwert:<br /><br /> 4 für [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]<br /><br /> 8 für alle anderen Editionen<br /><br /> Zulässiger Bereich: Min = Standardwert (4 oder 8), Max = 1024|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGFILEGROWTH<br /><br /> **Optional**|In [!INCLUDE[SQL VERSION](../../includes/sssql15-md.md)] eingeführt. Gibt die Anfangsgröße einer tempdb-Protokolldatei in MB an.<br/><br/>Standard = 4 MB für [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], 8 MB für alle anderen Editionen<br/><br/>Min = (4 oder 8 MB)<br/><br/>Max = 1024 MB (262.144 MB für [!INCLUDE[SQL VERSION](../../includes/sssqlv14-md.md)])|  
  
##  <a name="Uninstall"></a> Deinstallationsparameter  
 Entwickeln Sie mit den in der folgenden Tabelle aufgeführten Parametern Befehlszeilenskripts für die Deinstallation. 
  
|SQL Server-Komponente|Parameter|Description|  
|-----------------------------------------|---------------|-----------------|  
|SQL Server-Setupsteuerelement|/ACTION<br /><br /> **Erforderlich**|Erforderlich, um den Deinstallationsworkflow anzugeben.<br /><br /> Unterstützte Werte: **Uninstall**|  
|SQL Server-Setupsteuerelement|/CONFIGURATIONFILE<br /><br /> **Optional**|Gibt die zu verwendende [ConfigurationFile](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md) an.|  
|SQL Server-Setupsteuerelement|/FEATURES<br /><br /> **Erforderlich**|Gibt zu deinstallierende [Komponenten](#Feature) an.|  
|SQL Server-Setupsteuerelement|/HELP, H, ?<br /><br /> **Optional**|Zeigt die Verwendungsoptionen für die Parameter an.|  
|SQL Server-Setupsteuerelement|/INDICATEPROGRESS<br /><br /> **Optional**|Gibt an, dass die ausführliche Setupprotokolldatei an die Konsole weitergeleitet wird.|  
|SQL Server-Setupsteuerelement|/INSTANCENAME<br /><br /> **Erforderlich**|Gibt den Namen einer SQL Server-Instanz an.<br /><br /> Weitere Informationen finden Sie unter [Instance Configuration](http://msdn.microsoft.com/library/5bf822fc-6dec-4806-a153-e200af28e9a5).|  
|SQL Server-Setupsteuerelement|/Q<br /><br /> **Optional**|Gibt an, dass Setup ohne Benutzeroberfläche in einem stillen Modus ausgeführt wird. Dies wird für unbeaufsichtigte Installationen verwendet.|  
|SQL Server-Setupsteuerelement|/HIDECONSOLE<br /><br /> **Optional**|Gibt an, dass das Konsolenfenster ausgeblendet oder geschlossen ist.|  
  
###### <a name="sample-syntax"></a>Beispielsyntax:  
 So deinstallieren Sie eine vorhandene Instanz von SQL Server 
  
```  
Setup.exe /Action=Uninstall /FEATURES=SQL,AS,RS,IS,Tools /INSTANCENAME=MSSQLSERVER  
```  
  
 Um eine benannte Instanz zu entfernen, geben Sie in dem weiter oben genannten Beispiel anstelle von "MSSQLSERVER" den Namen der Instanz an. 
  
##  <a name="ClusterInstall"></a> Failoverclusterparameter  
 Lesen Sie vor dem Installieren einer SQL Server-Failoverclusterinstanz die folgenden Themen:  
  
-   [Hardware- und Softwareanforderungen für die Installation von SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
  
-   [[Überlegungen zur Sicherheit bei SQL Server-Installationen](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)]
  
-   [Vor dem Installieren des Failoverclusterings](../../sql-server/failover-clusters/install/before-installing-failover-clustering.md)  
  
-   [Always On-Failoverclusterinstanzen &#40;SQL Server&#41;](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)  
  
    > [!IMPORTANT]  
    >  Allen Installationsbefehlen für Failovercluster muss ein Windows-Cluster zugrunde liegen. Alle Knoten, die Teil eines SQL Server-Failoverclusters sind, müssen auch Teil desselben Windows-Clusters sein. 
  
 Testen Sie die folgenden Installationsskripts für Failovercluster, und ändern Sie diese so, dass sie den Anforderungen Ihrer Organisation entsprechen. 
  
#### <a name="integrated-install-failover-cluster-parameters"></a>Parameter für integrierte Failoverclusterinstallationen  
 Entwickeln Sie mit den in der folgenden Tabelle aufgeführten Parametern Befehlszeilenskripts für die Failoverclusterinstallation. 
  
 Weitere Informationen zur integrierten Installation finden Sie unter [Always On-Failoverclusterinstanzen &#40;SQL Server&#41;](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md). 
  
> **HINWEIS:** Um nach der Installation zusätzliche Knoten hinzuzufügen, verwenden Sie die Aktion [AddNode](#AddNode). 
  
|SQL Server-Komponente|Parameter|Details|  
|-----------------------------------------|---------------|-------------|  
|SQL Server-Setupsteuerelement|/ACTION<br /><br /> **Erforderlich**|Erforderlich, um den Installationsworkflow des Failoverclusters anzugeben.<br /><br /> Unterstützter Wert: **InstallFailoverCluster**|  
|SQL Server-Setupsteuerelement|/IACCEPTSQLSERVERLICENSETERMS<br /><br /> **Nur erforderlich, wenn der /Q-Parameter oder der /QS-Parameter für die unbeaufsichtigte Installation angegeben wird.**|Erforderlich, um das Einverständnis mit den Lizenzbedingungen zu erklären.|  
|SQL Server-Setupsteuerelement|/ENU<br /><br /> **Optional**|Verwenden Sie diesen Parameter, um die englische Version von SQL Server unter einem lokalisierten Betriebssystem zu installieren, wenn die Installationsmedien sowohl Language Packs für Englisch als auch für die Sprache des Betriebssystems enthalten.|  
|SQL Server-Setupsteuerelement|/FAILOVERCLUSTERGROUP<br /><br /> **Optional**|Gibt den Namen der Ressourcengruppe an, die für den SQL Server-Failovercluster verwendet werden soll. Es kann sich um den Namen einer vorhandenen Clustergruppe oder den Namen einer neuen Ressourcengruppe handeln.<br /><br /> Standardwert:<br /><br /> SQL Server (\<Instanzname>)|  
|PolyBase|/PBENGSVCACCOUNT<br /><br /> **Optional**|Gibt das Konto für den Moduldienst an. Der Standardwert ist **NT Authority\NETWORK SERVICE**.|  
|PolyBase|/PBDMSSVCPASSWORD<br /><br /> **Optional**|Gibt das Kennwort für das Moduldienstkonto an.|  
|PolyBase|/PBENGSVCSTARTUPTYPE<br /><br /> **Optional**|Gibt den Startmodus für den PolyBase-Moduldienst an: Automatisch (Standard), Deaktiviert und Manuell.|  
|PolyBase|/PBPORTRANGE<br /><br /> **Optional**|Gibt einen Portbereich für PolyBase-Dienste mit mindestens sechs Ports an. Beispiel:<br /><br /> `/PBPORTRANGE=16450-16460`|  
|PolyBase|/PBSCALEOUT<br /><br /> **Optional**|Gibt an, ob die SQL Server-Instanz als Teil einer PolyBase-Erweiterungsgruppe aus Computeknoten verwendet wird. Unterstützte Werte: **True**, **False**|  
|SQL Server-Setupsteuerelement|/*UpdateEnabled*<br /><br /> **Optional**|Geben Sie an, ob das SQL Server-Setup Produktupdates ermitteln und einschließen soll. Gültige Werte sind True und False oder 1 und 0. Standardmäßig schließt das SQL Server-Setup alle gefundenen Updates ein.|  
|SQL Server-Setupsteuerelement|/*UpdateSource*<br /><br /> **Optional**|Geben Sie an, wo Produktupdates vom SQL Server-Setup abgerufen werden sollen. Gültige Werte sind „MU“ für die Suche in [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update, ein gültiger Ordnerpfad, ein relativer Pfad wie „.\MyUpdates“ oder eine UNC-Freigabe. Das SQL Server-Setup durchsucht standardmäßig [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update oder einen Windows Update-Dienst über Windows Server Update Services.|  
|SQL Server-Setupsteuerelement|/CONFIGURATIONFILE<br /><br /> **Optional**|Gibt die zu verwendende [ConfigurationFile](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md) an.|  
|SQL Server-Setupsteuerelement|/ERRORREPORTING<br /><br /> **Optional**|Hat in SQL Server 2016 keine Auswirkungen. <br/><br/>Informationen dazu, wie Feedback zu Fehlern an Microsoft gesendet wird, finden Sie unter [Konfigurieren von SQL Server 2016 zum Senden von Feedback an Microsoft](http://support.microsoft.com/kb/3153756). <br/><br/>In älteren Versionen wird damit die Fehlerberichterstattung für SQL Server angegeben.<br /><br /> Weitere Informationen finden Sie in den [Datenschutzbestimmungen für den Microsoft-Fehlerberichterstattungsdienst](http://go.microsoft.com/fwlink/?LinkID=72173). Unterstützte Werte:<br /><br /> 1 = aktiviert<br /><br /> 0 = deaktiviert|  
|SQL Server-Setupsteuerelement|/FEATURES<br /><br /> **Erforderlich**|Gibt zu installierende [Komponenten](#Feature) an.|  
|SQL Server-Setupsteuerelement|/HELP, H, ?<br /><br /> **Optional**|Zeigt die Verwendungsoptionen für die Parameter an.|  
|SQL Server-Setupsteuerelement|/INDICATEPROGRESS<br /><br /> **Optional**|Gibt an, dass die ausführliche Setupprotokolldatei an die Konsole weitergeleitet wird.|  
|SQL Server-Setupsteuerelement|/INSTALLSHAREDDIR<br /><br /> **Optional**|Gibt ein nicht standardmäßiges Installationsverzeichnis für freigegebene 64-Bit-Komponenten an.<br /><br /> Das Standardverzeichnis lautet „%Program Files%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server“.<br /><br /> Eine Festlegung auf „%Program Files(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server“ ist nicht möglich.|  
|SQL Server-Setupsteuerelement|/INSTALLSHAREDWOWDIR<br /><br /> **Optional**|Gibt ein nicht standardmäßiges Installationsverzeichnis für freigegebene 32-Bit-Komponenten an. Wird nur auf 64-Bit-Systemen unterstützt.<br /><br /> Das Standardverzeichnis lautet „%Program Files(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server“.<br /><br /> Eine Festlegung auf „%Program Files%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server“ ist nicht möglich.|  
|SQL Server-Setupsteuerelement|/INSTANCEDIR<br /><br /> **Optional**|Gibt ein nicht standardmäßiges Installationsverzeichnis für instanzspezifische Komponenten an.|  
|SQL Server-Setupsteuerelement|/INSTANCEID<br /><br /> **Optional**|Gibt einen nicht standardmäßigen Wert für eine [InstanceID](#InstanceID)an.|  
|SQL Server-Setupsteuerelement|/INSTANCENAME<br /><br /> **Erforderlich**|Gibt den Namen einer SQL Server-Instanz an.<br /><br /> Weitere Informationen finden Sie unter [Instance Configuration](http://msdn.microsoft.com/library/5bf822fc-6dec-4806-a153-e200af28e9a5).|  
|SQL Server-Setupsteuerelement|/PID<br /><br /> **Optional**|Gibt den Product Key für die Edition von SQL Server an. Wenn dieser Parameter nicht angegeben wird, wird Evaluation verwendet.|  
|SQL Server-Setupsteuerelement|/Q<br /><br /> **Optional**|Gibt an, dass Setup ohne Benutzeroberfläche in einem stillen Modus ausgeführt wird. Dies wird für unbeaufsichtigte Installationen verwendet.|  
|SQL Server-Setupsteuerelement|/QS<br /><br /> **Optional**|Gibt an, dass Setup ausgeführt wird. Zudem wird der Fortschritt über die Benutzeroberfläche angezeigt. Es ist jedoch keine Eingabe möglich, und es werden keine Fehlermeldungen angezeigt.|  
|SQL Server-Setupsteuerelement|/SQMREPORTING<br /><br /> **Optional**|Hat in SQL Server 2016 keine Auswirkungen. <br/><br/>Informationen dazu, wie Feedback zu Fehlern an Microsoft gesendet wird, finden Sie unter [Konfigurieren von SQL Server 2016 zum Senden von Feedback an Microsoft](http://support.microsoft.com/kb/3153756). <br/><br/>In älteren Versionen wird damit die Erstellung von Funktionsverwendungsberichten für SQL Server angegeben.<br /><br />Unterstützte Werte:<br /><br /> 1 = aktiviert<br /><br /> 0 = deaktiviert|  
|SQL Server-Setupsteuerelement|/HIDECONSOLE<br /><br /> **Optional**|Gibt an, dass das Konsolenfenster ausgeblendet oder geschlossen ist.|  
|SQL Server-Setupsteuerelement|/FAILOVERCLUSTERDISKS<br /><br /> **Optional**|Gibt die Liste der freigegebenen Datenträger an, die in die SQL Server-Failovercluster-Ressourcengruppe einbezogen werden sollen.<br /><br /> Standardwert: Das erste Laufwerk wird als Standardlaufwerk für alle Datenbanken verwendet.|  
|SQL Server-Setupsteuerelement|/FAILOVERCLUSTERIPADDRESSES<br /><br /> **Erforderlich**|Gibt eine codierte IP-Adresse an. Die Codierungen sind durch Semikolons getrennt (;) und folgen dem Format \<IP-Typ>;\<Adresse>;\<Netzwerkname>;\<Subnetzmaske>. Zu den unterstützten IP-Typen gehören DHCP, IPv4 und IPv6.<br />Sie können mehrere Failovercluster-IP-Adressen mit einem Leerzeichen dazwischen angeben. Vergleichen Sie die folgenden Beispiele:<br /><br /> FAILOVERCLUSTERIPADDRESSES=DEFAULT<br /><br /> FAILOVERCLUSTERIPADDRESSES=IPv4;DHCP;ClusterNetwork1<br /><br /> FAILOVERCLUSTERIPADDRESSES=IPv4;172.16.0.0;ClusterNetwork1;172.31.255.255<br /><br /> FAILOVERCLUSTERIPADDRESSES=IPv6;DHCP;ClusterNetwork1<br /><br /> FAILOVERCLUSTERIPADDRESSES=IPv6;2001:db8:23:1002:20f:1fff:feff:b3a3;ClusterNetwork1|  
|SQL Server-Setupsteuerelement|/FAILOVERCLUSTERNETWORKNAME<br /><br /> **Erforderlich**|Gibt den Netzwerknamen für den neuen SQL Server-Failovercluster an. Dieser Name wird verwendet, um die neue SQL Server-Failoverclusterinstanz im Netzwerk zu erkennen.|  
|SQL Server-Agent|/AGTSVCACCOUNT<br /><br /> **Erforderlich**|Gibt das Konto für den SQL Server-Agent-Dienst an.|  
|SQL Server-Agent|/AGTSVCPASSWORD<br /><br /> [Erforderlich](#Accounts)|Gibt das Kennwort für das SQL Server-Agent-Dienstkonto an.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASBACKUPDIR<br /><br /> **Optional**|Gibt das Verzeichnis für Sicherungsdateien von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] an. Standardwerte:<br /><br /> Für den WOW-Modus auf 64-Bit-Systemen: %Program Files(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Backup<br /><br /> Für alle anderen Installationen: %Program Files%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Backup|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASCOLLATION<br /><br /> **Optional**|Legt die Sortierungseinstellung für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]fest.<br /><br /> Standardwert: **Latin1_General_CI_AS**|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASCONFIGDIR<br /><br /> **Optional**|Gibt das Verzeichnis für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Konfigurationsdateien an. Standardwerte:<br /><br /> Für den WOW-Modus auf 64-Bit-Systemen: %Program Files(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Config<br /><br /> Für alle anderen Installationen: %Program Files%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Config|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASDATADIR<br /><br /> **Optional**|Gibt das Verzeichnis für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datendateien an. Standardwerte:<br /><br /> Für den WOW-Modus auf 64-Bit-Systemen: %Program Files(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Data<br /><br /> Für alle anderen Installationen: %Program Files%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Data|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASLOGDIR<br /><br /> **Optional**|Gibt das Verzeichnis für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Protokolldateien an. Standardwerte:<br /><br /> Für den WOW-Modus auf 64-Bit-Systemen: %Program Files(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Log<br /><br /> Für alle anderen Installationen: %Program Files%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Log|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSYSADMINACCOUNTS<br /><br /> **Erforderlich**|Gibt die Administratoranmeldeinformationen für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]an.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASTEMPDIR<br /><br /> **Optional**|Gibt das Verzeichnis für temporäre [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Dateien an. Standardwerte:<br /><br /> Für den WOW-Modus auf 64-Bit-Systemen: %Program Files(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server \\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Temp<br /><br /> Für alle anderen Installationen: %Program Files%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Temp|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASPROVIDERMSOLAP<br /><br /> **Optional**|Gibt an, ob der MSOLAP-Anbieter innerhalb von Prozessen ausgeführt werden kann.<br /><br /> Standardwert: 1=aktiviert|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSERVERMODE<br /><br /> **Optional**|Gibt den Modus der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz an. Gültige Werte in einem Clusterszenario sind MULTIDIMENSIONAL oder TABULAR. Bei**ASSERVERMODE** wird die Groß- und Kleinschreibung berücksichtigt. Alle Werte müssen in Großbuchstaben angegeben werden. Weitere Informationen zu den gültigen Werten finden Sie im Tabellenmodus unter Analysis Services installieren.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/INSTALLSQLDATADIR<br /><br /> **Erforderlich**|Gibt das Datenverzeichnis für SQL Server-Datendateien an.<br /><br /> Das Datenverzeichnis muss angegeben werden und sich auf einem freigegebenen Clusterdatenträger befinden.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SAPWD<br /><br /> **Erforderlich, wenn /SECURITYMODE=SQL**|Gibt das Kennwort für das Systemadministratorkonto von SQL Server an.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SECURITYMODE<br /><br /> **Optional**|Gibt den Sicherheitsmodus für SQL Server an.<br /><br /> Wenn dieser Parameter nicht angegeben wird, kann die Authentifizierung nur über Windows erfolgen.<br /><br /> Unterstützter Wert: **SQL**|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLBACKUPDIR<br /><br /> **Optional**|Gibt das Verzeichnis für Sicherungsdateien an.<br /><br /> Standardwert: \<InstallSQLDataDir>\ \<SQLInstanceID>\MSSQL\Backup|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLCOLLATION<br /><br /> **Optional**|Legt die Sortierungseinstellungen für SQL Server fest.<br /><br /> Der Standardwert basiert auf dem Gebietsschema des Windows-Betriebssystems. Weitere Informationen finden Sie unter [Sortierungseinstellungen im Setup-Programm](http://msdn.microsoft.com/library/ms143508%28v=sql.105%29.aspx).|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCACCOUNT<br /><br /> **Erforderlich**|Gibt das Startkonto für den SQL Server-Dienst an.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCPASSWORD<br /><br /> [Erforderlich](#Accounts)|Gibt das Kennwort für SQLSVCACCOUNT an.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSYSADMINACCOUNTS<br /><br /> **Erforderlich**|Verwenden Sie diesen Parameter, um Anmeldenamen für Mitglieder der sysadmin-Rolle bereitzustellen.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLUSERDBDIR<br /><br /> **Optional**|Gibt das Verzeichnis für die Datendateien der Benutzerdatenbanken an.<br /><br /> Standardwert: \<InstallSQLDataDir>\ \<SQLInstanceID>\MSSQL\Data|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBDIR<br /><br /> **Optional**|Gibt die Verzeichnisse für tempdb-Datendateien an. Wenn Sie mehr als ein Verzeichnis angeben, trennen Sie die Verzeichnisse mit einem Leerzeichen. Wenn mehrere Verzeichnisse angegeben sind, werden die tempdb-Datendateien auf die Verzeichnisse im Rahmen eines Roundrobinverfahrens verteilt.<br /><br /> Standardwert: \<InstallSQLDataDir>\ \<SQLInstanceID>\MSSQL\Data(System Data Directory)<br /><br /> HINWEIS: Dieser Parameter wird dem RebuildDatabase-Szenario ebenfalls hinzugefügt.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGDIR<br /><br /> **Optional**|Gibt das Verzeichnis für die tempdb-Protokolldatei an.<br /><br /> Standardwert: \<InstallSQLDataDir>\ \<SQLInstanceID>\MSSQL\Data(System Data Directory)<br /><br /> HINWEIS: Dieser Parameter wird dem RebuildDatabase-Szenario ebenfalls hinzugefügt.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILECOUNT<br /><br /> **Optional**|Gibt die Anzahl von tempdb-Datendateien an, die von Setup hinzugefügt werden sollen. Dieser Wert kann bis zur Anzahl der Kerne heraufgesetzt werden. Standardwert:<br /><br /> 1 für [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]<br /><br /> 8 oder die Anzahl von Kernen, je nachdem, welcher Wert für alle anderen Editionen niedriger ist<br /><br /> **\*\* Wichtig \*\*** Die primäre Datenbankdatei für tempdb ist immer noch „tempdb.mdf“. Die zusätzlichen tempdb-Dateien werden nach dem Muster „tempdb_mssql_#.ndf“ benannt, wobei „#“ eine eindeutige Zahl für jede zusätzliche tempdb-Datenbankdatei darstellt, die beim Setup erstellt wurde. Diese Namenskonvention dient dazu, die Dateinamen eindeutig zu machen. Beim Deinstallieren einer Instanz von SQL Server werden die Dateien gelöscht, die der Namenskonvention „tempdb_mssql_#.ndf“ folgen. Verwenden Sie die Namenskonvention „tempdb_mssql_\*.ndf“ nicht für andere Datenbankdateien.<br /><br /> **\*\* Warnung \*\*** [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]wird für die Konfiguration dieses Parameters nicht unterstützt. Setup installiert nur 1 Tempdb-Datendatei.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILESIZE<br /><br /> **Optional**|In [!INCLUDE[SQL VERSION](../../includes/sssql15-md.md)] eingeführt. Gibt die Anfangsgröße jeder tempdb-Datendatei an.<br/><br/>Standard =  8 MB<br/><br/>Min =  8 MB<br/><br/>Max = 1024 MB (262.144 MB für [!INCLUDE[SQL VERSION](../../includes/sssqlv14-md.md)])|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILEGROWTH<br /><br /> **Optional**|Gibt das Dateivergrößerungsinkrement jeder tempdb-Datendatei in MB an. Der Wert 0 zeigt an, dass die automatische Vergrößerung deaktiviert ist und kein zusätzlicher Platz zulässig ist. Das Setup ermöglicht eine Größe von bis zu 1024 MB.<br /><br /> Standardwert: 64<br /><br /> Zulässiger Bereich: Min = 0, Max = 1024|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGFILESIZE<br /><br /> **Optional**|Gibt die Anfangsgröße einer tempdb-Protokolldatei in MB an. Das Setup ermöglicht eine Größe von bis zu 1024 MB. <br /> Standardwert:<br /><br /> 4 für [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]<br /><br /> 8 für alle anderen Editionen<br /><br /> Zulässiger Bereich: Min = Standardwert (4 oder 8), Max = 1024|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGFILEGROWTH<br /><br /> **Optional**|In [!INCLUDE[SQL VERSION](../../includes/sssql15-md.md)] eingeführt. Gibt die Anfangsgröße einer tempdb-Protokolldatei in MB an.<br/><br/>Standard = 4 MB für [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], 8 MB für alle anderen Editionen<br/><br/>Min = (4 oder 8 MB)<br/><br/>Max = 1024 MB (262.144 MB für [!INCLUDE[SQL VERSION](../../includes/sssqlv14-md.md)])|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLUSERDBLOGDIR<br /><br /> **Optional**|Gibt das Verzeichnis für die Protokolldateien der Benutzerdatenbanken an.<br /><br /> Standardwert: \<InstallSQLDataDir>\ \<SQLInstanceID>\MSSQL\Data|  
|FILESTREAM|/FILESTREAMLEVEL<br /><br /> **Optional**|Gibt die Zugriffsebene für die FILESTREAM-Funktion an. Unterstützte Werte:<br /><br /> 0 = FILESTREAM-Unterstützung für diese Instanz deaktivieren. (Standardwert)<br /><br /> 1 = FILESTREAM für den [!INCLUDE[tsql](../../includes/tsql-md.md)] -Zugriff aktivieren.<br /><br /> 2 = FILESTREAM für den [!INCLUDE[tsql](../../includes/tsql-md.md)] - und E/A-Streamingzugriff auf Datei aktivieren. (Nicht gültig für Clusterszenarien)<br /><br /> 3 = Streamingzugriff von Remoteclients auf FILESTREAM-Daten zulassen.|  
|FILESTREAM|/FILESTREAMSHARENAME<br /><br /> **Optional**<br /><br /> **Erforderlich, wenn FILESTREAMLEVEL größer als 1 ist.**|Gibt den Namen der Windows-Freigabe an, in der die FILESTREAM-Daten gespeichert werden.|  
|SQL Server-Volltext|/FTSVCACCOUNT<br /><br /> **Optional**|Gibt das Konto für den Volltextfilter-Startprogrammdienst an.<br /><br /> Dieser Parameter wird in [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]ignoriert. ServiceSID wird verwendet, um die Kommunikation zwischen SQL Server und dem Volltextfilter-Daemon zu sichern.<br /><br /> Wenn die Werte nicht bereitgestellt werden, wird der Volltextfilter-Startprogrammdienst deaktiviert. Sie müssen den SQL Server-Dienstkontroll-Manager verwenden, um das Dienstkonto zu ändern und die Volltextfunktion zu aktivieren.<br /><br /> Standardwert: Lokales Dienstkonto|  
|SQL Server-Volltext|/FTSVCPASSWORD<br /><br /> **Optional**|Gibt das Kennwort für den Volltextfilter-Startprogrammdienst an.<br /><br /> Dieser Parameter wird in [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]ignoriert.|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCACCOUNT<br /><br /> **Erforderlich**|Gibt das Konto für [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]an.<br /><br /> Der Standardwert ist: „NT Authority\NETWORK SERVICE“.|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCPASSWORD<br /><br /> [Erforderlich](#Accounts)|Gibt das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Kennwort an.|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCStartupType<br /><br /> **Optional**|Gibt den [Startmodus](#Accounts) für den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst an.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSINSTALLMODE<br /><br /> **Optional**|Gibt den Installationsmodus für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]an.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCACCOUNT<br /><br /> **Erforderlich**|Gibt das Startkonto für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]an.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCPASSWORD<br /><br /> [Erforderlich](#Accounts)|Gibt das Kennwort für das Startkonto für den [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienst an.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCStartupType<br /><br /> **Optional**|Gibt den [Startmodus](#Accounts) für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]an.|  
  
 Es wird empfohlen, die Dienst-SID anstelle von Domänengruppen zu verwenden. 
  
##### <a name="additional-notes"></a>Weitere Hinweise:  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] und [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] sind die einzigen Komponenten, die clusterfähig sind. Andere Funktionen sind nicht clusterfähig und haben keine hohe Verfügbarkeit über ein Failover. 
  
###### <a name="sample-syntax"></a>Beispielsyntax:  
 So installieren Sie eine SQL Server-Failoverclusterinstanz mit einem einzelnen Knoten mit der Standardinstanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] und [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 
  
```  
setup.exe /q /ACTION=InstallFailoverCluster /InstanceName=MSSQLSERVER /INDICATEPROGRESS /ASSYSADMINACCOUNTS="<DomainName\UserName>" /ASDATADIR=<Drive>:\OLAP\Data /ASLOGDIR=<Drive>:\OLAP\Log /ASBACKUPDIR=<Drive>:\OLAP\Backup /ASCONFIGDIR=<Drive>:\OLAP\Config /ASTEMPDIR=<Drive>:\OLAP\Temp /FAILOVERCLUSTERDISKS="<Cluster Disk Resource Name - for example, 'Disk S:'" /FAILOVERCLUSTERNETWORKNAME="<Insert Network Name>" /FAILOVERCLUSTERIPADDRESSES="IPv4;xx.xxx.xx.xx;Cluster Network;xxx.xxx.xxx.x" /FAILOVERCLUSTERGROUP="MSSQLSERVER" /Features=AS,SQL /ASSVCACCOUNT="<DomainName\UserName>" /ASSVCPASSWORD="xxxxxxxxxxx" /AGTSVCACCOUNT="<DomainName\UserName>" /AGTSVCPASSWORD="xxxxxxxxxxx" /INSTALLSQLDATADIR="<Drive>:\<Path>\MSSQLSERVER" /SQLCOLLATION="SQL_Latin1_General_CP1_CS_AS" /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="xxxxxxxxxxx" /SQLSYSADMINACCOUNTS="<DomainName\UserName> /IACCEPTSQLSERVERLICENSETERMS  
```  
  
#### <a name="prepare-failover-cluster-parameters"></a>Vorbereiten von Failoverclusterparametern  
 Entwickeln Sie mit den in der folgenden Tabelle aufgeführten Parametern Befehlszeilenskripts für die Failoverclustervorbereitung. Hierbei handelt es sich um den ersten Schritt bei der erweiterten Clusterinstallation, für den die Failoverclusterinstanzen auf allen Knoten des Failoverclusters vorbereitet werden müssen. Weitere Informationen finden Sie unter [Always On-Failoverclusterinstanzen &#40;SQL Server&#41;](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md). 
  
|SQL Server-Komponente|Parameter|Description|  
|-----------------------------------------|---------------|-----------------|  
|SQL Server-Setupsteuerelement|/ACTION<br /><br /> **Erforderlich**|Erforderlich, um den Vorbereitungsworkflow des Failoverclusters anzugeben.<br /><br /> Unterstützter Wert: **PrepareFailoverCluster**|  
|SQL Server-Setupsteuerelement|/IACCEPTSQLSERVERLICENSETERMS<br /><br /> **Nur erforderlich, wenn der /Q-Parameter oder der /QS-Parameter für die unbeaufsichtigte Installation angegeben wird.**|Erforderlich, um das Einverständnis mit den Lizenzbedingungen zu erklären.|  
|SQL Server-Setupsteuerelement|/ENU<br /><br /> **Optional**|Verwenden Sie diesen Parameter, um die englische Version von SQL Server unter einem lokalisierten Betriebssystem zu installieren, wenn die Installationsmedien sowohl Language Packs für Englisch als auch für die Sprache des Betriebssystems enthalten.|  
|SQL Server-Setupsteuerelement|/*UpdateEnabled*<br /><br /> **Optional**|Geben Sie an, ob das SQL Server-Setup Produktupdates ermitteln und einschließen soll. Gültige Werte sind True und False oder 1 und 0. Standardmäßig schließt das SQL Server-Setup alle gefundenen Updates ein.|  
|SQL Server-Setupsteuerelement|/*UpdateSource*<br /><br /> **Optional**|Geben Sie an, wo Produktupdates vom SQL Server-Setup abgerufen werden sollen. Gültige Werte sind „MU“ für die Suche in [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update, ein gültiger Ordnerpfad, ein relativer Pfad wie „.\MyUpdates“ oder eine UNC-Freigabe. Das SQL Server-Setup durchsucht standardmäßig [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update oder einen Windows Update-Dienst über Windows Server Update Services.|  
|SQL Server-Setupsteuerelement|/CONFIGURATIONFILE<br /><br /> **Optional**|Gibt die zu verwendende [ConfigurationFile](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md) an.|  
|SQL Server-Setupsteuerelement|/ERRORREPORTING<br /><br /> **Optional**|Hat in SQL Server 2016 keine Auswirkungen. <br/><br/>Informationen dazu, wie Feedback zu Fehlern an Microsoft gesendet wird, finden Sie unter [Konfigurieren von SQL Server 2016 zum Senden von Feedback an Microsoft](http://support.microsoft.com/kb/3153756). <br/><br/>In älteren Versionen wird damit die Fehlerberichterstattung für SQL Server angegeben.<br /><br /> Weitere Informationen finden Sie in den [Datenschutzbestimmungen für den Microsoft-Fehlerberichterstattungsdienst](http://go.microsoft.com/fwlink/?LinkID=72173). Unterstützte Werte:<br /><br /> 0 = deaktiviert<br /><br /> 1 = aktiviert|  
|SQL Server-Setupsteuerelement|/FEATURES<br /><br /> **Erforderlich**|Gibt zu installierende [Komponenten](#Feature) an.|  
|SQL Server-Setupsteuerelement|/HELP, H, ?<br /><br /> **Optional**|Zeigt die Verwendungsoptionen für die Parameter an.|  
|SQL Server-Setupsteuerelement|/INDICATEPROGRESS<br /><br /> **Optional**|Gibt an, dass die ausführliche Setupprotokolldatei an die Konsole weitergeleitet wird.|  
|SQL Server-Setupsteuerelement|/INSTALLSHAREDDIR<br /><br /> **Optional**|Gibt ein nicht standardmäßiges Installationsverzeichnis für freigegebene 64-Bit-Komponenten an.<br /><br /> Das Standardverzeichnis lautet „%Program Files%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server“.<br /><br /> Eine Festlegung auf „%Program Files(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server“ ist nicht möglich.|  
|SQL Server-Setupsteuerelement|/INSTALLSHAREDWOWDIR<br /><br /> **Optional**|Gibt ein nicht standardmäßiges Installationsverzeichnis für freigegebene 32-Bit-Komponenten an. Wird nur auf 64-Bit-Systemen unterstützt.<br /><br /> Das Standardverzeichnis lautet „%Program Files(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server“.<br /><br /> Eine Festlegung auf „%Program Files%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server“ ist nicht möglich.|  
|SQL Server-Setupsteuerelement|/INSTANCEDIR<br /><br /> **Optional**|Gibt ein nicht standardmäßiges Installationsverzeichnis für instanzspezifische Komponenten an.|  
|SQL Server-Setupsteuerelement|/INSTANCEID<br /><br /> **Optional**|Gibt einen nicht standardmäßigen Wert für eine [InstanceID](#InstanceID)an.|  
|SQL Server-Setupsteuerelement|/INSTANCENAME<br /><br /> **Erforderlich**|Gibt den Namen einer SQL Server-Instanz an.<br /><br /> Weitere Informationen finden Sie unter [Instance Configuration](http://msdn.microsoft.com/library/5bf822fc-6dec-4806-a153-e200af28e9a5).|  
|PolyBase|/PBENGSVCACCOUNT<br /><br /> **Optional**|Gibt das Konto für den Moduldienst an. Der Standardwert ist **NT Authority\NETWORK SERVICE**.|  
|PolyBase|/PBDMSSVCPASSWORD<br /><br /> **Optional**|Gibt das Kennwort für das Moduldienstkonto an.|  
|PolyBase|/PBENGSVCSTARTUPTYPE<br /><br /> **Optional**|Gibt den Startmodus für den PolyBase-Moduldienst an: Automatisch (Standard), Deaktiviert und Manuell.|  
|PolyBase|/PBPORTRANGE<br /><br /> **Optional**|Gibt einen Portbereich für PolyBase-Dienste mit mindestens sechs Ports an. Beispiel:<br /><br /> `/PBPORTRANGE=16450-16460`|  
|PolyBase|/PBSCALEOUT<br /><br /> **Optional**|Gibt an, ob die SQL Server-Instanz als Teil einer PolyBase-Erweiterungsgruppe aus Computeknoten verwendet wird. Unterstützte Werte: **True**, **False**|  
|SQL Server-Setupsteuerelement|/PID<br /><br /> **Optional**|Gibt den Product Key für die Edition von SQL Server an. Wenn dieser Parameter nicht angegeben wird,<br /><br /> wird Evaluation verwendet.|  
|SQL Server-Setupsteuerelement|/Q<br /><br /> **Optional**|Gibt an, dass Setup ohne Benutzeroberfläche in einem stillen Modus ausgeführt wird. Dies wird für unbeaufsichtigte Installationen verwendet.|  
|SQL Server-Setupsteuerelement|/QS<br /><br /> **Optional**|Gibt an, dass Setup ausgeführt wird. Zudem wird der Fortschritt über die Benutzeroberfläche angezeigt. Es ist jedoch keine Eingabe möglich, und es werden keine Fehlermeldungen angezeigt.|  
|SQL Server-Setupsteuerelement|/SQMREPORTING<br /><br /> **Optional**|Hat in SQL Server 2016 keine Auswirkungen. <br/><br/>Informationen dazu, wie Feedback zu Fehlern an Microsoft gesendet wird, finden Sie unter [Konfigurieren von SQL Server 2016 zum Senden von Feedback an Microsoft](http://support.microsoft.com/kb/3153756). <br/><br/>In älteren Versionen wird damit die Erstellung von Funktionsverwendungsberichten für SQL Server angegeben.<br /><br />Unterstützte Werte:<br /><br /> 0 = deaktiviert<br /><br /> 1 = aktiviert|  
|SQL Server-Setupsteuerelement|/HIDECONSOLE<br /><br /> **Optional**|Gibt an, dass das Konsolenfenster ausgeblendet oder geschlossen ist.|  
|SQL Server-Agent|/AGTSVCACCOUNT<br /><br /> **Erforderlich**|Gibt das Konto für den SQL Server-Agent-Dienst an.|  
|SQL Server-Agent|/AGTSVCPASSWORD<br /><br /> [Erforderlich](#Accounts)|Gibt das Kennwort für das SQL Server-Agent-Dienstkonto an.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSVCACCOUNT<br /><br /> **Erforderlich**|Gibt das Konto für den [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Dienst an.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSVCPASSWORD<br /><br /> [Erforderlich](#Accounts)|Gibt das Kennwort für den [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Dienst an.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCACCOUNT<br /><br /> **Erforderlich**|Gibt das Startkonto für den SQL Server-Dienst an.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCPASSWORD<br /><br /> [Erforderlich](#Accounts)|Gibt das Kennwort für SQLSVCACCOUNT an.|  
|FILESTREAM|/FILESTREAMLEVEL<br /><br /> **Optional**|Gibt die Zugriffsebene für die FILESTREAM-Funktion an. Unterstützte Werte:<br /><br /> 0 = FILESTREAM-Unterstützung für diese Instanz deaktivieren. (Standardwert)<br /><br /> 1 = FILESTREAM für den [!INCLUDE[tsql](../../includes/tsql-md.md)] -Zugriff aktivieren.<br /><br /> 2 = FILESTREAM für den [!INCLUDE[tsql](../../includes/tsql-md.md)] - und E/A-Streamingzugriff auf Datei aktivieren. (Nicht gültig für Clusterszenarien)<br /><br /> 3 = Streamingzugriff von Remoteclients auf FILESTREAM-Daten zulassen.|  
|FILESTREAM|/FILESTREAMSHARENAME<br /><br /> **Optional**<br /><br /> **Erforderlich** , wenn FILESTREAMLEVEL größer als 1 ist.|Gibt den Namen der Windows-Freigabe an, in der die FILESTREAM-Daten gespeichert werden.|  
|SQL Server-Volltext|/FTSVCACCOUNT<br /><br /> **Optional**|Gibt das Konto für den Volltextfilter-Startprogrammdienst an.<br /><br /> Dieser Parameter wird in [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]ignoriert. ServiceSID wird verwendet, um die Kommunikation zwischen SQL Server und dem Volltextfilter-Daemon zu sichern.<br /><br /> Wenn die Werte nicht bereitgestellt werden, wird der Volltextfilter-Startprogrammdienst deaktiviert. Sie müssen den SQL Server-Dienstkontroll-Manager verwenden, um das Dienstkonto zu ändern und die Volltextfunktion zu aktivieren.<br /><br /> Standardwert: Lokales Dienstkonto|  
|SQL Server-Volltext|/FTSVCPASSWORD<br /><br /> **Optional**|Gibt das Kennwort für den Volltextfilter-Startprogrammdienst an.<br /><br /> Dieser Parameter wird in [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]ignoriert.|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCACCOUNT<br /><br /> **Erforderlich**|Gibt das Konto für [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]an.<br /><br /> Der Standardwert ist: „NT Authority\NETWORK SERVICE“.|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCPASSWORD<br /><br /> [Erforderlich](#Accounts)|Gibt das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Kennwort an.|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCStartupType<br /><br /> **Optional**|Gibt den [Startmodus](#Accounts) für den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst an.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSINSTALLMODE<br /><br /> **Nur im reinen Dateimodus verfügbar.**|Gibt den Installationsmodus für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]an.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCACCOUNT<br /><br /> **Erforderlich**|Gibt das Startkonto für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]an.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCPASSWORD<br /><br /> [Erforderlich](#Accounts)|Gibt das Kennwort für das Startkonto für den [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienst an.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCStartupType<br /><br /> **Optional**|Gibt den [Startmodus](#Accounts) für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]an.|  
  
 Es wird empfohlen, die Dienst-SID anstelle von Domänengruppen zu verwenden. 
  
###### <a name="sample-syntax"></a>Beispielsyntax:  
 So führen Sie den Schritt zur Vorbereitung eines Failoverclusters in einem erweiterten Installationsszenario für [!INCLUDE[ssDE](../../includes/ssde-md.md)] und [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]aus 
  
 Führen Sie an der Eingabeaufforderung den folgenden Befehl aus, um eine Standardinstanz vorzubereiten:  
  
```  
setup.exe /q /ACTION=PrepareFailoverCluster /InstanceName=MSSQLSERVER /Features=AS,SQL /INDICATEPROGRESS /ASSVCACCOUNT="<DomainName\UserName>" /ASSVCPASSWORD="xxxxxxxxxxx" /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="xxxxxxxxxxx" /AGTSVCACCOUNT="<DomainName\UserName>" /AGTSVCPASSWORD="xxxxxxxxxxx" /IACCEPTSQLSERVERLICENSETERMS  
```  
  
 Führen Sie an der Eingabeaufforderung den folgenden Befehl aus, um eine benannte Instanz vorzubereiten:  
  
```  
setup.exe /q /ACTION=PrepareFailoverCluster /InstanceName="<Insert Instance name>" /Features=AS,SQL /INDICATEPROGRESS /ASSVCACCOUNT="<DomainName\UserName>" /ASSVCPASSWORD="xxxxxxxxxxx" /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="xxxxxxxxxxx" /AGTSVCACCOUNT="<DomainName\UserName>" /AGTSVCPASSWORD="xxxxxxxxxxx" /IACCEPTSQLSERVERLICENSETERMS  
```  
  
#### <a name="complete-failover-cluster-parameters"></a>Abschließende Failoverclusterparameter  
 Entwickeln Sie mit den in der folgenden Tabelle aufgeführten Parametern Befehlszeilenskripts für das Abschließen von Failoverclustern. Dies ist der zweite Schritt der erweiterten Failovercluster-Installationsoption. Nachdem Sie die Vorbereitung für alle Failoverclusterknoten ausgeführt haben, führen Sie diesen Befehl für den Knoten aus, der den (oder die) freigegebenen Datenträger besitzt. Weitere Informationen finden Sie unter [Always On-Failoverclusterinstanzen &#40;SQL Server&#41;](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md). 
  
|SQL Server-Komponente|Parameter|Description|  
|-----------------------------------------|---------------|-----------------|  
|SQL Server-Setupsteuerelement|/ACTION<br /><br /> **Erforderlich**|Erforderlich, um den Workflow für das Abschließen des Failoverclusters anzugeben.<br /><br /> Unterstützter Wert: **CompleteFailoverCluster**|  
|SQL Server-Setupsteuerelement|/ENU<br /><br /> **Optional**|Verwenden Sie diesen Parameter, um die englische Version von SQL Server unter einem lokalisierten Betriebssystem zu installieren, wenn die Installationsmedien sowohl Language Packs für Englisch als auch für die Sprache des Betriebssystems enthalten.|  
|SQL Server-Setupsteuerelement|/FAILOVERCLUSTERGROUP<br /><br /> **Optional**|Gibt den Namen der Ressourcengruppe an, die für den SQL Server-Failovercluster verwendet werden soll. Es kann sich um den Namen einer vorhandenen Clustergruppe oder den Namen einer neuen Ressourcengruppe handeln.<br /><br /> Standardwert:<br /><br /> SQL Server (\<Instanzname>)|  
|SQL Server-Setupsteuerelement|/CONFIGURATIONFILE<br /><br /> **Optional**|Gibt die zu verwendende [ConfigurationFile](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md) an.|  
|SQL Server-Setupsteuerelement|/ERRORREPORTING<br /><br /> **Optional**|Hat in SQL Server 2016 keine Auswirkungen. <br/><br/>Informationen dazu, wie Feedback zu Fehlern an Microsoft gesendet wird, finden Sie unter [Konfigurieren von SQL Server 2016 zum Senden von Feedback an Microsoft](http://support.microsoft.com/kb/3153756). <br/><br/>In älteren Versionen wird damit die Fehlerberichterstattung für SQL Server angegeben.<br /><br /> Weitere Informationen finden Sie in den [Datenschutzbestimmungen für den Microsoft-Fehlerberichterstattungsdienst](http://go.microsoft.com/fwlink/?LinkID=72173). Unterstützte Werte:<br /><br /> 1 = aktiviert<br /><br /> 0 = deaktiviert|  
|SQL Server-Setupsteuerelement|/HELP, H, ?<br /><br /> **Optional**|Zeigt die Verwendungsoptionen für die Parameter an.|  
|SQL Server-Setupsteuerelement|/INDICATEPROGRESS<br /><br /> **Optional**|Gibt an, dass die ausführliche Setupprotokolldatei an die Konsole weitergeleitet wird.|  
|SQL Server-Setupsteuerelement|/INSTANCENAME<br /><br /> **Erforderlich**|Gibt den Namen einer SQL Server-Instanz an.<br /><br /> Weitere Informationen finden Sie unter [Instance Configuration](http://msdn.microsoft.com/library/5bf822fc-6dec-4806-a153-e200af28e9a5).|  
|SQL Server-Setupsteuerelement|/PID<br /><br /> **Optional**|Gibt den Product Key für die Edition von SQL Server an. Wenn dieser Parameter nicht angegeben wird, wird Evaluation verwendet.|  
|SQL Server-Setupsteuerelement|/Q<br /><br /> **Optional**|Gibt an, dass Setup ohne Benutzeroberfläche in einem stillen Modus ausgeführt wird. Dies wird für unbeaufsichtigte Installationen verwendet.|  
|SQL Server-Setupsteuerelement|/QS<br /><br /> **Optional**|Gibt an, dass Setup ausgeführt wird. Zudem wird der Fortschritt über die Benutzeroberfläche angezeigt. Es ist jedoch keine Eingabe möglich, und es werden keine Fehlermeldungen angezeigt.|  
|SQL Server-Setupsteuerelement|/SQMREPORTING<br /><br /> **Optional**|Hat in SQL Server 2016 keine Auswirkungen. <br/><br/>Informationen dazu, wie Feedback zu Fehlern an Microsoft gesendet wird, finden Sie unter [Konfigurieren von SQL Server 2016 zum Senden von Feedback an Microsoft](http://support.microsoft.com/kb/3153756). <br/><br/>In älteren Versionen wird damit die Erstellung von Funktionsverwendungsberichten für SQL Server angegeben.<br /><br />Unterstützte Werte:<br /><br /> 1 = aktiviert<br /><br /> 0 = deaktiviert|  
|SQL Server-Setupsteuerelement|/HIDECONSOLE<br /><br /> **Optional**|Gibt an, dass das Konsolenfenster ausgeblendet oder geschlossen ist.|  
|SQL Server-Setupsteuerelement|/FAILOVERCLUSTERDISKS<br /><br /> **Optional**|Gibt die Liste der freigegebenen Datenträger an, die in die SQL Server-Failovercluster-Ressourcengruppe einbezogen werden sollen.<br /><br /> Standardwert:<br /><br /> Das erste Laufwerk wird als Standardlaufwerk für alle Datenbanken verwendet.|  
|SQL Server-Setupsteuerelement|/FAILOVERCLUSTERIPADDRESSES<br /><br /> **Erforderlich**|Gibt eine codierte IP-Adresse an. Die Codierungen sind durch Semikolons getrennt (;) und folgen dem Format \<IP-Typ>;\<Adresse>;\<Netzwerkname>;\<Subnetzmaske>. Zu den unterstützten IP-Typen gehören DHCP, IPv4 und IPv6.<br />Sie können mehrere Failovercluster-IP-Adressen mit einem Leerzeichen dazwischen angeben. Vergleichen Sie die folgenden Beispiele:<br /><br /> FAILOVERCLUSTERIPADDRESSES=DEFAULT<br /><br /> FAILOVERCLUSTERIPADDRESSES=IPv4;DHCP;ClusterNetwork1<br /><br /> FAILOVERCLUSTERIPADDRESSES=IPv4;172.16.0.0;ClusterNetwork1;172.31.255.255<br /><br /> FAILOVERCLUSTERIPADDRESSES=IPv6;DHCP;ClusterNetwork1<br /><br /> FAILOVERCLUSTERIPADDRESSES=IPv6;2001:db8:23:1002:20f:1fff:feff:b3a3;ClusterNetwork1|  
|SQL Server-Setupsteuerelement|/FAILOVERCLUSTERNETWORKNAME<br /><br /> **Erforderlich**|Gibt den Netzwerknamen für den neuen SQL Server-Failovercluster an. Dieser Name wird verwendet, um die neue SQL Server-Failoverclusterinstanz im Netzwerk zu erkennen.|  
|SQL Server-Setupsteuerelement|/CONFIRMIPDEPENDENCYCHANGE|Gibt an, dass die IP-Adressabhängigkeit für Multisubnetz-Failovercluster auf OR festgelegt werden soll. Weitere Informationen finden Sie unter [Erstellen eines neuen SQL Server-Failoverclusters &#40;Setup&#41;](../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md). Unterstützte Werte:<br /><br /> 0 = False (Standard)<br /><br /> 1 = True|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASBACKUPDIR<br /><br /> **Optional**|Gibt das Verzeichnis für Sicherungsdateien von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] an. Standardwerte:<br /><br /> Für den WOW-Modus auf 64-Bit-Systemen: %Program Files(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Backup<br /><br /> Für alle anderen Installationen: %Program Files%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Backup|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASCOLLATION<br /><br /> **Optional**|Legt die Sortierungseinstellung für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]fest.<br /><br /> Standardwert: **Latin1_General_CI_AS**|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASCONFIGDIR<br /><br /> **Optional**|Gibt das Verzeichnis für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Konfigurationsdateien an. Standardwerte:<br /><br /> Für den WOW-Modus auf 64-Bit-Systemen: %Program Files(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Config<br /><br /> Für alle anderen Installationen: %Program Files%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Config|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASDATADIR<br /><br /> **Optional**|Gibt das Verzeichnis für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datendateien an. Standardwerte:<br /><br /> Für den WOW-Modus auf 64-Bit-Systemen: %Program Files(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Data<br /><br /> Für alle anderen Installationen: %Program Files%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\\<INSTANCEDIR\>\\<ASInstanceID\>\OLAP\Data|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASLOGDIR<br /><br /> **Optional**|Gibt das Verzeichnis für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Protokolldateien an. Standardwerte:<br /><br /> Für den WOW-Modus auf 64-Bit-Systemen: %Program Files(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\ \<INSTANCEDIR>\\<ASInstanceID\>\OLAP\Log<br /><br /> Für alle anderen Installationen: %Program Files%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\ \<INSTANCEDIR>\\<ASInstanceID\>\OLAP\Log|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSERVERMODE<br /><br /> **Optional**|Gibt den Servermodus der Analysis Services-Instanz an. Gültige Werte in einem Clusterszenario sind MULTIDIMENSIONAL oder TABULAR. Bei**ASSERVERMODE** wird die Groß- und Kleinschreibung berücksichtigt. Alle Werte müssen in Großbuchstaben angegeben werden. Weitere Informationen zu den gültigen Werten finden Sie im Tabellenmodus unter Analysis Services installieren.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSYSADMINACCOUNTS<br /><br /> **Erforderlich**|Gibt die Administratoranmeldeinformationen für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]an.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASTEMPDIR<br /><br /> **Optional**|Gibt das Verzeichnis für temporäre [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Dateien an. Standardwerte:<br /><br /> Für den WOW-Modus auf 64-Bit-Systemen: %Program Files(x86)%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\ \<INSTANCEDIR>\\<ASInstanceID\>\OLAP\Temp<br /><br /> Für alle anderen Installationen: %Program Files%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]SQL Server\ \<INSTANCEDIR>\\<ASInstanceID\>\OLAP\Temp|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASPROVIDERMSOLAP<br /><br /> **Optional**|Gibt an, ob der MSOLAP-Anbieter innerhalb von Prozessen ausgeführt werden kann.<br /><br /> Standardwert: 1=aktiviert|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/INSTALLSQLDATADIR<br /><br /> **Erforderlich**|Gibt das Datenverzeichnis für SQL Server-Datendateien an.<br /><br /> Das Datenverzeichnis muss angegeben werden und sich auf einem freigegebenen Clusterdatenträger befinden.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SAPWD<br /><br /> **Erforderlich, wenn /SECURITYMODE=SQL**|Gibt das Kennwort für das Systemadministratorkonto von SQL Server an.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SECURITYMODE<br /><br /> **Optional**|Gibt den Sicherheitsmodus für SQL Server an.<br /><br /> Wenn dieser Parameter nicht angegeben wird, kann die Authentifizierung nur über Windows erfolgen.<br /><br /> Unterstützter Wert: **SQL**|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLBACKUPDIR<br /><br /> **Optional**|Gibt das Verzeichnis für Sicherungsdateien an.<br /><br /> Standardwert: \<InstallSQLDataDir>\ \<SQLInstanceID>\MSSQL\Backup|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLCOLLATION<br /><br /> **Optional**|Legt die Sortierungseinstellungen für SQL Server fest.<br /><br /> Der Standardwert basiert auf dem Gebietsschema des Windows-Betriebssystems. Weitere Informationen finden Sie unter [Sortierungseinstellungen im Setup-Programm](http://msdn.microsoft.com/library/ms143508%28v=sql.105%29.aspx).|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSYSADMINACCOUNTS<br /><br /> **Erforderlich**|Verwenden Sie diesen Parameter, um Anmeldenamen für Mitglieder der sysadmin-Rolle bereitzustellen.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLUSERDBDIR<br /><br /> **Optional**|Gibt das Verzeichnis für die Datendateien der Benutzerdatenbanken an.<br /><br /> Standardwert: \<InstallSQLDataDir>\ \<SQLInstanceID>\MSSQL\Data|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLUSERDBLOGDIR<br /><br /> **Optional**|Gibt das Verzeichnis für die Protokolldateien der Benutzerdatenbanken an.<br /><br /> Standardwert: \<InstallSQLDataDir>\ \<SQLInstanceID>\MSSQL\Data|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSINSTALLMODE<br /><br /> **Nur im reinen Dateimodus verfügbar.**|Gibt den Installationsmodus für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]an.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBDIR<br /><br /> **Optional**|Gibt die Verzeichnisse für tempdb-Datendateien an. Wenn Sie mehr als ein Verzeichnis angeben, trennen Sie die Verzeichnisse mit einem Leerzeichen. Wenn mehrere Verzeichnisse angegeben sind, werden die tempdb-Datendateien auf die Verzeichnisse im Rahmen eines Roundrobinverfahrens verteilt.<br /><br /> Standardwert: \<InstallSQLDataDir>\ \<SQLInstanceID>\MSSQL\Data(System Data Directory)<br /><br /> HINWEIS: Dieser Parameter wird dem RebuildDatabase-Szenario ebenfalls hinzugefügt.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGDIR<br /><br /> **Optional**|Gibt das Verzeichnis für die tempdb-Protokolldatei an.<br /><br /> Standardwert: \<InstallSQLDataDir>\ \<SQLInstanceID>\MSSQL\Data(System Data Directory)<br /><br /> HINWEIS: Dieser Parameter wird dem RebuildDatabase-Szenario ebenfalls hinzugefügt.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILECOUNT<br /><br /> **Optional**|Gibt die Anzahl von tempdb-Datendateien an, die von Setup hinzugefügt werden sollen. Dieser Wert kann bis zur Anzahl der Kerne heraufgesetzt werden. Standardwert:<br /><br /> 1 für [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]<br /><br /> 8 oder die Anzahl von Kernen, je nachdem, welcher Wert für alle anderen Editionen niedriger ist<br /><br /> **\*\* Wichtig \*\*** Die primäre Datenbankdatei für tempdb ist immer noch „tempdb.mdf“. Die zusätzlichen tempdb-Dateien werden nach dem Muster „tempdb_mssql_#.ndf“ benannt, wobei „#“ eine eindeutige Zahl für jede zusätzliche tempdb-Datenbankdatei darstellt, die beim Setup erstellt wurde. Diese Namenskonvention dient dazu, die Dateinamen eindeutig zu machen. Beim Deinstallieren einer Instanz von SQL Server werden die Dateien gelöscht, die der Namenskonvention „tempdb_mssql_#.ndf“ folgen. Verwenden Sie die Namenskonvention „tempdb_mssql_\*.ndf“ nicht für andere Datenbankdateien.<br /><br /> **\*\* Warnung \*\*** [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]wird für die Konfiguration dieses Parameters nicht unterstützt. Setup installiert nur 1 Tempdb-Datendatei.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILESIZE<br /><br /> **Optional**|In [!INCLUDE[SQL VERSION](../../includes/sssql15-md.md)] eingeführt. Gibt die Anfangsgröße jeder tempdb-Datendatei an.<br/><br/>Standard = 8 MB<br/><br/>Min = 8 MB<br/><br/>Max = 1024 MB (262.144 MB für [!INCLUDE[SQL VERSION](../../includes/sssqlv14-md.md)])|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBFILEGROWTH<br /><br /> **Optional**|Gibt das Dateivergrößerungsinkrement jeder tempdb-Datendatei in MB an. Der Wert 0 zeigt an, dass die automatische Vergrößerung deaktiviert ist und kein zusätzlicher Platz zulässig ist. Das Setup ermöglicht eine Größe von bis zu 1024 MB.<br /><br /> Standardwert: 64<br /><br /> Zulässiger Bereich: Min = 0, Max = 1024|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGFILESIZE<br /><br /> **Optional**|Gibt die Anfangsgröße einer tempdb-Protokolldatei in MB an. Das Setup ermöglicht eine Größe von bis zu 1024 MB. <br /> Standardwert:<br /><br /> 4 für [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]<br /><br /> 8 für alle anderen Editionen<br /><br /> Zulässiger Bereich: Min = Standardwert (4 oder 8), Max = 1024|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLTEMPDBLOGFILEGROWTH<br /><br /> **Optional**|In [!INCLUDE[SQL VERSION](../../includes/sssql15-md.md)] eingeführt. Gibt die Anfangsgröße einer tempdb-Protokolldatei in MB an.<br/><br/>Standard = 4 MB für [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], 8 MB für alle anderen Editionen<br/><br/>Min = (4 oder 8 MB)<br/><br/>Max = 1024 MB (262.144 MB für [!INCLUDE[SQL VERSION](../../includes/sssqlv14-md.md)])|  
  
###### <a name="sample-syntax"></a>Beispielsyntax:  
 So führen Sie den Schritt zum Fertigstellen eines Failoverclusters in einem erweiterten Installationsszenario für [!INCLUDE[ssDE](../../includes/ssde-md.md)] und [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]aus Führen Sie den folgenden Befehl auf dem Computer aus, der im Failovercluster als aktiver Knoten fungiert, um diesen in Betrieb zu nehmen. Sie müssen die Aktion "CompleteFailoverCluster" in dem Knoten ausführen, der im [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Failovercluster als Besitzer des freigegebenen Datenträgers fungiert. 
  
 Führen Sie an der Eingabeaufforderung den folgenden Befehl aus, um die Failoverclusterinstallation für eine Standardinstanz abzuschließen:  
  
```  
setup.exe /q /ACTION=CompleteFailoverCluster /InstanceName=MSSQLSERVER /INDICATEPROGRESS /ASSYSADMINACCOUNTS="<DomainName\Username>" /ASDATADIR=<Drive>:\OLAP\Data /ASLOGDIR=<Drive>:\OLAP\Log /ASBACKUPDIR=<Drive>:\OLAP\Backup /ASCONFIGDIR=<Drive>:\OLAP\Config /ASTEMPDIR=<Drive>:\OLAP\Temp /FAILOVERCLUSTERDISKS="<Cluster Disk Resource Name - for example, 'Disk S:'>:" /FAILOVERCLUSTERNETWORKNAME="<Insert FOI Network Name>" /FAILOVERCLUSTERIPADDRESSES="IPv4;xx.xxx.xx.xx;Cluster Network;xxx.xxx.xxx.x" /FAILOVERCLUSTERGROUP="MSSQLSERVER" /INSTALLSQLDATADIR="<Drive>:\<Path>\MSSQLSERVER" /SQLCOLLATION="SQL_Latin1_General_CP1_CS_AS" /SQLSYSADMINACCOUNTS="<DomainName\UserName>"  
```  
  
 Führen Sie an der Eingabeaufforderung den folgenden Befehl aus, um die Failoverclusterinstallation für eine benannte Instanz abzuschließen:  
  
```  
setup.exe /q /ACTION=CompleteFailoverCluster /InstanceName="<Insert Instance Name>" /INDICATEPROGRESS /ASSYSADMINACCOUNTS="<DomainName\UserName>" /ASDATADIR=<Drive>:\KATMAI\Data /ASLOGDIR=<drive>:\KATMAI\Log /ASBACKUPDIR=<Drive>:\KATMAI\Backup /ASCONFIGDIR=<Drive>:\KATMAI\Config /ASTEMPDIR=<Drive>:\KATMAI\Temp /FAILOVERCLUSTERDISKS="<Cluster Disk Resource Name - for example, 'Disk S:'>" /FAILOVERCLUSTERNETWORKNAME="CompNamedFOI" /FAILOVERCLUSTERIPADDRESSES="IPv4;xx.xxx.xx.xx;ClusterNetwork1;xxx.xxx.xxx.x" /FAILOVERCLUSTERGROUP="<Insert New Group Name>" /INSTALLSQLDATADIR="<Drive>:\<Path>\MSSQLSERVER_KATMAI" /SQLCOLLATION="SQL_Latin1_General_CP1_CS_AS" /SQLSYSADMINACCOUNTS="<DomainName\Username>"  
```  
  
#### <a name="upgrade-failover-cluster-parameters"></a>Parameter für das Aktualisieren von Failoverclustern  
 Entwickeln Sie mit den in der folgenden Tabelle aufgelisteten Parametern Befehlszeilenskripts für die Failoverclusterupgrades. Weitere Informationen finden Sie unter [Aktualisieren einer SQL Server-Failoverclusterinstanz &#40;Setup&#41;](../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance-setup.md) und [Always On-Failoverclusterinstanzen &#40;SQL Server&#41;](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md). 
  
|SQL Server-Komponente|Parameter|Description|  
|-----------------------------------------|---------------|-----------------|  
|SQL Server-Setupsteuerelement|/ACTION<br /><br /> **Erforderlich**|Erforderlich, um den Installationsworkflow anzugeben.<br /><br /> Unterstützter Wert: **Upgrade**|  
|SQL Server-Setupsteuerelement|/IACCEPTSQLSERVERLICENSETERMS<br /><br /> **Nur erforderlich, wenn der /Q-Parameter oder der /QS-Parameter für die unbeaufsichtigte Installation angegeben wird.**|Erforderlich, um das Einverständnis mit den Lizenzbedingungen zu erklären.|  
|SQL Server-Setupsteuerelement|/ENU<br /><br /> **Optional**|Verwenden Sie diesen Parameter, um die englische Version von SQL Server unter einem lokalisierten Betriebssystem zu installieren, wenn die Installationsmedien sowohl Language Packs für Englisch als auch für die Sprache des Betriebssystems enthalten.|  
|SQL Server-Setupsteuerelement|/*UpdateEnabled*<br /><br /> **Optional**|Geben Sie an, ob das SQL Server-Setup Produktupdates ermitteln und einschließen soll. Gültige Werte sind True und False oder 1 und 0. Standardmäßig schließt das SQL Server-Setup alle gefundenen Updates ein.|  
|SQL Server-Setupsteuerelement|/*UpdateSource*<br /><br /> **Optional**|Geben Sie an, wo Produktupdates vom SQL Server-Setup abgerufen werden sollen. Gültige Werte sind „MU“ für die Suche in [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update, ein gültiger Ordnerpfad, ein relativer Pfad wie „.\MyUpdates“ oder eine UNC-Freigabe. Das SQL Server-Setup durchsucht standardmäßig [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update oder einen Windows Update-Dienst über Windows Server Update Services.|  
|SQL Server-Setupsteuerelement|/CONFIGURATIONFILE<br /><br /> **Optional**|Gibt die zu verwendende [ConfigurationFile](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md) an.|  
|SQL Server-Setupsteuerelement|/ERRORREPORTING<br /><br /> **Optional**|Hat in SQL Server 2016 keine Auswirkungen. <br/><br/>Informationen dazu, wie Feedback zu Fehlern an Microsoft gesendet wird, finden Sie unter [Konfigurieren von SQL Server 2016 zum Senden von Feedback an Microsoft](http://support.microsoft.com/kb/3153756). <br/><br/>In älteren Versionen wird damit die Fehlerberichterstattung für SQL Server angegeben.<br /><br /> Weitere Informationen finden Sie in den [Datenschutzbestimmungen für den Microsoft-Fehlerberichterstattungsdienst](http://go.microsoft.com/fwlink/?LinkID=72173). Unterstützte Werte:<br /><br /> 0 = deaktiviert<br /><br /> 1 = aktiviert|  
|SQL Server-Setupsteuerelement|/HELP, H, ?<br /><br /> **Optional**|Zeigt die Verwendungsoptionen für die Parameter an.|  
|SQL Server-Setupsteuerelement|/INDICATEPROGRESS<br /><br /> **Optional**|Gibt an, dass die ausführliche Setupprotokolldatei an die Konsole weitergeleitet wird.|  
|SQL Server-Setupsteuerelement|/ INSTANCEDIR<br /><br /> **Optional**|Gibt ein nicht standardmäßiges Installationsverzeichnis für freigegebene Komponenten an.|  
|SQL Server-Setupsteuerelement|/INSTANCEID<br /><br /> **Erforderlich für Upgrades von [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] oder höher.**<br /><br /> **Optional für das Upgrade von [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]**|Gibt einen nicht standardmäßigen Wert für eine [InstanceID](#InstanceID)an.|  
|SQL Server-Setupsteuerelement|/INSTANCENAME<br /><br /> **Erforderlich**|Gibt den Namen einer SQL Server-Instanz an.<br /><br /> Weitere Informationen finden Sie unter [Instance Configuration](http://msdn.microsoft.com/library/5bf822fc-6dec-4806-a153-e200af28e9a5).|  
|SQL Server-Setupsteuerelement|/PID<br /><br /> **Optional**|Gibt den Product Key für die Edition von SQL Server an. Wenn dieser Parameter nicht angegeben wird, wird Evaluation verwendet.|  
|SQL Server-Setupsteuerelement|/Q<br /><br /> **Optional**|Gibt an, dass Setup ohne Benutzeroberfläche in einem stillen Modus ausgeführt wird. Dies wird für unbeaufsichtigte Installationen verwendet.|  
|SQL Server-Setupsteuerelement|/SQMREPORTING<br /><br /> **Optional**|Hat in SQL Server 2016 keine Auswirkungen. In älteren Versionen wird damit die Erstellung von Funktionsverwendungsberichten für SQL Server angegeben.<br /><br />Unterstützte Werte:<br /><br /> 0 = deaktiviert<br /><br /> 1 = aktiviert|  
|SQL Server-Setupsteuerelement|/HIDECONSOLE<br /><br /> **Optional**|Gibt an, dass das Konsolenfenster ausgeblendet oder geschlossen ist.|  
|SQL Server-Setupsteuerelement|/FAILOVERCLUSTERROLLOWNERSHIP|Gibt das [Failoververhalten](#RollOwnership) während des Upgradevorgangs an.|  
|SQL Server-Browserdienst|/BROWSERSVCSTARTUPTYPE<br /><br /> **Optional**|Gibt den [Startmodus](#Accounts) für den SQL Server-Browserdienst an. Unterstützte Werte:<br /><br /> **Automatisch**<br /><br /> **Deaktiviert**<br /><br /> **Manuell**|  
|SQL Server-Volltext|/FTUPGRADEOPTION<br /><br /> **Optional**|Gibt die Upgradeoption für den Volltextkatalog an. Unterstützte Werte:<br /><br /> **REBUILD**<br /><br /> **RESET**<br /><br /> **IMPORT**|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCACCOUNT<br /><br /> **Erforderlich**|Gibt das Konto für [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]an.<br /><br /> Der Standardwert ist: „NT Authority\NETWORK SERVICE“.|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCPASSWORD<br /><br /> [Erforderlich](#Accounts)|Gibt das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Kennwort an.|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCStartupType<br /><br /> **Optional**|Gibt den [Startmodus](#Accounts) für den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst an.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSUPGRADEDATABASEACCOUNT<br /><br /> **Optional**|Die Eigenschaft wird nur verwendet, wenn ein Upgrade eines Berichtsserver im SharePoint-Modus der Version 2008 R2 oder früher ausgeführt wird. Weitere Upgradevorgänge werden für Berichtsserver ausgeführt, die die ältere Architektur des SharePoint-Modus verwenden, die in SQL Server 2012 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]geändert wurde. Wenn diese Option in der Befehlszeileninstallation nicht eingeschlossen ist, wird das Standarddienstkonto für die alte Instanz des Berichtsservers verwendet. Wenn diese Eigenschaft verwendet wird, geben Sie mithilfe der **/RSUPGRADEPASSWORD** -Eigenschaft das Kennwort für das Konto an.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSUPGRADEPASSWORD<br /><br /> **Optional**|Kennwort des vorhandenen Berichtsserver-Dienstkontos.|  
  
####  <a name="AddNode"></a> Parameter zum Hinzufügen von Knoten  
 Entwickeln Sie mit den in der folgenden Tabelle aufgeführten Parametern Befehlszeilenskripts für AddNode. 
  
|SQL Server-Komponente|Parameter|Description|  
|-----------------------------------------|---------------|-----------------|  
|SQL Server-Setupsteuerelement|/ACTION<br /><br /> **Erforderlich**|Erforderlich, um den AddNode-Workflow anzugeben.<br /><br /> Unterstützter Wert: **AddNode**|  
|SQL Server-Setupsteuerelement|/IACCEPTSQLSERVERLICENSETERMS<br /><br /> **Nur erforderlich, wenn der /Q-Parameter oder der /QS-Parameter für die unbeaufsichtigte Installation angegeben wird.**|Erforderlich, um das Einverständnis mit den Lizenzbedingungen zu erklären.|  
|SQL Server-Setupsteuerelement|/ENU<br /><br /> **Optional**|Verwenden Sie diesen Parameter, um die englische Version von SQL Server unter einem lokalisierten Betriebssystem zu installieren, wenn die Installationsmedien sowohl Language Packs für Englisch als auch für die Sprache des Betriebssystems enthalten.|  
|SQL Server-Setupsteuerelement|/*UpdateEnabled*<br /><br /> **Optional**|Geben Sie an, ob das SQL Server-Setup Produktupdates ermitteln und einschließen soll. Gültige Werte sind True und False oder 1 und 0. Standardmäßig schließt das SQL Server-Setup alle gefundenen Updates ein.|  
|SQL Server-Setupsteuerelement|/*UpdateSource*<br /><br /> **Optional**|Geben Sie an, wo Produktupdates vom SQL Server-Setup abgerufen werden sollen. Gültige Werte sind „MU“ für die Suche in [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update, ein gültiger Ordnerpfad, ein relativer Pfad wie „.\MyUpdates“ oder eine UNC-Freigabe. Das SQL Server-Setup durchsucht standardmäßig [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update oder einen Windows Update-Dienst über Windows Server Update Services.|  
|SQL Server-Setupsteuerelement|/CONFIGURATIONFILE<br /><br /> **Optional**|Gibt die zu verwendende [ConfigurationFile](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md) an.|  
|SQL Server-Setupsteuerelement|/HELP, H, ?<br /><br /> **Optional**|Zeigt die Verwendungsoptionen für die Parameter an.|  
|SQL Server-Setupsteuerelement|/INDICATEPROGRESS<br /><br /> **Optional**|Gibt an, dass die ausführliche Setupprotokolldatei an die Konsole weitergeleitet wird.|  
|SQL Server-Setupsteuerelement|/INSTANCENAME<br /><br /> **Erforderlich**|Gibt den Namen einer SQL Server-Instanz an.<br /><br /> Weitere Informationen finden Sie unter [Instance Configuration](http://msdn.microsoft.com/library/5bf822fc-6dec-4806-a153-e200af28e9a5).|  
|PolyBase|/PBENGSVCACCOUNT<br /><br /> **Optional**|Gibt das Konto für den Moduldienst an. Der Standardwert ist **NT Authority\NETWORK SERVICE**.|  
|PolyBase|/PBDMSSVCPASSWORD<br /><br /> **Optional**|Gibt das Kennwort für das Moduldienstkonto an.|  
|PolyBase|/PBENGSVCSTARTUPTYPE<br /><br /> **Optional**|Gibt den Startmodus für den PolyBase-Moduldienst an: Automatisch (Standard), Deaktiviert und Manuell.|  
|PolyBase|/PBPORTRANGE<br /><br /> **Optional**|Gibt einen Portbereich für PolyBase-Dienste mit mindestens sechs Ports an. Beispiel:<br /><br /> `/PBPORTRANGE=16450-16460`|  
|PolyBase|/PBSCALEOUT<br /><br /> **Optional**|Gibt an, ob die SQL Server-Instanz als Teil einer PolyBase-Erweiterungsgruppe aus Computeknoten verwendet wird. Unterstützte Werte: **True**, **False**|  
|SQL Server-Setupsteuerelement|/PID<br /><br /> **Optional**|Gibt den Product Key für die Edition von SQL Server an. Wenn dieser Parameter nicht angegeben wird, wird Evaluation verwendet.|  
|SQL Server-Setupsteuerelement|/Q<br /><br /> **Optional**|Gibt an, dass Setup ohne Benutzeroberfläche in einem stillen Modus ausgeführt wird. Dies wird für unbeaufsichtigte Installationen verwendet.|  
|SQL Server-Setupsteuerelement|/QS<br /><br /> **Optional**|Gibt an, dass Setup ausgeführt wird. Zudem wird der Fortschritt über die Benutzeroberfläche angezeigt. Es ist jedoch keine Eingabe möglich, und es werden keine Fehlermeldungen angezeigt.|  
|SQL Server-Setupsteuerelement|/HIDECONSOLE<br /><br /> **Optional**|Gibt an, dass das Konsolenfenster ausgeblendet oder geschlossen ist.|  
|SQL Server-Setupsteuerelement|/FAILOVERCLUSTERIPADDRESSES<br /><br /> **Erforderlich**|Gibt eine codierte IP-Adresse an. Die Codierungen sind durch Semikolons getrennt (;) und folgen dem Format \<IP-Typ>;\<Adresse>;\<Netzwerkname>;\<Subnetzmaske>. Zu den unterstützten IP-Typen gehören DHCP, IPv4 und IPv6.<br />Sie können mehrere Failovercluster-IP-Adressen mit einem Leerzeichen dazwischen angeben. Vergleichen Sie die folgenden Beispiele:<br /><br /> FAILOVERCLUSTERIPADDRESSES=DEFAULT<br /><br /> FAILOVERCLUSTERIPADDRESSES=IPv4;DHCP;ClusterNetwork1<br /><br /> FAILOVERCLUSTERIPADDRESSES=IPv4;172.16.0.0;ClusterNetwork1;172.31.255.255<br /><br /> FAILOVERCLUSTERIPADDRESSES=IPv6;DHCP;ClusterNetwork1<br /><br /> FAILOVERCLUSTERIPADDRESSES=IPv6;2001:db8:23:1002:20f:1fff:feff:b3a3;ClusterNetwork1<br /><br /> <br /><br /> Weitere Informationen finden Sie unter [Hinzufügen oder Entfernen von Knoten in einem SQL Server-Failovercluster &#40;Setup&#41;](../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md).|  
|SQL Server-Setupsteuerelement|/CONFIRMIPDEPENDENCYCHANGE<br /><br /> **Erforderlich**|Gibt an, dass die IP-Adressabhängigkeit für Multisubnetz-Failovercluster auf OR festgelegt werden soll. Weitere Informationen finden Sie unter [Hinzufügen oder Entfernen von Knoten in einem SQL Server-Failovercluster &#40;Setup&#41;](../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md). Unterstützte Werte:<br /><br /> 0 = False (Standard)<br /><br /> 1 = True|  
|SQL Server-Agent|/AGTSVCACCOUNT<br /><br /> **Erforderlich**|Gibt das Konto für den SQL Server-Agent-Dienst an.|  
|SQL Server-Agent|/AGTSVCPASSWORD<br /><br /> [Erforderlich](#Accounts)|Gibt das Kennwort für das SQL Server-Agent-Dienstkonto an.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSVCACCOUNT<br /><br /> **Erforderlich**|Gibt das Konto für den [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Dienst an.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSVCPASSWORD<br /><br /> [Erforderlich](#Accounts)|Gibt das Kennwort für den [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Dienst an.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCACCOUNT<br /><br /> **Erforderlich**|Gibt das Startkonto für den SQL Server-Dienst an.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCPASSWORD<br /><br /> [Erforderlich](#Accounts)|Gibt das Kennwort für SQLSVCACCOUNT an.|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCPASSWORD<br /><br /> [Erforderlich](#Accounts)|Gibt das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Kennwort an.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSINSTALLMODE<br /><br /> **Nur im reinen Dateimodus verfügbar.**|Gibt den Installationsmodus für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]an.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCPASSWORD<br /><br /> [Erforderlich](#Accounts)|Gibt das Kennwort für das Startkonto für den [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienst an.|  
  
##### <a name="additional-notes"></a>Weitere Hinweise:  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] und [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] sind die einzigen Komponenten, die clusterfähig sind. Andere Funktionen sind nicht clusterfähig und haben keine hohe Verfügbarkeit über ein Failover. 
  
###### <a name="sample-syntax"></a>Beispielsyntax:  
 So fügen Sie einer vorhandenen Failoverclusterinstanz mit [!INCLUDE[ssDE](../../includes/ssde-md.md)] und [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]einen Knoten hinzu 
  
```  
setup.exe /q /ACTION=AddNode /INSTANCENAME="<Insert Instance Name>" /SQLSVCACCOUNT="<SQL account that is used on other nodes>" /SQLSVCPASSWORD="<password for SQL account>" /AGTSVCACCOUNT="<SQL Server Agent account that is used on other nodes>", /AGTSVCPASSWORD="<SQL Server Agent account password>" /ASSVCACCOUNT="<AS account that is used on other nodes>" /ASSVCPASSWORD=”<password for AS account>” /INDICATEPROGRESS /IACCEPTSQLSERVERLICENSETERMS /FAILOVERCLUSTERIPADDRESSES="IPv4;xx.xxx.xx.xx;ClusterNetwork1;xxx.xxx.xxx.x" /CONFIRMIPDEPENDENCYCHANGE=0  
```  
  
#### <a name="remove-node-parameters"></a>Parameter zum Entfernen von Knoten  
 Entwickeln Sie mit den in der folgenden Tabelle aufgeführten Parametern Befehlszeilenskripts für RemoveNode. Um einen Failovercluster zu deinstallieren, müssen Sie RemoveNode für jeden Failoverclusterknoten ausführen. Weitere Informationen finden Sie unter [Always On-Failoverclusterinstanzen &#40;SQL Server&#41;](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md). 
  
|SQL Server-Komponente|Parameter|Description|  
|-----------------------------------------|---------------|-----------------|  
|SQL Server-Setupsteuerelement|/ACTION<br /><br /> **Erforderlich**|Erforderlich, um den RemoveNode-Workflow anzugeben.<br /><br /> Unterstützter Wert: **RemoveNode**|  
|SQL Server-Setupsteuerelement|/CONFIGURATIONFILE<br /><br /> **Optional**|Gibt die zu verwendende [ConfigurationFile](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md) an.|  
|SQL Server-Setupsteuerelement|/HELP, H, ?<br /><br /> **Optional**|Zeigt die Verwendungsoptionen für die Parameter an.|  
|SQL Server-Setupsteuerelement|/INDICATEPROGRESS<br /><br /> **Optional**|Gibt an, dass die ausführliche Setupprotokolldatei an die Konsole weitergeleitet wird.|  
|SQL Server-Setupsteuerelement|/INSTANCENAME<br /><br /> **Erforderlich**|Gibt den Namen einer SQL Server-Instanz an.<br /><br /> Weitere Informationen finden Sie unter [Instance Configuration](http://msdn.microsoft.com/library/5bf822fc-6dec-4806-a153-e200af28e9a5).|  
|SQL Server-Setupsteuerelement|/Q<br /><br /> **Optional**|Gibt an, dass Setup ohne Benutzeroberfläche in einem stillen Modus ausgeführt wird. Dies wird für unbeaufsichtigte Installationen verwendet.|  
|SQL Server-Setupsteuerelement|/QS<br /><br /> **Optional**|Gibt an, dass Setup ausgeführt wird. Zudem wird der Fortschritt über die Benutzeroberfläche angezeigt. Es ist jedoch keine Eingabe möglich, und es werden keine Fehlermeldungen angezeigt.|  
|SQL Server-Setupsteuerelement|/HIDECONSOLE<br /><br /> **Optional**|Gibt an, dass das Konsolenfenster ausgeblendet oder geschlossen ist.|  
|SQL Server-Setupsteuerelement|/CONFIRMIPDEPENDENCYCHANGE<br /><br /> **Erforderlich**|Gibt an, dass die IP-Adressabhängigkeit für Multisubnetz-Failovercluster von OR auf AND festgelegt werden soll. Weitere Informationen finden Sie unter [Hinzufügen oder Entfernen von Knoten in einem SQL Server-Failovercluster &#40;Setup&#41;](../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md). Unterstützte Werte:<br /><br /> 0 = False (Standard)<br /><br /> 1 = True|  
  
###### <a name="sample-syntax"></a>Beispielsyntax:  
 So entfernen Sie mithilfe von [!INCLUDE[ssDE](../../includes/ssde-md.md)] und [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]einen Knoten aus einer vorhandenen Failoverclusterinstanz 
  
```  
setup.exe /q /ACTION=RemoveNode /INSTANCENAME="<Insert Instance Name>" [/INDICATEPROGRESS] /CONFIRMIPDEPENDENCYCHANGE=0  
```  
  
##  <a name="Accounts"></a> Dienstkontoparameter  
 Sie können die SQL Server-Dienste mithilfe eines integrierten oder lokalen Kontos oder mithilfe eines Domänenkontos konfigurieren. 
  
> **HINWEIS:** Wenn Sie ein verwaltetes Dienstkonto, ein virtuelles Konto oder ein integriertes Konto verwenden, sollten Sie die entsprechenden Kennwortparameter nicht angeben. Weitere Informationen zu diesen Dienstkonten finden Sie im Abschnitt **In [!INCLUDE[win7](../../includes/win7-md.md)] und [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] verfügbare neue Kontotypen** unter [Konfigurieren von Windows-Dienstkonten und -Berechtigungen](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md). 
  
 Weitere Informationen zur Konfiguration des Dienstkontos finden Sie unter [Konfigurieren von Windows-Dienstkonten und -Berechtigungen](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md). 
  
|SQL Server-Komponente|Kontoparameter|Kennwortparameter|Starttyp|  
|-----------------------------------------|-----------------------|------------------------|------------------|  
|SQL Server-Agent|/AGTSVCACCOUNT|/AGTSVCPASSWORD|/AGTSVCSTARTUPTYPE|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|/ASSVCACCOUNT|/ASSVCPASSWORD|/ASSVCSTARTUPTYPE|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|/SQLSVCACCOUNT|/SQLSVCPASSWORD|/SQLSVCSTARTUPTYPE|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|/ISSVCACCOUNT|/ISSVCPASSWORD|/ISSVCStartupType|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|/RSSVCACCOUNT|/RSSVCPASSWORD|/RSSVCStartupType|  
  
##  <a name="Feature"></a> Funktionsparameter  
 Um bestimmte Funktionen zu installieren, verwenden Sie den /FEATURES-Parameter und geben in der folgenden Tabelle die übergeordnete Funktion oder die Funktionswerte an. Eine Liste der Funktionen, die von den Editionen von SQL Server unterstützt werden, finden Sie unter [Editionen und unterstütze Funktionen für SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md). 
  
|Parameter übergeordneter Funktionen|Funktionsparameter|Description|  
|:---|:---|:---|  
|SQL||Installiert [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], Replikation, Volltext und [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)].|  
||SQLEngine|Installiert nur das [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].|  
||Replikation|Installiert die Replikationskomponente und das [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].|  
||FullText|Installiert die FullText-Komponente und das [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].|  
||DQ|Kopiert die erforderlichen Dateien zum Abschließen der Installation von [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] . Nach dem Fertigstellen der Installation von SQL Server müssen Sie zum Fertigstellen der Installation von [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] die Datei DQSInstaller.exe ausführen. Weitere Informationen finden Sie unter [Ausführen von DQSInstaller.exe zum Abschließen der Installation von Data Quality Server](../../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md). Dabei wird auch das [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]installiert.|  
||PolyBase|Installiert PolyBase-Komponenten.|  
||AdvancedAnalytics|Installiert R-Dienste (innerhalb der Datenbank).|  
|AS||Installiert alle [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Komponenten.|  
|RS||Installiert alle [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Komponenten.|  
|RS_SHP||Installiert [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Komponenten für SharePoint|  
|RS_SHPWFE||Installiert das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Add-In für SharePoint-Produkte |  
|DQC||Installiert [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)].|  
|IS||Installiert alle [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Komponenten.|  
|MDS||Installiert [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)].|  
|SQL_SHARED_MR||Installiert Microsoft R Server.|  
|Tools*||Installiert die Clienttools und die SQL Server-Onlinedokumentation.|  
||BC|Installiert Abwärtskompatibilitätskomponenten.|  
||Conn|Installiert Konnektivitätskomponenten.|
||DREPLAY_CTLR|Installiert Distributed Replay Controller|  
||DREPLAY_CLT|Installiert Distributed Replay Client|  
||SNAC_SDK|Installiert das SDK für [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQL Server Native Client|  
||SDK|Installiert das Software Development Kit.|  
||LocalDB**|Installiert LocalDB, einen Ausführungsmodus von [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] , der speziell für Programmentwickler konzipiert wurde.|  

*SQL Server-Verwaltungstools (SSMS) sind jetzt in einem eigenständigen Installationsprogramm enthalten, das vom SQL Server-Installationsprogramm getrennt ist. Weitere Informationen finden Sie unter [Installieren von SQL Server Management Studio über die Befehlszeile](https://msdn.microsoft.com/library/bb500441.aspx#Anchor_1).

 **LocalDB ist eine Option bei der Installation einer beliebigen SKU von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Express. Weitere Informationen finden Sie unter [SQL Server 2016 Express LocalDB](../../database-engine/configure-windows/sql-server-2016-express-localdb.md). 
  
### <a name="feature-parameter-examples"></a>Beispiele für Funktionsparameter:  
  
|Parameter und Werte|Beschreibung|  
|--------------------------|-----------------|  
|/FEATURES=SQLEngine|Installiert das [!INCLUDE[ssDE](../../includes/ssde-md.md)] ohne Replikation und Volltext.|  
|/FEATURES=SQLEngine, FullText|Installiert das [!INCLUDE[ssDE](../../includes/ssde-md.md)] und Volltext.|  
|/FEATURES=SQL, Tools|Installiert das vollständige [!INCLUDE[ssDE](../../includes/ssde-md.md)] und alle Tools.|  
|/FEATURES=BOL|Installiert die SQL Server-Onlinedokumentation zum Anzeigen und Verwalten von Hilfeinhalten.|  
|/FEATURES=SQLEngine, PolyBase|Installiert das PolyBase-Modul.|  
  
##  <a name="RoleParameters"></a> Rollenparameter  
 Die Setuprolle oder der /Role-Parameter wird verwendet, um eine vorkonfigurierte Auswahl von Funktionen zu installieren. Die [!INCLUDE[ssAS_md](../../includes/ssas-md.md)] -Rollen installieren eine [!INCLUDE[ssAS_md](../../includes/ssas-md.md)] -Instanz in einer vorhandenen SharePoint-Farm oder einer neuen nicht konfigurierten Farm. Für jedes Szenario werden zwei Setuprollen bereitgestellt. Sie können jeweils nur eine Setuprolle zur Installation auswählen. Wenn Sie eine Setuprolle auswählen, installiert Setup die Funktionen und Komponenten, die dieser Rolle angehören. Die für diese Rolle festgelegten Funktionen und Komponenten können nicht geändert werden. Weitere Informationen zur Verwendung des Funktionsrollenparameters finden Sie unter [Installieren von Power Pivot über die Eingabeaufforderung](http://msdn.microsoft.com/7f1f2b28-c9f5-49ad-934b-02f2fa6b9328). 
  
 Die AllFeatures_WithDefaults-Rolle ist das Standardverhalten für Editionen von [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] und reduziert die Anzahl der Dialogfelder, die dem Benutzer angezeigt werden. Sie kann bei der Installation einer anderen SQL Server-Edition als [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]in der Befehlszeile angegeben werden. 
  
|Rolle|Description|Installiert...|  
|----------|-----------------|---------------|  
|SPI_AS_ExistingFarm|Installiert [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] als benannte Instanz von [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] in einer vorhandenen [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] -Farm oder auf einem eigenständigen Server.|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Berechnungsmodul, vorkonfiguriert für Datenspeicherung und Verarbeitung im Arbeitsspeicher.<br /><br /> [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Projektmappenpakete<br /><br /> Installationsprogramm für den [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)]<br /><br /> SQL Server-Onlinedokumentation|  
|SPI_AS_NewFarm|Installiert [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] und [!INCLUDE[ssDE](../../includes/ssde-md.md)] als benannte Instanz von [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] in einer neuen und nicht konfigurierten Office [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] -Farm oder auf einem eigenständigen Server. SQL Server-Setup konfiguriert die Farm während der Installation der Funktionsrolle.|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Berechnungsmodul, vorkonfiguriert für Datenspeicherung und Verarbeitung im Arbeitsspeicher.<br /><br /> [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Projektmappenpakete<br /><br /> SQL Server-Onlinedokumentation<br /><br /> [!INCLUDE[ssDE](../../includes/ssde-md.md)]<br /><br /> Konfigurationstools<br /><br /> [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]|  
|AllFeatures_WithDefaults|Installiert alle in der aktuellen Edition verfügbaren Funktionen.<br /><br /> Fügt der festen Serverrolle **sysadmin** von SQL Server den aktuellen Benutzer hinzu.<br /><br /> Unter [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] oder höheren Versionen und wenn das Betriebssystem kein Domänencontroller ist, werden [!INCLUDE[ssDE](../../includes/ssde-md.md)]und [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] standardmäßig für die Verwendung des NT-AUTORITÄT\NETZWERKDIENST-Kontos und [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] standardmäßig für die Verwendung des NT-AUTORITÄT\LOKALER DIENST-Kontos konfiguriert.<br /><br /> Diese Rolle wird in Editionen von [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]standardmäßig aktiviert. Für alle anderen Editionen ist diese Rolle nicht aktiviert, kann jedoch über die Benutzeroberfläche oder mit Befehlszeilenparametern angegeben werden.|Für Editionen von [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]werden nur die in der Edition verfügbaren Funktionen installiert. Für andere Editionen werden alle SQL Server-Funktionen installiert.<br /><br /> Der **AllFeatures_WithDefaults** -Parameter kann mit anderen Parametern kombiniert werden, die die Einstellungen des **AllFeatures_WithDefaults** -Parameters überschreiben. Bei Verwendung des **AllFeatures_WithDefaults** -Parameters und des **/FEATURES = RS** -Parameters wird beispielsweise der Befehl zur Installation aller Funktionen überschrieben und nur [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]installiert. Der **AllFeatures_WithDefaults-Parameter** zur Verwendung des Standarddienstkontos für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]wird jedoch berücksichtigt.<br /><br /> Wenn der **AllFeatures_WithDefaults** -Parameter zusammen mit **/ADDCURRENTUSERASSQLADMIN=FALSE** verwendet wird, wird das bereitstellende Dialogfeld nicht automatisch mit dem Namen des aktuellen Benutzers aufgefüllt. Fügen Sie **/AGTSVCACCOUNT** und **/AGTSVCPASSWORD** hinzu, um ein Dienstkonto und ein Kennwort für den SQL Server-Agent anzugeben.|  
  
##  <a name="RollOwnership"></a> Steuern des Failoververhaltens mithilfe des Parameters /FAILOVERCLUSTERROLLOWNERSHIP  
 Um einen SQL Server-Failovercluster auf [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]zu aktualisieren, müssen Sie auf den einzelnen Failoverclusterknoten jeweils Setup ausführen. Dabei sollte mit den passiven Knoten begonnen werden. Setup ermittelt, zu welchem Zeitpunkt das Failover für den aktualisierten Knoten durchgeführt werden soll. Dies ist abhängig von der Gesamtzahl an Knoten in der Failoverclusterinstanz sowie von der Anzahl der bereits aktualisierten Knoten. Wenn mindestens die Hälfte der Knoten bereits aktualisiert wurde, führt Setup in der Standardeinstellung ein Failover zu einem aktualisierten Knoten durch. 
  
 Zum Steuern des Failoververhaltens von Clusterknoten während des Upgradevorgangs führen Sie den Upgradevorgang an der Eingabeaufforderung aus. Verwenden Sie dabei den Parameter /FAILOVERCLUSTERROLLOWNERSHIP, um das Failoververhalten zu steuern, bevor der Knoten vom Upgradevorgang in den Offlinemodus versetzt wird. Der Parameter kann folgendermaßen verwendet werden:  
  
-   /FAILOVERCLUSTERROLLOWNERSHIP=0 – Mit diesem Parameter wird der Clusterbesitz (Gruppe verschieben) nicht auf aktualisierte Knoten übertragen, und der Knoten wird nach Abschluss des Upgrades der Liste der möglichen Besitzer des SQL Server-Clusters nicht hinzugefügt. 
  
-   /FAILOVERCLUSTERROLLOWNERSHIP=1 – Mit diesem Parameter wird der Clusterbesitz (Gruppe verschieben) auf aktualisierte Knoten übertragen, und der Knoten wird nach Abschluss des Upgrades der Liste der möglichen Besitzer des SQL Server-Clusters hinzugefügt. 
  
-   /FAILOVERCLUSTERROLLOWNERSHIP=2 – Dies ist die Standardeinstellung. Sie wird verwendet, wenn der Parameter nicht angegeben ist. Diese Einstellung gibt an, dass SQL Server-Setup den Clusterbesitz (Gruppe verschieben) nach Bedarf verwaltet. 
  
##  <a name="InstanceID"></a> Instanz-ID- oder InstanceID-Konfiguration  
 Der Instanz-ID- oder /InstanceID-Parameter wird verwendet, um festzulegen, wo die Instanzkomponenten und der Registrierungspfad der Instanz installiert werden sollen. Der Wert für "INSTANCEID" ist eine Zeichenfolge, die eindeutig sein muss. 
  
-   SQL Instanz-ID:MSSQL13.\<INSTANCEID>  
  
-   AS Instanz-ID:MSAS13.\<INSTANCEID>  
  
-   RS Instanz-ID:MSRS13.\<INSTANCEID>  
  
 Die instanzabhängigen Komponenten werden an den folgenden Speicherorten installiert:  
  
 %Program Files%\\Microsoft SQL Server\\<SQLInstanceID\>  
  
 %Program Files%\\Microsoft SQL Server\\<ASInstanceID\>  
  
 %Program Files Microsoft SQL Server\\<RSInstanceID\>  
  
> **HINWEIS**: Wenn INSTANZID in der Befehlszeile nicht angegeben wurde, wird in der Standardeinstellung beim Setupvorgang \<INSTANZID> durch \<INSTANZNAME> ersetzt. 
  
## <a name="see-also"></a>Siehe auch  
 [Installieren von SQL Server 2016 vom Installations-Assistenten](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)   
 [SQL Server-Failoverclusterinstallation](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)   
 [[Installieren von SQL Server 2016 Business Intelligence-Funktionen](../../sql-server/install/install-sql-server-business-intelligence-features.md)]  
  

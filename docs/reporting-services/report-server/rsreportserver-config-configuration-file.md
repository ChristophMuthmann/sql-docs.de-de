---
title: RSReportServer.config-Konfigurationsdatei | Microsoft-Dokumentation
ms.custom: 
ms.date: 06/12/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 60e0a0b2-8a47-4eda-a5df-3e5e403dbdbc
caps.latest.revision: "20"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Active
ms.openlocfilehash: 68a812ca454de6c9ee1784d33cfb5e0730957fbd
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="rsreportserverconfig-configuration-file"></a>RSReportServer.config-Konfigurationsdatei
In der Datei [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]**RsReportServer.config** werden Einstellungen gespeichert, die vom Berichtsserver-Webdienst und der Hintergrundverarbeitung verwendet werden. Alle [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Anwendungen werden innerhalb eines einzelnen Prozesses ausgeführt, der die in der Datei RSReportServer.config gespeicherten Konfigurationseinstellungen liest. Sowohl der Berichtsserver im einheitlichen als auch der Berichtsserver im SharePoint-Modus verwenden "Rsreportserver.config". Die zwei Modi verwenden jedoch nicht alle gleichen Einstellungen in der Konfigurationsdatei. Die SharePoint-Modusversion der Datei ist kleiner, da viele der Einstellungen für den SharePoint-Modus in den SharePoint-Konfigurationsdatenbanken und nicht in der Datei gespeichert werden. In diesem Thema werden die für den einheitlichen und den SharePoint-Modus installierte Standardkonfigurationsdatei sowie einige wichtige Einstellungen und Verhaltensweisen beschrieben, die von der Konfigurationsdatei gesteuert werden.  

Im SharePoint-Modus enthält die Konfigurationsdatei die Einstellungen, die für alle Dienstanwendungsinstanzen gelten, die auf diesem Computer ausgeführt werden. Die SharePoint-Konfigurationsdatenbank enthält Konfigurationseinstellungen, die für bestimmte Dienstanwendungen gelten. Die Einstellungen, die in der Konfigurationsdatenbank gespeichert und über die SharePoint-Verwaltungsseiten verwaltet werden, können bei jeder [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendung variieren.  
  
 Die Einstellungen werden in folgenden Inhalten in der Reihenfolge erläutert, in der sie in der standardmäßig installierten Konfigurationsdatei aufgeführt sind. Weitere Anleitungen zum Bearbeiten dieser Datei finden Sie unter [Ändern einer Reporting Services-Konfigurationsdatei &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md).  
  
 
##  <a name="bkmk_file_location"></a> Dateispeicherort  

Die Datei RSReportServer.config befindet sich abhängig vom Berichtsservermodus in den folgenden Ordnern:  


  
### <a name="native-mode-report-server"></a>Berichtsserver im einheitlichen Modus  

 
**[!INCLUDE[applies](../../includes/applies-md.md)]**  SQL Server 2016
```  
C:\Program Files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\ReportServer  
```

**[!INCLUDE[applies](../../includes/applies-md.md)]** Januar 2017 Technical Preview von Power BI-Berichten in SQL Server Reporting Services
```  
C:\Program Files\Microsoft SQL Server Reporting Services\RSServer\ReportServer
```  
  
### <a name="sharepoint-mode-report-server"></a>Berichtsserver im SharePoint-Modus

> [!NOTE]
> Der integrierte Modus von SharePoint steht in der Technical Preview von Berichten von Power BI in SQL Server Reporting Services von Januar 2017 nicht zur Verfügung.
  
```  
C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\15\WebServices\Reporting  
```  
 
Weitere Informationen zum Bearbeiten dieser Datei finden Sie unter [Ändern einer Reporting Services-Konfigurationsdatei &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md).  
  
##  <a name="bkmk_generalconfiguration"></a> Allgemeine Konfigurationseinstellungen ("rsreportserver.config")  
 In der folgenden Tabelle sind Informationen zu den allgemeinen Konfigurationseinstellungen im ersten Teil der Datei enthalten. Diese Einstellungen werden in der Reihenfolge aufgeführt, in der sie in der Konfigurationsdatei angezeigt werden. Die letzte Spalte der Tabelle gibt an, ob die Einstellung für einen Berichtsserver im einheitlichen Modus **(N)** oder für einen Berichtsserver im SharePoint-Modus **(S)** oder für beide gilt.  
  
> [!NOTE]  
>  Maximale ganze Zahl bezieht sich in diesem Thema auf den INT_MAX-Wert 2147483647.  Weitere Informationen finden Sie unter [Grenzwerte für den Integer-Typ](http://msdn.microsoft.com/library/296az74e\(v=vs.110\).aspx) (http://msdn.microsoft.com/library/296az74e(v=vs.110).aspx).  
  
|Einstellung|Description|Mode|  
|-------------|-----------------|----------|  
|**Dsn**|Gibt die Verbindungszeichenfolge für die Verbindung zum Datenbankserver an, der die Berichtsserver-Datenbank hostet. Dieser Wert ist verschlüsselt und wird der Konfigurationsdatei beim Erstellen der Berichtsserver-Datenbank hinzugefügt. Für SharePoint werden die Informationen zur Datenbankverbindung aus der SharePoint-Konfigurationsdatenbank verwendet.|N,S|  
|**ConnectionType**|Gibt den Anmeldeinformationstyp an, der vom Berichtsserver zum Herstellen der Verbindung zur Berichtsserver-Datenbank verwendet wird. Gültige Werte sind **Standard** und **Identität annehmen**. **Standard** wird angegeben, wenn der Berichtsserver zur Verwendung einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldung oder des Dienstkontos konfiguriert ist, um eine Verbindung mit der Berichtsserver-Datenbank herzustellen. **Identität annehmen** wird angegeben, wenn der Berichtsserver ein Windows-Konto verwendet, um eine Verbindung mit der Berichtsserver-Datenbank herzustellen.|N|  
|**LogonUser, LogonDomain, LogonCred**|Speichert die Domäne, den Benutzernamen und das Kennwort eines Domänenkontos, das von einem Berichtsserver für die Verbindung zu einer Berichtsserver-Datenbank verwendet wird. Die Werte für **LogonUser**, **LogonDomain**und **LogonCred** werden erstellt, wenn die Berichtsserververbindung für die Verwendung eines Domänenkontos konfiguriert wird. Weitere Informationen zu einer Berichtsserver-Datenbankverbindung finden Sie unter [Konfigurieren einer Berichtsserver-Datenbankverbindung (SSRS-Konfigurations-Manager)](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md).|N|  
|**InstanceID**|Ein Bezeichner für die Berichtsserverinstanz. Die Namen von Berichtsserverinstanzen basieren auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanznamen. Dieser Wert gibt einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanznamen an. Der Standardwert ist **MSRS12***\<Instanzname>*. Ändern Sie diese Einstellung nicht. Folgendes ist ein Beispiel für den vollständigen Wert: `<InstanceId>MSRS13.MSSQLSERVER</InstanceId>`<br /><br /> Nachfolgend finden Sie eine Beispiel des SharePoint-Modus:<br /><br /> `<InstanceId>MSRS12.@Sharepoint</InstanceId>`|N,S|  
|**InstallationID**|Ein Bezeichner für die von Setup erstellte Berichtsserverinstallation. Dieser Wert ist auf eine GUID festgelegt. Ändern Sie diese Einstellung nicht.|N|  
|**SecureConnectionLevel**|Gibt den Grad an, zu dem Webdienstaufrufe Secure Sockets Layer (SSL) verwenden müssen. Diese Einstellung wird sowohl für den Berichtsserver-Webdienst als auch für das Webportal verwendet. Dieser Wert wird festgelegt, wenn Sie eine URL für die Verwendung von HTTP oder HTTPS im [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationstool konfigurieren. Gültige Werte sind 0 bis 3, wobei 0 die geringste Sicherheit bietet. Weitere Informationen finden Sie unter [Verwenden von sicheren Webdienstmethoden](../../reporting-services/report-server-web-service/net-framework/using-secure-web-service-methods.md) und [Konfigurieren von SSL-Verbindungen auf einem Berichtsserver im einheitlichen Modus](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md).|N,S|  
|**DisableSecureFormsAuthenticationCookie**|Der Standardwert ist False.<br /><br /> Gibt an, ob der Vorgang deaktiviert wird, durch den erzwungen wird, dass das für Formular- und benutzerdefinierte Authentifizierungen verwendete Cookie als sicher gekennzeichnet wird. Ab SQL Server 2012 werden die mit benutzerdefinierten Authentifizierungserweiterungen verwendeten Formularauthentifizierungscookies beim Senden an den Client von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] automatisch als sichere Cookies gekennzeichnet. Indem diese Eigenschaft geändert wird, können Berichtsserveradministratoren und Autoren von benutzerdefinierten Sicherheitserweiterungen wieder zum früheren Verhalten zurückkehren, bei dem der Autor der benutzerdefinierten Sicherheitserweiterung bestimmen konnte, ob das Cookie als sicheres Cookie gekennzeichnet werden soll. Es wird empfohlen, für die Formularauthentifizierung sichere Cookies zu verwenden, um die Netzwerkermittlung und Wiederholungsangriffe zu verhindern.|N|  
|**CleanupCycleMinutes**|Gibt die Anzahl von Minuten an, nach der alte Sitzungen und abgelaufene Momentaufnahmen aus den Berichtsserver-Datenbanken entfernt werden. Gültige Werte sind 0 bis zu einer maximalen ganzen Zahl. Der Standardwert ist 10. Wenn Sie den Wert 0 festlegen, wird der Cleanupprozess der Datenbank deaktiviert.|N,S|  
|**MaxActiveReqForOneUser**|Gibt die maximale Anzahl von Berichten an, die gleichzeitig von einem Benutzer verarbeitet werden können. Bei Erreichen dieses Grenzwerts werden weitere Berichtsverarbeitungsanforderungen abgelehnt. Gültige Werte sind 1 bis zu einer maximalen ganzen Zahl. Der Standardwert ist 20.<br /><br /> Beachten Sie, dass die meisten Anforderungen sehr schnell verarbeitet werden. Von daher ist es unwahrscheinlich, dass ein einzelner Benutzer mehr als 20 Verbindungen gleichzeitig geöffnet hat. Falls Benutzer mehr als 15 verarbeitungsintensive Berichte gleichzeitig öffnen, müssen Sie diesen Wert möglicherweise erhöhen.<br /><br /> Diese Einstellung wird für Berichtsserver ignoriert, die im integrierten SharePoint-Modus ausgeführt werden.|N,S|  
|**MaxActiveReqForAnonymous**|Gibt die maximale Anzahl von anonymen Anforderungen an, die gleichzeitig verarbeitet werden können. Bei Erreichen dieses Grenzwerts werden weitere Verarbeitungsanforderungen abgelehnt. Gültige Werte sind 1 bis zu einer maximalen ganzen Zahl. Der Standardwert ist 200.
|**DatabaseQueryTimeout**|Gibt die Anzahl von Sekunden an, nach der für eine Verbindung zur Berichtsserver-Datenbank ein Timeout auftritt. Dieser Wert wird an die System.Data.SQLClient.SQLCommand.CommandTimeout-Eigenschaft übergeben. Gültige Werte reichen von 0 bis 2147483647. Der Standardwert lautet 120. Ein Wert von 0 gibt eine unbegrenzte Wartezeit an und wird deshalb nicht empfohlen.|N|  
|**AlertingCleanupCycleMinutes**|Der Standardwert ist 20.<br /><br /> Bestimmt, wie häufig die in der Warnungsdatenbank gespeicherten temporären Daten bereinigt werden.|S|  
|**AlertingDataCleanupMinutes**|Der Standardwert ist 360.<br /><br /> Bestimmt, wie lange Sitzungsdaten, die zum Erstellen oder Bearbeiten einer Warnungsdefinition verwendet werden, in der Warnungsdatenbank beibehalten werden. Der Standardwert ist 6 Stunden.|S|  
|**AlertingExecutionLogCleanup**Minutes|Der Standardwert ist 10080.<br /><br /> Bestimmt, wie lange Werte des Warnungsausführungsprotokolls beibehalten werden. Der Standard ist 7 Tage.|S|  
|**AlertingMaxDataRetentionDays**|Die Standardeinstellung ist 180.<br /><br /> Bestimmt, wie lange Warnungsdaten beibehalten werden, durch die verhindert wird, dass doppelte Warnmeldungen ausgegeben werden, wenn sich die Daten für die Warnung nicht geändert haben.|S|  
|**RunningRequestsScavengerCycle**|Gibt an, wie oft verwaiste und abgelaufene Anforderungen abgebrochen werden. Der Wert wird in Sekunden angegeben. Gültige Werte sind 0 bis zu einer maximalen ganzen Zahl. Der Standardwert ist 60.|N,S|  
|**RunningRequestsDbCycle**|Gibt an, wie oft der Berichtsserver gerade ausgeführte Aufträge auswertet, um zu überprüfen, ob sie Timeouts für die Berichtsausführung überschritten haben, und wann Informationen über gerade ausgeführte Aufträge auf der Seite „Aufträge verwalten“ im Webportal angezeigt werden sollen. Der Wert wird in Sekunden angegeben. Gültige Werte reichen von 0 bis 2147483647. Der Standardwert ist 60.|N,S|  
|**RunningRequestsAge**|Gibt das Intervall in Sekunden an, nach dem der Status eines gerade ausgeführten Auftrags von Neu in Wird ausgeführt geändert wird. Gültige Werte reichen von 0 bis 2147483647. Der Standardwert ist 30.|N,S|  
|**MaxScheduleWait**|Gibt die Anzahl von Sekunden an, die der Berichtsserver-Windows-Dienst darauf wartet, dass ein Zeitplan vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienst aktualisiert wird, wenn der Wert für **Nächster Ausführungszeitpunkt** angefordert wird. Gültige Werte reichen von 1 bis 60.<br /><br /> In der Standardkonfigurationsdatei ist MaxScheduleWait auf **5**festgelegt.<br /><br /> Wenn der Berichtsserver die Konfigurationsdatei nicht finden oder lesen kann, wird MaxScheduleWait standardmäßig auf 1 festgelegt.|N,S|  
|**DisplayErrorLink**|Gibt an, ob ein Hyperlink zur [!INCLUDE[msCoName](../../includes/msconame-md.md)] Hilfe- und Support-Website angezeigt wird, wenn Fehler auftreten. Dieser Hyperlink wird in Fehlermeldungen angezeigt. Die Benutzer können auf den Link klicken, um aktualisierte Inhalte zu Fehlermeldungen anzuzeigen. Gültige Werte sind **TRUE** (Standardwert) und **FALSE**.|N,S|  
|**WebServiceUseFileShareStorage**|Gibt an, ob zwischengespeicherte Berichte und temporäre Momentaufnahmen (die vom Berichtsserver-Webdienst für die Dauer einer Benutzersitzung erstellt werden) im Dateisystem gespeichert werden. Gültige Werte sind **TRUE** und **FALSE** (Standardwert). Wenn der Wert auf False festgelegt ist, werden die temporären Daten in der reportservertempdb-Datenbank gespeichert.|N,S|  
|**WatsonFlags**|Gibt an, wie viele Informationen für Fehlerbedingungen protokolliert werden, die an [!INCLUDE[msCoName](../../includes/msconame-md.md)]gemeldet werden.<br /><br /> 0x0430 = ein vollständiger Dump<br /><br /> 0x0428 = ein Minidump<br /><br /> 0x0002 = kein Dump|N,S|  
|**WatsonDumpOnExceptions**|Gibt eine Liste der Ausnahmen an, die in einem Fehlerprotokoll aufgezeichnet werden sollen. Dies ist nützlich, wenn ein bestimmtes Problem immer wieder auftritt und Sie einen Dump mit Informationen erstellen möchten, um ihn zur Analyse an [!INCLUDE[msCoName](../../includes/msconame-md.md)] zu übermitteln. Die Erstellung von Dumps vermindert die Leistung. Ändern Sie diese Einstellung daher nur, wenn Sie ein Problem diagnostizieren müssen.|N,S|  
|**WatsonDumpExcludeIfContainsExceptions**|Gibt eine Liste der Ausnahmen an, die nicht in einem Fehlerprotokoll aufgezeichnet werden sollen. Dies ist nützlich, wenn Sie ein Problem diagnostizieren und nicht möchten, dass der Server für eine bestimmte Ausnahme Dumps erstellt.|N,S|  
  
##  <a name="bkmk_URLReservations"></a> URLReservations (Datei RSReportServer.config)  
 **URLReservations** definiert den HTTP-Zugriff auf den Berichtsserver-Webdienst und das Webportal für die aktuelle Instanz. URLs werden reserviert und in HTTP.SYS gespeichert, wenn Sie den Berichtsserver konfigurieren.  
  
> [!WARNING]  
>  Für den SharePoint-Modus werden URL-Reservierungen in der SharePoint-Zentraladministration konfiguriert. Weitere Informationen finden Sie unter [Konfigurieren einer alternativen Zugriffszuordnung (http://technet.microsoft.com/library/cc263208(office.12).aspx)](http://technet.microsoft.com/library/cc263208\(office.12\).aspx).  
  
 Ändern Sie keine URL-Reservierungen direkt in der Konfigurationsdatei. Verwenden Sie immer den [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurations-Manager oder den Berichtsserver-WMI-Anbieter zum Erstellen oder Ändern von URL-Reservierungen für einen Berichtsserver im einheitlichen Modus. Wenn Sie Werte in der Konfigurationsdatei ändern, beschädigen Sie dabei unter Umständen die Reservierung, wodurch Serverfehler zur Laufzeit auftreten oder verwaiste Reservierungen in HTTP.SYS entstehen, die beim Deinstallieren der Software nicht entfernt werden. Weitere Informationen finden Sie unter [Konfigurieren von Berichtsserver-URLs (SSRS-Konfigurations-Manager)](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md) und [URLs in Konfigurationsdateien (SSRS-Konfigurations-Manager)](../../reporting-services/install-windows/urls-in-configuration-files-ssrs-configuration-manager.md).  
  
 **URLReservations** ist ein optionales Element. Wenn es nicht in der Datei RSReportServer.config vorhanden ist, ist der Server unter Umständen nicht konfiguriert. Wenn es angegeben wird, sind alle untergeordneten Elemente außer **AccountName** erforderlich.  
  
 Die letzte Spalte der Tabelle gibt an, ob die Einstellung für einen Berichtsserver im einheitlichen Modus (N) oder für einen Berichtsserver im SharePoint-Modus (S) oder für beide gilt.  
  
|Einstellung|Description|Mode|  
|-------------|-----------------|----------|  
|**Application**|Enthält Einstellungen für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Anwendungen.|N|  
|**Name**|Gibt die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Anwendungen an. Gültige Werte sind ReportServerWebService oder ReportManager.|N|  
|**VirtualDirectory**|Gibt den Namen des virtuellen Verzeichnisses der Anwendung an.|N|  
|**URLs, URL**|Enthält eine oder mehrere URL-Reservierungen für die Anwendung.|N|  
|**UrlString**|Gibt die URL-Syntax an, die für HTTP.SYS gültig ist. Weitere Informationen zur Syntax finden Sie unter [URL-Reservierungssyntax (SSRS-Konfigurations-Manager)](../../reporting-services/install-windows/url-reservation-syntax-ssrs-configuration-manager.md).|N|  
|**AccountSid**|Gibt die Sicherheits-ID (SID) des Kontos an, für das die URL-Reservierung ausgeführt wurde. Dabei sollte es sich um das Konto handeln, unter dem der Report&nbsp;Server-Dienst ausgeführt wird. Wenn die SID nicht mit dem Dienstkonto übereinstimmt, ist der Berichtsserver möglicherweise nicht in der Lage, an der URL auf eingehende Anforderungen zu lauschen.|N|  
|**AccountName**|Gibt einen lesbaren Kontonamen an, der **AccountSid**entspricht. Dieser wird nicht verwendet, ist jedoch in der Datei enthalten, damit Sie das Dienstkonto für das Konto ermitteln können, das zur URL-Reservierung verwendet wird.|N|  
  
##  <a name="bkmk_Authentication"></a> Authentication (Datei RSReportServer.config)  
 **Authentication** gibt mindestens einen Authentifizierungstyp an, der vom Berichtsserver akzeptiert wird. Die Standardeinstellungen und Werte sind eine Untermenge der Einstellungen und Werte, die für diesen Abschnitt möglich sind. Nur die Standardeinstellungen werden automatisch hinzugefügt. Um andere Einstellungen hinzuzufügen, müssen Sie die Elementstruktur der Datei RSReportServer.config mithilfe eines Text-Editors hinzufügen und die Werte festlegen.  
  
 Standardwerte sind **RSWindowsNegotiate** und **RSWindowsNTLM** , wobei **EnableAuthPersistance** auf **True**festgelegt ist:  
  
```  
   <Authentication>  
      <AuthenticationTypes>  
         <RSWindowsNegotiate/>  
         <RSWindowsNTLM/>  
      </AuthenticationTypes>  
      <EnableAuthPersistence>true</EnableAuthPersistence>  
   </Authentication>  
```  
  
 Alle anderen Werte müssen manuell hinzugefügt werden. Weitere Informationen und Beispiele finden Sie unter [Authentifizierung mit dem Berichtsserver](../../reporting-services/security/authentication-with-the-report-server.md).  
  
 Die letzte Spalte der folgenden Tabelle gibt an, ob die Einstellung für einen Berichtsserver im einheitlichen Modus (N) oder für einen Berichtsserver im SharePoint-Modus (S) oder für beide gilt.  
  
|Einstellung|Description|Mode|  
|-------------|-----------------|----------|  
|**AuthenticationTypes**|Gibt einen oder mehrere Authentifizierungstypen an. Gültige Werte sind: **RSWindowsNegotiate**, **RSWindowsKerberos**, **RSWindowsNTLM**, **RSWindowsBasic**und **Custom**.<br /><br /> Der**RSWindows** -Typ und **Custom** -Typ schließen sich gegenseitig aus.<br /><br /> **RSWindowsNegotiate**, **RSWindowsKerberos**, **RSWindowsNTLM**und **RSWindowsBasic** sind kumulativ und können zusammen verwendet werden, wie im Beispiel mit Standardwerten weiter oben in diesem Abschnitt beschrieben.<br /><br /> Die Angabe verschiedener Authentifizierungstypen ist notwendig, wenn Sie Anforderungen von einer Reihe von Clientanwendungen oder Browsern erwarten, die verschiedene Authentifizierungstypen einsetzen.<br /><br /> **RSWindowsNTLM**sollte nicht entfernt werden, da die unterstützten Browsertypen andernfalls auf einen Teilbereich eingeschränkt würden. Weitere Informationen finden Sie unter [Browserunterstützung für Reporting Services und Power View](../../reporting-services/browser-support-for-reporting-services-and-power-view.md).|N|  
|**RSWindowsNegotiate**|Der Berichtsserver akzeptiert entweder Kerberos- oder NTLM-Sicherheitstoken. Das ist die Standardeinstellung, wenn der Berichtsserver im einheitlichen Modus ausgeführt wird und das Dienstkonto Netzwerkdienst lautet. Diese Standardeinstellung wird nicht angegeben, wenn der Berichtsserver im einheitlichen Modus ausgeführt wird und das Dienstkonto als Domänenbenutzerkonto konfiguriert ist.<br /><br /> Wenn ein Domänenkonto für das Report&nbsp;Server-Dienstkonto, aber kein Dienstprinzipalname für den Berichtsserver konfiguriert wird, verhindert diese Einstellung möglicherweise die Anmeldung von Benutzern auf dem Server.|N|  
|**RSWindowsNTLM**|Der Server akzeptiert NTLM-Sicherheitstoken.<br /><br /> Wenn Sie diese Einstellung entfernen, ist die Browserunterstützung für einige der unterstützten Browsertypen beschränkt. Weitere Informationen finden Sie unter [Browserunterstützung für Reporting Services und Power View](../../reporting-services/browser-support-for-reporting-services-and-power-view.md).|N, S|  
|**RSWindowsKerberos**|Der Server akzeptiert Kerberos-Sicherheitstoken.<br /><br /> Verwenden Sie diese Einstellung oder RSWindowsNegotiate, wenn Sie die Kerberos-Authentifizierung in einem eingeschränkten Delegierungsauthentifizierungsschema verwenden.|N|  
|**RSWindowsBasic**|Der Server akzeptiert Standardanmeldeinformationen und gibt eine Herausforderung/Antwort aus, wenn eine Verbindung ohne Anmeldeinformationen hergestellt wird.<br /><br /> Die Standardauthentifizierung übergibt Anmeldeinformationen in den HTTP-Anforderungen in Klartext. Wenn Sie die Standardauthentifizierung verwenden, verwenden Sie SSL, um Netzwerkdatenverkehr zum Berichtsserver und vom Berichtsserver zu verschlüsseln. Syntax für eine Beispielkonfiguration zur Standardauthentifizierung in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]finden Sie unter [Authentifizierung mit dem Berichtsserver](../../reporting-services/security/authentication-with-the-report-server.md).|N|  
|**Custom**|Geben Sie diesen Wert an, wenn Sie auf dem Berichtsservercomputer eine benutzerdefinierte Sicherheitserweiterung bereitgestellt haben. Weitere Informationen finden Sie unter [Implementing a Security Extension](../../reporting-services/extensions/security-extension/implementing-a-security-extension.md).|N|  
|**LogonMethod**|Dieser Wert gibt den Anmeldetyp für **RSWindowsBasic**an. Wenn Sie **RSWindowsBasic**angeben, ist dieser Wert erforderlich. Gültige Werte sind 2 oder 3, wobei die einzelnen Werte für Folgendes stehen:<br /><br /> **2** = Netzwerkanmeldung für Server mit hoher Leistungsfähigkeit, um Nur-Text-Kennwörter zu authentifizieren<br /><br /> **3** = Klartextanmeldung, wobei die Anmeldeinformationen aus dem mit jeder HTTP-Anforderung gesendeten Authentifizierungspaket beibehalten werden. Dadurch kann der Server beim Herstellen von Verbindungen zu anderen Servern im Netzwerk die Identität des Benutzers annehmen.<br /><br /> <br /><br /> Hinweis: Die Werte 0 (für interaktive Anmeldung) und 1 (für Batchanmeldung) werden in [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]nicht unterstützt.|N|  
|**Realm**|Dieser Wert wird für **RSWindowsBasic**verwendet. Er gibt eine Ressourcenpartition mit Autorisierungs- und Authentifizierungsfunktionen an, mit der der Zugriff auf geschützte Ressourcen in Ihrem Unternehmen gesteuert wird.|N|  
|**DefaultDomain**|Dieser Wert wird für **RSWindowsBasic**verwendet. Er wird verwendet, um die Domäne zu ermitteln, die vom Server für die Benutzerauthentifizierung verwendet wird. Dieser Wert ist optional. Wenn Sie ihn weglassen, verwendet der Berichtsserver den Computernamen als Domäne. Wenn Sie den Berichtsserver auf einem Domänencontroller installiert haben, ist die verwendete Domäne die vom Computer gesteuerte.|N|  
|**RSWindowsExtendedProtectionLevel**|Der Standardwert lautet **off**. Weitere Informationen finden Sie unter [Extended Protection for Authentication with Reporting Services](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md).|N|  
|**RSWindowsExtendedProtectionScenario**|Der Standardwert lautet **Proxy**.|N|  
|**EnableAuthPersistence**|Bestimmt, ob die Authentifizierung für die Verbindung oder für jede Anforderung ausgeführt wird.<br /><br /> Gültige Werte sind **TRUE** (Standardwert) und **FALSE**. Ist der Wert auf **True**festgelegt, wird für nachfolgende Anforderungen von der gleichen Verbindung vom Identitätswechselkontext der ersten Anforderung ausgegangen.<br /><br /> Dieser Wert muss auf **FALSE** festgelegt werden, wenn Sie Proxyserversoftware (wie ISA Server) für den Zugriff auf den Berichtsserver verwenden. Bei Verwendung eines Proxyservers kann eine einzige Verbindung vom Proxyserver von mehreren Benutzern verwendet werden. Für dieses Szenario sollten Sie die Authentifizierungspersistenz deaktivieren, damit jede Benutzeranforderung separat authentifiziert werden kann. Wenn Sie **EnableAuthPersistence** nicht auf **False**festlegen, stellen alle Benutzer eine Verbindung unter Verwendung des Identitätswechselkontexts der ersten Anforderung her.|N,S|  
  
##  <a name="bkmk_service"></a> Service (Datei RSReportServer.config)  
 **Service** gibt die Anwendungseinstellungen an, die für den Dienst als Ganzes gelten.  
  
 Die letzte Spalte der folgenden Tabelle gibt an, ob die Einstellung für einen Berichtsserver im einheitlichen Modus (N) oder für einen Berichtsserver im SharePoint-Modus (S) oder für beide gilt.  
  
|Einstellung|Description|Mode|  
|-------------|-----------------|----------|  
|**IsSchedulingService**|Gibt an, ob der Berichtsserver einen Satz [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agentaufträge behält, der Zeitplänen und Abonnements entspricht, die von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Benutzern erstellt wurden. Gültige Werte sind **TRUE** (Standardwert) und **FALSE**.<br /><br /> Diese Einstellung ist betroffen, wenn Sie [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Funktionen mit dem Facet Oberflächenkonfiguration für Reporting Services der richtlinienbasierten Verwaltung aktivieren oder deaktivieren. Weitere Informationen finden Sie unter [Starten und Beenden des Berichtsserverdiensts](../../reporting-services/report-server/start-and-stop-the-report-server-service.md).|N,S|  
|**IsNotificationService**|Gibt an, ob der Berichtsserver Benachrichtigungen und Übermittlungen verarbeitet. Gültige Werte sind **TRUE** (Standardwert) und **FALSE**. Wenn der Wert **False**lautet, werden Abonnements nicht übermittelt.<br /><br /> Diese Einstellung ist betroffen, wenn Sie [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Funktionen mit dem Facet Oberflächenkonfiguration für Reporting Services der richtlinienbasierten Verwaltung aktivieren oder deaktivieren. Weitere Informationen finden Sie unter [Starten und Beenden des Berichtsserverdiensts](../../reporting-services/report-server/start-and-stop-the-report-server-service.md).|N,S|  
|**IsEventService**|Gibt an, ob der Dienst Ereignisse in der Ereigniswarteschlange verarbeitet. Gültige Werte sind **TRUE** (Standardwert) und **FALSE**. Wenn der Wert **False**lautet, führt der Berichtsserver keine Vorgänge für Zeitpläne oder Abonnements aus.<br /><br /> Diese Einstellung ist betroffen, wenn Sie [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Funktionen mit dem Facet Oberflächenkonfiguration für Reporting Services der richtlinienbasierten Verwaltung aktivieren oder deaktivieren. Weitere Informationen finden Sie unter [Starten und Beenden des Berichtsserverdiensts](../../reporting-services/report-server/start-and-stop-the-report-server-service.md).|N,S|  
|**IsAlertingService**|Der Standardwert ist **True**.|S|  
|**PollingInterval**|Gibt das Intervall in Sekunden an, in dem die Ereignistabelle durch den Berichtsserver abgerufen wird. Gültige Werte sind 0 bis zu einer maximalen ganzen Zahl. Der Standardwert ist 10.|N,S|  
|**WindowsServiceUseFileShareStorage**|Gibt an, ob zwischengespeicherte Berichte und temporäre Momentaufnahmen (die vom Berichtsserverdienst für die Dauer einer Benutzersitzung erstellt werden) im Dateisystem gespeichert werden. Gültige Werte sind **TRUE** und **FALSE** (Standardwert).|N,S|  
|**MemorySafetyMargin**|Gibt einen Prozentwert von **WorkingSetMaximum** an, der die Grenze zwischen mittlerer und geringer Arbeitsspeicherauslastung definiert. Der Standardwert ist 80. Weitere Informationen zu **WorkingSetMaximum** und zum Konfigurieren des verfügbaren Arbeitsspeichers finden Sie unter [Konfigurieren von verfügbarem Speicher für Berichtsserveranwendungen](../../reporting-services/report-server/configure-available-memory-for-report-server-applications.md).|N,S|  
|**MemoryThreshold**|Gibt einen Prozentwert von **WorkingSetMaximum** an, der die Grenze zwischen hoher und mittlerer Arbeitsspeicherauslastung definiert. Der Standardwert ist **90**. Dieser Wert sollte höher sein als der Wert für **MemorySafetyMargin**. Weitere Informationen finden Sie unter [Konfigurieren von verfügbarem Speicher für Berichtsserveranwendungen](../../reporting-services/report-server/configure-available-memory-for-report-server-applications.md).|N,S|  
|**RecycleTime**|Gibt die Wiederverwendungszeit für die Anwendungsdomäne in Minuten an. Gültige Werte sind 0 bis zu einer maximalen ganzen Zahl. Der Standardwert ist 720.|N,S|  
|**MaxAppDomainUnloadTime**|Gibt ein Intervall an, in dem ein Entladen der Anwendungsdomäne während eines Wiederverwendungsvorgangs zulässig ist. Wenn die Wiederverwendung nach diesem Zeitraum nicht abgeschlossen ist, wird die gesamte Verarbeitung in der Anwendungsdomäne abgebrochen. Weitere Informationen finden Sie unter [Application Domains for Report Server Applications](../../reporting-services/report-server/application-domains-for-report-server-applications.md).<br /><br /> Der Wert wird in Minuten angegeben. Gültige Werte sind 0 bis zu einer maximalen ganzen Zahl. Der Standardwert ist **30**.|N,S|  
|**MaxQueueThreads**|Gibt die Anzahl der Threads an, die vom Berichtsserver-Windows-Dienst zur parallelen Verarbeitung von Abonnements und Benachrichtigungen verwendet werden. Gültige Werte sind 0 bis zu einer maximalen ganzen Zahl. Der Standardwert ist 0. Wenn Sie 0 auswählen, bestimmt der Berichtsserver die maximale Anzahl der Threads. Wenn Sie eine ganze Zahl eingeben, legt der angegebene Wert den oberen Grenzwert für das gleichzeitige Erstellen von Threads fest. Weitere Informationen zur Speicherverwaltung des Berichtsserver-Windows-Diensts für ausgeführte Prozesse finden Sie unter [Konfigurieren von verfügbarem Speicher für Berichtsserveranwendungen](../../reporting-services/report-server/configure-available-memory-for-report-server-applications.md).|N,S|  
|**UrlRoot**|Dient den Berichtsserver-Übermittlungserweiterungen zur Erstellung von URLs, die von Berichten verwendet werden, die in E-Mail- und Dateifreigabeabonnements übermittelt werden. Der Wert muss eine gültige URL-Adresse zum Berichtsserver sein, über den auf den veröffentlichten Bericht zugegriffen werden kann. Wird vom Berichtsserver verwendet, um URLs für Offline- oder unbeaufsichtigten Zugriff zu generieren. Diese URLs werden in exportierten Berichten verwendet und dienen Übermittlungserweiterungen dazu, eine URL zu erstellen, die in Übermittlungsnachrichten wie beispielsweise Links in E-Mails eingefügt wird. Der Berichtsserver bestimmt URLs in Berichten auf Grundlage des folgenden Verhaltens:<br /><br /> Wenn **UrlRoot** leer ist (Standardwert) und URL-Reservierungen bestehen, ermittelt der Berichtsserver URLs automatisch in der gleichen Weise, in der URLs für die ListReportServerUrls-Methode generiert werden. Die erste von der ListReportServerUrls-Methode zurückgegebene URL wird verwendet. Oder wenn SecureConnectionLevel größer als 0 (null) ist, wird die erste SSL-URL verwendet.<br /><br /> Wenn **UrlRoot** auf einen bestimmten Wert festgelegt ist, wird der explizite Wert verwendet.<br /><br /> Wenn **UrlRoot** leer ist und keine URL-Reservierungen konfiguriert wurden, sind die URLs in gerenderten Berichten und in E-Mail-Links falsch.|N,S|  
|**UnattendedExecutionAccount**|Gibt einen Benutzernamen, ein Kennwort und eine Domäne an, mit denen der Berichtsserver einen Bericht ausführt. Diese Werte sind verschlüsselt. Sie können mithilfe des [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationstools oder des Hilfsprogramms **rsconfig** festgelegt werden. Weitere Informationen finden Sie unter [Konfigurieren des Kontos für die unbeaufsichtigte Ausführung (SSRS-Konfigurations-Manager)](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).<br /><br /> Legen Sie für den SharePoint-Modus das Ausführungskonto für eine [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendung mithilfe der SharePoint-Zentraladministration fest. Weitere Informationen finden Sie unter [Verwalten einer Reporting Services-SharePoint-Dienstanwendung](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md).|N|  
|**PolicyLevel**|Gibt die Sicherheitsrichtlinien-Konfigurationsdatei an. Der gültige Wert ist Rssrvrpolicy.config. Weitere Informationen finden Sie unter [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md).|N,S|  
|**IsWebServiceEnabled**|Gibt an, ob der Berichtsserver-Webdienst auf SOAP- und URL-Zugriffsanforderungen antwortet. Dieser Wert wird festgelegt, wenn Sie den Dienst mit dem Facet Oberflächen-Konfigurationstool für Reporting Services der richtlinienbasierten Verwaltung aktivieren oder deaktivieren.|N,S|  
|**IsReportManagerEnabled**|Diese Einstellung wurde ab dem Kumulativen Update 2 von SQL Server 2016 Reporting Services als veraltet gekennzeichnet. Das Webportal bleibt weiterhin aktiviert.|N|  
|**FileShareStorageLocation**|Gibt einen einzelnen Ordner im Dateisystem für das Speichern temporärer Momentaufnahmen an. Die Angabe des Ordnerpfads als UNC-Pfad wird nicht empfohlen, ist aber möglich. Der Standardwert ist leer.<br /><br /> `<FileShareStorageLocation>`<br /><br /> `<Path>`<br /><br /> `</Path>`<br /><br /> `</FileShareStorageLocation>`|N,S|  
|**IsRdceEnabled**|Gibt an, ob die Erweiterung zur Anpassung von Berichtsdefinitionen (Report Definition Customization Extension, RDCE) aktiviert ist. Gültige Werte sind **True** und **False**.|N,S|  
  
##  <a name="bkmk_UI"></a> UI (Datei RSReportServer.config)  
 **UI** gibt Konfigurationseinstellungen an, die für die Webportal-Anwendung gelten.  
  
 Die letzte Spalte der folgenden Tabelle gibt an, ob die Einstellung für einen Berichtsserver im einheitlichen Modus (N) oder für einen Berichtsserver im SharePoint-Modus (S) oder für beide gilt.  
  
|Einstellung|Description|Mode|  
|-------------|-----------------|----------|  
|**ReportServerUrl**|Gibt die URL des Berichtsservers an, zu der das Webportal eine Verbindung herstellt. Ändern Sie diesen Wert nur, wenn Sie das Webportal konfigurieren, um eine Verbindung zu einem Berichtsserver in einer anderen Instanz oder auf einem Remotecomputer herzustellen.|N,S|  
|**ReportBuilderTrustLevel**|Ändern Sie diesen Wert nicht; er ist nicht konfigurierbar. In [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] und neueren Versionen wird der Berichts-Generator nur in **FullTrust**ausgeführt. Weitere Informationen finden Sie unter [Konfigurieren des Berichts-Generator-Zugriffs](../../reporting-services/report-server/configure-report-builder-access.md) . Weitere Informationen zum Beenden der Modus mit teilweiser Vertrauenswürdigkeit finden Sie unter [Nicht mehr unterstützte Funktionen in SQL Server Reporting Services in SQL Server 2016](../../reporting-services/discontinued-functionality-to-sql-server-reporting-services-in-sql-server.md).|N,S|  
|**PageCountMode**|Im Webportal wird durch diese Einstellung festgelegt, ob der Berichtsserver einen Seitenzahlwert berechnet, bevor der Bericht gerendert wird oder während der Anzeige des Berichts. Gültige Werte sind **Schätzung** (Standardwert) und **Tatsächlich**. Verwenden Sie **Estimate** , um den Seitenzahlwert während der Anzeige des Berichts zu berechnen. Anfangs wird die Seitenzahl auf 2 festgelegt (für die aktuelle Seite plus eine zusätzliche Seite) und jeweils erhöht, wenn der Benutzer durch den Bericht blättert. Verwenden Sie **Actual** , wenn die Seitenzahl vor der Anzeige des Berichts berechnet werden soll. **Actual** wird zu Zwecken der Abwärtskompatibilität bereitgestellt. Wenn Sie **PageCountMode** auf **Actual**festlegen, muss der gesamte Bericht verarbeitet werden, damit eine gültige Seitenzahl berechnet werden kann. Dadurch erhöht sich die Wartezeit, bis der Bericht geöffnet wird.|N,S|  
  
##  <a name="bkmk_extensions"></a> Erweiterungen (Datei "RSReportServer.config") für den einheitlichen Modus  
 Der Bereich **Erweiterungen** wird in der Datei rsreportserver.config nur für Berichtsserver im einheitlichen Modus angezeigt. Erweiterungsinformationen für SharePoint-Modusberichtsserver werden in der SharePoint-Konfigurationsdatenbank gespeichert und werden pro [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendung konfiguriert.  
  
 **Erweiterungen** gibt Konfigurationseinstellungen für die folgenden erweiterbaren Module einer [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Installation an:  
  
-   Übermittlungserweiterungen  
  
-   DeliveryUI-Erweiterungen  
  
-   Renderingerweiterungen  
  
-   Datenverarbeitungserweiterungen  
  
-   Semantikabfrageerweiterungen (nur intern)  
  
-   Modellgenerierungserweiterungen (nur intern)  
  
-   Sicherheitserweiterungen  
  
-   Authentifizierungserweiterungen  
  
-   Ereignisverarbeitungserweiterungen (nur intern)  
  
-   Anpassungserweiterungen für Berichtsdefinitionen  
  
 Einige dieser Erweiterungen sind nur zur internen Verwendung durch den Berichtsserver vorgesehen. Die Konfigurationseinstellungen für die nur zur internen Verwendung vorgesehenen Erweiterungen werden nicht dokumentiert. In den folgenden Abschnitten werden die Konfigurationseinstellungen für die Standarderweiterungen beschrieben. Wenn Sie einen Berichtsserver mit benutzerdefinierten Erweiterungen verwenden, enthalten Ihre Konfigurationsdateien unter Umständen Einstellungen, die hier nicht beschrieben sind. In diesem Abschnitt werden die Erweiterungen in der Reihenfolge aufgeführt, in der sie in der Konfigurationsdatei enthalten sind. Einstellungen, die für mehrere Instanzen der gleichen Erweiterung mehrmals auftreten, werden nur einmal beschrieben.  
  
###  <a name="bkmk_extensionsgeneral"></a> Allgemeine Konfiguration der Übermittlungserweiterung(en)  
 Gibt standardmäßige (und möglicherweise benutzerdefinierte) Übermittlungserweiterungen an, die zur Übermittlung von Berichten mithilfe von Abonnements verwendet werden. Die Datei "RSReportServer.config" enthält Anwendungseinstellungen für vier Übermittlungserweiterungen:  
  
1.  Berichtsserver-E-Mail  
  
2.  Dateifreigabeübermittlung.  
  
3.  Berichtsserverdokumentbibliothek, die für einen Berichtsserver verwendet wird, der im integrierten SharePoint-Modus ausgeführt wird.  
  
4.  NULL-Übermittlungsanbieter zum Vorladen des Berichtscaches.  
  
 Weitere Informationen zu Übermittlungserweiterungen finden Sie unter [Abonnements und Übermittlung (Reporting Services)](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md).  
  
 Alle Übermittlungserweiterungen weisen die Einstellungen **Extension Name**, **MaxRetries**, **SecondsBeforeRetry**und **Configuration**auf. Diese gemeinsamen Einstellungen werden zuerst dokumentiert. Die Beschreibungen der erweiterungsspezifischen Einstellungen folgen in einer zweiten Tabelle.  
  
|Einstellung|Description|  
|-------------|-----------------|  
|**Extension Name**|Gibt einen Anzeigenamen und eine Assembly der Übermittlungserweiterung an. Ändern Sie diesen Wert nicht.|  
|**MaxRetries**|Gibt an, wie oft ein Berichtsserver eine Übermittlung erneut versucht, wenn der erste Versuch fehlschlägt. Der Standardwert ist 3.|  
|**SecondsBeforeRetry**|Gibt den Zeitraum zwischen den einzelnen Wiederholungsversuchen in Sekunden an. Der Standardwert ist 900.|  
|**Configuration**|Enthält die Konfigurationseinstellungen, die für jede Übermittlungserweiterung spezifisch sind.|  
  
####  <a name="bkmk_fileshare_extension"></a> Konfigurationseinstellungen für die Dateifreigabe-Übermittlungerweiterung  
 Bei der Dateifreigabeübermittlung wird ein Bericht gesendet, der im Anwendungsdateiformat in einen freigegebenen Ordner im Netzwerk exportiert wurde. Weitere Informationen finden Sie unter [File Share Delivery in Reporting Services](../../reporting-services/subscriptions/file-share-delivery-in-reporting-services.md).  
  
|Einstellung|Description|  
|-------------|-----------------|  
|**ExcludedRenderFormats**, **RenderingExtension**|Diese Einstellungen werden verwendet, um Exportformate auszuschließen, die nicht in der Dateifreigabeübermittlung verwendet werden können. Diese Formate werden in der Regel zur interaktiven Berichterstellung, Vorschau oder zum Vorladen des Berichtscaches verwendet. Sie erzeugen keine Anwendungsdateien, die ganz einfach in einer Desktopanwendung angezeigt werden können.<br /><br /> HTMLOWC<br /><br /> RGDI<br /><br /> NULL|  
  
####  <a name="bkmk_email_extension"></a> Konfigurationseinstellungen für Berichtsserver-E-Mail-Erweiterung  
 Berichtsserver-E-Mail verwendet ein SMTP-Netzwerkgerät, um Berichte an E-Mail-Adressen zu senden. Diese Übermittlungserweiterung muss konfiguriert werden, bevor sie verwendet werden kann. Weitere Informationen finden Sie unter [Konfigurieren eines Berichtsservers für die E-Mail-Übermittlung (SSRS-Konfigurations-Manager)](http://msdn.microsoft.com/en-us/b838f970-d11a-4239-b164-8d11f4581d83) und [E-Mail-Übermittlung in Reporting Services](../../reporting-services/subscriptions/e-mail-delivery-in-reporting-services.md).  
  
|Einstellung|Description|  
|-------------|-----------------|  
|**SMTPServer**|Gibt einen Zeichenfolgenwert für die Adresse eines SMTP-Remoteservers oder einer Weiterleitung an. Dieser Wert ist für SMTP-Remotedienste erforderlich. Dabei kann es sich um eine IP-Adresse, den UNC-Namen eines Computers im Intranet Ihres Unternehmens oder um einen vollqualifizierten Domänennamen handeln.|  
|**SMTPServerPort**|Gibt eine ganze Zahl für den Port an, den der SMTP-Dienst zum Senden ausgehender E-Mails verwendet. Der Port 25 wird normalerweise zum Senden von E-Mail verwendet.|  
|**SMTPAccountName**|Enthält einen Zeichenfolgenwert, der einen [!INCLUDE[msCoName](../../includes/msconame-md.md)] Outlook Express-Kontonamen zuweist. Sie können diesen Wert festlegen, wenn Ihr SMTP-Server dafür konfiguriert ist; andernfalls lassen Sie dieses Feld leer. Verwenden Sie **From** , um ein E-Mail-Konto zum Senden von Berichten anzugeben.|  
|**SMTPConnectionTimeout**|Gibt eine ganze Zahl an, die angibt, wie viele Sekunden auf eine gültige Socketverbindung mit dem SMTP-Dienst gewartet wird, bevor der Vorgang wegen eines Timeouts abgebrochen wird. Der Standardwert ist 30 Sekunden. Dieser Wert wird jedoch ignoriert, wenn **SendUsing** auf 2 festgelegt ist.|  
|**SMTPServerPickupDirectory**|Gibt ein Zeichenfolgenwert für das Abholverzeichnis des lokalen SMTP-Diensts an. Bei diesem Wert muss es sich um einen vollqualifizierten lokalen Ordnerpfad (z. B. D:\rs-emails) handeln.|  
|**SMTPUseSSL**|Gibt einen booleschen Wert an, der für die Verwendung von Secure Sockets Layer (SSL) beim Senden einer SMTP-Nachricht im Netzwerk festgelegt werden kann. Der Standardwert ist 0 (oder False). Diese Einstellung kann verwendet werden, wenn das **SendUsing** -Element auf 2 festgelegt ist.|  
|**SendUsing**|Gibt die Methode zum Senden von Nachrichten an. Gültige Werte sind:<br /><br /> 1 = Sendet eine Nachricht mithilfe des Abholverzeichnisses des lokalen SMTP-Diensts.<br /><br /> 2 = Sendet die Nachricht mithilfe des Netzwerk-SMTP-Diensts.|  
|**SMTPAuthenticate**|Gibt eine ganze Zahl für die Authentifizierungsmethode an, die beim Senden von Nachrichten an einen SMTP-Dienst über eine TCP/IP-Verbindung verwendet werden soll. Gültige Werte sind:<br /><br /> 0 = Keine Authentifizierung.<br /><br /> 1 = (Nicht unterstützt).<br /><br /> 2 = NTLM-Authentifizierung (NT-LanMan). Zum Herstellen einer Verbindung zum Netzwerk-SMTP-Dienst wird der Sicherheitskontext des Berichtsserver-Windows-Diensts verwendet.|  
|**From**|Gibt eine E-Mail-Adresse an, mit der Berichte im Format *abc@host.xyz*. Die Adresse wird in der Zeile **Von** einer ausgehenden E-Mail-Nachricht angezeigt. Dieser Wert ist erforderlich, wenn Sie einen SMTP-Remoteserver verwenden. Es sollte ein gültiges E-Mail-Konto mit der Berechtigung zum Senden von E-Mail sein.|  
|**EmbeddedRenderFormats, RenderingExtension**|Gibt das Renderingformat zum Einschließen eines Berichts in den Textkörper einer E-Mail-Nachricht an. Bilder im Bericht werden anschließend in den Bericht eingebettet. Gültige Werte sind MHTML und HTML4.0.|  
|**PrivilegedUserRenderFormats**|Gibt die Renderingformate an, die ein Benutzer für ein Berichtsabonnement auswählen kann, wenn das Abonnieren über den Task "Alle Abonnements verwalten" aktiviert ist. Wenn dieser Wert nicht festgelegt wird, stehen alle nicht ausdrücklich ausgeschlossenen Renderingformate zur Verfügung.|  
|**ExcludedRenderFormats, RenderingExtension**|Schließt ausdrücklich Formate aus, die nicht für eine bestimmte Übermittlungserweiterung geeignet sind. Es können nicht mehrere Instanzen derselben Renderingerweiterung ausgeschlossen werden. Durch das Ausschließen mehrerer Instanzen wird ein Fehler ausgelöst, wenn der Berichtsserver die Konfigurationsdatei liest. Standardmäßig werden die folgenden Erweiterungen für die E-Mail-Übermittlung ausgeschlossen:<br /><br /> HTMLOWC<br /><br /> NULL<br /><br /> RGDI|  
|**SendEmailToUserAlias**|Dieser Wert wird zusammen mit **DefaultHostName**verwendet.<br /><br /> Wenn **SendEmailToUserAlias** auf **True**festgelegt ist, werden Benutzer, die einzelne Abonnements definieren, automatisch als Empfänger des Berichts angegeben. Das Feld **An** ist ausgeblendet. Ist dieser Wert auf **False**festgelegt, ist das Feld **An** sichtbar. Legen Sie für diesen Wert **True** fest, wenn Sie die volle Kontrolle über die Berichtsverteilung wünschen. Folgende Werte sind gültig:<br /><br /> **TRUE**= Die E-Mail-Adresse des Benutzers, der das Abonnement erstellt, wird verwendet. Dies ist der Standardwert.<br /><br /> **FALSE**= Eine beliebige E-Mail-Adresse kann angegeben werden.|  
|**DefaultHostName**|Dieser Wert wird zusammen mit **SendEmailToUserAlias**verwendet.<br /><br /> Gibt einen Zeichenfolgenwert für den Hostnamen an, der an den Benutzeralias angefügt werden soll, wenn **SendEmailToUserAlias** auf true festgelegt ist. Bei diesem Wert kann es sich um einen DNS-Namen (Domain Name System) oder eine IP-Adresse handeln.|  
|**PermittedHosts**|Beschränkt die Berichtsverteilung, indem explizit die Hosts angegeben werden, die die E-Mail-Übermittlung empfangen können. Bei **PermittedHosts**wird jeder Host als **HostName** -Element angegeben. Der Wert ist eine IP-Adresse oder ein DNS-Name.<br /><br /> Nur E-Mail-Konten, die für den Host definiert sind, sind gültige Empfänger. Wenn Sie **DefaultHostName**angegeben haben, müssen Sie sicherstellen, dass dieser Host als **HostName** -Element von **PermittedHosts**angegeben wurde. Bei diesem Wert muss es sich um mindestens einen DNS-Namen oder eine IP-Adressen handeln. Standardmäßig ist dieser Wert nicht festgelegt. Wenn dieser Wert nicht festgelegt ist, gibt es keine Einschränkungen, wer per E-Mail gesendete Berichte empfangen kann.|  
  
####  <a name="bkmk_documentlibrary_extension"></a> Konfiguration der Erweiterung für die Berichtsserver-SharePoint-Dokumentbibliothek  
 Die Berichtsserver-Dokumentbibliothek sendet einen Bericht, der in ein Anwendungsdateiformat exportiert wurde, in eine Dokumentbibliothek. Diese Übermittlungserweiterung kann nur von einem Berichtsserver verwendet werden, der für die Ausführung im integrierten SharePoint-Modus konfiguriert wurde. Weitere Informationen finden Sie unter [SharePoint Library Delivery in Reporting Services](../../reporting-services/subscriptions/sharepoint-library-delivery-in-reporting-services.md).  
  
|Einstellung|Description|  
|-------------|-----------------|  
|**ExcludedRenderFormats, RenderingExtension**|Diese Einstellungen werden verwendet, um Exportformate auszuschließen, die nicht mit der Dokumentbibliothek verwendet werden können. HTMLOWC, RGDI und NULL-Übermittlungserweiterungen werden ausgeschlossen. Diese Formate werden in der Regel zur interaktiven Berichterstellung, Vorschau oder zum Vorladen des Berichtscaches verwendet. Sie erzeugen keine Anwendungsdateien, die ganz einfach in einer Desktopanwendung angezeigt werden können.|  
  
####  <a name="bkmk_null_extension"></a> Konfiguration der Erweiterung der NULL-Übermittlung  
 Der NULL-Übermittlungsanbieter wird zum Vorladen des Caches mit vorgenerierten Berichten für einzelne Benutzer verwendet. Es sind keine Konfigurationseinstellungen für diese Übermittlungserweiterung vorhanden. Weitere Informationen finden Sie unter [Zwischenspeichern von Berichten &#40;SSRS&#41;](../../reporting-services/report-server/caching-reports-ssrs.md)bestand darin die einzige Möglichkeit, den Cache vorab zu laden.  
  
###  <a name="bkmk_ui"></a> Allgemeine Konfiguration der Erweiterung(en) für die Übermittlungsbenutzeroberfläche  
 Gibt Übermittlungserweiterungen mit einer Benutzeroberflächenkomponente an, die in den Abonnementdefinitionsseiten für die Definition einzelner Abonnements im Webportal angezeigt wird. Wenn Sie eine benutzerdefinierte Übermittlungserweiterung erstellen und bereitstellen, die benutzerdefinierte Optionen aufweist, und Sie das Webportal verwenden möchten, müssen Sie die Übermittlungserweiterung in diesem Abschnitt registrieren. Standardmäßig sind Konfigurationseinstellungen für Berichtsserver-E-Mail und Berichtsserver-Dateifreigabe vorhanden. Übermittlungserweiterungen, die nur in datengesteuerten Abonnements oder in SharePoint-Anwendungsseiten verwendet werden, weisen keine Einstellungen in diesem Abschnitt auf.  
  
|Einstellung|Description|  
|-------------|-----------------|  
|**DefaultDeliveryExtension**|Diese Einstellung legt fest, welche Übermittlungserweiterung als erster Übermittlungstyp in der Liste auf der Abonnementdefinitionsseite angezeigt wird. Nur eine Übermittlungserweiterung kann diese Einstellung enthalten. Gültige Werte sind **True** oder **False**. Wenn dieser Wert auf **True**festgelegt ist, ist die betreffende Erweiterung die Standardauswahl.|  
|**Configuration**|Konfigurationsoptionen für eine Übermittlungserweiterung. Für jede Übermittlungserweiterung kann ein Standardrenderingformat festgelegt werden. Gültige Werte sind die Renderingerweiterungsnamen, die im Renderingabschnitt der Konfigurationsdatei rsreportserver.config vermerkt sind.|  
|**DefaultRenderingExtension**|Gibt an, ob eine Übermittlungserweiterung der Standardwert ist. Berichtsserver-E-Mail ist die Standardübermittlungserweiterung. Gültige Werte sind **True** oder **False**. Enthalten mehrere Erweiterungen den Wert **True**, gilt die erste Erweiterung als Standarderweiterung.|  
  
###  <a name="bkmk_rendering"></a> Allgemeine Konfiguration der Renderingerweiterungen  
 Gibt standardmäßige (und möglicherweise benutzerdefinierte) Renderingerweiterungen für die Berichtspräsentation an.  
  
 Ändern Sie diesen Abschnitt nur, wenn Sie eine benutzerdefinierte Renderingerweiterung bereitstellen. Weitere Informationen finden Sie unter [Implementing a Rendering Extension](../../reporting-services/extensions/rendering-extension/implementing-a-rendering-extension.md).  
  
 Standardrenderingerweiterungen schließen Folgendes ein:  
  
-   XML  
  
-   NULL  
  
-   CSV  
  
-   PDF  
  
-   RGDI  
  
-   HTML4.0  
  
-   MHTML  
  
-   EXCEL  
  
-   RPL  
  
-   IMAGE  
  
 Ab der [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] -Version besitzen die Render MHTML und HTML 4.0 standardmäßig die folgenden Geräteinformationseinstellungen, um das Verhalten der Größenanpassung von Datenvisualisierungen zu steuern.  
  
```  
<DeviceInfo><DataVisualizationFitSizing>Approximate</DataVisualizationFitSizing></DeviceInfo>  
```  
  
 Weitere Informationen über DeviceInfo-Einstellungen finden Sie unten:  
  
-   [Geräteinformationseinstellungen für MHTML](../../reporting-services/mhtml-device-information-settings.md)  
  
-   [HTML-Geräteinformationseinstellungen](../../reporting-services/html-device-information-settings.md)  
  
-   [Geräteinformationseinstellungen für Renderingerweiterungen &#40;Reporting Services&#41;](../../reporting-services/device-information-settings-for-rendering-extensions-reporting-services.md)  
  
 Weitere Informationen zu den Attributen für das untergeordnete **<Erweiterung\<**-Element unter **\<Render>** finden Sie unter:  
  
-   [Anpassen der Parameter für Renderingerweiterungen in der Datei RSReportServer.config](../../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)  
  
-   [Bereitstellen von Renderingerweiterungen](../../reporting-services/extensions/rendering-extension/deploying-a-rendering-extension.md)  
  
 Ändern Sie diesen Abschnitt nur, wenn Sie eine benutzerdefinierte Renderingerweiterung bereitstellen. Weitere Informationen finden Sie unter [Implementing a Rendering Extension](../../reporting-services/extensions/rendering-extension/implementing-a-rendering-extension.md).  
  
###  <a name="bkmk_data"></a> Allgemeine Konfiguration der Datenerweiterung(en)  
 Gibt standardmäßige (und möglicherweise benutzerdefinierte) Datenverarbeitungserweiterungen zum Verarbeiten von Abfragen an. Standardmäßige Datenverarbeitungserweiterungen schließen Folgendes ein:  
  
-   SQL  
  
-   SQLAZURE  
  
-   SQLPDW  
  
-   OLEDB  
  
-   OLEDB-MD  
  
-   ORACLE  
  
-   ODBC  
  
-   XML  
  
-   SHAREPOINTLIST  
  
-   SAPBW  
  
-   ESSBASE  
  
-   TERADATA  
  
 Ändern Sie diesen Abschnitt nur, wenn Sie benutzerdefinierte Datenverarbeitungserweiterungen hinzufügen. Weitere Informationen finden Sie unter [Implementing a Data Processing Extension](../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md).  
  
###  <a name="bkmk_semantic"></a> Allgemeine Konfiguration der Erweiterungen für semantische Abfragen  
 Gibt die Semantikabfrage-Verarbeitungserweiterung zum Verarbeiten von Berichtsmodellen an. Die Semantikabfrage-Verarbeitungserweiterungen von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] bieten Unterstützung für relationale [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Daten und mehrdimensionale [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Daten. Ändern Sie diesen Abschnitt nicht. Die Abfrageverarbeitung ist nicht erweiterbar.  
  
###  <a name="bkmk_model"></a> Modellgenerierungskonfiguration  
 Gibt eine Modellgenerierungserweiterung an, mit der Modelle aus einer gemeinsam genutzten Datenquelle erstellt werden können, die bereits auf einem Berichtsserver veröffentlicht wurde. Sie können Modelle für relationale [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Daten, Oracle und mehrdimensionale [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenquellen generieren. Ändern Sie diesen Abschnitt nicht. Die Modellgenerierung ist nicht erweiterbar.  
  
###  <a name="bkmk_security"></a> Konfiguration der Sicherheitserweiterung  
 Gibt die von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]verwendete Autorisierungskomponente an. Diese Komponente wird von der Authentifizierungserweiterung, die im **Authentication** -Element der Datei RSReportServer.config registriert ist, verwendet. Ändern Sie diesen Abschnitt nur, wenn Sie eine benutzerdefinierte Authentifizierungserweiterung implementieren. Weitere Informationen zum Hinzufügen von benutzerdefinierten Sicherheitsfunktionen finden Sie unter [Implementing a Security Extension](../../reporting-services/extensions/security-extension/implementing-a-security-extension.md). Weitere Informationen zur Autorisierung finden Sie unter [Authorization in Reporting Services](../../reporting-services/extensions/security-extension/authorization-in-reporting-services.md).  
  
###  <a name="bkmk_authentication"></a> Konfigurieren der Authentifizierungseinstellung  
 Gibt standardmäßige und benutzerdefinierte Authentifizierungserweiterungen an, die vom Berichtsserver verwendet werden. Die Standarderweiterung basiert auf der Windows-Authentifizierung. Ändern Sie diesen Abschnitt nur, wenn Sie eine benutzerdefinierte Authentifizierungserweiterung implementieren. Weitere Informationen zur Authentifizierung in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]finden Sie unter [Authentifizierung in Reporting Services](../../reporting-services/extensions/security-extension/authentication-in-reporting-services.md) und [Authentifizierung mit dem Berichtsserver](../../reporting-services/security/authentication-with-the-report-server.md). Weitere Informationen zum Hinzufügen von benutzerdefinierten Sicherheitsfunktionen finden Sie unter [Implementing a Security Extension](../../reporting-services/extensions/security-extension/implementing-a-security-extension.md).  
  
###  <a name="bkmk_eventprocessing"></a> Ereignisverarbeitung  
 Gibt die Standardereignishandler an. Ändern Sie diesen Abschnitt nicht. Dieser Abschnitt ist nicht erweiterbar.  
  
###  <a name="bkmk_reportdefinition"></a> Berichtsdefinitionenanpassung  
 Gibt den Namen und den Typ einer benutzerdefinierten Erweiterung an, die eine Berichtsdefinition ändert.  
  
###  <a name="bkmk_rdlsandboxing"></a> RDLSandboxing  
 Gibt einen RDL-Modus (Report Definition Language, Berichtsdefinitionssprache) an, in dem die Verwendung bestimmter Berichtsressourcentypen durch einzelne Mandanten in einem Szenario erkannt und eingeschränkt werden kann, in dem mehrere Mandanten eine einzelne Webfarm von Berichtsservern gemeinsam nutzen. Weitere Informationen finden Sie unter [Enable and Disable RDL Sandboxing](../../reporting-services/report-server-sharepoint/enable-and-disable-rdl-sandboxing.md).  
  
##  <a name="bkmk_MapTileServer"></a> MapTileServerConfiguration (Datei 'RSReportServer.config')  
 **MapTileServerConfiguration** definiert Konfigurationseinstellungen für [!INCLUDE[msCoName](../../includes/msconame-md.md)] Bing Maps Web Services, die einen Kachelhintergrund für ein Kartenberichtselement in einem Bericht bereitstellen, der auf einem Berichtsserver veröffentlicht wird. Alle untergeordneten Elemente sind erforderlich.  
  
|Einstellung|Description|  
|-------------|-----------------|  
|**MaxConnections**|Gibt die maximale Anzahl von Verbindungen mit Bing Maps Web Services an.|  
|**Timeout**|Gibt das Timeout in Sekunden an, bis zu dem auf eine Antwort von Bing Maps Web Services gewartet wird.|  
|**AppID**|Gibt den für Bing Maps Web Services zu verwendenden Anwendungsbezeichner (AppID) an. **(Standard)** gibt die standardmäßige [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -AppID an.<br /><br /> Weitere Informationen zur Verwendung von Bing-Kartenkacheln im Bericht finden Sie in den [zusätzlichen Nutzungsbedingungen](http://go.microsoft.com/fwlink/?LinkId=151371).<br /><br /> Sie sollten diesen Wert nur ändern, wenn Sie eine benutzerdefinierten AppID für einen eigenen Bing Maps-Lizenzvertrag angeben müssen. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] muss nach dem Ändern der AppID nicht neu gestartet werden, damit die Änderung wirksam wird.|  
|**CacheLevel**|Gibt einen Wert aus der HttpRequestCacheLevel-Enumeration von System.Net.Cache an. Der Standardwert lautet **Default**. Weitere Informationen finden Sie unter [HttpRequestCacheLevel-Enumeration](http://go.microsoft.com/fwlink/?LinkId=153353).|  
  
##  <a name="bkmk_nativedefaultfile"></a> Standardkonfigurationsdatei für einen Berichtsserver im einheitlichen Modus  
 Die Datei "rsreportserver.config" wird standardmäßig am folgenden Speicherort installiert:  
  
 **C:\Programme\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\ReportServer**  
  
```  
<Configuration>
    <Dsn>AQAAANCMnd8BFdERjHoAwE/Cl+sBAAAAR58DMGebHUeMvyR6HR04kQQAAAAiAAAAUgBlAHAAbwBy
AHQAaQBuAGcAIABTAGUAcgB2AGUAcgAAAANmAADAAAAAEAAAADczfLRgZ4GF44iBHkLrKY4AAAAA
BIAAAKAAAAAQAAAAJ9wQOmDNauH+LS30rboJ2OAAAAAp0kiFFBrc3r3ypKaldZJtjCORX9LTZRzt
0/JCSVIZc4GXx0peGKqd+f85UyrY/KOyUSHogOC/XoBp9Ppxv6ITbdunsS/LXEcMUBVqEdQD4ylh
x6K1NTC/u8hl9v0MgK+xMQKaiV7BuNYbgGgkaViABcNH0xVzcc5rMTHUkrABbGDFGKyAFniGQ1qu
/rqHibNNyvYbP/2uiqvgC0tQl6u8VkVbXpWrkvO+bFCqxlaJlCoDc2f3rIO321SZEvoFbsYNgPLd
+mIAkSCnH3Z3gm/bI8bqVkFaHblKyQuSfFsi6RQAAACb87b26dV0GjHmMJnE0Tk8CzNmhg==</Dsn>
    <ConnectionType>Default</ConnectionType>
    <LogonUser></LogonUser>
    <LogonDomain></LogonDomain>
    <LogonCred></LogonCred>
    <InstanceId>MSRS13.MSSQLSERVER</InstanceId>
    <InstallationID>{cd920604-a5c7-4554-b2a0-aadc04312fe5}</InstallationID>
    <Add Key="SecureConnectionLevel" Value="0"/>
    <Add Key="DisableSecureFormsAuthenticationCookie" Value="false"/>
    <Add Key="CleanupCycleMinutes" Value="10"/>
    <Add Key="MaxActiveReqForOneUser" Value="20"/>
    <Add Key="DatabaseQueryTimeout" Value="120"/>
    <Add Key="RunningRequestsScavengerCycle" Value="60"/>
    <Add Key="RunningRequestsDbCycle" Value="60"/>
    <Add Key="RunningRequestsAge" Value="30"/>
    <Add Key="MaxScheduleWait" Value="5"/>
    <Add Key="DisplayErrorLink" Value="true"/>
    <Add Key="WebServiceUseFileShareStorage" Value="false"/>
    <!--  <Add Key="ProcessTimeout" Value="150" /> -->
    <!--  <Add Key="ProcessTimeoutGcExtension" Value="30" /> -->
    <!--  <Add Key="WatsonFlags" Value="0x0430" /> full dump-->
    <!--  <Add Key="WatsonFlags" Value="0x0428" /> minidump -->
    <!--  <Add Key="WatsonFlags" Value="0x0002" /> no dump-->
    <Add Key="WatsonFlags" Value="0x0428"/>
    <Add Key="WatsonDumpOnExceptions" Value="Microsoft.ReportingServices.Diagnostics.Utilities.InternalCatalogException,Microsoft.ReportingServices.Modeling.InternalModelingException,Microsoft.ReportingServices.ReportProcessing.UnhandledReportRenderingException"/>
    <Add Key="WatsonDumpExcludeIfContainsExceptions" Value="System.Threading.ThreadAbortException,System.Web.UI.ViewStateException,System.OutOfMemoryException,System.Web.HttpException,System.IO.IOException,System.IO.FileLoadException,Microsoft.SharePoint.SPException,Microsoft.ReportingServices.WmiProvider.WMIProviderException,System.AppDomainUnloadedException"/>
    <URLReservations>
        <Application>
            <Name>ReportServerWebService</Name>
            <VirtualDirectory>ReportServer</VirtualDirectory>
            <URLs>
                <URL>
                    <UrlString>http://+:80</UrlString>
                    <AccountSid>S-1-5-80-2885764129-887777008-271615777-1616004480-2722851051</AccountSid>
                    <AccountName>NT SERVICE\ReportServer</AccountName>
                </URL>
            </URLs>
        </Application>
        <Application>
            <Name>ReportServerWebApp</Name>
            <VirtualDirectory>Reports</VirtualDirectory>
            <URLs>
                <URL>
                    <UrlString>http://+:80</UrlString>
                    <AccountSid>S-1-5-80-2885764129-887777008-271615777-1616004480-2722851051</AccountSid>
                    <AccountName>NT SERVICE\ReportServer</AccountName>
                </URL>
            </URLs>
        </Application>
    </URLReservations>
    <Authentication>
        <AuthenticationTypes>
            <RSWindowsNTLM/>
        </AuthenticationTypes>
        <RSWindowsExtendedProtectionLevel>Off</RSWindowsExtendedProtectionLevel>
        <RSWindowsExtendedProtectionScenario>Proxy</RSWindowsExtendedProtectionScenario>
        <EnableAuthPersistence>true</EnableAuthPersistence>
    </Authentication>
    <Service>
        <IsSchedulingService>True</IsSchedulingService>
        <IsNotificationService>True</IsNotificationService>
        <IsEventService>True</IsEventService>
        <PollingInterval>10</PollingInterval>
        <WindowsServiceUseFileShareStorage>False</WindowsServiceUseFileShareStorage>
        <MemorySafetyMargin>80</MemorySafetyMargin>
        <MemoryThreshold>90</MemoryThreshold>
        <RecycleTime>720</RecycleTime>
        <MaxAppDomainUnloadTime>30</MaxAppDomainUnloadTime>
        <MaxQueueThreads>0</MaxQueueThreads>
        <UrlRoot>
        </UrlRoot>
        <UnattendedExecutionAccount>
            <UserName></UserName>
            <Password></Password>
            <Domain></Domain>
        </UnattendedExecutionAccount>
        <PolicyLevel>rssrvpolicy.config</PolicyLevel>
        <IsWebServiceEnabled>True</IsWebServiceEnabled>
        <IsReportManagerEnabled>True</IsReportManagerEnabled>
        <FileShareStorageLocation>
            <Path>
            </Path>
        </FileShareStorageLocation>
        <DefaultFileShareAccount>
            <Domain></Domain>
            <UserName></UserName>
            <Password></Password>
        </DefaultFileShareAccount>
    </Service>
    <UI>
        <ReportServerUrl>
        </ReportServerUrl>
        <PageCountMode>Estimate</PageCountMode>
    </UI>
    <Extensions>
        <Delivery>
            <Extension Name="Report Server FileShare" Type="Microsoft.ReportingServices.FileShareDeliveryProvider.FileShareProvider,ReportingServicesFileShareDeliveryProvider">
                <MaxRetries>3</MaxRetries>
                <SecondsBeforeRetry>900</SecondsBeforeRetry>
                <Configuration>
                    <FileShareConfiguration>
                        <ExcludedRenderFormats>
                            <RenderingExtension>HTMLOWC</RenderingExtension>
                            <RenderingExtension>NULL</RenderingExtension>
                            <RenderingExtension>RGDI</RenderingExtension>
                        </ExcludedRenderFormats>
                    </FileShareConfiguration>
                </Configuration>
            </Extension>
            <Extension Name="Report Server Email" Type="Microsoft.ReportingServices.EmailDeliveryProvider.EmailProvider,ReportingServicesEmailDeliveryProvider">
                <MaxRetries>3</MaxRetries>
                <SecondsBeforeRetry>900</SecondsBeforeRetry>
                <Configuration>
                    <RSEmailDPConfiguration>
                        <SMTPServer></SMTPServer>
                        <SMTPServerPort>
                        </SMTPServerPort>
                        <SMTPAccountName>
                        </SMTPAccountName>
                        <SMTPConnectionTimeout>
                        </SMTPConnectionTimeout>
                        <SMTPServerPickupDirectory>
                        </SMTPServerPickupDirectory>
                        <SMTPUseSSL>False</SMTPUseSSL>
                        <SendUsing>2</SendUsing>
                        <SMTPAuthenticate>0</SMTPAuthenticate>
                        <SendUserName></SendUserName>
                        <SendPassword></SendPassword>
                        <From></From>
                        <EmbeddedRenderFormats>
                            <RenderingExtension>MHTML</RenderingExtension>
                        </EmbeddedRenderFormats>
                        <PrivilegedUserRenderFormats>
                        </PrivilegedUserRenderFormats>
                        <ExcludedRenderFormats>
                            <RenderingExtension>HTMLOWC</RenderingExtension>
                            <RenderingExtension>NULL</RenderingExtension>
                            <RenderingExtension>RGDI</RenderingExtension>
                        </ExcludedRenderFormats>
                        <SendEmailToUserAlias>True</SendEmailToUserAlias>
                        <DefaultHostName>
                        </DefaultHostName>
                        <PermittedHosts>
                        </PermittedHosts>
                    </RSEmailDPConfiguration>
                </Configuration>
            </Extension>
            <Extension Name="Report Server DocumentLibrary" Type="Microsoft.ReportingServices.SharePoint.SharePointDeliveryExtension.DocumentLibraryProvider,ReportingServicesSharePointDeliveryExtension">
                <MaxRetries>3</MaxRetries>
                <SecondsBeforeRetry>900</SecondsBeforeRetry>
                <Configuration>
                    <DocumentLibraryConfiguration>
                        <ExcludedRenderFormats>
                            <RenderingExtension>HTMLOWC</RenderingExtension>
                            <RenderingExtension>NULL</RenderingExtension>
                            <RenderingExtension>RGDI</RenderingExtension>
                        </ExcludedRenderFormats>
                    </DocumentLibraryConfiguration>
                </Configuration>
            </Extension>
            <Extension Name="NULL" Type="Microsoft.ReportingServices.NullDeliveryProvider.NullProvider,ReportingServicesNullDeliveryProvider"/>
            <Extension Name="Report Server PowerBI" Type="Microsoft.ReportingServices.PowerBIDeliveryProvider.PowerBIDeliveryProvider,ReportingServicesPowerBIDeliveryProvider">
                <MaxRetries>3</MaxRetries>
                <SecondsBeforeRetry>900</SecondsBeforeRetry>
                <Configuration>
                    <PowerBIDeliveryConfiguration>
                    </PowerBIDeliveryConfiguration>
                </Configuration>
            </Extension>
        </Delivery>
        <DeliveryUI>
            <Extension Name="Report Server Email" Type="Microsoft.ReportingServices.EmailDeliveryProvider.EmailDeliveryProviderControl,ReportingServicesEmailDeliveryProvider">
                <DefaultDeliveryExtension>True</DefaultDeliveryExtension>
                <Configuration>
                    <RSEmailDPConfiguration>
                        <DefaultRenderingExtension>MHTML</DefaultRenderingExtension>
                    </RSEmailDPConfiguration>
                </Configuration>
            </Extension>
            <Extension Name="Report Server FileShare" Type="Microsoft.ReportingServices.FileShareDeliveryProvider.FileShareUIControl,ReportingServicesFileShareDeliveryProvider"/>
            <Extension Name="Report Server PowerBI" Type="Microsoft.ReportingServices.PowerBIDeliveryProvider.PowerBIDeliveryUIControl,ReportingServicesPowerBIDeliveryProvider"/>
        </DeliveryUI>
        <Render>
            <Extension Name="WORDOPENXML" Type="Microsoft.ReportingServices.Rendering.WordRenderer.WordOpenXmlRenderer.WordOpenXmlDocumentRenderer,Microsoft.ReportingServices.WordRendering"/>
            <Extension Name="WORD" Type="Microsoft.ReportingServices.Rendering.WordRenderer.WordDocumentRenderer,Microsoft.ReportingServices.WordRendering" Visible="false"/>
            <Extension Name="EXCELOPENXML" Type="Microsoft.ReportingServices.Rendering.ExcelOpenXmlRenderer.ExcelOpenXmlRenderer,Microsoft.ReportingServices.ExcelRendering"/>
            <Extension Name="EXCEL" Type="Microsoft.ReportingServices.Rendering.ExcelRenderer.ExcelRenderer,Microsoft.ReportingServices.ExcelRendering" Visible="false"/>
            <Extension Name="PPTX" Type="Microsoft.ReportingServices.Rendering.PowerPointRendering.PptxRenderingExtension,Microsoft.ReportingServices.PowerPointRendering"/>
            <Extension Name="PDF" Type="Microsoft.ReportingServices.Rendering.ImageRenderer.PDFRenderer,Microsoft.ReportingServices.ImageRendering"/>
            <Extension Name="IMAGE" Type="Microsoft.ReportingServices.Rendering.ImageRenderer.ImageRenderer,Microsoft.ReportingServices.ImageRendering"/>
            <Extension Name="MHTML" Type="Microsoft.ReportingServices.Rendering.HtmlRenderer.MHtmlRenderingExtension,Microsoft.ReportingServices.HtmlRendering">
                <Configuration>
                    <DeviceInfo>
                        <DataVisualizationFitSizing>Approximate</DataVisualizationFitSizing>
                    </DeviceInfo>
                </Configuration>
            </Extension>
            <Extension Name="CSV" Type="Microsoft.ReportingServices.Rendering.DataRenderer.CsvReport,Microsoft.ReportingServices.DataRendering"/>
            <Extension Name="XML" Type="Microsoft.ReportingServices.Rendering.DataRenderer.XmlDataReport,Microsoft.ReportingServices.DataRendering"/>
            <Extension Name="ATOM" Type="Microsoft.ReportingServices.Rendering.DataRenderer.AtomDataReport,Microsoft.ReportingServices.DataRendering"/>
            <Extension Name="NULL" Type="Microsoft.ReportingServices.Rendering.NullRenderer.NullReport,Microsoft.ReportingServices.NullRendering" Visible="false"/>
            <Extension Name="RGDI" Type="Microsoft.ReportingServices.Rendering.ImageRenderer.RGDIRenderer,Microsoft.ReportingServices.ImageRendering" Visible="false"/>
            <Extension Name="HTML4.0" Type="Microsoft.ReportingServices.Rendering.HtmlRenderer.Html40RenderingExtension,Microsoft.ReportingServices.HtmlRendering" Visible="false">
                <Configuration>
                    <DeviceInfo>
                        <DataVisualizationFitSizing>Approximate</DataVisualizationFitSizing>
                    </DeviceInfo>
                </Configuration>
            </Extension>
            <Extension Name="HTML5" Type="Microsoft.ReportingServices.Rendering.HtmlRenderer.Html5RenderingExtension,Microsoft.ReportingServices.HtmlRendering" Visible="false">
                <Configuration>
                    <DeviceInfo>
                        <DataVisualizationFitSizing>Approximate</DataVisualizationFitSizing>
                    </DeviceInfo>
                </Configuration>
            </Extension>
            <Extension Name="RPL" Type="Microsoft.ReportingServices.Rendering.RPLRendering.RPLRenderer,Microsoft.ReportingServices.RPLRendering" Visible="false" LogAllExecutionRequests="false"/>
        </Render>
        <!--
        For the SQLPDW extension to work, install the SQL Server PDW Client Tools on the report server.
        NOTE: The SQLPDW extension is deprecated. It supports old versions of SQL Server Parallel Data Warehouse (PDW).        
        To connect to Analytics Platform System, use the SQL (SQL Server) extension.        
        For the ORACLE extension to work, install the Oracle Data Provider for NET (ODP.NET) on the report server.
        For TERADATA extension to work, install the .NET Provider for Teradata on the report server.
      -->
        <Data>
            <Extension Name="SQL" Type="Microsoft.ReportingServices.DataExtensions.SqlConnectionWrapper,Microsoft.ReportingServices.DataExtensions"/>
            <Extension Name="SQLAZURE" Type="Microsoft.ReportingServices.DataExtensions.SqlAzureConnectionWrapper,Microsoft.ReportingServices.DataExtensions"/>
            <Extension Name="SQLPDW" Type="Microsoft.ReportingServices.DataExtensions.SqlDwConnectionWrapper,Microsoft.ReportingServices.DataExtensions"/>
            <Extension Name="OLEDB-MD" Type="Microsoft.ReportingServices.DataExtensions.AdoMdConnection,Microsoft.ReportingServices.DataExtensions"/>
            <Extension Name="SHAREPOINTLIST" Type="Microsoft.ReportingServices.DataExtensions.SharePointList.SPListConnection,Microsoft.ReportingServices.DataExtensions"/>
            <Extension Name="ORACLE" Type="Microsoft.ReportingServices.DataExtensions.OracleClientConnectionWrapper,Microsoft.ReportingServices.DataExtensions"/>
            <Extension Name="ESSBASE" Type="Microsoft.ReportingServices.DataExtensions.Essbase.EssbaseConnection,Microsoft.ReportingServices.DataExtensions.Essbase"/>
            <Extension Name="SAPBW" Type="Microsoft.ReportingServices.DataExtensions.SapBw.SapBwConnection,Microsoft.ReportingServices.DataExtensions.SapBw"/>
            <Extension Name="TERADATA" Type="Microsoft.ReportingServices.DataExtensions.TeradataConnectionWrapper,Microsoft.ReportingServices.DataExtensions"/>
            <Extension Name="OLEDB" Type="Microsoft.ReportingServices.DataExtensions.OleDbConnectionWrapper,Microsoft.ReportingServices.DataExtensions"/>
            <Extension Name="ODBC" Type="Microsoft.ReportingServices.DataExtensions.OdbcConnectionWrapper,Microsoft.ReportingServices.DataExtensions"/>
            <Extension Name="XML" Type="Microsoft.ReportingServices.DataExtensions.XmlDPConnection,Microsoft.ReportingServices.DataExtensions"/>
        </Data>
        <SemanticQuery>
            <Extension Name="SQL" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.MSSQL.MSSqlSQCommand,Microsoft.ReportingServices.SemanticQueryEngine">
                <Configuration>
                    <EnableMathOpCasting>False</EnableMathOpCasting>
                </Configuration>
            </Extension>
            <Extension Name="SQLAZURE" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.MSSQL.MSSqlSQCommand,Microsoft.ReportingServices.SemanticQueryEngine">
                <Configuration>
                    <EnableMathOpCasting>False</EnableMathOpCasting>
                </Configuration>
            </Extension>
            <Extension Name="SQLPDW" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.MSSQLADW.MSSqlAdwSQCommand,Microsoft.ReportingServices.SemanticQueryEngine">
                <Configuration>
                    <EnableMathOpCasting>False</EnableMathOpCasting>
                </Configuration>
            </Extension>
            <Extension Name="ORACLE" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.Oracle.OraSqlSQCommand,Microsoft.ReportingServices.SemanticQueryEngine">
                <Configuration>
                    <EnableMathOpCasting>True</EnableMathOpCasting>
                    <DisableNO_MERGEInLeftOuters>False</DisableNO_MERGEInLeftOuters>
                    <EnableUnistr>False</EnableUnistr>
                    <DisableTSTruncation>False</DisableTSTruncation>
                </Configuration>
            </Extension>
            <Extension Name="TERADATA" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.Teradata.TdSqlSQCommand,Microsoft.ReportingServices.SemanticQueryEngine">
                <Configuration>
                    <EnableMathOpCasting>True</EnableMathOpCasting>
                    <ReplaceFunctionName>oREPLACE</ReplaceFunctionName>
                </Configuration>
            </Extension>
            <Extension Name="OLEDB-MD" Type="Microsoft.AnalysisServices.Modeling.QueryExecution.ASSemanticQueryCommand,Microsoft.AnalysisServices.Modeling"/>
        </SemanticQuery>
        <ModelGeneration>
            <Extension Name="SQL" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.MSSQL.MsSqlModelGenerator,Microsoft.ReportingServices.SemanticQueryEngine"/>
            <Extension Name="SQLAZURE" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.MSSQL.MsSqlModelGenerator,Microsoft.ReportingServices.SemanticQueryEngine"/>
            <Extension Name="ORACLE" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.Oracle.OraSqlModelGenerator,Microsoft.ReportingServices.SemanticQueryEngine"/>
            <Extension Name="TERADATA" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.Teradata.TdSqlModelGenerator,Microsoft.ReportingServices.SemanticQueryEngine"/>
            <Extension Name="OLEDB-MD" Type="Microsoft.AnalysisServices.Modeling.Generation.ModelGeneratorExtention,Microsoft.AnalysisServices.Modeling"/>
        </ModelGeneration>
        <Security>
            <Extension Name="Windows" Type="Microsoft.ReportingServices.Authorization.WindowsAuthorization, Microsoft.ReportingServices.Authorization"/>
        </Security>
        <Authentication>
            <Extension Name="Windows" Type="Microsoft.ReportingServices.Authentication.WindowsAuthentication, Microsoft.ReportingServices.Authorization"/>
        </Authentication>
        <EventProcessing>
            <Extension Name="SnapShot Extension" Type="Microsoft.ReportingServices.Library.HistorySnapShotCreatedHandler,ReportingServicesLibrary">
                <Event>
                    <Type>ReportHistorySnapshotCreated</Type>
                </Event>
            </Extension>
            <Extension Name="Timed Subscription Extension" Type="Microsoft.ReportingServices.Library.TimedSubscriptionHandler,ReportingServicesLibrary">
                <Event>
                    <Type>TimedSubscription</Type>
                </Event>
            </Extension>
            <Extension Name="Cache Refresh Plan Extension" Type="Microsoft.ReportingServices.Library.CacheRefreshPlanHandler,ReportingServicesLibrary">
                <Event>
                    <Type>RefreshCache</Type>
                </Event>
            </Extension>
            <Extension Name="Shared Dataset Cache Update Extension" Type="Microsoft.ReportingServices.Library.SharedDatasetCacheUpdatePlanHandler,ReportingServicesLibrary">
                <Event>
                    <Type>SharedDatasetCacheUpdate</Type>
                </Event>
            </Extension>
            <Extension Name="Cache Update Extension" Type="Microsoft.ReportingServices.Library.ReportExecutionSnapshotUpdateEventHandler,ReportingServicesLibrary">
                <Event>
                    <Type>SnapshotUpdated</Type>
                </Event>
            </Extension>
        </EventProcessing>
    </Extensions>
    <MapTileServerConfiguration>
        <MaxConnections>2</MaxConnections>
        <Timeout>10</Timeout>
        <AppID>(Default)</AppID>
        <CacheLevel>Default</CacheLevel>
    </MapTileServerConfiguration>
</Configuration> 
```  
  
##  <a name="bkmk_sharepointdefaultfile"></a> Standardkonfigurationsdatei für einen Berichtsserver im SharePoint-Modus  
 Die Datei "rsreportserver.config" wird standardmäßig am folgenden Speicherort installiert:  
  
 **C:\Programme\Gemeinsame Dateien\Microsoft Shared\Web Server Extensions\15\WebServices\Reporting**  
  
```  
<Configuration>  
  <Dsn />  
  <ConnectionType>Default</ConnectionType>  
  <LogonUser>  
  </LogonUser>  
  <LogonDomain>  
  </LogonDomain>  
  <LogonCred>  
  </LogonCred>  
  <InstanceId>MSRS12.@Sharepoint</InstanceId>  
  <Add Key="SecureConnectionLevel" Value="0" />  
  <Add Key="CleanupCycleMinutes" Value="10" />  
  <Add Key="MaxActiveReqForOneUser" Value="20" />  
  <Add Key="AlertingCleanupCycleMinutes" Value="20" />  
  <Add Key="AlertingDataCleanupMinutes" Value="360" />  
  <Add Key="AlertingExecutionLogCleanupMinutes" Value="10080" />  
  <Add Key="AlertingMaxDataRetentionDays" Value="180" />  
  <Add Key="RunningRequestsScavengerCycle" Value="60" />  
  <Add Key="RunningRequestsDbCycle" Value="60" />  
  <Add Key="RunningRequestsAge" Value="30" />  
  <Add Key="MaxScheduleWait" Value="5" />  
  <Add Key="DisplayErrorLink" Value="true" />  
  <Add Key="WebServiceUseFileShareStorage" Value="false" />  
  <!--  <Add Key="ProcessTimeout" Value="150" /> -->  
  <!--  <Add Key="ProcessTimeoutGcExtension" Value="30" /> -->  
  <!--  <Add Key="WatsonFlags" Value="0x0430" /> full dump-->  
  <!--  <Add Key="WatsonFlags" Value="0x0428" /> minidump -->  
  <!--  <Add Key="WatsonFlags" Value="0x0002" /> no dump-->  
  <Add Key="WatsonFlags" Value="0x0428" />  
  <Add Key="WatsonDumpOnExceptions" Value="Microsoft.ReportingServices.Diagnostics.Utilities.InternalCatalogException,Microsoft.ReportingServices.Modeling.InternalModelingException,Microsoft.ReportingServices.ReportProcessing.UnhandledReportRenderingException" />  
  <Add Key="WatsonDumpExcludeIfContainsExceptions" Value="System.Threading.ThreadAbortException,System.Web.UI.ViewStateException,System.OutOfMemoryException,System.Web.HttpException,System.IO.IOException,System.IO.FileLoadException,Microsoft.SharePoint.SPException,Microsoft.ReportingServices.WmiProvider.WMIProviderException" />  
  <RStrace>  
    <add name="FileName" value="ReportServerService" />  
    <add name="FileSizeLimitMb" value="32" />  
    <add name="KeepFilesForDays" value="14" />  
    <add name="Prefix" value="tid, time" />  
    <add name="TraceListeners" value="file" />  
    <add name="TraceFileMode" value="unique" />  
    <add name="Components" value="all:3" />  
  </RStrace>  
  <URLReservations>  
    <Application>  
      <Name>ReportServerWebService</Name>  
      <VirtualDirectory>ReportServer</VirtualDirectory>  
      <URLs>  
        <URL>  
          <UrlString>http://+:80</UrlString>  
          <AccountSid>  
          </AccountSid>  
          <AccountName>  
          </AccountName>  
        </URL>  
      </URLs>  
    </Application>  
    <Application>  
      <Name>ReportManager</Name>  
      <VirtualDirectory>Reports</VirtualDirectory>  
      <URLs>  
        <URL>  
          <UrlString>http://+:80</UrlString>  
          <AccountSid>  
          </AccountSid>  
          <AccountName>  
          </AccountName>  
        </URL>  
      </URLs>  
    </Application>  
  </URLReservations>  
  <Authentication>  
    <AuthenticationTypes>  
      <RSWindowsNTLM />  
    </AuthenticationTypes>  
    <EnableAuthPersistence>true</EnableAuthPersistence>  
  </Authentication>  
  <Service>  
    <IsSchedulingService>True</IsSchedulingService>  
    <IsNotificationService>True</IsNotificationService>  
    <IsEventService>True</IsEventService>  
    <IsAlertingService>True</IsAlertingService>  
    <PollingInterval>10</PollingInterval>  
    <WindowsServiceUseFileShareStorage>False</WindowsServiceUseFileShareStorage>  
    <MemorySafetyMargin>80</MemorySafetyMargin>  
    <MemoryThreshold>90</MemoryThreshold>  
    <RecycleTime>720</RecycleTime>  
    <MaxAppDomainUnloadTime>30</MaxAppDomainUnloadTime>  
    <MaxQueueThreads>0</MaxQueueThreads>  
    <UrlRoot>  
    </UrlRoot>  
    <PolicyLevel>rssrvpolicy.config</PolicyLevel>  
    <IsWebServiceEnabled>True</IsWebServiceEnabled>    
    <FileShareStorageLocation>  
      <Path>  
      </Path>  
    </FileShareStorageLocation>  
  </Service>  
  <UI>  
    <ReportServerUrl>  
    </ReportServerUrl>  
    <PageCountMode>Estimate</PageCountMode>  
  </UI>  
  <MapTileServerConfiguration>  
    <MaxConnections>2</MaxConnections>  
    <Timeout>10</Timeout>  
    <AppID>(Default)</AppID>  
    <CacheLevel>Default</CacheLevel>  
  </MapTileServerConfiguration>  
</Configuration>  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Ändern einer Reporting Services-Konfigurationsdatei &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)   
 [Konfigurieren von verfügbarem Speicher für Berichtsserveranwendungen](../../reporting-services/report-server/configure-available-memory-for-report-server-applications.md)   
 [Reporting Services-Konfigurationsdateien](../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [Initialisieren eines Berichtsservers (SSRS-Konfigurations-Manager)](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)   
 [Speichern verschlüsselter Berichtsserverdaten (SSRS-Konfigurations-Manager)](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [Reporting Services-Konfigurations-Manager &#40;einheitlicher Modus&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)  
 Haben Sie dazu Fragen? [Besuchen Sie das Reporting Services-Forum](http://go.microsoft.com/fwlink/?LinkId=620231)
  
  

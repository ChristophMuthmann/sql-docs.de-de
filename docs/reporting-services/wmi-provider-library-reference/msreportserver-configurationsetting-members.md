---
title: "MSReportServer_ConfigurationSetting-Member | Microsoft Docs"
ms.custom: ""
ms.date: "03/20/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
apiname: 
  - "MSReportServer_ConfigurationSetting Members"
apilocation: 
  - "reportingservices.mof"
apitype: "MOFDef"
helpviewer_keywords: 
  - "WMI-Anbieter [Reporting Services], MSReportServer_ConfigurationSetting-Klasse"
  - "MSReportServer_ConfigurationSetting-Klasse"
ms.assetid: 5e21a53a-a2f8-4b35-a8d9-5483519e3857
caps.latest.revision: 46
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 46
---
# MSReportServer_ConfigurationSetting-Member
  Die MSReportServer_ConfigurationSetting-Klasse enthält die folgenden Eigenschaften und Methoden.  
  
## Öffentliche Eigenschaften  
  
|||  
|-|-|  
|[ConnectionPoolSize](../../reporting-services/wmi-provider-library-reference/connectionpoolsize-property-wmi-msreportserver-configurationsetting.md)|Gibt die Größe des Verbindungspools zurück, über den der Berichtsserver mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] kommuniziert, die die Berichtsserver-Datenbank hostet. Schreibgeschützt.|  
|[DatabaseLogonAccount](../../reporting-services/wmi-provider-library-reference/databaselogonaccount-property-wmi-msreportserver-configurationsetting.md)|Gibt das Anmeldekonto an, über das der Berichtsserver eine Verbindung mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] kommuniziert, die die Berichtsserver-Datenbank hostet. Schreibgeschützt.|  
|[DatabaseLogonTimeout](../../reporting-services/wmi-provider-library-reference/databaselogontimeout-property-wmi-msreportserver-configurationsetting.md)|Gibt die Anzahl von Sekunden an, die gewartet wird, ehe ein Anmeldeversuch bei der Berichtsserver-Datenbank fehlschlägt. Schreibgeschützt.|  
|[DatabaseLogonType](../../reporting-services/wmi-provider-library-reference/databaselogontype-property-wmi-msreportserver-configurationsetting.md)|Gibt an, ob der Berichtsserver für den Zugriff auf die Berichtsserver-Datenbank ein Windows-Dienstkonto, ein Windows-Benutzerkonto oder eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldung verwendet. Schreibgeschützt.|  
|[DatabaseName](../../reporting-services/wmi-provider-library-reference/databasename-property-wmi-msreportserver-configurationsetting.md)|Gibt den Namen der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz an, die die Berichtsserver-Datenbank hostet|  
|[DatabaseQueryTimeout](../../reporting-services/wmi-provider-library-reference/databasequerytimeout-property-wmi-msreportserver-configurationsetting.md)|Gibt die Anzahl von Sekunden an, die verstreichen müssen, ehe der Befehl fehlschlägt oder wegen eines Timeouts abgebrochen wird. Der Berichtsserver nimmt die zeitliche Steuerung des Prozesses anhand der Berichtsserver-Datenbank und nicht anhand einer Datenquelle für den Bericht vor.|  
|[DatabaseServerName](../../reporting-services/wmi-provider-library-reference/databaseservername-property-wmi-msreportserver-configurationsetting.md)|Gibt den Namen des Servers an, auf dem die Berichtsserver-Datenbank installiert ist|  
|[InstallationID-Eigenschaft](../../reporting-services/wmi-provider-library-reference/installationid-property-wmi-msreportserver-configurationsetting.md)|Gibt einen eindeutigen Bezeichner für eine bestimmte Berichtsserverinstanz zurück|  
|[InstanceName](../../reporting-services/wmi-provider-library-reference/instancename-property-wmi-msreportserver-configurationsetting.md)|Gibt den Namen einer Berichtsserverinstanz auf einem bestimmten Computer an.|  
|[IsInitialized](../../reporting-services/wmi-provider-library-reference/isinitialized-property-wmi-msreportserver-configurationsetting.md)|Gibt an, ob die Berichtsserverinstanz initialisiert wurde. Schreibgeschützt.|  
|[IsSharePointIntegrated](../../reporting-services/wmi-provider-library-reference/issharepointintegrated-property-wmi.md)|Gibt an, ob der Berichtsserver für den integrierten SharePoint-Modus konfiguriert ist.|  
|[IsWebServiceEnabled](../../reporting-services/wmi-provider-library-reference/iswebserviceenabled-property-wmi-msreportserver-configurationsetting.md)|Gibt an, ob der Report Server-Webdienst aktiviert ist. Schreibgeschützt.|  
|[IsWindowsServiceEnabled](../../reporting-services/wmi-provider-library-reference/iswindowsserviceenabled-property-wmi-msreportserver-configurationsetting.md)|Gibt an, ob der Report Server-Windows-Dienst aktiviert ist. Schreibgeschützt.|  
|[MachineAccountIdentity-Eigenschaft &#40;WMI&#41;](../../reporting-services/wmi-provider-library-reference/machineaccountidentity-property-wmi.md)|Ruft die Computerkontoidentität des Computers ab, auf dem der Berichtsserver installiert ist|  
|[PathName](../../reporting-services/wmi-provider-library-reference/pathname-property-wmi-msreportserver-configurationsetting.md)|Gibt den Installationspfad zu einer Berichtsserverinstanz an|  
|[SecureConnectionLevel](../../reporting-services/wmi-provider-library-reference/secureconnectionlevel-property-wmi-msreportserver-configurationsetting.md)|Gibt die in der Datei RSReportServer.config angegebene sichere Verbindungsebene zurück.|  
|[SenderEmailAddress](../../reporting-services/wmi-provider-library-reference/senderemailaddress-property-wmi-msreportserver-configurationsetting.md)|Ruft die Adresse ab, die verwendet wird, um E-Mails vom Berichtsserver zu senden. Schreibgeschützt.|  
|[SendUsingSMTPServer](../../reporting-services/wmi-provider-library-reference/sendusingsmtpserver-property-wmi-msreportserver-configurationsetting.md)|Gibt an, ob die SendUsing-Eigenschaft in der E-Mail-Konfiguration auf TRUE festgelegt wurde|  
|[SMTPServer](../../reporting-services/wmi-provider-library-reference/smtpserver-property-wmi-msreportserver-configurationsetting.md)|Ruft die SMTP-Server-Eigenschaft aus der Datei RSReportServer.config ab. Schreibgeschützt.|  
|[UnattendedExecutionAccount](../../reporting-services/wmi-provider-library-reference/unattendedexecutionaccount-property-wmi-msreportserver-configurationsetting.md)|Gibt das Benutzerkonto für die Anmeldung an, dessen Identität der Berichtsserver bei der unbeaufsichtigten Ausführung von Berichten annimmt. Schreibgeschützt.|  
|[Version](../../reporting-services/wmi-provider-library-reference/version-property-wmi-msreportserver-configurationsetting.md)|Gibt die Version des Berichtsservers zurück|  
|[VirtualDirectoryReportManager-Eigenschaft &#40;WMI: MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/virtualdirectoryreportmanager-property-wmi-msreportserver-configurationsetting.md)|Gibt das virtuelle Verzeichnis für die Berichts-Manager-Anwendung zurück|  
|[VirtualDirectoryReportServer-Eigenschaft &#40;WMI: MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/virtualdirectoryreportserver-property-wmi-msreportserver-configurationsetting.md)|Gibt das virtuelle Verzeichnis für die Report Server-Webdienstanwendung zurück|  
|[WindowsServiceIdentityActual](../../reporting-services/wmi-provider-library-reference/windowsserviceidentityactual-property-wmi-msreportserver-configurationsetting.md)|Gibt die Identität zurück, unter der der Report Server-Windows-Dienst tatsächlich ausgeführt wird. Schreibgeschützt.|  
|[WindowsServiceIdentityConfigured](../../reporting-services/wmi-provider-library-reference/windowsserviceidentityconfigured-property.md)|Gibt die Identität zurück, unter der der Report Server-Windows-Dienst entsprechend seiner letzten Konfiguration ausgeführt wird. Schreibgeschützt.|  
  
## Öffentliche Methoden  
  
|||  
|-|-|  
|[BackupEncryptionKey](../../reporting-services/wmi-provider-library-reference/backupencryptionkey-method-wmi-msreportserver-configurationsetting.md)|Sichert den Verschlüsselungsschlüssel für die Instanz. Der Verschlüsselungsschlüssel wird mit einem Kennwort verschlüsselt gespeichert.|  
|[CreateSSLCertificateBinding-Methode &#40;WMI: MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/createsslcertificatebinding-method-wmi-msreportserver-configurationsetting.md)|Erstellt eine SSL-Zertifikatsbindung|  
|[DeleteEncryptedInformation](../../reporting-services/wmi-provider-library-reference/deleteencryptedinformation-method-wmi-msreportserver-configurationsetting.md)|Löscht die verschlüsselten Informationen aus der Berichtsserver-Datenbank|  
|[DeleteEncryptionKey](../../reporting-services/wmi-provider-library-reference/deleteencryptionkey-method-wmi-msreportserver-configurationsetting.md)|Löscht die Verschlüsselungsschlüssel aus der Berichtsserver-Datenbank|  
|[GenerateDatabaseCreationScript](../../reporting-services/wmi-provider-library-reference/generatedatabasecreationscript-method-wmi-msreportserver-configurationsetting.md)|Generiert ein SQL-Skript, mit dem die Berichtsserver-Datenbank erstellt werden kann|  
|[GenerateDatabaseRightsScript](../../reporting-services/wmi-provider-library-reference/generatedatabaserightsscript-method-wmi-msreportserver-configurationsetting.md)|Generiert ein SQL-Skript, mit dem einem Benutzer Berechtigungen für die Berichtsserver-Datenbank erteilt werden können|  
|[GenerateDatabaseUpgradeScript](../../reporting-services/wmi-provider-library-reference/generatedatabaseupgradescript-method-wmi-msreportserver-configurationsetting.md)|Generiert ein SQL-Skript, mit dem die Berichtsserver-Datenbank aktualisiert werden kann|  
|[GetAdminSiteUrl-Methode &#40;WMI&#41;](../../reporting-services/wmi-provider-library-reference/getadminsiteurl-method-wmi.md)|Ruft die absolute URL für die Zentraladministrationswebsite ab|  
|[GetDatabaseVersionDisplayName](../../reporting-services/wmi-provider-library-reference/getdatabaseversiondisplayname-method-wmi.md)|Ruft den Anzeigenamen für eine gegebene Versionszeichenfolge in der Berichtsserver-Datenbank ab|  
|[InitializeReportServer](../../reporting-services/wmi-provider-library-reference/initializereportserver-method-wmi-msreportserver-configurationsetting.md)|Initialisiert die angegebene Berichtsserverinstanz.|  
|[ListInstalledSharePointVersions-Methode &#40;WMI&#41;](../../reporting-services/wmi-provider-library-reference/listinstalledsharepointversions-method-wmi.md)|Gibt einen Satz von Token zurück, die die Versionen von [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] [!INCLUDE[offSPServ](../../includes/offspserv-md.md)], [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]oder [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] darstellen, die auf dem gleichen Computer wie der Berichtsserver installiert sind.|  
|[ListIPAddresses-Methode &#40;WMI: MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/listipaddresses-method-wmi-msreportserver-configurationsetting.md)|Listet IP-Adressen für den Computer auf|  
|[ListReportServersInDatabase](../../reporting-services/wmi-provider-library-reference/listreportserversindatabase-method-wmi-msreportserver-configurationsetting.md)|Gibt eine Liste von Berichtsserverinstallationen zurück, die in der Berichtsserver-Datenbank vorhanden sind. Dies geschieht unabhängig davon, ob diese Installationen Zugriff auf sichere Informationen haben.|  
|[ListReservedURLs-Methode &#40;WMI: MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/listreservedurls-method-wmi-msreportserver-configurationsetting.md)|Listet für alle Anwendungen auf dem Berichtsserver reservierte URLs auf|  
|[ListSSLCertificateBindings-Methode &#40;WMI: MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/listsslcertificatebindings-method-wmi-msreportserver-configurationsetting.md)|Listet die in HTTP.SYS vorhandenen und die von rsreportserver.config erwarteten SSL-Zertifikatsbindungen auf|  
|[ListSSLCertificates-Methode &#40;WMI: MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/listsslcertificates-method-wmi-msreportserver-configurationsetting.md)|Listet die auf dem Computer installierten SSL-Zertifikate auf.|  
|[ReencryptSecureInformation](../../reporting-services/wmi-provider-library-reference/reencryptsecureinformation-method-wmi-msreportserver-configurationsetting.md)|Generiert einen neuen Verschlüsselungsschlüssel und verschlüsselt alle sicheren Informationen in der Berichtsserver-Datenbank erneut mit diesem neuen Schlüssel|  
|[RemoveSSLCertificateBindings-Methode &#40;WMI: MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/removesslcertificatebindings-method-wmi-msreportserver-configurationsetting.md)|Entfernt eine SSL-Zertifikatsbindung|  
|[RemoveUnattendedExecutionAccount](../../reporting-services/wmi-provider-library-reference/removeunattendedexecutionaccount-method-wmi-msreportserver-configurationsetting.md)|Löscht den Eintrag für das Konto für die unbeaufsichtigte Ausführung aus der Berichtsserverkonfiguration|  
|[RemoveURL-Methode &#40;WMI: MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/removeurl-method-wmi-msreportserver-configurationsetting.md)|Entfernt eine für den Berichtsserver reservierte URL|  
|[ReserveURL-Methode &#40;WMI: MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/reserveurl-method-wmi-msreportserver-configurationsetting.md)|Fügt eine URL-Reservierung für eine gegebene Anwendung hinzu|  
|[RestoreEncryptionKey](../../reporting-services/wmi-provider-library-reference/restoreencryptionkey-method-wmi-msreportserver-configurationsetting.md)|Wendet den angegebenen Verschlüsselungsschlüssel erneut auf die Berichtsserver-Datenbank an|  
|[SetDatabaseConnection](../../reporting-services/wmi-provider-library-reference/setdatabaseconnection-method-wmi-msreportserver-configurationsetting.md)|Legt die Berichtsserver-Datenbankverbindung auf eine bestimmte Berichtsserver-Datenbank fest|  
|[SetDatabaseLogonTimeout](../../reporting-services/wmi-provider-library-reference/setdatabaselogontimeout-method-wmi-msreportserver-configurationsetting.md)|Gibt den Standardtimeoutwert für Anmeldeversuche bei der Berichtsserver-Datenbank an|  
|[SetDatabaseQueryTimeout](../../reporting-services/wmi-provider-library-reference/setdatabasequerytimeout-method-wmi-msreportserver-configurationsetting.md)|Gibt den Standardtimeoutwert für Verbindungen mit der Berichtsserver-Datenbank an|  
|[SetEmailConfiguration](../../reporting-services/wmi-provider-library-reference/setemailconfiguration-method-wmi-msreportserver-configurationsetting.md)|Konfiguriert die E-Mail-Übermittlungserweiterung, die vom Berichtsserver zum Senden von E-Mails verwendet wird|  
|[SetSecureConnectionLevel](../../reporting-services/wmi-provider-library-reference/setsecureconnectionlevel-method-wmi-msreportserver-configurationsetting.md)|Legt die sichere Verbindungsebene des Berichtsservers fest|  
|[SetServiceState](../../reporting-services/wmi-provider-library-reference/setservicestate-method-wmi-msreportserver-configurationsetting.md)|Aktiviert und deaktiviert den Berichtsserver-Windows-Dienst und den Berichtsserver-Webdienst.|  
|[SetUnattendedExecutionAccount](../../reporting-services/wmi-provider-library-reference/setunattendedexecutionaccount-method-wmi-msreportserver-configurationsetting.md)|Gibt das Konto an, das verwendet wird, um Berichte unbeaufsichtigt auszuführen|  
|[SetVirtualDirectory-Methode &#40;WMI: MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/setvirtualdirectory-method-wmi-msreportserver-configurationsetting.md)|Legt das virtuelle Verzeichnis für eine Anwendung fest|  
|[SetWindowsServiceIdentity](../../reporting-services/wmi-provider-library-reference/setwindowsserviceidentity-method-wmi-msreportserver-configurationsetting.md)|Lässt den Berichtsserver-Windows-Dienst als den angegebenen Windows-Benutzer ausführen und gewährt diesem Konto die erforderlichen Dateisystemberechtigungen, damit der Berichtsserver ausgeführt werden kann.|  
  
## Siehe auch  
 [MSReportServer_ConfigurationSetting-Klasse](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
  
---
title: "MSReportServer_ConfigurationSetting-Methoden | Microsoft Docs"
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
  - "MSReportServer_ConfigurationSetting Methods"
apilocation: 
  - "reportingservices.mof"
apitype: "MOFDef"
helpviewer_keywords: 
  - "WMI-Anbieter [Reporting Services], MSReportServer_ConfigurationSetting-Klasse"
  - "MSReportServer_ConfigurationSetting-Klasse"
ms.assetid: a08c2476-5b8e-4792-94da-1360fe231c6e
caps.latest.revision: 45
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 45
---
# MSReportServer_ConfigurationSetting-Methoden
  Die MSReportServer_ConfigurationSetting-Klasse des Berichtsserver-WMI-Anbieters stellt die folgenden öffentlichen Methoden bereit.  
  
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
|[GetAdminSiteUrl Method &#40;WMI&#41;](../../reporting-services/wmi-provider-library-reference/getadminsiteurl-method-wmi.md)|Ruft die absolute URL für die Zentraladministrationswebsite ab|  
|[GetDatabaseVersionDisplayName](../../reporting-services/wmi-provider-library-reference/getdatabaseversiondisplayname-method-wmi.md)|Ruft den Anzeigenamen für eine gegebene Versionszeichenfolge in der Berichtsserver-Datenbank ab|  
|[InitializeReportServer](../../reporting-services/wmi-provider-library-reference/initializereportserver-method-wmi-msreportserver-configurationsetting.md)|Initialisiert die angegebene Berichtsserverinstanz.|  
|[ListInstalledSharePointVersions-Methode &#40;WMI&#41;](../../reporting-services/wmi-provider-library-reference/listinstalledsharepointversions-method-wmi.md)|Gibt einen Satz von Token zurück, die die Versionen von Microsoft [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] [!INCLUDE[offSPServ](../../includes/offspserv-md.md)], [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]oder [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] darstellen, die auf dem gleichen Computer wie der Berichtsserver installiert sind.|  
|[ListIPAddresses-Methode &#40;WMI: MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/listipaddresses-method-wmi-msreportserver-configurationsetting.md)|Listet IP-Adressen für den Computer auf|  
|[ListReportServersInDatabase](../../reporting-services/wmi-provider-library-reference/listreportserversindatabase-method-wmi-msreportserver-configurationsetting.md)|Gibt eine Liste von Berichtsserverinstallationen zurück, die in der Berichtsserver-Datenbank vorhanden sind. Dies geschieht unabhängig davon, ob diese Installationen Zugriff auf sichere Informationen haben.|  
|[ListReservedURLs-Methode &#40;WMI: MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/listreservedurls-method-wmi-msreportserver-configurationsetting.md)|Listet für alle Anwendungen auf dem Berichtsserver reservierte URLs auf|  
|[ListSSLCertificateBindings-Methode &#40;WMI: MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/listsslcertificatebindings-method-wmi-msreportserver-configurationsetting.md)|Listet die in HTTP.SYS vorhandenen und die von RSReportServer.config erwarteten SSL-Zertifikatsbindungen auf.|  
|[ListSSLCertificates-Methode &#40;WMI: MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/listsslcertificates-method-wmi-msreportserver-configurationsetting.md)|Listet die auf dem Computer installierten SSL-Zertifikate auf.|  
|[ReencryptSecureInformation](../../reporting-services/wmi-provider-library-reference/reencryptsecureinformation-method-wmi-msreportserver-configurationsetting.md)|Generiert einen neuen Verschlüsselungsschlüssel und verschlüsselt alle sicheren Informationen in der Berichtsserver-Datenbank erneut mit diesem neuen Schlüssel|  
|[RemoveSSLCertificateBindings-Methode &#40;WMI: MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/removesslcertificatebindings-method-wmi-msreportserver-configurationsetting.md)|Entfernt eine SSL-Zertifikatsbindung|  
|[RemoveUnattendedExecutionAccount](../../reporting-services/wmi-provider-library-reference/removeunattendedexecutionaccount-method-wmi-msreportserver-configurationsetting.md)|Löscht den Eintrag für das Konto für die unbeaufsichtigte Ausführung aus der Berichtsserverkonfiguration|  
|[RemoveURL-Methode &#40;WMI: MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/removeurl-method-wmi-msreportserver-configurationsetting.md)|Entfernt eine für den Berichtsserver reservierte URL|  
|[ReserveURL-Methode &#40;WMI: MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/reserveurl-method-wmi-msreportserver-configurationsetting.md)|Fügt eine URL-Reservierung für eine gegebene Anwendung hinzu|  
|[RestoreEncryptionKey](../../reporting-services/wmi-provider-library-reference/restoreencryptionkey-method-wmi-msreportserver-configurationsetting.md)|Wendet den angegebenen Verschlüsselungsschlüssel erneut auf die Berichtsserver-Datenbank an|  
|[SetDatabaseConnection](../../reporting-services/wmi-provider-library-reference/setdatabaseconnection-method-wmi-msreportserver-configurationsetting.md)|Legt die Berichtsserver-Datenbankverbindung auf eine bestimmte Berichtsserver-Datenbank fest|  
|[SetDatabaseLogonTimeout](../../reporting-services/wmi-provider-library-reference/setdatabaselogontimeout-method-wmi-msreportserver-configurationsetting.md)|Gibt den Standardtimeoutwert für Anmeldeversuche bei der Berichtsserver-Datenbank an|  
|[SetDatabaseQueryTimeout](../../reporting-services/wmi-provider-library-reference/setdatabasequerytimeout-method-wmi-msreportserver-configurationsetting.md)|Gibt den Standardtimeoutwert für Berichtsserver-Datenbankabfragen an.|  
|[SetEmailConfiguration](../../reporting-services/wmi-provider-library-reference/setemailconfiguration-method-wmi-msreportserver-configurationsetting.md)|Konfiguriert die E-Mail-Übermittlungserweiterung, die vom Berichtsserver zum Senden von E-Mails verwendet wird|  
|[SetSecureConnectionLevel](../../reporting-services/wmi-provider-library-reference/setsecureconnectionlevel-method-wmi-msreportserver-configurationsetting.md)|Legt die sichere Verbindungsebene des Berichtsservers fest|  
|[SetServiceState](../../reporting-services/wmi-provider-library-reference/setservicestate-method-wmi-msreportserver-configurationsetting.md)|Schaltet den Berichtsserverdienst ein und aus|  
|[SetUnattendedExecutionAccount](../../reporting-services/wmi-provider-library-reference/setunattendedexecutionaccount-method-wmi-msreportserver-configurationsetting.md)|Gibt das Konto an, das verwendet wird, um Berichte unbeaufsichtigt auszuführen|  
|[SetVirtualDirectory-Methode &#40;WMI: MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/setvirtualdirectory-method-wmi-msreportserver-configurationsetting.md)|Legt das virtuelle Verzeichnis für eine Anwendung fest|  
|[SetWindowsServiceIdentity](../../reporting-services/wmi-provider-library-reference/setwindowsserviceidentity-method-wmi-msreportserver-configurationsetting.md)|Lässt den Berichtsserverdienst als den angegebenen Windows-Benutzer ausführen und gewährt diesem Konto die erforderlichen Dateisystemberechtigungen, damit der Berichtsserver ausgeführt werden kann.|  
  
## Siehe auch  
 [MSReportServer_ConfigurationSetting-Klasse](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
  
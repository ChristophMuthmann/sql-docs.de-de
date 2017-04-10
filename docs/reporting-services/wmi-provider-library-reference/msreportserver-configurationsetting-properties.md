---
title: "MSReportServer_ConfigurationSetting-Eigenschaften | Microsoft Docs"
ms.custom: 
  - "force 2/17"
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
apiname: 
  - "MSReportServer_ConfigurationSetting Properties"
apilocation: 
  - "reportingservices.mof"
apitype: "MOFDef"
helpviewer_keywords: 
  - "WMI-Anbieter [Reporting Services], MSReportServer_ConfigurationSetting-Klasse"
  - "MSReportServer_ConfigurationSetting-Klasse"
ms.assetid: e75fe1e5-197b-4c65-859b-370821cad003
caps.latest.revision: 48
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 45
---
# MSReportServer_ConfigurationSetting-Eigenschaften
  Die „MSReportServer_ConfigurationSetting“-Klasse stellt die Installations- und die Laufzeitparameter einer Berichtsserverinstanz dar. Diese Einstellungen werden in der Konfigurationsdatei RSReportServer.config gespeichert.  
  
## Öffentliche Eigenschaften  
  
|||  
|-|-|  
|[ConnectionPoolSize](../../reporting-services/wmi-provider-library-reference/connectionpoolsize-property-wmi-msreportserver-configurationsetting.md)|Gibt die Größe des Verbindungspools zurück, über den der Berichtsserver mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] kommuniziert, die die Berichtsserver-Datenbank hostet. Schreibgeschützt.|  
|[DatabaseLogonAccount](../../reporting-services/wmi-provider-library-reference/databaselogonaccount-property-wmi-msreportserver-configurationsetting.md)|Gibt das Anmeldekonto an, über das der Berichtsserver eine Verbindung mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] kommuniziert, die die Berichtsserver-Datenbank hostet. Schreibgeschützt.|  
|[DatabaseLogonTimeout](../../reporting-services/wmi-provider-library-reference/databaselogontimeout-property-wmi-msreportserver-configurationsetting.md)|Gibt die Anzahl von Sekunden an, die gewartet wird, ehe ein Anmeldeversuch bei der Berichtsserver-Datenbank fehlschlägt. Schreibgeschützt.|  
|[DatabaseLogonType](../../reporting-services/wmi-provider-library-reference/databaselogontype-property-wmi-msreportserver-configurationsetting.md)|Gibt an, ob der Berichtsserver für den Zugriff auf die Berichtsserver-Datenbank ein Windows-Dienstkonto, ein Windows-Benutzerkonto oder eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldung verwendet. Schreibgeschützt.|  
|[DatabaseName](../../reporting-services/wmi-provider-library-reference/databasename-property-wmi-msreportserver-configurationsetting.md)|Gibt den Namen der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz an, die die Berichtsserver-Datenbank hostet|  
|[DatabaseQueryTimeout](../../reporting-services/wmi-provider-library-reference/databasequerytimeout-property-wmi-msreportserver-configurationsetting.md)|Gibt die Anzahl von Sekunden an, die verstreichen müssen, ehe der Befehl fehlschlägt oder wegen eines Timeouts abgebrochen wird. Der Berichtsserver nimmt die zeitliche Steuerung des Prozesses anhand des SQL Server-Katalogs und nicht anhand einer Datenquelle für den Bericht vor.|  
|[DatabaseServerName](../../reporting-services/wmi-provider-library-reference/databaseservername-property-wmi-msreportserver-configurationsetting.md)|Gibt den Namen des Servers an, auf dem die Berichtsserver-Datenbank installiert ist|  
|[InstallationID-Eigenschaft](../../reporting-services/wmi-provider-library-reference/installationid-property-wmi-msreportserver-configurationsetting.md)|Gibt einen eindeutigen Bezeichner für eine bestimmte Berichtsserverinstanz zurück|  
|[InstanceName](../../reporting-services/wmi-provider-library-reference/instancename-property-wmi-msreportserver-configurationsetting.md)|Gibt den Namen einer Berichtsserverinstanz auf einem bestimmten Computer an.|  
|[IsInitialized](../../reporting-services/wmi-provider-library-reference/isinitialized-property-wmi-msreportserver-configurationsetting.md)|Gibt an, ob die Berichtsserverinstanz initialisiert wurde.  Schreibgeschützt.|  
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
|[VirtualDirectoryReportManager-Eigenschaft &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/virtualdirectoryreportmanager-property-wmi-msreportserver-configurationsetting.md)|Gibt das virtuelle Verzeichnis für die Berichts-Manager-Anwendung zurück|  
|[VirtualDirectoryReportManager-Eigenschaft &#40;WMI: MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/virtualdirectoryreportserver-property-wmi-msreportserver-configurationsetting.md)|Gibt das virtuelle Verzeichnis für die Report Server-Webdienstanwendung zurück|  
|[WindowsServiceIdentityActual](../../reporting-services/wmi-provider-library-reference/windowsserviceidentityactual-property-wmi-msreportserver-configurationsetting.md)|Gibt die Identität zurück, unter der der Report Server-Windows-Dienst tatsächlich ausgeführt wird. Schreibgeschützt.|  
|[WindowsServiceIdentityConfigured](../../reporting-services/wmi-provider-library-reference/windowsserviceidentityconfigured-property.md)|Gibt die Identität zurück, unter der der Report Server-Windows-Dienst entsprechend seiner letzten Konfiguration ausgeführt wird. Schreibgeschützt.|  
  
## Siehe auch  
 [MSReportServer_ConfigurationSetting-Member](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
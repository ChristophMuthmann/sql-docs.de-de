---
title: MSReportServer_ConfigurationSetting-Eigenschaften | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: wmi-provider-library-reference
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
apiname: MSReportServer_ConfigurationSetting Properties
apilocation: reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- WMI provider [Reporting Services], MSReportServer_ConfigurationSetting class
- MSReportServer_ConfigurationSetting class
ms.assetid: e75fe1e5-197b-4c65-859b-370821cad003
caps.latest.revision: "48"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: b2a336cd583cdb629620b881a06d5a1fa46088e9
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="msreportserverconfigurationsetting-properties"></a>MSReportServer_ConfigurationSetting-Eigenschaften
  Die „MSReportServer_ConfigurationSetting“-Klasse stellt die Installations- und die Laufzeitparameter einer Berichtsserverinstanz dar. Diese Einstellungen werden in der Konfigurationsdatei RSReportServer.config gespeichert.  
  
## <a name="public-properties"></a>Öffentliche Eigenschaften  
  
|||  
|-|-|  
|[ConnectionPoolSize](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-connectionpoolsize.md)|Gibt die Größe des Verbindungspools zurück, über den der Berichtsserver mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] kommuniziert, die die Berichtsserver-Datenbank hostet. Schreibgeschützt.|  
|[DatabaseLogonAccount](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaselogonaccount.md)|Gibt das Anmeldekonto an, über das der Berichtsserver eine Verbindung mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] kommuniziert, die die Berichtsserver-Datenbank hostet. Schreibgeschützt.|  
|[DatabaseLogonTimeout](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaselogontimeout.md)|Gibt die Anzahl von Sekunden an, die gewartet wird, ehe ein Anmeldeversuch bei der Berichtsserver-Datenbank fehlschlägt. Schreibgeschützt.|  
|[DatabaseLogonType](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaselogontype.md)|Gibt an, ob der Berichtsserver für den Zugriff auf die Berichtsserver-Datenbank ein Windows-Dienstkonto, ein Windows-Benutzerkonto oder eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldung verwendet. Schreibgeschützt.|  
|[DatabaseName](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databasename.md)|Gibt den Namen der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz an, die die Berichtsserver-Datenbank hostet|  
|[DatabaseQueryTimeout](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databasequerytimeout.md)|Gibt die Anzahl von Sekunden an, die verstreichen müssen, ehe der Befehl fehlschlägt oder wegen eines Timeouts abgebrochen wird. Der Berichtsserver nimmt die zeitliche Steuerung des Prozesses anhand des SQL Server-Katalogs und nicht anhand einer Datenquelle für den Bericht vor.|  
|[DatabaseServerName](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaseservername.md)|Gibt den Namen des Servers an, auf dem die Berichtsserver-Datenbank installiert ist|  
|[InstallationID-Eigenschaft](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-installationid.md)|Gibt einen eindeutigen Bezeichner für eine bestimmte Berichtsserverinstanz zurück|  
|[InstanceName](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-instancename.md)|Gibt den Namen einer Berichtsserverinstanz auf einem bestimmten Computer an.|  
|[IsInitialized](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-isinitialized.md)|Gibt an, ob die Berichtsserverinstanz initialisiert wurde.  Schreibgeschützt.|  
|[IsSharePointIntegrated](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-issharepointintegrated.md)|Gibt an, ob der Berichtsserver für den integrierten SharePoint-Modus konfiguriert ist.|  
|[IsWebServiceEnabled](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-iswebserviceenabled.md)|Gibt an, ob der Report Server-Webdienst aktiviert ist. Schreibgeschützt.|  
|[IsWindowsServiceEnabled](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-iswindowsserviceenabled.md)|Gibt an, ob der Report Server-Windows-Dienst aktiviert ist. Schreibgeschützt.|  
|[MachineAccountIdentity-Eigenschaft &#40;WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-machineaccountidentity.md)|Ruft die Computerkontoidentität des Computers ab, auf dem der Berichtsserver installiert ist|  
|[PathName](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-pathname.md)|Gibt den Installationspfad zu einer Berichtsserverinstanz an|  
|[SecureConnectionLevel](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-secureconnectionlevel.md)|Gibt die in der Datei RSReportServer.config angegebene sichere Verbindungsebene zurück.|  
|[SenderEmailAddress](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-senderemailaddress.md)|Ruft die Adresse ab, die verwendet wird, um E-Mails vom Berichtsserver zu senden. Schreibgeschützt.|  
|[SendUsingSMTPServer](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-sendusingsmtpserver.md)|Gibt an, ob die SendUsing-Eigenschaft in der E-Mail-Konfiguration auf TRUE festgelegt wurde|  
|[SMTPServer](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-smtpserver.md)|Ruft die SMTP-Server-Eigenschaft aus der Datei RSReportServer.config ab. Schreibgeschützt.|  
|[UnattendedExecutionAccount](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-unattendedexecutionaccount.md)|Gibt das Benutzerkonto für die Anmeldung an, dessen Identität der Berichtsserver bei der unbeaufsichtigten Ausführung von Berichten annimmt. Schreibgeschützt.|  
|[Version](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-version.md)|Gibt die Version des Berichtsservers zurück|  
|[VirtualDirectoryReportManager-Eigenschaft &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-virtualdirectoryreportmanager.md)|Gibt das virtuelle Verzeichnis für die Berichts-Manager-Anwendung zurück|  
|[VirtualDirectoryReportManager-Eigenschaft &#40;WMI: MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-virtualdirectoryreportserver.md)|Gibt das virtuelle Verzeichnis für die Report Server-Webdienstanwendung zurück|  
|[WindowsServiceIdentityActual](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-windowsserviceidentityactual.md)|Gibt die Identität zurück, unter der der Report Server-Windows-Dienst tatsächlich ausgeführt wird. Schreibgeschützt.|  
|[WindowsServiceIdentityConfigured](../../reporting-services/wmi-provider-library-reference/windowsserviceidentityconfigured-property.md)|Gibt die Identität zurück, unter der der Report Server-Windows-Dienst entsprechend seiner letzten Konfiguration ausgeführt wird. Schreibgeschützt.|  
  
## <a name="see-also"></a>Siehe auch  
 [MSReportServer_ConfigurationSetting-Member](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  

  

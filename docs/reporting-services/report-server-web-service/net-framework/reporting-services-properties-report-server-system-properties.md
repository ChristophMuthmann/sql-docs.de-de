---
title: Berichtsserver-Systemeigenschaften | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: report-server-web-service
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- report servers [Reporting Services], properties
- system-specific properties [Reporting Services]
ms.assetid: cd874117-00e5-4ae6-8629-eb9ba9f40478
caps.latest.revision: "55"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: fda2938b017671334eba3b26111be7317e9245a0
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="reporting-services-properties---report-server-system-properties"></a>Berichtsserver-Eigenschaften: Berichtsserver-Systemeigenschaften
  Die folgenden Namen der Systemeigenschaften sind reserviert. Sie können keine benutzerdefinierten Eigenschaften des gleichen Namens erstellen. Sie können viele dieser Eigenschaften mit den Webdienstmethoden lesen oder ändern.  
  
## <a name="properties"></a>Eigenschaften  
  
|Eigenschaft|Description|  
|--------------|-----------------|  
|SiteName|Der Name der Berichtsserversite, der auf der Benutzeroberfläche angezeigt wird. Der Standardwert ist der **Berichtsserver von Microsoft**. Diese Eigenschaft kann eine leere Zeichenfolge sein. Die maximale Länge beträgt 8,000 Zeichen.|  
|SystemSnapshotLimit|Die maximale Anzahl an Momentaufnahmen, die für einen Bericht gespeichert werden. Gültige Werte sind **-1** bis **2**.**147**.**483**.**647**. Lautet der Wert **-1**, so ist die Anzahl von Momentaufnahmen nicht einschränkt.|  
|SystemReportTimeout|Der Standard-Timeoutwert für die Berichtsverarbeitung in Sekunden für alle im Berichtsserver-Namespace verwalteten Berichte. Dieser Wert kann auf Berichtsebene überschrieben werden. Ist diese Eigenschaft festgelegt, versucht der Berichtsserver, die Verarbeitung eines Berichts zu beenden, sobald der angegebene Zeitraum überschritten wird. Gültige Werte sind **-1** bis **2**.**147**.**483**.**647**. Wenn der Wert **-1**ist, tritt bei Berichten im Namespace während der Verarbeitung kein Timeout auf. Der Standardwert lautet **1800**.|  
|UseSessionCookies|Gibt an, ob der Berichtsserver beim Kommunizieren mit Clientbrowsern Sitzungscookies verwenden soll. Der Standardwert ist **true**.|  
|SessionTimeout|Der Zeitraum in Sekunden, in dem die Sitzung aktiv bleibt. Der Standardwert lautet **600**.|  
|EnableMyReports|Gibt an, ob die Funktion <legacyBold>Meine Berichte</legacyBold> aktiviert ist. Der Wert **true** gibt an, dass die Funktion aktiviert ist.|  
|MyReportsRole|Der Name der Rolle, die beim Erstellen von Sicherheitsrichtlinien für die Ordner <legacyBold>Meine Berichte</legacyBold> des Benutzers verwendet wird. Der Standardwert lautet **My Reports Role**.|  
|EnableExecutionLogging|Gibt an, ob die Protokollierung der Berichtsausführung aktiviert ist. Der Standardwert ist **true**.|  
|ExecutionLogDaysKept|Die Anzahl von Tagen, in denen die Berichtsausführungsdaten im Ausführungsprotokoll verbleiben. Gültige Werte für diese Eigenschaft sind **0** und **2**,**147**,**483**,**647**. Wenn der Wert **0** ist, werden Einträge nicht aus der Ausführungsprotokolltabelle gelöscht. Der Standardwert lautet **60**.|  
|SnapshotCompression|Definiert, wie Momentaufnahmen komprimiert werden. Der Standardwert lautet **SQL**. Die folgenden Werte sind gültig:<br /><br /> **SQL** = Momentaufnahmen werden komprimiert, wenn sie in der Berichtsserver-Datenbank gespeichert werden. Dies ist das aktuelle Verhalten.<br /><br /> **Keine** = Momentaufnahmen werden nicht komprimiert.<br /><br /> **Alle** = Momentaufnahmen werden bei allen Speicheroptionen komprimiert, was auch die Berichtsserver-Datenbank oder das Dateisystem einschließt.|  
|EnableClientPrinting|Bestimmt, ob das RSClientPrint-ActiveX-Steuerelement zum Herunterladen vom Berichtsserver verfügbar ist. Gültige Werte sind **true** und **false**. Der Standardwert ist **true**. Weitere Informationen zu zusätzlichen Einstellungen, die für dieses Steuerelement erforderlich sind, finden Sie unter [Aktivieren und Deaktivieren des clientseitigen Drucks für Reporting Services](../../../reporting-services/report-server/enable-and-disable-client-side-printing-for-reporting-services.md).|  
|EnableIntegratedSecurity|Bestimmt, ob die integrierte Sicherheit für Berichtsdatenquellen-Verbindungen unterstützt wird. Der Standardwert ist **True**. Die folgenden Werte sind gültig:<br /><br /> **TRUE** = Integrierte Sicherheit ist aktiviert.<br /><br /> **FALSE** = Integrierte Sicherheit ist nicht aktiviert. Berichtsdatenquellen, die für die Verwendung der integrierten Sicherheit konfiguriert sind, werden nicht ausgeführt.|  
|EnableRemoteErrors|Nimmt externe Fehlerinformationen (beispielsweise Fehlerinformationen zu Berichtsdatenquellen) in die Fehlermeldungen auf, die für Benutzer zurückgegeben werden, die Berichte von Remotecomputern anfordern. Gültige Werte sind **true** und **false**. Der Standardwert ist **false**. Weitere Informationen finden Sie unter [Aktivieren von Remotefehlern &#40;Reporting Services&#41;](../../../reporting-services/report-server/enable-remote-errors-reporting-services.md).|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 <xref:ReportService2010.ReportingService2010.GetSystemProperties%2A>   
 <xref:ReportService2010.ReportingService2010.SetSystemProperties%2A>   
 [Erstellen von Anwendungen mit dem Webdienst und .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Berichtsserver-Webdienst](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [Technische Referenz (SSRS)](../../../reporting-services/technical-reference-ssrs.md)  
  
  

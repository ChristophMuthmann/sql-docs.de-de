---
title: Reporting Services-Protokolldateien und Quellen | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- troubleshooting [Reporting Services], log files
- logs [Reporting Services]
- logs [Reporting Services], about log files
- report servers [Reporting Services], log files
- report server log files
- files [Reporting Services], logs
ms.assetid: 80ef0acc-cbef-49d0-87e7-844e3ce19604
caps.latest.revision: "49"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 5242a9107b7a69b017fbb0ceb78d1d33ff5ec24d
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="reporting-services-log-files-and-sources"></a>Reporting Services-Protokolldateien und Quellen
  Ein Berichtsserver und eine Berichtsserverumgebung verwenden eine Vielzahl von Protokollzielen, um Informationen zu Servervorgängen und zum Status aufzuzeichnen. Es gibt zwei grundlegende Kategorien von Protokollierung: Protokollierung der Ausführung und Ablaufprotokollierung. Die Protokollierung der Ausführung schließt Informationen zu Berichtsausführungsstatistiken, Überwachung, Leistungsdiagnose und Optimierung ein. Die Ablaufprotokollierung enthält Informationen zu Fehlermeldungen und allgemeiner Diagnose.  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] im SharePoint-Modus | [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] im einheitlichen Modus  
  
 Die folgende Tabelle enthält Links zu zusätzlichen Informationen zu den Protokollen, einschließlich ihrer Speicherorte und der Vorgehensweise zum Anzeigen ihrer Inhalte.  
  
|Log|Description|  
|---------|-----------------|  
|[Berichtsserver-Ausführungsprotokoll und die ExecutionLog3-Ansicht](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md)|Das Ausführungsprotokoll ist in der Berichtsserverdatenbank gespeicherte SQL Server-Sicht.<br /><br /> Das Berichtsserver-Ausführungsprotokoll enthält Daten zu bestimmten Berichten, beispielsweise, wann ein Bericht ausgeführt wurde, wer ihn ausgeführt hat, wohin er übermittelt wurde und welches Renderingformat verwendet wurde.|  
|SharePoint-Ablaufverfolgungsprotokoll|Für Berichtsserver, die in SharePoint ausgeführt werden, enthält das SharePoint-Ablaufverfolgungsprotokoll [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Informationen. Sie können auch für [!INCLUDE[ssRS](../../includes/ssrs-md.md)] spezifische Informationen für den vereinheitlichten SharePoint-Protokollierungsdienst (SharePoint Unified Logging Service) konfigurieren. Weitere Informationen finden Sie unter [Aktivieren von Reporting Services-Ereignissen für das SharePoint-Ablaufverfolgungsprotokoll &#40;ULS&#41;](../../reporting-services/report-server/turn-on-reporting-services-events-for-the-sharepoint-trace-log-uls.md)|  
|[Report Server Service Trace Log (Berichtsserverdienst-Ablaufverfolgungsprotokoll)](../../reporting-services/report-server/report-server-service-trace-log.md)|Das Ablaufverfolgungsprotokoll des Diensts enthält sehr detaillierte Informationen, die beim Debuggen einer Anwendung oder beim Analysieren eines Problems oder Ereignisses hilfreich sind. Die Ablaufverfolgungs-Protokolldateien heißen „ReportServerService_\<Zeitstempel>.log“ und befinden sich im folgenden Ordner:<br /><br /> `C:\Program Files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\LogFiles`|  
|[Report Server HTTP Log (Berichtsserver-HTTP-Protokoll)](../../reporting-services/report-server/report-server-http-log.md)|Die HTTP-Protokolldatei zeichnet alle HTTP-Anforderungen und -Antworten auf, die vom Report Server-Webdienst und Berichts-Manager verarbeitet werden.|  
|[Windows-Anwendungsprotokoll](../../reporting-services/report-server/windows-application-log.md)|Das Microsoft Windows-Anwendungsprotokoll enthält Informationen zu Berichtsserverereignissen.|  
|Windows-Leistungsprotokolle|Windows-Leistungsprotokolle enthalten Daten zur Berichtsserverleistung. Sie können Leistungsprotokolle erstellen und anschließend Leistungsindikatoren auswählen, die bestimmen, welche Daten gesammelt werden. Weitere Informationen finden Sie unter [Monitoring Report Server Performance](../../reporting-services/report-server/monitoring-report-server-performance.md).|  
|SQL Server-Setupprotokolldateien|Auch während der Installation werden Protokolldateien erstellt. Falls die Installation fehlschlägt oder mit Warn- oder anderen Meldungen erfolgreich beendet wird, können Sie zur Problembehandlung die Protokolldateien untersuchen. Weitere Informationen finden Sie unter [View and Read SQL Server Setup Log Files](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).|  
|IIS-Protokolle|Von Microsoft-Internetinformationsdiensten (IIS) erstellte Protokolldateien. Weitere Informationen finden Sie unter [Aktivieren der Protokollierung in Internetinformationsdienste (IIS)](http://support.microsoft.com/kb/313437) (http://support.microsoft.com/kb/313437).|  
  
## <a name="see-also"></a>Siehe auch  
 [Reporting Services-Berichtsserver &#40;einheitlicher Modus&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [Fehler- und Ereignisreferenz &#40;Reporting Services&#41;](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)  
  
  

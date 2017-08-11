---
title: Problembehandlung bei Reporting Services-Berichtsprobleme | Microsoft Docs
ms.custom: 
ms.date: 02/27/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a705d103-85b1-49b5-b27f-332b1040d029
caps.latest.revision: 9
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 9a8c5f76c0d2cd35f0ef52b77b79b13cc8b5efbe
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="troubleshoot--reporting-services-report-issues"></a>Problembehandlung bei Reporting Services-Problemen mit Berichten
In diesem Thema erhalten Sie Informationen zum Behandeln von Problemen mit dem [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion.md)] -Berichtsentwurf, dem Anzeigen der Vorschau eines Berichts, dem Veröffentlichen eines Berichts auf einem Berichtsserver im einheitlichen Modus oder im SharePoint-Modus, dem Anzeigen eines Berichts auf dem Berichtsserver oder dem Exportierten eines Berichts in ein anderes Dateiformat.  
## <a name="monitor-report-servers"></a>Überwachen von Berichtsservern  
Sie können mithilfe von System- und Datenbanktools die Berichtsserveraktivitäten überwachen. Außerdem können Sie die Ablaufverfolgungsprotokolldateien des Berichtsservers anzeigen oder das Ausführungsprotokoll des Berichtsservers nach detaillierten Informationen zu bestimmten Berichten abfragen. Wenn Sie mit Systemmonitor arbeiten, können Sie Leistungsindikatoren für den Berichtsserver-Webdienst und den Windows-Dienst hinzufügen, um Engpässe bei der bedarfsgesteuerten oder geplanten Verarbeitung erkennen zu können.  
Weitere Informationen finden Sie unter [Überwachen der Leistung des Berichtsservers](../../reporting-services/report-server/monitoring-report-server-performance.md).  
  
  
## <a name="view-the-report-server-logs"></a>Anzeigen der Berichtsserverprotokolle  
[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion.md)] erfasst eine Vielzahl von internen und externen Ereignissen in Protokolldateien, die Daten zu bestimmten Berichten, Debuginformationen, HTTP-Anforderungen und -Antworten und Berichtsserverereignisse aufzeichnen. Sie können außerdem Leistungsprotokolle erstellen und Leistungsindikatoren auswählen, mit denen angegeben wird, welche Daten erfasst werden sollen. Das Standardverzeichnis für die Protokolldateien einer Standardinstallation ist `<drive>\Program Files\Microsoft SQL Server\MSRS130.MSSQLSERVER\Reporting Services\LogFiles`.   
  
Weitere Informationen finden Sie unter [Reporting Services-Protokolldateien und Quellen](../../reporting-services/report-server/reporting-services-log-files-and-sources.md).  
  
Wenn Sie genau ermitteln möchten, ob Berichtswartezeiten auf den Datenabruf, die Berichtsverarbeitung oder das Berichtsrendering zurückzuführen sind, verwenden Sie das Ausführungsprotokoll. Weitere Informationen finden Sie unter [Berichtsserverausführungsprotokoll und die ExecutionLog3-Ansicht].   
  
## <a name="view-the-call-stack-for-report-processing-error-messages-on-the-report-server"></a>Anzeigen der Aufrufliste für Fehlermeldungen zur Berichtsverarbeitung auf dem Berichtsserver  
Wenn Sie einen veröffentlichten Bericht im Berichts-Manager anzeigen, wird möglicherweise eine Fehlermeldung für einen allgemeinen Verarbeitungs- oder Renderingfehler angezeigt. Wenn Sie weitere Informationen benötigen, können Sie die Aufrufliste anzeigen.   
  
Melden Sie sich zum Anzeigen der Aufrufliste als lokaler Administrator am Berichtsserver an, klicken Sie mit der rechten Maustaste auf die Seite im Berichts-Manager, und klicken Sie dann auf **Quelltext anzeigen**. Die Aufrufliste enthält den ausführlichen Kontext für die Fehlermeldung.  
  
## <a name="use-includessmanstudiofullincludesssmanstudiofullmd-to-verify-queries-and-credentials"></a>Verwenden von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull.md)] zum Überprüfen von Abfragen und Anmeldeinformationen  
Sie können mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull.md)] komplexe Abfragen überprüfen, bevor Sie sie in den Bericht einschließen.   
  
Weitere Informationen finden Sie in den Artikeln zum [Database Engine (Datenbankmodul)-Abfrage-Editor](../../relational-databases/scripting/database-engine-query-editor-sql-server-management-studio.md) und zum [Verwalten von Objekten mithilfe des Objekt-Explorers](~/ssms/object/manage-objects-by-using-object-explorer.md).  
  
## <a name="analyze-problem-reports-with-report-data-cached-on-the-client"></a>Analysieren von Problemberichten mit auf dem Client zwischengespeicherten Berichtsdaten  
Wenn ein Berichtsautor einen Bericht in Business Intelligence Development Studio erstellt, speichert der Berichterstellungsclient die Daten als RDL.DATA-Datei zwischen, die beim Anzeigen der Vorschau eines Berichts verwendet wird. Bei jeder Änderung der Abfrage wird der Cache aktualisiert. Zum Debuggen von Berichtsproblemen ist es in einigen Fällen sinnvoll, das Aktualisieren der Berichtsdaten zu verhindern, damit die Daten beim Debuggen nicht geändert werden.   
  
Um zu steuern, dass [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull.md)] nur zwischengespeicherte Daten verwenden kann, fügen Sie in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio.md)]den folgenden Abschnitt in devenv.exe.config hinzu. Der Speicherort des Standardverzeichnisses ist: `<drive>:Program Files\Microsoft Visual Studio 10.0\Common7\IDE`.   
  
```  
<system.diagnostics>  
      <switches>  
         <add name="Microsoft.ReportDesigner.ReportPreviewStore.ForceCache" value="1" />  
      </switches>  
   </system.diagnostics>  
```  
Solange der Wert auf 1 festgelegt ist, werden nur zwischengespeicherte Berichtsdaten verwendet. Achten Sie darauf, diesen Abschnitt zu entfernen, wenn das Debuggen des Berichts abgeschlossen ist.  
  
## <a name="see-also"></a>Siehe auch  
[Fehler und Ereignisse (Reporting Services)](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)  
  
  

[!INCLUDE[feedback_stackoverflow_msdn_connect](../../includes/feedback-stackoverflow-msdn-connect.md)]




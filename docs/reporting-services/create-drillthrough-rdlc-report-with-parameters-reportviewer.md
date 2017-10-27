---
title: Erstellen des Drillthroughberichts (RDLC) mit Parametern - ReportViewer | Microsoft Docs
ms.custom: 
ms.date: 05/18/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: 628c8775-c62d-45ac-b349-23db86fa4e6c
caps.latest.revision: 8
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 8ce79884745b9e2fc9fbddfd7d312e982b2dd61c
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="create-drillthrough-rdlc-report-with-parameters---reportviewer"></a>Erstellen des Drillthroughberichts (RDLC) mit Parametern - ReportViewer
Ein [Drillthroughbericht](http://technet.microsoft.com/library/ff519554.aspx) ist ein Bericht, der geöffnet werden kann, indem der Benutzer auf einen Link in einem anderen Bericht klickt. Drillthroughberichte enthalten in der Regel Details zu einem Element im ursprünglichen Zusammenfassungsbericht. Dieses Tutorial führt Sie in den folgenden Lektionen durch die Schritte zum Erstellen eines Drillthroughberichts mit Parametern und einer Abfrage. Dabei wird die [Berichterstellung im lokalen Modus](http://msdn.microsoft.com/library/ff487969.aspx)verwendet.  
  
## <a name="requirements"></a>Anforderungen  
Zur Verwendung dieser exemplarischen Vorgehensweise benötigen Sie Zugriff auf die Beispieldatenbank **AdventureWorks2014** . Weitere Informationen zum Abrufen der **AdventureWorks2014** -Beispieldatenbank, finden Sie unter [Microsoft SQL Server Database Product Samples](http://msftdbprodsamples.codeplex.com/).  
  
Bei dieser exemplarischen Vorgehensweise wird vorausgesetzt, dass Sie mit Transaction-SQL-Abfragen und den ADO.NET-Objekten [DataSet](https://msdn.microsoft.com/library/system.data.dataset.aspx) und [DataTable](http://msdn.microsoft.com/library/system.data.datatable.aspx) vertraut sind.  
  
Verwenden Sie Visual Studio 2015 und die ASP.NET-Webanwendung, um eine ASP.NET-Webseite mit einem ReportViewer-Steuerelement zu erstellen. Das Steuerelement wird für die Anzeige eines erstellten Berichts konfiguriert. Mithilfe dieser exemplarischen Vorgehensweise erstellen Sie die Anwendung in Microsoft Visual C#.  
  
## <a name="tasks"></a>Aufgaben  
[Lektion 1: Erstellen einer neuen Website](../reporting-services/lesson-1-create-a-new-web-site.md)  
[Lektion 2: Definieren einer Datenverbindung und einer Datentabelle für den übergeordneten Bericht](../reporting-services/lesson-2-define-a-data-connection-and-data-table-for-parent-report.md)  
[Lektion 3: Entwerfen des übergeordneten Berichts mithilfe des Berichts-Assistenten](../reporting-services/lesson-3-design-the-parent-report-using-the-report-wizard.md)  
[Lektion 4: Definieren einer Datenverbindung und einer Datentabelle für den untergeordneten Bericht](../reporting-services/lesson-4-define-a-data-connection-and-data-table-for-child-report.md)  
[Lektion 5: Entwerfen des untergeordneten Berichts mithilfe des Berichts-Assistenten](../reporting-services/lesson-5-design-the-child-report-using-the-report-wizard.md)  
[Lektion 6: Hinzufügen eines ReportViewer-Steuerelements zur Anwendung](../reporting-services/lesson-6-add-a-reportviewer-control-to-the-application.md)  
[Lektion 7: Hinzufügen einer Drillthroughaktion für den übergeordneten Bericht](../reporting-services/lesson-7-add-drillthrough-action-on-parent-report.md)  
[Lektion 8: Erstellen eines Datenfilters](../reporting-services/lesson-8-create-a-data-filter.md)  
[Lesson 9: Build and Run the Application](../reporting-services/lesson-9-build-and-run-the-application.md)  
  
## <a name="see-also"></a>Siehe auch  
[Reporting Services-Tutorials &#40;SSRS&#41;](../reporting-services/reporting-services-tutorials-ssrs.md)  
[Entwerfen von Berichten mithilfe des Berichts-Designers &#40;SSRS&#41;](../reporting-services/tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md)  
  



---
title: Leistung, Momentaufnahmen, Zwischenspeichern (Reporting Services) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- performance [Reporting Services]
- Reporting Services, performance
ms.assetid: 85afd00f-e8d7-4ef7-9174-2ff84d82f960
caps.latest.revision: 20
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c752ea8a5f05a1dc861b0297b7a1c0eaca5cfc88
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="performance-snapshots-caching-reporting-services"></a>Leistung, Momentaufnahmen, Zwischenspeichern (Reporting Services)
  Die Leistung des Berichtsservers wird von einer Reihe von Faktoren beeinflusst. Dazu zählen Hardware, Anzahl der Benutzer, die gleichzeitig auf Berichte zugreifen, Datenmenge in einem Bericht und Ausgabeformat. Um die Leistungsfaktoren, die spezifisch für Ihre Installation sind, und entsprechende Abhilfemaßnahmen zu ermitteln, müssen Sie sich zunächst mit den Basisdaten beschäftigen und Tests ausführen. Weitere Informationen zu Tools und Richtlinien stehen in den folgenden Publikationen auf MSDN zur Verfügung: [Leistungsoptimierung bei Reporting Services](http://blogs.msdn.com/b/sqlcat/archive/2013/10/30/reporting-services-performance-and-optimization.aspx) und [Verwenden von Visual Studio 2005 zum Ausführen von Ladetests für einen SQL Server 2005 Reporting Services-Berichtsserver](http://go.microsoft.com/fwlink/?LinkID=77519).  
  
 Folgende allgemeine Aspekte sind zu beachten:  
  
-   Die Berichtsverarbeitung und das Berichtsrendering sind speicherintensive Vorgänge. Wählen Sie wenn möglich einen Computer mit viel Arbeitsspeicher aus.  
  
-   Das Hosten von Berichtsserver und Berichtsserver-Datenbank auf verschiedenen Computern liefert in der Regel bessere Ergebnisse als das gemeinsame Hosten auf einem einzelnen leistungsstarken Computer.  
  
-   Wenn alle Berichte langsam verarbeitet werden, sollten Sie eine Bereitstellung für dezentrales Skalieren in Erwägung ziehen. Dabei unterstützen mehrere Berichtsserverinstanzen eine einzelne Berichtsserver-Datenbank. Verwenden Sie für beste Ergebnisse eine Lastenausgleichssoftware, die Anforderungen gleichmäßig über die Bereitstellung verteilt.  
  
-   Wird ein einzelner Bericht langsam verarbeitet, optimieren Sie die Datasetabfragen des Berichts, wenn der Bericht bei Bedarf ausgeführt werden muss. Weitere Möglichkeiten sind das Verwenden freigegebener Datasets, die Sie zwischenspeichern können, das Zwischenspeichern des Berichts oder das Ausführen des Berichts als Momentaufnahme.  
  
-   Wenn alle Berichte in einem spezifischen Format langsam verarbeitet werden (z. B. Rendern im PDF-Format), sollten Sie eine Dateifreigabeübermittlung, das Hinzufügen von Arbeitsspeicher oder die Auswahl eines anderen Formats erwägen.  
  
-   Die Dauer der Berichtsverarbeitung und andere Nutzungsdaten können Sie im Ausführungsprotokoll des Berichtsservers ermitteln. Weitere Informationen finden Sie unter [Berichtsserver-Ausführungsprotokoll und die ExecutionLog3-Sicht](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md).  
  
-   Weitere Informationen zum Minimieren von Leistungsproblemen durch das Optimieren der Speicherverwaltungs-Konfigurationseinstellungen finden Sie unter [Konfigurieren von verfügbarem Speicher für Berichtsserveranwendungen](../../reporting-services/report-server/configure-available-memory-for-report-server-applications.md).  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [Überwachen der Leistung des Berichtsservers](../../reporting-services/report-server/monitoring-report-server-performance.md)  
 Beschreibt die Leistungsobjekte, die Sie verwenden können, um die Verarbeitungslast auf dem Server zu verfolgen.  
  
 [Festlegen von Berichtsverarbeitungseigenschaften](../../reporting-services/report-server/set-report-processing-properties.md)  
 Beschreibt Möglichkeiten, einen Bericht so zu konfigurieren, dass er bedarfsgesteuert aus dem Cache oder nach Zeitplan als Berichtsmomentaufnahme ausgeführt wird.  
  
 [Konfigurieren von verfügbarem Speicher für Berichtsserveranwendungen](../../reporting-services/report-server/configure-available-memory-for-report-server-applications.md)  
 Beschreibt, wie Sie das Standardverhalten bei der Arbeitsspeicherverwaltung überschreiben können.  
  
 [Zwischenspeichern von Berichten &#40;SSRS&#41;](../../reporting-services/report-server/caching-reports-ssrs.md)  
 Beschreibt das Verhalten beim Zwischenspeichern auf einem Berichtsserver.  
  
 [Zwischenspeichern von freigegebenen Datasets &#40;SSRS&#41;](../../reporting-services/report-server/cache-shared-datasets-ssrs.md)  
 Beschreibt das Verhalten beim Zwischenspeichern freigegebener Datasets auf einem Berichtsserver.  
  
 [Verarbeiten von großen Berichten](../../reporting-services/report-server/process-large-reports.md)  
 Stellt Empfehlungen dazu bereit, wie ein großer Bericht konfiguriert und verteilt wird.  
  
 [Festlegen von Timeoutwerten für die Verarbeitung von Berichten und freigegebenen Datasets &#40;SSRS&#41;](../../reporting-services/report-server/setting-time-out-values-for-report-and-shared-dataset-processing-ssrs.md)  
 Erklärt, wie Timeouts für die Abfrage- und Berichtsverarbeitung festgelegt werden.  
  
## <a name="see-also"></a>Siehe auch  
 [Verwalten eines ausgeführten Prozesses](../../reporting-services/subscriptions/manage-a-running-process.md)   
 [Verifying a Report Run (Überprüfen der Berichtsausführung)](../../reporting-services/report-server/verifying-a-report-run.md)  
  
  

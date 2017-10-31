---
title: "Hinzufügen von Daten zu einem Tablix-Datenbereich (Berichts-Generator und SSRS) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8f1d0a76-afed-480f-98fb-89e2d4eb09b1
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b6f41b4d1b42db5ca020841f9363df3f4cf3eb99
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="adding-data-to-a-tablix-data-region-report-builder-and-ssrs"></a>Hinzufügen von Daten zu einem Tablix-Datenbereich (Berichts-Generator und SSRS)
Wenn Sie in einem paginierten [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Bericht Daten aus einem Berichtsdataset in einer Tabelle oder einer Matrix anzeigen möchten, geben Sie in jeder Datenzelle den Namen eines anzuzeigenden Datasetfelds an. Sie können Detaildaten oder gruppierte Daten anzeigen. Wenn Sie einer Tabelle oder Matrix Gruppen hinzufügen, werden automatisch Zeilen und Spalten für Gruppenwerte und Gruppendaten hinzugefügt. Anschließend können Sie Teilergebnisse und Gesamtergebnisse für die Daten hinzufügen.  
  
 Alle Daten in einem Datenbereich gehören zu mindestens einer Gruppe. Detaildaten sind ein Element der Detailgruppe. Weitere Informationen zu Detail- und Gruppendaten finden Sie unter [Grundlegendes zu Gruppen (Berichts-Generator und SSRS)](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="adding-detail-data"></a>Hinzufügen von Detaildaten  
 Detaildaten sind sämtliche Daten aus einem Berichtsdataset nach dem Anwenden von Filtern auf das Dataset, den Datenbereich und die Detailgruppe. Alle in einem Tablix-Datenbereich angezeigten Detaildaten müssen aus demselben Berichtsdataset stammen.  
  
 Wenn Sie einem Tablix-Datenbereich Detaildaten aus einem Berichtsdataset hinzufügen möchten, ziehen Sie ein Datasetfeld aus dem Berichtsdatenbereich in die einzelnen Zellen in der Detailzeile. Für vorhandene Zellen in einem Tablix-Datenbereich können Sie einen Datasetfeld-Ausdruck mithilfe der Feldauswahl der jeweiligen Zelle hinzufügen oder bearbeiten, oder indem Sie ein Feld aus dem Berichtsdatenbereich in die Zelle ziehen. Wenn Sie weitere Spalten erstellen möchten, können Sie das Feld aus dem Berichtsdatenbereich ziehen und in einen vorhandenen Tablix-Datenbereich einfügen.  
  
 Standardmäßig werden zur Laufzeit in einer Zelle in der Detailzeile Detaildaten angezeigt, während in einer Zelle in der Gruppenzeile ein Aggregatwert angezeigt wird. Weitere Informationen zu Tablix-Zeilen und -Spalten finden Sie unter [Zellen, Zeilen und Spalten des Tablix-Datenbereichs (Berichts-Generator und SSRS)](../../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md).  
  
 Eine Detailzeile wird von einer Tabellenvorlage und einer Listenvorlage bereitgestellt. Eine Matrixvorlage weist keine Detailzeile auf. Wenn im Tablix-Datenbereich keine Detailzeile enthalten ist, können Sie eine Detailzeile hinzufügen, indem Sie eine Detailgruppe definieren. Weitere Informationen finden Sie unter [Hinzufügen einer Detailgruppe (Berichts-Generator und SSRS)](../../reporting-services/report-design/add-a-details-group-report-builder-and-ssrs.md).  
  
## <a name="adding-grouped-data"></a>Hinzufügen von gruppierten Daten  
 Gruppierte Daten sind alle Detaildaten, die von einem Gruppierungsausdruck angegeben werden, nachdem Filter auf das Dataset, den Datenbereich und die Gruppe angewendet wurden. Wenn Sie Detaildaten in Gruppen organisieren möchten, ziehen Sie Felder aus dem Berichtsdatenbereich in den Bereich Gruppierung. Beim Hinzufügen einer Gruppe werden in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] dem Tablix-Datenbereich, in dem gruppierte Daten angezeigt werden sollen, automatisch verknüpfte Zeilen oder Spalten hinzugefügt. Zellen in diesen Zeilen oder Spalten werden gruppierten Daten zugeordnet. Weitere Informationen finden Sie unter [Hinzufügen oder Löschen einer Gruppe in einem Datenbereich &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md).  
  
 Wenn Sie ein Datasetfeld, das numerische Daten darstellt, einer Zelle in einer Gruppenzeile oder -spalte hinzufügen, ist der Wert der Zelle standardmäßig die Summe der gruppierten Daten, deren Bereich auf die innersten Zeilen- und Spaltengruppenmitgliedschaften für die Zelle festgelegt ist. Sie können die Standardaggregatfunktion Sum in eine beliebige andere Aggregatfunktion ändern, z.B. in Avg oder Count. Sie können auch den Standardbereich für eine Aggregatberechnung ändern, beispielsweise um den Prozentsatz zu berechnen, den ein Wert zu einer Zeilengruppe beiträgt. Weitere Informationen finden Sie unter [Ausdrucksbereich für Gesamtwerte, Aggregate und integrierte Sammlungen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)-Ausdruck dar.  
  
 Standardmäßig stammen alle gruppierten Daten aus demselben Berichtsdataset. In einem Tablix-Datenbereich können Sie Aggregatwerte aus einem anderen Dataset einbinden, indem Sie den Datasetnamen als Bereich angeben. Sie können mehrere Aggregatwerte aus mehreren Datasets in einem einzelnen Tablix-Datenbereich angeben. Weitere Informationen finden Sie unter [Aggregatfunktionsreferenz &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md).  
  
## <a name="adding-subtotals-and-totals"></a>Hinzufügen von Teilergebnissen und Gesamtergebnissen  
 Wenn Sie Teilergebnisse für eine Gruppe und Gesamtergebnisse für den Datenbereich hinzufügen möchten, wählen Sie die Funktion Gesamtergebnis hinzufügen im Kontextmenü einer Zelle oder im Bereich Gruppierung aus. Die Zeilen und die Spalten, in denen die Gesamtergebnisse angezeigt werden sollen, werden automatisch hinzugefügt. Für Teilergebnis- und Gesamtergebnisausdrücke wird standardmäßig die [Sum](../../reporting-services/report-design/report-builder-functions-sum-function.md) -Aggregatfunktion verwendet. Nach dem Hinzufügen des Ausdrucks können Sie die Standardfunktion ändern. Weitere Informationen finden Sie unter [Hinzufügen eines Gesamtergebnisses zu einer Gruppe oder einem Tablix-Datenbereich (Berichts-Generator und SSRS)](../../reporting-services/report-design/add-a-total-to-a-group-or-tablix-data-region-report-builder-and-ssrs.md) und [Ausdrucksbereich für Gesamtwerte, Aggregate und integrierte Auflistungen](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
## <a name="adding-labels"></a>Hinzufügen von Bezeichnungen  
 Wenn Sie Bezeichnungen für eine Gruppe oder für den Datenbereich hinzufügen möchten, fügen Sie eine Zeile oder Spalte außerhalb der Gruppe hinzu, der eine Bezeichnung zugewiesen werden soll. Bezeichnungszeilen und -spalten ähneln Zeilen und Spalten, die für die Anzeige von Ergebnissen hinzugefügt werden. Weitere Informationen finden Sie unter [Einfügen oder Löschen einer Zeile (Berichts-Generator und SSRS)](../../reporting-services/report-design/insert-or-delete-a-row-report-builder-and-ssrs.md) oder [Einfügen oder Löschen einer Spalte (Berichts-Generator und SSRS)](../../reporting-services/report-design/insert-or-delete-a-column-report-builder-and-ssrs.md).  
  
## <a name="adding-an-existing-tablix-data-region-from-another-report"></a>Hinzufügen eines vorhandenen Tablix-Datenbereichs aus einem anderen Bericht  
 Sie können einen Datenbereich aus einem anderen Bericht kopieren und diesen in einen neuen oder einen vorhandenen Bericht einfügen. Nach dem Einfügen des Datenbereichs müssen Sie sicherstellen, dass das vom Datenbereich verwendete Dataset definiert ist und dass die Datasetfelder dieselben Namen und Datentypen wie im ursprünglichen Bericht aufweisen. Sie können Datasets nicht von einem Bericht zu einem anderen kopieren, Wenn die Berichte jedoch freigegebene Datenquellen verwenden, können Sie das Dataset schnell im anderen Bericht duplizieren. Außerdem können Sie den Abfragetext für die Abfragen importieren, die die Daten für das Dataset abrufen. So können Abfragen in Berichten problemlos dupliziert werden. Weitere Informationen finden Sie unter [Erstellen von Berichten zu eingebetteten und freigegebenen Datasets &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Ausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [Berichtsparameter &#40;Berichts-Generator und Berichts-Designer&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [Interaktive Sortierung, Dokumentstrukturen und Links &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)   
 [Hinzufügen von Datasetfiltern, Datenbereichsfiltern und Gruppenfiltern &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [Hinzufügen, Bearbeiten und Aktualisieren von Feldern im Berichtsdatenbereich (Berichts-Generator und SSRS)](../../reporting-services/report-data/add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md)   
 [Hinzufügen eines Ausdrucks &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-an-expression-report-builder-and-ssrs.md)  
  
  

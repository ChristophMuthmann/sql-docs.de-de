---
title: "Verknüpfen mehrerer Datenbereiche mit dem gleichen Dataset (Berichts-Generator und SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 90c94a91-8fb2-42cb-b998-563691f30d2d
caps.latest.revision: 10
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 32d055510fd5b04676f2c8fc715e6b7ea132eda9
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---

# <a name="linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs"></a>Verknüpfen mehrerer Datenbereiche mit einem Dataset (Berichts-Generator und SSRS)

Sie können einem paginierten [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Bericht mehrere Datenbereiche hinzufügen, um verschiedene Datensichten für ein Berichtsdataset bereitzustellen. Beispielsweise können Sie Daten in einer Tabelle anzeigen und visuell in einem Diagramm veranschaulichen. Voraussetzung hierfür ist die Verwendung identischer Ausdrücke und Bereiche für die entsprechenden Filterausdrücke, Sortierungsausdrücke und Gruppenausdrücke.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 Die Verwendung eines Diagramms und einer Tabelle oder Matrix zum Anzeigen gleicher Daten hilft, die Ähnlichkeiten zwischen einer Tabelle und Formdiagrammen sowie einer Matrix und Bereichs-, Balken- und Säulendiagrammen zu verstehen. Tabellen mit einer einzelnen Zeilengruppe können einfach als Kreisdiagramm angezeigt werden. Beim Hinzufügen mehrerer Zeilengruppen können Sie verschiedene Diagramme zur optimalen Darstellung der geschachtelten Gruppen auswählen. Durch das Hinzufügen geschachtelter Zeilengruppen zu einem Kreisdiagramm wird die Anzahl der Slices im Kreis erhöht. Dabei ist zu beachten, dass die Gesamtanzahl der Gruppeninstanzen für die übergeordnete und die untergeordnete Gruppe zu groß sein kann, um in einem Kreisdiagramm angezeigt zu werden. Bei mehreren Gruppenwerten, die als kleine Slices in einem Kreisdiagramm angezeigt werden, können Sie mithilfe einer Eigenschaft festlegen, dass alle Werte unter einem bestimmten Schwellenwert als eine Kreisslice angezeigt werden. Weitere Informationen finden Sie unter [Sammeln von kleinen Slices in einem Kreisdiagramm](../../reporting-services/report-design/collect-small-slices-on-a-pie-chart-report-builder-and-ssrs.md).  
  
 Eine Tabelle mit mehreren Zeilengruppen kann als Säulendiagramm mit mehreren Kategoriegruppen angezeigt werden. Weitere Informationen finden Sie unter [anzeigen derselben Daten in einer Matrix und einem Diagramm](../../reporting-services/report-design/display-the-same-data-on-a-matrix-and-a-chart-report-builder.md). Ein Beispiel für eine Tabelle und ein Diagramm, die unterschiedliche Sichten des gleichen Berichtsdatasets darstellen, finden Sie im Product Line Sales-Bericht in den AdventureWorks-Beispielberichten. Die Tabelle und das Diagramm sind mit dem gleichen Dataset im Bericht verknüpft. Wenn Sie auf die Schaltfläche für die interaktive Sortierung für den Mitarbeiternamen in der Tabelle mit den führenden Mitarbeitern klicken, wird die neue Sortierungsreihenfolge automatisch auch für das entsprechende Diagramm übernommen. Weitere Informationen zum Herunterladen dieses Beispielberichts und anderer finden Sie unter [Beispielberichte für Berichts-Generator und Berichts-Designer](http://go.microsoft.com/fwlink/?LinkId=198283).  
  
 Eine Matrix mit mehreren Zeilen- und Spaltengruppen kann am besten mit einem Bereichs-, Balken- oder Säulendiagramm dargestellt werden, das über Kategorie- und Seriengruppen verfügt. Verwenden Sie einheitliche Gruppenausdrücke für Spaltengruppen in der Matrix und Kategoriegruppen im Diagramm, und verwenden Sie einheitliche Gruppenausdrücke für Zeilengruppen in der Matrix und Seriengruppen im Diagramm. Bedenken Sie, dass die Anzahl der Gruppeninstanzen Auswirkungen auf die Lesbarkeit des Diagramms hat. Sie können Gruppen auf der Basis von Bereichswerten definieren, um die Anzahl der Gruppeninstanzen in einem Bericht zu verringern. Weitere Informationen finden Sie unter [Beispiele für Gruppierungsausdrücke](../../reporting-services/report-design/group-expression-examples-report-builder-and-ssrs.md).  
  
## <a name="next-steps"></a>Nächste Schritte

[Diagramme](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
[Tabellen, Matrizen und Listen](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
[Geschachtelte Datenbereiche](../../reporting-services/report-design/nested-data-regions-report-builder-and-ssrs.md)  

Weiteren Fragen wenden? [Versuchen Sie das Reporting Services-Forum stellen](http://go.microsoft.com/fwlink/?LinkId=620231)


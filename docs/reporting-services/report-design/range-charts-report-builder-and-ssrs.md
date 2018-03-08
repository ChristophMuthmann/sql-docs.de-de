---
title: Bereichsdiagramme (Berichts-Generator und SSRS) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 48e351d3-ac5b-4eda-a4bd-32a0de206a30
caps.latest.revision: "5"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: a39861e7284e7fcf17cc57247adcd8844461eaa5
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="range-charts-report-builder-and-ssrs"></a>Bereichsdiagramme (Berichts-Generator und SSRS)
  Ein Bereichsdiagramm zeigt eine Menge von Datenpunkten an, die jeweils durch mehrere Werte für dieselbe Kategorie definiert sind. Die Werte werden durch die Höhe der Markierung, gemessen an der Wertachse, dargestellt. Kategoriebezeichnungen werden an der Kategorieachse angezeigt. Das einfache Bereichsdiagramm füllt den Bereich zwischen dem oberen und dem unteren Wert für jeden Datenpunkt aus.  
  
 Die folgende Illustration zeigt ein einfaches Bereichsdiagramm mit drei Reihen.  
  
 ![Bereichsdiagramm](../../reporting-services/report-design/media/rs-rangechart.gif "Range chart")  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="variations"></a>Variationen  
  
-   **Glatter Bereich**. Ein glattes Bereichsdiagramm zeigt gekrümmte statt gerade Linien an.  
  
-   **Spaltenbereich**. Ein Spaltenbereichsdiagramm verwendet Spalten statt Flächen, um die Bereiche anzuzeigen.  
  
-   **Balkenbereich**. Ein Balkenbereichsdiagramm verwendet Balken statt Flächen, um die Bereiche anzuzeigen.  
  
## <a name="data-considerations-for-range-charts"></a>Überlegungen zu Daten für ein Bereichsdiagramm  
  
-   Bereichsdiagrammtypen erfordern zwei Werte pro Datenpunkt. Diese Werte entsprechen einem hohen und einem niedrigen Wert, die den Bereich für jeden Datenpunkt definieren.  
  
-   Bereichsdiagramme sind nur für Analysezwecke nützlich, wenn die oberen Werte stets höher sind als die unteren Werte. Wenn dies nicht der Fall ist, sollten Sie ein Liniendiagramm verwenden. Wenn der obere Wert niedriger ist als der untere Wert, zeigt das Bereichsdiagramm die absolute Differenz zwischen diesen Werten an.  
  
-   Ist nur ein Wert angegeben, wird das Bereichsdiagramm wie ein normales Bereichsdiagramm mit einem Wert pro Datenpunkt angezeigt.  
  
-   Bereichsdiagramme werden häufig zur Darstellung von Daten verwendet, die Mindest- und Höchstwerte für jede Kategoriegruppe im Dataset enthalten.  
  
-   Die Anzeige von Markern auf jedem Datenpunkt wird im Bereichsdiagramm nicht unterstützt.  
  
-   Wie im Bereichsdiagramm überlappen die Reihen in einem einfachen Bereichsdiagramm, wenn die Werte in mehreren Reihen ähnlich sind. In diesem Szenario bietet es sich an, statt eines einfachen Bereichsdiagramms ein Spaltenbereichs- oder Balkenbereichsdiagramm zu verwenden.  
  
-   Gantt-Diagramme können mit einem Bereichsbalkendiagramm erstellt werden.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Diagramme &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [Diagrammtypen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/chart-types-report-builder-and-ssrs.md)   
 [Formatieren eines Diagramms &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)  
  
  

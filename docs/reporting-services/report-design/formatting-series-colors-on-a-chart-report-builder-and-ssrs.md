---
title: Formatieren von Reihenfarben in einem Diagramm (Berichts-Generator und SSRS) | Microsoft-Dokumentation
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
f1_keywords:
- "10245"
- "10252"
- sql13.rtp.rptdesigner.serieslabelproperties.borders.f1
- sql13.rtp.rptdesigner.seriesproperties.borders.f1
ms.assetid: fe541501-cac5-47b1-b95f-c410db789190
caps.latest.revision: "8"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: b506dfd94eaf507c7cb46498b45641a7a08f1ef3
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="formatting-series-colors-on-a-chart-report-builder-and-ssrs"></a>Formatieren von Reihenfarben in einem Diagramm (Berichts-Generator und SSRS)
  Reporting Services stellt mehrere integrierte Paletten für Diagramme bereit. Außerdem können Sie eine benutzerdefinierte Palette definieren. Diagramme verwenden standardmäßig die integrierte **Pacific** -Farbpalette, um die einzelnen Reihen auszufüllen. Diese Farben werden auch in der Legende angezeigt. Beim Hinzufügen mehrerer Reihen zum Diagramm erfolgt das Zuweisen von Farben zu einer Reihe durch das Diagramm anhand der Reihenfolge, in der die Farben in der Palette definiert wurden.  
  
 Wenn die Anzahl der Reihen größer ist als die Anzahl der Farben in der Palette, werden bereits verwendete Farben erneut verwendet, sodass zwei Reihen dann möglicherweise die gleiche Farbe aufweisen können. Dies ist häufig bei Verwendung eines Formdiagramms der Fall, in dem jedem Datenpunkt eine Farbe aus der Palette zugewiesen wird. Definieren Sie eine benutzerdefinierte Palette, die mindestens so viele Farben aufweist, wie das Diagramm Reihen, um Probleme mit dieser Funktion zu vermeiden.  
  
 Im Eigenschaftenbereich können Sie eine neue Palette auswählen oder eine benutzerdefinierte Palette definieren. Weitere Informationen finden Sie unter [Definieren von Farben in einem Diagramm mit einer Palette (Berichts-Generator und SSRS)](../../reporting-services/report-design/define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="using-built-in-palettes"></a>Verwenden von integrierten Paletten  
 Reporting Services stellt eine Liste vordefinierter, integrierter Paletten bereit, mit denen Sie Farben für eine Reihe im Diagramm definieren können. Alle integrierten Paletten enthalten zwischen 10 und 16 Farbwerten. Diese können nicht erweitert werden. Wenn Sie mehr als 16 Farben benötigen, ist das Definieren einer eigenen Farbpalette erforderlich.  
  
 Wenn Sie einen Bericht drucken möchten, können Sie die Palette **Graustufen** verwenden. Diese Palette verwendet Schwarzweißwerte zur Darstellung der Reihen in einem Diagramm.  
  
 Die Palette Standard wurde in früheren Versionen von Reporting Services als Standarddiagrammpalette verwendet. Der Name wurde aus Konsistenzgründen beibehalten. Diagramme können mit der Standardpalette nahtlos aktualisiert werden; nach dem Upgrade können Sie diese ggf. ändern.  
  
## <a name="using-custom-palettes"></a>Verwenden benutzerdefinierter Paletten  
 Wenn Sie eigene Farben für das Diagramm zuweisen möchten, können Sie eine benutzerdefinierte Palette verwenden. Mit einer benutzerdefinierten Palette können Sie eigene Farben in der Reihenfolge zuweisen, in der sie im Diagramm angezeigt werden sollen. Benutzerdefinierte Paletten sind besonders hilfreich, wenn die Anzahl der Reihen im Diagramm zur Entwurfszeit noch nicht genau feststeht. Weitere Informationen finden Sie unter [Definieren von Farben in einem Diagramm mit einer Palette (Berichts-Generator und SSRS)](../../reporting-services/report-design/define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md).  
  
## <a name="using-a-color-fill-on-each-series"></a>Verwenden von Farbfülleffekten für Einzelreihen  
 Sie können auch eigene Farben für das Diagramm definieren, indem Sie eine Farbe für jede Reihe im Diagramm angeben. Öffnen Sie dazu das Dialogfeld **Reiheneigenschaften** , und legen Sie für **Ausfüllen** die Eigenschaft **Farbe**fest. Dadurch werden alle definierten Paletten überschrieben. Benutzerdefinierte Farbpaletten sind im Allgemeinen gegenüber dem Definieren eigener Farben zu bevorzugen, da die Anzahl der Reihen im Dataset möglicherweise erst zum Zeitpunkt der Berichtsverarbeitung feststeht.  
  
 Dieser Ansatz eignet sich am besten, wenn Sie die Farbe der Reihe basierend auf einem Ausdruck bedingt festlegen möchten.  Weitere Informationen finden Sie unter [Formatieren von Datenpunkten in einem Diagramm &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/formatting-data-points-on-a-chart-report-builder-and-ssrs.md).  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [Angeben von Farben, die für mehrere Formdiagramme konsistent sind &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/specify-consistent-colors-across-multiple-shape-charts-report-builder-and-ssrs.md)  
  
 [Definieren von Farben in einem Diagramm mit einer Palette &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md))  
  
 [Hervorheben von Diagrammdaten durch Hinzufügen von Bereichsstreifen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/highlight-chart-data-by-adding-strip-lines-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Formatieren eines Diagramms &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [Hinzufügen einer Abschrägung, Prägung und Struktur zu einem Diagramm (Berichts-Generator und SSRS)](../../reporting-services/report-design/chart-effects-add-bevel-emboss-or-texture-report-builder.md)   
 [Diagramme &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [Formatieren der Legende in einem Diagramm &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/chart-legend-formatting-report-builder.md)  
  
  

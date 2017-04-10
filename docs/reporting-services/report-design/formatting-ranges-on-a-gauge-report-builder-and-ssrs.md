---
title: "Formatieren von Bereichen auf einem Messger&#228;t (Berichts-Generator und SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ffdec8ca-3e95-41cd-850b-9e8c83be4b49
caps.latest.revision: 7
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 7
---
# Formatieren von Bereichen auf einem Messger&#228;t (Berichts-Generator und SSRS)
 In einem paginierten [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)]-Bericht ist ein Messbereich eine Zone oder ein Bereich auf der Messgerätskala, die oder der einen wichtigen Unterabschnitt von Werten auf dem Messgerät angibt. Mit einem Messbereich können Sie grafisch angeben, wann der Zeigerwert in eine bestimmte Wertespanne eintritt. Messbereiche sind durch einen Startwert und einen Endwert definiert.  
  
 Mithilfe von Messbereichen können Sie auch unterschiedliche Abschnitte eines Messgeräts definieren. Auf einem Messgerät mit Werten von 0 bis 10 können Sie beispielsweise einen roten Messbereich mit Werten von 0 bis 3, einen gelben Messbereich mit Werten von 4 bis 7 und einen grünen Messbereich mit Werten von 8 bis 10 definieren. Wenn der von Ihnen angegebene Startwert größer als der angegebene Endwert ist, werden die Werte ausgetauscht, sodass der Startwert als Endwert und der Endwert als Startwert verwendet wird.  
  
 Sie können den Messbereich auf dieselbe Weise wie Zeiger auf einer Skala positionieren. Die Position des Messbereichs wird von den Eigenschaften **Position** und **Abstand von Skala** bestimmt. Weitere Informationen finden Sie unter [Messgeräte &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## Siehe auch  
 [Formatieren von Skalen auf einem Messgerät &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/formatting-scales-on-a-gauge-report-builder-and-ssrs.md)   
 [Formatieren von Zeigern auf einem Messgerät &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/formatting-pointers-on-a-gauge-report-builder-and-ssrs.md)   
 [Festlegen eines Mindestwerts oder eines Höchstwerts auf einem Messgerät &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/set-a-minimum-or-maximum-on-a-gauge-report-builder-and-ssrs.md)   
 [Tutorial: Hinzufügen eines KPI zu einem Bericht &#40;Berichts-Generator&#41;](../../reporting-services/tutorial-adding-a-kpi-to-your-report-report-builder.md)   
 [Messgeräte &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md)  
  
  
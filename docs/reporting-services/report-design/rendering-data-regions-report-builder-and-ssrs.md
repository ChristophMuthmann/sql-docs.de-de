---
title: Rendern von Datenbereichen (Berichts-Generator und SSRS) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4f3b2c7d-3669-457f-899b-b758d1db3426
caps.latest.revision: "6"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 83d210b33acb4e3cf3ac93b3f2eaeb47e8c326cc
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="rendering-data-regions-report-builder-and-ssrs"></a>Rendern von Datenbereichen (Berichts-Generator und SSRS)
  Zusätzlich zu den allgemeinen Renderingverhaltensweisen, die auf alle Berichtselemente zutreffen, befolgen Datenbereiche zusätzliche Verhaltensweisen zu Paginierung und Rendering. Datenbereichspezifische Renderingregeln geben unter anderem an, wie Datenbereiche wachsen, wie bestimmte Zellen, wie die Eckzelle oder die Kopfzeilenzellen, gerendert werden und wie ein Datenbereich mit Lesefolge von rechts nach links gerendert wird. In diesem Thema wird erläutert, wie die verschiedenen Teile eines Datenbereichs gerendert werden.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="tablix-data-regions"></a>Tablix-Datenbereiche  
 Der Tablix-Datenbereich, der es Ihnen ermöglicht, Tabellen, Matrizen und Listen zu erstellen, wird als Raster aus Spalten und Zeilen gerendert. Die Schnittstelle einer Zeile und einer Spalte ist eine Zelle. Beim Rendern kann diese Zelle Daten oder andere Berichtselemente, wie Bilder, Rechtecke, Textfelder oder Unterberichte, enthalten. Ein Tablix-Datenbereich kann vertikal und/oder horizontal wachsen. Außerdem können die Eckzelle, die Kopfzeilenzellen des Datenbereichs sowie die Textzellen des Datenbereichs basierend auf ihren Inhalten wachsen. Wenn sich der Datenbereich über mehrere Seiten erstreckt, werden Berichtselemente, die zur Wiederholung mit dem Datenbereich festgelegt sind, auf jeder Seite gerendert, auf der der Datenbereich angezeigt wird. Weitere Informationen finden Sie unter [Tabellen, Matrizen und Listen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md).  
  
### <a name="right-to-left"></a>Von rechts nach links  
 Ein Tablix-Datenbereich, der zur Anzeige von rechts nach links festgelegt ist, wird beim Rendering als Spiegelbild der Datenbereichsstruktur von links nach rechts behandelt. Die Ecke des Datenbereichs wird in der oberen rechten Ecke angezeigt. Wenn dynamische Spalten im Bericht vorhanden sind, werden sie nach links erweitert. Rechts-nach-links-Einstellungen beeinflussen die Reihenfolge der Daten im Datenbereich nicht. Ihre Spalten werden lediglich anders angeordnet.  
  
### <a name="tablix-headers"></a>Tablix-Kopfzeilen  
 Tablix-Kopfzeilen werden als Zeilen- oder Spaltenkopfzeilen gerendert, je nachdem, ob die Kopfzeilenzelle in der Zeilengruppenhierarchie oder in der Spaltengruppenhierarchie angezeigt wird. Wenn ein logischer Seitenumbruch innerhalb des Zelleninhalts einer Kopfzeile vorhanden ist, wird er ignoriert. Logische Seitenumbrüche in Spaltengruppen werden ignoriert.  
  
 Logische Seitenumbrüche in Gruppen bewirken nicht, dass äußere Gruppenkopfzeilen unterbrochen werden. Nehmen Sie beispielsweise an, dass in Ihrem Bericht das Land als äußere Gruppe und die Region als innere Gruppe verwendet wird. Wenn sich zwischen den Instanzen der Regionsgruppe ein logischer Seitenumbruch befindet, wird die äußere Gruppe, also das Land, auf beiden Seiten des Berichts angezeigt.  
  
#### <a name="repeated-tablix-headers"></a>Wiederholte Tablix-Kopfzeilen  
 Wenn die RepeatWith-Eigenschaft im Bereich **Eigenschaften** festgelegt ist, werden Elemente, die sich innerhalb des Datenbereichs nicht verändern, wie beispielsweise Spaltenkopfzeilen, auf jeder Seite wiederholt, auf der dieser Teil des Datenbereichs gerendert wird. Wenn z. B. eine Datenzeile auf der nächsten Seite angezeigt wird und die Eigenschaft Wiederholen mit festgelegt ist, werden die Spaltenkopfzeilen auch auf der gerenderten Seite angezeigt.  
  
### <a name="tablix-corner"></a>Tablix-Ecke  
 Die linke obere Zelle wird als Tablix-Ecke bezeichnet. Die Tablix-Ecke kann andere Berichtselemente enthalten, wenn jedoch logische Seitenumbrüche in die Ecke eingefügt werden, werden diese beim Rendern des Tablix-Datenbereichs ignoriert.  
  
### <a name="tablix-body"></a>Tablix-Text  
 Der Tablix-Text besteht aus Tablix-Zellen. Der Tablix-Text wird auf der Basis von Paginierungsregeln und den Renderingverhaltensweisen von Berichtselementen gerendert. Weitere Informationen finden Sie unter [Rendern von Berichtselementen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/rendering-report-items-report-builder-and-ssrs.md).  
  
## <a name="chart-gauge-and-map-data-regions"></a>Diagramm-, Maßstabs- und Zuordnungsdatenbereiche  
 Diagramm-, Maßstabs- und Zuordnungsdatenbereiche verhalten sich beim Rendern und Anzeigen im Berichtstext wie Bilder. Werten innerhalb des Datenbereichs können Aktionen zugeordnet sein, beispielsweise ein Link zu einem anderen Bericht oder ein Wechsel zu einem Lesezeichen. Diese Aktionen können ebenfalls gerendert werden, wenn der Renderer dies unterstützt.  
  
## <a name="see-also"></a>Siehe auch  
 [Paginierung in Reporting Services &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [Renderingverhalten (Berichts-Generator und SSRS)](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [Interaktive Funktionalität für verschiedene Berichtsrenderingerweiterungen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-builder/interactive-functionality-different-report-rendering-extensions.md)   
 [Rendern von Berichtselementen (Berichts-Generator und SSRS)](../../reporting-services/report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [Tabellen, Matrizen und Listen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Diagramme &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [Messgeräte &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md)  
  
  

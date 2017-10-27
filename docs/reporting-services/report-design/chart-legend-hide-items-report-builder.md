---
title: Ausblenden von Legendenelementen im Diagramm (Berichts-Generator und SSRS) | Microsoft Docs
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
ms.assetid: 92256240-0cd5-4be4-8904-d1e3b93cb6b3
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 06f1cf8cde2eb9a9c9aa261188e64aa2fc7afe4b
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="chart-legend---hide-items-report-builder"></a>Diagrammlegende - Hintergrund-Elementen (Berichts-Generator)
Standardmäßig werden alle in einem paginierten [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Bericht einem Nicht-Formdiagramm hinzugefügten Reihen in der Legende als Element hinzugefügt. Für Kreis-, Ring-, Trichter- und Pyramidendiagramme werden für alle dem Diagramm hinzugefügten Reihen der Legende einzelne Datenpunkte hinzugefügt.  
  
 Sie können in der Legende beliebige Elemente ausblenden. Wenn Sie ein Legendenelement ausblenden, wird dieses immer noch im Diagramm angezeigt. Dies ist hilfreich in Situationen, in denen für eine dem Diagramm hinzugefügte Reihe keine weiteren Informationen angezeigt werden sollen. Wenn Sie dem Diagramm beispielsweise eine berechnete Reihe (z. B. einen gleitenden Durchschnitt) hinzugefügt haben, empfiehlt es sich u. U., diesen Eintrag in der Legende auszublenden, sodass nur für die ursprüngliche Reihe weitere Informationen angezeigt werden.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-hide-an-item-from-display-in-the-legend"></a>So blenden Sie ein in der Legende angezeigtes Element aus  
  
1.  Klicken Sie mit der rechten Maustaste auf die auszublendende Reihe, und wählen Sie die Option **Reiheneigenschaften**aus.  
  
2.  Klicken Sie auf **Legende**. Aktivieren Sie die Option **Diese Reihe in Legende nicht anzeigen** .  
  
    > [!NOTE]  
    >  Eine Reihe kann nicht für eine Gruppe ausgeblendet und für andere angezeigt werden. Wenn Sie dem Bereich **Reihengruppen** ein Feld hinzugefügt haben, werden alle zu dieser Gruppe gehörenden Reihen ausgeblendet.  
  
## <a name="see-also"></a>Siehe auch  
 [Formatieren der Legende in einem Diagramm &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/chart-legend-formatting-report-builder.md)   
 [Formatieren von Datenpunkten in einem Diagramm &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
 [Ändern des Texts eines Legendenelements &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/chart-legend-change-item-text-report-builder.md)   
 [Hinzufügen eines gleitenden Durchschnitts zu einem Diagramm &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/add-a-moving-average-to-a-chart-report-builder-and-ssrs.md)   
 [Mininglegende Eigenschaften (Dialogfeld), Allgemein &#40; Berichts-Generator und SSRS &#41;](http://msdn.microsoft.com/library/db718f8f-f185-422f-871c-96f0749e5893)  
  
  


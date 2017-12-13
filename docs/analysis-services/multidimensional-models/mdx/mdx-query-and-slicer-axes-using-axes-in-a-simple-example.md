---
title: Verwenden von Abfrage- und Slicerachsen in einem einfachen Beispiel (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- slicer axis
- query axis [MDX]
ms.assetid: 85bcb26f-5971-4153-b334-61f8d8b475b5
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 9759826389cef8eb16f5330036a008723e27dc7b
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="mdx-query-and-slicer-axes---using-axes-in-a-simple-example"></a>MDX Abfrage- und Slicerachsen - mithilfe von Achsen in einem einfachen Beispiel
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Das einfache Beispiel in diesem Thema vorgestellten veranschaulicht die Grundlagen der angeben und Verwenden von Abfrage- und slicerachsen erläutert.  
  
## <a name="the-cube"></a>Der Cube  
 Ein Cube namens TestCube hat zwei einfache Dimensionen mit den Namen Route und Time. Jede Dimension hat nur eine Benutzerhierarchie, die den Namen Route bzw. Time hat. Da die Measures des Cubes Teil der Measures-Dimension sind, hat dieser Cube insgesamt drei Dimensionen.  
  
## <a name="the-query"></a>Die Abfrage  
 Die Abfrage muss eine Matrix bereitstellen, in der das Packages-Measure über Routen und Zeiten hinweg verglichen werden kann.  
  
 Im folgenden MDX-Abfragebeispiel sind die Hierarchien Route und Time die Abfrageachsen, und die Measures-Dimension ist die Slicerachse. Die [Members](../../../mdx/members-set-mdx.md) -Funktion zeigt an, dass MDX die Elemente der Hierarchie oder der Ebene zum Erstellen einer Menge verwendet. Wird die **Members** -Funktion verwendet, ist es nicht erforderlich, dass Sie in der jeweiligen MDX-Abfrage explizit jedes Element einer bestimmten Hierarchie oder Ebene angeben.  
  
```  
SELECT  
   { Route.nonground.Members } ON COLUMNS,  
   { Time.[1st half].Members } ON ROWS  
FROM TestCube  
WHERE ( [Measures].[Packages] )  
```  
  
## <a name="the-results"></a>Das Ergebnis  
 Das Ergebnis ist ein Raster, das die Werte enthält, die das Packages-Measure in jedem Schnittpunkt der Achsendimensionen COLUMNS und ROWS hat. Die folgende Tabelle zeigt, wie dieses Raster aussehen würde:  
  
||air|sea|  
|-|---------|---------|  
|Erstes Quartal|60|50|  
|Zweites Quartal|45|45|  
  
## <a name="see-also"></a>Siehe auch  
 [Angeben des Inhalts einer Abfrageachse &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-query-axis.md)   
 [Angeben des Inhalts einer Slicerachse &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-slicer-axis.md)  
  
  

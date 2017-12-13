---
title: Angeben des Inhalts einer slicerachse (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
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
- filtering data [MDX]
ms.assetid: c56b0a70-cdec-427f-990e-425290344e7d
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: c88d724873a7e2a7e811a4a28c9b76b5c9b12ccd
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="mdx-query-and-slicer-axes---specify-the-contents-of-a-slicer-axis"></a>MDX Abfrage- und Slicerachsen - Geben Sie den Inhalt einer Slicer-Achse
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Die slicerachse filtert die von der MDX (Multidimensional Expressions)-SELECT-Anweisung, beschränken die zurückgegebenen Daten, sodass nur Daten, die sich überschneidenden mit den angegebenen Elementen zurückgegeben werden. Sie kann als zusätzliche unsichtbare Achse in einer Abfrage betrachtet werden. Die Slicerachse wird in der WHERE-Klausel der SELECT-Anweisung von MDX definiert.  
  
## <a name="slicer-axis-syntax"></a>Slicerachse (Syntax)  
 Zum expliziten Angeben einer Slicerachse verwenden Sie in MDX die folgende `<SELECT slicer axis clause>` -Syntax:  
  
```  
<SELECT slicer axis clause> ::=  WHERE Set_Expression  
```  
  
 In dieser Syntax der Slicerachse kann `Set_Expression` entweder einem Tupelausdruck entsprechen, der zum Auswerten der Klausel wie eine Menge behandelt wird, oder einem Mengenausdruck. Wird ein Mengenausdruck angegeben, versucht MDX, die Menge auszuwerten, indem die Ergebniszellen in jedem Tupel der Menge aggregiert werden. Das heißt, MDX versucht, die [Aggregate](../../../mdx/aggregate-mdx.md) -Funktion auf die Menge anzuwenden und aggregiert jedes Measure durch die ihm zugeordnete Aggregatfunktion. Wenn der Mengenausdruck nicht als Kreuzprodukt von Elementen der Attributhierarchie ausgedrückt werden kann, behandelt MDX Zellen außerhalb des Mengenausdrucks für die Slicerachse bei der Auswertung als NULL-Werte.  
  
> [!IMPORTANT]  
>  Im Gegensatz zur WHERE-Klausel in SQL filtert die WHERE-Klausel einer MDX SELECT-Anweisung nie direkt, was auf der ROWS-Achse einer Abfrage zurückgegeben wird. Um zu filtern, was auf der ROWS- oder COLUMNS-Achse einer Abfrage angezeigt wird, können Sie eine Vielzahl von MDX-Funktionen verwenden, z. B. FILTER, NONEMPTY und TOPCOUNT.  
  
### <a name="implicit-slicer-axis"></a>Implizite Slicerachse  
 Wenn ein Element aus einer Hierarchie im Cube nicht explizit in eine Abfrageachse eingeschlossen wird, wird das Standardelement aus dieser Hierarchie implizit in die Slicerachse eingeschlossen. Weitere Informationen zu Standardelementen finden Sie unter [Definieren eines Standardelements](../../../analysis-services/multidimensional-models/attribute-properties-define-a-default-member.md).  
  
## <a name="examples"></a>Beispiele  
 Die folgende Abfrage enthält keine WHERE-Klausel und gibt den Wert des Internet Sales Amount-Measures für alle Kalenderjahre zurück:  
  
```  
SELECT {[Measures].[Internet Sales Amount]} ON COLUMNS,  
[Date].[Calendar Year].MEMBERS ON ROWS  
FROM [Adventure Works]  
```  
  
 Durch Hinzufügen einer WHERE-Klausel wie folgt:  
  
```  
SELECT {[Measures].[Internet Sales Amount]} ON COLUMNS,  
[Date].[Calendar Year].MEMBERS ON ROWS  
FROM [Adventure Works]  
WHERE([Customer].[Customer Geography].[Country].&[United States])  
  
```  
  
 wird nicht geändert, was in Zeilen oder Spalten in der Abfrage zurückgegeben wird. Dafür werden die zurückgegebenen Werte für die einzelnen Zellen geändert. In diesem Beispiel ist die Abfrage in Slices aufgeteilt, sodass sie den Wert von Internet Sales Amount für alle Kalenderjahre zurückgibt, jedoch nur für Kunden, die in den USA wohnen. Der WHERE-Klausel können mehrere Elemente unterschiedlicher Hierarchien hinzugefügt werden. Die folgende Abfrage zeigt den Wert von Internet Sales Amount für alle Kalenderjahre für Kunden, die in den USA wohnen und die Produkte in der Kategorie Bikes gekauft haben.  
  
```  
SELECT {[Measures].[Internet Sales Amount]} ON COLUMNS,  
[Date].[Calendar Year].MEMBERS ON ROWS  
FROM [Adventure Works]  
WHERE([Customer].[Customer Geography].[Country].&[United States], [Product].[Category].&[1])  
```  
  
 Wenn Sie mehrere Elemente aus derselben Hierarchie verwenden möchten, muss der WHERE-Klausel eine Menge hinzugefügt werden. Die folgende Abfrage zeigt beispielsweise den Wert von Internet Sales Amount für alle Kalenderjahre für Kunden, die Produkte in der Kategorie Bikes gekauft haben und die in den USA oder in Großbritannien wohnen:  
  
```  
SELECT {[Measures].[Internet Sales Amount]} ON COLUMNS,  
[Date].[Calendar Year].MEMBERS ON ROWS  
FROM [Adventure Works]  
WHERE(  
{[Customer].[Customer Geography].[Country].&[United States]  
, [Customer].[Customer Geography].[Country].&[United Kingdom]}  
, [Product].[Category].&[1])  
  
```  
  
 Wie oben erwähnt, werden bei Verwendung einer Menge in der WHERE-Klausel implizit Werte für alle Elemente in der Menge aggregiert. In diesem Fall zeigt die Abfrage aggregierte Werte für die USA und Großbritannien in jeder Zelle.  
  
  

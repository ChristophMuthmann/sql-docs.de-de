---
title: Die grundlegende MDX-Abfrage (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/13/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- queries [MDX], SELECT statement
- queries [MDX], about queries
- cellsets [MDX]
- SELECT statement [MDX]
- cubes [Analysis Services], SELECT statement
ms.assetid: 4fa5a95a-fec9-4584-875c-dbf030c53e82
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Active
ms.openlocfilehash: 9abd75f8cbed78630caac64447b8df59cde3ea56
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="mdx-query---the-basic-query"></a>MDX-Abfrage - die grundlegende Abfrage
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Die grundlegende MDX (Multidimensional Expressions)-Abfrage ist die SELECT-Anweisung, die am häufigsten verwendete Abfrage in MDX. Wenn Sie wissen, wie in einer SELECT-Anweisung von MDX ein Resultset angegeben wird, wie die Syntax der SELECT-Anweisung lautet und wie eine einfache Abfrage mit der SELECT-Anweisung erstellt wird, verfügen Sie über das Basiswissen zum Abfragen mehrdimensionaler Daten mit MDX.  
  
## <a name="specifying-a-result-set"></a>Angeben eines Resultsets  
 Die SELECT-Anweisung in MDX gibt ein Resultset an, das aus einer Teilmenge mehrdimensionaler Daten besteht, die aus einem Cube zurückgegeben wurde. Zum Angeben eines Resultsets muss die MDX-Abfrage die folgenden Informationen enthalten:  
  
-   Die Anzahl der Achsen, die das Resultset enthalten soll. Sie können maximal 128 Achsen in einer MDX-Abfrage angeben.  
  
-   Die Menge von Elementen oder Tupeln, die auf jeder Achse der MDX-Abfrage enthalten sein soll.  
  
-   Der Name des Cubes, der den Kontext der MDX-Abfrage festlegt.  
  
-   Die Menge von Elementen oder Tupeln, die auf der Slicer-Achse enthalten sein soll. Weitere Informationen zu Slicer- und Abfrageachsen finden Sie unter [Einschränken der Abfrage mit Abfrage- und Slicerachsen &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-restricting-the-query.md).  
  
 Die SELECT-Anweisung von MDX verwendet die folgenden Klauseln zum Identifizieren der Abfrage-Achsen, des abgefragten Cubes und der Slicer-Achse:  
  
-   Eine SELECT-Klausel, die die Abfrage-Achsen einer SELECT-Anweisung von MDX bestimmt. Weitere Informationen zur Erstellung von Abfrageachsen in einer SELECT-Klausel finden Sie unter [Angeben des Inhalts einer Abfrageachse &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-query-axis.md).  
  
-   Eine FROM-Klausel, mit der festgelegt wird, welcher Cube abgefragt wird. Weitere Informationen zur FROM-Klausel in der SELECT-Anweisung von MDX finden Sie unter [SELECT-Anweisung &#40;MDX&#41;](../../../mdx/mdx-data-manipulation-select.md).  
  
-   Eine optionale WHERE-Klausel, mit der festgelegt wird, welche Elemente oder Tupeln auf der Slicer-Achse verwendet werden sollen, um die zurückgegebenen Daten einzuschränken. Weitere Informationen zur Erstellung einer Abfrageachse in einer WHERE-Klausel finden Sie unter [Angeben des Inhalts einer Slicerachse &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-slicer-axis.md).  
  
> [!NOTE]  
>  Weitere Informationen zu den verschiedenen Klauseln der SELECT-Anweisung finden Sie unter [SELECT-Anweisung &#40;MDX&#41;](../../../mdx/mdx-data-manipulation-select.md).  
  
## <a name="select-statement-syntax"></a>Syntax der SELECT-Anweisung  
 Die folgende Syntax zeigt eine grundlegende SELECT-Anweisung, in der SELECT-, FROM- und WHERE-Klauseln verwendet werden:  
  
```  
[ WITH <SELECT WITH clause> [ , <SELECT WITH clause> ... ] ]   
SELECT [ * | ( <SELECT query axis clause>   
    [ , <SELECT query axis clause> ... ] ) ]  
FROM <SELECT subcube clause>   
[ <SELECT slicer axis clause> ]  
[ <SELECT cell property list clause> ]  
```  
  
 Die SELECT-Anweisung von MDX unterstützt optionale Syntax, wie z. B. das WITH-Schlüsselwort und die Erstellung von berechneten Elementen mithilfe von MDX-Funktionen, um die Elemente in eine Achse oder Slicer-Achse einzuschließen. Außerdem bietet sie die Möglichkeit, die Werte bestimmter Zelleneigenschaften im Rahmen der Abfrage zurückzugeben. Weitere Informationen zur SELECT-Anweisung von MDX finden Sie unter [SELECT-Anweisung &#40;MDX&#41;](../../../mdx/mdx-data-manipulation-select.md).  
  
### <a name="comparing-the-syntax-of-the-mdx-select-statement-to-sql"></a>Vergleich der Syntax der SELECT-Anweisung von MDX mit SQL  
 Das Syntaxformat der SELECT-Anweisung von MDX gleicht dem Format der SQL-Syntax. Es gibt jedoch einige deutliche Unterschiede:  
  
-   Die MDX-Syntax gibt Mengen an, indem Tupel oder Elemente in geschweifte Klammern (die Zeichen { und }) eingeschlossen werden. Weitere Informationen zur Syntax von Elementen, Tupeln und Mengen finden Sie unter [Verwenden von Elementen, Tupeln und Mengen &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md).  
  
-   MDX-Abfragen können 0, 1, 2 oder bis zu 128 Abfrage-Achsen in der SELECT-Anweisung enthalten. Jede Achse verhält sich auf exakt die gleiche Weise, im Gegensatz zu SQL, wo es deutliche Unterschiede zwischen den Verhaltensweisen der Zeilen und Spalten einer Abfrage gibt.  
  
-   Wie in einer SQL-Abfrage benennt die FROM-Klausel die Quelle der Daten für die MDX-Abfrage. Die MDX-FROM-Klausel ist jedoch auf einen einzelnen Cube beschränkt. Informationen aus anderen Cubes können Wert für Wert mithilfe der LookupCube-Funktion abgerufen werden.  
  
-   Die WHERE-Klausel beschreibt die Slicer-Achse in einer MDX-Abfrage. Sie verhält sich in etwa wie eine unsichtbare weitere Achse in der Abfrage, die die Werte, die in den Zellen im Resultset angezeigt werden, in Slices aufteilt. Im Gegensatz zur SQL-Klausel WHERE nimmt sie keinen direkten Einfluss darauf, was auf der ROWS-Achse der Abfrage angezeigt wird. Die Funktionalität der SQL-Klausel WHERE steht durch andere MDX-Funktionen zur Verfügung, wie z. B. die FILTER-Funktion.  
  
## <a name="select-statement-example"></a>Beispiel für die SELECT-Anweisung  
 Das folgende Beispiel zeigt eine grundlegende MDX-Abfrage mit der SELECT-Anweisung. Die Abfrage gibt ein Resultset zurück, das die Umsatz- und Steuerbeträge für 2002 und 2003 in den südwestlichen Vertriebsregionen enthält.  
  
```  
SELECT  
    { [Measures].[Sales Amount],   
        [Measures].[Tax Amount] } ON COLUMNS,  
    { [Date].[Fiscal].[Fiscal Year].&[2002],   
        [Date].[Fiscal].[Fiscal Year].&[2003] } ON ROWS  
FROM [Adventure Works]  
WHERE ( [Sales Territory].[Southwest] )  
```  
  
 In diesem Beispiel werden durch die Abfrage die folgenden Resultset-Informationen definiert:  
  
-   Die SELECT-Klausel legt die Abfrage-Achsen auf die Elemente Sales Amount (Umsatz) und Tax Amount (Steuern) der Measures-Dimension sowie auf die Elemente 2002 und 2003 der Date-Dimension fest.  
  
-   Die FROM-Klausel zeigt an, dass die Datenquelle im Adventure Works-Cube besteht.  
  
-   Die WHERE-Klausel definiert das Southwest-Element der Sales Territory-Dimension zur Slicer-Achse.  
  
 Beachten Sie, dass das Abfragebeispiel auch die Achsenaliase COLUMNS und ROWS verwendet. Ebenso können die Ordnungspositionen für diese Achsen verwendet werden. Das folgende Beispiel zeigt, wie die MDX-Abfrage mithilfe der Ordnungsposition jeder Achse geschrieben werden könnte:  
  
```  
SELECT  
    { [Measures].[Sales Amount],   
        [Measures].[Tax Amount] } ON 0,  
    { [Date].[Fiscal].[Fiscal Year].&[2002],   
        [Date].[Fiscal].[Fiscal Year].&[2003] } ON 1  
FROM [Adventure Works]  
WHERE ( [Sales Territory].[Southwest] )  
```  
  
 Ausführlichere Beispiele finden Sie unter [Angeben des Inhalts einer Abfrageachse &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-query-axis.md)und [Angeben des Inhalts einer Slicerachse &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-slicer-axis.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Schlüsselkonzepte in MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)   
 [SELECT-Anweisung &#40; MDX &#41;](../../../mdx/mdx-data-manipulation-select.md)  
  
  

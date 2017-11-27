---
title: DrilldownLevel (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DRILLDOWNLEVEL
dev_langs:
- kbMDX
helpviewer_keywords:
- DrilldownLevel function
ms.assetid: 47531ce5-1ac0-4aa9-a85c-824fb5d21e7c
caps.latest.revision: 43
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: d6f90b918cbb817154e699ac8e25bdcaf4119875
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="drilldownlevel-mdx"></a>DrilldownLevel (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Führt einen Drilldown der Elemente einer Menge in eine Ebene unter der untersten Ebene aus, die in der Menge dargestellt ist.  
  
 Angeben der Ebene klicken Sie zu dem einen Drilldown nach unten ist optional, aber wenn Sie die Ebene festlegen, können Sie entweder eine **Ebene Ausdruck** oder **Indexebene**. Diese Argumente schließen sich gegenseitig aus. Wenn berechnete Elemente in der Abfrage vorhanden sind, können Sie ein Argument angeben, um sie in das Rowset einzubeziehen.  
  
## <a name="syntax"></a>Syntax  
  
```  
DrilldownLevel(Set_Expression [,[Level_Expression] ,[Index]] [,INCLUDE_CALC_MEMBERS])  
```  
  
## <a name="arguments"></a>Argumente  
 *Set_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Menge zurückgibt.  
  
 *Level_Expression*  
 (Optional). Ein MDX-Ausdruck, der explizit die Ebene für den Drilldown identifiziert. Wenn Sie einen Ebenenausdruck angegeben, überspringen Sie das Indexargument unten.  
  
 *Index*  
 (Optional). Ein gültiger numerischer Ausdruck, der die Nummer der Hierarchie angibt, in die innerhalb der Menge ein Drilldown durchgeführt werden soll. Sie können die Indexebene statt Level_Expression verwenden, um explizit die Ebene festzulegen, auf die ein Drilldown ausgeführt werden soll.  
  
 *Include_Calc_Members*  
 (Optional). Ein Flag, das anzeigt, ob berechnete Elemente eingeschlossen werden sollen, wenn sie vorhanden sind (auf Drilldownebene).  
  
## <a name="remarks"></a>Hinweise  
 Die **DrilldownLevel** Funktion gibt einen Satz untergeordneter Elemente in einer hierarchischen Reihenfolge, basierend auf den Elementen in der angegebenen Menge enthalten. Die Reihenfolge der ursprünglichen Elemente in der angegebenen Menge wird beibehalten, wobei jedoch alle in das Resultset der Funktion aufgenommenen untergeordneten Elemente direkt unter ihrem übergeordneten Element aufgenommen werden.  
  
 Wenn eine Datenstruktur mit einer Hierarchie mit mehreren Ebenen vorliegt, können Sie explizit eine Ebene auswählen, auf die der Drilldown erfolgen soll. Es gibt zwei Möglichkeiten, die Ebene festzulegen. Diese schließen sich gegenseitig aus. Beim ersten Ansatz wird zum Festlegen der **Level_expression** Arguments mithilfe eines MDX-Ausdrucks, der die Ebene, ein alternativer Ansatz ist die Angabe der **Index** -Argument, mit dem ein numerischer Ausdruck, der die Ebene nach Zahlen festlegt.  
  
 Wenn ein Ebenenausdruck angegeben wird, erstellt die Funktion eine Menge in einer hierarchischen Reihenfolge, indem die untergeordneten Elemente nur für diejenigen Elemente abgerufen werden, die sich auf der angegebenen Ebene befinden. Wenn ein Ebenenausdruck festgelegt ist und sich auf dieser Ebene kein Element befindet, wird der Ebenenausdruck ignoriert.  
  
 Wenn ein Indexwert angegeben wird, erstellt die Funktion basierend auf einem nullbasierten Index eine Menge in einer hierarchischen Reihenfolge, indem die untergeordneten Elemente nur für die Elemente auf der nächstunteren Ebene der Dimension abgerufen werden, auf die in der Menge verwiesen wird.  
  
 Wenn weder ein Ebenenausdruck noch ein Indexwert angegeben wird, erstellt die Funktion eine Menge in einer hierarchischen Reihenfolge, indem die untergeordneten Elemente nur für die Elemente, die auf der untersten Ebene der ersten Dimension in der angegebenen Menge verwiesen werden abgerufen.  
  
 Abfrage der XMLA-Eigenschaft MdpropMdxDrillFunctions können Sie den Grad der Unterstützung, die der Server die drillingfunktionen bereitgestellt; finden Sie unter [unterstützten XMLA-Eigenschaften &#40; XMLA &#41; ](../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md) für Details.  
  
## <a name="examples"></a>Beispiele  
 Sie können die folgenden Beispiele im MDX-Abfragefenster in SSMS ausprobieren. Verwenden Sie dafür den Adventure Works-Cube.  
  
 **Beispiel 1 – zeigt minimale syntax**  
  
 Das erste Beispiel zeigt die minimale Syntax für **DrilldownLevel**. Das einzige erforderliche Argument ist ein Mengenausdruck. Beachten Sie, dass wenn Sie diese Abfrage ausführen, die übergeordnete [All Categories] und die Elemente der nächstniedrigeren Ebene, Sie nach unten erhalten: [Accessories], [Bikes] und so weiter. Obwohl in diesem Beispiel einfach ist, zeigt es den grundlegenden Zweck der der **DrilldownLevel** -Funktion, die auf der nächstniedrigeren Ebene Drilldowns ist.  
  
```  
SELECT DRILLDOWNLEVEL({[Product].[Product Categories]} * {[Sales Territory].[Sales Territory]}}) ON COLUMNS  
FROM [Adventure Works]  
```  
  
 Beispiel 2 – Alternative Syntax mit expliziter Indexebene  
  
 Dieses Beispiel zeigt die alternative Syntax. Hier wird die Indexebene über einen numerischen Ausdruck festgelegt. In diesem Fall ist die Indexebene 0. Für einen nullbasierten Index ist das die unterste Ebene.  
  
```  
SELECT  
DRILLDOWNLEVEL({[Product].[Product Categories]} * {[Sales Territory].[Sales Territory]},,0) ON COLUMNS  
FROM [Adventure Works]  
```  
  
 Beachten Sie, dass das Resultset mit der vorherigen Abfrage identisch ist. Allgemein gilt, ein Festlegen der Indexebene ist unnötig, es sei denn, der Drilldown soll auf einer bestimmten Ebene beginnen. Führen Sie die vorherige Abfrage erneut aus, und legen Sie einen Indexwert von 1 und dann von 2 fest. Ist der Indexwert auf 1 festgelegt, beginnt der Drilldown auf der zweiten Ebene der Hierarchie. Ist der Indexwert auf 2 festgelegt, beginnt der Drilldown auf der dritten Ebene, der höchsten Ebene in diesem Beispiel. Je höher der numerische Ausdruck, desto höher die Indexebene.  
  
 **Beispiel 3 – zeigt einen Ebenenausdruck**  
  
 Im folgenden Beispiel wird die Verwendung eines Ebenenausdrucks veranschaulicht. Wenn eine Menge vorliegt, die eine hierarchische Struktur darstellt, können Sie mit einem Ebenenausdruck eine Ebene in der Hierarchie auswählen, auf der der Drilldown beginnen soll.  
  
 In diesem Beispiel startet die Ebene der Drilldown auf [City], als das zweite Argument der der **DrilldownLevel** Funktion. Wenn Sie diese Abfrage ausführen, beginnt der Drilldown auf der Ebene [City] für die Staaten Washington und Oregon. Pro die **DrilldownLevel** -Funktion, auch das Resultset enthält die Elemente auf der nächstniedrigeren Ebene, [Postal Codes].  
  
```  
SELECT [Measures].[Internet Sales Amount] ON COLUMNS,  
   NON EMPTY (  
   DRILLDOWNLEVEL(  
       {[Customer].[Customer Geography].[Country].[United States],  
           DESCENDANTS(  
             { [Customer].[Customer Geography].[State-Province].[Washington],    
               [Customer].[Customer Geography].[State-Province].[Oregon]},   
               [Customer].[Customer Geography].[City]) } ,  
[Customer].[Customer Geography].[City] ) )  ON ROWS  
FROM [Adventure Works]  
```  
  
 **Beispiel 4 – einschließen berechneter Elemente**  
  
 Das letzte Beispiel zeigt ein berechnetes Element, das am unteren Rand der Ergebnis angezeigt wird. Legen Sie beim Hinzufügen der **Include_calculated_members** Flag. Beachten Sie, dass das Flag als vierter Parameter festgelegt ist.  
  
 Dieses Beispiel funktioniert, weil das berechnete Element sich auf derselben Ebene befindet wie die nicht berechneten Elemente. Das berechnete Element [West Coast] ist aus den Elementen aus [United States] und allen Elementen aus einer Ebene unter [United States] zusammengesetzt.  
  
```  
WITH MEMBER   
[Customer].[Customer Geography].[Country].&[United States].[West Coast] AS  
[Customer].[Customer Geography].[State-Province].&[OR]&[US] +  
[Customer].[Customer Geography].[State-Province].&[WA]&[US] +  
[Customer].[Customer Geography].[State-Province].&[CA]&[US]  
SELECT [Measures].[Internet Order Count] ON 0,  
DRILLDOWNLEVEL([Customer].[Customer Geography].[Country].&[United States],,,INCLUDE_CALC_MEMBERS) on 1  
FROM [Adventure Works]  
```  
  
 Wenn Sie nur das Flag entfernen und die Abfrage erneut ausführen, erhalten Sie die gleichen Ergebnisse, nur ohne das berechnete Element [West Coast].  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  


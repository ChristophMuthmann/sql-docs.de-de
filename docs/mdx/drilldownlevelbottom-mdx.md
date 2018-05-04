---
title: DrilldownLevelBottom (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DRILLDOWNLEVELBOTTOM
dev_langs:
- kbMDX
helpviewer_keywords:
- DrilldownLevelBottom function
ms.assetid: c00a6a02-e618-4713-805a-870e042f2d51
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 2628ef6a691772a4fc085130e1d1482b2bd4cb2e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="drilldownlevelbottom-mdx"></a>DrilldownLevelBottom (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Führt einen Drilldown der untersten Elemente einer Menge auf einer angegebenen Ebene in eine darunter liegende Ebene aus.  
  
## <a name="syntax"></a>Syntax  
  
```  
DrilldownLevelBottom(Set_Expression, Count [,[<Level_Expression>] [,[<Numeric_Expression>][,INCLUDE_CALC_MEMBERS]]])  
```  
  
## <a name="arguments"></a>Argumente  
 *Set_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Menge zurückgibt.  
  
 *Count*  
 Ein gültiger numerischer Ausdruck, der die Anzahl der Tupel angibt, die zurückgegeben werden sollen.  
  
 *Level_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Ebene zurückgibt.  
  
 *Numeric_expression*  
 Optional. Ein gültiger numerischer Ausdruck, bei dem es sich in der Regel um einen MDX-Ausdruck (Multidimensional Expressions) für Zellenkoordinaten handelt, die eine Zahl zurückgeben.  
  
 *Include_Calc_Members*  
 Optional. Ein Schlüsselwort, das Drilldownergebnissen berechnete Elemente hinzufügt.  
  
## <a name="remarks"></a>Hinweise  
 Wenn ein numerischer Wert angegeben wird, sortiert die **DrilldownLevelBottom** -Funktion die untergeordneten Elemente jedes Elements in der angegebenen Menge aufsteigend nach dem angegebenen Wert, ausgewertet über der Menge der untergeordneten Elemente. Wenn kein numerischer Ausdruck angegeben wird, sortiert die Funktion die untergeordneten Elemente jedes Elements in der angegebenen Menge in aufsteigender Reihenfolge nach den durch die Menge der untergeordneten Elemente dargestellten Zellenwerten, wie durch den Abfragekontext bestimmt. Dieses Verhalten ähnelt dem der BottomCount-Funktion und Tail (MDX)-Funktion, die eine Menge von Elementen in natürlicher Reihenfolge ohne Sortierung zurückgeben.  
  
 Nach dem Sortieren gibt die **DrilldownLevelBottom** -Funktion eine Menge zurück, die die übergeordneten Elemente und die in *Count*angegebene Anzahl der untergeordneten Elemente mit dem niedrigsten Wert enthält.  
  
 Die **DrilldownLevelBottom** Funktion ist vergleichbar mit der [DrilldownLevel](../mdx/drilldownlevel-mdx.md) -Funktion, statt jedoch alle untergeordneten Elemente für jedes Element auf der angegebenen Ebene einzuschließen der **DrilldownLevelBottom** Funktion gibt die Anzahl der untersten untergeordneten Elemente.  
  
 Abfrage der XMLA-Eigenschaft MdpropMdxDrillFunctions können Sie den Grad der Unterstützung, die der Server die drillingfunktionen bereitgestellt; finden Sie unter [XMLA-Eigenschaften unterstützt &#40;XMLA&#41; ](../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md) für Details.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden die untersten drei untergeordneten Elemente der Product Category-Ebene basierend auf dem Standardmeasure zurückgegeben. Im Adventure Works-Beispielcube sind die untersten drei untergeordneten Elemente für Accessories Tires and Tubes, Pumps und Panniers. In Management Studio können Sie im MDX-Abfragefenster zu Products | Product Categories | Members | All Products | Accessories navigieren, um die vollständige Liste anzuzeigen. Sie können das Count-Argument erhöhen, damit mehr Elemente zurückgegeben werden.  
  
```  
SELECT DrilldownLevelBottom   
   ([Product].[Product Categories].children,  
   3,  
   [Product].[Product Categories].[Category])  
   ON 0  
   FROM [Adventure Works]  
```  
  
 Im nächsten Beispiel wird die Verwendung des **include_calc_members** -Flags gezeigt. Dieses wird genutzt, um berechnete Elemente auf Drilldown-Ebene einzuschließen. Das Measure [Reseller Order Count] wird der **DrilldownLevelBottom** -Anweisung hinzugefügt, um sicherzustellen, dass die Ergebnisse nach diesem Measure sortiert werden. Sie müssen Count auf mindestens 9 erhöhen, um diese berechneten Elemente anzuzeigen.  
  
```  
WITH MEMBER   
[Product].[Product Categories].[Category].&[3].[Premium Clothes] AS  
[Product].[Product Categories].[Subcategory].&[18] +  
[Product].[Product Categories].[Subcategory].&[21]  
SELECT [Measures].[Reseller Order Count] ON 0,  
DRILLDOWNLEVELBOTTOM(  
  [Product].[Product Categories].children ,  
  9,  
  [Product].[Product Categories].[Category] ,  
  [Measures].[Reseller Order Count],  
  INCLUDE_CALC_MEMBERS ) ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Siehe auch  
 [DrilldownLevel & #40; MDX & #41;](../mdx/drilldownlevel-mdx.md)   
 [MDX-Funktionsreferenz & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  

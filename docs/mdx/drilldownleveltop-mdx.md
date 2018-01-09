---
title: DrilldownLevelTop (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: DRILLDOWNLEVELTOP
dev_langs: kbMDX
helpviewer_keywords: DrilldownLevelTop function
ms.assetid: b3b45dd6-2ade-4dd7-83dd-849231e2e517
caps.latest.revision: "38"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: f4f3454f14371a7d75cf04f18ba69f11bce6d71f
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="drilldownleveltop-mdx"></a>DrilldownLevelTop (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Führt einen Drilldown der obersten Elemente einer Menge auf einer bestimmten Ebene in eine darunter liegende Ebene aus.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
DrilldownLevelTop(<Set_Expression>, <Count> [,[<Level_Expression>] [,[<Numeric_Expression>][,INCLUDE_CALC_MEMBERS]]])  
  
```  
  
## <a name="arguments"></a>Argumente  
 *Set_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Menge zurückgibt.  
  
 *Anzahl*  
 Ein gültiger numerischer Ausdruck, der die Anzahl der Tupel angibt, die zurückgegeben werden sollen.  
  
 *Level_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Ebene zurückgibt.  
  
 *Numeric_expression*  
 Ein gültiger numerischer Ausdruck, bei dem es sich in der Regel um einen MDX-Ausdruck (Multidimensional Expressions) für Zellenkoordinaten handelt, die eine Zahl zurückgeben.  
  
 *Include_Calc_Members*  
 Ein Schlüsselwort zum Hinzufügen berechneter Elemente zu Drilldown-Ergebnissen.  
  
## <a name="remarks"></a>Hinweise  
 Wenn ein numerischer Wert angegeben wird, sortiert die **DrilldownLevelTop** -Funktion die untergeordneten Elemente jedes Elements in der angegebenen Menge absteigend nach dem Wert des numerischen Ausdrucks, ausgewertet über der Menge der untergeordneten Elemente. Wenn kein numerischer Wert angegeben wird, sortiert die Funktion die untergeordneten Elemente jedes Elements in der angegebenen Menge absteigend nach den Werten der durch die Menge der untergeordneten Elemente dargestellten Zellen, bestimmt durch den Abfragekontext.  
  
 Nach dem Sortieren gibt die **DrilldownLevelTop** -Funktion eine Menge zurück, die die übergeordneten Elemente und die in *Count,* angegebene Anzahl der untergeordneten Elemente mit dem höchsten Wert enthält.  
  
 Die **DrilldownLevelTop** Funktion ist vergleichbar mit der [DrilldownLevel](../mdx/drilldownlevel-mdx.md) -Funktion, statt jedoch alle untergeordneten Elemente für jedes Element auf der angegebenen Ebene einzuschließen der **DrilldownLevelTop** Funktion gibt die Anzahl die oberste untergeordneten Elemente zurück.  
  
 Abfrage der XMLA-Eigenschaft MdpropMdxDrillFunctions können Sie den Grad der Unterstützung, die der Server die drillingfunktionen bereitgestellt; finden Sie unter [unterstützten XMLA-Eigenschaften &#40; XMLA &#41; ](../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md) für Details.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden die obersten drei untergeordneten Elemente der Product Category-Ebene basierend auf dem Standardmeasure zurückgegeben. Im Adventure Works-Beispielcube sind die obersten drei untergeordneten Elemente für Accessories Bike Racks, Bike Stands und Bottles and Cages. In Management Studio können Sie im MDX-Abfragefenster zu Products | Product Categories | Members | All Products | Accessories navigieren, um die vollständige Liste anzuzeigen. Sie können das Count-Argument erhöhen, damit mehr Elemente zurückgegeben werden.  
  
```  
SELECT DrilldownLevelTop   
   ([Product].[Product Categories].children,  
   3,  
   [Product].[Product Categories].[Category])  
   ON 0  
   FROM [Adventure Works]  
```  
  
 Im nächsten Beispiel wird die Verwendung des **include_calc_members** -Flags gezeigt. Dieses wird genutzt, um berechnete Elemente auf Drilldown-Ebene einzuschließen. Das Measure [Reseller Order Count] befindet sich in der **DrilldownLevelTop** -Anweisung, um sicherzustellen, dass die Rückgabewerte nach diesem Measure sortiert werden.  
  
```  
WITH MEMBER   
[Product].[Product Categories].[Category].&[3].[Premium Clothes] AS  
[Product].[Product Categories].[Subcategory].&[18] +  
[Product].[Product Categories].[Subcategory].&[21]  
SELECT [Measures].[Reseller Order Count] ON 0,  
DRILLDOWNLEVELTOP(  
  [Product].[Product Categories].children ,  
  2,  
  [Product].[Product Categories].[Category] ,  
  [Measures].[Reseller Order Count],  
  INCLUDE_CALC_MEMBERS ) ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Siehe auch  
 [DrilldownLevel &#40; MDX &#41;](../mdx/drilldownlevel-mdx.md)   
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

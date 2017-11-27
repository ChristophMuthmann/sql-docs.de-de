---
title: DrilldownMemberBottom (MDX) | Microsoft Docs
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
- DRILLDOWNMEMBERBOTTOM
dev_langs:
- kbMDX
helpviewer_keywords:
- DrilldownMemberBottom function
ms.assetid: 603927ba-68f6-4e7a-b17f-44cad33bdfb0
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: d66f9aeb97a5219f85a33acfedb710f980b63401
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="drilldownmemberbottom-mdx"></a>DrilldownMemberBottom (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Führt einen Drilldown bei Elementen in einer angegebenen Menge aus, die in einer angegebenen zweiten Menge vorhanden sind, wobei das Resultset auf eine angegebene Anzahl von Elementen beschränkt wird. Alternativ können Sie einen Drilldown diese Funktion auch für eine Menge von Tupeln mit der ersten tupelhierarchie oder der optional angegebenen Hierarchie.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
DrillDownMemberBottom(<Set_Expression1>, <Set_Expression2>, <Count> [,[<Numeric_Expresion>] [,[<Hierarchy>]] [,[RECURSIVE][,INCLUDE_CALC_MEMBERS]]])  
```  
  
## <a name="arguments"></a>Argumente  
 *Set_Expression1*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Menge zurückgibt.  
  
 *Set_Expression2*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Menge zurückgibt.  
  
 *Count*  
 Ein gültiger numerischer Ausdruck, der die Anzahl der Tupel angibt, die zurückgegeben werden sollen.  
  
 *Numeric_expression*  
 Ein gültiger numerischer Ausdruck, bei dem es sich in der Regel um einen MDX-Ausdruck (Multidimensional Expressions) für Zellenkoordinaten handelt, die eine Zahl zurückgeben.  
  
 *Hierarchie*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Hierarchie zurückgibt.  
  
 *Rekursive*  
 Ein Schlüsselwort, das einen rekursiven Vergleich von Mengen angibt.  
  
 *Include_Calc_Members*  
 Ein Schlüsselwort, durch das berechnete Elemente in Drilldownergebnisse eingeschlossen werden können.  
  
## <a name="remarks"></a>Hinweise  
 Wenn ein numerischer Ausdruck angegeben wird, die **DrilldownMemberBottom** Funktion sortiert in aufsteigender Reihenfolge der untergeordneten Elemente jedes Elements in der ersten Menge, gemäß dem Wert des numerischen Ausdrucks, ausgewertet über der Menge der untergeordneten Elemente. Wenn kein numerischer Wert angegeben wird, sortiert die Funktion die untergeordneten Elemente jedes Elements in der ersten Menge aufsteigend nach den Werten der durch die Menge der untergeordneten Elemente dargestellten Zellen, wie durch den Abfragekontext bestimmt. Dieses Verhalten ähnelt dem der BottomCount-Funktion und der Tail (MDX)-Funktion, die eine MEnge untergeordneter Elemente in natürlicher Reihenfolge ohne Sortierung zurückgeben.  
  
 Nach dem Sortieren der **DrilldownMemberBottom** -Funktion eine Menge, die die übergeordneten Elemente und die Anzahl der untergeordneten Elemente im angegebenen enthält zurück *Count* mit dem niedrigsten Wert beiden Mengen enthaltenen.  
  
 Wenn **REKURSIVE** angegeben wird, sortiert die Funktion die erste Menge wie oben beschrieben, und vergleicht dann rekursiv die Elemente der ersten Menge in einer Hierarchie mit der zweiten Menge organisiert. Die Funktion ruft die Anzahl der untersten untergeordneten Elemente für jedes Element in der ersten Menge ab, das auch in der zweiten vorhanden ist.  
  
 Die erste Menge kann auch Tupel anstelle von Elementen enthalten. Der Drilldown für Tupel ist eine Erweiterung von OLE DB und gibt eine Menge von Tupeln anstelle von Elementen zurück.  
  
 Die **DrilldownMemberBottom** Funktion ist vergleichbar mit der [DrilldownMember](../mdx/drilldownmember-mdx.md) funktionieren jedoch INSTEAD OF including alle untergeordneten Elemente für jedes Element in der ersten Menge, die auch ist vorhanden, in der zweiten Menge der **DrilldownMemberBottom** Funktion gibt die Anzahl die unterste untergeordneten Elemente für jedes Element zurück.  
  
 Abfrage der XMLA-Eigenschaft MdpropMdxDrillFunctions können Sie den Grad der Unterstützung, die der Server die drillingfunktionen bereitgestellt; finden Sie unter [unterstützten XMLA-Eigenschaften &#40; XMLA &#41; ](../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md) für Details.  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  


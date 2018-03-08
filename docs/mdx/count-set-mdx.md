---
title: Count (Menge) (MDX) | Microsoft Docs
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
f1_keywords: COUNT
dev_langs: kbMDX
helpviewer_keywords: Count function [MDX]
ms.assetid: 22f530e9-f8e1-4608-affa-9a2bc0821591
caps.latest.revision: "39"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 41d5ff72346e95985b19812f194d266e8d5db165
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="count-set-mdx"></a>Count (Menge) (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Gibt die Anzahl der Zellen in einer Menge zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Standard syntax  
Count(Set_Expression [ , ( EXCLUDEEMPTY | INCLUDEEMPTY ) ] )  
  
Alternate syntax  
Set_Expression.Count  
```  
  
## <a name="arguments"></a>Argumente  
 *Set_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Menge zurückgibt.  
  
## <a name="remarks"></a>Hinweise  
 Die **Count (Menge)** -Funktion ein- oder ausgeschlossen leere Zellen, je nach Syntax verwendet. Wenn die Standardsyntax verwendet wird, leere Zellen können aus- oder eingeschlossen werden mithilfe der **EXCLUDEEMPTY** oder **INCLUDEEMPTY** flags. Wird die alternative Syntax verwendet, schließt die Funktion leere Zellen immer ein.  
  
 Um leere Zellen in der Zählung einer Menge auszuschließen, verwenden Sie die Standardsyntax und dem optionalen **EXCLUDEEMPTY** Flag.  
  
> [!NOTE]  
>  Die **Count (Menge)** -Funktion zählt die leere Zellen in der Standardeinstellung. Im Gegensatz dazu die **Anzahl** -Funktion in OLE DB, die eine Menge zählt werden leere Zellen standardmäßig ausgeschlossen.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die Anzahl der Zellen in der Menge der Elemente bestimmt, die aus den untergeordneten Elementen der Model Name-Attributhierarchie in der Product-Dimension bestehen.  
  
```  
WITH MEMBER measures.X AS  
   [Product].[Model Name].children.count   
SELECT Measures.X ON 0  
FROM [Adventure Works]  
```  
  
 Im folgenden Beispiel wird die Anzahl der Produkte in der Product-Dimension mithilfe der **DrilldownLevel** -Funktion in Verbindung mit der **Anzahl** Funktion.  
  
```  
Count(DrilldownLevel (   
   [Product].[Product].[Product]))  
```  
  
 Das folgende Beispiel gibt die Wiederverkäufer mit zurückgegangene Umsätze im Vergleich zum vorherigen Kalenderquartal mithilfe der **Anzahl** -Funktion in Verbindung mit der **Filter** -Funktion und eine Reihe weiterer Funktionen. Diese Abfrage verwendet die **aggregieren** Funktion, um die Auswahl mehrerer Geography-Elemente, wie z. B. zur Auswahl von in einer Dropdown-Liste in einer Clientanwendung zu unterstützen.  
  
```  
WITH MEMBER Measures.[Declining Reseller Sales] AS  
   Count  
   (Filter  
      (Existing(Reseller.Reseller.Reseller),  
         [Measures].[Reseller Sales Amount]   
         < ([Measures].[Reseller Sales Amount],  
            [Date].Calendar.PrevMember)  
      )  
   )  
MEMBER [Geography].[State-Province].x AS   
   Aggregate  
   ( {[Geography].[State-Province].&[WA]&[US],   
      [Geography].[State-Province].&[OR]&[US] }   
   )  
SELECT NON EMPTY HIERARCHIZE   
   (AddCalculatedMembers   
      ({DrillDownLevel  
         ({[Product].[All Products]})  
      })  
   ) DIMENSION PROPERTIES PARENT_UNIQUE_NAME ON COLUMNS   
FROM [Adventure Works]  
WHERE ([Geography].[State-Province].x,  
   [Date].[Calendar].[Calendar Quarter].&[2003]&[4]  
   ,[Measures].[Declining Reseller Sales])  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Anzahl &#40; Dimension &#41; &#40; MDX &#41;](../mdx/count-dimension-mdx.md)   
 [Anzahl &#40; Hierarchieebenen &#41; &#40; MDX &#41;](../mdx/count-hierarchy-levels-mdx.md)   
 [Anzahl &#40; Tupel &#41; &#40; MDX &#41;](../mdx/count-tuple-mdx.md)   
 [DrilldownLevel &#40; MDX &#41;](../mdx/drilldownlevel-mdx.md)   
 [AddCalculatedMembers &#40; MDX &#41;](../mdx/addcalculatedmembers-mdx.md)   
 [HIERARCHIZE &#40; MDX &#41;](../mdx/hierarchize-mdx.md)   
 [Datenbankeigenschaften &#40; MDX &#41;](../mdx/properties-mdx.md)   
 [Aggregat &#40; MDX &#41;](../mdx/aggregate-mdx.md)   
 [Filters &#40; MDX &#41;](../mdx/filter-mdx.md)   
 [PrevMember &#40; MDX &#41;](../mdx/prevmember-mdx.md)   
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

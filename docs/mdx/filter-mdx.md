---
title: Filter (MDX) | Microsoft Docs
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
- filter
dev_langs:
- kbMDX
helpviewer_keywords:
- Filter function
ms.assetid: f2df51c8-6acb-4300-b71c-2a480c9fbdf8
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 729adc2230242798e67914907b6928ec7346b871
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="filter-mdx"></a>Filter (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Filtert eine angegebene Menge basierend auf einer Suchbedingung und gibt dann das Resultset zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Filter(Set_Expression, Logical_Expression )  
```  
  
## <a name="arguments"></a>Argumente  
 *Set_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Menge zurückgibt.  
  
 *Logical_Expression*  
 Ein gültiger logischer MDX-Ausdruck (Multidimensional Expressions), dessen Auswertung TRUE oder FALSE ergibt.  
  
## <a name="remarks"></a>Hinweise  
 Die **Filter** -Funktion wertet den angegebenen logischen Ausdruck für jedes Tupel in der angegebenen Menge. Die Funktion gibt einen Satz, der jedes Tupel in der angegebenen Menge besteht, in dem der logische Ausdruck wird zu **"true"**. Wenn kein Tupel ausgewertet **"true"**, wird eine leere Menge zurückgegeben.  
  
 Die **Filter** -Funktion arbeitet ähnlich wie mit der [IIf](../mdx/iif-mdx.md) Funktion. Die **IIf** Funktion gibt nur eine der beiden Optionen dagegen basierend auf der Auswertung eines logischen MDX-Ausdrucks, der **Filter** Funktion gibt eine Menge von Tupeln, die die angegebenen Suchbedingung zu erfüllen. Tatsächlich die **Filter** Funktion führt Folgendes aus `IIf(Logical_Expression, Set_Expression.Current, NULL)` für jedes Tupel in der Menge aus und gibt die sich ergebende Menge zurück.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die Filter-Funktion auf der ROWS-Achse einer Abfrage verwendet, um nur Datumsangaben zurückzugeben, bei denen Internet Sales Amount größer als 10.000 US-Dollar ist:  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `FILTER(`  
  
 `[Date].[Date].[Date].MEMBERS`  
  
 `,  [Measures].[Internet Sales Amount]>10000)`  
  
 `ON 1`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
 Die Filter-Funktion kann auch in berechneten Elementdefinitionen verwendet werden. Das folgende Beispiel gibt die Summe der `Measures.[Order Quantity]` Elements, aggregiert über die ersten neun Monate von 2003 in der `Date` Dimension, aus der **Adventure Works** Cube. Die **PeriodsToDate** -Funktion definiert die Tupel in der Menge an, über den die **aggregieren** -Funktion arbeitet. Die **Filter** -Funktion beschränkt die zurückgegebenen Tupel auf Abonnements mit niedrigeren Werten für das Reseller Sales Amount-Measure für den vorherigen Zeitraum aufweisen.  
  
```  
WITH MEMBER Measures.[Declining Reseller Sales] AS Count  
   (Filter  
      (Existing  
         (Reseller.Reseller.Reseller),   
            [Measures].[Reseller Sales Amount] <   
               ([Measures].[Reseller Sales Amount],[Date].Calendar.PrevMember)  
        )  
    )  
MEMBER [Geography].[State-Province].x AS Aggregate   
( {[Geography].[State-Province].&[WA]&[US],   
   [Geography].[State-Province].&[OR]&[US] }   
)  
SELECT NON EMPTY HIERARCHIZE   
   (AddCalculatedMembers   
      ({DrillDownLevel  
         ({[Product].[All Products]})}  
        )  
    ) DIMENSION PROPERTIES PARENT_UNIQUE_NAME ON COLUMNS   
FROM [Adventure Works]  
WHERE ([Geography].[State-Province].x,   
   [Date].[Calendar].[Calendar Quarter].&[2003]&[4],  
   [Measures].[Declining Reseller Sales])  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

---
title: "EXISTING-Schlüsselwort (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: EXISTING
helpviewer_keywords: Existing keyword
ms.assetid: 651ee9ac-04ef-4316-87c9-a3df5ac27d22
caps.latest.revision: "38"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: c3a9ebbb73e8bf2b305a7ab2730439ffd0d53f8f
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="mdx-query---existing-keyword"></a>MDX-Abfrage - EXISTING-Schlüsselwort
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Erzwingt, dass einer angegebenen Menge im aktuellen Kontext ausgewertet werden.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Existing Set_Expression  
```  
  
## <a name="arguments"></a>Argumente  
 *Set_Expression*  
 Ein gültiger MDX-Mengenausdruck (Multidimensional Expressions).  
  
## <a name="remarks"></a>Hinweise  
 Standardmäßig werden Mengen im Kontext des Cubes ausgewertet, der die Elemente der Menge enthält. Das **Existing** -Schlüsselwort erzwingt dagegen die Auswertung einer angegebenen Menge im aktuellen Kontext.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird die Anzahl der Wiederverkäufer, deren Umsätze im vergangenen Zeitraum zurückgegangen sind, basierend auf vom Benutzer ausgewählten „State-Province“-Elementwerten zurückgegeben, die mit der **Aggregate** -Funktion ausgewertet wurden. Das [Hierarchize &#40;MDX&#41;](../../../mdx/hierarchize-mdx.md) und [DrilldownLevel (MDX)](../../../mdx/drilldownlevel-mdx.md) werden zum Zurückgeben von Werten für zurückgegangene Umsätze in Produktkategorien der Product-Dimension verwendet. Das **Existing** -Schlüsselwort erzwingt die Auswertung des Satzes der **Filter** -Funktion im aktuellen Kontext, d.h. für die Elemente „Washington“ und „Oregon“ der State-Province-Attributhierarchie.  
  
```  
WITH MEMBER Measures.[Declining Reseller Sales] AS  
   Count  
      (Filter  
         (Existing  
            (Reseller.Reseller.Reseller)  
         , [Measures].[Reseller Sales Amount] <   
            ([Measures].[Reseller Sales Amount]  
               ,[Date].Calendar.PrevMember  
            )  
        )  
      )  
MEMBER [Geography].[State-Province].x AS   
   Aggregate   
      ( {[Geography].[State-Province].&[WA]&[US]  
         , [Geography].[State-Province].&[OR]&[US] }   
      )  
SELECT NON EMPTY HIERARCHIZE   
      (AddCalculatedMembers   
         (   
            {DrillDownLevel  
               ({[Product].[All Products]}  
               )  
            }   
         )   
      ) DIMENSION PROPERTIES PARENT_UNIQUE_NAME ON COLUMNS   
FROM [Adventure Works]  
WHERE   
      ( [Geography].[State-Province].x  
        , [Date].[Calendar].[Calendar Quarter].&[2003]&[4]  
        ,[Measures].[Declining Reseller Sales]  
      )  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Count &#40;Menge&#41; &#40;MDX&#41;](../../../mdx/count-set-mdx.md)   
 [AddCalculatedMembers &#40; MDX &#41;](../../../mdx/addcalculatedmembers-mdx.md)   
 [Aggregat &#40; MDX &#41;](../../../mdx/aggregate-mdx.md)   
 [Filters &#40; MDX &#41;](../../../mdx/filter-mdx.md)   
 [Datenbankeigenschaften &#40; MDX &#41;](../../../mdx/properties-mdx.md)   
 [DrilldownLevel &#40; MDX &#41;](../../../mdx/drilldownlevel-mdx.md)   
 [HIERARCHIZE &#40; MDX &#41;](../../../mdx/hierarchize-mdx.md)   
 [MDX-Funktionsreferenz &#40; MDX &#41;](../../../mdx/mdx-function-reference-mdx.md)  
  
  

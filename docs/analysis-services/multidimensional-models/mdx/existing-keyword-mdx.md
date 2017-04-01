---
title: "EXISTING-Schl&#252;sselwort (MDX) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "EXISTING"
helpviewer_keywords: 
  - "Exsiting-Schlüsselwort"
ms.assetid: 651ee9ac-04ef-4316-87c9-a3df5ac27d22
caps.latest.revision: 38
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# EXISTING-Schl&#252;sselwort (MDX)
  Erzwingt die Auswertung einer angegebenen Menge im aktuellen Kontext.  
  
## Syntax  
  
```  
  
Existing Set_Expression  
```  
  
## Argumente  
 *Set_Expression*  
 Ein gültiger MDX-Mengenausdruck (Multidimensional Expressions).  
  
## Hinweise  
 Standardmäßig werden Mengen im Kontext des Cubes ausgewertet, der die Elemente der Menge enthält. Das **Existing** -Schlüsselwort erzwingt dagegen die Auswertung einer angegebenen Menge im aktuellen Kontext.  
  
## Beispiel  
 Im folgenden Beispiel wird die Anzahl der Wiederverkäufer, deren Umsätze im vergangenen Zeitraum zurückgegangen sind, basierend auf vom Benutzer ausgewählten „State-Province“-Elementwerten zurückgegeben, die mit der **Aggregate**-Funktion ausgewertet wurden. Die Funktionen [Hierarchize &#40;MDX&#41;](../../../mdx/hierarchize-mdx.md) und [DrilldownLevel (MDX)](../../../mdx/drilldownlevel-mdx.md) werden zum Zurückgeben von Werten für zurückgegangene Umsätze in Produktkategorien der Product-Dimension verwendet. Das **Existing**-Schlüsselwort erzwingt die Auswertung des Satzes der **Filter**-Funktion im aktuellen Kontext, d.h. für die Elemente „Washington“ und „Oregon“ der State-Province-Attributhierarchie.  
  
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
  
## Siehe auch  
 [Count &#40;Menge&#41; &#40;MDX&#41;](../../../mdx/count-set-mdx.md)   
 [AddCalculatedMembers &#40;MDX&#41;](../../../mdx/addcalculatedmembers-mdx.md)   
 [Aggregate &#40;MDX&#41;](../../../mdx/aggregate-mdx.md)   
 [Filter &#40;MDX&#41;](../../../mdx/filter-mdx.md)   
 [Properties &#40;MDX&#41;](../../../mdx/properties-mdx.md)   
 [DrilldownLevel &#40;MDX&#41;](../../../mdx/drilldownlevel-mdx.md)   
 [Hierarchize &#40;MDX&#41;](../../../mdx/hierarchize-mdx.md)   
 [MDX-Funktionsreferenz &#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md)  
  
  
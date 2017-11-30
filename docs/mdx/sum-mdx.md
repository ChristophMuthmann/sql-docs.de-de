---
title: SUM (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: SUM
dev_langs: kbMDX
helpviewer_keywords: Sum function [MDX]
ms.assetid: 6c3db1e3-2c02-49f2-a0bf-cab0fb78c622
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: c6b8c218e6c4c4d8c5981afdf24b61a0b066ae10
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="sum-mdx"></a>Sum (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Gibt die Summe eines numerischen Ausdrucks, ausgewertet über einer angegebenen Menge zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Sum( Set_Expression [ , Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *Set_Expression*  
 Ein gültiger MDX-Mengenausdruck (Multidimensional Expressions).  
  
 *Numeric_expression*  
 Ein gültiger numerischer Ausdruck, bei dem es sich in der Regel um einen MDX-Ausdruck (Multidimensional Expressions) für Zellenkoordinaten handelt, die eine Zahl zurückgeben.  
  
## <a name="remarks"></a>Hinweise  
 Wenn ein numerischer Ausdruck angegeben ist, wird der angegebene numerische Ausdruck über die Menge ausgewertet und anschließend die Summe gebildet. Wenn kein numerischer Ausdruck angegeben ist, wird die angegebene Menge im aktuellen Kontext der Elemente der Menge ausgewertet und anschließend die Summe gebildet. Wenn die SUM-Funktion auf einen nicht numerischen Ausdruck angewendet wird, sind die Ergebnisse nicht definiert.  
  
> [!NOTE]  
>  Analysis Services ignoriert Nullen, wenn die Summe einer Menge von Zahlen berechnet wird.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die Summe von Reseller Sales Amounts für alle Elemente der Product.Category-Attributhierarchie für die Kalenderjahre 2001 und 2002 zurückgegeben.  
  
```  
WITH MEMBER Measures.x AS SUM  
   ( { [Date].[Calendar Year].&[2001]  
         , [Date].[Calendar Year].&[2002] }  
      , [Measures].[Reseller Sales Amount]  
    )  
SELECT Measures.x ON 0  
,[Product].[Category].Members ON 1  
FROM [Adventure Works]  
```  
  
 Im folgenden Beispiel wird die Summe der Monat-bis-Datum-Frachtkosten für Internetverkäufe für den Monat Juli 2002 bis einschließlich 20. Juli zurückgegeben.  
  
```  
WITH MEMBER Measures.x AS SUM   
   (  
      MTD([Date].[Calendar].[Date].[July 20, 2002])  
     , [Measures].[Internet Freight Cost]  
     )  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
 Im folgenden Beispiel wird das WITH MEMBER-Schlüsselwort und die **Summe** Funktion, um ein berechnetes Element in der Measures-Dimension definieren, die die Summe des Reseller Sales Amount-Measures für die Elemente Canada und United States der Country-Attributhierarchie in der Geography-Dimension enthält.  
  
```  
WITH MEMBER Measures.NorthAmerica AS SUM   
      (  
         {[Geography].[Country].&[Canada]  
            , [Geography].[Country].&[United States]}  
       ,[Measures].[Reseller Sales Amount]  
      )  
SELECT {[Measures].[NorthAmerica]} ON 0,  
[Product].[Category].members ON 1  
FROM [Adventure Works]  
```  
  
 Häufig die **Summe** Funktion wird verwendet, mit der **CURRENTMEMBER** Funktion oder Funktionen, wie etwa **YTD** , die eine Gruppe, die der von CurrentMember einer Hierarchie variiert zurückgeben. Die folgende Abfrage gibt z. B. die Summe der Internet Sales Amount-Measure für alle Datumsangaben ab Beginn des Kalenderjahrs bis zu dem Datum an, das auf der Zeilenachse angezeigt wird:  
  
 `WITH MEMBER MEASURES.YTDSUM AS`  
  
 `SUM(YTD(), [Measures].[Internet Sales Amount])`  
  
 `SELECT {[Measures].[Internet Sales Amount], MEASURES.YTDSUM} ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

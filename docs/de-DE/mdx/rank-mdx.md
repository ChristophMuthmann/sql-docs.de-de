---
title: Rang (MDX) | Microsoft Docs
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
- RANK
dev_langs:
- kbMDX
helpviewer_keywords:
- Rank function [MDX]
ms.assetid: 3cea35ed-57c4-4b47-a736-cee00275509b
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: b8b428d2d6ca2f19102514876d9bcea22fb029f0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="rank-mdx"></a>Rank (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Gibt den einsbasierten Rang eines angegebenen Tupels in einer angegebenen Menge zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Rank(Tuple_Expression, Set_Expression [ ,Numeric Expression ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *Tuple_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der ein Tupel zurückgibt.  
  
 *Set_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Menge zurückgibt.  
  
 *Numeric_expression*  
 Ein gültiger numerischer Ausdruck, bei dem es sich in der Regel um einen MDX-Ausdruck (Multidimensional Expressions) für Zellenkoordinaten handelt, die eine Zahl zurückgeben.  
  
## <a name="remarks"></a>Hinweise  
 Wenn ein numerischer Ausdruck angegeben wird, die **Rang** -Funktion bestimmt den einsbasierten Rang für das angegebene Tupel durch das Auswerten des angegebenen numerischen Ausdrucks für das Tupel. Wenn ein numerischer Ausdruck angegeben wird, die **Rang** -Funktion Tupeln mit doppelten Werten in der Menge denselben Rang zugewiesen. Die Zuweisung desselben Ranges an doppelte Werte wirkt sich auf die Rangwerte nachfolgender Tupel in der Menge aus. Eine Menge besteht beispielsweise aus folgenden Tupeln: `{(a,b), (e,f), (c,d)}`. Das Tupel `(a,b)` weist denselben Wert auf wie das Tupel `(c,d)`. Wenn das Tupel `(a,b)` den Rang "1" aufweist, liegt für `(a,b)` und `(c,d)` der Rang "1" vor. Das Tupel `(e,f)` verfügt jedoch über den Rang "3". In diesem Satz kann kein Tupel mit dem Rang "2" vorhanden sein.  
  
 Wenn ein numerischer Ausdruck nicht angegeben wird, die **Rang** Funktion gibt die einsbasierte Ordnungsposition des angegebenen Tupels zurück.  
  
 Die **Rang** -Funktion sortiert die Menge nicht.  
  
## <a name="example"></a>Beispiel  
 Im folgende Beispiel gibt die Menge von Tupeln, die mit Kunden- und Kaufdaten, mithilfe der **Filter**, **NonEmpty**, **Element**, und **Rang** Funktionen, um das letzte Datum gefunden werden, dass jeder Kunde einen Kauf vorgenommen.  
  
```  
WITH SET MYROWS AS FILTER  
   (NONEMPTY  
      ([Customer].[Customer Geography].MEMBERS  
         * [Date].[Date].[Date].MEMBERS  
         , [Measures].[Internet Sales Amount]  
      ) AS MYSET  
   , NOT(MYSET.CURRENT.ITEM(0)  
      IS MYSET.ITEM(RANK(MYSET.CURRENT, MYSET)).ITEM(0))  
   )  
SELECT [Measures].[Internet Sales Amount] ON 0,  
MYROWS ON 1  
FROM [Adventure Works]  
```  
  
 Im folgenden Beispiel wird die **Reihenfolge** -Funktion, statt über das **Rang** -Funktion verwendet, um die Elemente der City-Hierarchie rank basierend auf dem Reseller Sales Amount-Measure, und klicken Sie dann in der Rangreihenfolge angezeigt. Mithilfe der **Reihenfolge** -Funktion zum vorsortieren der Menge der Elemente der City-Hierarchie, die Sortierung nur einmal ausgeführt und anschließend ein linearer Scan, bevor angezeigt wird, der Sortierreihenfolge.  
  
```  
WITH   
SET OrderedCities AS Order  
   ([Geography].[City].[City].members  
   , [Measures].[Reseller Sales Amount], BDESC  
   )  
MEMBER [Measures].[City Rank] AS Rank  
   ([Geography].[City].CurrentMember, OrderedCities)  
SELECT {[Measures].[City Rank],[Measures].[Reseller Sales Amount]}  ON 0   
,Order  
   ([Geography].[City].[City].MEMBERS  
   ,[City Rank], ASC)  
    ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Reihenfolge &#40;MDX&#41;](../mdx/order-mdx.md)   
 [MDX-Funktionsreferenz & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  

---
title: BottomCount-Funktion (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: BOTTOMCOUNT
dev_langs: kbMDX
helpviewer_keywords: BottomCount function
ms.assetid: 1441dab3-7885-4e92-9d48-21d832286677
caps.latest.revision: "39"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: bf3eb5bebe5c282dd32298665b3f5888ae1dc227
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="bottomcount-mdx"></a>BottomCount (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Sortiert eine Menge in aufsteigender Reihenfolge und gibt die angegebene Anzahl von Tupeln in der angegebenen Menge mit den niedrigsten Werten zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
BottomCount(Set_Expression, Count [,Numeric_Expression])  
```  
  
## <a name="arguments"></a>Argumente  
 *Set_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Menge zurückgibt.  
  
 *Anzahl*  
 Ein gültiger numerischer Ausdruck, der die Anzahl der Tupel angibt, die zurückgegeben werden sollen.  
  
 *Numeric_expression*  
 Ein gültiger numerischer Ausdruck, bei dem es sich in der Regel um einen MDX-Ausdruck (Multidimensional Expressions) für Zellenkoordinaten handelt, die eine Zahl zurückgeben.  
  
## <a name="remarks"></a>Hinweise  
 Wenn ein numerischer Ausdruck angegeben wird, sortiert die Funktion die Tupel in der angegebenen Menge nach dem Wert des angegebenen Ausdrucks, ausgewertet über die Menge, in aufsteigender Reihenfolge. Die **BottomCount** Funktion gibt dann die angegebene Anzahl von Tupeln mit dem niedrigsten Wert zurück.  
  
> [!IMPORTANT]  
>  Die **BottomCount** Funktion, wie auch die [TopCount](../mdx/topcount-mdx.md) funktionieren, unterbricht immer die Hierarchie.  
  
 Wenn ein numerischer Wert nicht angegeben ist, die Funktion gibt die Menge der Elemente in natürlicher Reihenfolge ohne Sortierung, verhält sich wie die [Tail (MDX)](../mdx/tail-mdx.md) Funktion.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird das Reseller Order Quantity-Measure für jedes Kalenderjahr für die fünf geringsten Product SubCategory-Umsätze in der vom Reseller Sales Amount-Measure vorgegebenen Reihenfolge zurückgegeben.  
  
```  
SELECT BottomCount([Product].[Product Categories].[Subcategory].Members  
   , 10  
   , [Measures].[Reseller Sales Amount]) ON 0,  
   [Date].[Calendar].[Calendar Year].Members ON 1  
  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Reseller Order Quantity]  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

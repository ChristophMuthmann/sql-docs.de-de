---
title: TopSum (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- TOPSUM
dev_langs:
- kbMDX
helpviewer_keywords:
- TopSum function
ms.assetid: e32496fd-4897-43c9-a388-4028609f4ffb
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 58a7bffc672af75c52eacca28f2e83d36a56af0c
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="topsum-mdx"></a>TopSum (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Sortiert eine Menge und gibt die obersten Elemente zurück, deren kumulative Summe mindestens einem angegebenen Wert entspricht.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
TopSum(Set_Expression, Value, Numeric_Expression)   
```  
  
## <a name="arguments"></a>Argumente  
 *Set_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Menge zurückgibt.  
  
 *Wert*  
 Ein gültiger numerischer Ausdruck, der den Wert angibt, mit dem die Tupel verglichen werden.  
  
 *Numeric_expression*  
 Ein gültiger numerischer Ausdruck, bei dem es sich in der Regel um einen MDX-Ausdruck (Multidimensional Expressions) handelt, der ein Measure zurückgibt.  
  
## <a name="remarks"></a>Hinweise  
 Die **TopSum** -Funktion berechnet die Summe des angegebenen Measures, ausgewertet über einer angegebenen Menge, die Menge in absteigender Reihenfolge sortiert. Anschließend gibt die Funktion die Elemente mit den höchsten Werten zurück, deren Gesamtwert des angegebenen numerischen Ausdrucks mindestens dem angegebenen Wert entspricht. Diese Funktion gibt die kleinste Teilmenge einer Menge zurück, deren kumulativer Gesamtwert mindestens dem angegebenen Wert entspricht. Die zurückgegebenen Elemente werden der Größe nach absteigend sortiert.  
  
> [!IMPORTANT]  
>  Wie die [BottomSum](../mdx/bottomsum-mdx.md) -Funktion, die **TopSum** Funktion immer die Hierarchie unterbrochen.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird für die Bike-Kategorie die kleinste Menge der Elemente der City-Ebene in der Geography-Hierarchie in der Geography-Dimension zurückgegeben, deren kumulativer Gesamtwert bezüglich des Reseller Sales Amount-Measures mindestens einer Summe von 6.000.000 (beginnend mit den Elementen dieser Menge, die den höchsten Umsatz aufweisen) entspricht.  
  
```  
SELECT [Measures].[Reseller Sales Amount] ON 0,  
TopSum  
   ({[Geography].[Geography].[City].Members}  
   , 6000000  
   , [Measures].[Reseller Sales Amount]  
   ) ON 1  
FROM [Adventure Works]  
WHERE([Product].[Product Categories].Bikes)  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  


---
title: BottomPercent (MDX) | Microsoft Docs
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
f1_keywords: BOTTOMPERCENT
dev_langs: kbMDX
helpviewer_keywords: BottomPercent function
ms.assetid: c04866e6-e6dd-4ed1-ae79-c718c194930c
caps.latest.revision: "39"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 3e188299440d09a941d82981b8a77bbf2d94bde1
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="bottompercent-mdx"></a>BottomPercent (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Sortiert eine Menge in aufsteigender Reihenfolge und gibt eine Menge von Tupeln mit den niedrigsten Werten zurück, deren kumulativer Gesamtwert größer oder gleich einem angegebenen Prozentsatz ist.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
BottomPercent(Set_Expression, Percentage, Numeric_Expression)   
```  
  
## <a name="arguments"></a>Argumente  
 *Set_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Menge zurückgibt.  
  
 *Prozentsatz*  
 Ein gültiger numerischer Ausdruck, der den Prozentsatz der zurückzugebenden Tupel angibt.  
  
 *Numeric_expression*  
 Ein gültiger numerischer Ausdruck, bei dem es sich in der Regel um einen MDX-Ausdruck (Multidimensional Expressions) für Zellenkoordinaten handelt, die eine Zahl zurückgeben.  
  
## <a name="remarks"></a>Hinweise  
 Die **BottomPercent** -Funktion berechnet die Summe der angegebenen numerischen Ausdrucks, ausgewertet über einer angegebenen Menge, die Menge in aufsteigender Reihenfolge sortiert. Anschließend gibt die Funktion die Elemente mit den niedrigsten Werten zurück, deren kumulativer Prozentsatz des Gesamtwertes mindestens dem angegebenen Prozentsatz entspricht. Diese Funktion gibt die kleinste Teilmenge einer Menge zurück, deren kumulativer Gesamtwert mindestens dem angegebenen Prozentsatz entspricht. Die zurückgegebenen Elemente werden der Größe nach absteigend sortiert.  
  
> [!IMPORTANT]  
>  Die **BottomPercent** Funktion, wie auch die [TopPercent](../mdx/toppercent-mdx.md) funktionieren, unterbricht immer die Hierarchie. Weitere Informationen finden Sie unter Order-Funktion.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird für die Bike-Kategorie die kleinste Menge der Elemente der City-Ebene in der Geography-Hierarchie in der Geography-Dimension für das Geschäftsjahr 2003 zurückgegeben, deren kumulativer Gesamtwert bezüglich des Reseller Sales Amount-Measures mindestens 15 % des kumulativen Gesamtwertes (beginnend mit den Elementen dieser Menge, die den geringsten Umsatz aufweisen) beträgt.  
  
```  
SELECT  
[Product].[Product Categories].Bikes ON 0,  
BottomPercent  
   ({[Geography].[Geography].[City].Members}  
   , 15  
   , ([Measures].[Reseller Sales Amount],[Product].[Product Categories].Bikes)  
   ) ON 1  
FROM [Adventure Works]  
WHERE ([Measures].[Reseller Sales Amount],[Date].[Fiscal].[Fiscal Year].[FY 2003])  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

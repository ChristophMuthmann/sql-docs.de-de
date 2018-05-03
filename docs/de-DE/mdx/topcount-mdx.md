---
title: TopCount (MDX) | Microsoft Docs
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
- TOPCOUNT
dev_langs:
- kbMDX
helpviewer_keywords:
- TopCount function
ms.assetid: 15026a8f-35c5-4307-8856-348f5c44bfd5
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 72dfbc5439e4df6e17f42f28589f966f6aec47f1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="topcount-mdx"></a>TopCount (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Sortiert eine Menge in absteigender Reihenfolge und gibt die angegebene Anzahl von Elementen mit den höchsten Werten zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
TopCount(Set_Expression,Count [ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *Set_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Menge zurückgibt.  
  
 *Count*  
 Ein gültiger numerischer Ausdruck, der die Anzahl der Tupel angibt, die zurückgegeben werden sollen.  
  
 *Numeric_expression*  
 Ein gültiger numerischer Ausdruck, bei dem es sich in der Regel um einen MDX-Ausdruck (Multidimensional Expressions) für Zellenkoordinaten handelt, die eine Zahl zurückgeben.  
  
## <a name="remarks"></a>Hinweise  
 Wenn ein numerischer Ausdruck angegeben wird, die **TopCount** Funktion sortiert in absteigender Reihenfolge der Tupel in der Menge, die von der angegebenen Menge nach dem Wert, der angegebenen numerischen Ausdrucks angegeben wird, über die angegebene Menge ausgewertet. Nach dem Sortieren der Menge der **TopCount** Funktion gibt dann die angegebene Anzahl von Tupeln mit dem höchsten Wert zurück.  
  
> [!IMPORTANT]  
>  Wie die [BottomCount](../mdx/bottomcount-mdx.md) -Funktion, die **TopCount** Funktion immer die Hierarchie unterbrochen.  
  
 Wenn ein numerischer Wert nicht angegeben ist, die Funktion gibt die Menge der Elemente in natürlicher Reihenfolge ohne Sortierung, verhält sich wie die [Head (MDX)](../mdx/head-mdx.md) Funktion.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel gibt die ersten 10 Daten nach Internetverkaufsbetrag zurück:  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `TOPCOUNT([Date].[Date].[Date].MEMBERS, 10, [Measures].[Internet Sales Amount])`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 Im folgenden Beispiel werden für die Bike-Kategorie die ersten fünf Elemente in der Menge der Elemente zurückgegeben, die alle Kombinationen von Elementen der City-Ebene in der Geography-Hierarchie in der Geography-Dimension sowie alle Geschäftsjahre aus der Fiscal-Hierarchie der Date-Dimension enthält, geordnet nach dem Reseller Sales Amount-Measure (beginnend mit den Elementen dieser Menge, die den höchsten Umsatz aufweisen).  
  
```  
SELECT [Measures].[Reseller Sales Amount] ON 0,  
TopCount  
   ({[Geography].[Geography].[City].Members   
      *[Date].[Fiscal].[Fiscal Year].Members}  
   , 5  
   , [Measures].[Reseller Sales Amount]  
   ) ON 1  
FROM [Adventure Works]  
WHERE([Product].[Product Categories].Bikes)  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  

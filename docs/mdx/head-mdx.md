---
title: Head (MDX) | Microsoft Docs
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
- HEAD
dev_langs:
- kbMDX
helpviewer_keywords:
- Head function
ms.assetid: 2a909bda-1366-4537-93b0-c089554fc11f
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 5529333ef2e81b8fee7d78765e0fb528ecb02577
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="head-mdx"></a>Head (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Gibt die erste angegebene Anzahl von Elementen aus einer Menge zurück, wobei doppelte Werte beibehalten werden.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Head(Set_Expression [ ,Count ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *Set_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Menge zurückgibt.  
  
 *Count*  
 Ein gültiger numerischer Ausdruck, der die Anzahl der Tupel angibt, die zurückgegeben werden sollen.  
  
## <a name="remarks"></a>Hinweise  
 Die **Head** Funktion gibt die angegebene Anzahl von Tupeln vom Anfang der angegebenen Menge zurück. Die Reihenfolge der Elemente wird beibehalten. Der Standardwert für Count ist 1. Wenn die angegebene Anzahl der Tupel kleiner als 1 ist, ist die **Head** Funktion eine leere Menge zurückgibt. Wenn die angegebene Anzahl der Tupel größer ist als die Anzahl der Tupel in der Menge, gibt die Funktion die ursprüngliche Menge zurück.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel werden die fünf bestverkauften Produktunterkategorien unabhängig von der Hierarchie basierend auf Reseller Gross Profit zurückgegeben. Die **Head** Funktion wird verwendet, um nur die ersten 5 Mengen aus dem Ergebnis zurückzugeben, nach dem Sortieren des Ergebnisses mithilfe der **Reihenfolge** Funktion.  
  
```  
SELECT   
[Measures].[Reseller Gross Profit] ON 0,  
Head  
   (Order   
      ([Product].[Product Categories].[SubCategory].members  
         ,[Measures].[Reseller Gross Profit]  
         ,BDESC  
      )  
   ,5  
   ) ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Tail &#40;MDX&#41;](../mdx/tail-mdx.md)   
 [Element &#40;Tupel&#41; &#40;MDX&#41;](../mdx/item-tuple-mdx.md)   
 [Element &#40;Member&#41; &#40;MDX&#41;](../mdx/item-member-mdx.md)   
 [Rang &#40;MDX&#41;](../mdx/rank-mdx.md)   
 [MDX-Funktionsreferenz & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  

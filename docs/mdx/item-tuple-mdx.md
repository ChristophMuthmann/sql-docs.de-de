---
title: Item (Tupel) (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ITEM
dev_langs:
- kbMDX
helpviewer_keywords:
- Item function
ms.assetid: 9ee7af55-d5b5-47c8-a480-ef23878306af
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 6e9411f3e4404a29ff0908ff53b0e0fb443b1703
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="item-tuple-mdx"></a>Item (Tupel) (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Gibt ein Tupel aus einer Menge zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Index syntax  
Set_Expression.Item(Index)  
  
String expression syntax  
Set_Expression.Item(String_Expression1 [ ,String_Expression2,...n])  
```  
  
## <a name="arguments"></a>Argumente  
 *Set_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Menge zurückgibt.  
  
 *String_Expression1*  
 Ein gültiger Zeichenfolgenausdruck, bei dem es sich normalerweise um ein als Zeichenfolge ausgedrücktes Tupel handelt.  
  
 *String_Expression2*  
 Ein gültiger Zeichenfolgenausdruck, bei dem es sich normalerweise um ein als Zeichenfolge ausgedrücktes Tupel handelt.  
  
 *Index*  
 Ein gültiger numerischer Ausdruck, der ein bestimmtes Tupel über die Position in der zurückzugebenden Menge angibt.  
  
## <a name="remarks"></a>Hinweise  
 Die **Element** -Funktion ein Tupel aus der angegebenen Menge zurück. Es gibt drei Möglichkeiten zum Aufrufen der **Element** Funktion:  
  
-   Wenn ein einzelner Zeichenfolgenausdruck angegeben wird, die **Element** Funktion das angegebene Tupel zurück. Beispiel: "([2005].Q3, [Store05])".  
  
-   Wenn mehr als ein Zeichenfolgenausdruck angegeben wird, die **Element** Funktion gibt die durch die angegebenen Koordinaten definierte Tupel zurück. Die Anzahl der Zeichenfolgen muss der Anzahl der Achsen entsprechen, und jede Zeichenfolge muss eine eindeutige Hierarchie identifizieren. Beispiel: "[2005].Q3", "[Store05]".  
  
-   Wenn eine ganze Zahl angegeben wird, die **Element** -Funktion das Tupel zurück, die in der vom angegebenen nullbasierten Position *Index*.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird ([1996],Sales) zurückgegeben:  
  
 `{([1996],Sales), ([1997],Sales), ([1998],Sales)}.Item(0)`  
  
 Im folgenden Beispiel wird ein Ebenenausdruck verwendet und Internet Sales Amount für alle Bundesstaaten in Australien sowie deren prozentualer Anteil an der Summe von Internet Sales Amount für Australien zurückgegeben. In diesem Beispiel verwendet die Item-Funktion, um das erste (und nur Tupel) aus dem Satz zurückgegebenes Extrahieren der **Vorgänger** Funktion.  
  
```  
WITH MEMBER Measures.x AS [Measures].[Internet Sales Amount] /   
   ( [Measures].[Internet Sales Amount],    
      Ancestors   
      ( [Customer].[Customer Geography].CurrentMember,  
        [Customer].[Customer Geography].[Country]  
      ).Item (0)  
   ), FORMAT_STRING = '0%'  
SELECT {[Measures].[Internet Sales Amount], Measures.x} ON 0,  
{ Descendants   
   ( [Customer].[Customer Geography].[Country].&[Australia],  
     [Customer].[Customer Geography].[State-Province], SELF   
   )   
} ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  


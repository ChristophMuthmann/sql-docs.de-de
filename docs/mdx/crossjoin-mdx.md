---
title: Crossjoin (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: CROSSJOIN
dev_langs: kbMDX
helpviewer_keywords: Crossjoin function
ms.assetid: 503b8376-d244-4855-8f44-a749764162e4
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 24eb58744008984fca4dab647b12226769f4ab81
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="crossjoin-mdx"></a>Crossjoin (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Gibt das Kreuzprodukt mindestens einer Menge zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Standard syntax  
Crossjoin(Set_Expression1 ,Set_Expression2 [,...n] )  
  
Alternate syntax  
Set_Expression1 * Set_Expression2 [* ...n]  
```  
  
## <a name="arguments"></a>Argumente  
 *Set_Expression1*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Menge zurückgibt.  
  
 *Set_Expression2*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Menge zurückgibt.  
  
## <a name="remarks"></a>Hinweise  
 Die **Crossjoin** Funktion gibt das Kreuzprodukt von zwei oder mehr angegebenen Mengen. Die Reihenfolge der Tupel in der sich ergebenden Menge hängt von der Reihenfolge der zu verknüpfenden Mengen und von der Reihenfolge ihrer Elemente ab. Angenommen, wenn die erste Menge besteht aus {X1, X2,..., x*n*}, und die zweite Gruppe besteht aus {y1, y2,..., y*n*}, ist das Kreuzprodukt dieser Sätze:  
  
 {(x1, y1), (x1, y2),...,(x1, y*n*), (x2, y1), (x2, y2),...,  
  
 (x2, y*n*),..., (x*n*, y1), (x*n*, y2),..., (xn, y*n*)}  
  
> [!IMPORTANT]  
>  Wenn die Mengen im Cross Join aus Tupeln unterschiedlicher Attributhierarchien der gleichen Dimension bestehen, gibt die Funktion nur die Tupel zurück, die tatsächlich vorhanden sind. Weitere Informationen finden Sie unter [Schlüsselkonzepte in MDX &#40; Analysis Services &#41; ](../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md).  
  
## <a name="examples"></a>Beispiele  
 Die folgende Abfrage enthält einfache Beispiele für die Verwendung der Crossjoin-Funktion auf der COLUMNS- und der ROWS-Achse einer Abfrage:  
  
 `SELECT`  
  
 `[Customer].[Country].Members *`  
  
 `[Customer].[State-Province].Members`  
  
 `ON 0,`  
  
 `Crossjoin(`  
  
 `[Date].[Calendar Year].Members,`  
  
 `[Product].[Category].[Category].Members)`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 `WHERE Measures.[Internet Sales Amount]`  
  
 Das folgende Beispiel veranschaulicht das automatische Filtern, das erfolgt, wenn auf unterschiedliche Hierarchien derselben Dimension die Crossjoin-Funktion angewendet wird:  
  
 `SELECT`  
  
 `Measures.[Internet Sales Amount]`  
  
 `ON 0,`  
  
 `//Only the dates in Calendar Years 2003 and 2004 will be returned here`  
  
 `Crossjoin(`  
  
 `{[Date].[Calendar Year].&[2003], [Date].[Calendar Year].&[2004]},`  
  
 `[Date].[Date].[Date].Members)`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 In den folgenden drei Beispielen wird das gleiche Ergebnis – Internet Sales Amount nach Bundesstaaten für die Bundesstaaten der USA – zurückgegeben. In den ersten beiden Beispielen werden die beiden Cross Join-Syntaxvarianten verwendet, im dritten Beispiel wird zur Veranschaulichung die WHERE-Klausel verwendet, um die gleichen Informationen zurückzugeben.  
  
### <a name="example-1"></a>Beispiel 1  
  
```  
SELECT CROSSJOIN  
   (  
      {[Customer].[Country].[United States]},  
       [Customer].[State-Province].Members  
   ) ON 0   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
### <a name="example-2"></a>Beispiel 2  
  
```  
SELECT   
   [Customer].[Country].[United States] *   
      [Customer].[State-Province].Members  
ON 0   
FROM [Adventure Works]  
WHERE Measures.[Internet Sales Amount]  
```  
  
### <a name="example-3"></a>Beispiel 3  
  
```  
SELECT   
   [Customer].[State-Province].Members  
ON 0   
FROM [Adventure Works]  
WHERE (Measures.[Internet Sales Amount],  
   [Customer].[Country].[United States])  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

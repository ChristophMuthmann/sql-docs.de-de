---
title: IIf (MDX) | Microsoft Docs
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
- IIF
dev_langs:
- kbMDX
helpviewer_keywords:
- IIf function
ms.assetid: ec7b35e6-f4c5-40bf-93c8-b83c1cc26fe2
caps.latest.revision: 41
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: e859e97cd013e7910238ef373bc4b4f5724df02c
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="iif-mdx"></a>IIf (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Wertet verschiedene Verzweigungsausdrücke abhängig davon aus, ob eine boolesche Bedingung "True" oder "False" ist.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
IIf(Logical_Expression, Expression1 [HINT <hints>], Expression2 [HINT <hints>])  
```  
  
## <a name="arguments"></a>Argumente  
 Die IIf-Funktion akzeptiert drei Argumente: Iif (\<Bedingung >, \<dann branch >, \<else Branch >).  
  
 *Logical_Expression*  
 Eine Bedingung, die ergibt **"true"** (1) oder **"false"** (0). Es muss sich um einen gültigen logischen Multidimensional Expressions (MDX)-Ausdruck handeln.  
  
 *Expression1 Hinweis [Eager | Strict | Verzögerte]]*  
 Verwendet, wenn der logische Ausdruck ergibt **"true"**. Expression1 muss ein gültiger Multidimensional Expressions (MDX)-Ausdruck sein.  
  
 *Expression2 Hinweis [Eager | Strict | Verzögerte]]*  
 Verwendet, wenn der logische Ausdruck ergibt **"false"**. Expression2 muss ein gültiger Multidimensional Expressions (MDX)-Ausdruck sein.  
  
## <a name="remarks"></a>Hinweise  
 Die vom logischen Ausdruck angegebene Bedingung ergibt **"false"** Wenn der Wert dieses Ausdrucks 0 (null) ist. Jeder andere Wert ergibt **"true"**.  
  
 Wenn die Bedingung ist **"true"**, **IIf** -Funktion den ersten Ausdruck zurück. Andernfalls gibt die Funktion den zweiten Ausdruck zurück.  
  
 Die angegebene Ausdrücke können Werte oder MDX-Objekte zurückgeben. Ferner muss der Typ der angegebenen Ausdrücke nicht übereinstimmen.  
  
 Die **IIf** Funktion wird zum Erstellen einer Menge von Elementen basierend auf Suchkriterien nicht empfohlen. Verwenden Sie stattdessen die [Filter](../mdx/filter-mdx.md) Funktion auf jedes Element in einer angegebenen Menge mit einem logischen Ausdruck auszuwerten und eine Teilmenge von Elementen zurückzugeben.  
  
> [!NOTE]  
>  Wenn die Auswertung einer der beiden Ausdrücke NULL ergibt, ist das Resultset NULL, wenn diese Bedingung erfüllt wird.  
  
 Ein Tipp ist ein optionaler Modifizierer, der festlegt, wie und wann der Ausdruck ausgewertet wird. Er ermöglicht es Ihnen, den Standard-Abfrageplan zu überschreiben, indem Sie angeben, wie der Ausdruck ausgewertet wird.  
  
-   EAGER wertet den Ausdruck für den ursprünglichen IIF-Teilbereich aus.  
  
-   STRICT wertet den Ausdruck nur im eingeschränkten Teilbereich aus, der durch den logischen Bedingungsausdruck erstellt wird.  
  
-   LAZY wertet den Ausdruck im zellenweisen Modus aus.  
  
 Während EAGER und STRICT nur für then-else-Verzweigungen von IIF gelten, gilt LAZY für alle MDX-Ausdrücke. Nach jedem MDX-Ausdruck kann HINT LAZY folgen, sodass dieser Ausdruck im zellenweisen Modus ausgewertet wird.  
  
 EAGER und STRICT schließen sich im Tipp gegenseitig aus. Sie können in IIF(,,) für verschiedene Ausdrücke verwendet werden.  
  
 Weitere Informationen finden Sie unter [if Function Query Hints in SQL Server Analysis Services 2008](http://go.microsoft.com/fwlink/?LinkId=269540) und [Execution Plans and Plan Hints for MDX IIF Function and CASE Statement](http://go.microsoft.com/fwlink/?LinkId=269565).  
  
## <a name="examples"></a>Beispiele  
 Die folgende Abfrage zeigt eine einfache Verwendung von **IIF** in einem berechneten Measure zur Rückgabe zweier unterschiedlicher Zeichenfolgen, wenn das Measure Internet Sales Amount größer oder kleiner als 10.000 $beträgt:  
  
 `WITH MEMBER MEASURES.IIFDEMO AS`  
  
 `IIF([Measures].[Internet Sales Amount]>10000`  
  
 `, "Sales Are High", "Sales Are Low")`  
  
 `SELECT {[Measures].[Internet Sales Amount],MEASURES.IIFDEMO} ON 0,`  
  
 `[Date].[Date].[Date].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
 Sehr häufig wird IIF zur Fehlerbehandlung bei „Division durch Null“ innerhalb von berechneten Measures eingesetzt wie im folgenden Beispiel:  
  
 `WITH`  
  
 `//Returns 1.#INF when the previous period contains no value`  
  
 `//but the current period does`  
  
 `MEMBER MEASURES.[Previous Period Growth With Errors] AS`  
  
 `([Measures].[Internet Sales Amount]-([Measures].[Internet Sales Amount], [Date].[Date].CURRENTMEMBER.PREVMEMBER))`  
  
 `/`  
  
 `([Measures].[Internet Sales Amount], [Date].[Date].CURRENTMEMBER.PREVMEMBER)`  
  
 `,FORMAT_STRING='PERCENT'`  
  
 `//Traps division by zero and returns null when the previous period contains`  
  
 `//no value but the current period does`  
  
 `MEMBER MEASURES.[Previous Period Growth] AS`  
  
 `IIF(([Measures].[Internet Sales Amount], [Date].[Date].CURRENTMEMBER.PREVMEMBER)=0,`  
  
 `NULL,`  
  
 `([Measures].[Internet Sales Amount]-([Measures].[Internet Sales Amount], [Date].[Date].CURRENTMEMBER.PREVMEMBER))`  
  
 `/`  
  
 `([Measures].[Internet Sales Amount], [Date].[Date].CURRENTMEMBER.PREVMEMBER)`  
  
 `),FORMAT_STRING='PERCENT'`  
  
 `SELECT {[Measures].[Internet Sales Amount],MEASURES.[Previous Period Growth With Errors], MEASURES.[Previous Period Growth]} ON 0,`  
  
 `DESCENDANTS(`  
  
 `[Date].[Calendar].[Calendar Year].&[2004],`  
  
 `[Date].[Calendar].[Date])`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 `WHERE([Product].[Product Categories].[Subcategory].&[26])`  
  
 Im folgenden ist ein Beispiel für **IIF** Zurückgeben einer von zwei Mengen innerhalb der Generate-Funktion, um einen komplexen Satz von Tupeln auf Zeilen zu erstellen:  
  
 `SELECT {[Measures].[Internet Sales Amount]} ON 0,`  
  
 `//If Internet Sales Amount is zero or null`  
  
 `//returns the current year and the All Customers member`  
  
 `//else returns the current year broken down by Country`  
  
 `GENERATE(`  
  
 `[Date].[Calendar Year].[Calendar Year].MEMBERS`  
  
 `, IIF([Measures].[Internet Sales Amount]=0,`  
  
 `{([Date].[Calendar Year].CURRENTMEMBER, [Customer].[Country].[All Customers])}`  
  
 `, {{[Date].[Calendar Year].CURRENTMEMBER} * [Customer].[Country].[Country].MEMBERS}`  
  
 `))`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 `WHERE([Product].[Product Categories].[Subcategory].&[26])`  
  
 Schließlich wird in diesem Beispiel gezeigt, wie PLAN-Tipps verwendet werden:  
  
 `WITH MEMBER MEASURES.X AS`  
  
 `IIF(`  
  
 `[Measures].[Internet Sales Amount]=0`  
  
 `, NULL`  
  
 `, (1/[Measures].[Internet Sales Amount]) HINT EAGER)`  
  
 `SELECT {[Measures].x} ON 0,`  
  
 `[Customer].[Customer Geography].[Country].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

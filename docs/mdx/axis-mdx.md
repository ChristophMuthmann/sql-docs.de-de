---
title: Achse (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: AXIS
dev_langs: kbMDX
helpviewer_keywords: Axis function
ms.assetid: a3a60a1e-e266-4fa1-ae13-bae73544de33
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: f996b2f9cf090a8b126de5ab349eb13dd0e46485
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="axis-mdx"></a>Axis (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt die Menge der Tupel auf der angegebenen Achse zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Axis(Axis_Number)  
```  
  
## <a name="arguments"></a>Argumente  
 *Axis_Number*  
 Ein gültiger numerischer Ausdruck, der eine Achsennummer angibt.  
  
## <a name="remarks"></a>Hinweise  
 Die **Achse** Funktion verwendet die nullbasierte Position einer Achse, um die Menge der Tupel auf dieser Achse zurückzugeben. Beispielsweise gibt `Axis(0)` die COLUMNS-Achse zurück, `Axis(1)` die ROWS-Achse usw. Die **Achse** Funktion kann nicht für die Filterachse verwendet werden. Diese Funktion kann verwendet werden, damit berechnete Elemente den Kontext der aktuell ausgeführten Abfrage erkennen. Wenn Sie z. B. ein berechnetes Element benötigen, das die Summe nur der Elemente bereitstellt, die auf der ROWS-Achse ausgewählt werden. Sie kann auch verwendet werden, um eine Achse in Abhängigkeit von der Definition einer anderen Achse zu definieren. Z. B. um den Inhalt der ROWS-Achse entsprechend dem Wert des ersten Eintrags auf der COLUMNS-Achse anzuordnen.  
  
> [!NOTE]  
>  Eine Achse kann nur auf eine vorhergehende Achse verweisen. Beispielsweise muss `Axis(0)` nach der Auswertung der COLUMNS-Achse auftreten, z. B auf einer ROW- oder PAGE-Achse.  
  
## <a name="examples"></a>Beispiele  
 Die folgende Beispielabfrage veranschaulicht die Verwendung der Axis-Funktion:  
  
 `WITH MEMBER MEASURES.AXISDEMO AS`  
  
 `SETTOSTR(AXIS(1))`  
  
 `SELECT MEASURES.AXISDEMO ON 0,`  
  
 `[Date].[Calendar Year].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
 Im folgenden Beispiel wird die Verwendung der Axis-Funktion in einem berechneten Element veranschaulicht:  
  
 `WITH MEMBER MEASURES.AXISDEMO AS`  
  
 `SUM(AXIS(1), [Measures].[Internet Sales Amount])`  
  
 `SELECT {[Measures].[Internet Sales Amount],MEASURES.AXISDEMO} ON 0,`  
  
 `{[Date].[Calendar Year].&[2003], [Date].[Calendar Year].&[2004]} ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

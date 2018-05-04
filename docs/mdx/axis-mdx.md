---
title: Achse (MDX) | Microsoft Docs
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
- AXIS
dev_langs:
- kbMDX
helpviewer_keywords:
- Axis function
ms.assetid: a3a60a1e-e266-4fa1-ae13-bae73544de33
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 125b0be234c3b3c233fac3c1d251144914f18a44
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="axis-mdx"></a>Axis (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
 [MDX-Funktionsreferenz & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  

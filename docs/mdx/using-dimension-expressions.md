---
title: "Verwenden von Dimensionsausdrücken | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- expressions [MDX], dimensions
- dimensions [Analysis Services], MDX
ms.assetid: 1d40cffb-e88f-4284-93cf-d62ab4f08395
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 66a955b547f5760ae1193b541fde5f3dc13d323f
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="using-dimension-expressions"></a>Verwenden von Dimensionsausdrücken
[!INCLUDE[tsql-appliesto-ss2008-all_md](../includes/tsql-appliesto-ss2008-all-md.md)]

  Dimensions- und Hierarchieausdrücke werden in MDX (Multidimensional Expressions) üblicherweise zur Übergabe von Parametern an Funktionen verwendet, um Elemente, Mengen oder Tupel einer Hierarchie zurückzugeben.  
  
 Dimensionsausdrücke können nur einfache Ausdrücke sein, da sie Objektbezeichner sind. Finden Sie unter [Ausdrücke &#40; MDX &#41; ](../mdx/expressions-mdx.md) eine Erläuterung der einfachen und komplexen Ausdrücken.  
  
## <a name="dimension-expressions"></a>Dimensionsausdrücke  
 Ein Dimensionsausdruck enthält entweder einen Dimensionsbezeichner oder eine Dimensionsfunktion.  
  
 Dimensionsausdrücke werden selten allein verwendet. Normalerweise wird in einer Dimension eine Hierarchie angegeben. Die einzige Ausnahme bildet die Measures-Dimension, die über keine Hierarchien verfügt.  
  
 Das folgende Beispiel zeigt ein berechnetes Element, das den Ausdruck [Measures] mit den Funktionen .Members und Count() verwendet, um die Anzahl der Elemente in der Measures-Dimension zurückzugeben.  
  
 `WITH MEMBER [Measures].[MeasureCount] AS`  
  
 `COUNT([Measures].MEMBERS)`  
  
 `SELECT [Measures].[MeasureCount] ON 0`  
  
 `FROM [Adventure Works]`  
  
 Ein dimensionsbezeichner wird als *Dimension_Name* in der BNF-Schreibweise zur Beschreibung von MDX-Anweisungen.  
  
## <a name="hierarchy-expressions"></a>Hierarchieausdrücke  
 Ein Hierarchieausdruck enthält entweder einen Hierarchiebezeichner oder eine Hierarchiefunktion. Im folgenden Beispiel wird der Hierarchieausdruck [Date].[Calendar] in Verbindung mit der .Levels- und der .Count-Funktion verwendet, um die Anzahl der Ebenen in der Calendar-Hierarchie der Date-Dimension zurückzugeben:  
  
 `WITH MEMBER [Measures].[CalendarLevelCount] AS`  
  
 `[Date].[Calendar].Levels.Count`  
  
 `SELECT [Measures].[CalendarLevelCount] ON 0`  
  
 `FROM [Adventure Works]`  
  
 Am häufigsten werden Hierarchieausdrücke in Verbindung mit der .Members-Funktion verwendet, um die Anzahl aller Elemente einer Hierarchie zurückzugeben. Im folgenden Beispiel werden alle Elemente von [Date].[Calendar] auf der ROWS-Achse zurückgegeben:  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
 Ein hierarchiebezeichner wird als *Dimension_Name**.* *Hierarchiename* in der BNF-Schreibweise zur Beschreibung von MDX-Anweisungen.  
  
## <a name="see-also"></a>Siehe auch  
 [Ausdrücke &#40; MDX &#41;](../mdx/expressions-mdx.md)  
  
  


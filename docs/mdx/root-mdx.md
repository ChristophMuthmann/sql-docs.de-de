---
title: Root (MDX) | Microsoft Docs
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
- Root
dev_langs:
- kbMDX
helpviewer_keywords:
- Root function
ms.assetid: f6c42e87-5a52-4e43-9dd1-ca757f2db79c
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 16e6fb8fb10816391a25d71a717cff5f4c7abe58
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="root-mdx"></a>Root (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Gibt ein Tupel, aus denen besteht die **alle** Elemente aus jeder Attributhierarchie innerhalb des aktuellen Bereichs in einem Cube, Dimension oder Tupel. Weitere Informationen zum Bereich finden Sie unter [SCOPE-Anweisung &#40; MDX &#41; ](../mdx/mdx-scripting-scope.md).  
  
> [!NOTE]  
>  Wenn eine Attributhierarchie kein ist ein **alle** Element, das Tupel enthält das Standardelement für diese Hierarchie.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Cube syntax  
Root ()  
Dimension syntax  
Root( Dimension_Name )  
Tuple syntax  
Root( Tuple_Expression )  
```  
  
## <a name="arguments"></a>Argumente  
 *Dimension_Name*  
 Ein gültiger Zeichenfolgenausdruck, der einen Dimensionsnamen angibt.  
  
 *Tuple_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der ein Tupel zurückgibt.  
  
## <a name="remarks"></a>Hinweise  
 Wenn weder ein Dimensionsname noch ein Tupelausdruck angegeben wird, die **Stamm** Funktion gibt ein Tupel, enthält der **alle** Member (oder das Standardelement Wenn der **alle** Element ist nicht vorhanden) jeder Attributhierarchie im Cube. Die Reihenfolge der Elemente im Tupel basiert auf der Reihenfolge, in der die Attributhierarchien innerhalb des Cubes definiert sind.  
  
 Wenn ein Dimensionsname angegeben wird, die **Stamm** Funktion gibt ein Tupel, enthält die **alle** Member (bzw. das Standardelement Wenn die **alle** Element ist nicht vorhanden) jeder Attributhierarchie in der angegebenen Dimension basierend auf dem Kontext des aktuellen Elements. Die Reihenfolge der Elemente im Tupel basiert auf der Reihenfolge, in der die Attributhierarchien innerhalb der Dimension definiert sind.  
  
> [!NOTE]  
>  Wenn ein Hierarchiename angegeben wird, die **Tupel** Funktion den Namen der Dimension aus dem angegebenen Hierarchienamen übernommen wird.  
  
 Wenn ein Tupelausdruck angegeben wird, die **Root** Funktion gibt ein Tupel, das die Schnittmenge der angegebenen Tupel enthält und die **alle** Mitglied aller anderen Dimensionsattribute, die nicht explizit in das angegebene Tupel eingeschlossen.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel gibt die Tupel mit den **alle** Member (oder den Standardwert Wenn die **alle** Element ist nicht vorhanden) jeder Hierarchie im Adventure Works-Cube.  
  
```  
SELECT Root()ON 0  
FROM [Adventure Works]  
```  
  
 Das folgende Beispiel gibt die Tupel mit den **alle** Member (oder den Standardwert Wenn die **alle** Element ist nicht vorhanden) jeder Hierarchie in der Date-Dimension im Adventure Works-Cube und der Wert für das angegebene Element der Measures-Dimension, die Schnittmenge mit diesen Standardelementen.  
  
```  
SELECT Root([Date]) ON 0  
FROM [Adventure Works]  
WHERE [Measures].[Order Count]  
```  
  
 Das folgende Beispiel gibt die angegebene Tupelelement enthaltendes Tupel (1. Juli 2001 zusammen mit der **alle** Member (oder den Standardwert Wenn die **alle** Element ist nicht vorhanden) jeder nicht angegebenen Hierarchie in der Date dimension Adventure Works-Cube sowie den Wert für das angegebene Element der Measures-Dimension, die Schnittmenge mit diesen Standardelementen.  
  
```  
SELECT Root([Date].[July 1, 2001]) ON 0  
FROM [Adventure Works]  
WHERE [Measures].[Order Count]  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

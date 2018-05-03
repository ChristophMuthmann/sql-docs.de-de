---
title: Verzögerung (MDX) | Microsoft Docs
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
- LAG
dev_langs:
- kbMDX
helpviewer_keywords:
- Lag function
ms.assetid: 08c704ea-35d8-44ee-abe5-93bd24b99906
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 7dce14ac4d98d3fd75da42ace8327115eefafd1e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="lag-mdx"></a>Lag (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Gibt das Element zurück, das eine angegebene Anzahl von Positionen vor einem angegebenen Element auf der Ebene des Elements liegt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Member_Expression.Lag(Index)   
```  
  
## <a name="arguments"></a>Argumente  
 *Member_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der ein Element zurückgibt.  
  
 *Index*  
 Ein gültiger numerischer Ausdruck, der die Anzahl der Elementpositionen angibt, die vor dem Element liegen sollen.  
  
## <a name="remarks"></a>Hinweise  
 Die Elementpositionen auf einer Ebene werden über die natürliche Reihenfolge der Attributhierarchie bestimmt. Die Nummerierung der Positionen basiert auf Null.  
  
 Wenn der angegebene Abstand 0 (null), ist die **Lag** Funktion gibt das angegebene Element selbst zurück.  
  
 Wenn der angegebene Abstand negativ ist, wird die **Lag** -Funktion ein nachfolgendes Element zurück.  
  
 `Lag(1)` entspricht der [PrevMember](../mdx/prevmember-mdx.md) Funktion. `Lag(-1)` entspricht der [NextMember](../mdx/nextmember-mdx.md) Funktion.  
  
 Die **Lag** Funktion ist vergleichbar mit der [führen](../mdx/lead-mdx.md) -Funktion, außer dass die **führen** Funktion sucht, in die entgegengesetzte Richtung auf die **Lag** Funktion. Somit ist `Lag(n)` äquivalent zu `Lead(-n)`.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird der Wert December 2001 zurückgegeben:  
  
```  
SELECT [Date].[Fiscal].[Month].[February 2002].Lag(2) ON 0  
FROM [Adventure Works]  
  
```  
  
 Im folgenden Beispiel wird der Wert March 2002 zurückgegeben:  
  
```  
SELECT [Date].[Fiscal].[Month].[February 2002].Lag(-1) ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  

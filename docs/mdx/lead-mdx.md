---
title: Führen Sie (MDX) | Microsoft Docs
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
- LEAD
dev_langs:
- kbMDX
helpviewer_keywords:
- Lead function
ms.assetid: f3250092-7b98-40b5-8dca-77e3b50734a0
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: c53f5c6c240404975318764716a1b6a333064536
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="lead-mdx"></a>Lead (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Gibt das Element zurück, das eine angegebene Anzahl von Positionen auf ein angegebenes Element entlang der Ebene des Elements folgt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Member_Expression.Lead( Index )  
```  
  
## <a name="arguments"></a>Argumente  
 *Member_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der ein Element zurückgibt.  
  
 *Index*  
 Ein gültiger numerischer Ausdruck, der eine Anzahl der Elementpositionen angibt.  
  
## <a name="remarks"></a>Hinweise  
 Die Elementpositionen auf einer Ebene werden über die natürliche Reihenfolge der Attributhierarchie bestimmt. Die Nummerierung der Positionen basiert auf Null.  
  
 Wenn der angegebene Abstand null (0), ist die **führen** Funktion gibt das angegebene Element zurück.  
  
 Wenn der angegebene Abstand negativ ist, wird die **führen** -Funktion ein vorausgehendes Element zurück.  
  
 `Lead(1)`entspricht der [NextMember](../mdx/nextmember-mdx.md) Funktion. `Lead(-1)`entspricht der [PrevMember](../mdx/prevmember-mdx.md) Funktion.  
  
 Die **führen** Funktion ist vergleichbar mit der [Lag](../mdx/lag-mdx.md) -Funktion, außer dass die **Lag** Funktion sucht, in die entgegengesetzte Richtung auf die **führen** Funktion. Somit ist `Lead(n)` äquivalent zu `Lag(-n)`.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird der Wert December 2001 zurückgegeben:  
  
```  
SELECT [Date].[Fiscal].[Month].[February 2002].Lead(-2) ON 0  
FROM [Adventure Works]  
  
```  
  
 Im folgenden Beispiel wird der Wert March 2002 zurückgegeben:  
  
```  
SELECT [Date].[Fiscal].[Month].[February 2002].Lead(1) ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

---
title: StDev (MDX) | Microsoft Docs
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
f1_keywords: STDEV
dev_langs: kbMDX
helpviewer_keywords: Stdev function [MDX]
ms.assetid: c3e31763-18ca-4a2b-bc03-3ee777970c68
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 6f1e975cb35d0de9d8aec1abaae590a5791422ad
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="stdev-mdx"></a>Stdev (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Gibt die Stichproben-Standardabweichung eines über einer Menge ausgewerteten numerischen Ausdrucks zurück, die mithilfe der Formel für die ausgewogene Auffüllung (geteilt durch n-1) berechnet wurde.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Stdev(Set_Expression [ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *Set_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Menge zurückgibt.  
  
 *Numeric_expression*  
 Ein gültiger numerischer Ausdruck, bei dem es sich in der Regel um einen MDX-Ausdruck (Multidimensional Expressions) für Zellenkoordinaten handelt, die eine Zahl zurückgeben.  
  
## <a name="remarks"></a>Hinweise  
 Die **Stdev** -Funktion verwendet die ausgewogene Auffüllung Formel, während die [StdevP](../mdx/stdevp-mdx.md) Funktion der Formel für die unausgewogene Auffüllung verwendet.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird die Standardabweichung für Internet Order Quantity, ausgewertet über die ersten drei Monate des Kalenderjahres 2003, mithilfe der Formel für die ausgewogene Auffüllung zurückgegeben.  
  
```  
WITH MEMBER Measures.x AS   
   Stdev   
   ( { [Date].[Calendar].[Month].[January 2003],  
       [Date].[Calendar].[Month].[February 2003],  
       [Date].[Calendar].[Month].[March 2003]},  
    [Measures].[Internet Order Quantity])  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

---
title: LinRegR2 (MDX) | Microsoft Docs
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
f1_keywords: LINREGR2
dev_langs: kbMDX
helpviewer_keywords: LinRegR2 function
ms.assetid: 770d1e1e-d034-43f1-82b1-3f91d52c86be
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: ff4cbeba77820d725ebef804efc1b9e467dcdd1c
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="linregr2-mdx"></a>LinRegR2 (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Berechnet die lineare Regression einer Menge und gibt den Bestimmungskoeffizienten, R<sup>2</sup>.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
LinRegR2(Set_Expression, Numeric_Expression_y [ ,Numeric_Expression_x ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *Set_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Menge zurückgibt.  
  
 *Numeric_Expression_y*  
 Ein gültiger numerischer Ausdruck, bei dem es sich in der Regel um einen MDX-Ausdruck (Multidimensional Expressions) für Zellenkoordinaten handelt. Die vom Ausdruck zurückgegebene Zahl stellt den Wert für die Y-Achse dar.  
  
 *Numeric_Expression_x*  
 Ein gültiger numerischer Ausdruck, bei dem es sich in der Regel um einen MDX-Ausdruck (Multidimensional Expressions) für Zellenkoordinaten handelt. Die vom Ausdruck zurückgegebene Zahl stellt den Wert für die X-Achse dar.  
  
## <a name="remarks"></a>Remarks  
 Die lineare Regression berechnet mit der Methode der kleinsten Quadrate die Gleichung einer Regressionsgeraden (d. h. der Ausgleichsgeraden für eine Reihe von Punkten). Die Regressionszeile hat die folgende Gleichung, in denen eine die Neigung und b das Konstante Glied:  
  
 y = ax+b  
  
 Die **LinRegR2** -Funktion wertet die angegebene Setagainst den ersten numerischen Expressionto die Werte für die y-Achse zu erhalten. Anschließend wertet die Funktion die angegebene Menge für den zweiten numerischen Ausdruck, sofern angegeben, aus, um die Werte für die X-Achse zu erhalten. Wenn die zweite numerischen AusdruckIS nicht angegeben ist, verwendet die Funktion den aktuellen Kontext der Zellen in der angegebenen Menge als Werte für die x-Achse an. Keine Angabe der X-Axisargument wird häufig mit der Time-Dimension verwendet.  
  
 Nach dem Erhalt des Satzes von Punkten, die **LinRegR2** Funktion gibt das statistische R<sup>2</sup> , die die Übereinstimmung der linearen Gleichung mit den Punkten beschreibt.  
  
> [!NOTE]  
>  Die **LinRegR2** Funktion ignoriert leere Zellen oder Zellen, die Text oder logische Werte enthalten. Zellen mit dem Wert Null (0) werden jedoch von der Funktion berücksichtigt.  
  
## <a name="example"></a>Beispiel  
 Das folgende Beispiel gibt das statistische R<sup>2</sup> , die die Eignung der Übereinstimmung der linearen Gleichung mit den Punkten für die Unit Sales- und Store sales-Measures beschreibt.  
  
```  
LinRegR2(LastPeriods(10), [Measures].[Unit Sales],[Measures].[Store Sales])  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

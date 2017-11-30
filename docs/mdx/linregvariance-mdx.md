---
title: LinRegVariance (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: LINREGVARIANCE
dev_langs: kbMDX
helpviewer_keywords: LinRegVariance function
ms.assetid: 09803510-2d71-401b-970e-bbdcac06558d
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: bad28c872f8e414eaa49fba168f55845567dc5ac
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="linregvariance-mdx"></a>LinRegVariance (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Berechnet die lineare Regression einer Menge und gibt die Varianz der regressionsgleichung zugeordnete y = Ax + b.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
LinRegVariance(Set_Expression, Numeric_Expression_y [ ,Numeric_Expression_x ] ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *Set_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Menge zurückgibt.  
  
 *Numeric_Expression_y*  
 Ein gültiger numerischer Ausdruck, bei dem es sich in der Regel um einen MDX-Ausdruck (Multidimensional Expressions) für Zellenkoordinaten handelt. Die vom Ausdruck zurückgegebene Zahl stellt den Wert für die Y-Achse dar.  
  
 *Numeric_Expression_x*  
 Ein gültiger numerischer Ausdruck, bei dem es sich in der Regel um einen MDX-Ausdruck (Multidimensional Expressions) für Zellenkoordinaten handelt. Die vom Ausdruck zurückgegebene Zahl stellt den Wert für die X-Achse dar.  
  
## <a name="remarks"></a>Hinweise  
 Die lineare Regression berechnet mit der Methode der kleinsten Quadrate die Gleichung einer Regressionsgeraden (d. h. der Ausgleichsgeraden für eine Reihe von Punkten). Die Regressionszeile hat die folgende Gleichung, in denen eine die Neigung und b das Konstante Glied:  
  
 y = ax+b  
  
 Die **LinRegVariance** -Funktion wertet die angegebene Setagainst den ersten numerischen Ausdruck aus, um die Werte für die y-Achse zu erhalten. Anschließend wertet die Funktion die angegebene Setagainst den zweiten numerischen Ausdruck aus, wenn angegeben, um die Werte für die x-Achse zu erhalten, wird. Wenn die zweite numerischen AusdruckIS nicht angegeben ist, verwendet die Funktion den aktuellen Kontext der Zellen in der angegebenen Menge als Werte für die x-Achse an. Das x-Achsen-Argument nicht angeben wird häufig mit der Time-Dimension verwendet.  
  
 Nach dem Erhalt des Satzes von Punkten, die **LinRegVariance** Funktion gibt die statistische Varianz zurück, die die Übereinstimmung der linearen Gleichung mit den Punkten beschreibt.  
  
> [!NOTE]  
>  Die **LinRegVariance** Funktion ignoriert leere Zellen oder Zellen, die Text oder logische Werte enthalten. Zellen mit dem Wert Null (0) werden jedoch von der Funktion berücksichtigt.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird die statistische Varianz zurückgegeben, die die Übereinstimmung der linearen Gleichung mit den Punkten für die Unit Sales- und die Store Sales-Measures beschreibt.  
  
```  
LinRegVariance(LastPeriods(10),[Measures].[Unit Sales],[Measures].[Store Sales])  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

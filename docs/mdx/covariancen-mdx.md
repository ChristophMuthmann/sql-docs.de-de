---
title: CovarianceN (MDX) | Microsoft Docs
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
- COVARIANCEN
dev_langs:
- kbMDX
helpviewer_keywords:
- Covariancen function
ms.assetid: 1cc621cd-ffa0-40aa-91f0-bc5cb57f692b
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: b9d83c327d40e73084386ed4f6adaf027bd8331b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="covariancen-mdx"></a>CovarianceN (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Gibt die Stichprobenkovarianz eines X-Y-Wertepaares zurück, die für ein Menge mithilfe der nicht unausgewogenen Auffüllungsformel (geteilt durch die Anzahl der X-Y-Paare) ausgewertet wurde.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
CovarianceN(Set_Expression, Numeric_Expression_y [ ,Numeric_Expression_x ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *Set_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Menge zurückgibt.  
  
 *Numeric_Expression_y*  
 Ein gültiger numerischer Ausdruck, bei dem es sich in der Regel um einen MDX-Ausdruck (Multidimensional Expressions) für Zellenkoordinaten handelt. Die vom Ausdruck zurückgegebene Zahl stellt den Wert für die Y-Achse dar.  
  
 *Numeric_Expression_x*  
 Ein gültiger numerischer Ausdruck, bei dem es sich in der Regel um einen MDX-Ausdruck (Multidimensional Expressions) für Zellenkoordinaten handelt. Die vom Ausdruck zurückgegebene Zahl stellt den Wert für die X-Achse dar.  
  
## <a name="remarks"></a>Hinweise  
 Die **CovarianceN** Funktion wertet die angegebene Menge für den ersten numerischen Ausdruck, um die Werte für die y-Achse zu erhalten. Anschließend wertet die Funktion die angegebene Menge für den zweiten numerischen Ausdruck aus, um die Werte für die X-Achse zu erhalten. Wenn Sie der zweite numerische Ausdruck nicht angegeben wird, verwendet die Funktion den aktuellen Kontext der Zellen in der angegebenen Menge als Werte für die x-Achse an.  
  
 Die **CovarianceN** Funktion der Formel für die ausgewogene Auffüllung verwendet. Dies ist im Gegensatz zu den [Kovarianz](../mdx/covariance-mdx.md) Funktion, die Formel für die unausgewogene Auffüllung (geteilt durch die Anzahl der X-y-Paare) verwendet.  
  
> [!NOTE]  
>  Die **CovarianceN** Funktion ignoriert leere Zellen oder Zellen, die Text oder logische Werte enthalten. Zellen mit dem Wert Null (0) werden jedoch von der Funktion berücksichtigt.  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  

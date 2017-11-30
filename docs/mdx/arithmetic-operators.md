---
title: Arithmetische Operatoren | Microsoft Docs
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
dev_langs: kbMDX
helpviewer_keywords: arithmetic operators
ms.assetid: 1dff3e20-fe9d-4155-bf06-27d6458188e9
caps.latest.revision: "27"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 4f441cec66ad8d1a4f2610a81c096662fdcdca87
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="arithmetic-operators"></a>Arithmetische Operatoren
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Sie können arithmetische Operatoren in MDX (Multidimensional Expressions) für beliebige arithmetische Berechnungen verwenden. Dazu gehören Addition, Subtraktion, Multiplikation und Division.  
  
 MDX unterstützt die arithmetischen Operatoren, die in der folgenden Tabelle aufgelistet sind.  
  
|Operator|Description|  
|--------------|-----------------|  
|[+ (Add) (+ (Addieren))](../mdx/add-mdx.md)|Addition zweier Zahlen.|  
|[/ (Division)](../mdx/divide-mdx-operator-reference.md)|Dividiert eine Zahl durch eine andere Zahl.|  
|[* (Multiply) (* (Multiplizieren))](../mdx/multiply-mdx.md)|Multipliziert zwei Zahlen.|  
|[- (Subtract) (- (Subtrahieren))](../mdx/subtract-mdx.md)|Subtraktion zweier Zahlen.|  
|^ (Potenz) |Potenziert eine Zahl mit einer anderen Zahl.|  
  
> [!NOTE]  
>  MDX enthält keine Funktion, um die Quadratwurzel einer Zahl zu erhalten. Um die Quadratwurzel einer Zahl zu erhalten, potenzieren Sie sie mit 0,5 unter Verwendung des ^-Operators.  
  
## <a name="order-of-precedence"></a>Rangfolge  
 Die folgenden Regeln bestimmen die Rangfolge, die arithmetische Operatoren in einem MDX-Ausdruck haben.  
  
-   Sind in einem Ausdruck mehrere arithmetische Operatoren vorhanden, führt MDX Multiplikationen und Divisionen vor Subtraktionen und Additionen aus.  
  
-   Wenn alle arithmetische Operatoren in einem Ausdruck dieselbe Ebene des Vorrang haben, ist die Reihenfolge der Ausführung links nach rechts ausgerichtet.  
  
-   Ausdrücke in Klammern erhalten Vorrang vor allen anderen Operationen.  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Operatorreferenz &#40; MDX &#41;](../mdx/mdx-operator-reference-mdx.md)   
 [Operatoren &#40; MDX-Syntax &#41;](../mdx/operators-mdx-syntax.md)  
  
  

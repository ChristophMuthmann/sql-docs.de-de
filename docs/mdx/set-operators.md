---
title: Mengenoperatoren | Microsoft Docs
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
helpviewer_keywords: set operators [MDX]
ms.assetid: 83500d2e-44b3-49eb-a221-3ce5a58277a5
caps.latest.revision: "27"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 55d5b2c2b28a644221673c7104881d5864fbbfa7
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="set-operators"></a>Mengenoperatoren
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  In MDX (Multidimensional Expressions) führen Mengenoperatoren Operationen für Elemente oder Mengen aus und geben dann eine Menge zurück. Mengenoperatoren werden häufig als Alternative zu mehreren Mengenfunktionen in MDX-Ausdrücken verwendet.  
  
 MDX unterstützt die Mengenoperatoren, die in der folgenden Tabelle aufgelistet sind.  
  
|Operator|Description|  
|--------------|-----------------|  
|[- (Except) (- (Außer))](../mdx/except-mdx-operator.md)|Gibt die Differenzmenge zweier Mengen zurück, wobei doppelte Elemente entfernt werden.<br /><br /> Dieser Operator ist funktionell gleichwertig mit der [außer](../mdx/except-mdx-function.md) Funktion.|  
|[* (Crossjoin)](../mdx/crossjoin-mdx-operator-reference.md)|Gibt das Kreuzprodukt zweier Mengen zurück.<br /><br /> Dieser Operator ist funktionell gleichwertig mit der [Crossjoin](../mdx/crossjoin-mdx.md) Funktion.|  
|[: (Range) (: (Bereich))](../mdx/range-mdx.md)|Gibt eine natürlich geordnete Menge zurück, wobei die beiden angegebenen Elemente als Endpunkte und alle Elemente zwischen den beiden angegebenen Elementen als Elemente der Menge eingeschlossen werden.|  
|[+ (Union) (+ (Vereinigung))](../mdx/union-mdx-operator-reference.md)|Gibt eine Vereinigungsmenge zweier Mengen zurück, wobei doppelte Elemente ausgeschlossen werden.<br /><br /> Dieser Operator ist funktionell gleichwertig mit der [Union &#40; MDX &#41; ](../mdx/union-mdx.md) Funktion.|  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)   
 [MDX-Operatorreferenz &#40; MDX &#41;](../mdx/mdx-operator-reference-mdx.md)   
 [Operatoren &#40; MDX-Syntax &#41;](../mdx/operators-mdx-syntax.md)  
  
  

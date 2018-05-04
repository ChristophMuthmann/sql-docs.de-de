---
title: MDX-Operatorreferenz (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- Multidimensional Expressions [Analysis Services], operators
- operators [MDX]
- MDX [Analysis Services], operators
ms.assetid: 1cdb8c31-a5f6-4430-b509-f81344f4622a
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 05351149c5c4b7e5b639a1d3c6cb16e9894f181e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="mdx-operator-reference-mdx"></a>MDX-Operatorreferenz (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Die MDX-Sprache (Multidimensional Expressions) unterstützt arithmetische, logische, Vergleichs-, Mengen-, Zeichenfolgen- und unäre Operatoren. In der folgenden Liste sind die unterstützten Operatoren und ihre Beschreibungen aufgeführt.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
|Thema|Description|  
|-----------|-----------------|  
|[--& #40; Kommentar & #41; & #40; MDX & #41;](../mdx/comment-mdx-operator-reference.md)|Zeigt vom Benutzer bereitgestellten Kommentartext an.|  
|[- &#40;Außer&#41; &#40;MDX&#41;](../mdx/except-mdx-operator.md)|Führt eine Mengenoperation aus, die die Differenz zwischen zwei Mengen zurückgibt. Dabei werden doppelte Werte entfernt.|  
|[- &#40;Negative&#41; &#40;MDX&#41;](../mdx/negative-mdx.md)|Führt eine unäre Operation aus, die den negativen Wert eines numerischen Ausdrucks zurückgibt.|  
|[- &#40;Subtrahieren&#41; &#40;MDX&#41;](../mdx/subtract-mdx.md)|Führt eine arithmetische Operation aus, die eine Zahl von einer anderen subtrahiert.|  
|[&#42;&#40;Crossjoin&#41; &#40;MDX&#41;](../mdx/crossjoin-mdx-operator-reference.md)|Führt eine Mengenoperation aus, die das Kreuzprodukt zweier Mengen zurückgibt.|  
|[&#42;&#40;Multiplizieren&#41; &#40;MDX&#41;](../mdx/multiply-mdx.md)|Führt eine arithmetische Operation aus, die zwei Zahlen multipliziert.|  
|[&#40;Teilen Sie&#41; &#40;MDX&#41;](../mdx/divide-mdx-operator-reference.md)|Führt eine arithmetische Operation aus, die eine Zahl durch eine andere dividiert.|  
|[^ &#40;Power&#41; &#40;MDX&#41;](../mdx/power-mdx.md)|Führt einen arithmetischen Vorgang aus, bei dem eine Zahl mit einer anderen potenziert wird.|  
|[Kommentar & #40; MDX & #41;](../mdx/comment-mdx.md)|Zeigt vom Benutzer bereitgestellten Kommentartext an.|  
|[& #40; Kommentar & #41; & #40; MDX & #41;](../mdx/comment-mdx-double-slash.md)|Gibt vom Benutzer bereitgestellten Text an.|  
|[: &#40;Bereich&#41; &#40;MDX&#41;](../mdx/range-mdx.md)|Führt eine Mengenoperation aus, die eine natürlich geordnete Menge zurückgibt, wobei die beiden angegebenen Elemente als Endpunkte dienen und alle Elemente zwischen den beiden angegebenen Elementen als Elemente der Menge eingeschlossen werden.|  
|[+ &#40;Hinzufügen&#41; &#40;MDX&#41;](../mdx/add-mdx.md)|Führt eine arithmetische Operation aus, die zwei Zahlen addiert.|  
|[+ &#40;Positive&#41; &#40;MDX&#41;](../mdx/positive-mdx.md)|Führt eine unäre Operation aus, die den positiven Wert eines numerischen Ausdrucks zurückgibt.|  
|[+ &#40;Zeichenfolgenverkettung&#41; &#40;MDX&#41;](../mdx/string-concatenation-mdx.md)|Führt eine Zeichenfolgenoperation aus, die mindestens zwei Zeichenfolgen, Tupel oder eine Kombination von Zeichenfolgen und Tupeln verkettet.|  
|[+ &#40;Union&#41; &#40;MDX&#41;](../mdx/union-mdx-operator-reference.md)|Führt eine Mengenoperation aus, die eine Vereinigungsmenge zweier Mengen zurückgibt. Dabei werden doppelte Elemente entfernt.|  
|[&#60;&#40;Kleiner als&#41; &#40;MDX&#41;](../mdx/less-than-mdx.md)|Führt eine Vergleichsoperation aus, die bestimmt, ob der Wert eines MDX-Ausdrucks kleiner als der Wert eines anderen MDX-Ausdrucks ist.|  
|[&#60;= &#40;Kleiner als oder gleich&#41; &#40;MDX&#41;](../mdx/less-than-or-equal-to-mdx.md)|Führt eine Vergleichsoperation aus, die bestimmt, ob der Wert eines MDX-Ausdrucks kleiner oder gleich dem Wert eines anderen MDX-Ausdrucks ist.|  
|[&#60;&#62;&#40;Ungleich&#41; &#40;MDX&#41;](../mdx/not-equal-to-mdx.md)|Führt eine Vergleichsoperation aus, die bestimmt, ob der Wert eines MDX-Ausdrucks ungleich dem Wert eines anderen MDX-Ausdrucks ist.|  
|[= &#40;Gleich&#41; &#40;MDX&#41;](../mdx/equal-to-mdx.md)|Führt eine Vergleichsoperation aus, die bestimmt, ob der Wert eines MDX-Ausdrucks gleich dem Wert eines anderen MDX-Ausdrucks ist.|  
|[&#62;&#40;Größer als&#41; &#40;MDX&#41;](../mdx/greater-than-mdx.md)|Führt eine Vergleichsoperation aus, die bestimmt, ob der Wert eines MDX-Ausdrucks größer als der Wert eines anderen MDX-Ausdrucks ist.|  
|[&#62;= &#40;Größer als oder gleich&#41; &#40;MDX&#41;](../mdx/greater-than-or-equal-to-mdx.md)|Führt eine Vergleichsoperation aus, die bestimmt, ob der Wert eines MDX-Ausdrucks größer oder gleich dem Wert eines anderen MDX-Ausdrucks ist.|  
|[UND &AMP;#40;MDX&AMP;#41;](../mdx/and-mdx.md)|Führt eine logische Konjunktion zweier numerischer Ausdrücke aus.|  
|[IST &AMP;#40;MDX&AMP;#41;](../mdx/is-mdx.md)|Führt einen logischen Vergleich zweier Objektausdrücke aus.|  
|[NICHT &AMP;#40;MDX&AMP;#41;](../mdx/not-mdx.md)|Führt eine logische Negation für einen numerischen Ausdruck aus.|  
|[ODER &AMP;#40;MDX&AMP;#41;](../mdx/or-mdx.md)|Führt eine logische Disjunktion mit zwei numerischen Ausdrücken aus.|  
|[XOR &AMP;#40;MDX&AMP;#41;](../mdx/xor-mdx.md)|Führt eine logische Exklusion zweier numerischer Ausdrücke aus.|  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Sprachreferenz & #40; MDX & #41;](../mdx/mdx-language-reference-mdx.md)  
  
  

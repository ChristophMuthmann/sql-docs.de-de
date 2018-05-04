---
title: Verwenden von Elementausdrücken | Microsoft Docs
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
- members [MDX], expressions
- expressions [MDX], members
ms.assetid: 63c7af49-8bea-47c5-9566-a961f77d2a3d
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 79e977a3c25b95d4789d6b7c56ce5e188788a4fa
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="using-member-expressions"></a>Verwenden von Elementausdrücken
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Ein Elementausdruck enthält einen Elementbezeichner, eine Elementfunktion oder einen Ausdruck, der in ein Element konvertiert werden kann.  
  
 Elementbezeichner können viele verschiedene Formate haben. Die einfachste Form eines Elementbezeichners besteht aus dem Namen des Elements. Beispiel:  
  
```  
SELECT Amount ON 0  
FROM [Adventure Works]  
  
```  
  
 Falls es jedoch mehrere Elemente des gleichen Namens in unterschiedlichen Hierarchien gibt, gibt es keine Möglichkeit, zu bestimmen, welches Element die Abfrage zurückgibt. Zum Beispiel fordert die folgende Abfrage Daten für ein Element mit dem Namen [CY 2004] an. Die Abfrage wird erfolgreich ausgeführt, jedoch gibt es im Adventure Works-Cube mindestens sechs Elemente mit diesem Namen:  
  
```  
SELECT [CY 2004] ON 0  
FROM [Adventure Works]  
  
```  
  
 Deshalb ist die zuverlässigste Form von Elementbezeichnern der eindeutige Name des Elements, um ein spezifisches Element in einem Cube sicher zu identifizieren. Analyses Services kann auf unterschiedliche Weise eindeutige Namen generieren, ein eindeutiger Name setzt sich jedoch immer aus mindestens zwei Bezeichnern zusammen: dem Dimensionsnamen sowie dem Elementnamen oder dem Elementschlüssel. Ein eindeutiger Name hat folgendes Format:  
  
```  
  
Dimension_Name  
.[Hierarchy_Name.] [[{Member_Name | &Member_Key}.]... ] {Member_Name | &Member_Key}  
  
```  
  
 Im Folgenden sind einige Beispiele für eindeutige Elementnamen aus dem Adventure Works-Cube aufgelistet:  
  
```  
[Measures].[Amount]  
[Date].[Calendar Year].&[2004]  
[Date].[Calendar].[Calendar Quarter].&[2004]&[1]  
[Employee].[Employees].&[112]  
[Product].[Product Categories].[All Products]  
  
```  
  
 Es gibt viele MDX-Funktionen, die Elemente zurückgeben. Eine vollständige Liste finden Sie unter [MDX-Funktionsreferenz &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
> [!NOTE]  
>  Weitere Informationen zu Elementnamen und Elementschlüssel finden Sie unter [arbeiten mit Elementen, Tupeln und Mengen &#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Ausdrücke &#40;MDX&#41;](../mdx/expressions-mdx.md)  
  
  

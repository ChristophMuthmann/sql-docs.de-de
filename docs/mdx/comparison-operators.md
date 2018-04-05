---
title: Vergleichsoperatoren | Microsoft Docs
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
dev_langs:
- kbMDX
helpviewer_keywords:
- comparison operators [MDX]
ms.assetid: 4a4bbc76-c6a2-4b19-ae75-6ac3ac14df01
caps.latest.revision: 27
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: e99997bd3d87dbe949c8658ac7f866c648959430
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="comparison-operators"></a>Vergleichsoperatoren
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Sie verwenden Vergleichsoperatoren mit skalaren Daten. Sie können Vergleichsoperatoren in jedem MDX-Ausdruck (Multidimensional Expressions) verwenden.  
  
 Um eine Bedingung zu überprüfen, können Sie auch Vergleichsoperatoren in MDX-Anweisungen und Funktionen, z. B. der MDX-Abfrage [IIf](../mdx/iif-mdx.md) Funktion. Wenn Sie mit Vergleichsoperatoren eine Bedingung überprüfen und dann anhand dieser Bedingung Daten ändern möchten, sollten Sie sich vorher allerdings vergewissern, dass Sie die entsprechenden Berechtigungen haben. Jeder Benutzer, der Zugriff auf die tatsächlichen Daten hat und diese Daten abfragen kann, kann Vergleichsoperatoren in zusätzlichen Abfragen verwenden. Dieser Zugriff bedeutet aber nicht, dass diese Benutzer die entsprechenden Berechtigungen zum Ändern von Daten haben oder haben sollten. Außerdem sollte, damit die Datenintegrität erhalten bleibt, die Anzahl der Benutzer beschränkt werden, die Daten abfragen und ändern können.  
  
 Vergleichsoperatoren ergeben einen booleschen Datentyp zurückgeben von "true" oder "false" auf das Ergebnis der getesteten Bedingung basiert.  
  
 MDX unterstützt die Vergleichsoperatoren, die in der folgenden Tabelle aufgelistet sind.  
  
|Operator|Description|  
|--------------|-----------------|  
|[= (Equal To) (= (Gleich))](../mdx/equal-to-mdx.md)|Gibt für Argumente, die nicht NULL enthalten, TRUE zurück, wenn das linke Argument gleich dem rechten Argument ist. Gibt andernfalls FALSE zurück.<br /><br /> Wenn mindestens eines der Argumente zu einem NULL-Wert ausgewertet wird, gibt der Operator einen NULL-Wert zurück, es sei denn, der Vergleich `0=null` wird ausgeführt; in diesem Fall enthält der boolesche Wert TRUE.|  
|[<> (Not Equal To) (<> (Ungleich))](../mdx/not-equal-to-mdx.md)|Gibt für Argumente, die nicht NULL enthalten, TRUE zurück, wenn das linke Argument ungleich dem rechten Argument ist. Gibt andernfalls FALSE zurück.<br /><br /> Wenn mindestens eines der Argumente zu einem NULL-Wert ausgewertet wird, gibt der Operator einen NULL-Wert zurück.|  
|[> (Greater Than) (> (Größer als))](../mdx/greater-than-mdx.md)|Gibt für Argumente, die nicht NULL enthalten, TRUE zurück, wenn das linke Argument einen Wert hat, der größer ist als der Wert des rechten Arguments. Gibt andernfalls FALSE zurück.<br /><br /> Wenn mindestens eines der Argumente zu einem NULL-Wert ausgewertet wird, gibt der Operator einen NULL-Wert zurück.|  
|[>= (Greater Than or Equal To) (>= (Größer als oder gleich)](../mdx/greater-than-or-equal-to-mdx.md)|Gibt für Argumente, die nicht NULL enthalten, TRUE zurück, wenn das linke Argument einen Wert hat, der größer gleich dem Wert des rechten Arguments ist. Gibt andernfalls FALSE zurück.<br /><br /> Wenn mindestens eines der Argumente zu einem NULL-Wert ausgewertet wird, gibt der Operator einen NULL-Wert zurück.|  
|[< (Less Than) (< (Kleiner als))](../mdx/less-than-mdx.md)|Gibt für Argumente, die nicht NULL enthalten, TRUE zurück, wenn das linke Argument einen Wert hat, der kleiner ist als der Wert des rechten Arguments. Gibt andernfalls FALSE zurück.<br /><br /> Wenn mindestens eines der Argumente zu einem NULL-Wert ausgewertet wird, gibt der Operator einen NULL-Wert zurück.|  
|[<= (Less Than or Equal To) (<= (Kleiner als oder gleich))](../mdx/less-than-or-equal-to-mdx.md)|Gibt für Argumente, die nicht NULL enthalten, TRUE zurück, wenn das linke Argument einen Wert hat, der kleiner gleich dem Wert des rechten Arguments ist. Gibt andernfalls FALSE zurück.<br /><br /> Wenn mindestens eines der Argumente zu einem NULL-Wert ausgewertet wird, gibt der Operator einen NULL-Wert zurück.|  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Operatorreferenz &#40; MDX &#41;](../mdx/mdx-operator-reference-mdx.md)   
 [Operatoren &#40; MDX-Syntax &#41;](../mdx/operators-mdx-syntax.md)  
  
  

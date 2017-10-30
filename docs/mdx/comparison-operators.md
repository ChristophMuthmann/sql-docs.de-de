---
title: Vergleichsoperatoren | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
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
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 5c022d67e874ebd333d8634e642d17a14d0b577f
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="comparison-operators"></a>Vergleichsoperatoren
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Sie verwenden Vergleichsoperatoren mit skalaren Daten. Sie können Vergleichsoperatoren in jedem MDX-Ausdruck (Multidimensional Expressions) verwenden.  
  
 Um eine Bedingung zu überprüfen, können Sie auch Vergleichsoperatoren in MDX-Anweisungen und Funktionen, z. B. der MDX-Abfrage [IIf](../mdx/iif-mdx.md) Funktion. Wenn Sie mit Vergleichsoperatoren eine Bedingung überprüfen und dann anhand dieser Bedingung Daten ändern möchten, sollten Sie sich vorher allerdings vergewissern, dass Sie die entsprechenden Berechtigungen haben. Jeder Benutzer, der Zugriff auf die tatsächlichen Daten hat und diese Daten abfragen kann, kann Vergleichsoperatoren in zusätzlichen Abfragen verwenden. Dieser Zugriff bedeutet aber nicht, dass diese Benutzer die entsprechenden Berechtigungen zum Ändern von Daten haben oder haben sollten. Außerdem sollte, damit die Datenintegrität erhalten bleibt, die Anzahl der Benutzer beschränkt werden, die Daten abfragen und ändern können.  
  
 Vergleichsoperatoren ergeben einen booleschen Datentyp zurückgeben von "true" oder "false" auf das Ergebnis der getesteten Bedingung basiert.  
  
 MDX unterstützt die Vergleichsoperatoren, die in der folgenden Tabelle aufgelistet sind.  
  
|Operator|Description|  
|--------------|-----------------|  
|[= (Gleich)](../mdx/equal-to-mdx.md)|Gibt für Argumente, die nicht NULL enthalten, TRUE zurück, wenn das linke Argument gleich dem rechten Argument ist. Gibt andernfalls FALSE zurück.<br /><br /> Wenn mindestens eines der Argumente zu einem NULL-Wert ausgewertet wird, gibt der Operator einen NULL-Wert zurück, es sei denn, der Vergleich `0=null` wird ausgeführt; in diesem Fall enthält der boolesche Wert TRUE.|  
|[<> (Ungleich)](../mdx/not-equal-to-mdx.md)|Gibt für Argumente, die nicht NULL enthalten, TRUE zurück, wenn das linke Argument ungleich dem rechten Argument ist. Gibt andernfalls FALSE zurück.<br /><br /> Wenn mindestens eines der Argumente zu einem NULL-Wert ausgewertet wird, gibt der Operator einen NULL-Wert zurück.|  
|[> (Größer als)](../mdx/greater-than-mdx.md)|Gibt für Argumente, die nicht NULL enthalten, TRUE zurück, wenn das linke Argument einen Wert hat, der größer ist als der Wert des rechten Arguments. Gibt andernfalls FALSE zurück.<br /><br /> Wenn mindestens eines der Argumente zu einem NULL-Wert ausgewertet wird, gibt der Operator einen NULL-Wert zurück.|  
|[> = (größer als oder gleich)](../mdx/greater-than-or-equal-to-mdx.md)|Gibt für Argumente, die nicht NULL enthalten, TRUE zurück, wenn das linke Argument einen Wert hat, der größer gleich dem Wert des rechten Arguments ist. Gibt andernfalls FALSE zurück.<br /><br /> Wenn mindestens eines der Argumente zu einem NULL-Wert ausgewertet wird, gibt der Operator einen NULL-Wert zurück.|  
|[< (Kleiner als)](../mdx/less-than-mdx.md)|Gibt für Argumente, die nicht NULL enthalten, TRUE zurück, wenn das linke Argument einen Wert hat, der kleiner ist als der Wert des rechten Arguments. Gibt andernfalls FALSE zurück.<br /><br /> Wenn mindestens eines der Argumente zu einem NULL-Wert ausgewertet wird, gibt der Operator einen NULL-Wert zurück.|  
|[< = (kleiner als oder gleich)](../mdx/less-than-or-equal-to-mdx.md)|Gibt für Argumente, die nicht NULL enthalten, TRUE zurück, wenn das linke Argument einen Wert hat, der kleiner gleich dem Wert des rechten Arguments ist. Gibt andernfalls FALSE zurück.<br /><br /> Wenn mindestens eines der Argumente zu einem NULL-Wert ausgewertet wird, gibt der Operator einen NULL-Wert zurück.|  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Operatorreferenz &#40; MDX &#41;](../mdx/mdx-operator-reference-mdx.md)   
 [Operatoren &#40; MDX-Syntax &#41;](../mdx/operators-mdx-syntax.md)  
  
  


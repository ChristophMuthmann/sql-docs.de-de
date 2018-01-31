---
title: Operatoren (SSIS-Ausdruck) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: expressions
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SSIS, operators
- SQL Server Integration Services, operators
- operators [Integration Services]
- expressions [Integration Services], operators
ms.assetid: 33df3a3d-1f5c-429b-a3b9-52b7d8689089
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: e38f6c1b3238371219c4be55d8da8d5c9b019bb2
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="operators-ssis-expression"></a>Operatoren (SSIS-Ausdruck)
  In diesem Abschnitt werden die von der Ausdruckssprache bereitgestellten Operatoren sowie die Operatorenrangfolge und die Assoziativität der Ausdrucksauswertung beschrieben.  
  
 In der folgenden Tabelle sind Themen zu Operatoren in diesem Abschnitt aufgeführt.  
  
|Operator|Description|  
|--------------|-----------------|  
|[CAST &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/cast-ssis-expression.md)|Konvertiert einen Ausdruck in einen anderen Datentyp.|  
|[&#40;&#41; &#40;Klammern&#41; &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/parentheses-ssis-expression.md)|Identifiziert die Auswertungsreihenfolge von Ausdrücken.|  
|[+ &#40;Addieren&#41; &#40;SSIS&#41;](../../integration-services/expressions/add-ssis.md)|Addiert zwei numerische Ausdrücke.|  
|[+ &#40;Verketten&#41; &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/concatenate-ssis-expression.md)|Verkettet zwei Ausdrücke.|  
|[- &#40;Subtrahieren&#41; &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/subtract-ssis-expression.md)|Subtrahiert den zweiten numerischen Ausdruck vom ersten.|  
|[- &#40;Negation&#41; &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/negate-ssis-expression.md)|Negiert einen numerischen Ausdruck.|  
|[&#42; &#40;Multiplizieren&#41; &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/multiply-ssis-expression.md)|Multipliziert zwei numerische Ausdrücke.|  
|[/ (Division) &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/divide-ssis-expression.md)|Dividiert den ersten numerischen Ausdruck durch den zweiten numerischen Ausdruck.|  
|[% &#40;Modulo&#41; &#40;SSIS-Ausdrücke&#41;](../../integration-services/expressions/modulo-ssis-expression.md)|Stellt den ganzzahligen Rest einer Division des ersten numerischen Ausdrucks durch den zweiten bereit.|  
|[&#124;&#124; &#40;Logisches OR&#41; &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/logical-or-ssis-expression.md)|Führt eine logische OR-Operation aus.|  
|[&& &#40;Logisches AND&#41; &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/logical-and-ssis-expression.md)|Führt eine logische AND-Operation aus.|  
|[\! &#40;Logisches Not&#41; &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/logical-not-ssis-expression.md)|Negiert einen booleschen Operanden.|  
|[&#124; &#40;Bitweises inklusives OR&#41; &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/bitwise-inclusive-or-ssis-expression.md)|Führt eine bitweise OR-Operation mit zwei ganzzahligen Werten aus.|  
|[^ &#40;Bitweises exklusives OR&#41; &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/bitwise-exclusive-or-ssis-expression.md)|Führt eine bitweise exklusive OR-Operation mit zwei ganzzahligen Werten aus.|  
|[& &#40;Bitweises AND&#41; &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/bitwise-and-ssis-expression.md)|Führt eine bitweise AND-Operation mit zwei ganzzahligen Werten aus.|  
|[~ &#40;Bitweises Not&#41; &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/bitwise-not-ssis-expression.md)|Führt eine bitweise Negation einer ganzen Zahl aus.|  
|[== &#40;Gleich&#41; &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/equal-ssis-expression.md)|Führt einen Vergleich aus, um zu ermitteln, ob zwei Ausdrücke gleich sind.|  
|[\!= &#40;Ungleich&#41; &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/unequal-ssis-expression.md)|Führt einen Vergleich aus, um zu ermitteln, ob zwei Ausdrücke ungleich sind.|  
|[&#62; &#40;Größer als&#41; &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/greater-than-ssis-expression.md)|Führt einen Vergleich aus, um zu ermitteln, ob der erste Ausdruck größer ist als der zweite.|  
|[&#60; &#40;Kleiner als&#41; &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/less-than-ssis-expression.md)|Führt einen Vergleich aus, um zu ermitteln, ob der erste Ausdruck kleiner ist als der zweite.|  
|[&#62;= &#40;Größer oder gleich&#41; &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/greater-than-or-equal-to-ssis-expression.md)|Führt einen Vergleich aus, um zu ermitteln, ob der erste Ausdruck größer oder gleich dem zweiten Ausdruck ist.|  
|[&#60;= &#40;Kleiner oder gleich&#41; &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/less-than-or-equal-to-ssis-expression.md)|Führt einen Vergleich aus, um zu ermitteln, ob der erste Ausdruck kleiner oder gleich dem zweiten Ausdruck ist.|  
|[? : &#40;Bedingt&#41; &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/conditional-ssis-expression.md)|Gibt einen von zwei Ausdrücken basierend auf der Auswertung eines booleschen Ausdrucks zurück.|  
  
 Informationen zum Platzieren der Operatoren in der Rangfolgenhierarchie finden Sie unter [Operator Precedence and Associativity](../../integration-services/expressions/operator-precedence-and-associativity.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Funktionen &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/functions-ssis-expression.md)   
 [Beispiele für erweiterte SQL Server Integration Services-Ausdrücke](../../integration-services/expressions/examples-of-advanced-integration-services-expressions.md)   
 [Integration Services-Ausdrücke &#40;SSIS&#41;](../../integration-services/expressions/integration-services-ssis-expressions.md)  
  
  

---
title: "Operatoren in Ausdrücken (Berichts-Generator und SSRS) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d22dc8b6-4353-40e7-91a1-65e8dae6325d
caps.latest.revision: "8"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 0507f28c6850aeab6a691ec594bdbf7e02423c81
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="operators-in-expressions-report-builder-and-ssrs"></a>Operatoren in Ausdrücken (Berichts-Generator und SSRS)
  Ein Operator ist ein Symbol, das Aktionen darstellt, die auf einen oder mehrere Begriffe in einem Ausdruck angewendet werden. Die folgenden Operatorkategorien werden in einem Ausdruck unterstützt: Arithmetik, Vergleich, Verkettung, logisch oder bitweise und Bitverschiebung  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="arithmetic"></a>Arithmetik  
 Arithmetische Operatoren führen mathematische Vorgänge für zwei numerische Begriffe in einem Ausdruck aus.  
  
|Operator|Description|  
|--------------|-----------------|  
|^|Erhebt eine Zahl zur Potenz einer anderen Zahl.|  
|*|Multipliziert zwei Zahlen.|  
|/|Dividiert zwei Zahlen und gibt ein Gleitkommaergebnis zurück.|  
|\|Dividiert zwei Zahlen und gibt eine ganze Zahl als Ergebnis zurück.|  
|Mod|Gibt den ganzzahligen Rest einer Division zurück. Beispiel: 7 Mod 5 = 2 (der Rest von 7 geteilt durch 5 ist 2).|  
|+|Addiert zwei Zahlen.|  
|-|Gibt die Differenz zwischen zwei Zahlen zurück oder gibt den negativen Wert eines numerischen Begriffs an.|  
  
### <a name="comparison"></a>Vergleich  
 Vergleichsoperatoren testen, ob zwei Ausdrücke gleichwertig sind.  
  
|Operator|Description|  
|--------------|-----------------|  
|<|Kleiner als.|  
|\<=|Kleiner oder gleich.|  
|>|Größer als.|  
|>=|Größer oder gleich.|  
|=|Gleich.|  
|<>|Ungleich.|  
|Wie|Bestimmt, ob eine bestimmte Zeichenfolge mit einem angegebenen Muster übereinstimmt. Ein Muster kann normale Zeichen und Platzhalterzeichen einschließen. Bei einem Mustervergleich müssen normale Zeichen exakt mit den angegebenen Zeichen in der Zeichenfolge übereinstimmen. Platzhalterzeichen können jedoch mit beliebigen Teilen der Zeichenfolge übereinstimmen. Das Verwenden der Vergleichsoperatoren für Zeichenfolgen = und != ist nicht so flexibel wie das Verwenden von Platzhalterzeichen mit dem LIKE-Operator.<br /><br /> In der folgenden Tabelle werden die Zeichen aufgelistet, die als Platzhalterzeichen verwendet werden können:<br /><br /> %: Eine Zeichenfolge mit null oder mehr Zeichen.<br /><br /> _: Ein einzelnes Zeichen.<br /><br /> [ ]: Ein einzelnes Zeichen innerhalb des angegebenen Bereichs (z. B. [a-f]) oder der festgelegten Gruppe (z. B. [aeiou]).<br /><br /> [^]: Ein einzelnes Zeichen, das nicht innerhalb des angegebenen Bereichs (z. B. [^a-f]) oder der festgelegten Gruppe (z. B. [^aeiou]) liegt.|  
|Is|Vergleicht zwei Objektverweise.|  
  
### <a name="string-concatenation"></a>Verketten von Zeichenfolgen  
 Mit der Zeichenfolgenverkettung wird die zweite Zeichenfolge in einem Ausdruck an die erste Zeichenfolge angefügt. Verwenden Sie für andere Zeichenfolgenoperationen integrierte Funktionen.  
  
|Operator|Description|  
|--------------|-----------------|  
|&|Verkettet zwei Zeichenfolgen.|  
|+|Verkettet zwei Zeichenfolgen.|  
  
### <a name="logical-and-bitwise"></a>Logisch und bitweise  
 Logische und bitweise Operatoren führen logische Manipulationen zwischen zwei ganzzahligen Begriffen in einem Ausdruck aus.  
  
|Operator|Description|  
|--------------|-----------------|  
|And|Führt eine logische Konjunktion zweier boolescher Ausdrücke oder eine bitweise Konjunktion zweier numerischer Ausdrücke aus.|  
|Not|Führt eine logische Negation eines booleschen Ausdrucks oder eine bitweise Negation eines numerischen Ausdrucks aus.|  
|oder|Führt eine logische Disjunktion zweier boolescher Ausdrücke oder eine bitweise Disjunktion zweier numerischer Werte aus.|  
|Xor|Führt einen logischen Ausschluss zweier boolescher Ausdrücke oder einen bitweisen Ausschluss zweier numerischer Ausdrücke durch.|  
|AndAlso|Führt eine logische Konjunktion zweier Ausdrücke durch.|  
|OrElse|Führt eine logische Disjunktion zweier Ausdrücke durch.|  
  
### <a name="bit-shift"></a>Bitverschiebung  
 Bitweise Operatoren führen Bitmanipulationen zwischen zwei ganzzahligen Begriffen in einem Ausdruck aus.  
  
|Operator|Description|  
|--------------|-----------------|  
|<\<|Führt eine arithmetische Verschiebung nach links für ein Bitmuster aus.|  
|>>|Führt eine arithmetische Verschiebung nach rechts für ein Bitmuster aus.|  
  
## <a name="see-also"></a>Siehe auch  
 [Ausdruck (Dialogfeld)](http://msdn.microsoft.com/library/e6c74ccb-4594-4d4f-b958-618d710e34eb)   
 [Ausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [Beispiele für Ausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Datentypen in Ausdrücken (Berichts-Generator und SSRS)](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Dialogfeld „Ausdruck“ (Berichts-Generator)](http://msdn.microsoft.com/library/e89c4d97-5d41-4b55-8695-79329edac15d)  
  
  

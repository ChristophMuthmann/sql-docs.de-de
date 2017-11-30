---
title: Operatoren (MDX-Syntax) | Microsoft Docs
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
helpviewer_keywords:
- Multidimensional Expressions [Analysis Services], operators
- operators [MDX]
- precedence [MDX]
- MDX [Analysis Services], operators
ms.assetid: 1ff5a529-88fd-4619-86e1-19fa214650d6
caps.latest.revision: "29"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: f7d13bdd9c8d5abd19e6b64d92e45bcd688feeef
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="operators-mdx-syntax"></a>Operatoren (MDX-Syntax)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  In MDX (Multidimensional Expressions) können Sie mit Operatoren die folgenden Aktionen ausführen:  
  
-   Ändern von Daten, temporär oder dauerhaft.  
  
-   Suchen nach Werten oder Objekten, die mit einer angegebenen Bedingung übereinstimmen.  
  
-   Implementieren einer Entscheidung zwischen Werten oder Ausdrücken.  
  
-   Testen hinsichtlich bestimmter Bedingungen vor dem Beginn einer Transaktion oder dem Ausführen eines Commits für eine Transaktion bzw. vor dem Ausführen bestimmter Anweisungen.  
  
 MDX unterstützt die Operatoren, die in der folgenden Tabelle aufgelistet sind:  
  
|Art der auszuführenden Operation|Verwenden Sie|  
|---------------------------------------|---------|  
|Weist einen Wert zu einer Variablen oder zuordnen eine Resultsetspalte zu einem Alias.|[Assignment Operators (Zuweisungsoperatoren)](../mdx/assignment-operators.md)|  
|Addition, Subtraktion, Multiplikation, Division.|[Arithmetic Operators (Arithmetische Operatoren)](../mdx/arithmetic-operators.md)|  
|Testen, ob eine Bedingung wahr ist (z. B. AND, OR, NOT oder XOR).|[Bitwise Operators (Bitweise Operatoren)](../mdx/bitwise-operators.md)|  
|Vergleichen eines Werts mit einem anderen Wert oder einem Ausdruck.|[Comparison Operators (Vergleichsoperatoren)](../mdx/comparison-operators.md)|  
|Dauerhaftes oder temporäres Kombinieren von zwei Zeichenfolgen zu einer Zeichenfolge.|[Concatenation Operators (Verkettungsoperatoren)](../mdx/concatenation-operators.md)|  
|Dauerhaftes oder temporäres Kombinieren von zwei Mengenausdrücken zu einer Menge.|[Set Operators (Mengenoperatoren)](../mdx/set-operators.md)|  
|Ausführen einer Operation für einen Operanden.|[Unary Operators (Unäre Operatoren)](../mdx/unary-operators.md)|  
  
> [!NOTE]  
>  In Abfragen kann jeder Benutzer Operationen ausführen, sofern die Daten in dem Cube, der mit einem Operator verwendet werden soll, für diesen Benutzer sichtbar sind. Sie benötigen allerdings die entsprechenden Berechtigungen, um die Daten erfolgreich ändern zu können.  
  
 Wenn mehrere Operatoren verwendet werden, spielt die Reihenfolge eine Rolle, in der MDX die Operatoren auswertet. Darüber hinaus kann es für das Verwenden von Operatoren erforderlich sein, dass ein Datentyp in einen anderen Datentyp konvertiert wird, bevor die Operatoren ausgewertet werden können.  
  
## <a name="evaluating-complex-expressions"></a>Auswerten von komplexen Ausdrücken  
 Sie können einen Ausdruck erstellen, indem Sie Operatoren dazu verwenden, mehrere kleinere Ausdrücke zu kombinieren. In solchen komplexen Ausdrücken wertet MDX die Operatoren in Abhängigkeit von der Definition der Operatorenrangfolge von [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. MDX führt Operatoren mit einer höheren Position in der Rangfolge vor Operatoren mit einer niedrigeren Position in der Rangfolge aus.  
  
### <a name="understanding-operator-precedence"></a>Grundlegendes zur Rangfolge von Operatoren  
 Die folgende Liste zeigt die Operatorenrangfolge (vom höchsten bis zum niedrigsten Operator). Operatoren, die in derselben Zeile stehen, sind in der Rangfolge gleichwertig und werden von links nach rechts ausgewertet, es sei denn, durch Klammern wird eine andere Reihenfolge erzwungen:  
  
-   IS  
  
-   AS  
  
-   DISTINCT  
  
-   :  
  
-   ^  
  
-   /, *  
  
-   +, -  
  
-   EXISTING  
  
-   <>, >=, =, \<=, >, <  
  
-   NICHT  
  
-   AND  
  
-   XOR  
  
-   oder  
  
 Weitere Informationen zu Operatoren in MDX finden Sie unter [MDX-Operatorreferenz &#40; MDX &#41; ](../mdx/mdx-operator-reference-mdx.md).  
  
### <a name="determining-results"></a>Bestimmen von Ergebnissen  
 Wenn Sie einfache Ausdrücke zu einem komplexen Ausdruck kombinieren, wird der Datentyp des sich ergebenden Werts bestimmt, indem die Regeln für die Operatoren mit den Regeln für die Rangfolge der Datentypen kombiniert werden.  
  
 Wenn das Ergebnis ein Zeichen- oder ein Unicode-Wert ist, wird die Sortierung des Ergebnisses bestimmt, indem die Regeln für die Operatoren mit den Regeln für die Sortierungsrangfolge kombiniert werden. Weitere Informationen zu Sortierungen finden Sie unter [Sprachen und Sortierungen &#40; Analysis Services &#41; ](../analysis-services/languages-and-collations-analysis-services.md).  
  
 Es gibt auch Regeln, die die Genauigkeit, Dezimalstellen und Länge des Ergebnisses basierend auf der Genauigkeit, Dezimalstellen und Länge der einfachen Ausdrücke festlegen.  
  
## <a name="converting-data-types"></a>Konvertieren von Datentypen  
 MDX konvertiert den Datentyp eines Objekts implizit in einen anderen Datentyp, wenn das Objekt in einem Ausdruck verwendet wird, der einen anderen Typ erfordert. In der folgenden Tabelle werden die Konvertierungsregeln für jedes Objekt aufgelistet.  
  
|Ursprünglicher Typ|Benötigter Typ|Konvertierung|  
|-------------------|-----------------|----------------|  
|Ebene|Legen Sie|\<Ebene > .members|  
|Hierarchy|Member|\<Hierarchie > .defaultmember|  
|Member|Tupel|(\<Member >)|  
|Tupel|Member|\<Tupel > .item(0)|  
|Tupel|Skalarwert|\<Tupel > .value|  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Operatorreferenz &#40; MDX &#41;](../mdx/mdx-operator-reference-mdx.md)   
 [MDX-Syntaxelemente &#40; MDX &#41;](../mdx/mdx-syntax-elements-mdx.md)  
  
  

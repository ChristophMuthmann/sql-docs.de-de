---
title: Arbeiten mit leeren Werten | Microsoft Docs
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
- expressions [MDX], empty values
- empty values [MDX]
ms.assetid: 6338fb85-f513-4c3e-a774-4fd7c6986a91
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: aef26d6b575ca340111054824fe024e81c6f7115
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="working-with-empty-values"></a>Arbeiten mit leeren Werten
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ein leerer Wert kennzeichnet, dass ein bestimmtes Element, ein bestimmtes Tupel oder eine bestimmte Zelle leer ist. Ein leerer Zellenwert kennzeichnet entweder, dass die Daten für die angegebene Zelle in der zugrunde liegenden Faktentabelle nicht gefunden wurden, oder, dass das Tupel für die angegebene Zelle einer Kombination aus Elementen entspricht, die für den Cube nicht anwendbar ist.  
  
> [!NOTE]  
>  Ein leerer Wert ist zwar nicht mit dem Wert 0 identisch, wird aber meistens wie der Wert 0 behandelt.  
  
 Die folgende Abfrage veranschaulicht das Verhalten von leeren Werten und von 0-Werten:  
  
```  
WITH  
//A calculated Product Category that always returns 0  
MEMBER [Product].[Category].[All Products].ReturnZero AS 0  
//Will return true for any null value  
MEMBER MEASURES.ISEMPTYDemo AS ISEMPTY([Measures].[Internet Tax Amount])  
//Will true for any null or zero value  
//To be clear: the expression 0=null always returns true in MDX  
MEMBER MEASURES.IsZero AS [Measures].[Internet Tax Amount]=0  
SELECT  
{[Measures].[Internet Tax Amount],MEASURES.ISEMPTYDemo,MEASURES.IsZero}  
ON COLUMNS,  
[Product].[Category].[Category].ALLMEMBERS  
ON ROWS  
FROM [Adventure Works]  
WHERE([Date].[Calendar].[Calendar Year].&[2001])  
```  
  
 Die folgenden Informationen gelten für leere Werte:  
  
-   Die [IsEmpty](../mdx/isempty-mdx.md) -Funktion gibt **"true"** nur, wenn die Zelle, die durch das in der Funktion angegebenen Tupel identifiziert leer ist. Die Funktion hingegen gibt **"false"**.  
  
    > [!NOTE]  
    >  Die **IsEmpty** -Funktion kann nicht feststellen, ob ein Elementausdruck einen null-Wert zurückgibt. Um zu bestimmen, ob ein null-Element aus einem Ausdruck zurückgegeben wird, verwenden die [IS](../mdx/is-mdx.md)Operator.  
  
-   Ist der leere Zellwert ein Operand für einen der numerischen Operatoren (+, -, *, /), wird der leere Zellwert als 0 behandelt, wenn der andere Operand ein nicht leerer Wert ist. Sind beide Operanden leer, gibt der numerische Operator den leeren Zellwert zurück.  
  
-   Ist der leere Zellwert ein Operand für den Operator für Zeichenfolgenverkettungen (+), wird der leere Zellwert als leere Zeichenfolge behandelt, wenn der andere Operand ein nicht leerer Wert ist. Sind beide Operanden leer, gibt der Operator für Zeichenfolgenverkettungen den leeren Zellwert zurück.  
  
-   Wenn der leere Zellwert ein Operand für einen der Vergleichsoperatoren (=. <>, > =, \<=, >, <), wird der leere Zellwert als 0 (null) behandelt, oder ist eine leere Zeichenfolge ist, je nachdem, ob der Datentyp des anderen Operanden numerisch oder String. Sind beide Operanden leer, werden beide als 0 behandelt.  
  
-   Beim Sortieren numerischer Werte nimmt der leere Zellwert dieselbe Stelle ein wie die Zahl Null. Bei der Sortierung zwischen dem leeren Zellwert und null wird der leere Zellwert vor null eingeordnet.  
  
-   Beim Sortieren von Zeichenfolgenwerten nimmt der leere Zellwert dieselbe Stelle ein wie die leere Zeichenfolge. Bei der Sortierung zwischen dem leeren Zellwert und der leeren Zeichenfolge wird der leere Zellwert vor der leeren Zeichenfolge eingeordnet.  
  
## <a name="dealing-with-empty-values-in-mdx-statements-and-cubes"></a>Umgehen mit leeren Werten in MDX-Anweisungen und Cubes  
 In MDX-Anweisungen (Multidimensional Expressions) können Sie nach leeren Werten suchen und dann bestimmte Berechnungen für Zellen ausführen, die gültige (also nicht leere) Daten enthalten. Das Entfernen von leeren Werten aus Berechnungen kann wichtig sein, da bestimmte Berechnungen (z. B. eine Durchschnittsberechnung) verfälscht werden können, wenn leere Zellwerte eingeschlossen werden.  
  
 Leere Werte, die in den Daten der zugrundeliegenden Faktentabelle gespeichert sind, werden bei der Verarbeitung des Cube standardmäßig in 0 konvertiert. Sie können die **Null-Verarbeitung** Option für ein Measure, um zu steuern, ob null Fakten in 0 konvertiert werden, einen leeren Wert oder sogar löst einen Fehler bei der Verarbeitung konvertierten. Wenn Sie nicht möchten, dass die Abfrageergebnisse leere Zellenwerte enthalten, erstellen Sie Abfragen, berechnete Elemente oder MDX-Skriptanweisungen, die leere Werte entweder ausschließen oder durch einen anderen Wert ersetzen.  
  
 Um leere Zeilen oder Spalten aus einer Abfrage zu entfernen, können Sie vor der Achsmengendefinition die NON EMPTY-Anweisung verwenden. Die folgende Beispielabfrage gibt nur die Produktkategorie „Bikes“ zurück, da dies die einzige Kategorie ist, die im Kalenderjahr 2001 verkauft wurde.  
  
 `SELECT`  
  
 `{[Measures].[Internet Tax Amount]}`  
  
 `ON COLUMNS,`  
  
 `//Comment out the following line to display all the empty rows for other Categories`  
  
 `NON EMPTY`  
  
 `[Product].[Category].[Category].MEMBERS`  
  
 `ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 `WHERE([Date].[Calendar].[Calendar Year].&[2001])`  
  
 Um leere Tupel aus einer Menge zu entfernen, können Sie grundsätzlich die NonEmpty-Funktion verwenden. Die folgende Abfrage zeigt zwei berechnete Measures. Eines zählt die Produktkategorien, während das andere die Anzahl der Produktkategorien anzeigt, die Werte für Measure [Internet Tax Amount] und das Kalenderjahr 2001 enthalten:  
  
 `WITH`  
  
 `MEMBER MEASURES.CategoryCount AS`  
  
 `COUNT([Product].[Category].[Category].MEMBERS)`  
  
 `MEMBER MEASURES.NonEmptyCategoryCountFor2001 AS`  
  
 `COUNT(`  
  
 `NONEMPTY(`  
  
 `[Product].[Category].[Category].MEMBERS`  
  
 `,([Date].[Calendar].[Calendar Year].&[2001], [Measures].[Internet Tax Amount])`  
  
 `))`  
  
 `SELECT`  
  
 `{MEASURES.CategoryCount,MEASURES.NonEmptyCategoryCountFor2001 }`  
  
 `ON COLUMNS`  
  
 `FROM [Adventure Works]`  
  
 Weitere Informationen finden Sie unter [NonEmpty &#40; MDX &#41; ](../mdx/nonempty-mdx.md).  
  
## <a name="empty-values-and-comparison-operators"></a>Leere Werte und Vergleichsoperatoren  
 Sind leere Werte in den Daten vorhanden, ist es möglich, dass logische Operatoren und Vergleichsoperatoren nicht nur TRUE oder FALSE zurückgeben, sondern ein drittes Ergebnis: EMPTY. Diese Notwendigkeit einer dreiwertigen Logik ist die Ursache für zahlreiche Anwendungsfehler. In den folgenden Tabellen wird dargestellt, welche Auswirkungen die Einführung von Vergleichen zwischen leeren Werten haben kann.  
  
 Die folgende Tabelle zeigt die Ergebnisse des Anwendens eines AND-Operators auf zwei boolesche Operanden.  
  
|AND|TRUE|EMPTY|FALSE|  
|---------|----------|-----------|-----------|  
|**"TRUE"**|TRUE|FALSE|FALSE|  
|**LEERE**|FALSE|EMPTY|FALSE|  
|**"FALSE"**|FALSE|FALSE|FALSE|  
  
 Diese Tabelle zeigt die Ergebnisse des Anwendens eines OR-Operators auf zwei boolesche Operanden.  
  
|OR|TRUE|FALSE|  
|--------|----------|-----------|  
|**"TRUE"**|TRUE|TRUE|  
|**LEERE**|TRUE|TRUE|  
|**"FALSE"**|TRUE|FALSE|  
  
 Diese Tabelle zeigt, wie der NOT-Operator negiert oder umkehrt, das Ergebnis eines booleschen Operators.  
  
|Boolescher Ausdruck, auf den der NOT-Operator angewendet wird|Auswertungsergebnis|  
|-------------------------------------------------------------|------------------|  
|TRUE|FALSE|  
|EMPTY|EMPTY|  
|FALSE|TRUE|  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)   
 [MDX-Operatorreferenz &#40; MDX &#41;](../mdx/mdx-operator-reference-mdx.md)   
 [Ausdrücke &#40; MDX &#41;](../mdx/expressions-mdx.md)  
  
  


---
title: Rangfolge von Sortierungen (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- coercible-default collation label
- precedence [SQL Server], collations
- collation sensitive
- collations [SQL Server], precedence
- explicit collation label [SQL Server]
- implicit collation label
- no-collation label
- collation insensitive
- operators [Transact-SQL], collations
- collation labels
- collation coercion rules
- rules [SQL Server], collations
ms.assetid: 58c4e64b-5634-4c29-aa22-33193282dd27
caps.latest.revision: "34"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d80966502f5538989f3615658e3766e8c3e718f2
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="collation-precedence-transact-sql"></a>Rangfolge von Sortierungen (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Mit der Rangfolge von Sortierungen, die auch als Sortierungsprioritätsregeln bezeichnet werden, wird Folgendes festgelegt:  
  
-   Die Sortierung des endgültigen Ergebnisses eines Ausdrucks, der zu einer Zeichenfolge ausgewertet wird.  
  
-   Die Sortierung, die von sortierungsabhängigen Operatoren verwendet wird, die Zeichenfolgen als Eingabe verwenden, jedoch keine Zeichenfolge zurückgeben, z. B. LIKE und IN.  
  
 Die sortierungsprioritätsregeln gelten nur für die Zeichenfolgen-Datentypen: **Char**, **Varchar**, **Text**, **Nchar**, **Nvarchar**, und **Ntext**. Objekte mit anderen Datentypen werden in Sortierungsbewertungen nicht einbezogen.  
  
## <a name="collation-labels"></a>Sortierungsbezeichnungen  
 In der folgenden Tabelle werden die vier Kategorien mit den jeweiligen Sortierungen aller Objekte aufgelistet und beschrieben. Der Name jeder Kategorie wird Sortierungsbezeichnung genannt.  
  
|Sortierungsbezeichnung|Typen von Objekten|  
|---------------------|----------------------|  
|Coercible-default|Alle [!INCLUDE[tsql](../../includes/tsql-md.md)]-Zeichenfolgenvariablen, Parameter, Literale oder die Ausgabe einer in einen Katalog integrierten Funktion oder einer integrierten Funktion, die keine Zeichenfolgeneingabe akzeptiert, jedoch eine Zeichenfolge ausgibt.<br /><br /> Wenn das Objekt in einer benutzerdefinierten Funktion, einer gespeicherten Prozedur oder einem Trigger deklariert ist, wird dem Objekt die Standardsortierung der Datenbank zugewiesen, in der die Funktion, die gespeicherte Prozedur oder der Trigger erstellt wurde. Wenn das Objekt in einem Batch deklariert ist, wird dem Objekt die Standardsortierung der aktuellen Datenbank für die Verbindung zugewiesen.|  
|Implicit X|Ein Spaltenverweis. Die Sortierung für den Ausdruck (X) wird von der Sortierung übernommen, die für die Spalte der Tabelle oder Sicht definiert ist.<br /><br /> Selbst wenn der Spalte explizit durch eine COLLATE-Klausel in der CREATE TABLE- oder CREATE VIEW-Anweisung eine Sortierung zugewiesen wurde, wird der Spaltenverweis als Implicit klassifiziert.|  
|Explicit X|Ein Ausdruck, der durch die Verwendung einer COLLATE-Klausel im Ausdruck explizit in eine bestimmte Sortierung (X) umgewandelt wird.|  
|No-collation|Zeigt an, dass der Wert eines Ausdrucks das Ergebnis eines Vorgangs zwischen zwei Zeichenfolgen ist, die konfliktverursachende Sortierungen mit der Sortierungsbezeichnung Implicit haben. Das Ergebnis des Ausdrucks hat definitionsgemäß keine Sortierung.|  
  
## <a name="collation-rules"></a>Sortierungsregeln  
 Die Sortierungsbezeichnung eines einfachen Ausdrucks, der nur auf ein Zeichenfolgenobjekt verweist, ist die Sortierungsbezeichnung des Objekts, auf das verwiesen wird.  
  
 Die Sortierungsbezeichnung eines komplexen Ausdrucks, der auf zwei Operandenausdrücke mit derselben Sortierungsbezeichnung verweist, ist die Sortierungsbezeichnung der Operandenausdrücke.  
  
 Für die Sortierungsbezeichnung des Endergebnisses eines komplexen Ausdrucks, der auf zwei Operandenausdrücke mit verschiedenen Sortierungen verweist, gelten die folgenden Regeln:  
  
-   Explicit hat Vorrang vor Implicit. Implicit hat Vorrang vor Coercible-default:  
  
     Explicit > Implicit > Coercible-default  
  
-   Durch Kombinieren von zwei Explicit-Ausdrücken, denen unterschiedliche Sortierungen zugewiesen wurden, wird ein Fehler erzeugt.  
  
     Explicit X + Explicit Y = Fehler  
  
-   Das Kombinieren von zwei Implicit-Ausdrücken mit unterschiedlichen Sortierungen ergibt ein Ergebnis ohne Sortierung (No-collation):  
  
     Implicit X + Implicit Y = No-collation  
  
-   Das Kombinieren eines Ausdrucks ohne Sortierung (No-collation) mit einem Ausdruck mit einer beliebigen Bezeichnung, lediglich ausgenommen einer expliziten Sortierung (Explicit) (siehe folgender Punkt), ergibt ein Ergebnis mit der Bezeichnung No-collation:  
  
     No-collation + beliebige Sortierung = No-collation  
  
-   Das Kombinieren eines Ausdrucks ohne Sortierung (No-collation) mit einem Ausdruck, der die Sortierung Explicit aufweist, ergibt einen Ausdruck mit der Bezeichnung Explicit.  
  
     No-collation + Explicit X = Explicit  
  
 In der folgenden Tabelle werden die Regeln zusammengefasst.  
  
|Prioritätsbezeichnung des Operanden|Explicit X|Implicit X|Coercible-default|No-collation|  
|----------------------------|----------------|----------------|------------------------|-------------------|  
|**EXPLICIT Y**|Ein Fehler wird erzeugt|Ergebnis ist Explicit Y|Ergebnis ist Explicit Y|Ergebnis ist Explicit Y|  
|**Implicit Y**|Ergebnis ist Explicit X|Ergebnis ist No-collation|Ergebnis ist Implicit Y|Ergebnis ist No-collation|  
|**Coercible-Standard**|Ergebnis ist Explicit X|Ergebnis ist Implicit X|Ergebnis ist Coercible-default|Ergebnis ist No-collation|  
|**No-collation**|Ergebnis ist Explicit X|Ergebnis ist No-collation|Ergebnis ist No-collation|Ergebnis ist No-collation|  
  
 Die folgenden zusätzlichen Regeln sind auch auf die Sortierungspriorität anwendbar:  
  
-   Sie können nicht mehrere COLLATE-Klauseln für einen Ausdruck festlegen, der bereits ein expliziter Ausdruck ist. Die folgende `WHERE`-Klausel ist beispielsweise ungültig, da für einen Ausdruck, der bereits ein expliziter Ausdruck ist, eine `COLLATE`-Klausel angegeben wurde:  
  
     `WHERE ColumnA = ( 'abc' COLLATE French_CI_AS) COLLATE French_CS_AS`  
  
-   Codepagekonvertierungen für **Text** Datentypen sind nicht zulässig. Sie können nicht umgewandelt eine **Text** Ausdruck von einer Sortierung in eine andere besäßen sie unterschiedliche Codepages. Der Zuweisungsoperator kann keine Werte zuweisen, wenn die Sortierung des rechten Textoperanden eine andere Codepage als die des linken Textoperanden besitzt.  
  
 Die Rangfolge von Sortierungen wird nach der Konvertierung der Datentypen bestimmt. Der Operand, von dem die resultierende Sortierung genommen wird, kann sich von dem Operanden unterscheiden, der den Datentyp für das Endergebnis bereitstellt. Betrachten Sie beispielsweise den folgenden Batch aus:  
  
```  
CREATE TABLE TestTab  
   (PrimaryKey int PRIMARY KEY,  
    CharCol char(10) COLLATE French_CI_AS  
   )  
  
SELECT *  
FROM TestTab  
WHERE CharCol LIKE N'abc'  
```  
  
 Der Unicode-Datentyp des einfachen Ausdrucks `N'abc'` besitzt eine höhere Datentyp-Rangfolge. Daher wird im sich ergebenden Ausdruck der Unicode-Datentyp `N'abc'` zugewiesen. Der Ausdruck `CharCol` hat jedoch die Sortierungsbezeichnung Implicit, während `N'abc'` die in der Priorität niedrigere Bezeichnung Coercible-default aufweist. Deshalb wird als Sortierung die `French_CI_AS`-Sortierung von `CharCol` verwendet.  
  
### <a name="examples-of-collation-rules"></a>Beispiele für Sortierungsregeln  
 Die folgenden Beispiele veranschaulichen die Funktionsweise der Sortierungsregeln. Erstellen Sie die folgende Testtabelle, um die Beispiele zu testen.  
  
```  
USE tempdb;  
GO  
  
CREATE TABLE TestTab (  
   id int,   
   GreekCol nvarchar(10) collate greek_ci_as,   
   LatinCol nvarchar(10) collate latin1_general_cs_as  
   )  
INSERT TestTab VALUES (1, N'A', N'a');  
GO  
```  
  
#### <a name="collation-conflict-and-error"></a>Sortierungskonflikt und Fehler  
 Das Prädikat in der folgenden Abfrage weist einen Sortierungskonflikt auf und generiert einen Fehler:  
  
```  
SELECT *   
FROM TestTab   
WHERE GreekCol = LatinCol;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Msg 448, Level 16, State 9, Line 2  
Cannot resolve collation conflict between 'Latin1_General_CS_AS' and 'Greek_CI_AS' in equal to operation.  
```  
  
#### <a name="explicit-label-vs-implicit-label"></a>Bezeichnung "Explicit" und Bezeichnung "Implicit"  
 Das Prädikat in der folgenden Abfrage wird zu `greek_ci_as` ausgewertet, da der rechte Ausdruck die Bezeichnung Explicit aufweist. Diese hat Vorrang vor der Bezeichnung Implicit des linken Ausdrucks.  
  
```  
SELECT *   
FROM TestTab   
WHERE GreekCol = LatinCol COLLATE greek_ci_as;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
id          GreekCol             LatinCol  
----------- -------------------- --------------------  
          1 A                    a  
  
(1 row affected)  
```  
  
#### <a name="no-collation-labels"></a>Bezeichnung No-Collation  
 Die `CASE`-Ausdrücke in den folgenden Abfragen weisen die Sortierungsbezeichnung No-collation auf; sie können deshalb nicht in der Auswahlliste angezeigt werden oder von sortierungsabhängigen Operatoren verwendet werden. Die Ausdrücke können jedoch von sortierungsunabhängigen Operatoren verwendet werden.  
  
```  
SELECT (CASE WHEN id > 10 THEN GreekCol ELSE LatinCol END)   
FROM TestTab;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Msg 451, Level 16, State 1, Line 1  
Cannot resolve collation conflict for column 1 in SELECT statement.  
```  
  
```  
SELECT PATINDEX((CASE WHEN id > 10 THEN GreekCol ELSE LatinCol END), 'a')  
FROM TestTab;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Msg 446, Level 16, State 9, Server LEIH2, Line 1  
Cannot resolve collation conflict for patindex operation.  
```  
  
```  
SELECT (CASE WHEN id > 10 THEN GreekCol ELSE LatinCol END) COLLATE Latin1_General_CI_AS   
FROM TestTab;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
--------------------  
a  
  
(1 row affected)  
```  
  
## <a name="collation-sensitive-and-collation-insensitive"></a>Sortierungsabhängig und sortierungsunabhängig  
 Operatoren und Funktionen sind sortierungsabhängig oder -unabhängig.  
  
 Sortierungsabhängig  
 Sortierungsabhängig bedeutet, dass das Angeben eines No-collation-Operanden zu einem Fehler während der Kompilierung führt. Das Ergebnis des Ausdrucks kann nicht No-collation lauten.  
  
 Sortierungsunabhängig  
 Sortierungsunabhängig bedeutet, dass die Operanden und das Ergebnis die Bezeichnung No-collation haben können.  
  
### <a name="operators-and-collation"></a>Operatoren und Sortierung  
 Die Vergleichsoperatoren und die Operatoren MAX, MIN, BETWEEN, LIKE und IN sind sortierungsabhängig. Der Zeichenfolge, die von den Operatoren verwendet wird, wird die Sortierungsbezeichnung des Operanden zugewiesen, der den höheren Rang hat. Der UNION-Operator ist ebenfalls sortierungsabhängig, und allen Zeichenfolgenoperanden und dem Endergebnis wird die Sortierung des Operanden mit dem höchsten Rang zugewiesen. Die Sortierungsrangfolge der UNION-Operanden und des Ergebnisses werden spaltenweise ausgewertet.  
  
 Der Zuweisungsoperator ist sortierungsabhängig, und der rechte Ausdruck wird in die linke Sortierung umgewandelt.  
  
 Der Operator für die Zeichenfolgenverkettung ist sortierungsabhängig, und den beiden Zeichenfolgenoperanden und dem Ergebnis wird die Sortierungsbezeichnung des Operanden mit dem höchsten Sortierungsrang zugewiesen. Der UNION ALL- und der CASE-Operator sind ebenfalls sortierungsunabhängig, und allen Zeichenfolgenoperanden und den Endergebnissen wird die Sortierungsbezeichnung des Operanden mit dem höchsten Rang zugewiesen. Die Sortierungsrangfolge der UNION ALL-Operanden und des Ergebnisses werden spaltenweise ausgewertet.  
  
### <a name="functions-and-collation"></a>Funktionen und Sortierung  
 DIE Funktionen CAST, CONVERT und COLLATE sind sortierungsabhängig für **Char**, **Varchar**, und **Text** -Datentypen. Wenn die Eingabe und die Ausgabe der Funktionen CAST und CONVERT Zeichenfolgen sind, hat die ausgegebene Zeichenfolge die Sortierungsbezeichnung der eingegebenen Zeichenfolge. Wenn die Eingabe keine Zeichenfolge ist, erhält die ausgegebene Zeichenfolge die Bezeichnung Coercible-default. Der Zeichenfolge wird die Sortierung der aktuellen Datenbank für die Verbindung oder die Sortierung der Datenbank zugewiesen, die die benutzerdefinierte Funktion, die gespeicherte Prozedur oder den Trigger enthält, in der bzw. dem auf die CAST- oder CONVERT-Funktion verwiesen wird.  
  
 Für integrierte Funktionen, die eine Zeichenfolge zurückgeben, jedoch keine Zeichenfolge als Eingabe verwenden, ist die Bezeichnung für die ausgegebene Zeichenfolge Coercible-default. Der Zeichenfolge wird die Sortierung der aktuellen Datenbank oder der Datenbank zugewiesen, die die benutzerdefinierte Funktion, die gespeicherte Prozedur oder den Trigger enthält, in der bzw. dem auf die Funktion verwiesen wird.  
  
 Die folgenden Funktionen sind sortierungsabhängig, und die entsprechenden ausgegebenen Zeichenfolgen weisen die Sortierungsbezeichnung der eingegebenen Zeichenfolge auf:  
  
|||  
|-|-|  
|CHARINDEX|REPLACE|  
|DIFFERENCE|REVERSE|  
|ISNUMERIC|RIGHT|  
|LEFT|SOUNDEX|  
|LEN|STUFF|  
|LOWER|SUBSTRING|  
|PATINDEX|GROSSBUCHSTABEN|  
  
## <a name="see-also"></a>Siehe auch  
 [COLLATE &#40;Transact-SQL&#41;](~/t-sql/statements/collations.md)   
 [Datentypkonvertierung &#40; Datenbankmodul &#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)   
 [Operatoren &#40; Transact-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [Ausdrücke &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
  
  

---
title: Suchbedingung (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 01/15/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- search
- Search Condition
- condition
dev_langs: TSQL
helpviewer_keywords:
- OR operator [Transact-SQL]
- CONTAINS predicate (Transact-SQL)
- ESCAPE keyword
- operators [Transact-SQL], search condition
- search conditions [SQL Server]
- WHERE clause, search conditions
- ALL keyword
- FREETEXT predicate (Transact-SQL)
- EXISTS keyword
- search conditions [SQL Server], about search conditions
- NOT operator [Transact-SQL]
- BETWEEN operator
- SOME | ANY keyword
- predicates [full-text search]
- AND, about search conditions
- logical operators [SQL Server], about search conditions
- precedence [SQL Server], logical operators
- logical operators [SQL Server], precedence
- LIKE comparisons
ms.assetid: 09974469-c5d2-4be8-bc5a-78e404660b2c
caps.latest.revision: "43"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: aff1f4010182b601111ed2ba892bb06b6e82b71d
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="search-condition-transact-sql"></a>Suchbedingung (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Bezeichnet eine Kombination aus einem oder mehreren Prädikaten, die die logischen Operatoren AND, OR und NOT verwenden.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
<search_condition> ::=   
    { [ NOT ] <predicate> | ( <search_condition> ) }   
    [ { AND | OR } [ NOT ] { <predicate> | ( <search_condition> ) } ]   
[ ,...n ]   
  
<predicate> ::=   
    { expression { = | < > | ! = | > | > = | ! > | < | < = | ! < } expression   
    | string_expression [ NOT ] LIKE string_expression   
  [ ESCAPE 'escape_character' ]   
    | expression [ NOT ] BETWEEN expression AND expression   
    | expression IS [ NOT ] NULL   
    | CONTAINS   
  ( { column | * } , '<contains_search_condition>' )   
    | FREETEXT ( { column | * } , 'freetext_string' )   
    | expression [ NOT ] IN ( subquery | expression [ ,...n ] )   
    | expression { = | < > | ! = | > | > = | ! > | < | < = | ! < }   
  { ALL | SOME | ANY} ( subquery )   
    | EXISTS ( subquery )     }   
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
< search_condition > ::=   
    { [ NOT ] <predicate> | ( <search_condition> ) }   
    [ { AND | OR } [ NOT ] { <predicate> | ( <search_condition> ) } ]   
[ ,...n ]   
  
<predicate> ::=   
    { expression { = | < > | ! = | > | > = | < | < = } expression   
    | string_expression [ NOT ] LIKE string_expression   
    | expression [ NOT ] BETWEEN expression AND expression   
    | expression IS [ NOT ] NULL   
    | expression [ NOT ] IN (subquery | expression [ ,...n ] )   
    | expression [ NOT ] EXISTS (subquery)     }   
```  
  
## <a name="arguments"></a>Argumente  
 \<search_condition>  
 Gibt die Bedingungen für die Zeilen an, die im Resultset einer SELECT-Anweisung, eines Abfrageausdrucks oder einer Unterabfrage zurückgegeben werden sollen. Bei einer UPDATE-Anweisung gibt dieses Argument die Bedingungen für die Zeilen an, die aktualisiert werden sollen. Bei einer DELETE-Anweisung gibt dieses Argument die Bedingungen für die Zeilen an, die gelöscht werden sollen. Es gibt keine Begrenzung für die Anzahl der Prädikate, die in einer Suchbedingung einer [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung enthalten sein können.  
  
 NICHT  
 Negiert den vom Prädikat festgelegten booleschen Ausdruck. Weitere Informationen finden Sie unter [nicht &#40; Transact-SQL &#41; ](../../t-sql/language-elements/not-transact-sql.md).  
  
 AND  
 Kombiniert zwei Bedingungen und gibt TRUE zurück, wenn beide Bedingungen TRUE sind. Weitere Informationen finden Sie unter [und &#40; Transact-SQL &#41; ](../../t-sql/language-elements/and-transact-sql.md).  
  
 OR  
 Kombiniert zwei Bedingungen und gibt TRUE zurück, wenn eine der Bedingungen TRUE ist. Weitere Informationen finden Sie unter [oder &#40; Transact-SQL &#41; ](../../t-sql/language-elements/or-transact-sql.md).  
  
 \<Prädikat >  
 Ein Ausdruck, der TRUE, FALSE oder UNKNOWN zurückgibt.  
  
 *expression*  
 Ein Spaltenname, eine Konstante, eine Funktion, eine Variable, eine skalare Unterabfrage oder eine Kombination aus Spaltennamen, Konstanten und Funktionen, die durch einen Operator bzw. Operatoren oder eine Unterabfrage miteinander verbunden sind. Der Ausdruck kann auch den CASE-Ausdruck enthalten.  
  
> [!NOTE]  
>  Nicht-Unicode-Zeichenfolgenkonstanten und Variablen verwenden die Codepage, die die standardsortierung der Datenbank entspricht. Seite Konvertierungen können sicherheitsbezogener Code, bei der Arbeit mit nur-Unicode-Zeichendaten und verweisen auf die nicht-Unicode-Zeichendatentypen **Char**, **Varchar**, und **Text**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Konvertiert von nicht-Unicode-Zeichenfolgenkonstanten und Variablen in die Codepage, die entspricht der Sortierung der Spalte, auf die verwiesen wird, oder Verwenden von COLLATE, angegeben, wenn diese Codepage von der Codepage unterscheidet, das die standardsortierung der Datenbank entspricht. Alle Zeichen in der neuen Codepage nicht gefunden werden zu einem ähnlichen Zeichen übersetzt werden, wenn eine [Zuordnung mit ähnlichen](http://www.unicode.org/Public/MAPPINGS/VENDORS/MICSFT/WindowsBestFit/) befinden, ansonsten werden in das standardersetzungszeichen der konvertiert wird "?".  
>  
> Bei der Arbeit mit mehreren Codepages Zeichenkonstanten können vorangestellt werden der Großbuchstabe n ", und Unicode-Variablen können verwendet werden, und um codepagekonvertierungen zu vermeiden.  
  
 =  
 Der Operator, mit dem die Gleichheit zwischen zwei Ausdrücken getestet wird.  
  
 <>  
 Der Operator, mit dem die Bedingung zweier Ausdrücke getestet wird, die nicht gleich sind  
  
 !=  
 Der Operator, mit dem die Bedingung zweier Ausdrücke getestet wird, die nicht gleich sind  
  
 \>  
 Der Operator, mit dem die Bedingung eines Ausdrucks getestet wird, der größer als der andere ist  
  
 \>=  
 Der Operator, mit dem die Bedingung eines Ausdrucks getestet wird, der größer oder gleich dem anderen Ausdruck ist  
  
 !>  
 Der Operator, mit dem die Bedingung eines Ausdrucks getestet wird, der nicht größer als der andere Ausdruck ist  
  
 <  
 Der Operator, mit dem die Bedingung eines Ausdrucks getestet wird, der kleiner als der andere ist  
  
 <=  
 Der Operator, mit dem die Bedingung eines Ausdrucks getestet wird, der kleiner oder gleich dem anderen Ausdruck ist  
  
 !<  
 Der Operator, mit dem die Bedingung eines Ausdrucks getestet wird, der nicht kleiner als der andere Ausdruck ist  
  
 *string_expression*  
 Eine Zeichenfolge mit Zeichen und Platzhalterzeichen  
  
 [ NOT ] LIKE  
 Zeigt an, dass die nachfolgende Zeichenfolge in Mustervergleichen verwendet werden soll. Weitere Informationen finden Sie unter [wie &#40; Transact-SQL &#41; ](../../t-sql/language-elements/like-transact-sql.md).  
  
 ESCAPE- **"***Escape_ Zeichen***"**  
 Ermöglicht einem Platzhalterzeichen, dass es in einer Zeichenfolge gesucht werden kann, statt als Platzhalter zu fungieren. *Escape_character* ist das Zeichen, das vor dem Platzhalterzeichen, um diese besondere Verwendung anzugeben eingefügt wird.  
  
 [ NOT ] BETWEEN  
 Gibt einen Inklusivbereich von Werten an. Verwenden Sie AND, um den Anfangs- und den Endwert voneinander zu trennen. Weitere Informationen finden Sie unter [BETWEEN &#40; Transact-SQL &#41; ](../../t-sql/language-elements/between-transact-sql.md).  
  
 IS [NOT] NULL  
 Gibt eine Suche nach NULL-Werten oder nach Werten ungleich Null in Abhängigkeit von den verwendeten Schlüsselwörtern an. Ein Ausdruck mit einem bitweisen oder arithmetischen Operator gibt NULL zurück, wenn einer der Operanden gleich NULL ist.  
  
 CONTAINS  
 Sucht Spalten mit zeichenbasierten Daten für präzise oder weniger präzise (*fuzzy*) Übereinstimmungen mit einzelnen Wörtern und Satzteilen, für den Abstand von Wörtern in einer bestimmten Entfernung voneinander sowie gewichtete Übereinstimmungen. Diese Option kann nur in Verbindung mit SELECT-Anweisungen verwendet werden. Weitere Informationen finden Sie unter [CONTAINS &#40; Transact-SQL &#41; ](../../t-sql/queries/contains-transact-sql.md).  
  
 FREETEXT  
 Stellt eine einfache Form der Abfrage in natürlicher Sprache dar, indem Spalten mit zeichenbasierten Daten im Hinblick auf Werte untersucht werden, die mit der Bedeutung übereinstimmen, statt dass die genauen Wörter im Prädikat gesucht werden. Diese Option kann nur in Verbindung mit SELECT-Anweisungen verwendet werden. Weitere Informationen finden Sie unter [FREETEXT &#40; Transact-SQL &#41; ](../../t-sql/queries/freetext-transact-sql.md).  
  
 [ NOT ] IN  
 Gibt die Suche nach einem Ausdruck an, die auf dem Einschluss oder Ausschluss des Ausdrucks in eine bzw. aus einer Liste basiert. Bei dem Suchausdruck kann es sich um eine Konstante oder einen Spaltennamen handeln. Die Liste kann eine Reihe von Konstanten oder in der Regel eine Unterabfrage sein. Schließen Sie die Liste der Werte in Klammern ein. Weitere Informationen finden Sie unter [IN &#40;Transact-SQL&#41;](../../t-sql/language-elements/in-transact-sql.md).  
  
 *subquery*  
 Kann eine eingeschränkte SELECT-Anweisung betrachtet werden und ähnelt \<Query_expresssion > in der SELECT-Anweisung. Die ORDER BY-Klausel und das INTO-Schlüsselwort sind nicht zulässig. Weitere Informationen finden Sie unter [SELECT &#40; Transact-SQL &#41; ](../../t-sql/queries/select-transact-sql.md).  
  
 ALL  
 Wird mit einem Vergleichsoperator und einer Unterabfrage verwendet. Gibt "true" für \<Prädikat > Wenn alle für die Unterabfrage abgerufenen Werte die Vergleichsoperation erfüllen, oder "false", wenn nicht alle Werte dem Vergleich entsprechen oder wenn die Unterabfrage keine Zeilen an die äußere Anweisung zurückgibt. Weitere Informationen finden Sie unter [alle &#40; Transact-SQL &#41; ](../../t-sql/language-elements/all-transact-sql.md).  
  
 { SOME | ANY }  
 Wird mit einem Vergleichsoperator und einer Unterabfrage verwendet. Gibt "true" für \<Prädikat > Wenn ausnahmslos abgerufen, für die Unterabfrage die Vergleichsoperation erfüllt, oder "false", wenn die Unterabfrage keine Werte dem Vergleich entsprechen oder wenn die Unterabfrage keine Zeilen an die äußere Anweisung zurückgibt. Der Ausdruck ist andernfalls UNKNOWN. Weitere Informationen finden Sie unter [einige &#124; Alle &#40; Transact-SQL &#41; ](../../t-sql/language-elements/some-any-transact-sql.md).  
  
 EXISTS  
 Wird mit einer Unterabfrage verwendet, um Tests im Hinblick auf das Vorhandensein von Zeilen durchzuführen, die von der Unterabfrage zurückgegeben wurden. Weitere Informationen finden Sie unter [EXISTS &#40; Transact-SQL &#41; ](../../t-sql/language-elements/exists-transact-sql.md).  
  
## <a name="remarks"></a>Hinweise  
 Die Rangfolge der logischen Operatoren beginnt mit NOT (höchster Operator). Darauf folgt AND und anschließend OR. Mithilfe von Klammern kann diese Rangfolge in einer Suchbedingung überschrieben werden. Die Reihenfolge der Auswertung logischer Operatoren kann variieren, abhängig von den vom Abfrageoptimierer gewählten Optionen. Weitere Informationen dazu, wie die logischen Operatoren logischen Werten ausgeführt werden, finden Sie unter [und &#40; Transact-SQL &#41; ](../../t-sql/language-elements/and-transact-sql.md), [Oder &#40; Transact-SQL &#41; ](../../t-sql/language-elements/or-transact-sql.md), und [nicht &#40; Transact-SQL &#41; ](../../t-sql/language-elements/not-transact-sql.md).  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-where-with-like-and-escape-syntax"></a>A. Verwenden von WHERE mit der LIKE- und ESCAPE-Syntax  
 Das folgende Beispiel sucht der Zeilen, in denen die `LargePhotoFileName` Spalte hat die Zeichen `green_`, und verwendet die `ESCAPE` option, da _ ein Platzhalterzeichen ist. Ohne Angabe der `ESCAPE` -Option würde die Abfrage nach allen Beschreibungswerten mit dem Wort suchen `green` gefolgt von einem einzelnen Zeichen _ enthalten.  
  
```  
USE AdventureWorks2012 ;  
GO  
SELECT *   
FROM Production.ProductPhoto  
WHERE LargePhotoFileName LIKE '%greena_%' ESCAPE 'a' ;  
```  
  
### <a name="b-using-where-and-like-syntax-with-unicode-data"></a>B. Verwenden der WHERE- und LIKE-Syntax mit Unicodedaten  
 Im folgenden Beispiel wird die `WHERE`-Klausel zum Abrufen der Postanschrift für Unternehmen außerhalb der USA (`US`) in einer Stadt, deren Namen mit `Pa` beginnt, abgerufen.  
  
```  
USE AdventureWorks2012 ;  
GO  
SELECT AddressLine1, AddressLine2, City, PostalCode, CountryRegionCode    
FROM Person.Address AS a  
JOIN Person.StateProvince AS s ON a.StateProvinceID = s.StateProvinceID  
WHERE CountryRegionCode NOT IN ('US')  
AND City LIKE N'Pa%' ;  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-where-with-like"></a>C. Verwenden von WHERE mit der LIKE-  
 Das folgende Beispiel sucht der Zeilen, in denen die `LastName` Spalte hat die Zeichen `and`.  
  
```  
-- Uses AdventureWorks  
  
SELECT EmployeeKey, LastName  
FROM DimEmployee  
WHERE LastName LIKE '%and%';  
```  
  
### <a name="d-using-where-and-like-syntax-with-unicode-data"></a>D. Verwenden der WHERE- und LIKE-Syntax mit Unicodedaten  
 Im folgenden Beispiel wird die `WHERE` -Klausel, um eine Unicode-Suchvorgänge auf der `LastName` Spalte.  
  
```  
-- Uses AdventureWorks  
  
SELECT EmployeeKey, LastName  
FROM DimEmployee  
WHERE LastName LIKE N'%and%';  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Aggregatfunktionen &#40; Transact-SQL &#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)   
 [CASE &#40;Transact-SQL&#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [CONTAINSTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [Cursors &#40;Transact-SQL&#41;](../../t-sql/language-elements/cursors-transact-sql.md)   
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [Expressions &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [FREETEXTTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/freetexttable-transact-sql.md)   
 [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)   
 [Operators &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)  
  
  


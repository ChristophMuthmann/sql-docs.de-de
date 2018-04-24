---
title: + (Verketten von Zeichenfolgen) (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 12/06/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|language-elements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- concatenation
- +
- string
dev_langs:
- TSQL
helpviewer_keywords:
- concatenation [SQL Server]
- string concatenation operators
- + (string concatenation)
ms.assetid: 35cb3d7a-48f5-4b13-926c-a9d369e20ed7
caps.latest.revision: 51
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d4e57cb9c9f71f90297265c1171ee105e51e678b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="-string-concatenation-transact-sql"></a>+ (Verketten von Zeichenfolgen) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Ein Operator in einem Zeichenfolgenausdruck, der zwei oder mehr Zeichenfolgen, binäre Zeichenfolgen oder Spalten oder eine Kombination aus Zeichenfolgen und Spaltennamen zu einem Ausdruck verkettet (ein Zeichenfolgenoperator).  `SELECT 'book'+'case';` gibt beispielsweise `bookcase` zurück.
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
expression + expression  
```  
  
## <a name="arguments"></a>Argumente  
 *expression*  
 Ein beliebiger gültiger [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) aus der binären Datentypkategorie oder der Datentypkategorie der Zeichen, mit Ausnahme der Datentypen **image**, **ntext** oder **text**. Beide Ausdrücke müssen denselben Datentyp haben, oder es muss möglich sein, einen Ausdruck implizit in den Datentyp des anderen Ausdrucks zu konvertieren.  
  
 Bei der Verkettung binärer Zeichenfolgen und Zeichen zwischen den binären Zeichenfolgen muss eine explizite Konvertierung in Zeichendaten erfolgen. Das folgende Beispiel zeigt, wann `CONVERT` (oder `CAST`) bei binärer Verkettung zu verwenden ist und wann `CONVERT` (oder `CAST`) nicht verwendet werden muss.  
  
```  
DECLARE @mybin1 varbinary(5), @mybin2 varbinary(5)  
SET @mybin1 = 0xFF  
SET @mybin2 = 0xA5  
-- No CONVERT or CAST function is required because this example   
-- concatenates two binary strings.  
SELECT @mybin1 + @mybin2  
-- A CONVERT or CAST function is required because this example  
-- concatenates two binary strings plus a space.  
SELECT CONVERT(varchar(5), @mybin1) + ' '   
   + CONVERT(varchar(5), @mybin2)  
-- Here is the same conversion using CAST.  
SELECT CAST(@mybin1 AS varchar(5)) + ' '   
   + CAST(@mybin2 AS varchar(5))  
  
```  
  
## <a name="result-types"></a>Ergebnistypen  
 Gibt einen Wert vom Datentyp des Arguments zurück, das in der Rangfolge am höchsten steht. Weitere Informationen finden Sie unter [Rangfolge der Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md).  
  
## <a name="remarks"></a>Remarks  
 Der +-Operator (Verketten von Zeichenfolgen) verhält sich anders, wenn er zusammen mit einer leeren Zeichenfolge verwendet wird, als wenn er mit einem NULL-Wert oder unbekannten Werten verwendet wird. Eine leere Zeichenfolge lässt sich als zwei einfache Anführungszeichen ohne Zeichen innerhalb der Anführungszeichen angeben. Eine leere binäre Zeichenfolge lässt sich als 0x ohne Bytewerte in der hexadezimalen Konstante angeben. Beim Verketten einer leeren Zeichenfolge werden immer die beiden angegebenen Zeichenfolgen verkettet. Wenn Sie mit Zeichenfolgen mit einem NULL-Wert arbeiten, hängt das Ergebnis der Verkettung von den Sitzungseinstellungen ab. Bei arithmetischen Operationen, die für NULL-Werte ausgeführt werden, ist das Ergebnis beim Hinzufügen eines NULL-Wertes zu einem bekannten Wert in der Regel ein unbekannter Wert. Parallel dazu führt eine Zeichenfolgenverkettungsoperation, die mit einem NULL-Wert ausgeführt wird, in der Regel zu einem NULL-Ergebnis. Sie können dieses Verhalten jedoch ändern, indem Sie die `CONCAT_NULL_YIELDS_NULL`-Einstellung für die aktuelle Sitzung ändern. Weitere Informationen finden Sie unter [SET CONCAT_NULL_YIELDS_NULL &#40;Transact-SQL&#41;](../../t-sql/statements/set-concat-null-yields-null-transact-sql.md).  
  
 Wenn das Ergebnis der Verkettung von Zeichenfolgen den Grenzwert von 8.000 Byte übersteigt, wird das Ergebnis abgeschnitten. Wenn jedoch mindestens eine der verketteten Zeichenfolgen einen umfangreichen Wert hat, wird das Ergebnis nicht abgeschnitten.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-string-concatenation"></a>A. Verwenden von Zeichenfolgenverkettungen  
 Im folgenden Beispiel wird unter der Spaltenüberschrift `Name` eine einzelne Spalte aus mehreren Zeichenspalten erstellt, mit dem Nachnamen der Person, gefolgt von einem Komma, einem einzelnen Leerzeichen und dem Vornamen der Person. Das Resultset ist in aufsteigender alphabetischer Reihenfolge sortiert (zuerst nach dem Nachnamen und dann nach dem Vornamen).  
  
```  
-- Uses AdventureWorks  
  
SELECT (LastName + ', ' + FirstName) AS Name  
FROM Person.Person  
ORDER BY LastName ASC, FirstName ASC;  
```  
  
### <a name="b-combining-numeric-and-date-data-types"></a>B. Kombinieren von numerischen Datentypen und Datumsdatentypen  
 Im folgenden Beispiel werden die Datentypen **numeric** und **date** mithilfe der `CONVERT`-Funktion verkettet.  
  
```  
-- Uses AdventureWorks  
  
SELECT 'The order is due on ' + CONVERT(varchar(12), DueDate, 101)  
FROM Sales.SalesOrderHeader  
WHERE SalesOrderID = 50001;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 ------------------------------------------------  
 The order is due on 04/23/2007  
 (1 row(s) affected)
 ```  
  
### <a name="c-using-multiple-string-concatenation"></a>C. Verwenden der Verkettung mehrerer Zeichenfolgen  
 Im folgenden Beispiel werden mehrere Zeichenfolgen verkettet, um eine lange Zeichenfolge zu bilden. Dabei wird der Nachname und der Anfangsbuchstabe des Vornamens der Vizepräsidenten in [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] angezeigt. Nach dem Nachnamen wird ein Komma hinzugefügt. Nach dem Anfangsbuchstaben des Vornamens wird ein Punkt hinzugefügt.  
  
```  
-- Uses AdventureWorks  
  
SELECT (LastName + ',' + SPACE(1) + SUBSTRING(FirstName, 1, 1) + '.') AS Name, e.JobTitle  
FROM Person.Person AS p  
    JOIN HumanResources.Employee AS e  
    ON p.BusinessEntityID = e.BusinessEntityID  
WHERE e.JobTitle LIKE 'Vice%'  
ORDER BY LastName ASC;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Name               Title  
 -------------      ---------------`  
 Duffy, T.          Vice President of Engineering  
 Hamilton, J.       Vice President of Production  
 Welcker, B.        Vice President of Sales  

 (3 row(s) affected)
 ```  
 
### <a name="d-using-large-strings-in-concatenation"></a>D. Verwenden von langen Zeichenfolgen bei Verkettungen
Im folgenden Beispiel werden mehrere Zeichenfolgen zu einer langen Zeichenfolge verkettet. Anschließend wird versucht, die Länge der endgültigen Zeichenfolge zu berechnen. Die endgültige Länge des Resultsets beträgt 16000, da die Auswertung des Ausdrucks links beginnt, d.h. @x + @z + @y = > (@x + @z) + @y. In diesem Fall wird das Ergebnis von (@x + @z) bei 8000 Byte abgeschnitten. Anschließend wird @y dem Resultset hinzugefügt, sodass sich die endgültige Zeichenfolgenlänge 16000 ergibt. Da @y eine Zeichenfolge vom Typ für hohe Werte ist, werden keine Daten abgeschnitten.

```
DECLARE @x varchar(8000) = replicate('x', 8000)
DECLARE @y varchar(max) = replicate('y', 8000)
DECLARE @z varchar(8000) = replicate('z',8000)
SET @y = @x + @z + @y
-- The result of following select is 16000
SELECT len(@y) AS y
GO
```
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 y        
 -------  
 16000  
  
 (1 row(s) affected)
 ```  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
### <a name="e-using-multiple-string-concatenation"></a>E. Verwenden der Verkettung mehrerer Zeichenfolgen  
 Im folgenden Beispiel werden mehrere Zeichenfolgen verkettet, um eine lange Zeichenfolge zu bilden. Dabei wird der Nachname und der Anfangsbuchstabe des Vornamens der Vizepräsidenten in einer Beispieldatenbank angezeigt. Nach dem Nachnamen wird ein Komma hinzugefügt. Nach dem Anfangsbuchstaben des Vornamens wird ein Punkt hinzugefügt.  
  
```  
-- Uses AdventureWorks  
  
SELECT (LastName + ', ' + SUBSTRING(FirstName, 1, 1) + '.') AS Name, Title  
FROM DimEmployee  
WHERE Title LIKE '%Vice Pres%'  
ORDER BY LastName ASC;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Name               Title                                           
-------------      ---------------  
Duffy, T.          Vice President of Engineering  
Hamilton, J.       Vice President of Production  
Welcker, B.        Vice President of Sales  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [+= &#40;Zeichenfolgenverkettungszuweisung&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/string-concatenation-equal-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [Datentypkonvertierung &#40;Datenbank-Engine&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)   
 [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Ausdrücke &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Integrierte Funktionen &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [Operatoren &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [SET-Anweisungen &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
  
  




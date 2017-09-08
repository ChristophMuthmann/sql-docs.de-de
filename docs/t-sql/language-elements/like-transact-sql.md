---
title: WIE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ESCAPE
- LIKE
- ESCAPE_TSQL
- LIKE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ESCAPE keyword
- '% (wildcard - character(s) to match)'
- ASCII pattern matching
- pattern searching [SQL Server]
- wildcard characters [SQL Server]
- literals [SQL Server], using wildcards
- character strings [SQL Server], LIKE
- exact matches [SQL Server]
- Boolean functions
- LIKE comparisons
- matching patterns [SQL Server]
- NOT LIKE keyword
ms.assetid: 581fb289-29f9-412b-869c-18d33a9e93d5
caps.latest.revision: 50
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 643966017caf06959fef24177dd93d7254f30915
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="like-transact-sql"></a>LIKE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Bestimmt, ob eine bestimmte Zeichenfolge mit einem angegebenen Muster übereinstimmt. Ein Muster kann normale Zeichen und Platzhalterzeichen einschließen. Bei einem Mustervergleich müssen normale Zeichen exakt mit den angegebenen Zeichen in der Zeichenfolge übereinstimmen. Platzhalterzeichen können jedoch mit beliebigen Teilen der Zeichenfolge übereinstimmen. Das Verwenden der Vergleichsoperatoren für Zeichenfolgen = und != ist nicht so flexibel wie das Verwenden von Platzhalterzeichen mit dem LIKE-Operator. Wenn eines der Argumente kein Zeichenfolgen-Datentyp ist, wird es ggf. von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] in einen Zeichenfolgen-Datentyp konvertiert.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
match_expression [ NOT ] LIKE pattern [ ESCAPE escape_character ]  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
match_expression [ NOT ] LIKE pattern  
```  
  
## <a name="arguments"></a>Argumente  
 *match_expression*  
 Ist ein beliebiger gültiger [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) eines Zeichendatentyps.  
  
 *Muster*  
 Ist die bestimmte Zeichenfolge von Zeichen im zu suchende *Match_expression*, und Sie können die folgenden gültigen Platzhalterzeichen enthalten. *Muster* kann maximal 8.000 Byte sein.  
  
|Platzhalter|Description|Beispiel|  
|------------------------|-----------------|-------------|  
|%|Eine Zeichenfolge aus null oder mehr Zeichen|WHERE title LIKE '%Computer%' findet alle Buchtitel, die das Wort 'Computer' enthalten.|  
|_ (Unterstrich)|Beliebiges einzelnes Zeichen.|WHERE au_fname LIKE '_ean' findet alle Vornamen mit vier Buchstaben, die auf ean enden (Dean, Sean usw.).|  
|[ ]|Beliebiges einzelnes Zeichen im angegebenen Bereich ([a-f]) oder in der angegebenen Menge ([abcdef]).|WHERE au_lname LIKE '[C-P]arsen' findet alle Autorennachnamen, die auf 'arsen' enden und mit einem einzelnen Zeichen zwischen C und P beginnen, z. B. Carsen, Larsen, Karsen usw. In Bereichssuchvorgängen unterscheiden sich die im Bereich enthaltenen Zeichen möglicherweise je nach den Sortierungsregeln für die Sortierung.|  
|[^]|Beliebiges einzelnes Zeichen, das sich nicht im angegebenen Bereich ([^a-f]) oder in der angegebenen Menge ([^abcdef]) befindet.|WHERE au_lname LIKE 'de[^l]%' findet alle Autorennachnamen, die mit 'de' beginnen und deren dritter Buchstabe nicht l ist.|  
  
 *escape_character*  
 Ist ein Zeichen, das vor einem Platzhalterzeichen eingefügt wird, um anzuzeigen, dass der Platzhalter als reguläres Zeichen und nicht als Platzhalter interpretiert werden soll. *Escape_character* ist ein Zeichenausdruck hat keinen Standardwert und muss zu einem einzelnen Zeichen ausgewertet.  
  
## <a name="result-types"></a>Ergebnistypen  
 **Boolean**  
  
## <a name="result-value"></a>Ergebniswert  
 Gibt z. B. "true" zurück, wenn die *Match_expression* entspricht dem angegebenen *Muster*.  
  
## <a name="remarks"></a>Hinweise  
 Bei Zeichenfolgenvergleichen mithilfe von LIKE werden alle Zeichen in der Musterzeichenfolge berücksichtigt. Dazu gehören alle vorhergehenden oder nachfolgenden Leerzeichen. Wenn in einer Abfrage LIKE 'abc ' (abc, gefolgt von einem Leerzeichen) verwendet wird, um Zeilen zurückzugeben, die dem Muster abc ähnlich sind, werden keine Zeilen zurückgegeben, die den Wert abc (abc ohne Leerzeichen) enthalten. Nachfolgende Leerzeichen in dem Ausdruck, der mit dem Muster verglichen wird, werden jedoch ignoriert. Wenn in einer Abfrage LIKE 'abc' (abc ohne Leerzeichen) verwendet wird, um Zeilen zurückzugeben, die dem Muster abc ähnlich sind, werden alle Zeilen zurückgegeben, die mit abc anfangen und null oder mehr nachfolgende Leerzeichen enthalten.  
  
 Mit einem Muster, die enthält einen Zeichenfolgenvergleich **Char** und **Varchar** Daten möglicherweise keinen Vergleich mit LIKE aufgrund der Art der dateispeicherung übergeben. Verschaffen Sie sich eine Übersicht darüber, wie die einzelnen Datentypen gespeichert werden und wann ein Vergleich mit LIKE fehlschlagen kann. Das folgende Beispiel übergibt eine lokale **Char** -Variablen an eine gespeicherte Prozedur ein, und Mustervergleich sollen alle Mitarbeiter, deren letzten beginnen mit einem angegebenen Satz von Zeichen gefunden.  
  
```tsql
-- Uses AdventureWorks  
  
CREATE PROCEDURE FindEmployee @EmpLName char(20)  
AS  
SELECT @EmpLName = RTRIM(@EmpLName) + '%';  
SELECT p.FirstName, p.LastName, a.City  
FROM Person.Person p JOIN Person.Address a ON p.BusinessEntityID = a.AddressID  
WHERE p.LastName LIKE @EmpLName;  
GO  
EXEC FindEmployee @EmpLName = 'Barb';  
GO  
```  
  
 In der `FindEmployee` Prozedur keine Zeilen werden zurückgegeben, da die **Char** Variable (`@EmpLName`) nachfolgende Leerzeichen enthält, wenn der Name weniger als 20 Zeichen enthält. Da die `LastName` Spalte **Varchar**, es sind keine nachfolgenden Leerzeichen. Diese Prozedur schlägt fehl, da die nachfolgenden Leerzeichen von Bedeutung sind.  
  
 Im folgenden Beispiel wird jedoch erfolgreich ist, da nachfolgende Leerzeichen nicht hinzugefügt werden eine **Varchar** Variable.  
  
```tsql
-- Uses AdventureWorks  
  
CREATE PROCEDURE FindEmployee @EmpLName varchar(20)  
AS  
SELECT @EmpLName = RTRIM(@EmpLName) + '%';  
SELECT p.FirstName, p.LastName, a.City  
FROM Person.Person p JOIN Person.Address a ON p.BusinessEntityID = a.AddressID  
WHERE p.LastName LIKE @EmpLName;  
GO  
EXEC FindEmployee @EmpLName = 'Barb';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 FirstName      LastName            City
 ----------     -------------------- --------------- 
 Angela         Barbariol            Snohomish
 David          Barber               Snohomish
 (2 row(s) affected)  
 ``` 
 
## <a name="pattern-matching-by-using-like"></a>Mustervergleich mithilfe von LIKE  
 LIKE unterstützt Mustervergleiche im ASCII- und Unicode-Format. Wenn alle Argumente (*Match_expression*, *Muster*, und *Escape_character*, falls vorhanden) ASCII-Zeichen-Datentypen sind ASCII-Mustervergleich wird durchgeführt. Wenn eines der Argumente von einem Unicode-Datentyp ist, werden alle Argumente in Unicode konvertiert und ein Unicode-Mustervergleich durchgeführt. Bei Verwendung von Unicode-Daten (**Nchar** oder **Nvarchar** Datentypen) mit der LIKE-, nachfolgende Leerzeichen sind von Bedeutung; allerdings für nicht-Unicode-Daten, nachfolgende Leerzeichen nicht relevant sind. Der Unicode-LIKE-Operator ist mit dem ISO-Standard kompatibel. Der ASCII-LIKE-Operator ist mit früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kompatibel.  
  
 Die folgenden Beispiele verdeutlichen die Unterschiede der zurückgegebenen Zeilen beim Durchführen von Mustervergleichen mit ASCII- und Unicode-LIKE-Operatoren.  
  
```tsql  
-- ASCII pattern matching with char column  
CREATE TABLE t (col1 char(30));  
INSERT INTO t VALUES ('Robert King');  
SELECT *   
FROM t   
WHERE col1 LIKE '% King';   -- returns 1 row  
  
-- Unicode pattern matching with nchar column  
CREATE TABLE t (col1 nchar(30));  
INSERT INTO t VALUES ('Robert King');  
SELECT *   
FROM t   
WHERE col1 LIKE '% King';   -- no rows returned  
  
-- Unicode pattern matching with nchar column and RTRIM  
CREATE TABLE t (col1 nchar (30));  
INSERT INTO t VALUES ('Robert King');  
SELECT *   
FROM t   
WHERE RTRIM(col1) LIKE '% King';   -- returns 1 row  
```  
  
> [!NOTE]  
>  LIKE-Vergleiche werden von der Sortierung beeinflusst. Weitere Informationen finden Sie unter [COLLATE &#40;Transact-SQL&#41;](~/t-sql/statements/collations.md).  
  
## <a name="using-the--wildcard-character"></a>Verwenden des %-Platzhalterzeichens  
 Wird bei LIKE beispielsweise '5%' angegeben, sucht [!INCLUDE[ssDE](../../includes/ssde-md.md)] nach der Zahl 5, gefolgt von einer beliebigen Zeichenfolge mit 0 oder mehr Zeichen.  
  
 Mit der folgenden Abfrage werden beispielsweise alle dynamischen Verwaltungssichten in der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank angezeigt, da sie alle mit den Buchstaben `dm` beginnen.  
  
```tsql  
-- Uses AdventureWorks  
  
SELECT Name  
FROM sys.system_views  
WHERE Name LIKE 'dm%';  
GO  
```  
  
 Wenn Objekte angezeigt werden sollen, die keine dynamischen Verwaltungssichten sind, verwenden Sie `NOT LIKE 'dm%'`. Sind insgesamt 32 Objekte vorhanden und LIKE ermittelt 13 dieser Objekte, die dem Muster entsprechen, ermittelt NOT LIKE die 19 Objekte, die dem Muster nicht entsprechen.  
  
 Mit einem Muster wie `LIKE '[^d][^m]%'` werden möglicherweise nicht immer die gleichen Namen gefunden. Statt 19 Namen werden möglicherweise nur 14 angezeigt, da Namen, die mit `d` beginnen oder deren zweiter Buchstabe `m` ist, aus dem Resultset ebenso entfernt werden wie die Namen der dynamischen Verwaltungssichten. Grund dafür ist die schrittweise Auswertung von Musterzeichenfolgen mit negativen Platzhalterzeichen, d. h., dass Platzhalter für Platzhalter ausgewertet wird. Wenn der Vergleich an einem beliebigen Punkt der Auswertung fehlschlägt, wird das entsprechende Objekt aus dem Resultset entfernt.  
  
## <a name="using-wildcard-characters-as-literals"></a>Verwenden von Platzhalterzeichen als Literale  
 Platzhalterzeichen können auch als Literalzeichen verwendet werden. Um ein Platzhalterzeichen als Literalzeichen zu verwenden, schließen Sie das Platzhalterzeichen in Klammern ein. Die folgende Tabelle enthält einige Beispiele für die Verwendung des LIKE-Schlüsselworts und der [ ]-Platzhalterzeichen.  
  
|Symbol|Bedeutung|  
|------------|-------------|  
|LIKE '5[%]'|5%|  
|LIKE '[_]n'|_N|  
|LIKE '[a-cdf]'|a, b, c, d oder f|  
|LIKE '[-acdf]'|-, a, c, d oder f|  
|LIKE '[ [ ]'|[|  
|LIKE ']'|]|  
|LIKE 'abc[_]d%'|abc_d und abc_de|  
|LIKE 'abc[def]'|abcd, abce und abcf|  
  
## <a name="pattern-matching-with-the-escape-clause"></a>Mustervergleich mit der ESCAPE-Klausel  
 Sie können nach Zeichenfolgen suchen, die ein oder mehrere Platzhalterzeichen enthalten. Die discounts-Tabelle in der customers-Datenbank kann beispielsweise Rabattwerte mit einem Prozentzeichen (%) speichern. Um nach dem Prozentzeichen als Zeichen und nicht als Platzhalterzeichen zu suchen, müssen das ESCAPE-Schlüsselwort und das Escapezeichen angegeben werden. Eine Beispieldatenbank enthält beispielsweise eine comment-Spalte, die den Text 30% enthält. Wenn Sie in den Zeilen der comment-Spalte nach der Zeichenfolge "30%" suchen, geben Sie eine WHERE-Klausel wie `WHERE comment LIKE '%30!%%' ESCAPE '!'` an. Werden ESCAPE und das Escapezeichen nicht angegeben, gibt [!INCLUDE[ssDE](../../includes/ssde-md.md)] alle Zeilen zurück, die die Zeichenfolge 30 enthalten.  
  
 Wenn im LIKE-Muster kein Zeichen auf ein Escapezeichen folgt, ist das Muster nicht gültig und das LIKE-Muster gibt FALSE zurück. Wenn es sich beim Zeichen nach einem Escapezeichen nicht um ein Platzhalterzeichen handelt, wird das Escapezeichen verworfen und das Zeichen, das auf das Escapezeichen folgt, als reguläres Zeichen im Muster behandelt. Dazu gehören die Platzhalterzeichen Prozent (%), Unterstrich (_) und linke Klammer ([), wenn sie in doppelte Klammern ([ ]) eingeschlossen sind. Innerhalb doppelter Klammern ([ ]) können Escapezeichen verwendet werden; dem Caretzeichen (^), dem Bindestrich (-) sowie der rechten Klammer (]) kann ein Escapezeichen vorangestellt werden.  
  
 0 x 0000 (**char(0) zurück**) ist ein nicht definiertes Zeichen in Windows-Sortierungen und kann nicht in LIKE enthalten sein.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-like-with-the--wildcard-character"></a>A. Verwenden von NOT LIKE mit dem Platzhalterzeichen %  
 Im folgenden Beispiel werden alle Telefonnummern gefunden, die die Vorwahl `415` in der `PersonPhone`-Tabelle enthalten.  
  
```tsql  
-- Uses AdventureWorks  
  
SELECT p.FirstName, p.LastName, ph.PhoneNumber  
FROM Person.PersonPhone AS ph  
INNER JOIN Person.Person AS p  
ON ph.BusinessEntityID = p.BusinessEntityID  
WHERE ph.PhoneNumber LIKE '415%'  
ORDER by p.LastName;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
 
 ```
 FirstName             LastName             Phone
 -----------------     -------------------  ------------
 Ruben                 Alonso               415-555-124  
 Shelby                Cook                 415-555-0121  
 Karen                 Hu                   415-555-0114  
 John                  Long                 415-555-0147  
 David                 Long                 415-555-0123  
 Gilbert               Ma                   415-555-0138  
 Meredith              Moreno               415-555-0131  
 Alexandra             Nelson               415-555-0174  
 Taylor                Patterson            415-555-0170  
 Gabrielle              Russell             415-555-0197  
 Dalton                 Simmons             415-555-0115  
 (11 row(s) affected)  
 ``` 
 
### <a name="b-using-not-like-with-the--wildcard-character"></a>B. Verwenden von NOT LIKE mit dem Platzhalterzeichen %  
 Im folgenden Beispiel werden alle Telefonnummern in der `PersonPhone`-Tabelle gefunden, die nicht die Vorwahl `415` aufweisen.  
  
```tsql  
-- Uses AdventureWorks  
  
SELECT p.FirstName, p.LastName, ph.PhoneNumber  
FROM Person.PersonPhone AS ph  
INNER JOIN Person.Person AS p  
ON ph.BusinessEntityID = p.BusinessEntityID  
WHERE ph.PhoneNumber NOT LIKE '415%' AND p.FirstName = 'Gail'  
ORDER BY p.LastName;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
 
 ```
FirstName              LastName            Phone
---------------------- -------------------- -------------------
Gail                  Alexander            1 (11) 500 555-0120  
Gail                  Butler               1 (11) 500 555-0191  
Gail                  Erickson             834-555-0132  
Gail                  Erickson             849-555-0139  
Gail                  Griffin              450-555-0171  
Gail                  Moore                155-555-0169  
Gail                  Russell              334-555-0170  
Gail                  Westover             305-555-0100  
(8 row(s) affected)  
```  

### <a name="c-using-the-escape-clause"></a>C. Verwenden der ESCAPE-Klausel  
 Im folgenden Beispiel werden die `ESCAPE`-Klausel und das Escapezeichen verwendet, um die exakte Zeichenfolge `10-15%` in der `c1`-Spalte der `mytbl2`-Tabelle zu suchen.  
  
```tsql
USE tempdb;  
GO  
IF EXISTS(SELECT TABLE_NAME FROM INFORMATION_SCHEMA.TABLES  
      WHERE TABLE_NAME = 'mytbl2')  
   DROP TABLE mytbl2;  
GO  
USE tempdb;  
GO  
CREATE TABLE mytbl2  
(  
 c1 sysname  
);  
GO  
INSERT mytbl2 VALUES ('Discount is 10-15% off'), ('Discount is .10-.15 off');  
GO  
SELECT c1   
FROM mytbl2  
WHERE c1 LIKE '%10-15!% off%' ESCAPE '!';  
GO  
```  
  
### <a name="d-using-the---wildcard-characters"></a>D. Verwenden des []-Platzhalterzeichens  
 Im folgende Beispiel werden Mitarbeiter ermittelt, auf die `Person` Tabelle mit den ersten Vornamen des `Cheryl` oder `Sheryl`.  
  
```tsql  
-- Uses AdventureWorks  
  
SELECT BusinessEntityID, FirstName, LastName   
FROM Person.Person   
WHERE FirstName LIKE '[CS]heryl';  
GO  
```  
  
 Im folgenden Beispiel werden in der `Person`-Tabelle Zeilen für Mitarbeiter mit den Nachnamen `Zheng` oder `Zhang` gesucht.  
  
```tsql  
-- Uses AdventureWorks  
  
SELECT LastName, FirstName  
FROM Person.Person  
WHERE LastName LIKE 'Zh[ae]ng'  
ORDER BY LastName ASC, FirstName ASC;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-using-like-with-the--wildcard-character"></a>E. Verwenden von NOT LIKE mit dem Platzhalterzeichen %  
 Das folgende Beispiel findet alle Mitarbeiter in der `DimEmployee` Tabelle mit Telefonnummern, die mit beginnt `612`.  
  
```tsql  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName, Phone  
FROM DimEmployee  
WHERE phone LIKE '612%'  
ORDER by LastName;  
```  
  
### <a name="f-using-not-like-with-the--wildcard-character"></a>F. Verwenden von NOT LIKE mit dem Platzhalterzeichen %  
 Das folgende Beispiel findet alle Telefonnummern in der `DimEmployee` Tabelle, die nicht mit beginnen `612`.  zugreifen.  
  
```tsql  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName, Phone  
FROM DimEmployee  
WHERE phone NOT LIKE '612%'  
ORDER by LastName;  
```  
  
### <a name="g-using-like-with-the--wildcard-character"></a>G. Verwenden von NOT LIKE mit dem Platzhalterzeichen _  
 Das folgende Beispiel findet alle Telefonnummern Ortsvorwahl ab, mit denen `6` und Endziffern `2` in der `DimEmployee` Tabelle. Beachten Sie, dass es sich bei das Platzhalterzeichen % auch am Ende das Suchmuster enthalten ist, da die Ortskennzahl der erste Teil der Rufnummer ist und zusätzliche Zeichen nach dem in der Wert der Spalte vorhanden sein.  
  
```tsql  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName, Phone  
FROM DimEmployee  
WHERE phone LIKE '6_2%'  
ORDER by LastName;   
```  
  
### <a name="h-using-the---wildcard-characters"></a>H. Verwenden des []-Platzhalterzeichens  
 Das folgende Beispiel sucht nach `DimEmployee` Zeilen mit den ersten Vornamen des `Rob` oder `Bob`.  
  
```tsql  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName, Phone  
FROM DimEmployee  
WHERE FirstName LIKE '[RB]ob'  
ORDER by LastName;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Ausdrücke &#40; Transact-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Integrierte Funktionen &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [WOBEI &#40; Transact-SQL &#41;](../../t-sql/queries/where-transact-sql.md)  
 


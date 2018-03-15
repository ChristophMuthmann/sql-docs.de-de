---
title: LIKE (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
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
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 4fa2299a1efade9f44de85d02c60286a25aad8d0
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="like-transact-sql"></a>LIKE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

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
 Ein gültiger [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) eines Zeichendatentyps.  
  
 *pattern*  
 Ist die bestimmte Zeichenfolge, nach der in *match_expression* gesucht werden soll, und kann die folgenden gültigen Platzhalterzeichen enthalten. *pattern* darf maximal 8.000 Bytes umfassen.  
  
|Platzhalter|Description|Beispiel|  
|------------------------|-----------------|-------------|  
|%|Eine Zeichenfolge aus null oder mehr Zeichen|WHERE title LIKE '%Computer%' findet alle Buchtitel, die das Wort 'Computer' enthalten.|  
|_ (Unterstrich)|Ein einzelnes Zeichen.|WHERE au_fname LIKE '_ean' findet alle Vornamen mit vier Buchstaben, die auf ean enden (Dean, Sean usw.).|  
|[ ]|Beliebiges einzelnes Zeichen im angegebenen Bereich ([a-f]) oder in der angegebenen Menge ([abcdef]).|WHERE au_lname LIKE '[C-P]arsen' findet alle Autorennachnamen, die auf 'arsen' enden und mit einem einzelnen Zeichen zwischen C und P beginnen, z. B. Carsen, Larsen, Karsen usw. In Bereichssuchvorgängen unterscheiden sich die im Bereich enthaltenen Zeichen möglicherweise je nach den Sortierungsregeln für die Sortierung.|  
|[^]|Beliebiges einzelnes Zeichen, das sich nicht im angegebenen Bereich ([^a-f]) oder in der angegebenen Menge ([^abcdef]) befindet.|WHERE au_lname LIKE 'de[^l]%' findet alle Autorennachnamen, die mit 'de' beginnen und deren dritter Buchstabe nicht l ist.|  
  
 *escape_character*  
 Ist ein Zeichen, das vor einem Platzhalterzeichen eingefügt wird, um anzuzeigen, dass der Platzhalter als reguläres Zeichen und nicht als Platzhalter interpretiert werden soll. *excape_character* ist ein Zeichenausdruck ohne Standard und muss zu einem einzelnen Zeichen ausgewertet werden.  
  
## <a name="result-types"></a>Ergebnistypen  
 **Boolean**  
  
## <a name="result-value"></a>Ergebniswert  
 LIKE gibt TRUE zurück, wenn *match_expression* dem angegebenen *pattern* entspricht.  
  
## <a name="remarks"></a>Remarks  
 Bei Zeichenfolgenvergleichen mithilfe von LIKE werden alle Zeichen in der Musterzeichenfolge berücksichtigt. Dazu gehören alle vorhergehenden oder nachfolgenden Leerzeichen. Wenn in einer Abfrage LIKE 'abc ' (abc, gefolgt von einem Leerzeichen) verwendet wird, um Zeilen zurückzugeben, die dem Muster abc ähnlich sind, werden keine Zeilen zurückgegeben, die den Wert abc (abc ohne Leerzeichen) enthalten. Nachfolgende Leerzeichen in dem Ausdruck, der mit dem Muster verglichen wird, werden jedoch ignoriert. Wenn in einer Abfrage LIKE 'abc' (abc ohne Leerzeichen) verwendet wird, um Zeilen zurückzugeben, die dem Muster abc ähnlich sind, werden alle Zeilen zurückgegeben, die mit abc anfangen und null oder mehr nachfolgende Leerzeichen enthalten.  
  
 Ein Zeichenfolgenvergleich mithilfe eines Musters, das Daten der Typen **char** und **varchar** enthält, kann bei einem Vergleich mit dem LIKE-Operator aufgrund der Art der Datenspeicherung fehlschlagen. Verschaffen Sie sich eine Übersicht darüber, wie die einzelnen Datentypen gespeichert werden und wann ein Vergleich mit LIKE fehlschlagen kann. Im folgenden Beispiel wird eine lokale **char**-Variable an eine gespeicherte Prozedur übergeben. Mit einem Mustervergleich sollen dann alle Mitarbeiter gefunden werden, deren Nachnamen mit bestimmten Zeichen beginnen.  
  
```sql
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
  
 Die `FindEmployee`-Prozedur gibt keine Zeilen zurück, da die **char**-Variable (`@EmpLName`) immer dann nachfolgende Leerzeichen enthält, wenn der Name weniger als 20 Zeichen enthält. Da die `LastName`-Spalte vom Typ **varchar** ist, sind keine nachfolgenden Leerzeichen vorhanden. Diese Prozedur schlägt fehl, da die nachfolgenden Leerzeichen von Bedeutung sind.  
  
 Das folgende Beispiel ist jedoch erfolgreich, da der **varchar**-Variablen keine nachfolgenden Leerzeichen hinzugefügt werden.  
  
```sql
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
 LIKE unterstützt Mustervergleiche im ASCII- und Unicode-Format. Sind alle Argumente (*match_expression*, *pattern* und ggf. *escape_character*) ASCII-Zeichen, wird ein ASCII-Mustervergleich durchgeführt. Wenn eines der Argumente von einem Unicode-Datentyp ist, werden alle Argumente in Unicode konvertiert und ein Unicode-Mustervergleich durchgeführt. Wenn Sie beim LIKE-Operator Unicode-Daten (**nchar**- oder **nvarchar**-Datentypen) verwenden, werden nachfolgende Leerzeichen berücksichtigt. Bei Daten, die nicht vom Typ Unicode sind, werden nachfolgende Leerzeichen ignoriert. Der Unicode-LIKE-Operator ist mit dem ISO-Standard kompatibel. Der ASCII-LIKE-Operator ist mit früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kompatibel.  
  
 Die folgenden Beispiele verdeutlichen die Unterschiede der zurückgegebenen Zeilen beim Durchführen von Mustervergleichen mit ASCII- und Unicode-LIKE-Operatoren.  
  
```sql  
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
  
```sql  
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
|LIKE '[_]n'|_n|  
|LIKE '[a-cdf]'|a, b, c, d oder f|  
|LIKE '[-acdf]'|-, a, c, d oder f|  
|LIKE '[ [ ]'|[|  
|LIKE ']'|]|  
|LIKE 'abc[_]d%'|abc_d und abc_de|  
|LIKE 'abc[def]'|abcd, abce und abcf|  
  
## <a name="pattern-matching-with-the-escape-clause"></a>Mustervergleich mit der ESCAPE-Klausel  
 Sie können nach Zeichenfolgen suchen, die ein oder mehrere Platzhalterzeichen enthalten. Die discounts-Tabelle in der customers-Datenbank kann beispielsweise Rabattwerte mit einem Prozentzeichen (%) speichern. Um nach dem Prozentzeichen als Zeichen und nicht als Platzhalterzeichen zu suchen, müssen das ESCAPE-Schlüsselwort und das Escapezeichen angegeben werden. Eine Beispieldatenbank enthält beispielsweise eine comment-Spalte, die den Text 30% enthält. Wenn Sie in den Zeilen der comment-Spalte nach der Zeichenfolge "30%" suchen, geben Sie eine WHERE-Klausel wie `WHERE comment LIKE '%30!%%' ESCAPE '!'` an. Werden ESCAPE und das Escapezeichen nicht angegeben, gibt [!INCLUDE[ssDE](../../includes/ssde-md.md)] alle Zeilen zurück, die die Zeichenfolge 30 enthalten.  
  
 Wenn im LIKE-Muster kein Zeichen auf ein Escapezeichen folgt, ist das Muster nicht gültig und das LIKE-Muster gibt FALSE zurück. Wenn es sich beim Zeichen nach einem Escapezeichen nicht um ein Platzhalterzeichen handelt, wird das Escapezeichen verworfen und das Zeichen, das auf das Escapezeichen folgt, als reguläres Zeichen im Muster behandelt. Dazu gehören die Platzhalterzeichen Prozent (%), Unterstrich (_) und linke Klammer ([), wenn sie in doppelte Klammern ([ ]) eingeschlossen sind. Innerhalb doppelter Klammern ([ ]) können Escapezeichen verwendet werden; dem Caretzeichen (^), dem Bindestrich (-) sowie der rechten Klammer (]) kann ein Escapezeichen vorangestellt werden.  
  
 0x0000 (**char(0)**) ist ein nicht definiertes Zeichen in Windows-Sortierungen und kann nicht in LIKE enthalten sein.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-like-with-the--wildcard-character"></a>A. Verwenden von NOT LIKE mit dem Platzhalterzeichen %  
 Im folgenden Beispiel werden alle Telefonnummern gefunden, die die Vorwahl `415` in der `PersonPhone`-Tabelle enthalten.  
  
```sql  
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
  
```sql  
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
  
```sql
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
 Im folgenden Beispiel werden Mitarbeiter in der `Person`-Tabelle mit dem Vornamen `Cheryl` oder `Sheryl` gesucht.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT BusinessEntityID, FirstName, LastName   
FROM Person.Person   
WHERE FirstName LIKE '[CS]heryl';  
GO  
```  
  
 Im folgenden Beispiel werden in der `Person`-Tabelle Zeilen für Mitarbeiter mit den Nachnamen `Zheng` oder `Zhang` gesucht.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT LastName, FirstName  
FROM Person.Person  
WHERE LastName LIKE 'Zh[ae]ng'  
ORDER BY LastName ASC, FirstName ASC;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
### <a name="e-using-like-with-the--wildcard-character"></a>E. Verwenden von NOT LIKE mit dem Platzhalterzeichen %  
 Im folgenden Beispiel werden alle Mitarbeiter in der `DimEmployee`-Tabelle mit Telefonnummern gefunden, die mit `612` beginnen.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName, Phone  
FROM DimEmployee  
WHERE phone LIKE '612%'  
ORDER by LastName;  
```  
  
### <a name="f-using-not-like-with-the--wildcard-character"></a>F. Verwenden von NOT LIKE mit dem Platzhalterzeichen %  
 Im folgenden Beispiel werden alle Telefonnummern in der `DimEmployee`-Tabelle gefunden, die nicht mit `612` beginnen.  zugreifen.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName, Phone  
FROM DimEmployee  
WHERE phone NOT LIKE '612%'  
ORDER by LastName;  
```  
  
### <a name="g-using-like-with-the--wildcard-character"></a>G. Verwenden von LIKE mit dem Platzhalterzeichen _  
 Im folgenden Beispiel werden alle Telefonnummern in der `DimEmployee`-Tabelle gefunden, die eine Vorwahl aufweisen, die mit `6` beginnt und mit `2` endet. Das Platzhalterzeichen % wurde am Ende des Suchmusters nicht eingefügt, da die Vorwahl der erste Teil der Telefonnummer ist und danach weitere Zeichen im Spaltenwert vorhanden sind.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName, Phone  
FROM DimEmployee  
WHERE phone LIKE '6_2%'  
ORDER by LastName;   
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Ausdrücke &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Integrierte Funktionen &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)  
 

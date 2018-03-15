---
title: CHAR (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- char_TSQL
- char
dev_langs:
- TSQL
helpviewer_keywords:
- converting int ACSII code to character
- control characters
- tab
- ASCII conversions
- CHAR function
- carriage return
- inserting control characters
- characters [SQL Server], control
- line feed
- printing ASCII values
ms.assetid: 955afe94-539c-465d-af22-16ec45da432a
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 5dd3a4f8b6fd308560ddcf2db3c6940625dc6ee3
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="char-transact-sql"></a>CHAR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Wandelt einen **int**-ASCII-Code in ein Zeichen um.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
CHAR ( integer_expression )  
```  
  
## <a name="arguments"></a>Argumente  
*integer_expression*  
Eine ganze Zahl zwischen 0 und 255. `NULL` wird zurückgegeben, wenn der Integerausdruck außerhalb dieses Bereichs liegt.
  
## <a name="return-types"></a>Rückgabetypen
**char(1)**
  
## <a name="remarks"></a>Remarks  
Mit `CHAR` können Steuerzeichen in Zeichenfolgen eingefügt werden. In der folgenden Tabelle finden Sie einige häufig verwendete Steuerzeichen.
  
|Steuerzeichen|value|  
|---|---|
|Registerkarte|**char(9)**|  
|Zeilenvorschub|**char(10)**|  
|Wagenrücklauf|**char(13)**|  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-ascii-and-char-to-print-ascii-values-from-a-string"></a>A. Verwenden von ASCII und CHAR, um die ASCII-Werte einer Zeichenfolge auszugeben  
Im folgenden Beispiel werden der ASCII-Wert und das Zeichen für jedes in der Zeichenfolge `New Moon` enthaltene Zeichen ausgegeben.
  
```sql
SET TEXTSIZE 0;  
-- Create variables for the character string and for the current   
-- position in the string.  
DECLARE @position int, @string char(8);  
-- Initialize the current position and the string variables.  
SET @position = 1;  
SET @string = 'New Moon';  
WHILE @position <= DATALENGTH(@string)  
   BEGIN  
   SELECT ASCII(SUBSTRING(@string, @position, 1)),   
      CHAR(ASCII(SUBSTRING(@string, @position, 1)))  
   SET @position = @position + 1  
   END;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
----------- -
78          N  
----------- -  
101         e  
----------- -  
119         w  
----------- -  
32  
----------- -  
77          M  
----------- -  
111         o  
----------- -  
111         o  
----------- - 
110         n  
```
  
### <a name="b-using-char-to-insert-a-control-character"></a>B. Verwenden von CHAR, um ein Steuerzeichen einzufügen  
Im folgenden Beispiel wird `CHAR(13)` verwendet, um den Namen und die E-Mail-Adresse eines Mitarbeiters in separaten Zeilen auszugeben, wenn die Ergebnisse in einem Text zurückgegeben werden. In diesem Beispiel wird die [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank verwendet.
  
```sql
SELECT p.FirstName + ' ' + p.LastName, + CHAR(13)  + pe.EmailAddress   
FROM Person.Person p JOIN Person.EmailAddress pe  
ON p.BusinessEntityID = pe.BusinessEntityID  
AND p.BusinessEntityID = 1;  
GO  
```
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
Ken Sanchez
ken0@adventure-works.com
  
(1 row(s) affected)
```
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
### <a name="c-using-ascii-and-char-to-print-ascii-values-from-a-string"></a>C. Verwenden von ASCII und CHAR, um die ASCII-Werte einer Zeichenfolge auszugeben  
Im folgenden Beispiel, in dem von einem ASCII-Zeichensatz ausgegangen wird, wird der Zeichenwert für sechs ASCII-Zeichennummern zurückgegeben.
  
```sql
SELECT CHAR(65) AS [65], CHAR(66) AS [66],   
CHAR(97) AS [97], CHAR(98) AS [98],   
CHAR(49) AS [49], CHAR(50) AS [50];  
```
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
65   66   97   98   49   50  
---- ---- ---- ---- ---- ----  
A    B    a    b    1    2  
```
  
### <a name="d-using-char-to-insert-a-control-character"></a>D. Verwenden von CHAR, um ein Steuerzeichen einzufügen  
Im folgenden Beispiel wird `CHAR(13)` verwendet, um Informationen zu den Datenbanken auf unterschiedlichen Zeilen zurückzugeben, wenn die Ergebnisse in Textform zurückgegeben werden.
  
```sql
SELECT name, 'was created on ', create_date, CHAR(13), name, 'is currently ', state_desc   
FROM sys.databases;  
GO  
```
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
name     create_date    name    state_desc  
------------------------------------------------------------  
master                   was created on  2003-04-08 09:13:36.390   
master                   is currently  ONLINE  
tempdb                   was created on  2014-01-10 17:24:24.023   
tempdb                   is currently  ONLINE  
AdventureWorksPDW2012    was created on  2014-05-07 09:05:07.083 
AdventureWorksPDW2012    is currently  ONLINE  
```
  
## <a name="see-also"></a>Siehe auch
 [ASCII &#40;Transact-SQL&#41;](../../t-sql/functions/ascii-transact-sql.md)  
 [NCHAR &#40;Transact-SQL&#41;](../../t-sql/functions/nchar-transact-sql.md)  
 [UNICODE &#40;Transact-SQL&#41;](../../t-sql/functions/unicode-transact-sql.md)  
 [+ &#40;String Concatenation&#41; &#40;Transact-SQL&#41; (+ (Verketten von Zeichenfolgen) (Transact-SQL))](../../t-sql/language-elements/string-concatenation-transact-sql.md)  
 [String Functions &#40;Transact-SQL&#41; (Zeichenfolgenfunktionen (Transact-SQL))](../../t-sql/functions/string-functions-transact-sql.md)
  
  


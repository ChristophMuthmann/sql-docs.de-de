---
title: CHAR (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- char_TSQL
- char
dev_langs: TSQL
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
caps.latest.revision: "39"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 71b8ce296640f1d205335be7d5f58d8c8e22b7c4
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="char-transact-sql"></a>CHAR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Konvertiert eine **Int** ASCII-Code in ein Zeichen.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
CHAR ( integer_expression )  
```  
  
## <a name="arguments"></a>Argumente  
*integer_expression*  
Eine ganze Zahl zwischen 0 und 255. `NULL`wird zurückgegeben, wenn der ganzzahlige Ausdruck nicht in diesem Bereich ist.
  
## <a name="return-types"></a>Rückgabetypen
**char(1)**
  
## <a name="remarks"></a>Hinweise  
`CHAR`kann verwendet werden, um die Steuerzeichen in Zeichenfolgen eingefügt. In der folgenden Tabelle finden Sie einige häufig verwendete Steuerzeichen.
  
|Steuerzeichen|Wert|  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-ascii-and-char-to-print-ascii-values-from-a-string"></a>C. Verwenden von ASCII und CHAR, um die ASCII-Werte einer Zeichenfolge auszugeben  
Im folgende Beispiel wird angenommen, ein ASCII-Zeichen festgelegt und gibt den Zeichenwert für 6 Ziffern von ASCII-Zeichen.
  
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
Im folgenden Beispiel wird `CHAR(13)` Informationen zu den Datenbanken in separaten Zeilen zurückgegeben, wenn die Ergebnisse in Text zurückgegeben werden.
  
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
[+ &#40; Verketten von Zeichenfolgen &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/string-concatenation-transact-sql.md)  
[Zeichenfolgenfunktionen &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)
  
  


---
title: UNICODE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- UNICODE
- UNICODE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- first character of input expression [SQL Server]
- UNICODE function
- Unicode [SQL Server], UNICODE function
ms.assetid: 5e3c40b2-8401-4741-9f2a-bae70eaa4da6
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: ce87bcab037ff99b7eaa03a443727db17db19b74
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="unicode-transact-sql"></a>UNICODE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt laut Definition des Unicode-Standards eine ganze Zahl für das erste Zeichen des Eingabeausdrucks zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
UNICODE ( 'ncharacter_expression' )  
```  
  
## <a name="arguments"></a>Argumente  
 **'** *ncharacter_expression* **'**  
 Ist ein **Nchar** oder **Nvarchar** Ausdruck.  
  
## <a name="return-types"></a>Rückgabetypen  
 **int**  
  
## <a name="remarks"></a>Hinweise  
 In früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] als [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] gibt die UNICODE-Funktion einen UCS-2-Codepunkt im Bereich 0 bis 0xFFFF zurück. In [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] und höheren Editionen gibt UNICODE bei Verwendung von SC-Sortierungen einen UTF-16-Codepunkt im Bereich 0 bis 0x10FFFF zurück.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-unicode-and-the-nchar-function"></a>A. Verwenden von UNICODE und der NCHAR-Funktion  
 Im folgenden Beispiel werden die Funktionen `UNICODE` und `NCHAR` zur Ausgabe des UNICODE-Werts des ersten Zeichens der Zeichenfolge `Åkergatan` 24 sowie zur Ausgabe des tatsächlichen ersten Zeichens, und zwar `Å`, verwendet.  
  
```  
DECLARE @nstring nchar(12);  
SET @nstring = N'Åkergatan 24';  
SELECT UNICODE(@nstring), NCHAR(UNICODE(@nstring));  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----------- -   
197         Å  
```  
  
### <a name="b-using-substring-unicode-and-convert"></a>B. Verwenden von SUBSTRING, UNICODE und CONVERT  
 Im folgenden Beispiel werden die Funktionen `SUBSTRING`, `UNICODE` und `CONVERT` zur Ausgabe der Zeichennummer, des Unicode-Zeichens und des UNICODE-Werts für jedes Zeichen in der Zeichenfolge `Åkergatan 24` verwendet.  
  
```  
-- The @position variable holds the position of the character currently  
-- being processed. The @nstring variable is the Unicode character   
-- string to process.  
DECLARE @position int, @nstring nchar(12);  
-- Initialize the current position variable to the first character in   
-- the string.  
SET @position = 1;  
-- Initialize the character string variable to the string to process.   
-- Notice that there is an N before the start of the string, which   
-- indicates that the data following the N is Unicode data.  
SET @nstring = N'Åkergatan 24';  
-- Print the character number of the position of the string you are at,   
-- the actual Unicode character you are processing, and the UNICODE   
-- value for this particular character.  
PRINT 'Character #' + ' ' + 'Unicode Character' + ' ' + 'UNICODE Value';  
WHILE @position <= DATALENGTH(@nstring)  
-- While these are still characters in the character string,  
   BEGIN;  
   SELECT @position,   
      CONVERT(char(17), SUBSTRING(@nstring, @position, 1)),  
      UNICODE(SUBSTRING(@nstring, @position, 1));  
   SELECT @position = @position + 1;  
   END;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Character # Unicode Character UNICODE Value  
  
----------- ----------------- -----------   
1           Å                 197           
  
----------- ----------------- -----------   
2           k                 107           
  
----------- ----------------- -----------   
3           e                 101           
  
----------- ----------------- -----------   
4           r                 114           
  
----------- ----------------- -----------   
5           g                 103           
  
----------- ----------------- -----------   
6           a                 97            
  
----------- ----------------- -----------   
7           t                 116           
  
----------- ----------------- -----------   
8           a                 97            
  
----------- ----------------- -----------   
9           n                 110           
  
----------- ----------------- -----------   
10                            32            
  
----------- ----------------- -----------   
11          2                 50            
  
----------- ----------------- -----------   
12          4                 52  
```  
  
## <a name="see-also"></a>Siehe auch  
 [ASCII &#40;Transact-SQL&#41;](../../t-sql/functions/ascii-transact-sql.md)  
 [CHAR &#40;Transact-SQL&#41;](../../t-sql/functions/char-transact-sql.md)  
 [NCHAR &#40;Transact-SQL&#41;](../../t-sql/functions/nchar-transact-sql.md)   
 [Zeichenfolgenfunktionen &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)  
  
  


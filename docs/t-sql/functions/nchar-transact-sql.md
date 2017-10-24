---
title: NCHAR (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- nchar
- nchar_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- NCHAR function
- Unicode [SQL Server], NCHAR function
ms.assetid: 68cefc68-7c4f-4326-80c1-300f90cf19db
caps.latest.revision: 43
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: b70c591517177ad9febd1d0d9873a41192bf9414
ms.contentlocale: de-de
ms.lasthandoff: 10/17/2017

---
# <a name="nchar-transact-sql"></a>NCHAR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt das Unicode-Zeichen mit dem angegebenen ganzzahligen Code gemäß der Definition durch den Unicode-Standard zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
NCHAR ( integer_expression )  
```  
  
## <a name="arguments"></a>Argumente  
 *integer_expression*  
 Wenn die Sortierung der Datenbank das ergänzende Zeichenflag nicht enthält, entspricht dies einer positiven ganzen Zahl von 0 bis 65535 (0 bis 0xFFFF). Wenn ein Wert außerhalb dieses Bereichs angegeben wurde, wird NULL zurückgegeben. Weitere Informationen zu ergänzenden Zeichen finden Sie unter [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md).  
  
 Wenn die Sortierung der Datenbank das ergänzende Zeichenflag unterstützt, entspricht dies einer positiven ganzen Zahl von 0 bis 1114111 (0 bis 0x10FFFF). Wenn ein Wert außerhalb dieses Bereichs angegeben wurde, wird NULL zurückgegeben.  
  
## <a name="return-types"></a>Rückgabetypen  
 **NCHAR(1)-Wert** Wenn die standarddatenbanksortierung nicht ergänzende Zeichen unterstützt.  
  
 **nvarchar(2)** Wenn die standarddatenbanksortierung ergänzende Zeichen unterstützt.  
  
 Wenn der Parameter *Integer_expression* liegt im Bereich 0 - 0xFFFF liegt, wird nur ein Zeichen zurückgegeben. Bei höheren Werten gibt NCHAR das entsprechende Ersatzzeichenpaar zurück. Erstellen Sie kein Ersatzzeichenpaar mit `NCHAR(<High surrogate>) + NCHAR(\<Low Surrogate>)`. Verwenden Sie stattdessen eine Datenbanksortierung, die ergänzende Zeichen unterstützt, und geben Sie dann den Unicode-Codepunkt für das Ersatzzeichenpaar an. Im folgenden Beispiel werden sowohl die alte Methode zur Erstellung eines Ersatzzeichenpaares sowie die bevorzugte Methode zur Angabe des Unicode-Codepunkts erläutert.  
  
```  
CREATE DATABASE test COLLATE Finnish_Swedish_100_CS_AS_SC;  
DECLARE @d nvarchar(10) = N'ࣅ炙   
-– Old style method.  
SELECT NCHAR(0xD84C) + NCHAR(0xDD7F);   
  
-- Preferred method.   
SELECT NCHAR(143743);   
  
-- Alternative preferred method.  
SELECT NCHAR(UNICODE(@d));    
```  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-nchar-and-unicode"></a>A. Verwenden von NCHAR und UNICODE  
 Im folgenden Beispiel werden die Funktionen `UNICODE` und `NCHAR` zur Ausgabe des `UNICODE`- und des `NCHAR`-Wertes (Unicode-Zeichen) des zweiten Zeichens der Zeichenfolge `København` verwendet sowie zur Ausgabe des tatsächlichen zweiten Zeichens `ø`.  
  
```  
DECLARE @nstring nchar(8);  
SET @nstring = N'København';  
SELECT UNICODE(SUBSTRING(@nstring, 2, 1)),   
   NCHAR(UNICODE(SUBSTRING(@nstring, 2, 1)));  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----------- -   
248         ø  
(1 row(s) affected)  
```  
  
### <a name="b-using-substring-unicode-convert-and-nchar"></a>B. Verwenden von SUBSTRING, UNICODE, CONVERT und NCHAR  
 Im folgenden Beispiel werden die Funktionen `SUBSTRING`, `UNICODE`, `CONVERT` und `NCHAR` zur Ausgabe der Zeichennummer, des Unicode-Zeichens und des UNICODE-Wertes für jedes Zeichen in der Zeichenfolge `København` verwendet.  
  
```  
-- The @position variable holds the position of the character currently  
-- being processed. The @nstring variable is the Unicode character   
-- string to process.  
DECLARE @position int, @nstring nchar(9);  
-- Initialize the current position variable to the first character in   
-- the string.  
SET @position = 1;  
-- Initialize the character string variable to the string to process.  
-- Notice that there is an N before the start of the string. This   
-- indicates that the data following the N is Unicode data.  
SET @nstring = N'København';  
-- Print the character number of the position of the string you are at,   
-- the actual Unicode character you are processing, and the UNICODE   
-- value for this particular character.  
PRINT 'Character #' + ' ' + 'Unicode Character' + ' ' + 'UNICODE Value';  
WHILE @position <= DATALENGTH(@nstring)  
   BEGIN  
   SELECT @position,   
      NCHAR(UNICODE(SUBSTRING(@nstring, @position, 1))),  
      CONVERT(NCHAR(17), SUBSTRING(@nstring, @position, 1)),  
      UNICODE(SUBSTRING(@nstring, @position, 1))  
   SELECT @position = @position + 1  
   END;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Character # Unicode Character UNICODE Value  
  
----------- ---- ----------------- -----------   
1           K    K                 75  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
2           ø    ø                 248  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
3           b    b                 98  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
4           e    e                 101  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
5           n    n                 110  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
6           h    h                 104  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
7           a    a                 97  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
8           v    v                 118  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
9           n    n                 110  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
10          NULL                   NULL  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
11          NULL                   NULL  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
12          NULL                   NULL  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
13          NULL                   NULL  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
14          NULL                   NULL  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
15          NULL                   NULL  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
16          NULL                   NULL  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
17          NULL                   NULL  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
18          NULL                   NULL  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Zeichenfolgenfunktionen &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [Unicode- &#40; Transact-SQL &#41;](../../t-sql/functions/unicode-transact-sql.md)  
  
  



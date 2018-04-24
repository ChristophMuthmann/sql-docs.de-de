---
title: SUBSTRING (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 10/21/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- SUBSTRING
- SUBSTRING_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- portion of expression returned [SQL Server]
- part of expression returned [SQL Server]
- SUBSTRING function
- offsets [SQL Server]
- binary [SQL Server], returning part of
- expressions [SQL Server], part returned
- characters [SQL Server], returning part of
ms.assetid: a19c808f-aaf9-4a69-af59-b1a5fc3e5c4c
caps.latest.revision: 65
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 75aab8f9b1035e94b65d96319f8589b11e032ecb
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="substring-transact-sql"></a>SUBSTRING (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt einen Teil eines Zeichen-, Binär-, Text- oder Bildausdrucks in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
SUBSTRING ( expression ,start , length )  
```  
  
## <a name="arguments"></a>Argumente  
 *expression*  
 ist ein **character**-, **binary**-, **text**-, **ntext**- oder **image**-[Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md).  
  
 *start*  
 ist eine ganze Zahl oder ein **bigint**-Ausdruck, der angibt, wo die zurückgegebenen Zeichen beginnen. (Die Nummerierung basiert auf 1, das bedeutet, dass das erste Zeichen im Ausdruck 1 ist.) Wenn *start* kleiner als 1 ist, beginnt der zurückgegebene Ausdruck beim ersten Zeichen, das in *expression* angegeben wird. In diesem Fall handelt es sich bei der Anzahl von zurückgegebenen Zeichen um den größten Wert der Summe von *start* + *length*- 1 oder 0. Wenn *start* größer ist als die Anzahl der Zeichen in dem Werteausdruck, wird eine Zeichenfolge der Länge 0 zurückgegeben.  
  
 *length*  
 Eine positive ganze Zahl, oder ein **bigint**-Ausdruck, die angeben, wie viele Zeichen des *Ausdrucks* zurückgegeben werden. Wenn *length* negativ ist, wird ein Fehler generiert, und die Anweisung wird beendet. Wenn die Summe von *start* und *length* größer ist als die Anzahl der Zeichen in *expression*, wird der gesamte Wertausdruck, beginnend bei *start*, zurückgegeben.  
  
## <a name="return-types"></a>Rückgabetypen  
 Gibt Zeichendaten zurück, wenn *expression* einer der unterstützten Zeichendatentypen ist. Gibt Binärdaten zurück, wenn *expression* einer der unterstützten **Binärdatentypen** ist. Die zurückgegebene Zeichenfolge hat denselben Typ wie der angegebene Ausdruck, mit den folgenden Ausnahmen:  
  
|Angegebener Ausdruck|Rückgabetyp|  
|--------------------------|-----------------|  
|**char**/**varchar**/**text**|**varchar**|  
|**nchar**/**nvarchar**/**ntext**|**nvarchar**|  
|**binary**/**varbinary**/**image**|**varbinary**|  
  
## <a name="remarks"></a>Remarks  
 Die Werte für *start* und *length* müssen als Anzahl der Zeichen für die Datentypen **ntext**, **char** oder **varchar** und Bytes für die Datentypen **text**, **image**, **binary** oder **varbinary** angegeben werden.  
  
 Der *Ausdruck* muss **varchar(max)** oder **varbinary(max)** sein, wenn *start* oder *length* einen Wert enthält, der größer als 2.147.483.647 ist.  
  
## <a name="supplementary-characters-surrogate-pairs"></a>Ergänzende Zeichen (Ersatzpaare)  
 Bei SC (Supplementary Characters)-Sortierungen werden alle Ersatzzeichenpaare in *expression* von *start* und *length* als einzelne Zeichen behandelt. Weitere Informationen finden Sie unter [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md).  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-substring-with-a-character-string"></a>A. Verwenden von SUBSTRING mit einer Zeichenfolge  
 Im folgenden Beispiel wird gezeigt, wie Sie nur einen Teil einer Zeichenfolge zurückgeben können. Diese Abfrage gibt aus der Tabelle `sys.databases` in der ersten Spalte die Namen der Systemdatenbank zurück, in der zweiten Spalten den ersten Buchstaben der Datenbank und in der letzten Spalte den dritten und vierten Buchstaben.  
  
```  
SELECT name, SUBSTRING(name, 1, 1) AS Initial ,
SUBSTRING(name, 3, 2) AS ThirdAndFourthCharacters
FROM sys.databases  
WHERE database_id < 5;   
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  

|NAME |Initial |ThirdAndFourthCharacters|
|---|--|--|
|master  |m  |st |
|tempdb  |t  |mp |
|model   |m  |de |
|msdb    |m  |db |


  
 So zeigen Sie den zweiten, dritten und vierten Buchstaben der Zeichenfolgenkonstanten `abcdef` an:  
  
```  
SELECT x = SUBSTRING('abcdef', 2, 3);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
x  
----------  
bcd  
  
(1 row(s) affected)
```  
  
### <a name="b-using-substring-with-text-ntext-and-image-data"></a>B. Verwenden von SUBSTRING mit text-, ntext- und image-Daten  
  
> [!NOTE]  
>  Sie müssen die **pubs**-Datenbank installieren, um die folgenden Beispiele auszuführen.  
  
 Im folgenden Beispiel wird gezeigt, wie die ersten 10 Zeichen aus allen **text**- und **image**-Datenspalten in der `pub_info`-Tabelle der `pubs`-Datenbank zurückgegeben werden. **text**-Daten werden als **varchar** zurückgegeben, und **image**-Daten werden als **varbinary** zurückgegeben.  
  
```  
USE pubs;  
SELECT pub_id, SUBSTRING(logo, 1, 10) AS logo,   
   SUBSTRING(pr_info, 1, 10) AS pr_info  
FROM pub_info  
WHERE pub_id = '1756';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 pub_id logo    pr_info
------ ---------------------- ----------
1756   0x474946383961E3002500 This is sa

(1 row(s) affected)
```  
  
 Im folgenden Beispiel wird die Wirkung von SUBSTRING auf **text**- und auf **ntext**-Daten gezeigt. Zunächst wird in diesem Beispiel eine neue Tabelle in der `pubs`-Datenbank namens `npub_info` erstellt. Im nächsten Schritt wird die Spalte `pr_info` in der `npub_info`-Tabelle aus den ersten 80 Zeichen der `pub_info.pr_info`-Spalte erstellt und ein `ü` als erstes Zeichen hinzugefügt. Abschließend ruft ein `INNER JOIN` alle Verleger-IDs sowie den `SUBSTRING` der **text**- und **ntext**-Spalten mit Verlegerinformationen ab.  
  
```  
IF EXISTS (SELECT table_name FROM INFORMATION_SCHEMA.TABLES   
      WHERE table_name = 'npub_info')  
   DROP TABLE npub_info;  
GO  
-- Create npub_info table in pubs database. Borrowed from instpubs.sql.  
USE pubs;  
GO  
CREATE TABLE npub_info  
(  
 pub_id char(4) NOT NULL  
    REFERENCES publishers(pub_id)  
    CONSTRAINT UPKCL_npubinfo PRIMARY KEY CLUSTERED,  
pr_info ntext NULL  
);  
  
GO  
  
-- Fill the pr_info column in npub_info with international data.  
RAISERROR('Now at the inserts to pub_info...',0,1);  
  
GO  
  
INSERT npub_info VALUES('0736', N'üThis is sample text data for New Moon Books, publisher 0736 in the pubs database')  
,('0877', N'üThis is sample text data for Binnet & Hardley, publisher 0877 in the pubs databa')  
,('1389', N'üThis is sample text data for Algodata Infosystems, publisher 1389 in the pubs da')  
,('9952', N'üThis is sample text data for Scootney Books, publisher 9952 in the pubs database')  
,('1622', N'üThis is sample text data for Five Lakes Publishing, publisher 1622 in the pubs d')  
,('1756', N'üThis is sample text data for Ramona Publishers, publisher 1756 in the pubs datab')  
,('9901', N'üThis is sample text data for GGG&G, publisher 9901 in the pubs database. GGG&G i')  
,('9999', N'üThis is sample text data for Lucerne Publishing, publisher 9999 in the pubs data');  
GO  
-- Join between npub_info and pub_info on pub_id.  
SELECT pr.pub_id, SUBSTRING(pr.pr_info, 1, 35) AS pr_info,  
   SUBSTRING(npr.pr_info, 1, 35) AS npr_info  
FROM pub_info pr INNER JOIN npub_info npr  
   ON pr.pub_id = npr.pub_id  
ORDER BY pr.pub_id ASC;  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
### <a name="c-using-substring-with-a-character-string"></a>C. Verwenden von SUBSTRING mit einer Zeichenfolge  
 Im folgenden Beispiel wird gezeigt, wie Sie nur einen Teil einer Zeichenfolge zurückgeben können. Diese Abfrage gibt aus der `dbo.DimEmployee`-Tabelle den Nachnamen eines jeden Autors in einer Spalte und den ersten Buchstaben des entsprechenden Vornamens in der zweiten Spalte zurück.  
  
```  
-- Uses AdventureWorks  
  
SELECT LastName, SUBSTRING(FirstName, 1, 1) AS Initial  
FROM dbo.DimEmployee  
WHERE LastName LIKE 'Bar%'  
ORDER BY LastName;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
LastName             Initial
-------------------- -------
Barbariol            A
Barber               D
Barreto de Mattos    P
```  
  
 Das folgende Beispiel stellt dar, wie die zweiten, dritten und vierten Buchstaben der Zeichenfolgenkonstanten `abcdef` zurückgegeben werden.  
  
```  
USE ssawPDW;  
  
SELECT TOP 1 SUBSTRING('abcdef', 2, 3) AS x FROM dbo.DimCustomer;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
x
-----
bcd
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [LEFT &#40;Transact-SQL&#41;](../../t-sql/functions/left-transact-sql.md)  
 [LTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/ltrim-transact-sql.md)  
 [RIGHT &#40;Transact-SQL&#41;](../../t-sql/functions/right-transact-sql.md)  
 [RTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/rtrim-transact-sql.md)  
 [STRING_SPLIT &#40;Transact-SQL&#41;](../../t-sql/functions/string-split-transact-sql.md)  
 [TRIM &#40;Transact-SQL&#41;](../../t-sql/functions/trim-transact-sql.md)  
 [Zeichenfolgenfunktionen &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  



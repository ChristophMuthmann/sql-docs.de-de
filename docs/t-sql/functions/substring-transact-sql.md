---
title: SUBSTRING (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 10/21/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7f36ec82c65e5d52c2186c67033adddbf1700c4d
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="substring-transact-sql"></a>SUBSTRING (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt einen Teil eines Zeichen-, Binär-, Text- oder Bildausdrucks in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
SUBSTRING ( expression ,start , length )  
```  
  
## <a name="arguments"></a>Argumente  
 *expression*  
 Ist eine **Zeichen**, **binäre**, **Text**, **Ntext**, oder **Image**[Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md).  
  
 *Starten*  
 Eine ganze Zahl oder **"bigint"** Ausdruck, der angibt, wo die zurückgegebenen Zeichen beginnen. (Die Nummerierung ist 1 basierend, was bedeutet, dass das erste Zeichen im Ausdruck 1 ist). Wenn *starten* ist kleiner als 1 ist, beginnt der zurückgegebene Ausdruck beim ersten Zeichen, die im angegebenen *Ausdruck*. In diesem Fall wird die Anzahl der Zeichen, die zurückgegeben werden den größten Wert der Summe der *starten* + *Länge*– 1 oder 0. Wenn *starten* ist größer als die Anzahl der Zeichen im Wertausdruck, wird ein Ausdruck mit der Länge 0 (null) zurückgegeben.  
  
 *length*  
 Eine positive ganze Zahl oder **"bigint"** Ausdruck, der angibt, wie viele Zeichen von der *Ausdruck* zurückgegeben werden. Wenn *Länge* ist negativ ist, wird ein Fehler generiert, und die Anweisung wird beendet. Wenn die Summe der *starten* und *Länge* ist größer als die Anzahl der Zeichen in *Ausdruck*, der gesamte Wertausdruck, beginnend bei *starten*zurückgegeben wird.  
  
## <a name="return-types"></a>Rückgabetypen  
 Gibt Zeichendaten zurück, wenn *Ausdruck* ist einer der unterstützten Zeichendatentypen. Gibt Binärdaten zurück, wenn *Ausdruck* ist einer der unterstützten **binäre** Datentypen. Die zurückgegebene Zeichenfolge hat denselben Typ wie der angegebene Ausdruck, mit den folgenden Ausnahmen:  
  
|Angegebener Ausdruck|Rückgabetyp|  
|--------------------------|-----------------|  
|**Char**/**Varchar**/**Text**|**varchar**|  
|**NCHAR**/**Nvarchar**/**Ntext**|**nvarchar**|  
|**binäre**/**Varbinary**/**Bild**|**varbinary**|  
  
## <a name="remarks"></a>Hinweise  
 Die Werte für *starten* und *Länge* muss angegeben werden, in der Anzahl der Zeichen für **Ntext**, **Char**, oder **Varchar**  Datentypen und Bytes für **Text**, **Image**, **binäre**, oder **Varbinary** Datentypen.  
  
 Die *Ausdruck* muss **varchar(max)** oder **varbinary(max)** bei der *starten* oder *Länge* enthält einen Wert größer als 2147483647.  
  
## <a name="supplementary-characters-surrogate-pairs"></a>Ergänzende Zeichen (Ersatzpaare)  
 Bei Verwendung von (SC Supplementary) Characters Sortierungen beide *starten* und *Länge* alle Ersatzzeichenpaare *Ausdruck* als einzelnes Zeichen. Weitere Informationen finden Sie unter [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md).  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-substring-with-a-character-string"></a>A. Verwenden von SUBSTRING mit einer Zeichenfolge  
 Im folgenden Beispiel wird gezeigt, wie Sie nur einen Teil einer Zeichenfolge zurückgeben können. Aus der `sys.databases` Tabelle, diese Abfrage wird das System wieder Datenbanknamen in der ersten Spalte, die den ersten Buchstaben der Datenbank in der zweiten Spalte und der dritten und vierten Zeichen in die letzte Spalte.  
  
```  
SELECT name, SUBSTRING(name, 1, 1) AS Initial ,
SUBSTRING(name, 3, 2) AS ThirdAndFourthCharacters
FROM sys.databases  
WHERE database_id < 5;   
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  

|name |Initial |ThirdAndFourthCharacters|
|---|--|--|
|master  |m  |St |
|tempdb  |t  |Management Pack |
|model   |m  |de |
|msdb    |m  |DB |


  
 So zeigen Sie den zweiten, dritten und vierten Buchstaben der Zeichenfolgenkonstanten `abcdef` an:  
  
```  
SELECT x = SUBSTRING('abcdef', 2, 3);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `x`  
  
 `----------`  
  
 `bcd`  
  
 `(1 row(s) affected)`  
  
### <a name="b-using-substring-with-text-ntext-and-image-data"></a>B. Verwenden von SUBSTRING mit text-, ntext- und image-Daten  
  
> [!NOTE]  
>  Um die folgenden Beispiele auszuführen, müssen Sie installieren die **Pubs** Datenbank.  
  
 Im folgende Beispiel wird gezeigt, wie die ersten 10 Zeichen aus jeder der zurückzugebenden eine **Text** und **Image** -Datenspalte in der `pub_info` Tabelle mit der `pubs` Datenbank. **Text** Daten werden zurückgegeben, als **Varchar**, und **Image** Daten werden zurückgegeben, als **Varbinary**.  
  
```  
USE pubs;  
SELECT pub_id, SUBSTRING(logo, 1, 10) AS logo,   
   SUBSTRING(pr_info, 1, 10) AS pr_info  
FROM pub_info  
WHERE pub_id = '1756';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `pub_id logo    pr_info`  
  
 `------ ---------------------- ----------`  
  
 `1756   0x474946383961E3002500 This is sa`  
  
 `(1 row(s) affected)`  
  
 Das folgende Beispiel zeigt die Wirkung von SUBSTRING auf beiden **Text** und **Ntext** Daten. Zunächst wird in diesem Beispiel eine neue Tabelle in der `pubs`-Datenbank namens `npub_info` erstellt. Im nächsten Schritt wird die Spalte `pr_info` in der `npub_info`-Tabelle aus den ersten 80 Zeichen der `pub_info.pr_info`-Spalte erstellt und ein `ü` als erstes Zeichen hinzugefügt. Abschließend wird eine `INNER JOIN` Ruft alle Verleger-IDs und die `SUBSTRING` beider der **Text** und **Ntext** -Spalten mit Verlegerinformationen.  
  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
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
  
 `LastName             Initial`  
  
 `-------------------- -------`  
  
 `Barbariol            A`  
  
 `Barber               D`  
  
 `Barreto de Mattos    P`  
  
 Im folgende Beispiel wird gezeigt, wie das zweite zurückzugebenden dritten und vierten Buchstaben der Zeichenfolgenkonstanten `abcdef`.  
  
```  
USE ssawPDW;  
  
SELECT TOP 1 SUBSTRING('abcdef', 2, 3) AS x FROM dbo.DimCustomer;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `x`  
  
 `-----`  
  
 `bcd`  
  
## <a name="see-also"></a>Siehe auch  
 [Zeichenfolgenfunktionen &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  




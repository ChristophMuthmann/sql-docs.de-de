---
title: LEN (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 09/03/2015
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
- LEN
- LEN_TSQL
dev_langs: TSQL
helpviewer_keywords:
- LEN function
- characters [SQL Server], number of
- number of characters
ms.assetid: fa20fee4-884d-4301-891a-c03e901345ae
caps.latest.revision: "47"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 3c04897ed4143db632f2e96401caa02ecabe2f6b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="len-transact-sql"></a>LEN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt die Anzahl von Zeichen im angegebenen Zeichenfolgenausdruck zurück, wobei nachfolgende Leerzeichen ausgeschlossen werden.  
  
> [!NOTE]  
>  Um die Anzahl der Bytes, die zur Darstellung eines Ausdrucks zurückzugeben, verwenden die [DATALENGTH](../../t-sql/functions/datalength-transact-sql.md) Funktion.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
LEN ( string_expression )  
```  
  
## <a name="arguments"></a>Argumente  
 *string_expression*  
 Die Zeichenfolge [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) ausgewertet werden soll. *String_expression* kann eine Konstante, Variable oder Spalte mit Zeichen- oder Binärdaten sein.  
  
## <a name="return-types"></a>Rückgabetypen  
 **"bigint"** Wenn *Ausdruck* wird von der **varchar(max)**, **nvarchar(max)** oder **varbinary(max)** -Datentypen; andernfalls **Int**.  
  
 Wenn Sie SC-Sortierungen verwenden, betrachtet der zurückgegebene ganzzahlige Wert UTF-16-Ersatzpaare als einzelne Zeichen. Weitere Informationen finden Sie unter [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md).  
  
## <a name="remarks"></a>Hinweise  
 LEN werden nachfolgende Leerzeichen ausgeschlossen. Wenn dies ein Problem aufgetreten ist, erwägen Sie die [DATALENGTH &#40; Transact-SQL &#41; ](../../t-sql/functions/datalength-transact-sql.md) Funktion, die die Zeichenfolge nicht abtrennt. Wenn eine Unicode-Zeichenfolge zu verarbeiten, gibt die DATALENGTH doppelt so viele Zeichen zurück. Im folgenden Beispiel wird veranschaulicht, LEN und DATALENGTH mit einem Leerzeichen.  
  
```  
DECLARE @v1 varchar(40),  
    @v2 nvarchar(40);  
SELECT   
@v1 = 'Test of 22 characters ',   
@v2 = 'Test of 22 characters ';  
SELECT LEN(@v1) AS [varchar LEN] , DATALENGTH(@v1) AS [varchar DATALENGTH];  
SELECT LEN(@v2) AS [nvarchar LEN], DATALENGTH(@v2) AS [nvarchar DATALENGTH];  
  
```  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel wählt die Anzahl von Zeichen und die Daten in `FirstName` für Personen in `Australia` aus. In diesem Beispiel wird die [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank verwendet.  
  
```  
SELECT LEN(FirstName) AS Length, FirstName, LastName   
FROM Sales.vIndividualCustomer  
WHERE CountryRegionName = 'Australia';  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 Im folgende Beispiel gibt die Anzahl der Zeichen in der Spalte `FirstName` und die Namen vor- und Nachnamen der Mitarbeiter in `Australia`.  
  
```  
-- Uses AdventureWorks  
  
SELECT DISTINCT LEN(FirstName) AS FNameLength, FirstName, LastName   
FROM dbo.DimEmployee AS e  
INNER JOIN dbo.DimGeography AS g   
    ON e.SalesTerritoryKey = g.SalesTerritoryKey   
WHERE EnglishCountryRegionName = 'Australia';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
FNameLength  FirstName  LastName  
-----------  ---------  ---------------  
4            Lynn       Tsoflias
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Zeichenfolgenfunktionen &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [DATALENGTH &#40; Transact-SQL &#41;](../../t-sql/functions/datalength-transact-sql.md)   
 [Links &#40; Transact-SQL &#41;](../../t-sql/functions/left-transact-sql.md)   
 [RECHTS &#40; Transact-SQL &#41;](../../t-sql/functions/right-transact-sql.md)  
  
  



---
title: CHARINDEX (Transact-SQL) | Microsoft-Dokumentation
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
- CHARINDEX
- CHARINDEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- expressions [SQL Server], pattern searching
- CHARINDEX function
- pattern searching [SQL Server]
- starting point of expression in character string
ms.assetid: 78c10341-8373-4b30-b404-3db20e1a3ac4
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: ed2f5334c0c76288ca31cf07857a87f2d1c72033
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="charindex-transact-sql"></a>CHARINDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Sucht in einem Ausdruck nach einem anderen Ausdruck und gibt dessen Startposition zurück, falls gefunden.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
CHARINDEX ( expressionToFind , expressionToSearch [ , start_location ] )   
```  
  
## <a name="arguments"></a>Argumente  
*expressionToFind*  
Ein [Zeichenausdruck](../../t-sql/language-elements/expressions-transact-sql.md), der die zu suchende Sequenz enthält. *expressionToFind* ist auf 8000 Zeichen beschränkt.
  
*expressionToSearch*  
Der zu suchende Zeichenausdruck.
  
*start_location*  
Ein **integer** oder **bigint**-Ausdruck, bei dem die Suche beginnt. Wenn *start_location* nicht angegeben ist, eine negative Zahl oder 0 (null) ist, wird die Suche am Anfang von *expressionToSearch* begonnen.
  
## <a name="return-types"></a>Rückgabetypen
**bigint**, wenn *expressionToSearch* vom Datentyp **varchar(max)**, **nvarchar(max)** oder **varbinary(max)** ist; andernfalls **int**.
  
## <a name="remarks"></a>Remarks  
Wenn entweder *expressionToFind* oder *expressionToSearch* als Unicode-Datentypen deklariert werden kann (**nvarchar** oder **nchar**), das jeweils andere Element hingegen nicht, wird dieses in einen Unicode-Datentyp konvertiert. CHARINDEX kann nicht mit den Datentypen **text**, **ntext** und **image** verwendet werden.
  
Wenn entweder *expressionToFind* oder *expressionToSearch* NULL zurückgeben, gibt auch CHARINDEX NULL zurück.
  
Wenn *expressionToFind* innerhalb von *expressionToSearch* nicht gefunden werden kann, gibt CHARINDEX 0 (null) zurück.
  
CHARINDEX führt Vergleiche basierend auf der Sortierung der Eingabe aus. Zum Ausführen eines Vergleichs in einer angegebenen Sortierung können Sie mithilfe von COLLATE eine ausdrückliche Sortierung auf die Eingabe anwenden.
  
Die zurückgegebene Startposition ist 1-basiert, nicht 0-basiert.
  
0x0000 (**char(0)**) ist ein nicht definiertes Zeichen in Windows-Sortierungen und kann nicht in CHARINDEX enthalten sein.
  
## <a name="supplementary-characters-surrogate-pairs"></a>Ergänzende Zeichen (Ersatzpaare)  
Bei Verwendung von SC-Sortierungen werden Ersatzzeichenpaare sowohl von *start_location* als auch vom Rückgabewert als ein anstelle von zwei Zeichen gezählt. Weitere Informationen finden Sie unter [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md).
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-returning-the-starting-position-of-an-expression"></a>A. Zurückgeben der Startposition eines Ausdrucks  
Im folgenden Beispiel wird die Position zurückgegeben, an der die Zeichenfolge `bicycle` in der `DocumentSummary`-Spalte der `Document`-Tabelle in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank beginnt.
  
```sql
DECLARE @document varchar(64);  
SELECT @document = 'Reflectors are vital safety' +  
                   ' components of your bicycle.';  
SELECT CHARINDEX('bicycle', @document);  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
-----------   
48            
```  
  
### <a name="b-searching-from-a-specific-position"></a>B. Suchen ab einer bestimmten Position  
Im folgenden Beispiel wird der optionale *start_location*-Parameter verwendet, um die Suche nach `vital` beim fünften Zeichen in der `DocumentSummary`-Spalte der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank zu beginnen.
  
```sql
DECLARE @document varchar(64);  
  
SELECT @document = 'Reflectors are vital safety' +  
                   ' components of your bicycle.';  
SELECT CHARINDEX('vital', @document, 5);  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
-----------   
16            
  
(1 row(s) affected)  
```  
  
### <a name="c-searching-for-a-nonexistent-expression"></a>C. Suchen nach einem nicht vorhandenen Ausdruck  
Im folgenden Beispiel wird das Resultset dargestellt, wenn *expressionToFind* nicht in *expressionToSearch* gefunden wird.
  
```sql
DECLARE @document varchar(64);  
  
SELECT @document = 'Reflectors are vital safety' +  
                   ' components of your bicycle.';  
SELECT CHARINDEX('bike', @document);  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
-----------
0
  
(1 row(s) affected)
```
  
### <a name="d-performing-a-case-sensitive-search"></a>D. Ausführen einer Suche unter Beachtung der Groß-/Kleinschreibung  
Im folgenden Beispiel wird eine Suche nach der Zeichenfolge `'TEST'` in `'This is a Test``'` ausgeführt, wobei die Groß-/Kleinschreibung berücksichtigt wird.
  
```sql
USE tempdb;  
GO  
--perform a case sensitive search  
SELECT CHARINDEX ( 'TEST',  
       'This is a Test'  
       COLLATE Latin1_General_CS_AS);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
-----------
0
```  
  
Im folgenden Beispiel wird eine Suche nach der Zeichenfolge `'Test'` in `'This is a Test'` ausgeführt, wobei die Groß-/Kleinschreibung berücksichtigt wird.
  
```sql
  
USE tempdb;  
GO  
SELECT CHARINDEX ( 'Test',  
       'This is a Test'  
       COLLATE Latin1_General_CS_AS);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
-----------
13
```  
  
### <a name="e-performing-a-case-insensitive-search"></a>E. Ausführen einer Suche ohne Beachtung der Groß-/Kleinschreibung  
Im folgenden Beispiel wird eine Suche nach der Zeichenfolge `'TEST'` in `'This is a Test'` ausgeführt, wobei Groß-/Kleinschreibung nicht berücksichtigt wird.
  
```sql
  
USE tempdb;  
GO  
SELECT CHARINDEX ( 'TEST',  
       'This is a Test'  
       COLLATE Latin1_General_CI_AS);  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
-----------
13
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
### <a name="f-searching-from-the-start-of-a-string-expression"></a>F. Suche ab dem Beginn eines Zeichenfolgenausdrucks  
Das folgende Beispiel gibt den ersten Speicherort der `is`-Zeichenfolge in `This is a string` ab Position 1 (also ab dem ersten Zeichen) in der Zeichenfolge zurück.
  
```sql
SELECT CHARINDEX('is', 'This is a string');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
---------
3
```  
  
### <a name="g-searching-from-a-position-other-than-the-first-position"></a>G. Suchen ab einer anderen Position als der ersten  
Das folgende Beispiel gibt den ersten Speicherort der `is`-Zeichenfolge in `This is a string` ab Position 4 in der Zeichenfolge zurück.
  
```sql
SELECT CHARINDEX('is', 'This is a string', 4);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
---------
 6
 ```  
  
### <a name="h-results-when-the-string-is-not-found"></a>H. Ergebnisse, wenn die Zeichenfolge nicht gefunden wird  
Das folgende Beispiel zeigt den Rückgabewert, wenn *string_pattern* nicht in der gesuchten Zeichenfolge gefunden wird.
  
```sql
SELECT TOP(1) CHARINDEX('at', 'This is a string') FROM dbo.DimCustomer;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
---------
0
```  
  
## <a name="see-also"></a>Siehe auch
 [LEN &#40;Transact-SQL&#41;](../../t-sql/functions/len-transact-sql.md)  
 [PATINDEX &#40;Transact-SQL&#41;](../../t-sql/functions/patindex-transact-sql.md)  
 [String Functions &#40;Transact-SQL&#41; (Zeichenfolgenfunktionen (Transact-SQL))](../../t-sql/functions/string-functions-transact-sql.md)  
 [+ &#40;String Concatenation&#41; &#40;Transact-SQL&#41; (+ (Verketten von Zeichenfolgen) (Transact-SQL))](../../t-sql/language-elements/string-concatenation-transact-sql.md)  
 [Sortierung und Unicode-Unterstützung](../../relational-databases/collations/collation-and-unicode-support.md)  
  
  



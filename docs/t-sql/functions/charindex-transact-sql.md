---
title: CHARINDEX (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
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
caps.latest.revision: 52
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 80c1228faeaaa4012afc0fd27992a2f5cf389f6e
ms.openlocfilehash: 5467f9d98562fac8262e537887d03c1d68b25d88
ms.contentlocale: de-de
ms.lasthandoff: 10/12/2017

---
# <a name="charindex-transact-sql"></a>CHARINDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Sucht in einem Ausdruck nach einem anderen Ausdruck und gibt dessen Startposition zurück, falls gefunden.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
CHARINDEX ( expressionToFind , expressionToSearch [ , start_location ] )   
```  
  
## <a name="arguments"></a>Argumente  
*expressionToFind*  
Ist ein Zeichen [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) , die die zu suchende Sequenz enthält. *ExpressionToFind* ist auf 8000 Zeichen beschränkt.
  
*"expressiontosearch"*  
Der zu suchende Zeichenausdruck.
  
*"start_location"*  
Ist ein **Ganzzahl** oder **"bigint"** Ausdruck, bei dem die Suche beginnt. Wenn *"start_location"* nicht angegeben wird, ist eine negative Zahl oder 0 ist, die Suche beginnt am Anfang des *"expressiontosearch"*.
  
## <a name="return-types"></a>Rückgabetypen
**"bigint"** Wenn *"expressiontosearch"* wird von der **varchar(max)**, **nvarchar(max)**, oder **varbinary(max)** Daten Typen andernfalls **Int**.
  
## <a name="remarks"></a>Hinweise  
Wenn entweder *ExpressionToFind* oder *"expressiontosearch"* wird von einem Unicode-Datentyp (**Nvarchar** oder **Nchar**) und der andere nicht, die andere wird in einen Unicode-Datentyp konvertiert. CHARINDEX kann nicht verwendet werden, mit **Text**, **Ntext**, und **Image** -Datentypen.
  
Wenn entweder *ExpressionToFind* oder *"expressiontosearch"* NULL ist, gibt CHARINDEX NULL zurück.
  
Wenn *ExpressionToFind* befindet sich nicht innerhalb von *"expressiontosearch"*, gibt CHARINDEX 0 zurück.
  
CHARINDEX führt Vergleiche basierend auf der Sortierung der Eingabe aus. Zum Ausführen eines Vergleichs in einer angegebenen Sortierung können Sie mithilfe von COLLATE eine ausdrückliche Sortierung auf die Eingabe anwenden.
  
Die zurückgegebene Startposition ist 1-basiert, nicht 0-basiert.
  
0 x 0000 (**char(0) zurück**) ist ein nicht definiertes Zeichen in Windows-Sortierungen und kann nicht in CHARINDEX enthalten sein.
  
## <a name="supplementary-characters-surrogate-pairs"></a>Ergänzende Zeichen (Ersatzpaare)  
Bei Verwendung von SC-Sortierungen beide *"start_location"* und der Rückgabewert Count-Ersatzzeichenpaare als ein Zeichen, nicht zwei. Weitere Informationen finden Sie unter [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md).
  
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
Im folgenden Beispiel wird der optionale *"start_location"* Parameter zum Starten der Suche nach `vital` beim fünften Zeichen von der `DocumentSummary` Spalte in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] Datenbank.
  
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
Das folgende Beispiel zeigt das Ergebnis, wenn festgelegt *ExpressionToFind* befindet sich nicht innerhalb von *"expressiontosearch"*.
  
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
Im folgenden Beispiel wird die Groß-/ Kleinschreibung für die Zeichenfolge `'TEST'` in `'This is a Test``'`.
  
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
  
Im folgenden Beispiel wird die Groß-/ Kleinschreibung für die Zeichenfolge `'Test'` in `'This is a Test'`.
  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="f-searching-from-the-start-of-a-string-expression"></a>F. Suche am Anfang eines Zeichenfolgenausdrucks  
Das folgende Beispiel gibt den ersten Speicherort eines der `is` -Zeichenfolge in `This is a string`, beginnend ab Position 1 (das erste Zeichen) in der Zeichenfolge.
  
```sql
SELECT CHARINDEX('is', 'This is a string');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
---------
3
```  
  
### <a name="g-searching-from-a-position-other-than-the-first-position"></a>G. Suchen von einer anderen Position als die erste position  
Das folgende Beispiel gibt den ersten Speicherort eines der `is` -Zeichenfolge in `This is a string`, beginnend mit der vierten Position.
  
```sql
SELECT CHARINDEX('is', 'This is a string', 4);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
---------
 6
 ```  
  
### <a name="h-results-when-the-string-is-not-found"></a>H. Ergebnisse, wenn die Zeichenfolge nicht gefunden wird  
Das folgende Beispiel zeigt den Rückgabewert, wenn die *String_pattern* befindet sich nicht in den durchsuchten Zeichenfolge.
  
```sql
SELECT TOP(1) CHARINDEX('at', 'This is a string') FROM dbo.DimCustomer;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
---------
0
```  
  
## <a name="see-also"></a>Siehe auch
[Zeichenfolgenfunktionen &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
[+ &#40; Verketten von Zeichenfolgen &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/string-concatenation-transact-sql.md)  
[Sortierung und Unicode-Unterstützung](../../relational-databases/collations/collation-and-unicode-support.md)
  
  




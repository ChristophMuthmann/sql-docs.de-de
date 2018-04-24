---
title: PATINDEX (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/19/2016
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
- PATINDEX
- PATINDEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- first occurrence of pattern [SQL Server]
- searches [SQL Server], pattern starting position
- starting position of patten search
- pattern searching [SQL Server]
- PATINDEX function
ms.assetid: c0dfb17f-2230-4e36-98da-a9b630bab656
caps.latest.revision: 53
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 261662a301bf0eaa754284e6255286c4c6d6cc0d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="patindex-transact-sql"></a>PATINDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt für alle gültigen Text- und Zeichendatentypen die Startposition des ersten Auftretens eines Musters in einem angegebenen Ausdruck zurück bzw. 0, wenn das Muster nicht gefunden wird.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
PATINDEX ( '%pattern%' , expression )  
```  
  
## <a name="arguments"></a>Argumente  
 *pattern*  
 Ein Zeichenausdruck, der die zu suchende Sequenz enthält. Platzhalterzeichen können verwendet werden, jedoch muss das %-Zeichen vorangestellt werden und *pattern* folgen (es sei denn, Sie suchen nach den ersten oder letzten Zeichen). *pattern* ist ein Ausdruck aus der Kategorie der Zeichenfolgen-Datentypen. *pattern* ist auf 8000 Zeichen beschränkt.  
  
 *expression*  
 Ein [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md), in der Regel eine Spalte, der nach dem angegebenen Muster durchsucht wird. *expression* ist ein Ausdruck aus der Kategorie der Zeichenfolgen-Datentypen.  
  
## <a name="return-types"></a>Rückgabetypen  
 **bigint**, wenn *expression* vom Datentyp **varchar(max)** oder **nvarchar(max)** ist; andernfalls **int**.  
  
## <a name="remarks"></a>Remarks  
 Wenn *pattern* oder *expression* NULL ist, gibt PATINDEX NULL zurück.  
  
 PATINDEX führt Vergleiche auf Basis der Sortierung der Eingabe aus. Zum Ausführen eines Vergleichs in einer angegebenen Sortierung können Sie mithilfe von COLLATE eine ausdrückliche Sortierung auf die Eingabe anwenden.  
  
## <a name="supplementary-characters-surrogate-pairs"></a>Ergänzende Zeichen (Ersatzpaare)  
 Bei SC-Sortierungen werden UTF-16-Ersatzpaare im *expression*-Parameter vom Rückgabewert als einzelnes Zeichen gezählt. Weitere Informationen finden Sie unter [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md).  
  
 0x0000 (**char(0)**) ist ein nicht definiertes Zeichen in Windows-Sortierungen und kann nicht in PATINDEX enthalten sein.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-simple-patindex-example"></a>A. Ein einfaches Beispiel für PATINDEX  
 Im folgenden Beispiel wird eine kurze Zeichenfolge (`interesting data`) auf die Startposition der Zeichen `ter` überprüft.  
  
```  
SELECT PATINDEX('%ter%', 'interesting data');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `3`  
  
### <a name="b-using-a-pattern-with-patindex"></a>B. Verwenden eines Musters mit PATINDEX  
 Im folgenden Beispiel wird die Position gefunden, an der in einer bestimmten Zeile der `ensure`-Spalte in der `DocumentSummary`-Tabelle der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank das Muster `Document` beginnt.  
  
```  
SELECT PATINDEX('%ensure%',DocumentSummary)  
FROM Production.Document  
WHERE DocumentNode = 0x7B40;  
GO   
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
-----------  
64  
(1 row(s) affected)
```  
  
 Wenn Sie die zu durchsuchenden Zeilen nicht durch eine `WHERE`-Klausel beschränken, gibt die Abfrage alle Zeilen in der Tabelle zurück und meldet Werte ungleich 0 für die Zeilen, in denen das Muster gefunden wurde, sowie 0 für alle Zeilen, in denen das Muster nicht gefunden wurde.  
  
### <a name="c-using-wildcard-characters-with-patindex"></a>C. Verwenden von Platzhalterzeichen mit PATINDEX  
 Im folgenden Beispiel wird mit dem Platzhalterzeichen % und dem Platzhalterzeichen _ nach der Position gesucht, an der das Muster `'en'` in der angegebenen Zeichenfolge beginnt und auf das ein beliebiges Zeichen sowie `'ure'` folgen (Index beginnt bei 1):  
  
```  
SELECT PATINDEX('%en_ure%', 'please ensure the door is locked');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
-----------  
8  
```  
  
 `PATINDEX` funktioniert analog zu `LIKE`; Sie können daher eines der Platzhalterzeichen verwenden. Sie müssen das Muster nicht mit Prozentzeichen umschließen. `PATINDEX('a%', 'abc')` gibt 1 und `PATINDEX('%a', 'cba')` 3 zurück.  
  
 Im Gegensatz zu `LIKE` gibt `PATINDEX` ähnlich wie `CHARINDEX` eine Position zurück.  
  
### <a name="d-using-collate-with-patindex"></a>D. Verwenden von COLLATE mit PATINDEX  
 Im folgenden Beispiel wird die `COLLATE`-Funktion verwendet, um die Sortierung des durchsuchten Ausdrucks ausdrücklich anzugeben.  
  
```  
USE tempdb;  
GO  
SELECT PATINDEX ( '%ein%', 'Das ist ein Test'  COLLATE Latin1_General_BIN) ;  
GO  
```  
  
### <a name="e-using-a-variable-to-specify-the-pattern"></a>E. Verwenden einer Variable, um das Muster anzugeben  
 Im folgenden Beispiel wird eine Variable verwendet, um einen Wert an den *pattern*-Parameter zu übergeben. In diesem Beispiel wird die [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank verwendet.  
  
```  
DECLARE @MyValue varchar(10) = 'safety';   
SELECT PATINDEX('%' + @MyValue + '%', DocumentSummary)   
FROM Production.Document  
WHERE DocumentNode = 0x7B40;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 ------------  
 22
 ```  
  

  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [CHARINDEX &#40;Transact-SQL&#41;](../../t-sql/functions/charindex-transact-sql.md)  
 [LEN &#40;Transact-SQL&#41;](../../t-sql/functions/len-transact-sql.md)  
 [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [String Functions &#40;Transact-SQL&#41; (Zeichenfolgenfunktionen (Transact-SQL))](../../t-sql/functions/string-functions-transact-sql.md)   
 [&#40;Wildcard - Character&#40;s&#41; to Match&#41; &#40;Transact-SQL&#41; (% (Platzhalterzeichen – zu suchende(s) Zeichen) (Transact-SQL))](../../t-sql/language-elements/wildcard-character-s-to-match-transact-sql.md)   
 [&#40;Wildcard - Character&#40;s&#41; to Match&#41; &#40;Transact-SQL&#41; (% (Platzhalterzeichen – nicht zu suchende(s) Zeichen) (Transact-SQL))](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)   
 [_ &#40;Wildcard - Match One Character&#41; &#40;Transact-SQL&#41; (_ (Platzhalterzeichen – einzelnes zu suchendes Zeichen) (Transact-SQL))](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)   
 [Percent character &#40;Wildcard - Character&#40;s&#41; to Match&#41; &#40;Transact-SQL&#41; (Prozentzeichen (Platzhalterzeichen – zu suchende(s) Zeichen) (Transact-SQL))](../../t-sql/language-elements/percent-character-wildcard-character-s-to-match-transact-sql.md)  
  
  



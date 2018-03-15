---
title: JSON_VALUE (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- JSON_VALUE
- JSON_VALUE_TSQL
helpviewer_keywords:
- JSON_VALUE function
- JSON, extracting
- JSON, querying
ms.assetid: cd016e14-11eb-4eaf-bf05-c7cfcc820a10
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: ab4c14769dc51c6d5b97a6ad2fe6f0cb06fad4e0
ms.sourcegitcommit: 19e1c4067142d33e8485cb903a7a9beb7d894015
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/28/2017
---
# <a name="jsonvalue-transact-sql"></a>JSON_VALUE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Extrahiert einen Skalarwert aus einer JSON-Zeichenfolge.  
  
 Informationen zum Extrahieren eines Objekts oder eines Arrays aus einer JSON-Zeichenfolge anstelle eines Skalarwerts finden Sie unter [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md). Informationen zu den Unterschieden zwischen **JSON_VALUE** und **JSON_QUERY** finden Sie unter [Vergleichen von JSON_VALUE und JSON_QUERY](../../relational-databases/json/validate-query-and-change-json-data-with-built-in-functions-sql-server.md#JSONCompare).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```sql  
JSON_VALUE ( expression , path )  
```  
  
## <a name="arguments"></a>Argumente  
 *expression*  
 Ein Ausdruck. In der Regel der Name einer Variablen oder einer Spalte, die JSON-Text enthält.  
 
 Wenn **JSON_VALUE** feststellt, dass JSON im *Ausdruck* ungültig ist, bevor der von *path* identifizierte Wert gefunden wird, gibt die Funktion einen Fehler zurück. Wenn **JSON_VALUE* den von *path* identifizierten Wert nicht findet, wird der gesamte Text durchsucht und ein Fehler zurückgegeben, wenn JSON-Text gefunden wird, der an einer beliebigen Stelle von *expression* ungültig ist.
  
 *path*  
 Ein JSON-Pfad, der die zu extrahierende Eigenschaft angibt. Weitere Informationen finden Sie unter [JSON-Pfadausdrücke &#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md).  
 
In [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] und [!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)] können Sie eine Variable als Wert von *path* bereitstellen.
  
 **JSON_VALUE** gibt einen Fehler zurück, wenn das Format von *path* ungültig ist.  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt einen einzelnen Textwert vom Typ nvarchar(4000) zurück. Die Sortierung des zurückgegebenen Werts ist identisch mit der Sortierung des Eingabeausdrucks.  
  
 Wenn der Wert 4000 Zeichen überschreitet:  
  
-   Im Lax-Modus gibt **JSON_VALUE** NULL zurück.  
  
-   Im strict-Modus gibt **JSON_VALUE** einen Fehler zurück.  
  
 Wenn Sie Skalarwerte zurückgeben müssen, die 4000 Zeichen überschreiten, verwenden Sie **OPENJSON** statt **JSON_VALUE**. Weitere Informationen finden Sie unter [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md).  
  
## <a name="remarks"></a>Remarks

### <a name="lax-mode-and-strict-mode"></a>Lax- und Strict-Modus

 Betrachten Sie folgenden JSON-Text:  
  
```json  
DECLARE @jsonInfo NVARCHAR(MAX)

SET @jsonInfo=N'{  
     "info":{    
       "type":1,  
       "address":{    
         "town":"Bristol",  
         "county":"Avon",  
         "country":"England"  
       },  
       "tags":["Sport", "Water polo"]  
    },  
    "type":"Basic"  
 }'  
```  
  
 Die folgende Tabelle vergleicht das Verhalten von **JSON_VALUE** im Lax-Modus und im Strict-Modus. Weitere Informationen zu den optionalen Pfadmodusangaben (lax oder strict) finden Sie unter [JSON-Pfadausdrücke &#40;SQLServer&#41; ](../../relational-databases/json/json-path-expressions-sql-server.md).  
  
|Pfad|Rückgabewert im Lax-Modus|Rückgabewert im strict-Modus|Weitere Informationen|  
|----------|------------------------------|---------------------------------|---------------|  
|$|NULL|Fehler|Kein Skalarwert.<br /><br /> Verwenden Sie stattdessen **JSON_QUERY**.|  
|$.info.type|N'1'|N'1'|N/V|  
|$.info.address.town|N'Bristol'|N'Bristol'|N/V|  
|$.info."address"|NULL|Fehler|Kein Skalarwert.<br /><br /> Verwenden Sie stattdessen **JSON_QUERY**.|  
|$.info.tags|NULL|Fehler|Kein Skalarwert.<br /><br /> Verwenden Sie stattdessen **JSON_QUERY**.|  
|$.info.type[0]|NULL|Fehler|Kein Array.|  
|$.info.none|NULL|Fehler|Die Eigenschaft ist nicht vorhanden.|  
  
## <a name="examples"></a>Beispiele  
  
### <a name="example-1"></a>Beispiel 1  
 Im folgenden Beispiel werden die Werte der JSON-Eigenschaften `town` und `state` in Abfrageergebnissen verwendet. Da **JSON_VALUE** die Sortierung der Quelle beibehält, hängt die Sortierreihenfolge der Ergebnisse von der Sortierung der `jsonInfo`-Spalte ab. 

> [!NOTE]
> (In diesem Beispiel wird davon ausgegangen, dass eine Tabelle namens `Person.Person` eine `jsonInfo`-Spalte mit JSON-Text enthält, und dass diese Spalte die Struktur aufweist, die zuvor in der Diskussion zum Lax- und Strict-Modus dargestellt wurde. In der Beispieldatenbank „AdventureWorks“ enthält die `Person`-Tabelle keine `jsonInfo`-Spalte.)
  
```sql  
SELECT FirstName, LastName,
 JSON_VALUE(jsonInfo,'$.info.address[0].town') AS Town
FROM Person.Person
WHERE JSON_VALUE(jsonInfo,'$.info.address[0].state') LIKE 'US%'
ORDER BY JSON_VALUE(jsonInfo,'$.info.address[0].town')
```  
  
### <a name="example-2"></a>Beispiel 2  
 Im folgenden Beispiel wird der Wert der JSON-Eigenschaft `town` in eine lokale Variable extrahiert.  
  
```sql  
DECLARE @jsonInfo NVARCHAR(MAX)
DECLARE @town NVARCHAR(32)

SET @jsonInfo=N'<array of address info>'

SET @town=JSON_VALUE(@jsonInfo,'$.info.address.town')
```  
  
### <a name="example-3"></a>Beispiel 3  
 Im folgenden Beispiel werden berechnete Spalten erstellt, die auf den Werten der JSON-Eigenschaften basieren.  
  
```sql  
CREATE TABLE dbo.Store
 (
  StoreID INT IDENTITY(1,1) NOT NULL,
  Address VARCHAR(500),
  jsonContent NVARCHAR(8000),
  Longitude AS JSON_VALUE(jsonContent, '$.address[0].longitude'),
  Latitude AS JSON_VALUE(jsonContent, '$.address[0].latitude')
 )
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [JSON Path Expressions &#40;SQL Server&#41; (JSON-Pfadausdrücke &#40;SQL Server&#41;)](../../relational-databases/json/json-path-expressions-sql-server.md)   
 [JSON-Daten &#40;SQL Server&#41;](../../relational-databases/json/json-data-sql-server.md)  
  
  

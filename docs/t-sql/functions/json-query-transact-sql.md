---
title: JSON_QUERY (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 06/02/2016
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
- JSON_QUERY
- JSON_QUERY_TSQL
helpviewer_keywords:
- JSON, extracting
- JSON, querying
- JSON_QUERY function
ms.assetid: 1ab0d90f-19b6-4988-ab4f-22fdf28b7c79
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 310d85e26226cd54eff5d1c99e94b235348a90f7
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="jsonquery-transact-sql"></a>JSON_QUERY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

 Extrahiert ein Objekt oder ein Array aus einer JSON-Zeichenfolge.  
  
 Informationen zum Extrahieren eines Skalarwerts aus einer JSON-Zeichenfolge anstelle eines Objekts oder eines Array finden Sie unter [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md). Informationen zu den Unterschieden zwischen **JSON_VALUE** und **JSON_QUERY** finden Sie unter [Vergleichen von JSON_VALUE und JSON_QUERY](../../relational-databases/json/validate-query-and-change-json-data-with-built-in-functions-sql-server.md#JSONCompare).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```sql  
JSON_QUERY ( expression [ , path ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *expression*  
 Ein Ausdruck. In der Regel der Name einer Variablen oder einer Spalte, die JSON-Text enthält.  
  
 Wenn **JSON_QUERY** sieht, dass JSON in *expression* ungültig ist, bevor sie den von *path* identifizierten Wert findet, gibt die Funktion einen Fehler zurück. Wenn **JSON_QUERY** den von *path* identifizierten Wert nicht ermittelt, wird der gesamte Text durchsucht und ein Fehler zurückgegeben, wenn JSON nirgendwo in *expression*  gültig ist.  
  
 *path*  
 Ein JSON-Pfad, der das zu extrahierende Objekt oder Array angibt.

In [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] und [!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)] können Sie eine Variable als Wert von *path* bereitstellen.

Der JSON-Pfad kann den Lax- oder Strict-Modus für die Analyse angeben. Wenn Sie den Analysemodus nicht angeben, ist der Lax-Modus die Standardeinstellung. Weitere Informationen finden Sie unter [JSON-Pfadausdrücke &#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md).  

Der Standardwert für *path* lautet „$“. Wenn Sie also keinen Wert für *path* bereitstellen, gibt **JSON_QUERY** den Eingabe-*Ausdruck* zurück.

**JSON_QUERY** gibt einen Fehler zurück, wenn das Format von *path* ungültig ist.  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt ein JSON-Fragment vom Typ nvarchar(max) zurück. Die Sortierung des zurückgegebenen Werts ist identisch mit der Sortierung des Eingabeausdrucks.  
  
 Wenn der Wert kein Objekt oder Array ist:  
  
-   Im Lax-Modus gibt **JSON_QUERY** NULL zurück.  
  
-   Im Strict-Modus gibt **JSON_QUERY** einen Fehler zurück.  
  
## <a name="remarks"></a>Remarks  

### <a name="lax-mode-and-strict-mode"></a>Lax- und Strict-Modus

 Betrachten Sie das folgende Beispiel eines JSON-Texts:  
  
```json  
{
    "info": {
        "type": 1,
        "address": {
            "town": "Bristol",
            "county": "Avon",
            "country": "England"
        },
        "tags": ["Sport", "Water polo"]
    },
    "type": "Basic"
} 
```  
  
 Die folgende Tabelle vergleicht das Verhalten von **JSON_QUERY** im Lax-Modus und im Strict-Modus. Weitere Informationen zu den optionalen Path-Modusangaben (Lax oder Strict) finden Sie unter [JSON Path Expressions &#40;SQL Server&#41; (JSON-Pfadausdrücke [SQL Server])](../../relational-databases/json/json-path-expressions-sql-server.md).  
  
|Pfad|Rückgabewert im Lax-Modus|Rückgabewert im Strict-Modus|Weitere Informationen|  
|----------|------------------------------|---------------------------------|---------------|  
|$|Gibt den gesamten JSON-Text zurück.|Gibt den gesamten JSON-Text zurück.|N/V|  
|$.info.type|NULL|Fehler|Kein Objekt oder Array.<br /><br /> Verwenden Sie stattdessen **JSON_VALUE**.|  
|$.info.address.town|NULL|Fehler|Kein Objekt oder Array.<br /><br /> Verwenden Sie stattdessen **JSON_VALUE**.|  
|$.info."address"|N'{ "town":"Bristol", "county":"Avon", "country":"England" }'|N'{ "town":"Bristol", "county":"Avon", "country":"England" }'|N/V|  
|$.info.tags|N'[ "Sport", "Water polo"]'|N'[ "Sport", "Water polo"]'|N/V|  
|$.info.type[0]|NULL|Fehler|Kein Array.|  
|$.info.none|NULL|Fehler|Die Eigenschaft ist nicht vorhanden.|  

### <a name="using-jsonquery-with-for-json"></a>Verwenden von JSON_QUERY mit FOR JSON

**JSON_QUERY** gibt ein gültiges JSON-Fragment zurück. Folglich versieht **FOR JSON** Sonderzeichen im Rückgabewert **JSON_QUERY** nicht mit Escapezeichen.

Wenn Sie verschiedene Ergebnisse mit FOR JSON zurückgeben und Sie Daten einschließen, die bereits im JSON-Format (in einer Spalte oder als Ergebnis eines Ausdrucks) vorhanden sind, dann umschließen Sie die JSON-Daten mit **JSON_QUERY** ohne den *path*-Parameter.

## <a name="examples"></a>Beispiele  
  
### <a name="example-1"></a>Beispiel 1  
 Im folgenden Beispiel wird gezeigt, wie ein JSON-Fragment einer `CustomFields`-Spalte in den Abfrageergebnissen zurückgegeben wird.  
  
```sql  
SELECT PersonID,FullName,
 JSON_QUERY(CustomFields,'$.OtherLanguages') AS Languages
FROM Application.People
```  
  
### <a name="example-2"></a>Beispiel 2  
Im folgende Beispiel wird gezeigt, wie JSON-Fragmente in die Ausgabe der FOR JSON-Klausel eingeschlossen werden.  
  
```sql  
SELECT StockItemID, StockItemName,
         JSON_QUERY(Tags) as Tags,
         JSON_QUERY(CONCAT('["',ValidFrom,'","',ValidTo,'"]')) ValidityPeriod
FROM Warehouse.StockItems
FOR JSON PATH
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [JSON-Pfadausdrücke &#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)   
 [JSON-Daten &#40;SQL Server&#41;](../../relational-databases/json/json-data-sql-server.md)  

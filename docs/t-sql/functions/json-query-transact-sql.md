---
title: JSON_QUERY (Transact-SQL) | Microsoft Docs
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
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 56b50c0497a2e0ee40f9cf086124eba8e55bdd03
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="jsonquery-transact-sql"></a>JSON_QUERY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

 Extrahiert ein Objekt oder ein Array aus einer JSON-Zeichenfolge.  
  
 Um einen skalaren Wert aus einer JSON-Zeichenfolge anstelle eines Objekts oder ein Array zu extrahieren, finden Sie unter [JSON_VALUE &#40; Transact-SQL &#41; ](../../t-sql/functions/json-value-transact-sql.md). Informationen zu den Unterschieden zwischen **JSON_VALUE** und **JSON_QUERY**, finden Sie unter [Vergleichen von JSON_VALUE und JSON_QUERY](../../relational-databases/json/validate-query-and-change-json-data-with-built-in-functions-sql-server.md#JSONCompare).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```sql  
JSON_QUERY ( expression [ , path ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *expression*  
 Ein Ausdruck. In der Regel der Name einer Variablen oder eine Spalte, die JSON-Text enthält.  
  
 Wenn **JSON_QUERY** sucht nach JSON, das ungültig ist *Ausdruck* bevor sie den Wert identifizierte findet *Pfad*, die Funktion gibt einen Fehler zurück. Wenn **JSON_QUERY** nicht ermittelt den Wert, der identifizierten *Pfad*, durchsucht den gesamten Text, und gibt einen Fehler, wenn JSON findet gilt nicht an einer beliebigen Stelle in *Ausdruck*.  
  
 *Pfad*  
 Ein JSON-Pfad, der angibt, das Objekt oder Array zu extrahieren.

In [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] und [!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)], Sie können eine Variable bereitstellen, als Wert des *Pfad*.

Der JSON-Pfad festlegbaren lax oder strict-Modus für die Analyse. Wenn Sie der Analysemodus angeben, ist der lax Modus die Standardeinstellung. Weitere Informationen finden Sie unter [JSON-Pfadausdrücke &#40; SQLServer &#41; ](../../relational-databases/json/json-path-expressions-sql-server.md).  

Der Standardwert für *Pfad* wird "$". Als Ergebnis, wenn Sie einen Wert für nicht bieten *Pfad*, **JSON_QUERY** gibt die Eingabe *Ausdruck*.

Wenn das Format der *Pfad* ist ungültig, **JSON_QUERY** gibt einen Fehler zurück.  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt eine JSON-Fragment Typ nvarchar(max) zurück. Die Sortierung des zurückgegebenen Werts ist identisch mit der Sortierung des Eingabeausdrucks.  
  
 Wenn der Wert nicht auf ein Objekt oder ein Array ist:  
  
-   Im Modus "lax" **JSON_QUERY** gibt null zurück.  
  
-   Im strict-Modus **JSON_QUERY** gibt einen Fehler zurück.  
  
## <a name="remarks"></a>Hinweise  

### <a name="lax-mode-and-strict-mode"></a>Lax und strict-Modus

 Betrachten Sie den folgenden JSON-Text ein:  
  
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
  
 Die folgende Tabelle vergleicht das Verhalten des **JSON_QUERY** im lax Modus und im strict-Modus. Weitere Informationen zu den optionalen Modus Pfadangabe ("lax" oder "strict"), finden Sie unter [JSON-Pfadausdrücke &#40; SQLServer &#41; ](../../relational-databases/json/json-path-expressions-sql-server.md).  
  
|Pfad|Rückgabewert im lax-Modus|Rückgabewert im strict-Modus|Weitere Informationen|  
|----------|------------------------------|---------------------------------|---------------|  
|$|Der gesamte JSON-Text zurückgegeben.|Der gesamte JSON-Text zurückgegeben.|N/V|  
|$. info.type|NULL|Fehler|Kein Objekt oder Array.<br /><br /> Verwendung **JSON_VALUE** stattdessen.|  
|$. info.address.town|NULL|Fehler|Kein Objekt oder Array.<br /><br /> Verwendung **JSON_VALUE** stattdessen.|  
|$.info." Address"|N'{"Stadt": "Bristol", "Landkreis": "Avon", "Land": "England"} "|N'{"Stadt": "Bristol", "Landkreis": "Avon", "Land": "England"} "|N/V|  
|$. info.tags|N "[" Sport","Water Poloshirt"]"|N "[" Sport","Water Poloshirt"]"|N/V|  
|$. info.type[0]|NULL|Fehler|Kein Array.|  
|$. info.none|NULL|Fehler|Eigenschaft ist nicht vorhanden.|  

### <a name="using-jsonquery-with-for-json"></a>Mithilfe der JSON_QUERY mit FOR JSON

**JSON_QUERY** gibt eine gültige JSON-Fragment zurück. Folglich **FOR JSON** nicht Escapesonderzeichen in der **JSON_QUERY** Rückgabewert.

Wenn von Ergebnissen mit FOR JSON zurückgeben sind, und Sie sind einschließlich der Daten, die bereits im JSON-Format (in einer Spalte oder als Ergebnis eines Ausdrucks) ist, binden Sie die JSON-Daten mit **JSON_QUERY** ohne die *Pfad* Parameter.

## <a name="examples"></a>Beispiele  
  
### <a name="example-1"></a>Beispiel 1  
 Im folgende Beispiel wird gezeigt, wie ein JSON-Fragment aus zurückgegeben eine `CustomFields` Spalte in den Abfrageergebnissen.  
  
```sql  
SELECT PersonID,FullName,
 JSON_QUERY(CustomFields,'$.OtherLanguages') AS Languages
FROM Application.People
```  
  
### <a name="example-2"></a>Beispiel 2  
Im folgende Beispiel wird gezeigt, wie JSON-Fragmente in die Ausgabe der FOR JSON-Klausel eingeschlossen wird.  
  
```sql  
SELECT StockItemID, StockItemName,
         JSON_QUERY(Tags) as Tags,
         JSON_QUERY(CONCAT('["',ValidFrom,'","',ValidTo,'"]')) ValidityPeriod
FROM Warehouse.StockItems
FOR JSON PATH
```  
  
## <a name="see-also"></a>Siehe auch  
 [JSON-Pfadausdrücke &#40; SQLServer &#41;](../../relational-databases/json/json-path-expressions-sql-server.md)   
 [JSON-Daten &#40; SQLServer &#41;](../../relational-databases/json/json-data-sql-server.md)  


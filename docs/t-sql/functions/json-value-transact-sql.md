---
title: JSON_VALUE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-json
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
caps.latest.revision: "18"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 5762af5115dd65b819bc74c3585cfc8275a516b1
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="jsonvalue-transact-sql"></a>JSON_VALUE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Extrahiert einen skalaren Wert aus einer JSON-Zeichenfolge.  
  
 Um ein Objekt oder ein Array aus einer JSON-Zeichenfolge, statt einen skalaren Wert extrahieren zu können, finden Sie unter [JSON_QUERY &#40; Transact-SQL &#41; ](../../t-sql/functions/json-query-transact-sql.md). Informationen zu den Unterschieden zwischen **JSON_VALUE** und **JSON_QUERY**, finden Sie unter [Vergleichen von JSON_VALUE und JSON_QUERY](../../relational-databases/json/validate-query-and-change-json-data-with-built-in-functions-sql-server.md#JSONCompare).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```sql  
JSON_VALUE ( expression , path )  
```  
  
## <a name="arguments"></a>Argumente  
 *expression*  
 Ein Ausdruck. In der Regel der Name einer Variablen oder eine Spalte, die JSON-Text enthält.  
 
 Wenn **JSON_VALUE** sucht nach JSON, das ungültig ist *Ausdruck* bevor sie den Wert identifizierte findet *Pfad*, die Funktion gibt einen Fehler zurück. Wenn **JSON_VALUE* nicht ermittelt den Wert, der identifizierten *Pfad*, durchsucht den gesamten Text, und gibt einen Fehler, wenn JSON findet gilt nicht an einer beliebigen Stelle in *Ausdruck*.
  
 *Pfad*  
 Ein JSON-Pfad, der angibt, die Eigenschaft zu extrahieren. Weitere Informationen finden Sie unter [JSON-Pfadausdrücke &#40; SQLServer &#41; ](../../relational-databases/json/json-path-expressions-sql-server.md).  
 
In [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] und [!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)], Sie können eine Variable bereitstellen, als Wert des *Pfad*.
  
 Wenn das Format der *Pfad* ist ungültig, **JSON_VALUE** gibt einen Fehler zurück.  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt einen einzelnen Textwert des Typs nvarchar(4000) zurück. Die Sortierung des zurückgegebenen Werts ist identisch mit der Sortierung des Eingabeausdrucks.  
  
 Wenn der Wert größer als 4000 Zeichen ist:  
  
-   Im Modus "lax" **JSON_VALUE** gibt null zurück.  
  
-   Im strict-Modus **JSON_VALUE** gibt einen Fehler zurück.  
  
 Wenn Sie Skalare Werte größer als 4000 Zeichen zurückgeben, verwenden **OPENJSON** anstelle von **JSON_VALUE**. Weitere Informationen finden Sie unter [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md).  
  
## <a name="remarks"></a>Hinweise

### <a name="lax-mode-and-strict-mode"></a>Lax und strict-Modus

 Betrachten Sie den folgenden JSON-Text ein:  
  
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
  
 Die folgende Tabelle vergleicht das Verhalten des **JSON_VALUE** im lax Modus und im strict-Modus. Weitere Informationen zu den optionalen Modus Pfadangabe ("lax" oder "strict"), finden Sie unter [JSON-Pfadausdrücke &#40; SQLServer &#41; ](../../relational-databases/json/json-path-expressions-sql-server.md).  
  
|Pfad|Rückgabewert im lax-Modus|Rückgabewert im strict-Modus|Weitere Informationen|  
|----------|------------------------------|---------------------------------|---------------|  
|$|NULL|Fehler|Nicht in einen skalaren Wert.<br /><br /> Verwendung **JSON_QUERY** stattdessen.|  
|$. info.type|N '1'|N '1'|N/V|  
|$. info.address.town|N'Bristol "|N'Bristol "|N/V|  
|$.info." Address"|NULL|Fehler|Nicht in einen skalaren Wert.<br /><br /> Verwendung **JSON_QUERY** stattdessen.|  
|$. info.tags|NULL|Fehler|Nicht in einen skalaren Wert.<br /><br /> Verwendung **JSON_QUERY** stattdessen.|  
|$. info.type[0]|NULL|Fehler|Kein Array.|  
|$. info.none|NULL|Fehler|Eigenschaft ist nicht vorhanden.|  
  
## <a name="examples"></a>Beispiele  
  
### <a name="example-1"></a>Beispiel 1  
 Das folgende Beispiel verwendet die Werte der JSON-Eigenschaften `town` und `state` in den Abfrageergebnissen. Da **JSON_VALUE** behält die Sortierung der Quelle, die Sortierreihenfolge der Ergebnisse hängt von der Sortierung der `jsonInfo` Spalte.  
  
```sql  
SELECT FirstName,LastName,
 JSON_VALUE(jsonInfo,'$.info.address[0].town') AS Town
FROM Person.Person
WHERE JSON_VALUE(jsonInfo,'$.info.address[0].state') LIKE 'US%'
ORDER BY JSON_VALUE(jsonInfo,'$.info.address[0].town')
```  
  
### <a name="example-2"></a>Beispiel 2  
 Das folgende Beispiel extrahiert den Wert der JSON-Eigenschaft `town` in eine lokale Variable.  
  
```sql  
DECLARE @jsonInfo NVARCHAR(MAX)
DECLARE @town NVARCHAR(32)

SET @jsonInfo=N'<array of address info>'

SET @town=JSON_VALUE(@jsonInfo,'$.info.address.town')
```  
  
### <a name="example-3"></a>Beispiel 3  
 Das folgende Beispiel erstellt die berechnete Spalten, die basierend auf den Werten der JSON-Eigenschaften.  
  
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
  
## <a name="see-also"></a>Siehe auch  
 [JSON-Pfadausdrücke &#40; SQLServer &#41;](../../relational-databases/json/json-path-expressions-sql-server.md)   
 [JSON-Daten &#40; SQLServer &#41;](../../relational-databases/json/json-data-sql-server.md)  
  
  

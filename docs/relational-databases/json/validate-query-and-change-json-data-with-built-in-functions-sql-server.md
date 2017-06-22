---
title: "Überprüfen, Abfragen und Ändern von JSON-Daten mit integrierten Funktionen (SQL Server) | Microsoft-Dokumentation"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- JSON, built-in functions
- functions (JSON)
ms.assetid: 6b6c7673-d818-4fa9-8708-b4ed79cb1b41
caps.latest.revision: 21
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 439b568fb268cdc6e6a817f36ce38aeaeac11fab
ms.openlocfilehash: e2b7d75694080b52e9c31e58ffd1e1f738b1035c
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="validate-query-and-change-json-data-with-built-in-functions-sql-server"></a>Überprüfen, Abfragen und Ändern von JSON-Daten mit integrierten Funktionen (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Die integrierte Unterstützung für JSON umfasst die integrierten Funktionen, die in diesem Thema beschrieben werden.  
  
-   [ISJSON](#ISJSON) testet, ob eine Zeichenfolge gültiges JSON enthält.  
  
-   [JSON_VALUE](#VALUE) extrahiert einen skalaren Wert aus einer JSON-Zeichenfolge.  
  
-   [JSON_QUERY](#QUERY) extrahiert ein Objekt oder ein Array aus einer JSON-Zeichenfolge.  
  
-   [JSON_MODIFY](#MODIFY) aktualisiert den Wert einer Eigenschaft in einer JSON-Zeichenfolge und gibt die aktualisierte JSON-Zeichenfolge zurück.  
 
## <a name="json-text-for-the-examples-on-this-page"></a>JSON-Text für die Beispiele auf dieser Seite
Die Beispiele auf dieser Seite enthalten den folgenden JSON-Text, der ein komplexes Element enthält.

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

##  <a name="ISJSON"></a> Überprüfen von JSON-Text mithilfe der ISJSON-Funktion  
 Die **ISJSON** -Funktion testet, ob eine Zeichenfolge gültiges JSON enthält.  
  
 Im folgenden Beispiel wird der JSON-Text zurückgegeben, falls die Spalte gültige JSON enthält.  
  
```sql  
SELECT id,json_col
FROM tab1
WHERE ISJSON(json_col)>0 
```  
  
 Weitere Informationen finden Sie unter [ISJSON &#40;Transact-SQL&#41;](../../t-sql/functions/isjson-transact-sql.md).  
  
##  <a name="VALUE"></a> Extrahieren eines Wertes aus JSON-Text mithilfe der JSON_VALUE-Funktion  
 Die **JSON_VALUE** -Funktion extrahiert einen skalaren Wert aus einer JSON-Zeichenfolge.  
  
 Das folgende Beispiel extrahiert den Wert einer JSON-Eigenschaft in eine lokale Variable.  
  
```sql  
SET @town=JSON_VALUE(@jsonInfo,'$.info.address.town')  
```  
  
 Weitere Informationen finden Sie unter [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md).  
  
##  <a name="QUERY"></a> Extrahieren eines Objekts oder eines Arrays aus JSON-Text mithilfe der JSON_QUERY-Funktion  
 Die **JSON_QUERY** -Funktion extrahiert ein Objekt oder ein Array aus einer JSON-Zeichenfolge.  
 
 Im folgenden Beispiel wird gezeigt, wie ein JSON-Fragment in den Abfrageergebnissen zurückgegeben wird.  
  
```sql  
SELECT FirstName,LastName,JSON_QUERY(jsonInfo,'$.info.address') AS Address
FROM Person.Person
ORDER BY LastName
```  
  
 Weitere Informationen finden Sie unter [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md).  
  
##  <a name="JSONCompare"></a> Vergleichen von JSON_VALUE und JSON_QUERY  
 Der Hauptunterschied zwischen **JSON_VALUE** und **JSON_QUERY** besteht darin, dass **JSON_VALUE** einen skalaren Wert, wogegen **JSON_QUERY** ein Objekt oder Array zurückgibt.  
  
 Betrachten Sie das folgende Beispiel eines JSON-Texts.  
  
```json  
{
    "a": "[1,2]",
    "b": [1, 2],
    "c": "hi"
}  
```  
  
 In diesem Beispiel-JSON-Text sind die Datenelemente „a“ und „c“ Zeichenfolgenwerte, während Datenelement „b“ ein Array ist. **JSON_VALUE** und **JSON_QUERY** geben die folgenden Ergebnisse zurück:  
  
|Abfrage|**JSON_VALUE** gibt zurück|**JSON_QUERY** gibt zurück|  
|-----------|-----------------------------|-----------------------------|  
|**$**|NULL oder Fehler|`{ "a": "[1,2]", "b": [1,2], "c":"hi"}`|  
|**$.a**|[1,2]|NULL oder Fehler|  
|**$.b**|NULL oder Fehler|[1,2]|  
|**$.b[0]**|1|NULL oder Fehler|  
|**$.c**|hi|NULL oder Fehler|  
  
## <a name="test-jsonvalue-and-jsonquery-with-the-adventureworks-sample-database"></a>Testen von JSON_VALUE und JSON_QUERY mit der AdventureWorks-Beispieldatenbank  
 Testen Sie die integrierten Funktionen, die in diesem Thema beschrieben werden, indem Sie die folgenden Beispiele mit der AdventureWorks-Beispieldatenbank ausführen, welche JSON-Daten beinhaltet. [Klicken Sie hier](http://www.microsoft.com/en-us/download/details.aspx?id=49502), um die AdventureWorks-Beispieldatenbank zu erhalten.  
  
 In den folgenden Beispielen enthält die Info-Spalte in der Tabelle SalesOrder_json JSON-Text.  
  
### <a name="example-1---return-both-standard-columns-and-json-data"></a>Beispiel 1 – Gib sowohl Standardspalten als auch JSON-Daten zurück  
 Die folgende Abfrage gibt sowohl die standardmäßigen relationalen Spalten sowie Werte aus einer JSON-Spalte zurück.  
  
```sql  
SELECT SalesOrderNumber,OrderDate,Status,ShipDate,Status,AccountNumber,TotalDue,
 JSON_QUERY(Info,'$.ShippingInfo') ShippingInfo,
 JSON_QUERY(Info,'$.BillingInfo') BillingInfo,
 JSON_VALUE(Info,'$.SalesPerson.Name') SalesPerson,
 JSON_VALUE(Info,'$.ShippingInfo.City') City,
 JSON_VALUE(Info,'$.Customer.Name') Customer,
 JSON_QUERY(OrderItems,'$') OrderItems
FROM Sales.SalesOrder_json
WHERE ISJSON(Info)>0
```  
  
### <a name="example-2--aggregate-and-filter-json-values"></a>Beispiel 2 – Aggregiere und filtere JSON-Werte  
 Die folgende Abfrage aggregiert Teilergebnisse nach Kundennamen (im JSON-Format gespeichert), und Status (gespeichert in einer normalen Spalte). Sie filtert dann die Ergebnisse nach Stadt (im JSON-Format gespeichert) und OrderDate (gespeichert in einer normalen Spalte).  
  
```sql  
DECLARE @territoryid INT;
DECLARE @city NVARCHAR(32);

SET @territoryid=3;

SET @city=N'Seattle';

SELECT JSON_VALUE(Info,'$.Customer.Name') AS Customer,Status,SUM(SubTotal) AS Total
FROM Sales.SalesOrder_json
WHERE TerritoryID=@territoryid
 AND JSON_VALUE(Info,'$.ShippingInfo.City')=@city
 AND OrderDate>'1/1/2015'
GROUP BY JSON_VALUE(Info,'$.Customer.Name'),Status
HAVING SUM(SubTotal)>1000
```  
  
##  <a name="MODIFY"></a> Aktualisieren von Eigenschaftswerten in JSON-Text mithilfe der JSON_MODIFY-Funktion  
 Die **JSON_MODIFY**  -Funktion aktualisiert den Wert einer Eigenschaft in einer JSON-Zeichenfolge, und gibt die aktualisierte JSON-Zeichenfolge zurück.  
  
 Im folgenden Beispiel wird der Wert einer Eigenschaft in einer Variable aktualisiert, die JSON enthält.  
  
```sql  
SET @info=JSON_MODIFY(@jsonInfo,"$.info.address[0].town",'London')    
```  
  
 Weitere Informationen finden Sie unter [JSON_MODIFY &#40;Transact-SQL&#41;](../../t-sql/functions/json-modify-transact-sql.md).  
  
## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>Erfahren Sie mehr über die integrierte JSON-Unterstützung in SQL Server  
Für viele spezifische Lösungen Fälle und Empfehlungen zu verwenden, finden Sie unter der [Blogeinträge von jovan zur integrierten JSON-Unterstützung](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) in SQL Server und Azure SQL-Datenbank von Microsoft Program Manager Jovan Popovic.
  
## <a name="see-also"></a>Siehe auch  
 [ISJSON &#40;Transact-SQL&#41;](../../t-sql/functions/isjson-transact-sql.md)   
 [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md)   
 [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md)   
 [JSON_MODIFY &#40;Transact-SQL&#41;](../../t-sql/functions/json-modify-transact-sql.md)   
 [JSON Path Expressions &#40;SQL Server&#41; (JSON-Pfadausdrücke [SQL Server])](../../relational-databases/json/json-path-expressions-sql-server.md)  
  
  


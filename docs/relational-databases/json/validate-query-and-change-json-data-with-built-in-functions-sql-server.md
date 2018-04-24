---
title: Überprüfen, Abfragen und Ändern von JSON-Daten mit integrierten Funktionen (SQL Server) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: json
ms.reviewer: douglasl
ms.suite: sql
ms.technology:
- dbe-json
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- JSON, built-in functions
- functions (JSON)
ms.assetid: 6b6c7673-d818-4fa9-8708-b4ed79cb1b41
caps.latest.revision: 21
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
ms.workload: On Demand
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: f141625abf8c12314ab1aabe3c86618f6fb18f57
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="validate-query-and-change-json-data-with-built-in-functions-sql-server"></a>Überprüfen, Abfragen und Ändern von JSON-Daten mit integrierten Funktionen (SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Die integrierte Unterstützung für JSON umfasst die integrierten Funktionen, die in diesem Thema kurz beschrieben werden.  
  
-   [ISJSON](#ISJSON) testet, ob eine Zeichenfolge gültiges JSON enthält.  
  
-   [JSON_VALUE](#VALUE) extrahiert einen skalaren Wert aus einer JSON-Zeichenfolge.  
  
-   [JSON_QUERY](#QUERY) extrahiert ein Objekt oder ein Array aus einer JSON-Zeichenfolge.  
  
-   [JSON_MODIFY](#MODIFY) aktualisiert den Wert einer Eigenschaft in einer JSON-Zeichenfolge und gibt die aktualisierte JSON-Zeichenfolge zurück.  
 
## <a name="json-text-for-the-examples-on-this-page"></a>JSON-Text für die Beispiele auf dieser Seite
Die Beispiele auf dieser Seite enthalten den folgenden JSON-Text, der ein komplexes Element enthält.

```sql 
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
  
Im folgenden Beispiel werden die Spalten zurückgegeben, falls die Spalte `json_col` ein gültiges JSON enthält.  
  
```sql  
SELECT id, json_col
FROM tab1
WHERE ISJSON(json_col) > 0 
```  

Weitere Informationen finden Sie unter [ISJSON &#40;Transact-SQL&#41;](../../t-sql/functions/isjson-transact-sql.md).  
  
##  <a name="VALUE"></a> Extrahieren eines Wertes aus JSON-Text mithilfe der JSON_VALUE-Funktion  
Die **JSON_VALUE** -Funktion extrahiert einen skalaren Wert aus einer JSON-Zeichenfolge.  
  
Das folgende Beispiel extrahiert den Wert der geschachtelten JSON-Eigenschaft `town` in eine lokale Variable.  
  
```sql  
SET @town = JSON_VALUE(@jsonInfo, '$.info.address.town')  
```  
  
Weitere Informationen finden Sie unter [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md).  
  
##  <a name="QUERY"></a> Extrahieren eines Objekts oder eines Arrays aus JSON-Text mithilfe der JSON_QUERY-Funktion  
Die **JSON_QUERY** -Funktion extrahiert ein Objekt oder ein Array aus einer JSON-Zeichenfolge.  
 
Im folgenden Beispiel wird gezeigt, wie ein JSON-Fragment in den Abfrageergebnissen zurückgegeben wird.  
  
```sql  
SELECT FirstName, LastName, JSON_QUERY(jsonInfo,'$.info.address') AS Address
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
  
|Pfad|**JSON_VALUE** gibt zurück|**JSON_QUERY** gibt zurück|  
|-----------|-----------------------------|-----------------------------|  
|**$**|NULL oder Fehler|`{ "a": "[1,2]", "b": [1,2], "c":"hi"}`|  
|**$.a**|[1,2]|NULL oder Fehler|  
|**$.b**|NULL oder Fehler|[1,2]|  
|**$.b[0]**|1|NULL oder Fehler|  
|**$.c**|hi|NULL oder Fehler|  
  
## <a name="test-jsonvalue-and-jsonquery-with-the-adventureworks-sample-database"></a>Testen von JSON_VALUE und JSON_QUERY mit der AdventureWorks-Beispieldatenbank  
Testen Sie die integrierten Funktionen, die in diesem Thema beschrieben werden, indem Sie die folgenden Beispiele mit der AdventureWorks-Beispieldatenbank ausführen. Informationen zum Herunterladen von AdventureWorks und Informationen zum Hinzufügen von JSON-Daten für Testzwecke durch Ausführen eines Skripts finden Sie unter [Test drive built-in JSON support (Testen des in die JSON-Unterstützung integrierten Laufwerks)](json-data-sql-server.md#test-drive-built-in-json-support-with-the-adventureworks-sample-database).
  
Im folgenden Beispiel enthält die `Info`-Spalte in der Tabelle `SalesOrder_json` den JSON-Text.  
  
### <a name="example-1---return-both-standard-columns-and-json-data"></a>Beispiel 1 – Gib sowohl Standardspalten als auch JSON-Daten zurück  
Die folgende Abfrage gibt sowohl die relationalen Standardspalten sowie Werte aus einer JSON-Spalte zurück.  
  
```sql  
SELECT SalesOrderNumber, OrderDate, Status, ShipDate, Status, AccountNumber, TotalDue,
 JSON_QUERY(Info,'$.ShippingInfo') ShippingInfo,
 JSON_QUERY(Info,'$.BillingInfo') BillingInfo,
 JSON_VALUE(Info,'$.SalesPerson.Name') SalesPerson,
 JSON_VALUE(Info,'$.ShippingInfo.City') City,
 JSON_VALUE(Info,'$.Customer.Name') Customer,
 JSON_QUERY(OrderItems,'$') OrderItems
FROM Sales.SalesOrder_json
WHERE ISJSON(Info) > 0
```  
  
### <a name="example-2--aggregate-and-filter-json-values"></a>Beispiel 2 – Aggregiere und filtere JSON-Werte  
Die folgende Abfrage aggregiert Teilergebnisse nach Kundennamen (im JSON-Format gespeichert), und Status (gespeichert in einer normalen Spalte). Sie filtert dann die Ergebnisse nach Stadt (im JSON-Format gespeichert) und Bestelldatum (gespeichert in einer normalen Spalte).  
  
```sql  
DECLARE @territoryid INT;
DECLARE @city NVARCHAR(32);

SET @territoryid=3;

SET @city=N'Seattle';

SELECT JSON_VALUE(Info, '$.Customer.Name') AS Customer, Status, SUM(SubTotal) AS Total
FROM Sales.SalesOrder_json
WHERE TerritoryID=@territoryid
 AND JSON_VALUE(Info, '$.ShippingInfo.City') = @city
 AND OrderDate > '1/1/2015'
GROUP BY JSON_VALUE(Info, '$.Customer.Name'), Status
HAVING SUM(SubTotal)>1000
```  
  
##  <a name="MODIFY"></a> Aktualisieren von Eigenschaftswerten in JSON-Text mithilfe der JSON_MODIFY-Funktion  
Die **JSON_MODIFY**-Funktion aktualisiert den Wert einer Eigenschaft in einer JSON-Zeichenfolge, und gibt die aktualisierte JSON-Zeichenfolge zurück.  
  
Im folgenden Beispiel wird der Wert einer JSON-Eigenschaft in einer Variable aktualisiert, die JSON enthält.  
  
```sql  
SET @info = JSON_MODIFY(@jsonInfo, "$.info.address[0].town", 'London')    
```  
  
 Weitere Informationen finden Sie unter [JSON_MODIFY &#40;Transact-SQL&#41;](../../t-sql/functions/json-modify-transact-sql.md).  
  
## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>Weitere Informationen zu JSON in SQL Server und Azure SQL-Datenbank  
  
### <a name="microsoft-blog-posts"></a>Microsoft-Blogbeiträge  
  
Spezielle Lösungen, Anwendungsfälle und Empfehlungen finden Sie in den [Blogbeiträgen über die integrierte JSON-Unterstützung](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) in SQL-Server und in Azure SQL-Datenbank.  

### <a name="microsoft-videos"></a>Microsoft-Videos

Eine visuelle Einführung in die JSON-Unterstützung, die in SQL Server und Azure SQL-Datenbank integriert ist, finden Sie in den folgenden Videos:

-   [SQL Server 2016 and JSON Support](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [Using JSON in SQL Server 2016 and Azure SQL Database](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [JSON as a bridge between NoSQL and relational worlds](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [ISJSON &#40;Transact-SQL&#41;](../../t-sql/functions/isjson-transact-sql.md)   
 [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md)   
 [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md)   
 [JSON_MODIFY &#40;Transact-SQL&#41;](../../t-sql/functions/json-modify-transact-sql.md)   
 [JSON Path Expressions &#40;SQL Server&#41; (JSON-Pfadausdrücke [SQL Server])](../../relational-databases/json/json-path-expressions-sql-server.md)  
  
  

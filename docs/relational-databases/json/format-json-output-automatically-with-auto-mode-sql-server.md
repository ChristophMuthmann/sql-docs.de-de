---
title: Automatisches Formatieren der JSON-Ausgabe im AUTO-Modus (SQL Server) | Microsoft-Dokumentation
ms.custom:
- SQL2016_New_Updated
ms.date: 07/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FOR JSON AUTO
ms.assetid: 178a2a4e-e0f6-49b9-9895-396956d3c7d9
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 9045ebe77cf2f60fecad22672f3f055d8c5fdff2
ms.openlocfilehash: 0a1219eb4dac8621ef678cf309ef36b4b039536b
ms.contentlocale: de-de
ms.lasthandoff: 07/31/2017

---
# <a name="format-json-output-automatically-with-auto-mode-sql-server"></a>Automatisches Formatieren der JSON-Ausgabe im AUTO-Modus (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Wenn die Ausgabe der **FOR JSON**-Klausel automatisch entsprechend der Struktur der **SELECT**-Anweisung formatiert werden soll, geben Sie die Option **AUTO** an.  
  
Wenn Sie die Option **AUTO** angeben, entspricht das Format der JSON-Ausgabe automatisch der Reihenfolge der Spalten in der SELECT-Liste und deren Quelltabellen. Dieses Format können Sie nicht ändern.
 
Wenn Sie die vollständige Kontrolle über die Ausgabe behalten möchten, geben Sie alternativ die Option **PATH** an.
-   Weitere Informationen zur Option **PATH** finden Sie unter [Format Nested JSON Output with PATH Mode (Formatieren einer geschachtelten JSON-Ausgabe im PATH-Modus)](../../relational-databases/json/format-nested-json-output-with-path-mode-sql-server.md).
-   Einen Überblick über die beiden Optionen finden Sie unter [Format Query Results as JSON with FOR JSON (Formatieren von Abfrageergebnissen als JSON mit FOR JSON)](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md).

Eine Abfrage, die die Option **FOR JSON AUTO** verwendet, benötigt eine **FROM** -Klausel.  
  
Nachstehend finden Sie einige Beispiele für die **FOR JSON** -Klausel mit der Option **AUTO** .  
  
## <a name="examples"></a>Beispiele

### <a name="example-1"></a>Beispiel 1
 **Abfrage**  
  
Die Ergebnisse der FOR JSON AUTO-Klausel ähneln den Ergebnissen von FOR JSON PATH, wenn nur eine Tabelle in der Abfrage verwendet wird. In diesem Fall erstellt FOR JSON AUTO keine geschachtelten Objekte. Der einzige Unterschied besteht darin, dass FOR JSON AUTO durch Punkt getrennte Aliase (z.B. `Info.MiddleName` im folgenden Beispiel) als Schlüssel mit Punkten ausgibt, nicht als geschachtelte Objekte.  
  
```sql  
SELECT TOP 5   
       BusinessEntityID As Id,  
       FirstName, LastName,  
       Title As 'Info.Title',  
       MiddleName As 'Info.MiddleName'  
   FROM Person.Person  
   FOR JSON AUTO  
```  
  
 **Ergebnis**  
  
```json  
[{
    "Id": 1,
    "FirstName": "Ken",
    "LastName": "Sánchez",
    "Info.MiddleName": "J"
}, {
    "Id": 2,
    "FirstName": "Terri",
    "LastName": "Duffy",
    "Info.MiddleName": "Lee"
}, {
    "Id": 3,
    "FirstName": "Roberto",
    "LastName": "Tamburello"
}, {
    "Id": 4,
    "FirstName": "Rob",
    "LastName": "Walters"
}, {
    "Id": 5,
    "FirstName": "Gail",
    "LastName": "Erickson",
    "Info.Title": "Ms.",
    "Info.MiddleName": "A"
}]
```  

### <a name="example-2"></a>Beispiel 2

**Abfrage**  
  
Wenn Sie Tabellen verknüpfen, werden die Spalten der ersten Tabelle als Eigenschaften des Stammobjekts generiert. Die Spalten der zweiten Tabelle werden als Eigenschaften eines geschachtelten Objekts generiert. Der Tabellenname oder Alias der zweiten Tabelle (z.B. `D` im folgenden Beispiel) wird als Name des geschachtelten Arrays verwendet.  
  
```sql  
SELECT TOP 2 SalesOrderNumber,  
        OrderDate,  
        UnitPrice,  
        OrderQty  
FROM Sales.SalesOrderHeader H  
   INNER JOIN Sales.SalesOrderDetail D  
     ON H.SalesOrderID = D.SalesOrderID  
FOR JSON AUTO   
```  
  
**Ergebnis**  
  
```json  
[{
    "SalesOrderNumber": "SO43659",
    "OrderDate": "2011-05-31T00:00:00",
    "D": [{
        "UnitPrice": 24.99,
        "OrderQty": 1
    }]
}, {
    "SalesOrderNumber": "SO43659",
    "D": [{
        "UnitPrice": 34.40
    }, {
        "UnitPrice": 134.24,
        "OrderQty": 5
    }]
}]
```  

### <a name="example-3"></a>Beispiel 3
 
**Abfrage**  
Statt FOR JSON AUTO zu verwenden, können Sie eine FOR JSON PATH-Unterabfrage in der SELECT-Anweisung schachteln, wie im folgenden Beispiel gezeigt. In diesem Beispiel wird das gleiche Ergebnis ausgegeben wie im vorherigen Beispiel.  
  
```sql  
SELECT TOP 2  
    SalesOrderNumber,  
    OrderDate,  
    (SELECT UnitPrice, OrderQty  
      FROM Sales.SalesOrderDetail AS D  
      WHERE H.SalesOrderID = D.SalesOrderID  
     FOR JSON PATH) AS D  
FROM Sales.SalesOrderHeader AS H  
FOR JSON PATH  
```  
  
**Ergebnis**  
  
```json  
[{
    "SalesOrderNumber": "SO43659",
    "OrderDate": "2011-05-31T00:00:00",
    "D": [{
        "UnitPrice": 24.99,
        "OrderQty": 1
    }]
}, {
    "SalesOrderNumber": "SO4390",
    "D": [{
        "UnitPrice": 24.99
    }]
}]
```  

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>Erfahren Sie mehr über die integrierte JSON-Unterstützung in SQL Server  
Viele spezifische Lösungen, Anwendungsfälle und Empfehlungen finden Sie im [Blogbeitrag über die integrierte JSON-Unterstützung](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) in SQL-Server und in Azure SQL-Datenbank von Jovan Popovic, Program Manager bei Microsoft.

## <a name="see-also"></a>Siehe auch  
 [FOR-Klausel &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)  


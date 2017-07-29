---
title: Formatieren einer geschachtelten JSON-Ausgabe im PATH-Modus (SQL Server) | Microsoft-Dokumentation
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
ms.assetid: 032761b0-6358-42e4-b05c-dbfd663ac881
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 1aa87e3d821e6d111948baa0843edf31d087d739
ms.openlocfilehash: 3fc86f957f4ece3564d8f72558467cdf6c54c935
ms.contentlocale: de-de
ms.lasthandoff: 07/18/2017

---
# <a name="format-nested-json-output-with-path-mode-sql-server"></a>Formatieren einer geschachtelten JSON-Ausgabe im PATH-Modus (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Wenn Sie die vollständige Kontrolle über die Ausgabe der **FOR JSON**-Klausel behalten möchten, geben Sie die Option **PATH** an.  
  
Im**PATH** -Modus können Sie Wrapper-Objekte erstellen und komplexe Eigenschaften schachteln. Die Ergebnisse werden als Array von JSON-Objekten formatiert.  
  
Alternativ können Sie die Option **AUTO** verwenden, um die Ausgabe automatisch entsprechend der Struktur der **SELECT**-Anweisung zu formatieren.
 -   Weitere Informationen zur Option **AUTO** finden Sie unter [Automatisches Formatieren der JSON-Ausgabe im AUTO-Modus](../../relational-databases/json/format-json-output-automatically-with-auto-mode-sql-server.md).
 -   Einen Überblick über die beiden Optionen finden Sie unter [Formatieren von Abfrageergebnissen als JSON mit FOR JSON &#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md).
 
Hier sind einige Beispiele für die **FOR JSON** -Klausel mit der Option **PATH** . Geschachtelte Ergebnisse formatieren Sie, wie nachfolgend gezeigt, mit durch Punkte getrennten Spaltennamen oder mit verschachtelten Abfragen. Nullwerte sind standardmäßig nicht in der **FOR JSON**-Ausgabe enthalten.  

## <a name="example---dot-separated-column-names"></a>Beispiel – Durch Punkte getrennte Spaltennamen  
Die ersten fünf Zeilen der AdventureWorks-Tabelle `Person` werden durch die Abfrage als JSON formatiert.  

Die Klausel **FOR JSON PATH** verwendet das Spaltenalias oder einen Spaltennamen, um den Schlüsselnamen in der JSON-Ausgabe zu bestimmen. Wenn ein Alias Punkte enthält, erstellt die Option PATH geschachtelte Objekte.  

 **Abfrage**  
  
```sql  
SELECT TOP 5   
       BusinessEntityID As Id,  
       FirstName, LastName,  
       Title As 'Info.Title',  
       MiddleName As 'Info.MiddleName'  
   FROM Person.Person  
   FOR JSON PATH   
```  
  
 **Ergebnis**  
  
```json  
[{
    "Id": 1,
    "FirstName": "Ken",
    "LastName": "Sanchez",
    "Info": {
        "MiddleName": "J"
    }
}, {
    "Id": 2,
    "FirstName": "Terri",
    "LastName": "Duffy",
    "Info": {
        "MiddleName": "Lee"
    }
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
    "Info": {
        "Title": "Ms.",
        "MiddleName": "A"
    }
}]
```  
   
## <a name="example---multiple-tables"></a>Beispiel – Mehrere Tabellen  
Wenn Sie in einer Abfrage auf mehr als eine Tabelle verweisen, schachtelt **FOR JSON PATH** jede Spalte mithilfe des Alias. Die folgende Abfrage erstellt ein JSON-Objekt pro (OrderHeader, OrderDetails) Paar, das in der Abfrage verknüpft ist. 
  
 **Abfrage**  
  
```sql  
SELECT TOP 2 SalesOrderNumber AS 'Order.Number',  
        OrderDate AS 'Order.Date',  
        UnitPrice AS 'Product.Price',  
        OrderQty AS 'Product.Quantity'  
FROM Sales.SalesOrderHeader H  
   INNER JOIN Sales.SalesOrderDetail D  
     ON H.SalesOrderID = D.SalesOrderID  
FOR JSON PATH   
```  
  
 **Ergebnis**  
  
```json  
[{
    "Order": {
        "Number": "SO43659",
        "Date": "2011-05-31T00:00:00"
    },
    "Product": {
        "Price": 2024.9940,
        "Quantity": 1
    }
}, {
    "Order": {
        "Number": "SO43659"
    },
    "Product": {
        "Price": 2024.9940
    }
}]
```  

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>Erfahren Sie mehr über die integrierte JSON-Unterstützung in SQL Server  
Für viele spezifische Lösungen Fälle und Empfehlungen zu verwenden, finden Sie unter der [Blogeinträge von jovan zur integrierten JSON-Unterstützung](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) in SQL Server und Azure SQL-Datenbank von Microsoft Program Manager Jovan Popovic.

## <a name="see-also"></a>Siehe auch  
 [FOR-Klausel &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)  


---
title: "Formatieren einer geschachtelten JSON-Ausgabe im PATH-Modus (SQL Server) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "06/02/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-json"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 032761b0-6358-42e4-b05c-dbfd663ac881
caps.latest.revision: 19
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 16
---
# Formatieren einer geschachtelten JSON-Ausgabe im PATH-Modus (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Wenn Sie die vollständige Kontrolle über das Format der JSON-Ausgabe behalten möchten, geben Sie mit der Klausel **FOR JSON** die Option **PATH** an.  
  
 Im **PATH**-Modus können Sie Wrapper-Objekte erstellen und komplexe Eigenschaften schachteln. Die Ergebnisse werden wie ein JSON-Objekt-Array formatiert.  
  
 Hier sind einige Beispiele für die **FOR JSON**-Klausel mit der Option **PATH**. Geschachtelte Ergebnisse formatieren Sie, wie nachfolgend gezeigt, mit durch Punkte getrennten Spaltennamen oder mit verschachtelten Abfragen. Nullwerte sind standardmäßig nicht in der Ausgabe enthalten.  
  
## Beispiel – Durch Punkte getrennte Spaltennamen  
 Die ersten fünf Zeilen der AdventureWorks Tabelle „Person“ werden durch die Abfrage als JSON formatiert.  
  
 **Abfrage**  
  
```tsql  
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
[  
    {"Id":1,"FirstName":"Ken","LastName":"Sánchez","Info":{"MiddleName":"J"}},  
    {"Id":2,"FirstName":"Terri","LastName":"Duffy","Info":{"MiddleName":"Lee"}},  
    {"Id":3,"FirstName":"Roberto","LastName":"Tamburello"},  
    {"Id":4,"FirstName":"Rob","LastName":"Walters"},  
    {"Id":5,"FirstName":"Gail","LastName":"Erickson","Info":{"Title":"Ms.","MiddleName":"A"}}  
]  
```  
  
 Die Klausel FOR JSON PATH verwendet ein Spaltenalias oder einen Spaltennamen, um den Schlüsselnamen in der JSON-Ausgabe zu bestimmen. Wenn einige Aliase Punkte enthalten, erstellt die FOR JSON PATH-Klausel ein geschachteltes Objekt. Beachten Sie, dass Zellen mit NULL-Werten nicht in der Ausgabe generiert werden.  
  
## Beispiel – Mehrere Tabellen  
 Enthält Ihre Abfrage Verweise auf mehr als eine Tabelle, werden die Ergebnisse als flache Liste dargestellt und anschließend verschachtelt die FOR JSON PATH-Klausel jede Spalte mithilfe ihres Alias. Die folgende Abfrage erstellt ein JSON-Objekt pro (OrderHeader, OrderDetails) Paar, das in der Abfrage verknüpft ist:  
  
 **Abfrage**  
  
```tsql  
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
[  
  {  
    "Order":{  
        "Number":"SO43659",  
        "Date":"2011-05-31T00:00:00"  
      },  
    "Product":{  
         "Price":2024.9940,  
         "Quantity":1  
     }  
  },  
  {  
    "Order":{ "Number":"SO43659“ },  
    "Product":{"Price":2024.9940}  
  }  
]  
```  
  
## Siehe auch  
 [FOR-Klausel &#40;Transact-SQL&#41;](../Topic/FOR%20Clause%20\(Transact-SQL\).md)  
  
  
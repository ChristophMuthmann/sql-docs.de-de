---
title: "Automatisches Formatieren der JSON-Ausgabe im AUTO-Modus (SQL Server) | Microsoft Docs"
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
helpviewer_keywords: 
  - "FOR JSON AUTO"
ms.assetid: 178a2a4e-e0f6-49b9-9895-396956d3c7d9
caps.latest.revision: 17
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 15
---
# Automatisches Formatieren der JSON-Ausgabe im AUTO-Modus (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Wenn die JSON-Ausgabe automatisch entsprechend der Struktur der **SELECT**-Anweisung formatiert werden soll, geben Sie die Option **AUTO** mit der **FOR JSON**Klausel an.  
  
 Die Option **AUTO** bestimmt das Format der JSON-Ausgabe automatisch entsprechend der Reihenfolge der Spalten in der SELECT-Liste und deren Quelltabellen. Dieses Format können Sie nicht ändern.  
  
 Eine Abfrage, die die Option **FOR JSON AUTO** verwendet, benötigt eine **FROM**-Klausel.  
  
 Nachstehend finden Sie einige Beispiele für die **FOR JSON**-Klausel mit der Option **AUTO**.  
  
## Beispiele  
 **Abfrage 1**  
  
 Die Ergebnisse der FOR JSON AUTO-Klausel ähneln FOR JSON PATH, wenn nur eine Tabelle in der Abfrage verwendet wird. In diesem Fall erstellt FOR JSON AUTO keine geschachtelten Objekte. Der einzige Unterschied ist, dass durch Punkte getrennte Aliase als Schlüssel mit Punkten generiert werden (d.h. FOR JSON AUTO verwendet keine Spaltenaliase für die Formatierung ).  
  
```tsql  
SELECT TOP 5   
      BusinessEntityID As Id,  
      FirstName, LastName,  
      Title As 'Info.Title',  
      MiddleName As 'Info.MiddleName'  
  FROM Person.Person  
  FOR JSON AUTO  
```  
  
 **Ergebnis 1**  
  
```json  
[  
      {"Id":1,"FirstName":"Ken","LastName":"Sánchez","Info.MiddleName":"J"},  
      {"Id":2,"FirstName":"Terri","LastName":"Duffy","Info.MiddleName":"Lee"},  
      {"Id":3,"FirstName":"Roberto","LastName":"Tamburello"},  
      {"Id":4,"FirstName":"Rob","LastName":"Walters"},  
      {"Id":5,"FirstName":"Gail","LastName":"Erickson","Info.Title":"Ms.","Info.MiddleName":"A"}  
]  
```  
  
 **Abfrage 2**  
  
 Wenn Sie Tabellen verknüpfen, werden die Spalten der ersten Tabelle als Eigenschaften des Stammobjekts generiert. Die Spalten der zweiten Tabelle werden als Eigenschaften eines geschachtelten Objekts generiert. Der Tabellenname oder das Alias der zweiten Tabelle wird als Name des geschachtelten Arrays verwendet.  
  
```tsql  
SELECT TOP 2 SalesOrderNumber,  
       OrderDate,  
       UnitPrice,  
       OrderQty  
FROM Sales.SalesOrderHeader H  
  INNER JOIN Sales.SalesOrderDetail D  
    ON H.SalesOrderID = D.SalesOrderID  
FOR JSON AUTO  
```  
  
 **Ergebnis 2**  
  
```json  
[  
  {  
       "SalesOrderNumber":"SO43659",  
        "OrderDate":"2011-05-31T00:00:00",  
        "D":[  
            {"UnitPrice":24.99, "OrderQty":1  }  
         ]  
  },  
  {  
       "SalesOrderNumber":"SO43659" ,  
       "D":[  
          { "UnitPrice":34.40  },  
          { "UnitPrice":134.24, "OrderQty":5 }  
        ]  
  }  
]  
  
```  
  
## Beispiele – Generieren einer geschachtelten JSON-Ausgabe  
 Anstelle von FOR JSON AUTO können Sie geschachtelte FOR JSON-Abfragen schreiben, die mit der FOR JSON PATH-Klausel im SELECT-Teil der Hauptabfrage platziert werden, wie in die folgenden Beispiele zeigen.  
  
 **Abfrage 1**  
  
```tsql  
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
  
 **Ergebnis 1**  
  
```json  
[  
  {  
       "SalesOrderNumber":"SO43659",  
        "OrderDate":"2011-05-31T00:00:00",  
        "D":[  
            { "UnitPrice":24.99,  "OrderQty":1 }  
         ]  
  },  
  {  
       "SalesOrderNumber":"SO4390" ,  
       "D":[  
            { "UnitPrice":24.99 }  
        ]  
  }  
]  
  
```  
  
## Siehe auch  
 [FOR-Klausel &#40;Transact-SQL&#41;](../Topic/FOR%20Clause%20\(Transact-SQL\).md)  
  
  
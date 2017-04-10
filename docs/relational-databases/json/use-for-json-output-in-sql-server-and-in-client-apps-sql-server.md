---
title: "Verwenden der FOR JSON-Ausgabe in SQL Server und in Client-Apps (SQL Server) | Microsoft Docs"
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
  - "FOR JSON, Verwendung in Client-Apps"
  - "FOR JSON, Verwendung in SQL Server"
ms.assetid: 302e5397-b499-4ea3-9a7f-c24ccad698eb
caps.latest.revision: 12
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 11
---
# Verwenden der FOR JSON-Ausgabe in SQL Server und in Client-Apps (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Die folgenden Beispiele veranschaulichen einige Möglichkeiten, die **FOR JSON**-Klausel oder ihre Ausgabe in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oder Client-Apps zu verwenden.  
  
## Verwenden der FOR JSON-Ausgabe in SQL Server-Variablen  
 Die Ausgabe der FOR JSON-Klausel ist vom Typ NVARCHAR(MAX) und kann daher jeder Variablen zugewiesen werden, wie im folgenden Beispiel gezeigt.  
  
```tsql  
DECLARE @x NVARCHAR(MAX) = (SELECT TOP 10 * FROM Sales.SalesOrderHeader FOR JSON AUTO)  
```  
  
## Verwenden der FOR JSON-Ausgabe in benutzerdefinierten SQL Server-Funktionen  
 Sie können benutzerdefinierte Funktionen erstellen, die Resultsets als JSON formatieren und diese JSON-Ausgabe zurückgeben. Im folgenden Beispiel wird eine benutzerdefinierte Funktion erstellt, die einige Auftragsdetailzeilen abruft und sie als JSON-Array formatiert.  
  
```tsql  
CREATE FUNCTION GetSalesOrderDetails(@salesOrderId int)  
RETURNS NVARCHAR(MAX)  
AS  
BEGIN  
  RETURN (SELECT UnitPrice, OrderQty  
          FROM Sales.SalesOrderDetail  
          WHERE SalesOrderID = @salesOrderId  
          FOR JSON AUTO)  
END  
```  
  
 Sie können diese Funktion in einem Batch oder in einer Abfrage verwenden, wie im folgenden Beispiel gezeigt.  
  
```tsql  
DECLARE @x NVARCHAR(MAX) = dbo.GetSalesOrderDetails(43659)  
PRINT dbo.GetSalesOrderDetails(43659)  
SELECT TOP 10 H.*, dbo.GetSalesOrderDetails(H.SalesOrderId) AS Details  
FROM Sales.SalesOrderHeader H  
```  
  
## Zusammenführen von übergeordneten und untergeordneten Daten in einer einzelnen Tabelle  
 Im folgenden Beispiel wird jeder Satz untergeordneter Zeilen als JSON-Array formatiert, und aus diesem wird der Wert der Spalte „Details“ in der übergeordneten Tabelle.  
  
```tsql  
select top 10 SalesOrderId, OrderDate,  
     (select top 3 UnitPrice, OrderQty  
        from Sales.SalesOrderDetail D  
        where H.SalesOrderId = D.SalesOrderID  
        for json auto) as Details  
into SalesOrder  
from Sales.SalesOrderHeader H  
```  
  
## Aktualisieren der Daten in JSON-Spalten  
 Im folgenden Beispiel wird gezeigt, dass Sie den Wert der Spalten aktualisieren können, die JSON-Text enthalten.  
  
```tsql  
UPDATE SalesOrder  
SET Details =  
    (SELECT TOP 1 UnitPrice, OrderQty  
      FROM Sales.SalesOrderDetail D  
      WHERE D.SalesOrderId = SalesOrder.SalesOrderId  
     FOR JSON AUTO)  
```  
  
## Verwenden der FOR JSON-Ausgabe in einer C#-Client-App  
 Im folgenden Beispiel wird veranschaulicht, wie die JSON-Ausgabe einer Abfrage in ein StringBuilder-Objekt in einer C#-Client-App abgerufen wird. Angenommen, die Variable „queryWithForJson“ enthält den Text einer SELECT-Anweisung mit einer FOR JSON-Klausel.  
  
```csharp  
var cmd = new SqlCommand(queryWithForJson, conn);  
conn.Open();  
var jsonResult = new StringBuilder();  
var reader = cmd.ExecuteReader();  
if (!reader.HasRows)  
{  
    jsonResult.Append("[]");  
}  
else  
{  
    while (reader.Read())  
    {  
        jsonResult.Append(reader.GetValue(0).ToString());  
    }  
}  
```  
  
## Siehe auch  
 [Formatieren von Abfrageergebnisse als JSON mit FOR JSON &#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
  
  
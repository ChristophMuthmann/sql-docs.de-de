---
title: Verwenden der FOR JSON-Ausgabe in SQL Server und in Client-Apps (SQL Server) | Microsoft-Dokumentation
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
- FOR JSON, using in client apps
- FOR JSON, using in SQL Server
ms.assetid: 302e5397-b499-4ea3-9a7f-c24ccad698eb
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: Human Translation
ms.sourcegitcommit: 439b568fb268cdc6e6a817f36ce38aeaeac11fab
ms.openlocfilehash: 9383b62ac3413b0e4dc8780413bdde09bfc04af3
ms.contentlocale: de-de
ms.lasthandoff: 06/23/2017

---
# <a name="use-for-json-output-in-sql-server-and-in-client-apps-sql-server"></a>Verwenden der FOR JSON-Ausgabe in SQL Server und in Client-Apps (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Die folgenden Beispiele veranschaulichen einige Möglichkeiten zum Verwenden der **FOR JSON** -Klausel und die JSON-Ausgabe im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oder in Client-apps.  
  
## <a name="use-for-json-output-in-sql-server-variables"></a>Verwenden der FOR JSON-Ausgabe in SQL Server-Variablen  
Die Ausgabe der FOR JSON-Klausel ist vom Typ NVARCHAR(MAX) und aus, damit Sie es jeder Variablen zuweisen können wie im folgenden Beispiel gezeigt.  
  
```sql  
DECLARE @x NVARCHAR(MAX) = (SELECT TOP 10 * FROM Sales.SalesOrderHeader FOR JSON AUTO)  
```  
  
## <a name="use-for-json-output-in-sql-server-user-defined-functions"></a>Verwenden der FOR JSON-Ausgabe in benutzerdefinierten SQL Server-Funktionen  
 Sie können benutzerdefinierte Funktionen erstellen, die Resultsets als JSON formatieren und diese JSON-Ausgabe zurückgeben. Im folgenden Beispiel wird eine benutzerdefinierte Funktion erstellt, die einige Auftragsdetailzeilen abruft und sie als JSON-Array formatiert.  
  
```sql  
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
  
```sql  
DECLARE @x NVARCHAR(MAX) = dbo.GetSalesOrderDetails(43659)

PRINT dbo.GetSalesOrderDetails(43659)

SELECT TOP 10
  H.*, dbo.GetSalesOrderDetails(H.SalesOrderId) AS Details
FROM Sales.SalesOrderHeader H
```  
  
## <a name="merge-parent-and-child-data-into-a-single-table"></a>Zusammenführen von übergeordneten und untergeordneten Daten in einer einzelnen Tabelle  
Im folgenden Beispiel wird jeder Satz untergeordneter Zeilen als JSON-Array formatiert. Das JSON-Array wird der Wert der Spalte "Details" in der übergeordneten Tabelle.  
  
```sql  
SELECT TOP 10 SalesOrderId, OrderDate,  
      (SELECT TOP 3 UnitPrice, OrderQty  
         FROM Sales.SalesOrderDetail D  
         WHERE H.SalesOrderId = D.SalesOrderID  
         FOR JSON AUTO) AS Details  
INTO SalesOrder  
FROM Sales.SalesOrderHeader H  
```  
  
## <a name="update-the-data-in-json-columns"></a>Aktualisieren der Daten in JSON-Spalten  
 Im folgende Beispiel wird veranschaulicht, dass Sie den Wert einer Spalte aktualisieren können, die JSON-Text enthält.  
  
```sql  
UPDATE SalesOrder  
SET Details =  
     (SELECT TOP 1 UnitPrice, OrderQty  
       FROM Sales.SalesOrderDetail D  
       WHERE D.SalesOrderId = SalesOrder.SalesOrderId  
      FOR JSON AUTO 
```  
  
## <a name="use-for-json-output-in-a-c-client-app"></a>Verwenden der FOR JSON-Ausgabe in einer C#-Client-App  
 Im folgenden Beispiel wird veranschaulicht, wie die JSON-Ausgabe einer Abfrage in ein StringBuilder-Objekt in einer C#-Client-App abgerufen wird. Vorausgesetzt, dass die Variable `queryWithForJson` enthält den Text einer SELECT-Anweisung mit einer FOR JSON-Klausel.  
  
```csharp  
var queryWithForJson = "SELECT ... FOR JSON";
var conn = new SqlConnection("<connection string>");
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

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>Erfahren Sie mehr über die integrierte JSON-Unterstützung in SQL Server  
Für viele spezifische Lösungen Fälle und Empfehlungen zu verwenden, finden Sie unter der [Blogeinträge von jovan zur integrierten JSON-Unterstützung](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) in SQL Server und Azure SQL-Datenbank von Microsoft Program Manager Jovan Popovic.
 
## <a name="see-also"></a>Siehe auch  
 [Formatieren von Abfrageergebnisse als JSON mit FOR JSON &#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
  
  


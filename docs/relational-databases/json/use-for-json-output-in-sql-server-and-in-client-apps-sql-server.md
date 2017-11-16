---
title: Verwenden der FOR JSON-Ausgabe in SQL Server und in Client-Apps (SQL Server) | Microsoft-Dokumentation
ms.custom: 
ms.date: 06/02/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: json
ms.reviewer: 
ms.suite: sql
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
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 9045ebe77cf2f60fecad22672f3f055d8c5fdff2
ms.openlocfilehash: 1fa05e61c8c057141eceee65c5c1da39c5d4200e
ms.contentlocale: de-de
ms.lasthandoff: 07/31/2017

---
# <a name="use-for-json-output-in-sql-server-and-in-client-apps-sql-server"></a>Verwenden der FOR JSON-Ausgabe in SQL Server und in Client-Apps (SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Die folgenden Beispiele veranschaulichen einige Möglichkeiten, die **FOR JSON**-Klausel und ihre JSON-Ausgabe in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oder Client-Apps zu verwenden.  
  
## <a name="use-for-json-output-in-sql-server-variables"></a>Verwenden der FOR JSON-Ausgabe in SQL Server-Variablen  
Die Ausgabe der FOR JSON-Klausel ist vom Typ NVARCHAR(MAX) und kann daher jeder Variablen zugewiesen werden, wie im folgenden Beispiel gezeigt.  
  
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
Im folgenden Beispiel wird jeder Satz von untergeordneten Zeilen als JSON-Array formatiert. Das JSON-Array wird der Wert der Spalte „Details“ in der übergeordneten Tabelle.  
  
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
 Im folgenden Beispiel wird gezeigt, dass Sie den Wert einer Spalte aktualisieren können, die JSON-Text enthält.  
  
```sql  
UPDATE SalesOrder  
SET Details =  
     (SELECT TOP 1 UnitPrice, OrderQty  
       FROM Sales.SalesOrderDetail D  
       WHERE D.SalesOrderId = SalesOrder.SalesOrderId  
      FOR JSON AUTO 
```  
  
## <a name="use-for-json-output-in-a-c-client-app"></a>Verwenden der FOR JSON-Ausgabe in einer C#-Client-App  
 Im folgenden Beispiel wird veranschaulicht, wie die JSON-Ausgabe einer Abfrage in ein StringBuilder-Objekt in einer C#-Client-App abgerufen wird. Angenommen, die Variable `queryWithForJson` enthält den Text einer SELECT-Anweisung mit einer FOR JSON-Klausel.  
  
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
Viele spezifische Lösungen, Anwendungsfälle und Empfehlungen finden Sie im [Blogbeitrag über die integrierte JSON-Unterstützung](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) in SQL-Server und in Azure SQL-Datenbank von Jovan Popovic, Program Manager bei Microsoft.
 
## <a name="see-also"></a>Siehe auch  
 [Formatieren von Abfrageergebnisse als JSON mit FOR JSON &#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
  
  


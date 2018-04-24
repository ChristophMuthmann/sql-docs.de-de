---
title: Implementieren eines CASE-Ausdrucks in einer nativ kompilierten gespeicherten Prozedur | Microsoft-Dokumentation
ms.custom: ''
ms.date: 11/21/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: in-memory-oltp
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2f82db01-da7e-4a7d-8bc0-48b245e6f768
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 884aa0d1acc75bac791dfdcc8ef1c10eceb1a02e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="implementing-a-case-expression-in-a-natively-compiled-stored-procedure"></a>Implementieren eines CASE-Ausdrucks in einer systemintern kompilierten gespeicherten Prozedur
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

**Gilt für:**  [!INCLUDE[ssSDSFull_md](../../includes/ssSDSFull_md.md)] und SQL Server ab Version [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]

CASE-Ausdrücke werden in nativ kompilierten gespeicherten T-SQL-Modulen unterstützt. Das folgende Beispiel zeigt, wie Sie den CASE-Ausdruck in einer Abfrage verwenden können. 

``` 
-- Query using a CASE expression in a natively compiled stored procedure.
CREATE PROCEDURE dbo.usp_SOHOnlineOrderResult  
   WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
   AS BEGIN ATOMIC WITH  (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE=N'us_english')  
   SELECT   
      SalesOrderID,   
      CASE (OnlineOrderFlag)   
      WHEN 1 THEN N'Order placed online by customer'  
      ELSE N'Order placed by sales person'  
      END  
   FROM Sales.SalesOrderHeader_inmem
END  
GO  
  
EXEC dbo.usp_SOHOnlineOrderResult  
GO  
``` 

**Gilt für:**  [!INCLUDE[ssSQL14-md](../../includes/ssSQL14-md.md)] und SQL Server ab Version [!INCLUDE[ssSQL15-md](../../includes/ssSQL15-md.md)]

  CASE-Ausdrücke werden *nicht* in nativ kompilierten T-SQL-Modulen unterstützt. Das folgende Beispiel zeigt eine Möglichkeit, die Funktionalität eines CASE-Ausdrucks in einer systemintern kompilierten gespeicherten Prozedur zu implementieren.  
  
 In den Codebeispielen wird eine Tabellenvariable verwendet, durch die ein einzelnes Resultset erstellt wird. Dies empfiehlt sich nur, wenn die Anzahl der verarbeiteten Zeilen begrenzt ist, da hierbei eine zusätzliche Kopie der Datenzeilen erstellt wird.  
  
 Sie sollten die Leistung dieser Problemumgehung testen.  
  
```  
-- original query  
SELECT   
   SalesOrderID,   
   CASE (OnlineOrderFlag)   
   WHEN 1 THEN N'Order placed online by customer'  
   ELSE N'Order placed by sales person'  
   END  
FROM Sales.SalesOrderHeader_inmem  
  
--  workaround for CASE in natively compiled stored procedures  
--  use a table for the single resultset  
CREATE TYPE dbo.SOHOnlineOrderResult AS TABLE  
(  
   SalesOrderID uniqueidentifier not null index ix_SalesOrderID,  
     OrderFlag nvarchar(100) not null  
) with (memory_optimized=on)  
go  
  
-- natively compiled stored procedure that includes the query  
CREATE PROCEDURE dbo.usp_SOHOnlineOrderResult  
   WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
   AS BEGIN ATOMIC WITH  
      (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE=N'us_english')  
  
   -- table variable for creating the single resultset  
   DECLARE @result dbo.SOHOnlineOrderResult  
  
   -- CASE OnlineOrderFlag=1  
   INSERT @result   
   SELECT SalesOrderID, N'Order placed online by customer'  
      FROM Sales.SalesOrderHeader_inmem  
      WHERE OnlineOrderFlag=1  
  
   -- ELSE  
   INSERT @result   
   SELECT SalesOrderID, N'Order placed by sales person'  
      FROM Sales.SalesOrderHeader_inmem  
      WHERE OnlineOrderFlag!=1  
  
   -- return single resultset  
   SELECT SalesOrderID, OrderFlag FROM @result  
END  
GO  
  
EXEC dbo.usp_SOHOnlineOrderResult  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Migrationsprobleme bei nativ kompilierten gespeicherten Prozeduren](../../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md)   
 [Von In-Memory OLTP nicht unterstützte Transact-SQL-Konstrukte](../../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md)  
  
  

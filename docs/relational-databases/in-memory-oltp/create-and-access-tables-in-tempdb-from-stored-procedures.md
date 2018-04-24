---
title: Erstellen und Zugreifen auf Tabellen in TempDB aus gespeicherten Prozeduren | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/07/2017
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
ms.assetid: 12be8011-b76c-45c1-8f55-7f46e0e374e9
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: b299b96beb4d5278305867ea6515fa27580396fb
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="create-and-access-tables-in-tempdb-from-stored-procedures"></a>Erstellen und Zugreifen auf Tabellen in TempDB aus gespeicherten Prozeduren
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Das Erstellen von und Zugreifen auf Tabellen in TempDB aus systemintern kompilierten gespeicherten Prozeduren wird nicht unterstützt. Verwenden Sie stattdessen entweder speicheroptimierte Tabellen mit DURABILITY=SCHEMA_ONLY, oder verwenden Sie Tabellentypen und Tabellenvariablen. 

Weitere Details zur Speicheroptimierung temporärer Tabellen- und Tabellenvariablenszenarios finden Sie unter [Faster temp table and table variable by using memory optimization](../../relational-databases/in-memory-oltp/faster-temp-table-and-table-variable-by-using-memory-optimization.md)(Schnellere Leistung von temporären Tabellen und Tabellenvariablen mithilfe von Speicheroptimierung).
  
  Im folgenden Beispiel wird veranschaulicht, wie Sie anstelle einer temporären Tabelle mit drei Spalten (id, ProductID, Quantity) eine Tabellenvariable **@OrderQuantityByProduct** des Typs **dbo.OrderQuantityByProduct**verwenden können:  
  
```sql  
CREATE TYPE dbo.OrderQuantityByProduct   
  AS TABLE   
   (id INT NOT NULL PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT=100000),   
    ProductID INT NOT NULL,   
    Quantity INT NOT NULL) WITH (MEMORY_OPTIMIZED=ON)  
GO  
CREATE PROCEDURE dbo.usp_OrderQuantityByProduct   
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH   
(  
    TRANSACTION ISOLATION LEVEL = SNAPSHOT,  
    LANGUAGE = N'ENGLISH'  
)  
  -- declare table variables for the list of orders   
  DECLARE @OrderQuantityByProduct dbo.OrderQuantityByProduct  
  
  -- populate input  
  INSERT @OrderQuantityByProduct SELECT ProductID, Quantity FROM dbo.[Order Details]  
  end  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Migrationsprobleme bei nativ kompilierten gespeicherten Prozeduren](../../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md)   
 [Von In-Memory OLTP nicht unterstützte Transact-SQL-Konstrukte](../../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md)  
  
  

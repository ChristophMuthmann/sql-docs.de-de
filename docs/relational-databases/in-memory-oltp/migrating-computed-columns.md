---
title: Migrieren von berechneten Spalten | Microsoft-Dokumentation
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: in-memory-oltp
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 64a9eade-22c3-4a9d-ab50-956219e08df1
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f4fda63a6cf7dae045a247eb26163d0e041841b8
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="migrating-computed-columns"></a>Migrieren von berechneten Spalten
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Berechnete Spalten werden in speicheroptimierten Tabellen nicht unterstützt. Sie können jedoch eine berechnete Spalte simulieren.

**Applies to:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.  
Ab [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1 werden in speicheroptimierten Tabellen und Indizes berechnete Spalten unterstützt.

Sie sollten berücksichtigen, dass berechnete Spalten beibehalten werden müssen, wenn Sie datenträgerbasierte Tabellen zu speicheroptimierten Tabellen migrieren. Aufgrund der unterschiedlichen Leistungsmerkmale speicheroptimierter Tabellen und systemintern kompilierter gespeicherter Prozeduren ist u. U. keine Persistenz erforderlich.  
  
## <a name="non-persisted-computed-columns"></a>Nicht permanent berechnete Spalten  
 Um die Auswirkungen einer nicht permanent berechneten Spalte zu simulieren, erstellen Sie eine Sicht für die speicheroptimierte Tabelle. Fügen Sie in der SELECT-Anweisung, durch die die Sicht definiert wird, die Definition der berechneten Spalte in die Sicht ein. Außer in einer systemintern kompilierten gespeicherten Prozedur sollten Abfragen, die Werte aus der berechneten Spalte verwenden, aus der Sicht lesen. Innerhalb der systemintern kompilierten gespeicherten Prozeduren sollten Sie eine SELECT-, UPDATE- oder DELETE-Anweisung gemäß der Definition der berechneten Spalte aktualisieren.  
  
```tsql  
-- Schema for the table dbo.OrderDetails:  
-- OrderId int not null primary key,  
-- ProductId int not null,  
-- SalePrice money not null,  
-- Quantity int not null,  
-- Total money not null  
--  
-- Total is computed as SalePrice * Quantity and is not persisted.  
CREATE VIEW dbo.v_order_details AS  
   SELECT  
      OrderId,  
      ProductId,  
      SalePrice,  
      Quantity,  
      Quantity * SalePrice AS Total  
   FROM dbo.order_details  
```  
  
## <a name="persisted-computed-columns"></a>Permanent berechnete Spalten  
 Um die Auswirkungen einer permanent berechneten Spalte zu simulieren, erstellen Sie eine gespeicherte Prozedur zum Einfügen in die Tabelle und eine weitere gespeicherte Prozedur zum Aktualisieren der Tabelle. Wenn Sie die Tabelle einfügen oder aktualisieren, rufen Sie diese gespeicherten Prozeduren auf, um diese Tasks auszuführen. Innerhalb der gespeicherten Prozeduren berechnen Sie den Wert für das berechnete Feld gemäß den Eingaben, ähnlich der Definition der berechneten Spalte in der ursprünglichen datenträgerbasierten Tabelle. Anschließend können Sie die Tabelle nach Bedarf in der gespeicherten Prozedur einfügen oder aktualisieren.  
  
```tsql  
-- Schema for the table dbo.OrderDetails:  
-- OrderId int not null primary key,  
-- ProductId int not null,  
-- SalePrice money not null,  
-- Quantity int not null,  
-- Total money not null  
--  
-- Total is computed as SalePrice * Quantity and is persisted.  
-- we need to create insert and update procedures to calculate Total.  
CREATE PROCEDURE sp_insert_order_details   
@OrderId int, @ProductId int, @SalePrice money, @Quantity int  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH (LANGUAGE = N'english', TRANSACTION ISOLATION LEVEL = SNAPSHOT)  
-- compute the value here.   
-- this stored procedure works with single rows only.  
-- for bulk inserts, accept a table-valued parameter into the stored procedure  
-- and use an INSERT INTO SELECT statement.  
DECLARE @total money = @SalePrice * @Quantity  
INSERT INTO dbo.OrderDetails (OrderId, ProductId, SalePrice, Quantity, Total)  
VALUES (@OrderId, @ProductId, @SalePrice, @Quantity, @total)  
END  
GO  
  
CREATE PROCEDURE sp_update_order_details_by_id  
@OrderId int, @ProductId int, @SalePrice money, @Quantity int  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH (LANGUAGE = N'english', TRANSACTION ISOLATION LEVEL = SNAPSHOT)  
-- compute the value here.   
-- this stored procedure works with single rows only.  
DECLARE @total money = @SalePrice * @Quantity  
UPDATE dbo.OrderDetails   
SET ProductId = @ProductId, SalePrice = @SalePrice, Quantity = @Quantity, Total = @total  
WHERE OrderId = @OrderId  
END  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Migrieren zu In-Memory OLTP](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)  
  
  


---
title: Erstellen einer speicheroptimierten Tabelle und einer systemintern kompilierten gespeicherten Prozedur | Microsoft-Dokumentation
ms.custom:
- SQL2016_New_Updated
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 48a9a0a3-930f-477b-bd0f-e82e77999ecc
caps.latest.revision: 35
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: cf291b900f61590446776dab273d2fcc14509234
ms.lasthandoff: 04/11/2017

---
# <a name="creating-a-memory-optimized-table-and-a-natively-compiled-stored-procedure"></a>Erstellen einer speicheroptimierten Tabelle und einer systemintern kompilierten gespeicherten Prozedur
  Dieses Thema enthält ein Beispiel, das Sie in die Syntax für In-Memory OLTP einführt.  
  
 Um einer Anwendung die Verwendung von In-Memory OLTP zu ermöglichen, müssen folgende Aufgaben ausgeführt werden:  
  
-   Erstellen Sie eine speicheroptimierte Datendateigruppe, und fügen Sie der Dateigruppe einen Container hinzu.  
  
-   Erstellen Sie speicheroptimierte Tabellen und Indizes. Weitere Informationen finden Sie unter [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md).  
  
-   Laden Sie Daten in die speicheroptimierte Tabelle, und aktualisieren Sie die Statistiken, nachdem Sie die Daten geladen haben und bevor Sie die kompilierten gespeicherten Prozeduren erstellen. Weitere Informationen finden Sie unter [Statistiken für speicheroptimierte Tabellen](../../relational-databases/in-memory-oltp/statistics-for-memory-optimized-tables.md).  
  
-   Erstellen Sie systemintern kompilierte gespeicherte Prozeduren für den Zugriff auf Daten in speicheroptimierten Tabellen. Weitere Informationen finden Sie unter [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md). Sie können auch herkömmliches interpretiertes [!INCLUDE[tsql](../../includes/tsql-md.md)] für den Zugriff auf Daten in speicheroptimierten Tabellen verwenden.  
  
-   Migrieren Sie bei Bedarf Daten aus vorhandenen Tabellen zu den speicheroptimierten Tabellen.  
  
 Weitere Informationen zur Verwendung von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , um speicheroptimierte Tabellen zu erstellen, finden Sie unter [SQL Server Management Studio-Unterstützung für In-Memory-OLTP](../../relational-databases/in-memory-oltp/sql-server-management-studio-support-for-in-memory-oltp.md).  
  
 Im folgenden Codebeispiel ist das Verzeichnis c:\Data erforderlich.  
  
```tsql  
CREATE DATABASE imoltp   
GO  
  
--------------------------------------  
-- create database with a memory-optimized filegroup and a container.  
ALTER DATABASE imoltp ADD FILEGROUP imoltp_mod CONTAINS MEMORY_OPTIMIZED_DATA   
ALTER DATABASE imoltp ADD FILE (name='imoltp_mod1', filename='c:\data\imoltp_mod1') TO FILEGROUP imoltp_mod   
ALTER DATABASE imoltp SET MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT=ON  
GO  
  
USE imoltp  
GO  
  
-- create a durable (data will be persisted) memory-optimized table  
-- two of the columns are indexed  
  CREATE TABLE dbo.ShoppingCart (   
    ShoppingCartId INT IDENTITY(1,1) PRIMARY KEY NONCLUSTERED,  
    UserId INT NOT NULL INDEX ix_UserId NONCLUSTERED HASH WITH (BUCKET_COUNT=1000000),   
    CreatedDate DATETIME2 NOT NULL,   
    TotalPrice MONEY  
    ) WITH (MEMORY_OPTIMIZED=ON)   
  GO  
  
 -- create a non-durable table. Data will not be persisted, data loss if the server turns off unexpectedly  
 CREATE TABLE dbo.UserSession (   
   SessionId INT IDENTITY(1,1) PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT=400000),   
   UserId int NOT NULL,   
   CreatedDate DATETIME2 NOT NULL,  
   ShoppingCartId INT,  
   INDEX ix_UserId NONCLUSTERED HASH (UserId) WITH (BUCKET_COUNT=400000)   
 )   
 WITH (MEMORY_OPTIMIZED=ON, DURABILITY=SCHEMA_ONLY)   
 GO  
  
-- insert data into the tables  
INSERT dbo.UserSession VALUES (342, SYSDATETIME(), 4)   
INSERT dbo.UserSession VALUES (65, SYSDATETIME(), NULL)   
INSERT dbo.UserSession VALUES (8798, SYSDATETIME(), 1)   
INSERT dbo.UserSession VALUES (80, SYSDATETIME(), NULL)   
INSERT dbo.UserSession VALUES (4321, SYSDATETIME(), NULL)   
INSERT dbo.UserSession VALUES (8578, SYSDATETIME(), NULL)   
  
INSERT dbo.ShoppingCart VALUES (8798, SYSDATETIME(), NULL)   
INSERT dbo.ShoppingCart VALUES (23, SYSDATETIME(), 45.4)   
INSERT dbo.ShoppingCart VALUES (80, SYSDATETIME(), NULL)   
INSERT dbo.ShoppingCart VALUES (342, SYSDATETIME(), 65.4)   
GO  
  
-- verify table contents   
  SELECT * FROM dbo.UserSession   
  SELECT * FROM dbo.ShoppingCart   
  GO  
  
--  update statistics on memory-optimized tables   
  UPDATE STATISTICS dbo.UserSession WITH FULLSCAN, NORECOMPUTE   
  UPDATE STATISTICS dbo.ShoppingCart WITH FULLSCAN, NORECOMPUTE   
  GO  
  
-- in an explicit transaction, assign a cart to a session and update the total price.   
-- SELECT/UPDATE/DELETE statements in explicit transactions   
  BEGIN TRAN   
   UPDATE dbo.UserSession SET ShoppingCartId=3 WHERE SessionId=4   
   UPDATE dbo.ShoppingCart SET TotalPrice=65.84 WHERE ShoppingCartId=3   
 COMMIT   
 GO   
  
 -- verify table contents   
 SELECT *   
 FROM dbo.UserSession u JOIN dbo.ShoppingCart s on u.ShoppingCartId=s.ShoppingCartId   
 WHERE u.SessionId=4   
 GO  
  
-- natively compiled stored procedure for assigning a shopping cart to a session   
 CREATE PROCEDURE dbo.usp_AssignCart @SessionId int   
 WITH NATIVE_COMPILATION, SCHEMABINDING   
 AS   
 BEGIN ATOMIC   
 WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
  
  DECLARE @UserId INT,  
          @ShoppingCartId INT  
  
  SELECT @UserId=UserId, @ShoppingCartId=ShoppingCartId   
  FROM dbo.UserSession WHERE SessionId=@SessionId  
  
  IF @UserId IS NULL   
  THROW 51000, N'The session or shopping cart does not exist.', 1  
  
  UPDATE dbo.UserSession SET ShoppingCartId=@ShoppingCartId WHERE SessionId=@SessionId   
 END   
 GO  
  
 EXEC usp_AssignCart 1   
 GO  
  
-- natively compiled stored procedure for inserting a large number of rows   
-- this demonstrates the performance of native procs   
 CREATE PROCEDURE dbo.usp_InsertSampleCarts @InsertCount int   
 WITH NATIVE_COMPILATION, SCHEMABINDING   
 AS   
 BEGIN ATOMIC   
 WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
  
  DECLARE @i int = 0  
  
  WHILE @i < @InsertCount   
  BEGIN   
    INSERT INTO dbo.ShoppingCart VALUES (1, SYSDATETIME() , NULL)   
    SET @i += 1   
  END  
  
END   
GO  
  
-- insert 1,000,000 rows   
 EXEC usp_InsertSampleCarts 1000000   
 GO  
  
---- verify the rows have been inserted   
 SELECT COUNT(*) FROM dbo.ShoppingCart   
 GO  
  
-- sample memory-optimized tables for sales orders and sales order details  
CREATE TABLE dbo.SalesOrders   
(  
   so_id INT NOT NULL PRIMARY KEY NONCLUSTERED,  
   cust_id INT NOT NULL,  
   so_date DATE NOT NULL INDEX ix_date NONCLUSTERED,  
   so_total MONEY NOT NULL,  
   INDEX ix_date_total NONCLUSTERED (so_date DESC, so_total DESC)  
) WITH (MEMORY_OPTIMIZED=ON)  
GO  
  
CREATE TABLE dbo.SalesOrderDetails  
(  
   so_id INT NOT NULL,  
   lineitem_id INT NOT NULL,  
   product_id INT NOT NULL,  
   unitprice MONEY NOT NULL,  
  
   CONSTRAINT PK_SOD PRIMARY KEY NONCLUSTERED (so_id,lineitem_id)  
) WITH (MEMORY_OPTIMIZED=ON)  
GO  
  
-- memory-optimized table type for collecting sales order details  
CREATE TYPE dbo.SalesOrderDetailsType AS TABLE  
(  
   so_id INT NOT NULL,  
   lineitem_id INT NOT NULL,  
   product_id INT NOT NULL,  
   unitprice MONEY NOT NULL,  
  
   PRIMARY KEY NONCLUSTERED (so_id,lineitem_id)  
) WITH (MEMORY_OPTIMIZED=ON)  
GO  
  
-- stored procedure that inserts a sales order, along with its details  
CREATE PROCEDURE dbo.InsertSalesOrder @so_id INT, @cust_id INT, @items dbo.SalesOrderDetailsType READONLY  
WITH NATIVE_COMPILATION, SCHEMABINDING  
AS BEGIN ATOMIC WITH   
(  
   TRANSACTION ISOLATION LEVEL = SNAPSHOT,  
   LANGUAGE = N'us_english'  
)  
   DECLARE @total MONEY  
   SELECT @total = SUM(unitprice) FROM @items  
   INSERT dbo.SalesOrders VALUES (@so_id, @cust_id, getdate(), @total)  
   INSERT dbo.SalesOrderDetails SELECT so_id, lineitem_id, product_id, unitprice FROM @items  
END  
GO  
  
-- insert a sample sales order  
DECLARE @so_id INT = 18,  
       @cust_id INT = 8,  
       @items dbo.SalesOrderDetailsType  
INSERT @items  VALUES   
       (@so_id, 1, 4, 43),   
       (@so_id, 2, 3, 3),   
       (@so_id, 3, 8, 453),   
       (@so_id, 4, 5, 76),   
       (@so_id, 5, 4, 43)  
EXEC dbo.InsertSalesOrder @so_id, @cust_id, @items  
GO  
  
-- verify the content of the tables  
SELECT   
       so.so_id,  
       so.so_date,  
       sod.lineitem_id,  
       sod.product_id,  
       sod.unitprice  
FROM dbo.SalesOrders so JOIN dbo.SalesOrderDetails sod on so.so_id=sod.so_id  
ORDER BY so.so_id, sod.lineitem_id  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Codebeispiele für In-Memory OLTP](../../relational-databases/in-memory-oltp/in-memory-oltp-code-samples.md)  
  
  

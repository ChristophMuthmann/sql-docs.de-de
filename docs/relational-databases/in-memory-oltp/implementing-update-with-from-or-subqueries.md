---
title: Implementieren von UPDATE mit FROM oder Unterabfragen | Microsoft-Dokumentation
ms.custom:
- SQL2016_New_Updated
ms.date: 11/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 138f5b0e-f8a4-400f-b581-8062aebc62b6
caps.latest.revision: 4
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c9f044bbde8edd542e3a2a1017a726b8d939654a
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="implementing-update-with-from-or-subqueries"></a>Implementieren von UPDATE mit FROM oder Unterabfragen
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

Nativ kompilierte T-SQL-Module bieten keine Unterstützung für die FROM-Klausel und unterstützen keine Unterabfragen in UPDATE-Anweisungen (sie werden in SELECT unterstützt). UPDATE-Anweisungen mit der FROM-Klausel werden normalerweise verwendet, um Informationen in einer Tabelle, die auf einem Tabellenwertparameter (table-valued parameter; TVP) basiert, oder Spalten in einer Tabelle in einem AFTER-Trigger zu aktualisieren. 

Ein Updateszenario, das auf einem Tabellenwertparameter basiert, finden Sie unter [Implementieren von MERGE-Funktionalität in einer nativ kompilierten gespeicherten Prozedur](../../relational-databases/in-memory-oltp/implementing-merge-functionality-in-a-natively-compiled-stored-procedure.md). 

Das nachstehende Beispiel veranschaulicht ein in einem Trigger ausgeführtes Update. Die Tabellenspalte „LastUpdated“ wird mithilfe des AFTER-Triggers auf das aktuelle Datum bzw. die aktuelle Uhrzeit aktualisiert. Das Problem kann umgangen werden, indem Sie eine Tabellenvariable mit einer Identitätsspalte und eine WHILE-Schleife einsetzen, die die Zeilen der Tabellenvariablen durchläuft und einzelne Updates ausführt.
  
Dies ist die ursprüngliche T-SQL UPDATE-Anweisung:  
  
  
  
  
    UPDATE dbo.Table1  
        SET LastUpdated = SysDateTime()  
        FROM  
            dbo.Table1 t  
            JOIN Inserted i ON t.Id = i.Id;  
  
  
  

Der T-SQL-Beispielcode in diesem Abschnitt veranschaulicht eine leistungsstarke Problemumgehung. Die Problemumgehung wird in einem nativ kompilierten Trigger implementiert. Beachten Sie unbedingt:  
  
- Den Typen namens dbo.Type1, der einen speicheroptimierten Tabellentyp darstellt.  
- Die WHILE-Schleife im Trigger.  
  - Dass die Schleife die Zeilen eine nach der anderen aus „Inserted“ abruft.  
  
  
  

    DROP TABLE IF EXISTS dbo.Table1;  
    go  
    DROP TYPE IF EXISTS dbo.Type1;  
    go  
    -----------------------------  
    <a name="---table-and-table-type"></a>-- Tabelle und Tabellentyp
    -----------------------------
  
    CREATE TABLE dbo.Table1  
    (  
        Id           INT        NOT NULL  PRIMARY KEY NONCLUSTERED,  
        Column2      INT        NOT NULL,  
        LastUpdated  DATETIME2  NOT NULL  DEFAULT (SYSDATETIME())  
    )  
        WITH (MEMORY_OPTIMIZED = ON);  
    go  
  
  
    CREATE TYPE dbo.Type1 AS TABLE  
    (  
        Id       INT NOT  NULL,  
        
        RowID    INT NOT  NULL  IDENTITY,  
        INDEX ix_RowID HASH (RowID) WITH (BUCKET_COUNT=1024)
    )   
        WITH (MEMORY_OPTIMIZED = ON);  
    go  
    ----------------------------- 
    <a name="---trigger-that-contains-the-workaround-for-update-with-from"></a>-- Der Trigger, der die Problemumgehung für UPDATE mit FROM enthält. 
    -----------------------------  
  
    CREATE TRIGGER dbo.tr_a_u_Table1  
        ON dbo.Table1  
        WITH NATIVE_COMPILATION, SCHEMABINDING  
        AFTER UPDATE  
    AS BEGIN ATOMIC WITH  
        (  
        TRANSACTION ISOLATION LEVEL = SNAPSHOT,  
        LANGUAGE = N'us_english'  
        )  
        
      DECLARE @tabvar1 dbo.Type1;  
    
      INSERT @tabvar1 (Id)   
          SELECT Id FROM Inserted;  
    
      DECLARE  
          @i INT = 1,  @Id INT,  
          @max INT = SCOPE_IDENTITY();  
    
      ---- Schleife als Problemumgehung, um einen Cursor zu simulieren.
    ---- Durchläuft die Zeile in der speicheroptimierten Tabelle.  
      ---- variabel und führt für jede Zeile ein Update aus.  
    
      WHILE @i <= @max  
      BEGIN  
          SELECT @Id = Id  
              FROM @tabvar1  
              WHERE RowID = @i;  
    
          UPDATE dbo.Table1  
              SET LastUpdated = SysDateTime()  
              WHERE Id = @Id;  
    
          SET @i += 1;  
      END  
    END  
    go  
    -----------------------------  
    <a name="---test-to-verify-functionality"></a>-- Test zur Überprüfung der Funktionalität
    -----------------------------  
  
    SET NOCOUNT ON;  
  
    INSERT dbo.Table1 (Id, Column2)  
        VALUES (1,9), (2,9), (3,600);  
    
    SELECT N'BEFORE-Update' AS [BEFORE-Update], *  
        FROM dbo.Table1  
        ORDER BY Id;  
  
    WAITFOR DELAY '00:00:01';  

    UPDATE dbo.Table1  
        SET   Column2 += 1  
        WHERE Column2 <= 99;  
  
    SELECT N'AFTER--Update' AS [AFTER--Update], *  
        FROM dbo.Table1  
        ORDER BY Id;  
    go  
    -----------------------------  
  
    /**** Tatsächliche Ausgabe:  
  
    BEFORE-Update   Id   Column2   LastUpdated  
    BEFORE-Update   1       9      2016-04-20 21:18:42.8394659  
    BEFORE-Update   2       9      2016-04-20 21:18:42.8394659  
    BEFORE-Update   3     600      2016-04-20 21:18:42.8394659  
  
    AFTER--Update   Id   Column2   LastUpdated  
    AFTER--Update   1      10      2016-04-20 21:18:43.8529692  
    AFTER--Update   2      10      2016-04-20 21:18:43.8529692  
    AFTER--Update   3     600      2016-04-20 21:18:42.8394659  
    ****/  
  
  
  


---
title: "Datenbankübergreifende Abfragen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 08/04/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a0305f5b-91bd-4d18-a2fc-ec235b062fd3
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: Human Translation
ms.sourcegitcommit: 41b00b196f6cfad66ae0e26bbb1516da2641d9b7
ms.openlocfilehash: 8289b02c3e15f1b299196c343503c9cb87387c6c
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="cross-database-queries"></a>Datenbankübergreifende Abfragen
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  Ab [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]bieten speicheroptimierte Tabellen keine Unterstützung für datenbankübergreifende Transaktionen. Innerhalb einer Transaktion oder Abfrage, die auf eine speicheroptimierte Tabelle zugreift, können Sie nicht gleichzeitig auf eine andere Datenbank zugreifen. Daten aus einer Tabelle in einer Datenbank können nicht einfach in eine speicheroptimierte Tabelle in einer anderen Datenbank kopiert werden.  
  
 Tabellenvariablen sind nicht transaktional. Daher können speicheroptimierte Tabellenvariablen in datenbankübergreifenden Abfragen verwendet werden, um Daten aus einer Datenbank in speicheroptimierte Tabellen in einer anderen Datenbank zu verschieben. Sie können zwei Transaktionen verwenden. In der ersten Transaktion fügen Sie die Daten aus der Remotetabelle in die Variable ein. In der zweiten Transaktion fügen Sie die Daten aus der Variablen in die lokale speicheroptimierte Tabelle ein.  Weitere Informationen zu speicheroptimierten Tabellenvariablen finden Sie unter [Schnellere temporäre Tabellen und Tabellenvariablen durch Speicheroptimierung](../../relational-databases/in-memory-oltp/faster-temp-table-and-table-variable-by-using-memory-optimization.md).
  
## <a name="example"></a>Beispiel
Dieses Beispiel zeigt eine Methode zum Übertragen von Daten aus einer Datenbank in eine speicheroptimierte Tabelle in einer anderen Datenbank.

1. Erstellen Sie Testobjekte.  Führen Sie das folgende [!INCLUDE[tsql](../../includes/tsql-md.md)] in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]aus.  

    ```tsql

    USE master;
    GO
    
    SET NOCOUNT ON;
    
    -- Create simple database
    CREATE DATABASE SourceDatabase;
    ALTER DATABASE SourceDatabase SET RECOVERY SIMPLE;
    GO

    -- Create a table and insert a few records
    USE SourceDatabase;
    
    CREATE TABLE SourceDatabase.[dbo].[SourceTable] (
        [ID] [int] PRIMARY KEY CLUSTERED,
        [FirstName] nvarchar(8)
        );
    
    INSERT [SourceDatabase].[dbo].[SourceTable]
    VALUES (1, N'Bob'),
        (2, N'Susan');
    GO

    -- Create a database with a MEMORY_OPTIMIZED_DATA filegroup

    CREATE DATABASE DestinationDatabase
     ON  PRIMARY 
    ( NAME = N'DestinationDatabase_Data', FILENAME = N'D:\DATA\DestinationDatabase_Data.mdf',   SIZE = 8MB), 
     FILEGROUP [DestinationDatabase_mod] CONTAINS MEMORY_OPTIMIZED_DATA  DEFAULT
    ( NAME = N'DestinationDatabase_mod', FILENAME = N'D:\DATA\DestinationDatabase_mod', MAXSIZE = UNLIMITED)
     LOG ON 
    ( NAME = N'DestinationDatabase_Log', FILENAME = N'D:\LOG\DestinationDatabase_Log.ldf', SIZE = 8MB);
    
    ALTER DATABASE DestinationDatabase SET RECOVERY SIMPLE;
    GO
    
    USE DestinationDatabase;
    GO

    -- Create a memory-optimized table
    CREATE TABLE [dbo].[DestTable_InMem] (
        [ID] [int] PRIMARY KEY NONCLUSTERED,
        [FirstName] nvarchar(8)
        )
    WITH ( MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA );
    GO
    ```

2.  Versuchen Sie eine datenbankübergreifende Abfrage. Führen Sie das folgende [!INCLUDE[tsql](../../includes/tsql-md.md)] in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]aus.
  
    ```tsql  
    INSERT [DestinationDatabase].[dbo].[DestTable_InMem]
    SELECT * FROM [SourceDatabase].[dbo].[SourceTable]
    ```  

    Es sollte die folgende Fehlermeldung angezeigt werden:
    > Meldung 41317, Ebene 16, Status 5  
    > Eine Benutzertransaktion, über die auf speicheroptimierte Tabellen oder systemintern kompilierte Module zugegriffen wird, kann maximal auf eine Benutzerdatenbank, ein Datenbankmodell und eine msdb-Datenbank zugreifen. Schreibzugriffe auf die Masterdatenbank werden nicht unterstützt.

3.  Erstellen Sie einen speicheroptimierten Tabellentyp.  Führen Sie das folgende [!INCLUDE[tsql](../../includes/tsql-md.md)] in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]aus.

    ```tsql
    USE DestinationDatabase;
    GO
    
    CREATE TYPE [dbo].[MemoryType]  
        AS TABLE  
        (  
        [ID] [int] PRIMARY KEY NONCLUSTERED,
        [FirstName] nvarchar(8)
        )  
        WITH  
            (MEMORY_OPTIMIZED = ON);  
    GO
    ```

4.  Versuchen Sie erneut die datenbankübergreifende Abfrage.  Dieses Mal werden die Daten zunächst in eine speicheroptimierte Tabellenvariable übertragen.  Dann werden die Daten aus der Tabellenvariablen in die speicheroptimierte Tabelle übertragen.
    ```tsql
    -- Declare table variable utilizing the newly created type - MemoryType
    DECLARE @InMem dbo.MemoryType;
    
    -- Populate table variable
    INSERT @InMem SELECT * FROM SourceDatabase.[dbo].[SourceTable];
    
    -- Populate the destination memory-optimized table
    INSERT [DestinationDatabase].[dbo].[DestTable_InMem] SELECT * FROM @InMem;
    GO 
    ```
   
## <a name="see-also"></a>Siehe auch  
 [Migrieren zu In-Memory OLTP](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)  
  
  


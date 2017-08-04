---
title: Erste Schritte mit der Leistungsfunktionen von SQL Server on Linux | Microsoft Docs
description: "Dieses Thema enthält eine Einführung in SQL Server-Leistung-Funktionen für Linux-Benutzer, die noch nicht mit SQL Server sind. Viele dieser Beispiele auf allen Plattformen funktioniert, aber im Rahmen dieses Artikels ist Linux."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 60036d26-4797-4872-9a9e-3552841c61be
ms.custom: H1Hack27Feb2017
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 4f4f58b682451b7dabf336241ec94797a4d1469e
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="walkthrough-for-the-performance-features-of-sql-server-on-linux"></a>Exemplarische Vorgehensweise für die Leistungsfunktionen von SQL Server on Linux
Wenn Sie einen Linux-Benutzer, der noch nicht mit SQL Server ist sind, führen die folgenden Aufgaben über einige der Leistungsfeatures. Diese sind nicht eindeutig oder gelten speziell für Linux, aber sie hilft bei der bieten einen Überblick über Bereiche genauere Untersuchung durchführen. In jedem Beispiel wird ein Link in der Dokumentation Tiefe für diesen Bereich bereitgestellt.

> [!NOTE]
> Die folgenden Beispiele verwenden die AdventureWorks-Beispieldatenbank. Informationen zum Herunterladen und Installieren dieser Beispieldatenbank finden Sie unter [wiederherstellen eine SQL Server-Datenbank von Windows, Linux](sql-server-linux-migrate-restore-database.md).

## <a name="create-a-columnstore-index"></a>Erstellen Sie einen columnstore-Index
Ein columnstore-Index ist eine Technologie zum Speichern und Abfragen großer speichert Daten in eines spaltenbasierten Datenformats, das als Columnstore bezeichnet wird.  

1. Fügen Sie einen columnstore-Index der SalesOrderDetail-Tabelle hinzu, durch das Ausführen des folgenden T-SQL:

   ```sql
   CREATE NONCLUSTERED COLUMNSTORE INDEX [IX_SalesOrderDetail_ColumnStore]
      ON Sales.SalesOrderDetail
      (UnitPrice, OrderQty, ProductID)
   GO
   ```

2. Führen Sie die folgende Abfrage, die den columnstore-Index zum Scannen der Tabelle verwenden:

   ```sql
   SELECT ProductID, SUM(UnitPrice) SumUnitPrice, AVG(UnitPrice) AvgUnitPrice,
      SUM(OrderQty) SumOrderQty, AVG(OrderQty) AvgOrderQty
   FROM Sales.SalesOrderDetail
      GROUP BY ProductID
      ORDER BY ProductID
   ```

3. Stellen Sie sicher, dass der columnstore-Index verwendet wurde, indem die Objekt-ID für den columnstore-Index nachschlagen und bestätigt, dass er in die Verwendungsstatistiken für der SalesOrderDetail-Tabelle angezeigt wird:

   ```sql
   SELECT * FROM sys.indexes WHERE name = 'IX_SalesOrderDetail_ColumnStore'
   GO

   SELECT * 
   FROM sys.dm_db_index_usage_stats
      WHERE database_id = DB_ID('AdventureWorks')
      AND object_id = OBJECT_ID('AdventureWorks.Sales.SalesOrderDetail');
   ```
   
## <a name="use-in-memory-oltp"></a>Verwenden von In-Memory OLTP
SQL Server bietet In-Memory-OLTP-Funktionen, die die Leistung von Anwendungssystemen erheblich verbessert werden können.  In diesem Abschnitt des Handbuchs Auswertung begleiten Sie durch die Schritte zum Erstellen einer speicheroptimierten Tabellenstatus gespeichert, die im Arbeitsspeicher und einer systemintern kompilierten gespeicherten Prozedur, die auf die Tabelle ohne kompiliert oder interpretiert werden.

### <a name="configure-database-for-in-memory-oltp"></a>Konfigurieren Sie für In-Memory-OLTP-Datenbank
1. Es wird empfohlen, die Datenbank einen Kompatibilitätsgrad von mindestens 130 mit In-Memory OLTP festlegen.  Verwenden Sie die folgende Abfrage, um den aktuellen Kompatibilitätsgrad von AdventureWorks zu überprüfen:  

   ```sql
   USE AdventureWorks
   GO
   SELECT d.compatibility_level
   FROM sys.databases as d
     WHERE d.name = Db_Name();
   GO
   ```
   
   Aktualisieren Sie bei Bedarf die Ebene in "130":

   ```sql
   ALTER DATABASE CURRENT
   SET COMPATIBILITY_LEVEL = 130;
   GO
   ```

2. Wenn eine Transaktion eine datenträgerbasierte Tabelle und eine Speicheroptimierte Tabelle einschließt, Namens der grundlegende, die der Speicheroptimierte Teil der Transaktion ausgeführt werden, auf die Transaktionsisolationsstufe SNAPSHOT.  Um diese Stufe für Speicheroptimierte Tabellen in einer containerübergreifenden Transaktion zuverlässig zu erzwingen, führen Sie die folgenden Schritte aus:

   ```sql
   ALTER DATABASE CURRENT SET MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT=ON
   GO
   ```

3. Vor der Erstellung eine speicheroptimierten Tabelle müssen Sie zunächst erstellen Sie eine Speicheroptimierte DATEIGRUPPE und einen Container für Datendateien:

   ```sql
   ALTER DATABASE AdventureWorks ADD FILEGROUP AdventureWorks_mod CONTAINS memory_optimized_data
   GO  
   ALTER DATABASE AdventureWorks ADD FILE (NAME='AdventureWorks_mod', FILENAME='/var/opt/mssql/data/AdventureWorks_mod') TO FILEGROUP AdventureWorks_mod
   GO
   ```

### <a name="create-a-memory-optimized-table"></a>Erstellen Sie eine Speicheroptimierte Tabelle
Der primäre Speicher für Speicheroptimierte Tabellen Hauptspeicher und im Gegensatz zu datenträgerbasierten Tabellen ist daher, muss Daten nicht in vom Datenträger in den Arbeitsspeicher gelesen werden.  Verwenden Sie zum Erstellen einer speicheroptimierten Tabellenstatus die MEMORY_OPTIMIZED = ON-Klausel.

1. Führen Sie die folgende Abfrage aus, um das "Dbo" eine Speicheroptimierte Tabelle zu erstellen. ShoppingCart.  Standardmäßig werden die Daten auf Datenträgern aufbewahrt werden für Dauerhaftigkeit Zwecke (Beachten Sie, die DAUERHAFTIGKEIT auch festgelegt werden kann, um das Schema nur persistent zu speichern). 

   ```sql
   CREATE TABLE dbo.ShoppingCart ( 
   ShoppingCartId INT IDENTITY(1,1) PRIMARY KEY NONCLUSTERED,
   UserId INT NOT NULL INDEX ix_UserId NONCLUSTERED HASH WITH (BUCKET_COUNT=1000000), 
   CreatedDate DATETIME2 NOT NULL, 
   TotalPrice MONEY
   ) WITH (MEMORY_OPTIMIZED=ON) 
   GO
   ```

2. Fügen Sie einige Datensätze in die Tabelle ein:

   ```sql
   INSERT dbo.ShoppingCart VALUES (8798, SYSDATETIME(), NULL) 
   INSERT dbo.ShoppingCart VALUES (23, SYSDATETIME(), 45.4) 
   INSERT dbo.ShoppingCart VALUES (80, SYSDATETIME(), NULL) 
   INSERT dbo.ShoppingCart VALUES (342, SYSDATETIME(), 65.4) 
   ```

### <a name="natively-compiled-stored-procedure"></a>Systemintern kompilierte gespeicherte Prozedur
SQL Server unterstützt systemintern kompilierte gespeicherte Prozeduren, die auf Speicheroptimierte Tabellen zugreifen. Die T-SQL-Anweisungen sind in Computercode kompiliert und als systemeigene DLL-Dateien, Aktivieren der schnelleren Datenzugriff und eine effizientere abfrageausführung als herkömmliche T-SQL gespeichert.   Gespeicherte Prozeduren, die mit NATIVE_COMPILATION markiert sind, werden systemintern kompiliert. 

1. Führen Sie das folgende Skript aus, um eine systemintern kompilierte gespeicherte Prozedur zu erstellen, die eine große Anzahl von Datensätzen in der Tabelle ShoppingCart einfügt:


   ```sql
   CREATE PROCEDURE dbo.usp_InsertSampleCarts @InsertCount int 
    WITH NATIVE_COMPILATION, SCHEMABINDING AS 
   BEGIN ATOMIC 
   WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')

   DECLARE @i int = 0

   WHILE @i < @InsertCount 
    BEGIN 
     INSERT INTO dbo.ShoppingCart VALUES (1, SYSDATETIME() , NULL) 
     SET @i += 1 
    END
   END 
   ```
2. 1.000.000 Zeilen einfügen:

   ```sql
   EXEC usp_InsertSampleCarts 1000000 
   ```

3. Stellen Sie sicher, dass die Zeilen eingefügt wurden:

   ```sql
   SELECT COUNT(*) FROM dbo.ShoppingCart 
   ```

### <a name="learn-more-about-in-memory-oltp"></a>Weitere Informationen zu In-Memory OLTP
Weitere Informationen zu In-Memory OLTP finden Sie unter den folgenden Themen:

- [Schnellstart 1: In-Memory-OLTP-Technologien für höhere Transact-SQL-Leistung](https://msdn.microsoft.com/library/mt694156.aspx)
- [Migrieren zu In-Memory OLTP](https://msdn.microsoft.com/library/dn247639.aspx)
- [Schnellere temporäre Tabellen und Tabellenvariablen durch Speicheroptimierung](https://msdn.microsoft.com/library/mt718711.aspx)
- [Überwachung und Fehlerbehebung für die Arbeitsspeicherauslastung](https://msdn.microsoft.com/library/dn465869.aspx)
- [In-Memory OLTP (Arbeitsspeicheroptimierung)](https://msdn.microsoft.com/library/dn133186.aspx)

## <a name="use-query-store"></a>Verwenden Sie den Abfragespeicher
Der Abfragespeicher sammelt detaillierte Leistungsinformationen über Abfragen, Ausführungspläne und Statistiken.

Der Abfragespeicher ist nicht standardmäßig aktiviert und kann mit ALTER DATABASE aktiviert werden:

   ```sql
   ALTER DATABASE AdventureWorks SET QUERY_STORE = ON;
   ```

Führen Sie die folgende Abfrage aus, um Informationen über Abfragen und Pläne im Abfragespeicher zurückzugeben: 

   ```sql
   SELECT Txt.query_text_id, Txt.query_sql_text, Pl.plan_id, Qry.*
   FROM sys.query_store_plan AS Pl
      JOIN sys.query_store_query AS Qry
         ON Pl.query_id = Qry.query_id
      JOIN sys.query_store_query_text AS Txt
         ON Qry.query_text_id = Txt.query_text_id ;
   ```

## <a name="query-dynamic-management-views"></a>Dynamische Verwaltungssichten Abfrage
Dynamische Verwaltungssichten zurück Informationen zum Serverstatus, die verwendet werden kann, wird der Zustand einer Serverinstanz überwacht, Probleme zu diagnostizieren und Optimieren der Leistung.

Die verwaltungssicht Dm_os_wait Stats dynamische Abfragen:

   ```sql
   SELECT wait_type, wait_time_ms
   FROM sys.dm_os_wait_stats;
   ```

---
title: 'Demo: Leistungsverbesserungen von In-Memory OLTP | Microsoft-Dokumentation'
ms.custom: 
ms.date: 08/19/2016
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
ms.assetid: c6def45d-d2d4-4d24-8068-fab4cd94d8cc
caps.latest.revision: 
author: JennieHubbard
ms.author: jhubbard
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c482c0a7e79f2732e98594eccdd1da57e3d5d37d
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2018
---
# <a name="demonstration-performance-improvement-of-in-memory-oltp"></a>Demo: Leistungsverbesserungen von In-Memory OLTP
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Das Codebeispiel in diesem Thema veranschaulicht die hohe Leistung von speicheroptimierten Tabellen. Die Leistungsverbesserung wird ersichtlich, wenn über herkömmliches, interpretiertes [!INCLUDE[tsql](../../includes/tsql-md.md)]auf Daten in einer speicheroptimierten Tabelle zugegriffen wird. Diese Leistungsverbesserung wird noch größer, wenn von einer nativ kompilierten gespeicherten Prozedur (NCSProc) aus auf Daten in einer speicheroptimierten Tabelle zugegriffen werden.  
 
Eine umfassendere Darstellung der potenziellen Leistungssteigerungen von In-Memory OLTP finden Sie unter [In-Memory OLTP Performance Demo v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0). 
  
 Das Codebeispiel in diesem Artikel verwendet nur einen einzelnen Thread und nutzt nicht die Parallelitätsvorteile von In-Memory-OLTP. Eine Arbeitsauslastung, die Parallelität verwendet, bietet noch größere Leistungsvorteile. Das Codebeispiel zeigt nur einen Aspekt der Leistungssteigerung, und zwar die Datenzugriffseffizienz für INSERT.  
  
 Die durch speicheroptimierte Tabellen erzielte Leistungsverbesserung wird voll genutzt, wenn auf die Daten in einer speicheroptimierten Tabelle mithilfe einer NCSProc zugegriffen wird.  
  
## <a name="code-example"></a>Codebeispiel  
 Diese jeweiligen Schritte werden in den nächsten Unterabschnitten beschrieben.  
  
### <a name="step-1a-prerequisite-if-using-includessnoversionincludesssnoversion-mdmd"></a>Schritt 1a: Voraussetzung bei Verwendung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Die Schritte in diesem ersten Unterabschnitt gelten nur, wenn Sie mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]arbeiten, nicht mit [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]. Gehen Sie folgendermaßen vor:  
  
1.  Verwenden Sie SQL Server Management Studio (SSMS.exe), um eine Verbindung mit Ihrem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]herzustellen. Alternativ können Sie jedes Tool nehmen, das wie „SSMS.exe“ funktioniert.  
  
2.  Erstellen Sie manuell ein Verzeichnis namens **C:\data\\**. In dem Transact-SQL-Beispielcode wird davon ausgegangen, dass das Verzeichnis bereits vorhanden ist.  
  
3.  Führen Sie das kurze T-SQL aus, um die Datenbank und die speicheroptimierte Dateigruppe zu erstellen.  
  
```sql  
go  
CREATE DATABASE imoltp;    --  Transact-SQL  
go  
  
ALTER DATABASE imoltp ADD FILEGROUP [imoltp_mod]  
    CONTAINS MEMORY_OPTIMIZED_DATA;  
  
ALTER DATABASE imoltp ADD FILE  
    (name = [imoltp_dir], filename= 'c:\data\imoltp_dir')  
    TO FILEGROUP imoltp_mod;  
go  
  
USE imoltp;  
go  
```  
  
### <a name="step-1b-prerequisite-if-using-includesssdsfullincludessssdsfull-mdmd"></a>Schritt 1b: Voraussetzung bei Verwendung von [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]  
 Dieser Unterabschnitt gilt nur, wenn Sie [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]verwenden. Gehen Sie folgendermaßen vor:  
  
1.  Entscheiden Sie, welche vorhandene Testdatenbank Sie für das Codebeispiel verwenden möchten.  
  
2.  Wenn Sie eine neue Testdatenbank erstellen möchten, verwenden Sie das [Azure-Portal](http://portal.azure.com) , und erstellen Sie eine Datenbank namens **imoltp**.  
  
 Wenn Sie Anleitungen zur Erstellung einer Testdatenbank mit dem Azure-Portal suchen, lesen Sie [Erste Schritte mit Azure SQL-Datenbank](http://azure.microsoft.com/documentation/articles/sql-database-get-started).  
  
### <a name="step-2-create-memory-optimized-tables-and-ncsproc"></a>Schritt 2: Erstellen von speicheroptimierten Tabellen und NCSProc  
 In diesem Schritt wird die Erstellung einer speicheroptimierten Tabelle und einer nativ kompilierten gespeicherten Prozedur (NCSProc) erläutert. Gehen Sie folgendermaßen vor:  
  
1.  Verwenden Sie „SSMS.exe“, um sich mit der neuen Datenbank zu verbinden.  
  
2.  Führen Sie die folgende T-SQL-Anweisung in der Datenbank aus.  
  
```sql  
go  
DROP PROCEDURE IF EXISTS ncsp;  
DROP TABLE IF EXISTS sql;  
DROP TABLE IF EXISTS hash_i;  
DROP TABLE IF EXISTS hash_c;  
go  
  
CREATE TABLE [dbo].[sql] (  
  c1 INT NOT NULL PRIMARY KEY,  
  c2 NCHAR(48) NOT NULL  
);  
go  
  
CREATE TABLE [dbo].[hash_i] (  
  c1 INT NOT NULL PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT=1000000),  
  c2 NCHAR(48) NOT NULL  
) WITH (MEMORY_OPTIMIZED=ON, DURABILITY = SCHEMA_AND_DATA);  
go  
  
CREATE TABLE [dbo].[hash_c] (  
  c1 INT NOT NULL PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT=1000000),  
  c2 NCHAR(48) NOT NULL  
) WITH (MEMORY_OPTIMIZED=ON, DURABILITY = SCHEMA_AND_DATA);  
go  
  
CREATE PROCEDURE ncsp  
    @rowcount INT,  
    @c NCHAR(48)  
  WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
  AS   
  BEGIN ATOMIC   
  WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
  DECLARE @i INT = 1;  
  WHILE @i <= @rowcount  
  BEGIN;  
    INSERT INTO [dbo].[hash_c] VALUES (@i, @c);  
    SET @i += 1;  
  END;  
END;  
go  
```  
  
### <a name="step-3-run-the-code"></a>Schritt 3: Ausführen des Codes  
 Sie können nun die Abfragen ausführen, die die Leistung von speicheroptimierten Tabellen veranschaulichen. Gehen Sie folgendermaßen vor:  
  
1.  Verwenden Sie „SSMS.exe“, um die folgende T-SQL-Anweisung in der Datenbank auszuführen,  
  
     Ignorieren Sie die Geschwindigkeits- oder andere Leistungsdaten, die bei dieser ersten Ausführung generiert werden. Die erste Ausführung stellt sicher, dass mehrere einmalige Vorgänge ausgeführt werden, z.B. die anfängliche Zuordnung von Arbeitsspeicher.  
  
2.  Verwenden Sie „SSMS.exe“ erneut, um die folgende T-SQL-Anweisung erneut in der Datenbank auszuführen,  
  
```sql  
go  
SET STATISTICS TIME OFF;  
SET NOCOUNT ON;  
  
-- Inserts, one at a time.  
  
DECLARE @starttime DATETIME2 = sysdatetime();  
DECLARE @timems INT;  
DECLARE @i INT = 1;  
DECLARE @rowcount INT = 100000;  
DECLARE @c NCHAR(48) = N'12345678901234567890123456789012345678';  
  
-- Harddrive-based table and interpreted Transact-SQL.  
  
BEGIN TRAN;  
  WHILE @i <= @rowcount  
  BEGIN;  
    INSERT INTO [dbo].[sql] VALUES (@i, @c);  
    SET @i += 1;  
  END;  
COMMIT;  
  
SET @timems = datediff(ms, @starttime, sysdatetime());  
SELECT 'A: Disk-based table and interpreted Transact-SQL: '  
    + cast(@timems AS VARCHAR(10)) + ' ms';  
  
-- Interop Hash.  
  
SET @i = 1;  
SET @starttime = sysdatetime();  
  
BEGIN TRAN;  
  WHILE @i <= @rowcount  
    BEGIN;  
      INSERT INTO [dbo].[hash_i] VALUES (@i, @c);  
      SET @i += 1;  
    END;  
COMMIT;  
  
SET @timems = datediff(ms, @starttime, sysdatetime());  
SELECT 'B: memory-optimized table with hash index and interpreted Transact-SQL: '  
    + cast(@timems as VARCHAR(10)) + ' ms';  
  
-- Compiled Hash.  
  
SET @starttime = sysdatetime();  
  
EXECUTE ncsp @rowcount, @c;  
  
SET @timems = datediff(ms, @starttime, sysdatetime());  
SELECT 'C: memory-optimized table with hash index and native SP:'  
    + cast(@timems as varchar(10)) + ' ms';  
go  
  
DELETE sql;  
DELETE hash_i;  
DELETE hash_c;  
go  
```  
  
 Als Nächstes kommen die Ausgabezeitstatistiken, die bei unserer zweiten Testausführung generiert werden.  
  
```sql  
10453 ms , A: Disk-based table and interpreted Transact-SQL.  
5626 ms , B: memory-optimized table with hash index and interpreted Transact-SQL.  
3937 ms , C: memory-optimized table with hash index and native SP.  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [In-Memory-OLTP &#40;Arbeitsspeicheroptimierung&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  

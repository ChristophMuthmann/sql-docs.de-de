---
title: Columnstore-Index-Defragmentierung | Microsoft Dokumentation
ms.custom: 
ms.date: 01/27/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: indexes
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d3efda1a-7bdb-47f5-80bf-f075329edee5
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 283b8e0fe5173c6527e6f3708b578eca87c80ff3
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2018
---
# <a name="columnstore-indexes---defragmentation"></a>Columnstore-Index-Defragmentierung
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Aufgaben für die Defragmentierung von Columnstore-Indizes.  
  
## <a name="use-alter-index-reorganize-to-defragment-a-columnstore-index-online"></a>Verwenden von ALTER INDEX REORGANIZE, um einen Columnstore-Index online zu defragmentieren  
 **Gilt für:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (ab [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]), [!INCLUDE[ssSDS](../../includes/sssds-md.md)]  
  
Nach dem Ausführen verschiedener Auslastungstypen weist Ihr Deltastore möglicherweise mehrere kleine Zeilengruppen auf. Sie können `ALTER INDEX REORGANIZE` verwenden, um alle Zeilengruppen in den Columnstore zu zwingen und anschließend zu kombinieren, sodass weniger Zeilengruppen mit mehr Zeilen entstehen.  Der Neuorganisationsvorgang entfernt auch Zeilen, die aus dem Columnstore gelöscht wurden.  
  
Weitere Informationen finden Sie in folgenden Blogbeiträgen des Teamblogs für SQL Server-Datenbank-Engine.  
-   [Minimieren der Indexfragmentierung in Columnstore-Indizes](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/07/columnstore-index-defragmentation-using-reorganize-command/)  
-   [Columnstore-Indizes und Zusammenführungsrichtlinien für Zeilengruppen](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/08/columnstore-index-merge-policy-for-reorganize/)  
  
### <a name="recommendations-for-reorganizing"></a>Empfehlungen zum Neuorganisieren  
Organisieren Sie einen Columnstore-Index nach einem oder mehreren Datenladevorgängen neu, um so schnell wie möglich die bessere Abfrageleistung nutzbar zu machen. Beim Neuorganisieren sind zunächst zusätzliche CPU-Ressourcen zum Komprimieren der Daten erforderlich. Dies kann die Gesamtleistung des Systems beeinträchtigen. Sobald die Daten jedoch komprimiert sind, kann sich die Abfrageleistung verbessern.  
  
Verwenden Sie das Beispiel in [sys.dm_db_column_store_row_group_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-column-store-row-group-physical-stats-transact-sql.md), um die Fragmentierung zu berechnen. Dadurch können Sie bestimmen, ob ein REORGANIZE-Vorgang sinnvoll ist.  
  
### <a name="example-how-reorganizing-works"></a>Beispiel: So funktioniert eine Neuorganisierung  
 In diesem Beispiel wird zeigt, wie ALTER INDEX REORGANIZE alle Deltastore-Zeilengruppen in den Columnstore zwingen und sie kombinieren kann.  
  
1.  Führen Sie diese Transact-SQL-Anweisung aus, um eine Stagingtabelle mit 300.000 Zeilen zu erstellen. Wir verwenden dies, um Zeilen massenhaft in einen Columnstore-Index zu laden.  
  
    ```sql  
    USE master;  
    GO  
  
    IF EXISTS (SELECT name FROM sys.databases  
        WHERE name = N'[columnstore]')  
        DROP DATABASE [columnstore];  
    GO  
  
    CREATE DATABASE [columnstore];  
    GO  
  
    IF EXISTS (SELECT name FROM sys.tables  
        WHERE name = N'staging'  
        AND object_id = OBJECT_ID (N'staging'))  
    DROP TABLE dbo.staging;  
    GO  
  
    CREATE TABLE [staging] (  
         AccountKey int NOT NULL,  
         AccountDescription nvarchar (50),  
         AccountType nvarchar(50),  
         AccountCodeAlternateKey int  
    );  
    GO  
  
    -- Load data  
    DECLARE @loop int;  
    DECLARE @AccountDescription varchar(50);  
    DECLARE @AccountKey int;  
    DECLARE @AccountType varchar(50);  
    DECLARE @AccountCode int;  
  
    SELECT @loop = 0;  
    BEGIN TRAN  
        WHILE (@loop < 300000)   
          BEGIN  
            SELECT @AccountKey = CAST (RAND()*10000000 AS int);  
            SELECT @AccountDescription = 'accountdesc ' + CONVERT(varchar(20), @AccountKey);  
            SELECT @AccountType = 'AccountType ' + CONVERT(varchar(20), @AccountKey);  
            SELECT @AccountCode =  CAST (RAND()*10000000 AS int);  
  
            INSERT INTO staging VALUES (  
               @AccountKey,   
               @AccountDescription,   
               @AccountType,   
               @AccountCode  
            );  
  
            SELECT @loop = @loop + 1;  
          END  
    COMMIT  
    ```  
  
2.  Erstellen Sie eine als Columnstore-Index gespeicherte Tabelle.  
  
    ```sql  
    IF EXISTS (SELECT name FROM sys.tables  
        WHERE name = N'cci_target'  
        AND object_id = OBJECT_ID (N'cci_target'))  
    DROP TABLE dbo.cci_target;  
    GO  
  
    -- Create a table with a clustered columnstore index  
    -- and the same columns as the rowstore staging table.  
    CREATE TABLE cci_target (  
         AccountKey int NOT NULL,  
         AccountDescription nvarchar (50),  
         AccountType nvarchar(50),  
         AccountCodeAlternateKey int,  
         INDEX idx_cci_target CLUSTERED COLUMNSTORE  
    )  
    GO  
    ```  
  
3.  Fügen Sie die Zeilen der Stagingtabelle massenhaft in die Columnstore-Tabelle ein. `INSERT INTO ... SELECT` führt eine Masseneinfügung aus. `TABLOCK` ermöglicht, dass `INSERT` mit Parallelität ausgeführt wird.  
  
    ```sql  
    -- Insert rows in parallel  
    INSERT INTO cci_target WITH (TABLOCK)  
    SELECT TOP (300000) * FROM staging;  
    GO  
    ```  
  
4.  Zeigen Sie die Zeilengruppen mithilfe der dynamischen Verwaltungssicht (Dynamic Management View; DMV) *sys.dm_db_column_store_row_group_physical_stats* an.  
  
    ```sql  
    -- Run this dynamic management view (DMV) to see the OPEN rowgroups.   
    -- The number of rowgroups depends on the degree of parallelism.   
    -- You will see multiple OPEN rowgroups depending on the degree of parallelism.   
    -- This is because insert operation can run in parallel in [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].  
  
    SELECT *   
    FROM sys.dm_db_column_store_row_group_physical_stats   
    WHERE object_id  = object_id('cci_target')  
    ORDER BY row_group_id;  
    ```  
  
     In diesem Beispiel weisen die Ergebnisse acht OPEN-Zeilengruppen auf, von denen jede 37.500 Zeilen besitzt. Die Anzahl der OPEN-Zeilengruppen hängt von der Einstellung *max_degree_of_parallelism* ab.  
  
     ![OPEN Zeilengruppen](../../relational-databases/indexes/media/cci-openrowgroups.png "OPEN rowgroups")  
  
5.  Verwenden Sie `ALTER INDEX REORGANIZE` mit der `COMPRESS_ALL_ROW_GROUPS`-Option, um eine Komprimierung aller Zeilengruppen in den Columnstore zu erzwingen.  
  
    ```sql  
    -- This command will force all CLOSED and OPEN rowgroups into the columnstore.  
    ALTER INDEX idx_cci_target ON cci_target   
    REORGANIZE WITH (COMPRESS_ALL_ROW_GROUPS = ON);  
  
    SELECT *   
    FROM sys.dm_db_column_store_row_group_physical_stats   
    WHERE object_id  = object_id('cci_target')  
    ORDER BY row_group_id;  
    ```  
  
     Die Ergebnisse weisen acht COMPRESSED-Zeilengruppen und acht TOMBSTONE-Zeilengruppen auf. Jede Zeilengruppe wurde unabhängig von ihrer Größe in den Columnstore komprimiert. Die TOMBSTONE-Zeilengruppen werden vom System entfernt.  
  
     ![TOMBSTONE- und COMPRESSED- Zeilengruppen](../../relational-databases/indexes/media/cci-tombstone-compressed-rowgroups.png "TOMBSTONE- und COMPRESSED- Zeilengruppen")  
  
6.  Die Abfrageleistung verbessert sich maßgeblich, wenn Sie kleine Zeilengruppen kombinieren. `ALTER INDEX REORGANIZE` fasst `COMPRESSED`-Zeilengruppen zusammen. Da die Delta-Zeilengruppen nun in den Columnstore komprimiert wurden, führen Sie ALTER INDEX REORGANIZE erneut aus, um die kleinen COMPRESSED-Zeilengruppen zu kombinieren. In diesem Fall benötigen Sie die `COMPRESS_ALL_ROW_GROUPS`-Option nicht.  
  
    ```sql  
    -- Run this again and you will see that smaller rowgroups   
    -- combined into one compressed rowgroup with 300,000 rows  
    ALTER INDEX idx_cci_target ON cci_target REORGANIZE;  
  
    SELECT *   
    FROM sys.dm_db_column_store_row_group_physical_stats   
    WHERE object_id  = object_id('cci_target')  
    ORDER BY row_group_id;  
    ```  
  
     Die Ergebnisse weisen die acht COMPRESSED-Zeilengruppen auf, die nun in einer COMPRESSED-Zeilengruppe kombiniert sind.  
  
     ![Kombinierte Zeilengruppen](../../relational-databases/indexes/media/cci-compressed-rowgroups.png "Combined rowgroups")  
  
## <a name="rebuild"></a> Verwenden von ALTER INDEX REBUILD, um den Columnstore-Index offline zu defragmentieren  
 Für [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] oder höher ist die Neuerstellung des Columnstore-Indexes in der Regel nicht notwendig, da `REORGANIZE` die Grundlagen der Neuerstellung im Hintergrund als Onlinevorgang ausführt.  
  
 Das Neuerstellen eines Columnstore-Indexes entfernt die Fragmentierung und verschiebt alle Zeilen in den Columnstore. Verwenden Sie [CREATE COLUMNSTORE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md) oder [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md), um einen vorhandenen gruppierten Columnstore-Index komplett neu zu erstellen. Darüber hinaus können Sie die ALTER INDEX... REBUILD zum Neu erstellen einer bestimmten Partition.  
  
### <a name="rebuild-process"></a>Neuerstellungsprozess  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]führt Folgendes durch, um einen Columnstore-Index neu zu erstellen:  
  
1.  Abrufen einer exklusiven Sperre für die Tabelle oder Partition, während die Neuerstellung ausgeführt wird. Die Daten sind während der Neuerstellung offline und nicht verfügbar, auch wenn Sie `NOLOCK`, RCSI oder SI verwenden.  
  
2.  Neukomprimierung aller Daten im Columnstore. Während die Neuerstellung ausgeführt wird, gibt es zwei Kopien des columnstore-Indexes. Nach Abschluss der Neuerstellung wird der ursprüngliche columnstore-Index in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gelöscht.  
  
### <a name="recommendations-for-rebuilding-a-columnstore-index"></a>Empfehlungen zum Neuerstellen eines Columnstore-Indexes  
 Das Neuerstellen eines Columnstore-Indexes ist sinnvoll, um Fragmentierungen zu beseitigen, und um alle Zeilen in den Columnstore zu verschieben. Berücksichtigen Sie die folgenden Empfehlungen:  
  
1.  Erstellen Sie nur eine Partition neu und nicht die gesamte Tabelle.  
    -   Wenn der Index groß ist, nimmt das Neuerstellen der gesamten Tabelle viel Zeit in Anspruch, und es muss ausreichend Speicherplatz verfügbar sein, um während der Neuerstellung eine zusätzliche Kopie des Indexes speichern zu können. In der Regel muss nur die zuletzt verwendete Partition neu erstellt werden.  
    -   Bei partitionierten Tabellen müssen Sie nicht den gesamten Columnstore-Index neu erstellen, da die Fragmentierung wahrscheinlich nur in den Partitionen vorliegt, die kürzlich geändert wurden. Faktentabellen und große Dimensionstabellen werden i. d. R. partitioniert, um Sicherungs- und Verwaltungsvorgänge für Segmente der Tabelle auszuführen.  

2.  Erstellen Sie eine Partition nach intensiven DML-Vorgängen neu.  
    -   Durch das Neuerstellen einer Partition wird die Partition defragmentiert und der benötigte Festplattenspeicherplatz reduziert. Beim Neuerstellen werden alle zum Löschen markierten Zeilen aus dem Columnstore gelöscht und alle Zeilengruppen aus dem Deltastore in den Columnstore verschoben. Beachten Sie, dass mehrere Zeilengruppen im Deltastore vorhanden sein können, von denen jede weniger als eine Million Zeilen enthält.  
  
3.  Erstellen Sie eine Partition neu, nachdem Sie Daten geladen haben.  
    -   Dadurch wird sichergestellt, dass alle Daten im Columnstore gespeichert sind. Wenn gleichzeitige Prozesse zur gleichen Zeit jeweils weniger als 100.000 Zeilen in dieselbe Partition laden, kann die Partition im Endeffekt mehrere Deltastores aufweisen. Durch das Neuerstellen werden alle Deltastore-Zeilen in den Columnstore verschoben.  

## <a name="automatic-index-and-statistics-management"></a>Automatische Verwaltung von Index und Statistiken

Nutzen Sie Lösungen wie [Adaptive Index Defrag](http://github.com/Microsoft/tigertoolbox/tree/master/AdaptiveIndexDefrag), um die Indexdefragmentierung und das Aktualisieren der Statistiken für eine oder mehrere Datenbanken automatisch zu verwalten. Dieser Vorgang entscheidet unter anderem anhand des Fragmentierungsgrads automatisch, ob ein Index neu organisiert oder neu erstellt wird und aktualisiert Statistiken mit einem linearen Schwellenwert.

## <a name="see-also"></a>Weitere Informationen finden Sie unter        
[Columnstore indexes - what's new (Columnstore-Indizes: Neuigkeiten)](../../relational-databases/indexes/columnstore-indexes-what-s-new.md)    
[Abfrageleistung für Columnstore-Indizes](../../relational-databases/indexes/columnstore-indexes-query-performance.md)   
[Erste Schritte mit Columnstore für operative Echtzeitanalyse](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)   
[Columnstore-Indizes für Data Warehousing](../../relational-databases/indexes/columnstore-indexes-data-warehouse.md)  
[Columnstore Index Architecture (Columnstore-Indizes: Architektur)](../../relational-databases/sql-server-index-design-guide.md#columnstore_index)    
[Adaptive Indexdefragmentierung](http://github.com/Microsoft/tigertoolbox/tree/master/AdaptiveIndexDefrag)    
  
  

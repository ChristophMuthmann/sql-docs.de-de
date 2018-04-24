---
title: Verwenden von speicheroptimierten temporalen Tabellen mit Systemversionsverwaltung | Microsoft-Dokumentation
ms.custom: ''
ms.date: 05/05/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-tables
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 691d4f80-6754-43f5-8b43-d4facf08f6fc
caps.latest.revision: 12
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 8db58a982b33f061dc32548d4bd3f64cd8018b27
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="working-with-memory-optimized-system-versioned-temporal-tables"></a>Verwenden von speicheroptimierten temporalen Tabellen mit Systemversionsverwaltung
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  In diesem Thema wird erläutert, wie sich die Verwendung einer speicheroptimierten temporalen Tabelle mit Systemversionsverwaltung von der Verwendung einer datenträgerbasierten temporalen Tabelle mit Systemversionsverwaltung unterscheidet.  
  
> [!NOTE]  
>  Das Verwenden von temporalen mit speicheroptimierten Tabellen gilt nur für [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , und nicht für [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
## <a name="discovering-metadata"></a>Ermittlung von Metadaten  
 Um Metadaten zu einer speicheroptimierten temporalen Tabelle mit Systemversionsverwaltung zu ermitteln, müssen Sie Informationen aus [sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md) und [sys.internal_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-internal-tables-transact-sql.md)kombinieren. Eine temporale Tabelle mit Systemversionsverwaltung ist als "parent_object_id" der speicherinternen Verlaufstabelle vorhanden.  
  
 Dieses Beispiel zeigt, wie Sie diese Tabellen abfragen und verknüpfen können.  
  
```  
SELECT SCHEMA_NAME (T1.schema_id) as TemporalTableSchema  
   , OBJECT_NAME(IT.parent_object_id) as TemporalTableName  
   , T1.object_id as TemporalTableObjectId  
   , IT.Name as InternalHistoryStagingName   
   , SCHEMA_NAME (T2.schema_id) as HistoryTableSchema  
   , OBJECT_NAME (T1.history_table_id) as HistoryTableName   
FROM sys.internal_tables IT    
JOIN sys.tables T1   
   ON IT.parent_object_id = T1.object_id   
JOIN sys.tables T2   
   ON T1.history_table_id = T2.object_id   
WHERE T1.is_memory_optimized  = 1 AND T1.temporal_type = 2  
  
```  
  
## <a name="modifying-data"></a>Ändern von Daten  
 Speicheroptimierte temporale Tabellen mit Systemversionsverwaltung können über systeminterne kompilierte gespeicherte Prozeduren geändert werden, sodass Sie die Möglichkeit erhalten, nicht temporale speicheroptimierte Tabellen in Tabellen mit Systemversionsverwaltung zu konvertieren und vorhandene systemeigene gespeicherte Prozeduren beizubehalten.  
  
 Dieses Beispiel zeigt, wie eine zuvor erstellte Beispieltabelle in ein systemintern kompiliertes Modul geändert werden kann.  
  
```  
CREATE PROCEDURE dbo.UpdateFXCurrencyPair  
   (   
       @ProviderID int  
     , @CurrencyID1 int  
     , @CurrencyID2 int  
     , @BidRate decimal(8,4)  
     , @AskRate decimal(8,4)   
   )   
WITH NATIVE_COMPILATION, SCHEMABINDING  
   , EXECUTE AS OWNER   
AS    
   BEGIN ATOMIC WITH   
   (TRANSACTION ISOLATION LEVEL = SNAPSHOT  , LANGUAGE = N'English')   
      UPDATE dbo.FXCurrencyPairs SET AskRate = @AskRate, BidRate  = @BidRate   
     WHERE ProviderID = @ProviderID AND CurrencyID1 = @CurrencyID1 AND CurrencyID2 = @CurrencyID2   
END   
GO ;  
  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Temporale Tabellen mit Systemversionsverwaltung und speicheroptimierten Tabellen](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [Erstellen einer speicheroptimierten temporalen Tabelle mit Systemversionsverwaltung](../../relational-databases/tables/creating-a-memory-optimized-system-versioned-temporal-table.md)   
 [Überwachung von speicheroptimierten temporalen Tabellen mit Systemversionsverwaltung](../../relational-databases/tables/monitoring-memory-optimized-system-versioned-temporal-tables.md)   
 [Überlegungen zur Systemleistung bei Verwendung von speicheroptimierten temporalen Tabellen mit Systemversionsverwaltung](../../relational-databases/tables/memory-optimized-system-versioned-temporal-tables-performance.md)   
 [Temporale Tabellen](../../relational-databases/tables/temporal-tables.md)   
 [Systemkonsistenzprüfungen von temporalen Tabellen](../../relational-databases/tables/temporal-table-system-consistency-checks.md)   
 [Verwalten der Beibehaltung von Verlaufsdaten in temporalen Tabellen mit Systemversionsverwaltung](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [Metadatenansichten und Funktionen für temporale Tabellen](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
  
  

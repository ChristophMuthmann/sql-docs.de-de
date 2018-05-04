---
title: Sys. dm_db_xtp_hash_index_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_xtp_hash_index_stats
- sys.dm_db_xtp_hash_index_stats_TSQL
- dm_db_xtp_hash_index_stats
- dm_db_xtp_hash_index_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_hash_index_stats (dynamic management view)
ms.assetid: 45969884-cd61-48e8-aee5-c725c78e3e4c
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: cd0d4a52f685c1753cc9073d08dfc02982f1784a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmdbxtphashindexstats-transact-sql"></a>sys.dm_db_xtp_hash_index_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  Diese Statistik ist für das Verständnis und die Optimierung der Bucketanzahl hilfreich. Sie kann auch verwendet werden, um Fälle zu erkennen, in denen der Indexschlüssel viele Duplikate aufweist.  
  
 Eine große durchschnittliche Kettenlänge weist darauf hin, dass viele Zeilen demselben Hashbucket hinzugefügt werden. Dies könnte folgende Ursachen haben:  
  
-   Wenn die Anzahl der leeren Buckets niedrig ist oder die durchschnittliche und die maximale Kettenlänge ähnlich sind, besteht die Wahrscheinlichkeit, dass die Bucketgesamtanzahl zu niedrig ist. Dies führt dazu, dass viele verschiedene Indexschlüssel demselben Hashbucket hinzugefügt werden.  
  
-   Wenn die Anzahl der leeren Buckets hoch oder die maximale Kettenlänge relativ zur durchschnittlichen Kettenlänge hoch ist, besteht die Wahrscheinlichkeit, dass viele Zeilen mit doppelten Indexschlüsselwerten vorliegen oder dass die Schlüsselwerte verzerrt sind. Alle Zeilen mit demselben Indexschlüsselwert werden demselben Hashbucket hinzugefügt. Daher weist dieser Bucket eine große Kettenlänge auf.  
  
Hohe Kettenlängen können die Leistung aller DML-Vorgänge für einzelne Zeilen, einschließlich von SELECT oder INSERT, deutlich beeinträchtigen. Kurze Kettenlängen in Kombination mit einer hohen Anzahl von leeren Buckets weisen auf eine zu hohe Bucketanzahl hin. Dadurch wird die Leistung von Indexscans verringert.  
  
> [!WARNING]
> **Sys. dm_db_xtp_hash_index_stats** überprüft die gesamte Tabelle. Wenn große Tabellen in der Datenbank stehen also **dm_db_xtp_hash_index_stats** kann sehr lange dauern ausführen.  
  
Weitere Informationen finden Sie unter [Hash-Indizes für Speicheroptimierte Tabellen](../../relational-databases/sql-server-index-design-guide.md#hash_index).  
  
|Spaltenname|Typ|Description|  
|-----------------|----------|-----------------|  
|object_id|**int**|Die Objekt-ID der übergeordneten Tabelle.|  
|xtp_object_id|**bigint**|Die ID der speicheroptimierten Tabelle.|  
|index_id|**int**|Die Index-ID.|  
|total_bucket_count|**bigint**|Die Gesamtanzahl der Hashbuckets im Index.|  
|empty_bucket_count|**bigint**|Die Anzahl der leeren Hashbuckets im Index.|  
|avg_chain_length|**bigint**|Die durchschnittliche Länge der Zeilenketten für alle Hashbuckets im Index.|  
|max_chain_length|**bigint**|Die maximale Länge der Zeilenketten in den Hashbuckets.|  
|xtp_object_id|**bigint**|Die in-Memory-OLTP-Objekt-ID, der die Speicheroptimierte Tabelle entspricht.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW DATABASE STATE-Berechtigung auf dem Server.  

## <a name="examples"></a>Beispiele  
  
### <a name="a-troubleshooting-hash-index-bucket-count"></a>A. Problembehandlung bei Hashindex-Bucketanzahl

Die folgende Abfrage kann verwendet werden, um einer vorhandenen Tabelle die Hashindex-Bucketanzahl zu beheben. Die Abfrage gibt Statistiken zu den Prozentsatz des leeren Buckets und kettenlänge für alle Hash-Indizes für Benutzertabellen.

```sql
  SELECT  
    QUOTENAME(SCHEMA_NAME(t.schema_id)) + N'.' + QUOTENAME(OBJECT_NAME(h.object_id)) as [table],   
    i.name                   as [index],   
    h.total_bucket_count,  
    h.empty_bucket_count,  
    FLOOR((  
      CAST(h.empty_bucket_count as float) /  
        h.total_bucket_count) * 100)  
                             as [empty_bucket_percent],  
    h.avg_chain_length,   
    h.max_chain_length  
  FROM sys.dm_db_xtp_hash_index_stats as h   
  INNER JOIN sys.indexes as i  
            ON h.object_id = i.object_id  
           AND h.index_id  = i.index_id  
    INNER JOIN sys.memory_optimized_tables_internal_attributes ia ON h.xtp_object_id=ia.xtp_object_id
    INNER JOIN sys.tables t on h.object_id=t.object_id
  WHERE ia.type=1
  ORDER BY [table], [index];  
``` 

Weitere Informationen zum Interpretieren der Ergebnisse dieser Abfrage finden Sie unter [Problembehandlung Hash-Indizes für Speicheroptimierte Tabellen](../../relational-databases/in-memory-oltp/hash-indexes-for-memory-optimized-tables.md) .  

### <a name="b-hash-index-statistics-for-internal-tables"></a>B. Hashindexstatistik für interne Tabellen

Bestimmte Funktionen verwendet interne Tabellen, die den Hash-Indizes, z. B. columnstore-Indizes für Speicheroptimierte Tabellen zu nutzen. Die folgende Abfrage gibt Statistiken für Hashindizes für interne Tabellen, die an Benutzertabellen verknüpft sind.

```sql
  SELECT  
    QUOTENAME(SCHEMA_NAME(t.schema_id)) + N'.' + QUOTENAME(OBJECT_NAME(h.object_id)) as [user_table],
    ia.type_desc as [internal_table_type],
    i.name                   as [index],   
    h.total_bucket_count,  
    h.empty_bucket_count,  
    h.avg_chain_length,   
    h.max_chain_length  
  FROM sys.dm_db_xtp_hash_index_stats as h   
  INNER JOIN sys.indexes as i  
            ON h.object_id = i.object_id  
           AND h.index_id  = i.index_id  
    INNER JOIN sys.memory_optimized_tables_internal_attributes ia ON h.xtp_object_id=ia.xtp_object_id
    INNER JOIN sys.tables t on h.object_id=t.object_id
  WHERE ia.type!=1
  ORDER BY [user_table], [internal_table_type], [index]; 
```

Beachten Sie, dass der bucket_count-Wert des Indexes für interne Tabellen kann nicht geändert werden, daher die Ausgabe dieser Abfrage sollte berücksichtigt werden informative nur. Keine Aktion erforderlich.  

Diese Abfrage ist nicht davon keine Zeilen zurückgeben, es sei denn, Sie verwenden eine Funktion, die Hash-Indizes für Tabellen internen nutzt. Das folgende Speicheroptimierte Tabelle enthält einen columnstore-Index. Nach dem Erstellen dieser Tabelle, wird der Hash-Indizes für interne Tabellen angezeigt werden.

```sql
  CREATE TABLE dbo.table_columnstore
  (
    c1 INT NOT NULL PRIMARY KEY NONCLUSTERED,
    INDEX ix_columnstore CLUSTERED COLUMNSTORE
  ) WITH (MEMORY_OPTIMIZED=ON)
```

## <a name="see-also"></a>Siehe auch  
 [Eine Speicheroptimierte Tabelle dynamische Verwaltungssichten &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  

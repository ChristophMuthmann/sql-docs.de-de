---
title: memory_optimized_tables_internal_attributes (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.memory_optimized_tables_internal_attributes
- sys.memory_optimized_tables_internal_attributes_TSQL
- memory_optimized_tables_internal_attributes
- memory_optimized_tables_internal_attributes_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.memory_optimized_tables_internal_attributes catalog view
ms.assetid: 78ef5807-0504-4de8-9a01-ede6c03c7ff1
caps.latest.revision: "13"
author: jodebrui
ms.author: jodebrui
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3ab05ef27e9687be506db960e628868cb08184d3
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysmemoryoptimizedtablesinternalattributes-transact-sql"></a>sys.memory_optimized_tables_internal_attributes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Enthält eine Zeile für jede interne speicheroptimierte Tabelle, die zum Speichern von speicheroptimierten Benutzertabellen verwendet wird. Jede Benutzertabelle entspricht mindestens einer internen Tabelle. Eine einzelne Tabelle wird für die Speicherung von Kerndaten verwendet. Zusätzliche interne Tabellen werden für die Unterstützung von Funktionen wie dem temporalen Columnstore-Index und die Speicherung außerhalb von Zeilen (LOB) für speicheroptimierte Tabellen verwendet.
 
| Spaltenname  | Datentyp  | Beschreibung |
| :------ |:----------| :-----|
|object_id  |**int**|       Die ID der Benutzertabelle. Interne speicheroptimierte Tabellen, die der Unterstützung einer Benutzertabelle dienen (wie etwa Speicherung außerhalb der Zeile oder gelöschte Zeilen im Fall von Hk/Columnstore-Kombinationen), weisen die gleiche object_id wie ihr übergeordnetes Objekt auf. |
|xtp_object_id  |**bigint**|    In-Memory-OLTP-Objekt-ID, die der internen speicheroptimierten Tabelle entspricht, die für die Unterstützung der Benutzertabelle verwendet wird. Sie ist innerhalb der Datenbank eindeutig und kann sich im Lauf der Lebensspanne des Objekts ändern. 
|Typ|  **int** |   Der Typ der internen Tabelle.<br/><br/> 0 => DELETED_ROWS_TABLE <br/> 1 => USER_TABLE <br/> 2 => DICTIONARIES_TABLE<br/>3 => SEGMENTS_TABLE<br/>4 => ROW_GROUPS_INFO_TABLE<br/>5 => INTERNAL OFF-ROW DATA TABLE<br/>252 => INTERNAL_TEMPORAL_HISTORY_TABLE | 
|type_desc| **nvarchar(60)**|   Beschreibung des Typs<br/><br/>DELETED_ROWS_TABLE -> Interne Tabelle zur Nachverfolgung gelöschter Zeilen für einen Columnstore-Index<br/>USER_TABLE -> Tabelle, die die zeileninternen Benutzerdaten enthält<br/>DICTIONARIES_TABLE -> Wörterbücher für einen Columnstore-Index<br/>SEGMENTS_TABLE -> Komprimierte Segmente für einen Columnstore-Index<br/>ROW_GROUPS_INFO_TABLE -> Metadaten zu komprimierten Zeilengruppen eines Columnstore-Indexes<br/>INTERNAL OFF-ROW DATA TABLE -> Interne Tabelle, die für die Speicherung einer Spalte außerhalb von Zeilen verwendet wird. In diesem Fall gibt minor_id die column_id an.<br/>INTERNAL_TEMPORAL_HISTORY_TABLE -> Heißes Endsegment der datenträgerbasierten Verlaufstabelle. Zeilen, die in den Verlauf eingefügt werden, werden zuerst in diese interne speicheroptimierte Tabelle eingefügt. Eine Hintergrundaufgabe verschiebt asynchron Zeilen aus dieser internen Tabelle in die datenträgerbasierte Verlaufstabelle. |
|minor_id|  **int**|    0 gibt eine Benutzer- oder eine interne Tabelle an<br/><br/>Ein anderer Wert als 0 gibt die ID einer außerhalb von Zeilen gespeicherten Spalte an. Joins mit column_id in sys.columns.<br/><br/>Jeder außerhalb von Zeilen gespeicherten Spalte entspricht eine Zeile in dieser Systemansicht.|

## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-returning-all-columns-that-are-stored-off-row"></a>A. Zurückgeben aller Spalten, die außerhalb von Zeilen gespeichert sind

Das folgende T-SQL-Skript veranschaulicht eine Tabelle mit mehreren großen Spalten, die nicht vom LOB-Typ sind, und einer einzelnen LOB-Spalte:

```Transact-SQL
CREATE TABLE dbo.LargeTableSample
(
      Id   int IDENTITY PRIMARY KEY NONCLUSTERED,
      C1   nvarchar(4000),
      C2   nvarchar(4000),
      C3   nvarchar(4000),
      C4   nvarchar(4000),
      Misc nvarchar(max)
) WITH (MEMORY_OPTIMIZED = ON);
GO
```

Die folgende Abfrage zeigt alle Spalten, die außerhalb der Zeile gespeichert sind, zusammen mit ihrer Größe. Eine Größe von-1 gibt eine LOB-Spalte an. Alle LOB-Spalten werden außerhalb von Zeilen gespeichert.

```Transact-SQL
SELECT 
  QUOTENAME(SCHEMA_NAME(o.schema_id)) + N'.' + QUOTENAME(OBJECT_NAME(moa.object_id)) AS 'table', 
  c.name AS 'column', 
  c.max_length
FROM sys.memory_optimized_tables_internal_attributes moa
     JOIN sys.columns c ON moa.object_id = c.object_id AND moa.minor_id=c.column_id
     JOIN sys.objects o on moa.object_id=o.object_id 
WHERE moa.type=5;
```

### <a name="b-returning-memory-consumption-of-all-columns-that-are-stored-off-row"></a>B. Zurückgeben des Speicherverbrauchs aller Spalten, die außerhalb von Zeilen gespeichert sind

Um mehr Details zum Speicherverbrauch von außerhalb von Zeilen gespeicherten Spalten abzurufen, können Sie die folgende Abfrage verwenden, die den Speicherverbrauch aller internen Tabellen und ihre Indizes angibt, die zum Speichern der Spalten außerhalb von Zeilen verwendet werden:

```Transact-SQL
SELECT
  QUOTENAME(SCHEMA_NAME(o.schema_id)) + N'.' + QUOTENAME(OBJECT_NAME(moa.object_id)) AS 'table',
  c.name AS 'column',
  c.max_length,
  mc.memory_consumer_desc,
  mc.index_id,
  mc.allocated_bytes,
  mc.used_bytes
FROM sys.memory_optimized_tables_internal_attributes moa
   JOIN sys.columns c ON moa.object_id = c.object_id AND moa.minor_id=c.column_id
   JOIN sys.dm_db_xtp_memory_consumers mc ON moa.xtp_object_id=mc.xtp_object_id
   JOIN sys.objects o on moa.object_id=o.object_id 
WHERE moa.type=5;
```

### <a name="c-returning-memory-consumption-of-columnstore-indexes-on-memory-optimized-tables"></a>C. Zurückgeben des Speicherverbrauches von Columnstore-Indizes für speicheroptimierte Tabellen

Verwenden Sie die folgende Abfrage, um die arbeitsspeichernutzung der columnstore-Indizes für Speicheroptimierte Tabellen anzuzeigen:

```Transact-SQL
SELECT
  QUOTENAME(SCHEMA_NAME(o.schema_id)) + N'.' + QUOTENAME(OBJECT_NAME(moa.object_id)) AS 'table',
  i.name AS 'columnstore index',
  SUM(mc.allocated_bytes) / 1024 as [allocated_kb],
  SUM(mc.used_bytes) / 1024 as [used_kb]
FROM sys.memory_optimized_tables_internal_attributes moa
   JOIN sys.indexes i ON moa.object_id = i.object_id AND i.type in (5,6)
   JOIN sys.dm_db_xtp_memory_consumers mc ON moa.xtp_object_id=mc.xtp_object_id
   JOIN sys.objects o on moa.object_id=o.object_id
WHERE moa.type IN (0, 2, 3, 4)
GROUP BY o.schema_id, moa.object_id, i.name;
```

Verwenden Sie die folgende Abfrage Aufschlüsselung der Speicherverbrauch interner Datenstrukturen, die für columnstore-Indizes für Speicheroptimierte Tabellen verwendet:

```Transact-SQL
SELECT
  QUOTENAME(SCHEMA_NAME(o.schema_id)) + N'.' + QUOTENAME(OBJECT_NAME(moa.object_id)) AS 'table',
  i.name AS 'columnstore index',
  moa.type_desc AS 'internal table',
  mc.index_id AS 'index',
  mc.memory_consumer_desc,
  mc.allocated_bytes / 1024 as [allocated_kb],
  mc.used_bytes / 1024 as [used_kb]
FROM sys.memory_optimized_tables_internal_attributes moa
   JOIN sys.indexes i ON moa.object_id = i.object_id AND i.type in (5,6)
   JOIN sys.dm_db_xtp_memory_consumers mc ON moa.xtp_object_id=mc.xtp_object_id
   JOIN sys.objects o on moa.object_id=o.object_id
WHERE moa.type IN (0, 2, 3, 4)
```



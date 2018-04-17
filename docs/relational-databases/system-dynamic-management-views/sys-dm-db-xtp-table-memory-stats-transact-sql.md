---
title: dm_db_xtp_table_memory_stats (Transact-SQL) | Microsoft Docs
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
- sys.dm_db_xtp_table_memory_stats_TSQL
- dm_db_xtp_table_memory_stats
- sys.dm_db_xtp_table_memory_stats
- dm_db_xtp_table_memory_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_table_memory_stats
- dm_db_xtp_table_memory_stats
ms.assetid: ad0efc06-3d9c-4861-9dfa-a7a87822d0c8
caps.latest.revision: 17
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 3cf854d48d05e37a4ca6ff2cbc4418bd56df9b6b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmdbxtptablememorystats-transact-sql"></a>sys.dm_db_xtp_table_memory_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  Gibt Speicherauslastungsstatistiken für jede [!INCLUDE[hek_2](../../includes/hek-2-md.md)]-Tabelle (Benutzer und System) in der aktuellen Datenbank zurück. Die Systemtabellen haben negative Objekt-IDs und werden verwendet, um Laufzeitinformationen für das [!INCLUDE[hek_2](../../includes/hek-2-md.md)]-Modul zu speichern. Im Gegensatz zu Benutzerobjekten sind Systemtabellen intern und nur im Arbeitsspeicher vorhanden. Daher werden sie in Katalogsichten nicht aufgeführt. Systemtabellen werden verwendet, um Informationen wie Metadaten für alle Daten/Änderungsdateien im Speicher, Zusammenführungsanforderungen, Wasserzeichen für Änderungsdateien und Zeilenfilterung, gelöschte Tabellen und relevante Informationen für Wiederherstellungen und Sicherungen zu speichern. Das [!INCLUDE[hek_2](../../includes/hek-2-md.md)]-Modul unterstützt bis zu 8.192 Daten- und Änderungsdateipaare. Bei großen Datenbanken im Arbeitsspeicher ergibt sich damit eine Arbeitsspeicherauslastung durch Systemtabellen von einigen Megabyte.  
  
 Weitere Informationen finden Sie unter [In-Memory OLTP &#40;Arbeitsspeicheroptimierung&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|object_id|**int**|Die Objekt-ID der Tabelle. NULL für In-Memory OLTP-Systemtabellen.|  
|memory_allocated_for_table_kb|**bigint**|Für diese Tabelle zugeordneter Arbeitsspeicher.|  
|memory_used_by_table_kb|**bigint**|Von der Tabelle verwendeter Arbeitsspeicher einschließlich Zeilenversionen.|  
|memory_allocated_for_indexes_kb|**bigint**|Für Indizes dieser Tabelle zugeordneter Arbeitsspeicher.|  
|memory_used_by_indexes_kb|**bigint**|Für Indizes dieser Tabelle verwendeter Speicher.|  
  
## <a name="permissions"></a>Berechtigungen  
 Alle Zeilen werden zurückgegeben, wenn Sie über die VIEW DATABASE STATE-Berechtigung für die aktuelle Datenbank verfügen. Andernfalls wird ein leeres Rowset zurückgegeben.  
  
 Wenn Sie nicht über die VIEW DATABASE-Berechtigung verfügen, werden alle Spalten für Zeilen in Tabellen zurückgegeben, für die Sie die SELECT-Berechtigung besitzen.  
  
 Systemtabellen werden nur für Benutzer mit der VIEW DATABASE STATE-Berechtigung zurückgegeben.  
  
## <a name="examples"></a>Beispiele  
 Sie können die folgende DMV abfragen, um den Arbeitsspeicher abzurufen, der für die Tabellen und Indizes in der Datenbank zugeordnet ist:  
  
```  
-- finding memory for objects  
SELECT OBJECT_NAME(object_id), *   
FROM sys.dm_db_xtp_table_memory_stats;  
```  
  
 So suchen Sie nach dem Arbeitsspeicher für alle Objekte innerhalb der Datenbank:  
  
```  
SELECT SUM( memory_allocated_for_indexes_kb + memory_allocated_for_table_kb) AS  
 memoryallocated_objects_in_kb   
FROM sys.dm_db_xtp_table_memory_stats;  
```  
  
## <a name="user-scenario"></a>Benutzerszenario  
 Erstellen Sie zunächst die folgenden Tabellen in einer Datenbank mit der Bezeichnung "HkDb1".  
  
```  
-- set max server memory to 4 GB  
EXEC sp_configure 'max server memory (MB)', 4048  
go  
  
RECONFIGURE  
go  
  
-- create a resource pool for database with memory-optimized objects  
CREATE RESOURCE POOL PoolHkDb1 WITH (MAX_MEMORY_PERCENT = 50);  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
go  
  
--bind the pool to the database  
EXEC sp_xtp_bind_db_resource_pool 'HkDb1', 'PoolHkdb1'  
go  
  
-- take database offline/online to associate the pool  
use master  
go  
  
alter database HkDb1 set offline  
go  
alter database HkDb1 set online  
go  
  
USE HkDb1  
go  
  
CREATE TABLE dbo.t1 (  
       c1 int NOT NULL,  
       c2 char(40) NOT NULL,  
       c3 char(8000) NOT NULL,  
  
       CONSTRAINT [pk_t1_c1] PRIMARY KEY NONCLUSTERED HASH (c1) WITH (BUCKET_COUNT = 100000)  
) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
go  
  
CREATE TABLE dbo.t2 (  
       c1 int NOT NULL,  
       c2 char(40) NOT NULL,  
       c3 char(8000) NOT NULL,  
  
       CONSTRAINT [pk_t2_c1] PRIMARY KEY NONCLUSTERED HASH (c1) WITH (BUCKET_COUNT = 100000)  
) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
go  
  
CREATE TABLE dbo.t3 (  
       c1 int NOT NULL,  
       c2 char(40) NOT NULL,  
       c3 char(8000) NOT NULL,  
  
       CONSTRAINT [pk_t3_c1] PRIMARY KEY NONCLUSTERED HASH (c1) WITH (BUCKET_COUNT = 1000000)  
) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
go  
  
-- load 150K rows  
declare @i int = 0  
while (@i <= 150000)  
begin  
       insert t1 values (@i, 'a', replicate ('b', 8000))  
       set @i += 1;  
end  
go  
```  
  
 Wenn Daten in eine Tabelle geladen werden, können Sie benutzerdefinierte Tabellen und den von ihnen belegten Speicher sehen. Jede Zeile einer Tabelle kann beispielsweise ungefähr 8.070 Bytes umfassen (Zuordnungsgröße ist 8 K (8.192 Bytes)). Sie können die Indizes pro Tabelle und den vom Index belegten Speicher sehen. 1 MB sind beispielsweise 100 K Einträge, die auf die nächste Zweierpotenz gerundet werden 2 (2**17) = 131072 von je 8 Bytes. Möglicherweise weist eine Tabelle keinen Index auf. In diesem Fall wird die Speicherbelegung für den Index angezeigt. Andere Zeilen können Systemtabellen darstellen.  
  
```  
select convert(char(10), object_name(object_id)) as Name,*   
from sys.dm_db_xtp_table_memory_stats  
```  
  
 Im Folgenden die zweiteilige Ausgabe:  
  
```  
Name       object_id   memory_allocated_for_table_kb memory_used_by_table_kb  
---------- ----------- ----------------------------- -----------------------  
t3         629577281   0                             0  
t1         565577053   1372928                       1202351  
t2         597577167   0                             0  
NULL       -6          0                             0  
NULL       -5          0                             0  
NULL       -4          0                             0  
NULL       -3          0                             0  
NULL       -2          192                           25  
  
memory_allocated_for_indexes_kb memory_used_by_indexes_kb  
------------------------------- -------------------------  
8192                            8192  
1024                            1024  
8192                            8192  
2                               2  
24                              24  
2                               2  
2                               2  
16                              16  
```  
  
 Die Ausgabe von  
  
```  
select  sum(allocated_bytes)/(1024*1024) as total_allocated_MB,   
       sum(used_bytes)/(1024*1024) as total_used_MB  
from sys.dm_db_xtp_memory_consumers  
```  
  
 ist  
  
```  
total_allocated_MB   total_used_MB  
-------------------- --------------------  
1357                 1191  
```  
  
 Als Nächstes betrachten wir die Ausgabe des Ressourcenpools. Aus dem Pool wurden 1356 MB Arbeitsspeicher genutzt.  
  
```  
select pool_id,convert(char(10), name) as Name, min_memory_percent, max_memory_percent,   
   max_memory_kb/1024 as max_memory_mb  
from sys.dm_resource_governor_resource_pools  
  
select used_memory_kb/1024 as used_memory_mb ,target_memory_kb/1024 as target_memory_mb  
from sys.dm_resource_governor_resource_pools  
```  
  
 Im Folgenden die Ausgabe:  
  
```  
pool_id     Name       min_memory_percent max_memory_percent max_memory_mb  
----------- ---------- ------------------ ------------------ --------------------  
1           internal   0                  100                3845  
2           default    0                  100                3845  
259         PoolHkDb1  0                  100                3845  
  
used_memory_mb       target_memory_mb  
-------------------- --------------------  
125                  3845  
32                   3845  
1356                 3845  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Eine Speicheroptimierte Tabelle dynamische Verwaltungssichten &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  

---
title: Sys. dm_db_xtp_memory_consumers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
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
- sys.dm_db_xtp_memory_consumers
- dm_db_xtp_memory_consumers
- dm_db_xtp_memory_consumers_TSQL
- sys.dm_db_xtp_memory_consumers_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_memory_consumers dynamic management view
ms.assetid: f7ab2eaf-e627-464d-91fe-0e170b3f37bc
caps.latest.revision: 24
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: e2edb2149c92cd0325145af5396abc3063ae3b73
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmdbxtpmemoryconsumers-transact-sql"></a>sys.dm_db_xtp_memory_consumers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  Meldet die Arbeitsspeicherconsumer auf Datenbankebene in der [!INCLUDE[hek_2](../../includes/hek-2-md.md)]-Datenbank-Engine. Diese Sicht gibt eine Zeile für jeden Arbeitsspeicherconsumer zurück, den die Datenbank-Engine verwendet. Verwenden Sie diese DMV, um anzuzeigen, wie der Arbeitsspeicher auf andere interne Objekte verteilt ist.  
  
 Weitere Informationen finden Sie unter [In-Memory OLTP &#40;Arbeitsspeicheroptimierung&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|memory_consumer_id|**bigint**|ID (intern) des Arbeitsspeicherconsumers.|  
|memory_consumer_type|**int**|Der Typ des Arbeitsspeicherconsumers:<br /><br /> 0=Aggregation. (Aggregiert die Arbeitsspeichernutzung von mindestens zwei Consumern. Sollte nicht angezeigt werden.)<br /><br /> 2=VARHEAP (Verfolgt die Arbeitsspeichernutzung für einen Heap variabler Länge nach.)<br /><br /> 3=HASH (Verfolgt die Arbeitsspeichernutzung für einen Index nach.)<br /><br /> 5=DB-Seitenpool (Verfolgt die Arbeitsspeichernutzung für einen Datenbank-Seitenpool nach, der für Laufzeitvorgänge verwendet wird, z. B. Tabellenvariablen und einige serialisierbare Scans. Es gibt nur einen Arbeitsspeicherconsumer dieses Typs pro Datenbank.)|  
|memory_consumer_type_desc|**nvarchar(64)**|Typ des Arbeitsspeicherconsumers: VARHEAP, HASH oder PGPOOL.<br /><br /> 0 – (Sollte nicht angezeigt werden.)<br /><br /> 2 - VARHEAP<br /><br /> 3 – HASH<br /><br /> 5 - PGPOOL|  
|memory_consumer_desc|**nvarchar(64)**|Die Beschreibung der Arbeitsspeicherconsumer-Instanz:<br /><br /> VARHEAP: <br />Datenbankheap. Wird zum Zuordnen von Benutzerdaten für eine Datenbank (d. h. Zeilen) verwendet.<br />Datenbank-Systemheap. Wird zum Zuordnen von Datenbankdaten verwendet, die in Speicherabbilder eingefügt werden und keine Benutzerdaten enthalten.<br />Bereichsindexheap. Ein privater Heap, der vom Breichsindex zum Zuordnen von BW-Seiten verwendet wird.<br /><br /> HASH: Keine Beschreibung, da Object_id gibt an, die Tabelle und Index_id den Hashindex selbst.<br /><br /> PGPOOL: Für die Datenbank ist nur ein Seitenpool Datenbank 64 KB-Seitenpool.|  
|object_id|**bigint**|Die Objekt-ID, der der belegte Arbeitsspeicher attributiert wird. Ein negativer Wert für Systemobjekte.|  
|xtp_object_id|**bigint**|Die Objekt-ID für die Speicheroptimierte Tabelle.|  
|index_id|**int**|Die Index-ID des Consumers (sofern vorhanden). NULL für Basistabellen.|  
|allocated_bytes|**bigint**|Anzahl der für den Consumer reservierten Bytes.|  
|used_bytes|**bigint**|Die von diesem Consumer verwendeten Bytes. Gilt nur für varheap.|  
|allocation_count|**int**|Anzahl der Zuordnungen.|  
|partition_count|**int**|Nur interne Verwendung.|  
|sizeclass_count|**int**|Nur interne Verwendung.|  
|min_sizeclass|**int**|Nur interne Verwendung.|  
|max_sizeclass|**int**|Nur interne Verwendung.|  
|memory_consumer_address|**varbinary**|Interne Adresse des Consumers. Nur zur internen Verwendung.|  
|xtp_object_id|**bigint**|Die in-Memory-OLTP-Objekt-ID, der die Speicheroptimierte Tabelle entspricht.|  
  
## <a name="remarks"></a>Hinweise  
 In der Ausgabe verweisen die Zuordnungen auf Datenbankebene auf Benutzertabellen, Indizes und Systemtabellen. VARHEAP mit object_id = NULL verweist auf Arbeitsspeicher, der Tabellen mit Spalten variabler Länge zugeordnet ist.  
  
## <a name="permissions"></a>Berechtigungen  
 Alle Zeilen werden zurückgegeben, wenn Sie über die VIEW DATABASE STATE-Berechtigung für die aktuelle Datenbank verfügen. Andernfalls wird ein leeres Rowset zurückgegeben.  
  
 Wenn Sie nicht über die VIEW DATABASE-Berechtigung verfügen, werden alle Spalten für Zeilen in Tabellen zurückgegeben, für die Sie die SELECT-Berechtigung besitzen.  
  
 Systemtabellen werden nur für Benutzer mit der VIEW DATABASE STATE-Berechtigung zurückgegeben.  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 Wenn eine Speicheroptimierte Tabelle einen columnstore-Index verfügt, verwendet das System einige interne Tabellen, bei die bestimmte Menge an Arbeitsspeicher belegen und zum Nachverfolgen von Daten für den columnstore-Index. Weitere Informationen zu diesen internen Tabellen sowie Beispielabfragen, die mit ihren Speicherverbrauch finden Sie unter [memory_optimized_tables_internal_attributes (Transact-SQL)](../../relational-databases/system-catalog-views/sys-memory-optimized-tables-internal-attributes-transact-sql.md).
 
  
## <a name="examples"></a>Beispiele  
  
```  
-- memory consumers (database level)  
SELECT OBJECT_NAME(object_id), *   
FROM sys.dm_db_xtp_memory_consumers;  
```  
  
## <a name="user-scenario"></a>Benutzerszenario  
  
```  
-- memory consumers (database level)  
  
select  convert(char(10), object_name(object_id)) as Name,   
convert(char(10),memory_consumer_type_desc ) as memory_consumer_type_desc, object_id,index_id, allocated_bytes,  used_bytes   
from sys.dm_db_xtp_memory_consumers  
```  
  
 Im Folgenden die Ausgabe mit einer Teilmenge der Spalten. Die Zuordnungen auf Datenbankebene verweisen auf Benutzertabellen, Indizes und Systemtabellen. VARHEAP mit object_id = NULL (letzte Zeile) verweist auf Arbeitsspeicher, der Datenzeilen der Tabellen (in diesem Beispiel "t1") zugeordnet ist. In MB konvertiert betragen die belegten Bytes 1340 MB.  
  
```  
Name       memory_consumer_type_desc object_id   index_id    allocated_bytes      used_bytes  
---------- ------------------------- ----------- ----------- -------------------- --------------------  
t3         HASH                      629577281   2           8388608              8388608  
t2         HASH                      597577167   2           8388608              8388608  
t1         HASH                      565577053   2           1048576              1048576  
NULL       HASH                      -6          1           2048                 2048  
NULL       VARHEAP                   -6          NULL        0                    0  
NULL       HASH                      -5          3           8192                 8192  
NULL       HASH                      -5          2           8192                 8192  
NULL       HASH                      -5          1           8192                 8192  
NULL       HASH                      -4          1           2048                 2048  
NULL       VARHEAP                   -4          NULL        0                    0  
NULL       HASH                      -3          1           2048                 2048  
NULL       HASH                      -2          2           8192                 8192  
NULL       HASH                      -2          1           8192                 8192  
NULL       VARHEAP                   -2          NULL        196608               26496  
NULL       HASH                      0           1           2048                 2048  
NULL       PGPOOL                    0           NULL        0                    0  
NULL       VARHEAP                   NULL        NULL        1405943808           1231220560  
  
(17 row(s) affected)  
```  
  
 Der gesamte Speicher belegten und verwendeten aus dieser DMV ist identisch mit der Objektebene in [dm_db_xtp_table_memory_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-table-memory-stats-transact-sql.md).  
  
```  
select  sum(allocated_bytes)/(1024*1024) as total_allocated_MB,   
        sum(used_bytes)/(1024*1024) as total_used_MB  
from sys.dm_db_xtp_memory_consumers  
  
total_allocated_MB   total_used_MB  
-------------------- --------------------  
1358                 1191  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Eine Speicheroptimierte Tabelle dynamische Verwaltungssichten &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  

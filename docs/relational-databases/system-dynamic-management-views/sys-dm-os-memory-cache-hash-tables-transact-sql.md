---
title: dm_os_memory_cache_hash_tables (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_os_memory_cache_hash_tables_TSQL
- sys.dm_os_memory_cache_hash_tables
- dm_os_memory_cache_hash_tables
- dm_os_memory_cache_hash_tables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_cache_hash_tables dynamic management view
ms.assetid: 68b94f35-8f80-4d2b-bcde-7a21934219af
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 3d78e8d9ec962fd69edcd885439d1c908f1fdddc
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmosmemorycachehashtables-transact-sql"></a>sys.dm_os_memory_cache_hash_tables (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt eine Zeile für jeden aktiven Cache in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz zurück.  
  
> [!NOTE]  
>  Aufrufen von [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] oder [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], verwenden Sie den Namen **sys.dm_pdw_nodes_os_memory_cache_hash_tables**.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**cache_address**|**varbinary(8)**|Die Adresse (Primärschlüssel) des Cacheeintrags. Lässt keine NULL-Werte zu.|  
|**name**|**nvarchar(256)**|Name des Caches. Lässt keine NULL-Werte zu.|  
|**type**|**nvarchar(60)**|Typ des Caches. Lässt keine NULL-Werte zu.|  
|**table_level**|**int**|Die Hashtabellennummer. Ein bestimmter Cache kann mehrere Hashtabellen besitzen, die unterschiedlichen Hashfunktionen entsprechen. Lässt keine NULL-Werte zu.|  
|**buckets_count**|**int**|Die Anzahl der Buckets in der Hashtabelle. Lässt keine NULL-Werte zu.|  
|**buckets_in_use_count**|**int**|Die Anzahl der Buckets, die zurzeit verwendet werden. Lässt keine NULL-Werte zu.|  
|**buckets_min_length**|**int**|Die minimale Anzahl von Cacheeinträgen in einem Bucket. Lässt keine NULL-Werte zu.|  
|**buckets_max_length**|**int**|Die maximale Anzahl von Cacheeinträgen in einem Bucket. Lässt keine NULL-Werte zu.|  
|**buckets_avg_length**|**int**|Die durchschnittliche Anzahl von Cacheeinträgen in jedem Bucket. Lässt keine NULL-Werte zu.|  
|**buckets_max_length_ever**|**int**|Die maximale Anzahl der Cacheinträge in einem Hashbucket für diese Hashtabelle seit dem Start des Servers. Lässt keine NULL-Werte zu.|  
|**hits_count**|**bigint**|Die Anzahl von Cachetreffern. Lässt keine NULL-Werte zu.|  
|**misses_count**|**bigint**|Die Anzahl von Cachefehlversuchen. Lässt keine NULL-Werte zu.|  
|**buckets_avg_scan_hit_length**|**int**|Die durchschnittliche Anzahl der untersuchten Einträge in einem Bucket, bevor das gesuchte Element gefunden wurde. Lässt keine NULL-Werte zu.|  
|**buckets_avg_scan_miss_length**|**int**|Die durchschnittliche Anzahl der untersuchten Einträge in einem Bucket, bevor die Suche ohne Erfolg beendet wurde. Lässt keine NULL-Werte zu.|  
|**pdw_node_id**|**int**|Der Bezeichner für den Knoten, dem auf diesem Verteilungspunkt befindet.<br /><br /> **Gilt für**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]|  
  
## <a name="permissions"></a>Berechtigungen 

Auf [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], erfordert `VIEW SERVER STATE` Berechtigung.   
Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], erfordert die `VIEW DATABASE STATE` Berechtigung in der Datenbank.   

## <a name="see-also"></a>Siehe auch  
 
  [SQL Server-Betriebssystem verbundene dynamische Verwaltungssichten &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  



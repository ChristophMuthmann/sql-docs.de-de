---
title: Sys.dm_db_xtp_nonclustered_index_stats (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/29/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_db_xtp_nonclustered_index_stats_TSQL
- dm_db_xtp_nonclustered_index_stats
- sys.dm_db_xtp_nonclustered_index_stats_TSQL
- sys.dm_db_xtp_nonclustered_index_stats
dev_langs: TSQL
helpviewer_keywords: sys.dm_db_xtp_nonclustered_index_stats
ms.assetid: d55ba31c-296c-419b-9c4b-c126e0a3d156
caps.latest.revision: "10"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e1b54d3955dd250a3d3799170e4ad15a7312802f
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="sysdmdbxtpnonclusteredindexstats-transact-sql"></a>sys.dm_db_xtp_nonclustered_index_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  "sys.dm_db_xtp_nonclustered_index_stats" enthält Statistikdaten zu Vorgängen, die für nicht gruppierte Indizes in speicheroptimierten Tabellen ausgeführt werden. "sys.dm_db_xtp_nonclustered_index_stats" enthält eine Zeile für jeden nicht gruppierten Index einer speicheroptimierten Tabelle in der aktuellen Datenbank.  
  
 Die in "sys.dm_db_xtp_nonclustered_index_stats" enthaltenen Statistikdaten werden bei der Erstellung der In-Memory-Indexstruktur erfasst. In-Memory-Indexstrukturen werden beim Neustart der Datenbank neu erstellt.  
  
 Verwenden Sie sys.dm_db_xtp_nonclustered_index_stats, um die Indexaktivitäten zu verstehen und zu überwachen, während DML-Vorgänge ausgeführt werden und eine Datenbank online geschaltet wird. Wenn eine Datenbank mit einer speicheroptimierten Tabelle neu gestartet wird, wird der Index erstellt, indem jeweils eine Zeile in den Arbeitsspeicher eingefügt wird. Anhand der Anzahl der Seitenteilungen, Zusammenführungen und Konsolidierungen können Sie nachvollziehen, welche Schritte zur Indexerstellung ausgeführt werden, wenn eine Datenbank online geschaltet wird. Sie können diese Werte auch vor und nach einer Reihe von DML-Vorgängen vergleichen.  
  
 Eine große Anzahl wiederholter Versuche weist auf Parallelitätsprobleme hin; wenden Sie sich an den [!INCLUDE[msCoName](../../includes/msconame-md.md)] Support.  
  
 Weitere Informationen zu speicheroptimierten, nicht gruppierten Indizes finden Sie unter [Übersicht über die SQL Server In-Memory-OLTP-Merkmale](http://t.co/T6zToWc6y6), Seite 17.  
  
|Spaltenname|Datentyp|Beschreibung|  
|-----------------|---------------|-----------------|  
|object_id|**int**|ID des Objekts.|  
|xtp_object_id|**bigint**|Die ID der speicheroptimierten Tabelle.|  
|index_id|**int**|Die ID des Index.|  
|delta_pages|**bigint**|Die Gesamtanzahl der Änderungsseiten für diesen Index in der Struktur.|  
|internal_pages|**bigint**|Für die interne Verwendung. Die Gesamtanzahl der internen Seiten für diesen Index in der Struktur.|  
|leaf_pages|**bigint**|Die Gesamtanzahl der Blattseiten für diesen Index in der Struktur.|  
|outstanding_retired_nodes|**bigint**|Für die interne Verwendung. Die Gesamtanzahl der Knoten für diesen Index in den internen Strukturen.|  
|page_update_count|**bigint**|Die kumulative Anzahl der Updatevorgänge für eine Seite im Index.|  
|page_update_retry_count|**bigint**|Die kumulative Anzahl der wiederholten Updatevorgänge für eine Seite im Index.|  
|page_consolidation_count|**bigint**|Die kumulative Anzahl der Seitenkonsolidierungen im Index.|  
|page_consolidation_retry_count|**bigint**|Die kumulative Anzahl der wiederholten Seitenkonsolidierungen.|  
|page_split_count|**bigint**|Die kumulative Anzahl der Seitenteilungsvorgänge im Index.|  
|page_split_retry_count|**bigint**|Die kumulative Anzahl der wiederholten Seitenteilungsvorgänge.|  
|key_split_count|**bigint**|Die kumulative Anzahl der Schlüsselteilungen im Index.|  
|key_split_retry_count|**bigint**|Die kumulative Anzahl der wiederholten Schlüsselteilungsvorgänge.|  
|page_merge_count|**bigint**|Die kumulative Anzahl der Seitenzusammenführungen im Index.|  
|page_merge_retry_count|**bigint**|Die kumulative Anzahl der wiederholten Seitenzusammenführungen.|  
|key_merge_count|**bigint**|Die kumulative Anzahl der Schlüsselzusammenführungen im Index.|  
|key_merge_retry_count|**bigint**|Die kumulative Anzahl der wiederholten Schlüsselzusammenführungen.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW DATABASE STATE-Berechtigung für die aktuelle Datenbank.  
  
## <a name="see-also"></a>Siehe auch  
 [Dynamische Verwaltungssichten für Speicheroptimierte Tabelle &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  

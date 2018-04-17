---
title: dm_fts_outstanding_batches (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/29/2017
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
- dm_fts_outstanding_batches
- dm_fts_outstanding_batches_TSQL
- sys.dm_fts_outstanding_batches_TSQL
- sys.dm_fts_outstanding_batches
dev_langs:
- TSQL
helpviewer_keywords:
- troubleshooting [SQL Server], full-text search
- sys.dm_fts_outstanding_batches dynamic management view
ms.assetid: c4d697ed-c906-4c28-b137-036a25e13c84
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: f8f68b3aba67ae2301588e0f064ed8b133489a0b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmftsoutstandingbatches-transact-sql"></a>sys.dm_fts_outstanding_batches (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt Informationen zu den einzelnen Volltext-Indizierungsbatches zurück.  
  
  |Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|database_id|**int**|ID der Datenbank|  
|catalog_id|**int**|ID des Volltextkatalogs|  
|table_id|**int**|ID der Tabellen-ID, die den Volltextindex enthält|  
|batch_id|**int**|Batch-ID|  
|memory_address|**varbinary(8)**|Die Speicheradresse des Batchobjekts|  
|crawl_memory_address|**varbinary(8)**|Speicheradresse des Durchforstungsobjekts (übergeordnetes Objekt)|  
|memregion_memory_address|**varbinary(8)**|Arbeitsspeicherbereichs-Speicheradresse des ausgehenden freigegebenen Speichers des Filterdaemonhosts (fdhost.exe)|  
|hr_batch|**int**|Zuletzt aufgetretener Fehlercode für den Batch|  
|is_retry_batch|**bit**|Gibt an, ob dies ein Wiederholungsbatch ist:<br /><br /> 0 = Nein<br /><br /> 1 = Ja|  
|retry_hints|**int**|Typ der für den Batch benötigten Wiederholung:<br /><br /> 0 = Keine Wiederholung<br /><br /> 1 = Multithreadwiederholung<br /><br /> 2 = Einzelthreadwiederholung<br /><br /> 3 = Einzel- und Multithreadwiederholung<br /><br /> 5 = Letzte Multithreadwiederholung<br /><br /> 6 = Letzte Einzelthreadwiederholung<br /><br /> 7 = Letzte Einzel- und Multithreadwiederholung|  
|retry_hints_description|**nvarchar(120)**|Beschreibung des benötigten Wiederholungstyps:<br /><br /> NO RETRY<br /><br /> MULTI THREAD RETRY<br /><br /> SINGLE THREAD RETRY<br /><br /> SINGLE AND MULTI THREAD RETRY<br /><br /> MULTI THREAD FINAL RETRY<br /><br /> SINGLE THREAD FINAL RETRY<br /><br /> SINGLE AND MULTI THREAD FINAL RETRY|  
|doc_failed|**bigint**|Anzahl der fehlgeschlagenen Dokumente im Batch|  
|batch_timestamp|**timestamp**|Der Timestampwert, der bei der Erstellung des Batches erhalten wurde|  
  
## <a name="permissions"></a>Berechtigungen  

Auf [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], erfordert `VIEW SERVER STATE` Berechtigung.   
Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], erfordert die `VIEW DATABASE STATE` Berechtigung in der Datenbank.   
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird in Erfahrung gebracht, wieviele Batches derzeit für jede Tabelle in der Serverinstanz verarbeitet werden.  
  
```  
SELECT database_id, table_id, COUNT(*) AS batch_count FROM sys.dm_fts_outstanding_batches GROUP BY database_id, table_id ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Volltextsuche und semantische Suche dynamische Verwaltungssichten und Funktionen &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)   
 [Volltextsuche](../../relational-databases/search/full-text-search.md)  
  
  

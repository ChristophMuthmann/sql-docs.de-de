---
title: Sys.index_resumable_operations (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.service: ''
ms.component: system-catalog-views
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.index_resumable_operations_TSQL
- sys.indexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.indexes
- sys.index_resumable_operations
ms.assetid: ''
caps.latest.revision: 1
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2017 || = sqlallproducts-allversions
ms.openlocfilehash: 5ab677122523c42f27aa206104911f213510d35e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="indexresumableoperations-transact-sql"></a>Index_resumable_operations (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]
**Sys.index_resumable_operations** ist eine Systemansicht, die überwacht und überprüft den aktuellen Ausführungsstatus für fortsetzbar indexneuerstellung.  
**Gilt für**: SQL Server-2017 und Azure SQL-Datenbank 
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Die ID des Objekts, zu dem dieser Index (keine Nullwerte zulässt) gehört.|  
|**index_id**|**int**|Die ID des Indexes (keine Nullwerte zulässt). **Index_id** ist nur innerhalb des Objekts eindeutig.|
|**name**|**sysname**|Der Name des Indexes. **Namen** ist nur innerhalb des Objekts eindeutig.|  
|**sql_text**|**nvarchar(max)**|Text der DDL-T-SQL-Anweisung|
|**last_max_dop**|**smallint**|Letzte MAX_DOP verwendet (Standardeinstellung = 0)|
|**partition_number**|**int**|Partitionsnummer im besitzenden Index oder Heap. Für nicht partitionierte Tabellen und Indizes oder im Fall werden alle Partitionen werden Neuerstellung der Wert dieser Spalte NULL ist.|
|**state**|**tinyint**|Betriebsstatus für fortsetzbar Index:<br /><br />0 = wird ausgeführt<br /><br />1 = anhalten|
|**state_desc**|**nvarchar(60)**|Beschreibung des Betriebsstatus für fortsetzbar Index (ausgeführt oder angehalten)|  
|**start_time**|**datetime**|Index Operation-Startzeit (nicht NULL zulassen)|
|**last_pause_time**|**datatime**| Indexvorgang anhalten zuletzt (NULL zulassen). NULL, wenn der Vorgang ausgeführt wird und nie angehalten wird.|
|**total_execution_time**|**int**|Gesamtausführungszeit von Startzeit in Minuten (nicht NULL zulassen)|
|**percent_complete**|**real**|Indizieren Sie die Bearbeitung abgeschlossen in % (keine Nullwerte zulässt).|
|**page_count**|**bigint**|Die Gesamtanzahl von Indexseiten, die von der Erstellungsvorgang für den neuen Index und die Zuordnung Indizes (keine Nullwerte zulässt) zugeordnet. 

## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
   
## <a name="example"></a>Beispiel  
 Listen Sie alle fortsetzbar Index Rebuild-Vorgänge, die sich im Status "angehalten" befinden. 
  
```  
SELECT * FROM  sys.index_resumable_operations WHERE STATE = 1;  
```  
  
## <a name="see-also"></a>Siehe auch 
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)    
 [Katalogsichten &#40;Transact-SQL&#41; ](catalog-views-transact-sql.md) [-Objekt Katalogsichten &#40;Transact-SQL&#41; ](object-catalog-views-transact-sql.md) [sys.indexes &#40;Transact-SQL&#41; ](sys-xml-indexes-transact-sql.md) [index_columns &#40;Transact-SQL&#41;](sys-index-columns-transact-sql.md)   
 [sys.xml_indexes &#40;Transact-SQL&#41;](sys-xml-indexes-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](sys-index-columns-transact-sql.md)   
 [sys.key_constraints &#40;Transact-SQL&#41;](sys-key-constraints-transact-sql.md)   
 [sys.filegroups &#40;Transact-SQL&#41;](sys-filegroups-transact-sql.md)   
 [sys.partition_schemes &#40;Transact-SQL&#41;](sys-partition-schemes-transact-sql.md)   
 [Häufig gestellte Fragen zu Abfragen des SQL Server-Systemkatalogs](querying-the-sql-server-system-catalog-faq.md)   
  

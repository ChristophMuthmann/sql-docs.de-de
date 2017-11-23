---
title: Sys.index_resumable_operations (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.reviewer: 
ms.service: 
ms.component: system-catalog-views
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.index_resumable_operations_TSQL
- sys.indexes_TSQL
dev_langs: TSQL
helpviewer_keywords:
- sys.indexes
- sys.index_resumable_operations
ms.assetid: 
caps.latest.revision: "1"
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bb2d574822922598524458e9e5a5fe45638a178e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
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
|**"sql_text"**|**nvarchar(max)**|Text der DDL-T-SQL-Anweisung|
|**last_max_dop**|**smallint**|Letzte MAX_DOP verwendet (Standardeinstellung = 0)|
|**Partitionsnummer**|**int**|Partitionsnummer im besitzenden Index oder Heap. Für nicht partitionierte Tabellen und Indizes oder im Fall werden alle Partitionen werden Neuerstellung der Wert dieser Spalte NULL ist.|
|**Status**|**tinyint**|Betriebsstatus für fortsetzbar Index:<br /><br />0 = wird ausgeführt<br /><br />1 = anhalten|
|**state_desc**|**nvarchar(60)**|Beschreibung des Betriebsstatus für fortsetzbar Index (ausgeführt oder angehalten)|  
|**start_time**|**datetime**|Index Operation-Startzeit (nicht NULL zulassen)|
|**last_pause_time**|**DateTime**| Indexvorgang anhalten zuletzt (NULL zulassen). NULL, wenn der Vorgang ausgeführt wird und nie angehalten wird.|
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
 [Katalogsichten &#40; Transact-SQL &#41; ](catalog-views-transact-sql.md) [Katalogsichten &#40; Objekt Transact-SQL &#41; ](object-catalog-views-transact-sql.md) [sys.indexes &#40; Transact-SQL &#41; ](sys-xml-indexes-transact-sql.md) [index_columns &#40; Transact-SQL &#41;](sys-index-columns-transact-sql.md)   
 [Sys. xml_indexes &#40; Transact-SQL &#41;](sys-xml-indexes-transact-sql.md)   
 [Sys.Objects &#40; Transact-SQL &#41;](sys-index-columns-transact-sql.md)   
 [Sys. key_constraints &#40; Transact-SQL &#41;](sys-key-constraints-transact-sql.md)   
 ["Sys.FileGroups" &#40; Transact-SQL &#41;](sys-filegroups-transact-sql.md)   
 [Sys. partition_schemes &#40; Transact-SQL &#41;](sys-partition-schemes-transact-sql.md)   
 [Häufig gestellte Fragen zu Abfragen des SQL Server-Systemkatalogs](querying-the-sql-server-system-catalog-faq.md)   
  

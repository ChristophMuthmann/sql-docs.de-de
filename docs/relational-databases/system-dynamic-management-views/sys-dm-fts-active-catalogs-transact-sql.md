---
title: Sys. dm_fts_active_catalogs (Transact-SQL) | Microsoft Docs
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
- sys.dm_fts_active_catalogs_TSQL
- dm_fts_active_catalogs
- dm_fts_active_catalogs_TSQL
- sys.dm_fts_active_catalogs
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_active_catalogs dynamic management view
ms.assetid: 40ab5453-040c-4d2e-bb49-e340cf90c3ee
caps.latest.revision: 38
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 8104491ddcdf6c63e872da7a70374f8475cb1a62
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmftsactivecatalogs-transact-sql"></a>sys.dm_fts_active_catalogs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt Informationen zu den Volltextkatalogen zurück, für die zurzeit Auffüllungsaktivitäten auf dem Server ausgeführt werden.  
  
> [!NOTE]  
>  Die folgenden Spalten werden in einer zukünftigen Version von entfernt [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: Is_paused, Previous_status, Previous_status_description, Row_count_in_thousands, Status, Status_description und Worker_count. Verwenden Sie diese Spalten in Neuentwicklungen nicht. Planen Sie die Änderung von Anwendungen, die diese Spalten derzeit verwenden.  
  
 
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|ID der Datenbank, die den aktiven Volltextkatalog enthält.|  
|**catalog_id**|**int**|ID des aktiven Volltextkatalogs.|  
|**memory_address**|**varbinary(8)**|Adresse von Speicherpuffern, die für Auffüllungsaktivitäten im Zusammenhang mit diesem Volltextkatalog zugeordnet wurden.|  
|**name**|**nvarchar(128)**|Name des aktiven Volltextkatalogs.|  
|**is_paused**|**bit**|Gibt an, ob das Auffüllen des aktiven Volltextkatalogs angehalten wurde.|  
|**status**|**int**|Aktueller Status des Volltextkatalogs. Einer der folgenden Typen:<br /><br /> 0 = Wird initialisiert<br /><br /> 1 = Bereit<br /><br /> 2 = Angehalten<br /><br /> 3 = Temporärer Fehler<br /><br /> 4 = Erneute Einbindung erforderlich<br /><br /> 5 = Herunterfahren<br /><br /> 6 = Übernehmen von Änderungen zu Sicherungszwecken<br /><br /> 7 = Sicherung erfolgt über Katalog<br /><br /> 8 = Katalog ist beschädigt|  
|**status_description**|**nvarchar(120)**|Beschreibung des aktuellen Status des aktiven Volltextkatalogs.|  
|**previous_status**|**int**|Vorhergehender Status des Volltextkatalogs. Einer der folgenden Typen:<br /><br /> 0 = Wird initialisiert<br /><br /> 1 = Bereit<br /><br /> 2 = Angehalten<br /><br /> 3 = Temporärer Fehler<br /><br /> 4 = Erneute Einbindung erforderlich<br /><br /> 5 = Herunterfahren<br /><br /> 6 = Übernehmen von Änderungen zu Sicherungszwecken<br /><br /> 7 = Sicherung erfolgt über Katalog<br /><br /> 8 = Katalog ist beschädigt|  
|**previous_status_description**|**nvarchar(120)**|Beschreibung des vorhergehenden Status des aktiven Volltextkatalogs.|  
|**worker_count**|**int**|Anzahl der zurzeit aktiven Arbeitsthreads für diesen Volltextkatalog.|  
|**active_fts_index_count**|**int**|Anzahl der Volltextindizes, die aufgefüllt werden.|  
|**auto_population_count**|**int**|Anzahl von Tabellen, bei denen dieser Volltextkatalog automatisch aufgefüllt wird.|  
|**manual_population_count**|**int**|Anzahl von Tabellen, bei denen das manuelle Auffüllen für diesen Volltextkatalog ausgeführt wird.|  
|**full_incremental_population_count**|**int**|Anzahl von Tabellen, bei denen der Volltextkatalog vollständig oder inkrementell aufgefüllt wird.|  
|**row_count_in_thousands**|**int**|Geschätzte Zeilenanzahl (in Tausenden) in allen Volltextindizes in diesem Volltextkatalog.|  
|**is_importing**|**bit**|Gibt an, ob der Volltextkatalog importiert wird:<br /><br /> 1 = Der Katalog wird importiert.<br /><br /> 2 = Der Katalog wird nicht importiert.|  
  
## <a name="remarks"></a>Hinweise  
 Die Spalte is_importing ist neu in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
## <a name="permissions"></a>Berechtigungen  

Auf [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], erfordert `VIEW SERVER STATE` Berechtigung.   
Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], erfordert die `VIEW DATABASE STATE` Berechtigung in der Datenbank.   
   
## <a name="physical-joins"></a>Physische Joins  
 ![Wesentliche Joins dieser dynamischen verwaltungssicht](../../relational-databases/system-dynamic-management-views/media/join-dm-fts-active-catalogs-1.gif "wesentliche Joins dieser dynamischen verwaltungssicht")  
  
## <a name="relationship-cardinalities"></a>Kardinalität der Beziehungen  
  
|Von|Aktion|Beziehung|  
|----------|--------|------------------|  
|dm_fts_active_catalogs.database_id|dm_fts_index_population.database_id|1:1|  
|dm_fts_active_catalogs.catalog_id|dm_fts_index_population.catalog_id|1:1|  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden Informationen zu den aktiven Volltextkatalogen in der aktuellen Datenbank zurückgegeben.  
  
```  
SELECT catalog.name, catalog.is_importing, catalog.auto_population_count,  
  OBJECT_NAME(population.table_id) AS table_name,  
  population.population_type_description, population.is_clustered_index_scan,  
  population.status_description, population.completion_type_description,  
  population.queued_population_type_description, population.start_time,  
  population.range_count   
FROM sys.dm_fts_active_catalogs catalog   
CROSS JOIN sys.dm_fts_index_population population   
WHERE catalog.database_id = population.database_id   
AND catalog.catalog_id = population.catalog_id   
AND catalog.database_id = (SELECT dbid FROM sys.sysdatabases WHERE name = DB_NAME());  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 
 [Volltextsuche und semantische Suche dynamische Verwaltungssichten und Funktionen &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)  
  
  

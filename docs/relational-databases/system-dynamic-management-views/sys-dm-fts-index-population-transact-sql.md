---
title: Sys. dm_fts_index_population (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/29/2017
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
- sys.dm_fts_index_population
- dm_fts_index_population
- sys.dm_fts_index_population_TSQL
- dm_fts_index_population_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_fts_index_population dynamic management view
ms.assetid: 82d1c102-efcc-4b60-9a5e-3eee299bcb2b
caps.latest.revision: "38"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 719da7d41ba34adcf7a3aa7ccc53a14217e657ff
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmftsindexpopulation-transact-sql"></a>sys.dm_fts_index_population (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt Informationen zu den aktuell ausgeführten Auffüllungen des Volltextindexes und semantischen Schlüsselausdrucks zurück, die gerade in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt werden.  
 
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|ID der Datenbank, die den aufzufüllenden Volltextindex enthält.|  
|**catalog_id**|**int**|ID des Volltextkatalogs, in dem dieser Volltextindex enthalten ist.|  
|**table_id**|**int**|ID der Tabelle, für die der Volltextindex aufgefüllt wird.|  
|**memory_address**|**varbinary(8)**|Speicheradresse der internen Datenstruktur, mit der ein aktiver Auffüllprozess dargestellt wird.|  
|**population_type**|**int**|Typ der Auffüllung. Einer der folgenden Typen:<br /><br /> 1 = Vollständiges Auffüllen<br /><br /> 2 = Inkrementelles, auf Timestamps basierendes Auffüllen<br /><br /> 3 = Manuelles Aktualisieren von Überarbeitungen<br /><br /> 4 = Aktualisieren von Überarbeitungen im Hintergrund.|  
|**population_type_description**|**nvarchar(120)**|Beschreibung des Auffüllungstyps.|  
|**is_clustered_index_scan**|**bit**|Gibt an, ob die Auffüllung einen Scanvorgang im gruppierten Index umfasst.|  
|**range_count**|**int**|Anzahl der Teilbereiche, in die diese Auffüllung parallelisiert wurde.|  
|**completed_range_count**|**int**|Anzahl der Bereiche, für die die Verarbeitung abgeschlossen ist.|  
|**outstanding_batch_count**|**int**|Aktuelle Anzahl ausstehender Batches für diese Auffüllung. Weitere Informationen finden Sie unter [dm_fts_outstanding_batches &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-fts-outstanding-batches-transact-sql.md).|  
|**status**|**int**|**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Status dieser Auffüllung. Hinweis: Einige Status sind vorübergehend. Einer der folgenden Typen:<br /><br /> 3 = Wird gestartet<br /><br /> 5 = Normal verarbeiten<br /><br /> 7 = Verarbeitung wurde angehalten<br /><br /> Dieser Status tritt zum Beispiel auf, wenn eine automatische Zusammenführung ausgeführt wird.<br /><br /> 11 = Auffüllen abgebrochen<br /><br /> 12 = Verarbeiten einer semantischen Ähnlichkeitsextraktion|  
|**status_description**|**nvarchar(120)**|Beschreibung des Status der Auffüllung.|  
|**COMPLETION_TYPE**|**int**|Status des Abschlusses dieser Auffüllung.|  
|**completion_type_description**|**nvarchar(120)**|Beschreibung des Abschlusstyps.|  
|**worker_count**|**int**|Dieser Wert ist immer 0.|  
|**queued_population_type**|**int**|Typ der Auffüllung, basierend auf Überarbeitungen, die ggf. nach der aktuellen Auffüllung folgt.|  
|**queued_population_type_description**|**nvarchar(120)**|Beschreibung der Auffüllung, die ggf. folgt. Wenn beispielsweise CHANGE TRACKING = AUTO und die erste vollständige Auffüllung durchgeführt wird, wird in dieser Spalte "Autom. Auffüllen" angezeigt.|  
|**start_time**|**datetime**|Zeit des Starts der Auffüllung.|  
|**incremental_timestamp**|**timestamp**|Stellt den Timestamp des Starts einer vollständigen Auffüllung dar. Für alle anderen Auffüllungstypen ist dieser Wert der letzte Prüfpunkt, für den ein Commit ausgeführt wurde, der den Fortschritt der Auffüllung darstellt.|  
  
## <a name="remarks"></a>Hinweise  
 Wenn die statistische semantische Indizierung zusätzlich zur Volltextindizierung aktiviert ist, erfolgen die semantischen Extraktion und Auffüllung von Schlüsselausdrücken sowie die Extraktion von Dokumentähnlichkeitsdaten gleichzeitig mit der Volltextindizierung. Die Auffüllung des Dokumentähnlichkeitsindexes erfolgt später in einer zweiten Phase. Weitere Informationen finden Sie unter [verwalten und Überwachen der semantischen Suche](../../relational-databases/search/manage-and-monitor-semantic-search.md).  
  
## <a name="permissions"></a>Berechtigungen  
Auf [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], erfordert `VIEW SERVER STATE` Berechtigung.   
Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] benötigen Premium-Ebenen der `VIEW DATABASE STATE` Berechtigung in der Datenbank. Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard und grundlegenden Organisationsebenen erfordert die **Serveradministrator** oder ein **Azure Active Directory-Administrators** Konto.  
 
## <a name="physical-joins"></a>Physische Joins  
 ![Wesentliche Joins dieser dynamischen verwaltungssicht](../../relational-databases/system-dynamic-management-views/media/join-dm-fts-index-population-1.gif "wesentliche Joins dieser dynamischen verwaltungssicht")  
  
## <a name="relationship-cardinalities"></a>Kardinalität der Beziehungen  
  
|Von|Aktion|Beziehung|  
|----------|--------|------------------|  
|dm_fts_active_catalogs.database_id|dm_fts_index_population.database_id|1:1|  
|dm_fts_active_catalogs.catalog_id|dm_fts_index_population.catalog_id|1:1|  
|dm_fts_population_ranges.parent_memory_address|dm_fts_index_population.memory_address|n:1|  
  
## <a name="see-also"></a>Siehe auch  
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Volltextsuche und semantische Suche dynamische Verwaltungssichten und Funktionen &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)  
  
  


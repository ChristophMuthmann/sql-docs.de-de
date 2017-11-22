---
title: Sys. dm_fts_memory_buffers (Transact-SQL) | Microsoft Docs
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
- sys.dm_fts_memory_buffers
- dm_fts_memory_buffers_TSQL
- dm_fts_memory_buffers
- sys.dm_fts_memory_buffers_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_fts_memory_buffers dynamic management view
ms.assetid: 56895fe5-e8df-4d75-9adc-c1f7757cdef8
caps.latest.revision: "33"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3708d5c98e8869e0a1d1a68fe2bc2df3376bcadf
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmftsmemorybuffers-transact-sql"></a>sys.dm_fts_memory_buffers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt Informationen zu Speicherpuffern zurück, die einem bestimmten Speicherpool angehören, der im Rahmen einer Volltextdurchforstung oder eines Volltext-Durchforstungsbereichs verwendet wird.  
  
> [!NOTE]
> Die folgende Spalte wird in einer zukünftigen Version von entfernt [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **Row_count**. Vermeiden Sie diese Spalte bei Neuentwicklungen, und planen Sie die Änderung von Anwendungen, in denen die Spalte derzeit verwendet wird.  

  
|Column|Datentyp|Description|  
|------------|---------------|-----------------|  
|**pool_id**|**int**|ID des belegten Speicherpools.<br /><br /> 0 = Kleine Puffer<br /><br /> 1 = Große Puffer|  
|**memory_address**|**varbinary(8)**|Adresse des belegten Speicherpuffers.|  
|**name**|**nvarchar(4000)**|Name des freigegebenen Speicherpuffers, für den die Zuordnung erstellt wurde.|  
|**is_free**|**bit**|Aktueller Status des Speicherpuffers.<br /><br /> 0 = Frei<br /><br /> 1 = Belegt|  
|**row_count**|**int**|Anzahl von Zeilen, die dieser Puffer zurzeit bearbeitet.|  
|**bytes_used**|**int**|Umfang des zurzeit im Puffer belegten Speichers (in Bytes).|  
|**percent_used**|**int**|Prozentsatz des verwendeten belegten Arbeitsspeichers.|  
  
## <a name="permissions"></a>Berechtigungen  
Auf [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], erfordert `VIEW SERVER STATE` Berechtigung.   
Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] benötigen Premium-Ebenen der `VIEW DATABASE STATE` Berechtigung in der Datenbank. Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard und grundlegenden Organisationsebenen erfordert die **Serveradministrator** oder ein **Azure Active Directory-Administrators** Konto.  
 
## <a name="physical-joins"></a>Physische Joins  
 ![Wesentliche Joins dieser dynamischen verwaltungssicht](../../relational-databases/system-dynamic-management-views/media/join-dm-fts-memory-buffers-1.gif "wesentliche Joins dieser dynamischen verwaltungssicht")  
  
## <a name="relationship-cardinalities"></a>Kardinalität der Beziehungen  
  
|Von|Aktion|Beziehung|  
|----------|--------|------------------|  
|dm_fts_memory_buffers.pool_id|dm_fts_memory_pools.pool_id|n:1|  
  
## <a name="see-also"></a>Siehe auch  
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Volltextsuche und semantische Suche dynamische Verwaltungssichten und Funktionen &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)  
  
  


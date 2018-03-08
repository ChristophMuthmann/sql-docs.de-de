---
title: dm_fts_memory_pools (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/29/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_fts_memory_pools_TSQL
- sys.dm_fts_memory_pools_TSQL
- sys.dm_fts_memory_pools
- dm_fts_memory_pools
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_memory_pools dynamic management view
ms.assetid: 24747239-cd78-4d55-a00a-19233a457f42
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 02b742ae19835ef9167351bac9db6f53cfb5b08d
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmftsmemorypools-transact-sql"></a>sys.dm_fts_memory_pools (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt Informationen zu den Shared Memory-Pools zurück, die für die Volltext-Gatherer-Komponente für einen Volltext-Durchforstungsvorgang oder einen Volltext-Durchforstungsbereich zur Verfügung stehen.  
   
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**pool_id**|**int**|ID des belegten Speicherpools.<br /><br /> 0 = Kleine Puffer<br /><br /> 1 = Große Puffer|  
|**buffer_size**|**int**|Größe der einzelnen zugeordneten Puffer im Speicherpool.|  
|**min_buffer_limit**|**int**|Mindestzahl der zulässigen Puffer im Speicherpool.|  
|**max_buffer_limit**|**int**|Höchstzahl der zulässigen Puffer im Speicherpool.|  
|**buffer_count**|**int**|Derzeitige Anzahl der auf dem freigegebenen Speicherbereich basierenden Puffer im Speicherpool.|  
  
## <a name="permissions"></a>Berechtigungen  
Auf [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], erfordert `VIEW SERVER STATE` Berechtigung.   
Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] benötigen Premium-Ebenen der `VIEW DATABASE STATE` Berechtigung in der Datenbank. Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard und grundlegenden Organisationsebenen erfordert die **Serveradministrator** oder ein **Azure Active Directory-Administrators** Konto.  

## <a name="physical-joins"></a>Physische Joins  
 ![Wesentliche Joins dieser dynamischen verwaltungssicht](../../relational-databases/system-dynamic-management-views/media/join-dm-fts-memory-pools-1.gif "wesentliche Joins dieser dynamischen verwaltungssicht")  
  
## <a name="relationship-cardinalities"></a>Kardinalität der Beziehungen  
  
|Von|Aktion|Beziehung|  
|----------|--------|------------------|  
|dm_fts_memory_buffers.pool_id|dm_fts_memory_pools.pool_id|n:1|  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird das gesamte Shared Memory zurückgegeben, das von der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Volltext-Gatherer-Komponente des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Prozesses verwendet wird.  
  
```  
SELECT SUM(buffer_size * buffer_count) AS "total memory"   
    FROM sys.dm_fts_memory_pools;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Volltextsuche und semantische Suche dynamische Verwaltungssichten und Funktionen &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)  
  
  

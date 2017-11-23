---
title: dm_repl_tranhash (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_repl_tranhash
- sys.dm_repl_tranhash_TSQL
- dm_repl_tranhash_TSQL
- dm_repl_tranhash
dev_langs: TSQL
helpviewer_keywords: sys.dm_repl_tranhash dynamic management view
ms.assetid: 0cc52338-e805-4ed4-9835-b19bbf72448e
caps.latest.revision: "13"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 40d5bdff43e1022e62f20092b8b3d8dff1928231
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmrepltranhash-transact-sql"></a>sys.dm_repl_tranhash (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt Informationen zu Transaktionen zurück, die in einer Transaktionsveröffentlichung repliziert werden.  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
|column_name|data_type|Beschreibung|  
|------------------|----------------|-----------------|  
|**Buckets**|**bigint**|Die Anzahl der Buckets in der Hashtabelle.|  
|**hashed_trans**|**bigint**|Anzahl der im aktuellen Batch replizierten Transaktionen, für die ein Commit durchgeführt wurde.|  
|**completed_trans**|**bigint**|Anzahl der bisher abgeschlossenen Transaktionen.|  
|**compensated_trans**|**bigint**|Anzahl der Transaktionen, die teilweise Rollbacks enthalten.|  
|**first_begin_lsn**|**nvarchar(64)**|Erste Protokollfolgenummer (LSN, Log Sequence Number) im aktuellen Batch.|  
|**last_commit_lsn**|**nvarchar(64)**|LSN des letzten Commits im aktuellen Batch.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW DATABASE STATE-Berechtigung für die Veröffentlichungsdatenbank, die **dm_repl_tranhash**aufruft.  
  
## <a name="remarks"></a>Hinweise  
 Informationen werden nur für replizierte Datenbankobjekte zurückgegeben, die zurzeit in den Replikationsartikelcache geladen sind.  
  
## <a name="see-also"></a>Siehe auch  
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Mit der Replikation verbundene dynamische Verwaltungssichten &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/replication-related-dynamic-management-views-transact-sql.md)  
  
  

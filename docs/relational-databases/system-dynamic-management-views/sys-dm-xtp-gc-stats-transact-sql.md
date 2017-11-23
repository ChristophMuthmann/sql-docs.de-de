---
title: dm_xtp_gc_stats (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
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
- dm_xtp_gc_stats
- dm_xtp_gc_stats_TSQL
- sys.dm_xtp_gc_stats_TSQL
- sys.dm_xtp_gc_stats
dev_langs: TSQL
helpviewer_keywords: sys.dm_xtp_gc_stats dynamic management view
ms.assetid: 8287d611-50e3-43e1-ba8d-3e3793d3ba0e
caps.latest.revision: "20"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0a690854a31bb01d3b998ae70b8f682750416b72
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmxtpgcstats-transact-sql"></a>sys.dm_xtp_gc_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  Enthält Informationen (Gesamtstatistiken) über das aktuelle Verhalten der [!INCLUDE[hek_2](../../includes/hek-2-md.md)] Garbage Collection-Prozesses.  
  
 Zeilen werden im Rahmen der regulären Transaktionsverarbeitung von der Garbage Collection oder vom Garbage Collection-Hauptthread bereinigt, der als Leerlaufthread bezeichnet wird. Wenn eine Benutzertransaktion ein Commit ausgeführt wird, entfernt Sie eine Arbeitsaufgabe aus der Warteschlange der Garbage Collection ([Sys. dm_xtp_gc_queue_stats &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-xtp-gc-queue-stats-transact-sql.md)). Alle Zeilen, die durch die Garbage Collection bereinigt werden konnten, auf die jedoch nicht durch die Hauptbenutzertransaktion zugegriffen wurde, werden im Rahmen des Dusty-Corner-Scans (einem Scan der Indexbereiche, auf die seltener zugegriffen wird) durch den Leerlaufthread bereinigt.  
  
 Weitere Informationen finden Sie unter [In-Memory OLTP &#40;Arbeitsspeicheroptimierung&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
|Spaltenname|Typ|Beschreibung|  
|-----------------|----------|-----------------|  
|rows_examined|**bigint**|Die Anzahl der Zeilen, die vom Subsystem der Garbage Collection überprüft werden, nachdem der Server gestartet wurde.|  
|rows_no_sweep_needed|**bigint**|Die Anzahl der Zeilen, die ohne Dusty-Corner-Scan entfernt wurden.|  
|rows_first_in_bucket|**bigint**|Die Anzahl der Zeilen, die von der Garbage Collection überprüft wurden und die die erste Zeile im Hashbucket waren.|  
|rows_first_in_bucket_removed|**bigint**|Die Anzahl der Zeilen, die von der Garbage Collection überprüft wurden und die als erste Zeile im Hashbucket entfernt wurden.|  
|rows_marked_for_unlink|**bigint**|Die Anzahl der Zeilen, die von der Garbage Collection überprüft wurden und in ihren Indizes mit ref count=0 bereits als nicht mehr verknüpft markiert sind.|  
|parallel_assist_count|**bigint**|Die Anzahl der Zeilen, die durch Benutzertransaktionen verarbeitet wurden.|  
|idle_worker_count|**bigint**|Die Anzahl der Garbage-Zeilen, die durch den Leerlaufthread verarbeitet wurden.|  
|sweep_scans_started|**bigint**|Die Anzahl der durch das Garbage Collection-Subsystem ausgeführten Dusty-Corner-Scans.|  
|sweep_scans_retries|**bigint**|Die Anzahl der durch das Garbage Collection-Subsystem ausgeführten Dusty-Corner-Scans.|  
|sweep_rows_touched|**bigint**|Die durch die Dusty-Corner-Verarbeitung gelesenen Zeilen.|  
|sweep_rows_expiring|**bigint**|Die durch die Dusty-Corner-Verarbeitung gelesenen ablaufenden Zeilen.|  
|sweep_rows_expired|**bigint**|Die durch die Dusty-Corner-Verarbeitung gelesenen abgelaufenen Zeilen.|  
|sweep_rows_expired_removed|**bigint**|Die durch die Dusty-Corner-Verarbeitung entfernten abgelaufenen Zeilen.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW SERVER STATE-Berechtigung für die Instanz.  
  
## <a name="usage-scenario"></a>Verwendungsszenario  
 Im Folgenden eine Beispielausgabe:  
  
```  
rows_examined        rows_no_sweep_needed rows_first_in_bucket rows_first_in_bucket_removed  
280085               209512               69905  
rows_first_in_bucket_removed rows_marked_for_unlink parallel_assist_count idle_worker_count  
69905                        0                      8953  
  
idle_worker_count    sweep_scans_started  sweep_scan_retries   sweep_rows_touched  
10306473             670                  0                    1343  
  
sweep_rows_expiring  sweep_rows_expired   sweep_rows_expired_removed  
               0                 673673  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Dynamische Verwaltungssichten für Speicheroptimierte Tabelle &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  

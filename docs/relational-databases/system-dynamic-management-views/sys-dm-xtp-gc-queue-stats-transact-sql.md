---
title: Sys. dm_xtp_gc_queue_stats (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/02/2016
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
ms.assetid: addef774-318d-46a7-85df-f93168a800cb
caps.latest.revision: "18"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1f5af0d350c90067c75a8f26d2fbf429d018acff
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmxtpgcqueuestats-transact-sql"></a>sys.dm_xtp_gc_queue_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  Gibt Informationen über jede Garbage Collection-Arbeitsthreadwarteschlange auf dem Server sowie verschiedene Statistiken zu diesen Warteschlangen aus. Pro logische CPU ist eine Warteschlange vorhanden.  
  
 Der Garbage Collection-Hauptthread (Leerlaufthread) verfolgt aktualisierte, gelöschte und eingefügte Zeilen für alle Transaktionen nach, die seit dem letzten Aufruf des Garbage Collection-Hauptthreads abgeschlossen wurden. Sobald er aktiviert wird, überprüft der Garbage Collection-Thread, ob der Zeitstempel der ältesten aktiven Transaktion geändert wurde. Wenn die älteste aktive Transaktion geändert wurde, reiht der Leerlaufthread Arbeitsaufgaben für Transaktionen, deren Schreibmengen nicht mehr benötigt werden, (in Segmenten von 16 Zeilen) in die Warteschlange ein. Wenn Sie z. B. 1.024 Zeilen löschen, enthält die Warteschlange schließlich 64 Garbage Collection-Arbeitsaufgaben mit jeweils 16 gelöschten Zeilen.  Nachdem für eine Benutzertransaktion ein Commit ausgeführt wurde, werden alle im zugehörigen Zeitplanungsmodul in die Warteschlange eingereihten Arbeitsaufgaben ausgewählt. Wenn die Warteschlange im Zeitplanungsmodul keine Arbeitsaufgaben enthält, werden von der Benutzertransaktion alle Warteschlangen im aktuellen NUMA-Knoten durchsucht.  
  
 Sie können feststellen, ob Arbeitsspeicher für gelöschte Zeilen durch die Garbage Collection freigegeben wird, indem Sie sys.dm_xtp_gc_queue_stats ausführen und überprüfen, ob die Arbeitsaufgaben in der Warteschlange verarbeitet werden. Wenn Sie Einträge in Current_queue_depth nicht verarbeitet werden, oder wenn Current_queue_depth keine neue Arbeitsaufgaben hinzugefügt werden, ist dies ein Hinweis, dass die Garbagecollection keinen Arbeitsspeicher freigibt. Beispielsweise wird die Garbage Collection durch eine Transaktion mit langer Ausführungszeit verhindert.  
  
 Weitere Informationen finden Sie unter [In-Memory OLTP &#40;Arbeitsspeicheroptimierung&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  

|Spaltenname|Typ|Description|  
|-----------------|----------|-----------------|  
|queue_id|**int**|Der eindeutige Bezeichner der Warteschlange.|  
|total_enqueues|**bigint**|Die Gesamtanzahl von Arbeitselementen der Garbage Collection, die seit dem Start des Servers in die Warteschlange eingereiht wurden.|  
|total_dequeues|**bigint**|Die Gesamtanzahl von Arbeitselementen der Garbage Collection, die seit dem Start des Servers aus der Warteschlange entfernt wurden.|  
|current_queue_depth|**bigint**|Die aktuelle Anzahl von Arbeitselementen der Garbage Collection, die in dieser Warteschlange vorhanden sind. Dieses Element bedeutet möglicherweise, dass eine oder mehrere Garbage Collections durchgeführt werden sollen.|  
|maximum_queue_depth|**bigint**|Die maximale Tiefe, die diese Warteschlange aufgewiesen hat.|  
|last_service_ticks|**bigint**|CPU-Takte zu dem Zeitpunkt, als die Warteschlange zuletzt aktiv war.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW SERVER STATE-Berechtigung.  
  
## <a name="user-scenario"></a>Benutzerszenario  
 Diese Ausgabe veranschaulicht, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entweder auf vier Kernen ausgeführt wird oder dass die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz vier Kernen zugeordnet wurde:  
  
 Diese Ausgabe veranschaulicht, dass in den Warteschlangen keine zu verarbeitenden Arbeitsaufgaben enthalten sind. Für Warteschlange 0 wurden seit dem SQL-Start insgesamt 15.625 Arbeitsaufgaben aus der Warteschlange entfernt, und die maximale Warteschlangentiefe betrug 215.625.  
  
```  
queue_id total_enqueues total_dequeues current_queue_depth  maximum_queue_depth  last_service_ticks  
----------------------------------------------------------------------------------------------------  
0        15625                15625    0                    15625                1233573168347  
1        15625                15625    0                    15625                1234123295566  
2        15625                15625    0                    15625                1233569418146  
3        15625                15625    0                    15625                1233571605761  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Dynamische Verwaltungssichten für Speicheroptimierte Tabelle &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  

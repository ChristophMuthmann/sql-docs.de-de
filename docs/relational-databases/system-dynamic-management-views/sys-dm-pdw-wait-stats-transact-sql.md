---
title: Sys.dm_pdw_wait_stats (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: 
ms.service: sql-data-warehouse
ms.component: dmv's
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: cfb8d905-c34f-44de-9574-dde81e170916
caps.latest.revision: "7"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c2a567c103a0a2b3f3dac24accd8099d2bd85e80
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmpdwwaitstats-transact-sql"></a>Sys.dm_pdw_wait_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Enthält Informationen, die im Zusammenhang mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OS-Status im Zusammenhang mit Instanzen, die auf verschiedenen Knoten ausgeführt. Eine Liste der Wartevorgänge Typen und deren Beschreibung, finden Sie unter [dm_os_wait_stats](http://msdn.microsoft.com/en-us/library/ms179984\(v=sql.120\).aspx).  
  
|Spaltenname|Datentyp|Description|Bereich|  
|-----------------|---------------|-----------------|-----------|  
|**pdw_node_id**|**int**|Die ID des Knotens, auf das dieser Eintrag verweist.||  
|**wait_name**|**nvarchar(255)**|Name des Wartetyps.||  
|**max_wait_time**|**bigint**|Maximale Wartezeit für diesen Wartetyp.||  
|**request_count**|**bigint**|Anzahl von Wartevorgängen Dieser Wartetyp ausstehen.||  
|**signal_time**|**bigint**|Differenz zwischen dem Zeitpunkt der Signalisierung des wartenden Threads und dem Beginn der Ausführung.||  
|**completed_count**|**bigint**|Gesamtanzahl von Wartevorgängen dieses Typs, die seit dem letzten Serverneustart abgeschlossen Neustart.||  
|**Wartezeit**|**bigint**|Gesamtwartezeit für diesen Wartetyp in Millisecons. Inklusive der Signal_time.||  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Datawarehouse und dynamische Verwaltungssichten für Parallel Datawarehouse &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)   
 [Sys.dm_pdw_waits &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md)  
  
  

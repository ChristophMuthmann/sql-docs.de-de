---
title: Sys.dm_pdw_wait_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.service: sql-data-warehouse
ms.component: dmv's
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: cfb8d905-c34f-44de-9574-dde81e170916
caps.latest.revision: 7
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: b038e289f515f196171c5fcbbad9e96d9c0fc26d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
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
|**wait_time**|**bigint**|Gesamtwartezeit für diesen Wartetyp in Millisecons. Inklusive der Signal_time.||  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Datawarehouse und Parallel Data Warehouse-dynamische Verwaltungssichten &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)   
 [sys.dm_pdw_waits &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md)  
  
  

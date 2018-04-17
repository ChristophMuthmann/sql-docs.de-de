---
title: Sys.dm_pdw_node_status (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: pdw
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 8e263b65-81d0-49d0-8873-62ef424369d6
caps.latest.revision: 7
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 2ff2f23fcfc6314d06f55bca2b918d954f43514e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmpdwnodestatus-transact-sql"></a>Sys.dm_pdw_node_status (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Enthält zusätzliche Informationen (über [sys.dm_pdw_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)) über die Leistung und Status aller Appliance-Knoten. Sie enthält eine Zeile pro Knoten in der Einheit.  
  
|Spaltenname|Datentyp|Description|Bereich|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|Eindeutige numerische Id, die dem Knoten zugeordnet.<br /><br /> Der Schlüssel für diese Ansicht.|Für die Appliance, unabhängig vom Typ eindeutig.|  
|process_id|**int**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|process_name|**nvarchar(255)**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|allocated_memory|**bigint**|Insgesamt zugeordneter Arbeitsspeicher auf diesem Knoten.||  
|available_memory|**bigint**|Insgesamt verfügbare Arbeitsspeicher auf diesem Knoten.||  
|process_cpu_usage|**bigint**|Insgesamt Prozess CPU-Auslastung in Ticks.||  
|total_cpu_usage|**bigint**|Gesamter CPU-Auslastung in Ticks.||  
|Thread_Count|**bigint**|Gesamtanzahl der Threads auf diesem Knoten verwendet.||  
|handle_count|**bigint**|Die Gesamtanzahl der Handles auf diesem Knoten verwendet.||  
|total_elapsed_time|**bigint**|Insgesamt verstrichene Zeit seit System gestartet oder neu gestartet.|Insgesamt verstrichene Zeit seit System gestartet oder neu gestartet. Wenn Total_elapsed_time den maximalen Wert für eine ganze Zahl (24.8 Tage in Millisekunden) überschreitet, führt es Materialisierung Fehler aufgrund einer dazu, dass "Überlauf".<br /><br /> Der maximale Wert in Millisekunden entspricht 24.8 Tage.|  
|is_available|**bit**|Ein Flag, der angibt, ob dieser Knoten verfügbar ist.||  
|sent_time|**datetime**|Zuletzt ein Netzwerk-Paket wurde von diesem Knoten gesendet werden.||  
|received_time|**datetime**|Zuletzt ein Netzwerk-Paket wurde von diesem Knoten empfangen werden.||  
|error_id|**nvarchar(36)**|Eindeutiger Bezeichner des letzten Fehlers, der auf diesem Knoten aufgetreten ist.||  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Datawarehouse und Parallel Data Warehouse-dynamische Verwaltungssichten &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  

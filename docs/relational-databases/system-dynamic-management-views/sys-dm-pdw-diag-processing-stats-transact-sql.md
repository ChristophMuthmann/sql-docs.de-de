---
title: Sys.dm_pdw_diag_processing_stats (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: df659c55-4f63-45f8-8afe-ce300031bc5b
caps.latest.revision: "7"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 05dc9dc5854b970dd97227672f5f75eecbb34718
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmpdwdiagprocessingstats-transact-sql"></a>Sys.dm_pdw_diag_processing_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Zeigt Informationen im Zusammenhang mit der alle internen Diagnoseereignisse, die vom Administrator definierte diagnosesitzungen integriert werden konnte. Abfrageansicht Sie folgendermaßen vor, um den Statistiken hinter die Diagnose- und Ereignisse Subsysteme dieses Laufwerk die Auffüllung für die anderen DMVs zu verstehen. Es gibt eine Gruppe von Warteschlangen für jeden Prozess auf jedem Knoten aus.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**pdw_node_id**|**int**|Appliance-Knoten, die dieses Protokoll stammt.|  
|**process_id**|**int**|Der Bezeichner des Prozesses ausgeführt wird, senden diese Statistik.|  
|**Zielname**|**nvarchar(255)**|Der Name der Warteschlange.|  
|**queue_size**|**int**|Die Anzahl der Elemente in der Verarbeitungswarteschlange. Die Warteschlangengröße ist in der Regel 0. Eine positive Zahl bedeutet, dass das System ist unter Belastung ist erstellen Rückstands von Ereignissen. Eine positive Anzahl in den anderen Spalten bedeutet System für diese bestimmte Warteschlange beschädigt wurde und alle zugehörigen DMVs.|  
|**lost_events_count**|**bigint**|Die Anzahl verloren gegangener Ereignisse.|  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Datawarehouse und dynamische Verwaltungssichten für Parallel Datawarehouse &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  

---
title: Sys.dm_pdw_sys_info (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 686976b4-2d5d-4d64-bf12-56eba1dc59b1
caps.latest.revision: 7
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 750579342ab5a59115fe2aa2dd3d78d151a6f44c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmpdwsysinfo-transact-sql"></a>sys.dm_pdw_sys_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Stellt einen Satz von Indikatoren Appliance-Ebene, die Gesamtaktivität auf dem Gerät widerspiegeln.  
  
|Spaltenname|Datentyp|Description|Bereich|  
|-----------------|---------------|-----------------|-----------|  
|total_sessions|**int**|Anzahl der Sitzungen, die zurzeit im System.|0 bis Max_active_sessions (siehe unten).|  
|idle_sessions|**int**|Anzahl der Sitzungen, die derzeit im Leerlauf.||  
|active_requests|**int**|Die Anzahl der aktiven Anforderungen, die zurzeit ausgeführt.||  
|queued_requests|**int**|Anzahl der Anforderungen derzeit in der Warteschlange.||  
|active_loads|**int**|Anzahl der Lasten, die zurzeit im System ausgeführt werden.||  
|queued_loads|**int**|Die Anzahl der in der Warteschlange Lasten, die Ausführung warten.||  
|active_backups|**int**|Die Anzahl von Sicherungen, die zurzeit ausgeführt.||  
|active_restores|**int**|Anzahl der Sicherung wiederhergestellt, die zurzeit ausgeführt.||  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Datawarehouse und Parallel Data Warehouse-dynamische Verwaltungssichten &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  

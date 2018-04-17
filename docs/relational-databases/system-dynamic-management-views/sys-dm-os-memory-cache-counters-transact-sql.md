---
title: Sys. dm_os_memory_cache_counters (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_os_memory_cache_counters_TSQL
- dm_os_memory_cache_counters_TSQL
- sys.dm_os_memory_cache_counters
- dm_os_memory_cache_counters
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_cache_counters dynamic management view
ms.assetid: ca7bd036-d661-4c17-b00a-e1a975bd8932
caps.latest.revision: 36
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d16da7e5bbc38b7017da1f94741d4c4955e3485d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmosmemorycachecounters-transact-sql"></a>sys.dm_os_memory_cache_counters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt eine Momentaufnahme des Zustands eines Caches in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zurück. **Sys. dm_os_memory_cache_counters** stellt Laufzeitinformationen zu den zugeordneten Cacheeinträgen, deren Verwendung und die Quelle des Arbeitsspeichers für die Cacheeinträge bereit.  
  
> **Hinweis:** von Aufrufen [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] oder [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], verwenden Sie den Namen **sys.dm_pdw_nodes_os_memory_cache_counters**.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**cache_address**|**varbinary(8)**|Gibt die Adresse (Primärschlüssel) der Leistungsindikatoren an, die einem bestimmten Cache zugeordnet sind. Lässt keine NULL-Werte zu.|  
|**name**|**nvarchar(256)**|Gibt den Namen des Caches an. Lässt keine NULL-Werte zu.|  
|**type**|**nvarchar(60)**|Gibt den Typ des Caches an, der diesem Eintrag zugeordnet ist. Lässt keine NULL-Werte zu.|  
|**single_pages_kb**|**bigint**|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].<br /><br /> Der Umfang (in KB) des zugeordneten Einzelseiten-Arbeitsspeichers. Hierbei handelt es sich um den Arbeitsspeicher, der mithilfe der Einzelseitenzuordnung zugeordnet wird. Dies bezieht sich auf die 8-KB-Seiten, die direkt aus dem Pufferpool für diesen Cache verwendet werden. Lässt keine NULL-Werte zu.|  
|**pages_kb**|**bigint**|**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Gibt die dem Cache zugeordnete Arbeitsspeichermenge in Kilobyte an. Lässt keine NULL-Werte zu.|  
|**multi_pages_kb**|**bigint**|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].<br /><br /> Der Umfang (in KB) des zugeordneten mehrseitigen Arbeitsspeichers. Hierbei handelt es sich um den Arbeitsspeicher, der mithilfe der Zuordnung für mehrere Seiten des Arbeitsspeicherknotens zugeordnet wird. Dieser Arbeitsspeicher wird außerhalb des Pufferpools zugeordnet und nutzt die virtuelle Zuordnung der Arbeitsspeicherknoten. Lässt keine NULL-Werte zu.|  
|**pages_in_use_kb**|**bigint**|**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Gibt die dem Cache zugeordnete und vom Cache verwendete Arbeitsspeichermenge in Kilobyte an. Lässt NULL-Werte zu.  Werte für Objekte vom Typ `USERSTORE_<*>` werden nicht nachverfolgt.  NULL wird gemeldet.|  
|**single_pages_in_use_kb**|**bigint**|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].<br /><br /> Der Umfang (in KB) des verwendeten Einzelseiten-Arbeitsspeichers. Lässt NULL-Werte zu. Diese Informationen werden für Objekte vom Typ USERSTORE_ nicht nachverfolgt\<* >, und diese Werte werden auf NULL.|  
|**multi_pages_in_use_kb**|**bigint**|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].<br /><br /> Der Umfang (in Kilobytes) des verwendeten mehrseitigen Arbeitsspeichers. Lässt NULL-Werte zu. Diese Informationen werden für Objekte vom Typ USERSTORE_ nicht nachverfolgt\<* >, und diese Werte werden auf NULL.|  
|**entries_count**|**bigint**|Gibt die Anzahl der Einträge im Cache an. Lässt keine NULL-Werte zu.|  
|**entries_in_use_count**|**bigint**|Gibt die Anzahl der Einträge im Cache an, der verwendet wird. Lässt keine NULL-Werte zu.|  
|**pdw_node_id**|**int**|**Gilt für**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Der Bezeichner für den Knoten, dem auf diesem Verteilungspunkt befindet.|  
  
## <a name="permissions"></a>Berechtigungen 

Auf [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], erfordert `VIEW SERVER STATE` Berechtigung.   
Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], erfordert die `VIEW DATABASE STATE` Berechtigung in der Datenbank.   

## <a name="see-also"></a>Siehe auch  
  [SQL Server-Betriebssystem verbundene dynamische Verwaltungssichten &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  



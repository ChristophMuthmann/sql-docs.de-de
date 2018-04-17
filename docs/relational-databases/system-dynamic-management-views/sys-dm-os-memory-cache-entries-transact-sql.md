---
title: Sys. dm_os_memory_cache_entries (Transact-SQL) | Microsoft Docs
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
- dm_os_memory_cache_entries
- sys.dm_os_memory_cache_entries
- dm_os_memory_cache_entries_TSQL
- sys.dm_os_memory_cache_entries_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_cache_entries dynamic management view
ms.assetid: dd32be6b-10d1-4059-b4fd-0bf817f40d54
caps.latest.revision: 39
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a69088658cf9e76ac52c882872ef0e1eed6500b9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmosmemorycacheentries-transact-sql"></a>sys.dm_os_memory_cache_entries (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt Informationen zu allen Einträgen in Caches in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zurück. Verwenden Sie diese Sicht, um Cacheeinträge für die zugehörigen Objekte nachzuverfolgen. Mit dieser Sicht können Sie auch Statistiken zu Cacheeinträgen abrufen.  
  
> [!NOTE]  
>  Aufrufen von [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] oder [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], verwenden Sie den Namen **sys.dm_pdw_nodes_os_memory_cache_entries**.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**cache_address**|**varbinary(8)**|Adresse des Caches. Lässt keine NULL-Werte zu.|  
|**name**|**nvarchar(256)**|Name des Caches. Lässt keine NULL-Werte zu.|  
|**type**|**varchar(60)**|Typ des Caches. Lässt keine NULL-Werte zu.|  
|**entry_address**|**varbinary(8)**|Adresse des Deskriptors des Cacheeintrags. Lässt keine NULL-Werte zu.|  
|**entry_data_address**|**varbinary(8)**|Adresse der Benutzerdaten im Cacheeintrag.<br /><br /> 0x00000000 = Eintragsdatenadresse ist nicht verfügbar.<br /><br /> Lässt keine NULL-Werte zu.|  
|**in_use_count**|**int**|Anzahl gleichzeitiger Benutzer dieses Cacheeintrags. Lässt keine NULL-Werte zu.|  
|**is_dirty**|**bit**|Gibt an, ob dieser Cacheeintrag zum Löschen ausgewählt wurde. 1 = zum Löschen ausgewählt. Lässt keine NULL-Werte zu.|  
|**disk_ios_count**|**int**|Anzahl von E/A-Vorgängen aufgrund der Erstellung dieses Eintrags. Lässt keine NULL-Werte zu.|  
|**context_switches_count**|**int**|Anzahl der Kontextwechseln aufgrund der Erstellung dieses Eintrags. Lässt keine NULL-Werte zu.|  
|**original_cost**|**int**|Ursprüngliche Kosten des Eintrags. Dieser Wert entspricht der ungefähren Anzahl von E/A-Vorgängen, den ungefähren CPU-Anweisungskosten sowie dem ungefähr vom Eintrag belegten Speicher. Je höher die Kosten, desto niedriger ist die Chance, dass das Element aus dem Cache entfernt wird. Lässt keine NULL-Werte zu.|  
|**current_cost**|**int**|Aktuelle Kosten des Cacheeintrags. Dieser Wert wird beim Löschen von Einträgen aktualisiert. Die aktuellen Kosten werden auf den ursprünglichen Wert zurückgesetzt, wenn der Eintrag wiederverwendet wird. Lässt keine NULL-Werte zu.|  
|**memory_object_address**|**varbinary(8)**|Adresse des zugeordneten Arbeitsspeicherobjekts. Lässt NULL-Werte zu.|  
|**pages_allocated_count**|**bigint**|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].<br /><br /> Anzahl von 8-KB-Seiten zum Speichern dieses Cacheeintrags. Lässt keine NULL-Werte zu.|  
|**pages_kb**|**bigint**|**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Der Arbeitsspeicher, der von diesem Cacheeintrag verwendet wird, in Kilobyte (KB).  Lässt keine NULL-Werte zu.|  
|**entry_data**|**nvarchar(2048)**|Serialisierte Darstellung des zwischengespeicherten Eintrags. Diese Informationen sind vom Cachespeicher abhängig. Lässt NULL-Werte zu.|  
|**pool_id**|**int**|**Gilt für**: [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Die ID des Ressourcen-Pools, der diesem Eintrag zugeordnet ist. Lässt NULL-Werte zu.<br /><br /> nicht Katmai|  
|**pdw_node_id**|**int**|**Gilt für**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Der Bezeichner für den Knoten, dem auf diesem Verteilungspunkt befindet.|  
  
## <a name="permissions"></a>Berechtigungen 

Auf [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], erfordert `VIEW SERVER STATE` Berechtigung.   
Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], erfordert die `VIEW DATABASE STATE` Berechtigung in der Datenbank.   

## <a name="see-also"></a>Siehe auch  
 
  [SQL Server-Betriebssystem verbundene dynamische Verwaltungssichten &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  



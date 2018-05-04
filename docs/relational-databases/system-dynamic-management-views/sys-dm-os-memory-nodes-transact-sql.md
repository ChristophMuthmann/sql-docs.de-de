---
title: dm_os_memory_nodes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_os_memory_nodes_TSQL
- sys.dm_os_memory_nodes
- sys.dm_os_memory_nodes_TSQL
- dm_os_memory_nodes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_nodes dynamic management view
ms.assetid: bf4032fe-7db1-40e9-a62e-d69cebff4b44
caps.latest.revision: 24
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: fda6857b9d4469ae0b95eb90aed831c84b866308
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmosmemorynodes-transact-sql"></a>sys.dm_os_memory_nodes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Interne Zuordnungen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwenden den Speicher-Manager von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Nachverfolgung der Unterschiede zwischen der Prozess Arbeitsspeicher-Leistungsindikatoren von **dm_os_process_memory** und interne Indikatoren können die arbeitsspeichernutzung von externen Komponenten an die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] belegten Speicherplatz.  
  
 Die Knoten werden einzeln für physische NUMA-Arbeitsspeicherknoten erstellt. Diese möglicherweise von den CPU-Knoten in verschiedenen **dm_os_nodes**.  
  
 Zuordnungen, die direkt durch Windows-Routinen für die Speicherbelegung vorgenommen wurden, werden nicht nachverfolgt. Die folgende Tabelle enthält Informationen über Arbeitsspeicherbelegungen, die ausschließlich über die Speicher-Manager-Schnittstellen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] durchgeführt werden.  
  
> [!NOTE]  
>  Aufrufen von [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] oder [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], verwenden Sie den Namen **sys.dm_pdw_nodes_os_memory_nodes**.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**memory_node_id**|**smallint**|Gibt die ID des Speicherknotens an. Im Zusammenhang mit **Memory_node_id** von **dm_os_memory_clerks**. Lässt keine NULL-Werte zu.|  
|**virtual_address_space_reserved_kb**|**bigint**|Gibt die Anzahl der virtuellen Adressreservierungen in Kilobytes (KB) an, für die weder ein Commit noch eine Zuordnung zu physischen Seiten besteht. Lässt keine NULL-Werte zu.|  
|**virtual_address_space_committed_kb**|**bigint**|Gibt die Menge virtueller Adressen in KB an, für die ein Commit oder eine Zuordnung zu physischen Seiten besteht. Lässt keine NULL-Werte zu.|  
|**locked_page_allocations_kb**|**bigint**|Gibt die Menge an physischem Speicher in KB an, der von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gesperrt wurde. Lässt keine NULL-Werte zu.|  
|**single_pages_kb**|**bigint**|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].<br /><br /> Speichermenge in KB, für die ein Commit ausgeführt wurde und die mithilfe der Einzelseitenzuordnung durch Threads, die auf diesem Knoten ausgeführt werden, zugeordnet wird. Dieser Speicher wird aus dem Pufferpool zugeordnet. Dieser Wert gibt den Knoten an, auf dem die Zuordnungen angefordert wurden, und nicht den physischen Speicherort, an dem die Zuordnungsanforderung erfüllt wurde.|  
|**pages_kb**|**bigint**|**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Gibt die Menge des zugesicherten Arbeitsspeichers in KB an, der diesem NUMA-Knoten von der Seitenzuordnung im Speicher-Manager zugeordnet wird. Lässt keine NULL-Werte zu.|  
|**multi_pages_kb**|**bigint**|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].<br /><br /> Speichermenge in KB, für die ein Commit ausgeführt wurde und die mithilfe der Mehrfachseitenzuordnung durch Threads, die auf diesem Knoten ausgeführt werden, zugeordnet wird. Dieser Speicher wird von außerhalb des Pufferpools zugeordnet. Dieser Wert gibt an, der Knoten, auf dem der belegungsanforderungen aufgetreten ist, nicht den physischen Speicherort, in dem die zuordnungsanforderung erfüllt wurde.|  
|**shared_memory_reserved_kb**|**bigint**|Gibt die Menge an gemeinsam genutzten Speicher in KB an, die auf diesem Knoten reserviert wurde. Lässt keine NULL-Werte zu.|  
|**shared_memory_committed_kb**|**bigint**|Gibt die Menge an gemeinsam genutzten Speicher in KB an, für die auf diesem Knoten ein Commit ausgeführt wurde. Lässt keine NULL-Werte zu.|  
|**cpu_affinity_mask**|**bigint**|**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Nur interne Verwendung. Lässt keine NULL-Werte zu.|  
|**online_scheduler_mask**|**bigint**|**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Nur interne Verwendung. Lässt keine NULL-Werte zu.|  
|**processor_group**|**smallint**|**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Nur interne Verwendung. Lässt keine NULL-Werte zu.|  
|**foreign_committed_kb**|**bigint**|**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Gibt die Menge an zugesichertem Arbeitsspeicher von anderen Arbeitsspeicherknoten in KB an. Lässt keine NULL-Werte zu.|  
|**target_kb** |**bigint** |**Gilt für**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].<br /><br /> Gibt das Ziel bei den Speicherknoten der Arbeitsspeicher in KB. |   
|**pdw_node_id**|**int**|**Gilt für**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Der Bezeichner für den Knoten, dem auf diesem Verteilungspunkt befindet.|  
  
## <a name="permissions"></a>Berechtigungen

Auf [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], erfordert `VIEW SERVER STATE` Berechtigung.   
Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], erfordert die `VIEW DATABASE STATE` Berechtigung in der Datenbank.   

## <a name="see-also"></a>Siehe auch  
  [SQL Server-Betriebssystem verbundene dynamische Verwaltungssichten &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  



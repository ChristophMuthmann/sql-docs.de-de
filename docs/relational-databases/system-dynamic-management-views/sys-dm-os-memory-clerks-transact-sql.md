---
title: dm_os_memory_clerks (Transact-SQL) | Microsoft Docs
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
- dm_os_memory_clerks
- sys.dm_os_memory_clerks
- dm_os_memory_clerks_TSQL
- sys.dm_os_memory_clerks_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_clerks dynamic management view
ms.assetid: 1d556c67-5c12-46d5-aa8c-7ec1bb858df7
caps.latest.revision: 47
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: b3a0587bf929135f0e0659b608a8df627bf36505
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmosmemoryclerks-transact-sql"></a>sys.dm_os_memory_clerks (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt die Gruppe aller derzeit in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz aktiven Arbeitsspeicherclerks zurück.  
  
> [!NOTE]  
>  Aufrufen von [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] oder [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], verwenden Sie den Namen **sys.dm_pdw_nodes_os_memory_clerks**.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**memory_clerk_address**|**varbinary(8)**|Gibt die eindeutige Speicheradresse des Arbeitsspeicherclerks an. Dies ist die Primärschlüsselspalte. Lässt keine NULL-Werte zu.|  
|**type**|**nvarchar(60)**|Gibt den Typ des Arbeitsspeicherclerks an. Jeder Clerk entspricht einem bestimmten Typ, wie z. B. dem CLR-Clerk MEMORYCLERK_SQLCLR. Lässt keine NULL-Werte zu.|  
|**name**|**nvarchar(256)**|Gibt den intern zugewiesenen Namen des Arbeitsspeicherclerks an. Eine Komponente kann über mehrere Arbeitsspeicherclerks eines bestimmten Typs verfügen. Eine Komponente hat die Möglichkeit, bestimmte Namen zum Identifizieren von Arbeitsspeicherclerks desselben Typs zu verwenden. Lässt keine NULL-Werte zu.|  
|**memory_node_id**|**smallint**|Gibt die ID des Speicherknotens an. Lässt keine NULL-Werte zu.|  
|**single_pages_kb**|**bigint**|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].|  
|**pages_kb**|**bigint**|**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Gibt an, wie viel Arbeitsspeicher für Seiten diesem Arbeitsspeicherclerk (in Kilobyte) zugewiesen wurde. Lässt keine NULL-Werte zu.|  
|**multi_pages_kb**|**bigint**|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].<br /><br /> Umfang des zugeordneten Arbeitsspeichers für mehrere Seiten in KB. Dies entspricht dem Umfang des Arbeitsspeichers, der mithilfe der Mehrfachseitenzuordnung der Speicherknoten zugeordnet wurde. Dieser Arbeitsspeicher wird außerhalb des Pufferpools zugeordnet und nutzt die virtuelle Zuordnung der Arbeitsspeicherknoten. Lässt keine NULL-Werte zu.|  
|**virtual_memory_reserved_kb**|**bigint**|Gibt den Umfang des von einem Arbeitsspeicherclerk reservierten virtuellen Arbeitsspeichers an. Lässt keine NULL-Werte zu.|  
|**virtual_memory_committed_kb**|**bigint**|Gibt den Umfang des virtuellen Arbeitsspeichers an, für den ein Arbeitsspeicherclerk ein Commit ausgeführt hat. Der Umfang des Arbeitsspeichers, für den ein Commit ausgeführt wurde, sollte immer geringer als der Umfang des reservierten Arbeitsspeichers sein. Lässt keine NULL-Werte zu.|  
|**awe_allocated_kb**|**bigint**|Gibt den Arbeitsspeicher in Kilobyte (KB) an, der im physischen Speicher gesperrt und nicht vom Betriebssystem ausgelagert ist. Lässt keine NULL-Werte zu.|  
|**shared_memory_reserved_kb**|**bigint**|Gibt den Umfang des von einem Arbeitsspeicherclerk reservierten gemeinsamen Arbeitsspeichers an. Der Umfang des Arbeitsspeichers, der als freigegebener Speicherbereich und für die Dateizuordnung reserviert ist. Lässt keine NULL-Werte zu.|  
|**shared_memory_committed_kb**|**bigint**|Gibt den Umfang des freigegebenen Speicherbereichs an, für den vom Arbeitsspeicherclerk ein Commit ausgeführt wurde. Lässt keine NULL-Werte zu.|  
|**page_size_in_bytes**|**bigint**|Gibt die Granularität der Seitenzuordnung für diesen Arbeitsspeicherclerk an. Lässt keine NULL-Werte zu.|  
|**page_allocator_address**|**varbinary(8)**|Gibt die Adresse der Seitenzuordnung an. Diese Adresse ist für einen Arbeitsspeicherclerk eindeutig und kann verwendet werden, **dm_os_memory_objects** zu suchen, die an diesen Clerk gebunden sind. Lässt keine NULL-Werte zu.|  
|**host_address**|**varbinary(8)**|Gibt die Arbeitsspeicheradresse des Hosts für diesen Arbeitsspeicherclerk an. Weitere Informationen finden Sie unter [dm_os_hosts &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-hosts-transact-sql.md). Komponenten, wie z. B. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client Access [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Speicherressourcen über die Hostschnittstelle.<br /><br /> 0x00000000 = Arbeitsspeicherclerk gehört zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Lässt keine NULL-Werte zu.|  
|**pdw_node_id**|**int**|**Gilt für**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Der Bezeichner für den Knoten, dem auf diesem Verteilungspunkt befindet.|  
  
## <a name="permissions"></a>Berechtigungen 

Auf [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], erfordert `VIEW SERVER STATE` Berechtigung.   
Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], erfordert die `VIEW DATABASE STATE` Berechtigung in der Datenbank.   
  
## <a name="remarks"></a>Hinweise  
 Der Speicher-Manager von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] besteht aus einer Hierarchie mit drei Ebenen. Die unterste Ebene der Hierarchie bilden Speicherknoten. Die mittlere Ebene besteht aus Arbeitsspeicherclerks, Arbeitsspeichercaches und Arbeitsspeicherpools. Die obere Ebene besteht aus Speicherobjekten. Diese Objekte werden im Allgemeinen für die Zuordnung von Arbeitsspeicher in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz verwendet.  
  
 Speicherknoten stellen die Schnittstelle und die Implementierung für Zuordnungen auf unterer Ebene bereit. Innerhalb von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] haben nur Arbeitsspeicherclerks Zugriff auf Speicherknoten. Arbeitsspeicherclerks greifen für die Belegung von Arbeitsspeicher auf Speicherknotenschnittstellen zu. Zudem können Speicherknoten den mithilfe des Clerks zugeordneten Arbeitsspeicher zu Diagnosezwecken nachverfolgen. Jede Komponente, die eine beträchtliche Speichermenge zuordnet, muss einen eigenen Arbeitsspeicherclerk erstellen und ihren gesamten Arbeitsspeicher mithilfe der Clerkschnittstellen zuordnen. Komponenten erstellen häufig ihre entsprechenden Clerks, wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gestartet wird.  
  
## <a name="see-also"></a>Siehe auch  

 [SQL Server-Betriebssystem verbundene dynamische Verwaltungssichten &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [sys.dm_os_sys_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)   
 [dm_exec_query_memory_grants &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [sys.dm_exec_query_plan &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)   
 [sys.dm_exec_sql_text &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)  
  
  



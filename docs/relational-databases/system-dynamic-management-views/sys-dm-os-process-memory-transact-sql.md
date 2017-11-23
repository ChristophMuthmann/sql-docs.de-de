---
title: dm_os_process_memory (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_os_process_memory_TSQL
- dm_os_process_memory_TSQL
- dm_os_process_memory
- sys.dm_os_process_memory
dev_langs: TSQL
helpviewer_keywords: sys.dm_os_process_memory dynamic management view
ms.assetid: e838130c-95d4-4605-9e3b-eb0ab71cd250
caps.latest.revision: "23"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2941cc2e290d08f8c634dc38634544f036aea79c
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmosprocessmemory-transact-sql"></a>sys.dm_os_process_memory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Die meisten Speicherbelegungen, die für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Prozessraum attributiert sind, werden über Schnittstellen gesteuert, die eine Nachverfolgung und Berücksichtigung dieser Zuordnungen ermöglichen. Speicherbelegungen werden jedoch eventuell in dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Adressraum ausgeführt, der die internen Arbeitsspeicherverwaltungsroutinen umgeht. Die Werte werden durch Aufrufe des Basisbetriebssystems erhalten. Sie sind nicht durch interne Methoden von bearbeitet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], außer wenn es Anpassung für gesperrte oder umfangreiche seitenzuordnungen.  
  
 Alle zurückgegebenen Werte mit Angaben zu den Arbeitsspeichergrößen werden in Kilobytes (KB) angezeigt. Die Spalte **Total_virtual_address_space_reserved_kb** ist ein Duplikat eines **Virtual_memory_in_bytes** aus **Sys. dm_os_sys_info**.  
  
 In der folgenden Tabelle wird ein vollständiges Bild des Prozessadressraums angegeben.  
  
> [!NOTE]  
>  Aufrufen von [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] oder [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], verwenden Sie den Namen **sys.dm_pdw_nodes_os_process_memory**.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**physical_memory_in_use_kb**|**bigint**|Gibt das Prozessworkingset in KB an, wie vom Betriebssystem gemeldet, sowie nachverfolgte Zuordnungen, die über APIs umfangreicher Seiten und AWE-APIs durchgeführt wurden. Lässt keine NULL-Werte zu.|  
|**large_page_allocations_kb**|**bigint**|Gibt den physischen Arbeitsspeicher an, der über APIs umfangreicher Seiten zugeordnet wird. Lässt keine NULL-Werte zu.|  
|**locked_page_allocations_kb**|**bigint**|Gibt im Arbeitsspeicher gesperrte Speicherseiten an. Lässt keine NULL-Werte zu.|  
|**total_virtual_address_space_kb**|**bigint**|Gibt die Gesamtgröße des Benutzermodusteils im virtuellen Adressraum an. Lässt keine NULL-Werte zu.|  
|**virtual_address_space_reserved_kb**|**bigint**|Gibt die Gesamtmenge des vom Prozess reservierten virtuellem Adressraums an. Lässt keine NULL-Werte zu.|  
|**virtual_address_space_committed_kb**|**bigint**|Gibt die Menge des reservierten virtuellen Adressraums an, für die ein Commit oder eine Zuordnung zu physischen Seiten besteht. Lässt keine NULL-Werte zu.|  
|**virtual_address_space_available_kb**|**bigint**|Gibt die Menge an virtuellen Adressräumen an, die gerade frei sind. Lässt keine NULL-Werte zu.<br /><br /> **Hinweis:** frei von Regionen, die kleiner sind als die Granularität für die Zuordnung vorhanden sein kann. Diese Bereiche sind für Zuordnungen nicht verfügbar.|  
|**page_fault_count**|**bigint**|Gibt die Anzahl der Seitenfehler an, die vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Prozess verursacht wurden. Lässt keine NULL-Werte zu.|  
|**memory_utilization_percentage**|**int**|Gibt den Prozentwert des Arbeitsspeichers an, für den ein Commit ausgeführt wurde und der sich im Workingset befindet. Lässt keine NULL-Werte zu.|  
|**available_commit_limit_kb**|**bigint**|Gibt den Arbeitsspeicher an, der für den Commit durch den Prozess verfügbar ist. Lässt keine NULL-Werte zu.|  
|**process_physical_memory_low**|**bit**|Gibt an, dass der Prozess auf Benachrichtigung zu nicht genügend physischem Arbeitsspeicher reagiert. Lässt keine NULL-Werte zu.|  
|**process_virtual_memory_low**|**bit**|Gibt an, dass eine Bedingung nicht genügenden virtuellen Arbeitsspeichers erkannt wurde. Lässt keine NULL-Werte zu.|  
|**pdw_node_id**|**int**|**Gilt für**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Der Bezeichner für den Knoten, dem auf diesem Verteilungspunkt befindet.|  
  
## <a name="permissions"></a>Berechtigungen  
 Auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erfordert die VIEW SERVER STATE-Berechtigung auf dem Server.  
  
 Auf [!INCLUDE[ssSDS](../../includes/sssds-md.md)] benötigen Premium-Ebenen die VIEW DATABASE STATE-Berechtigung in der Datenbank. Auf [!INCLUDE[ssSDS](../../includes/sssds-md.md)] Standard und grundlegenden Organisationsebenen erfordert die [!INCLUDE[ssSDS](../../includes/sssds-md.md)] -Administratorkonto ein.  
  
## <a name="see-also"></a>Siehe auch  
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [SQL Server-Betriebssystem in Verbindung mit dynamischen Verwaltungssichten &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  



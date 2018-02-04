---
title: dm_os_threads (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_os_threads_TSQL
- sys.dm_os_threads
- dm_os_threads
- sys.dm_os_threads_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_threads dynamic management view
ms.assetid: a5052701-edbf-4209-a7cb-afc9e65c41c1
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 41727f804fb31ed6773c671a40b63cb02ca6793b
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmosthreads-transact-sql"></a>sys.dm_os_threads (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt eine Liste aller [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Betriebssystemthreads zurück, die unter dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Prozess ausgeführt werden.  
  
> [!NOTE]  
>  Aufrufen von [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] oder [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], verwenden Sie den Namen **sys.dm_pdw_nodes_os_threads**.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|thread_address|**varbinary(8)**|Speicheradresse (Primärschlüssel) des Threads.|  
|started_by_sqlservr|**bit**|Gibt den Threadinitiator an.<br /><br /> 1 = Der Thread wurde von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gestartet.<br /><br /> 0 = Der Thread wurde von einer anderen Komponente gestartet, z. B. von einer erweiterten gespeicherten Prozedur innerhalb von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|os_thread_id|**int**|ID des vom Betriebssystem zugewiesenen Threads.|  
|status|**int**|Internes Statusflag.|  
|instruction_address|**varbinary(8)**|Adresse der zurzeit ausgeführten Anweisung.|  
|creation_time|**datetime**|Zeit, zu der dieser Thread erstellt wurde.|  
|kernel_time|**bigint**|Menge der von diesem Thread verwendeten Kernelzeit.|  
|usermode_time|**bigint**|Menge der von diesem Thread verwendeten Benutzerzeit.|  
|stack_base_address|**varbinary(8)**|Speicheradresse der höchsten Stapeladresse für diesen Thread.|  
|stack_end_address|**varbinary(8)**|Speicheradresse der niedrigsten Stapeladresse für diesen Thread.|  
|stack_bytes_committed|**int**|Anzahl von Bytes, für die im Stapel ein Commit ausgeführt wurde.|  
|stack_bytes_used|**int**|Anzahl von Bytes, die aktiv im Thread verwendet werden.|  
|affinity|**bigint**|CPU-Maske, in der dieser Thread ausgeführt wird. Dies hängt vom konfigurierten Wert der **ALTER SERVER CONFIGURATION SET PROCESS AFFINITY** Anweisung. Kann sich bei weicher Affinität vom Zeitplanungsmodul unterscheiden.|  
|Priority|**int**|Prioritätswert dieses Threads.|  
|Gebietsschema|**int**|Zwischengespeicherter Gebietsschemabezeichner (LCID) für den Thread.|  
|Token|**varbinary(8)**|Zwischengespeichertes Identitätswechsel-Tokenhandle für den Thread.|  
|is_impersonating|**int**|Gibt an, ob dieser Thread den Win32-Identitätswechsel verwendet.<br /><br /> 1 = Der Thread verwendet Sicherheitsanmeldeinformationen, die von der Standardeinstellung des Prozesses abweichen. Dieser Wert gibt an, dass der Thread die Identität einer Entität annimmt, die nicht mit der Entität übereinstimmt, die den Prozess erstellt hat.|  
|is_waiting_on_loader_lock|**int**|Betriebssystemstatus, der angibt, ob der Thread in der Loadersperre wartet.|  
|fiber_data|**varbinary(8)**|Aktuelle Win32-Fiber, die im Thread ausgeführt wird. Dies gilt nur, wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] für Lightweightpooling konfiguriert ist.|  
|thread_handle|**varbinary(8)**|Nur interne Verwendung.|  
|event_handle|**varbinary(8)**|Nur interne Verwendung.|  
|scheduler_address|**varbinary(8)**|Speicheradresse des Zeitplanungsmoduls, das diesem Thread zugeordnet ist. Weitere Informationen finden Sie unter [DM_OS_SCHEDULERS &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md).|  
|worker_address|**varbinary(8)**|Speicheradresse des Arbeitsthreads, der an diesen Thread gebunden ist. Weitere Informationen finden Sie unter [dm_os_workers &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md).|  
|fiber_context_address|**varbinary(8)**|Interne Fiberkontextadresse. Dies gilt nur, wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] für Lightweightpooling konfiguriert ist.|  
|self_address|**varbinary(8)**|Interner Konsistenzzeiger.|  
|processor_group|**smallint**|**Gilt für**: [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Prozessorgruppen-ID.|  
|pdw_node_id|**int**|**Gilt für**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Der Bezeichner für den Knoten, dem auf diesem Verteilungspunkt befindet.|  
  
## <a name="permissions"></a>Berechtigungen  
Auf [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], erfordert `VIEW SERVER STATE` Berechtigung.   
Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] benötigen Premium-Ebenen der `VIEW DATABASE STATE` Berechtigung in der Datenbank. Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard und grundlegenden Organisationsebenen erfordert die **Serveradministrator** oder ein **Azure Active Directory-Administrators** Konto.  
  
## <a name="examples"></a>Beispiele  
 Beim Start werden von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Threads gestartet, denen anschließend Arbeitsthreads zugeordnet werden. Externe Komponenten, z. B. eine erweiterte gespeicherte Prozedur, können jedoch Threads unter dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Prozess starten. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hat keine Kontrolle über diese Threads. dm_os_threads bieten Informationen zu extern gestarteten Threads, die Ressourcen in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Prozess.  
  
 Mit der folgenden Abfrage werden Arbeitsthreads zusammen mit der jeweiligen Ausführungszeit ermittelt, die nicht von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gestartete Threads ausführen.  
  
> [!NOTE]  
>  Aus Gründen der Kürze wird in der folgenden Abfrage ein Sternchen (`*`) in der `SELECT`-Anweisung verwendet. Vermeiden Sie die Verwendung des Sternchens (*) insbesondere für Katalogsichten, dynamische Verwaltungssichten und Systemfunktionen mit Tabellenrückgabe. Zukünftige Upgrades und Versionen von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] können Spalten hinzufügen und ändern Sie die Reihenfolge der Spalten in diesen Sichten und Funktionen. Diese Änderungen könnten zur Funktionsunfähigkeit von Anwendungen führen, die eine bestimmte Reihenfolge und Anzahl von Spalten erwarten.  
  
```  
SELECT *  
  FROM sys.dm_os_threads  
  WHERE started_by_sqlservr = 0;  
```  
  
## <a name="see-also"></a>Siehe auch  
  [sys.dm_os_workers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md)   
 [SQL Server-Betriebssystem in Verbindung mit dynamischen Verwaltungssichten &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  



---
title: dm_os_hosts (Transact-SQL) | Microsoft Docs
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
- sys.dm_os_hosts_TSQL
- dm_os_hosts
- dm_os_hosts_TSQL
- sys.dm_os_hosts
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_hosts dynamic management view
ms.assetid: a313ff3b-1fe9-421e-b94b-cea19c43b0e5
caps.latest.revision: 35
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ce4f4f05071fe56f4543c1bdaafdbed367b17ea6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmoshosts-transact-sql"></a>sys.dm_os_hosts (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt alle Hosts zurück, die zurzeit in einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] registriert sind. Diese Sicht gibt auch die von diesen Hosts verwendeten Ressourcen zurück.  
  
> [!NOTE]  
>  Aufrufen von [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] oder [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], verwenden Sie den Namen **sys.dm_pdw_nodes_os_hosts**.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**host_address**|**varbinary(8)**|Die interne Speicheradresse des Hostobjekts.|  
|**type**|**nvarchar(60)**|Der Typ der gehosteten Komponente. Beispiel:<br /><br /> SOSHOST_CLIENTID_SERVERSNI= SQL Server Native Interface<br /><br /> SOSHOST_CLIENTID_SQLOLEDB = SQL Server Native Client OLE DB Provider<br /><br /> SOSHOST_CLIENTID_MSDART = Microsoft Data Access Run Time|  
|**name**|**nvarchar(32)**|Der Name des Hosts.|  
|**enqueued_tasks_count**|**int**|Gesamtanzahl der Tasks, die von diesem Host in Warteschlangen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] platziert wurden.|  
|**active_tasks_count**|**int**|Gesamtanzahl der aktuell ausgeführten Tasks, die von diesem Host in Warteschlangen platziert wurden.|  
|**completed_ios_count**|**int**|Gesamtanzahl der E/A-Vorgänge, die über diesen Host ausgegeben und abgeschlossen wurden.|  
|**completed_ios_in_bytes**|**bigint**|Gesamtanzahl von Bytes der E/A-Vorgänge, die über diesen Host abgeschlossen wurden.|  
|**active_ios_count**|**int**|Gesamtanzahl von E/A-Anforderungen in Verbindung mit diesem Host, die zurzeit auf Beendigung warten.|  
|**default_memory_clerk_address**|**varbinary(8)**|Speicheradresse des diesem Host zugeordneten Arbeitsspeicherclerk-Objekts. Weitere Informationen finden Sie unter [dm_os_memory_clerks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md).|  
|**pdw_node_id**|**int**|**Gilt für**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Der Bezeichner für den Knoten, dem auf diesem Verteilungspunkt befindet.|  
  
## <a name="permissions"></a>Berechtigungen

Auf [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], erfordert `VIEW SERVER STATE` Berechtigung.   
Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], erfordert die `VIEW DATABASE STATE` Berechtigung in der Datenbank.   

## <a name="remarks"></a>Hinweise  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] lässt Komponenten, z. B. einen OLE DB-Anbieter, die nicht Teil der ausführbaren Datei von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sind, Arbeitsspeicher belegen und an nicht präemptiven Planungen teilnehmen. Diese Komponenten werden von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gehostet, und alle von diesen Komponenten zugeordneten Ressourcen werden nachverfolgt. Als Host kann [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Ressourcen besser berücksichtigen, die von Komponenten außerhalb der ausführbaren Datei von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet werden.  
  
## <a name="relationship-cardinalities"></a>Kardinalität der Beziehungen  
  
|Von|Aktion|Beziehung|  
|----------|--------|------------------|  
|sys.dm_os_hosts. default_memory_clerk_address|sys.dm_os_memory_clerks. memory_clerk_address|1:1|  
|sys.dm_os_hosts. host_address|sys.dm_os_memory_clerks. host_address|1:1|  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird der Gesamtumfang des Arbeitsspeichers, für den von einer gehosteten Komponente ein Commit ausgeführt wurde, bestimmt.  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
  
```  
SELECT h.type, SUM(mc.pages_kb) AS commited_memory  
FROM sys.dm_os_memory_clerks AS mc   
INNER JOIN sys.dm_os_hosts AS h   
    ON mc.memory_clerk_address = h.default_memory_clerk_address  
GROUP BY h.type;  
```  
  
## <a name="see-also"></a>Siehe auch  

 [sys.dm_os_memory_clerks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)   
 [SQL Server-Betriebssystem verbundene dynamische Verwaltungssichten &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  



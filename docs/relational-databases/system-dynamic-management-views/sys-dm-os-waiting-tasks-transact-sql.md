---
title: Sys. dm_os_waiting_tasks (Transact-SQL) | Microsoft Docs
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
- dm_os_waiting_tasks
- sys.dm_os_waiting_tasks_TSQL
- dm_os_waiting_tasks_TSQL
- sys.dm_os_waiting_tasks
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_waiting_tasks dynamic management view
ms.assetid: ca5e6844-368c-42e2-b187-6e5f5afc8df3
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 914d26a40ea2c1c5f3246dd134e0888dddeff891
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmoswaitingtasks-transact-sql"></a>sys.dm_os_waiting_tasks (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt Informationen zur Warteschlange von Tasks zurück, die auf eine Ressource warten.  
  
> [!NOTE]  
>  Aufrufen von [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] oder [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], verwenden Sie den Namen **sys.dm_pdw_nodes_os_waiting_tasks**.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**waiting_task_address**|**varbinary(8)**|Adresse des wartenden Tasks.|  
|**session_id**|**smallint**|ID der Sitzung, die dem Task zugeordnet ist.|  
|**exec_context_id**|**int**|ID des Ausführungskontexts, der dem Task zugeordnet ist.|  
|**wait_duration_ms**|**bigint**|Gesamtwartezeit für diesen Wartetyp (in Millisekunden). Diese Zeit **Signal_wait_time**.|  
|**wait_type**|**nvarchar(60)**|Name des Wartetyps.|  
|**resource_address**|**varbinary(8)**|Adresse der Ressource, auf die der Task wartet.|  
|**blocking_task_address**|**varbinary(8)**|Task, der derzeit diese Ressource verwendet.|  
|**blocking_session_id**|**smallint**|ID der Sitzung, die die Anforderung blockiert. Wenn diese Spalte den Wert NULL aufweist, wird die Anforderung nicht blockiert, oder die Sitzungsinformationen der blockierenden Sitzung sind nicht verfügbar (bzw. können nicht identifiziert werden).<br /><br /> -2 = Der Besitzer der blockierenden Ressource ist eine verwaiste verteilte Transaktion.<br /><br /> -3 = Der Besitzer der blockierenden Ressource ist eine verzögerte Wiederherstellungstransaktion.<br /><br /> -4 = Die Sitzungs-ID des Besitzers des blockierenden Latches konnte aufgrund interner Latchstatusübergänge nicht bestimmt werden.|  
|**blocking_exec_context_id**|**int**|ID des Ausführungskontexts des blockierenden Tasks.|  
|**resource_description**|**nvarchar(3072)**|Beschreibung der verwendeten Ressource. Weitere Informationen finden Sie in der unten stehenden Liste.|  
|**pdw_node_id**|**int**|**Gilt für**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Der Bezeichner für den Knoten, dem auf diesem Verteilungspunkt befindet.|  
  
## <a name="resourcedescription-column"></a>resource_description-Spalte  
 Die Resource_description-Spalte verfügt über folgende Werte möglich.  
  
 **Der Besitzer der Threadpool-Ressource:**  
  
-   Threadpool-Id = Planer\<Hex-Adresse >  
  
 **Ressourcenbesitzer der parallelen Abfrage:**  
  
-   ExchangeEvent-Id = {Port | Pipe}\<Hex-Address > Wartetyp =\<Exchange Wartetyp > NodeId =\<Exchange-Knoten-Id >  
  
 **Exchange-Wait-Type:**  
  
-   e_waitNone  
  
-   e_waitPipeNewRow  
  
-   e_waitPipeGetRow  
  
-   e_waitSynchronizeConsumerOpen  
  
-   e_waitPortOpen  
  
-   e_waitPortClose  
  
-   e_waitRange  
  
 **Der Besitzer der Lock-Ressource:**  
  
-   \<Type-Specific-Description > Id = Sperre\<Lock-Hex-Address > Modus =\<Modus > AssociatedObjectId =\<zugeordnete-Obj-Id >  
  
     **\<Type-Specific-Description > kann sein:**  
  
    -   Für DATABASE: Databaselock Subresource =\<Databaselock-Subresource > Dbid =\<Db-Id >  
  
    -   Für die Datei: Filelock Fileid =\<Datei-Id > Subresource =\<Filelock-Subresource > Dbid =\<Db-Id >  
  
    -   Für OBJECT: Objectlock LockPartition =\<Lock-Partitions-Id > Objid =\<Obj-Id > Subresource =\<Objectlock-Subresource > Dbid =\<Db-Id >  
  
    -   Für PAGE: Pagelock Fileid =\<Datei-Id > Pageid =\<-Seiten-Id > Dbid =\<Db-Id > Subresource =\<Pagelock-Subresource >  
  
    -   Für Key: Keylock Hobtid =\<Hobt-Id > Dbid =\<Db-Id >  
  
    -   Für EXTENT: Extentlock Fileid =\<Datei-Id > Pageid =\<-Seiten-Id > Dbid =\<Db-Id >  
  
    -   Für RID: Ridlock Fileid =\<Datei-Id > Pageid =\<-Seiten-Id > Dbid =\<Db-Id >  
  
    -   Für APPLICATION: Applicationlock Hash =\<Hash > DatabasePrincipalId =\<Rolle-Id > Dbid =\<Db-Id >  
  
    -   Für METADATA: Metadatalock Subresource =\<Metadaten-Subresource > Classid =\<Metadatalock-Description > Dbid =\<Db-Id >  
  
    -   Für HOBT: Hobtlock Hobtid =\<Hobt-Id > Subresource =\<Hobt-Subresource > Dbid =\<Db-Id >  
  
    -   Für ALLOCATION_UNIT: Allocunitlock Hobtid =\<Hobt-Id > Subresource =\<Alloc-Unit-Subresource > Dbid =\<Db-Id >  
  
     **\<Mode > kann sein:**  
  
     Sch-S, Sch-M, S, U, X, IS, IU, IX, SIU, SIX, UIX, BU, RangeS-S, RangeS-U, RangeI-N, RangeI-S, RangeI-U, RangeI-X, RangeX-, RangeX-U, RangeX-X  
  
 **Besitzer der externen Ressource:**  
  
-   Externe ExternalResource =\<Wartetyp >  
  
 **Besitzer der allgemeinen Ressource:**  
  
-   Arbeitsbereich "TransactionMutex TransactionInfo" =\<Arbeitsbereich-Id >  
  
-   Mutex  
  
-   CLRTaskJoin  
  
-   CLRMonitorEvent  
  
-   CLRRWLockEvent  
  
-   resourceWait  
  
 **Besitzer der latchressource:**  
  
-   \<db-id>:\<file-id>:\<page-in-file>  
  
-   \<GUID>  
  
-   \<latchklasse > (\<Latch-Adresse >)  
  
## <a name="permissions"></a>Berechtigungen

Auf [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], erfordert `VIEW SERVER STATE` Berechtigung.   
Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], erfordert die `VIEW DATABASE STATE` Berechtigung in der Datenbank.   
 
## <a name="example"></a>Beispiel
In diesem Beispiel wird die blockierte Sitzungen identifiziert.  Führen Sie die [!INCLUDE[tsql](../../includes/tsql-md.md)] -Abfrage im [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].
```sql
SELECT * FROM sys.dm_os_waiting_tasks 
WHERE blocking_session_id IS NOT NULL; 
``` 
  
## <a name="see-also"></a>Siehe auch  
  [SQL Server-Betriebssystem verbundene dynamische Verwaltungssichten &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  



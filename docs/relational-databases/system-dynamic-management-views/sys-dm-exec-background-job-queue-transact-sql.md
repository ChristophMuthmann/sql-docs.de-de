---
title: dm_exec_background_job_queue (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
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
- dm_exec_background_job_queue
- sys.dm_exec_background_job_queue_TSQL
- dm_exec_background_job_queue_TSQL
- sys.dm_exec_background_job_queue
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_background_job_queue dynamic management function
ms.assetid: 05d9884f-b74c-4e3c-a23b-c90c1ea5ef02
caps.latest.revision: 31
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: fd0986b83ee1f4fa98408e15b500330060c7f254
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmexecbackgroundjobqueue-transact-sql"></a>sys.dm_exec_background_job_queue (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt eine Zeile für jeden Abfrageprozessorauftrag zurück, der für die asynchrone Ausführung (im Hintergrund) geplant ist.  
  
> **HINWEIS!** Aufrufen von **[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]** oder **[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]**, verwenden Sie den Namen **sys.dm_pdw_nodes_exec_background_job_queue**.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**time_queued**|**datetime**|Zeitpunkt, zu dem der Auftrag der Warteschlange hinzugefügt wurde.|  
|**job_id**|**int**|Auftragsbezeichner.|  
|**database_id**|**int**|Datenbank, für die der Auftrag ausgeführt werden soll.|  
|**object_id1**|**int**|Wert hängt vom Auftragstyp ab. Weitere Informationen finden Sie im Abschnitt mit Hinweisen.|  
|**object_id2**|**int**|Wert hängt vom Auftragstyp ab. Weitere Informationen finden Sie im Abschnitt mit Hinweisen.|  
|**object_id3**|**int**|Wert hängt vom Auftragstyp ab. Weitere Informationen finden Sie im Abschnitt mit Hinweisen.|  
|**object_id4**|**int**|Wert hängt vom Auftragstyp ab. Weitere Informationen finden Sie im Abschnitt mit Hinweisen.|  
|**error_code**|**int**|Fehlercode, wenn der Auftrag aufgrund eines Fehlers wieder eingefügt wurde. NULL, wenn der Auftrag angehalten, nicht entnommen oder abgeschlossen wurde.|  
|**request_type**|**smallint**|Typ der Auftragsanforderung.|  
|**retry_count**|**smallint**|Häufigkeit, mit der der Auftrag aufgrund mangelnder Ressourcen oder sonstiger Gründe aus der Warteschlange entnommen und wieder eingefügt wurde.|  
|**in_progress**|**smallint**|Gibt an, ob der Auftrag mit der Ausführung begonnen hat.<br /><br /> 1 = Gestartet<br /><br /> 0 = Wartet|  
|**session_id**|**smallint**|Sitzungsbezeichner.|  
|**pdw_node_id**|**int**|**Gilt für**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Der Bezeichner für den Knoten, dem auf diesem Verteilungspunkt befindet.|  
  
## <a name="permissions"></a>Berechtigungen

Auf [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], erfordert `VIEW SERVER STATE` Berechtigung.   
Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], erfordert die `VIEW DATABASE STATE` Berechtigung in der Datenbank.   
  
## <a name="remarks"></a>Hinweise  
 Diese Sicht gibt nur Informationen für Aufträge zum asynchronen Aktualisieren von Statistiken zurück. Weitere Informationen zum asynchronen Aktualisieren von Statistiken finden Sie unter [Statistiken](../../relational-databases/statistics/statistics.md).  
  
 Die Werte der **object_id1** über **object_id4** hängen vom Typ der auftragsanforderung. In der folgenden Tabelle wird die Bedeutung dieser Spalten für die verschiedenen Auftragstypen zusammengefasst.  
  
|Anforderungstyp|object_id1|object_id2|object_id3|object_id4|  
|------------------|-----------------|-----------------|-----------------|-----------------|  
|Asynchrones Statistikupdate|Tabellen- oder Sicht-ID|Statistik-ID|Wird nicht verwendet|Wird nicht verwendet|  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die Anzahl der aktiven asynchronen Aufträge in der Hintergrundwarteschlange für die einzelnen Datenbanken in der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zurückgegeben.  
  
```  
SELECT DB_NAME(database_id) AS [Database], COUNT(*) AS [Active Async Jobs]  
FROM sys.dm_exec_background_job_queue  
WHERE in_progress = 1  
GROUP BY database_id;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Ausführung dynamische Verwaltungssichten und-Funktionen im Zusammenhang &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [Statistiken](../../relational-databases/statistics/statistics.md)   
 [KILL STATS JOB &#40;Transact-SQL&#41;](../../t-sql/language-elements/kill-stats-job-transact-sql.md)  
  
  




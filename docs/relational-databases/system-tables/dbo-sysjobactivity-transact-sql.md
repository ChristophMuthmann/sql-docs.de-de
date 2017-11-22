---
title: dbo.sysjobactivity (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/05/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dbo.sysjobactivity_TSQL
- dbo.sysjobactivity
- sysjobactivity
- sysjobactivity_TSQL
dev_langs: TSQL
helpviewer_keywords: sysjobactivity system table
ms.assetid: fd17cac9-5d1f-4b44-b2dc-ee9346d8bf1e
caps.latest.revision: "17"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 0b7991dfbe4aee731d436d725aba2081adf87e84
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="dbosysjobactivity-transact-sql"></a>dbo.sysjobactivity (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Datensätze, die aktuelle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agentauftragsaktivität und Status.  Diese Tabelle wird in der **msdb** -Datenbank gespeichert.
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|ID der Sitzung, die in der **syssessions** -Tabelle in der **msdb** -Datenbank gespeichert ist.|  
|**job_id**|**uniqueidentifier**|ID des Auftrags.|  
|**run_requested_date**|**datetime**|Datum und Uhrzeit, zu der der Auftrag laut Anforderung ausgeführt werden sollte.|  
|**run_requested_source**|**sysname(nvarchar(128))**|Quelle der Anforderung der Auftragsausführung.<br /><br /> **1** = SOURCE_SCHEDULER<br /><br /> **2** = SOURCE_ALERTER<br /><br /> **3** = SOURCE_BOOT<br /><br /> **4** = SOURCE_USER<br /><br /> **6** = SOURCE_ON_IDLE_SCHEDULE|  
|**queued_date**|**datetime**|Datum und Uhrzeit, zu der dieser Auftrag in der Warteschlange angeordnet wurde. Wird der Auftrag direkt ausgeführt, enthält diese Spalte den Wert NULL.|  
|**start_execution_date**|**datetime**|Datum und Uhrzeit, für die die Ausführung des Auftrags geplant wurde.|  
|**last_executed_step_id**|**int**|ID des letzten ausgeführten Auftragsschrittes.|  
|**last_executed_step_**<br /><br /> **Datum**|**datetime**|Datum und Uhrzeit, zu der die Ausführung des letzten Auftragsschrittes begann.|  
|**stop_execution_date**|**datetime**|Datum und Uhrzeit, zu der die Ausführung des Auftrags fertig gestellt wurde.|  
|**job_history_id**|**int**|Wird verwendet, um eine Zeile in der **sysjobhistory** -Tabelle zu identifizieren.|  
|**next_scheduled_run_date**|**datetime**|Nächstes Datum und nächste Uhrzeit, für die die Ausführung des Auftrags geplant ist.|  

## <a name="example"></a>Beispiel
In diesem Beispiel wird den Laufzeit-Status für alle SQL Server-Agent-Aufträge zurück.  Führen Sie das folgende [!INCLUDE[tsql](../../includes/tsql-md.md)] in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]aus.
```tsql
SELECT sj.Name, 
    CASE
        WHEN sja.start_execution_date IS NULL THEN 'Not running'
        WHEN sja.start_execution_date IS NOT NULL AND sja.stop_execution_date IS NULL THEN 'Running'
        WHEN sja.start_execution_date IS NOT NULL AND sja.stop_execution_date IS NOT NULL THEN 'Not running'
    END AS 'RunStatus'
FROM msdb.dbo.sysjobs sj
JOIN msdb.dbo.sysjobactivity sja
ON sj.job_id = sja.job_id
WHERE session_id = (
    SELECT MAX(session_id) FROM msdb.dbo.sysjobactivity); 
```
  
## <a name="see-also"></a>Siehe auch  
 [dbo.sysjobhistory &#40; Transact-SQL &#41;](../../relational-databases/system-tables/dbo-sysjobhistory-transact-sql.md)  
  
  

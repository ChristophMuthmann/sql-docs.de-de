---
title: "Für Ad-hoc-Arbeitsauslastungen optimieren (Serverkonfigurationsoption) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 11/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: optimize for ad hoc workloads option
ms.assetid: 0972e028-3a8e-454b-a186-e814a1d431f2
caps.latest.revision: "14"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 96e21a0eb32b9aeecabdfeb574d3e793b3ab99d8
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/02/2018
---
# <a name="optimize-for-ad-hoc-workloads-server-configuration-option"></a>Für Ad-hoc-Arbeitsauslastungen optimieren (Serverkonfigurationsoption)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Die Option **Optimieren für Ad-hoc-Arbeitsauslastung** wird zum Verbessern der Effizienz des Plancaches für Arbeitsauslastungen verwendet, die viele Ad-hoc-Batches für die einmalige Verwendung enthalten. Wenn diese Option auf 1 festgelegt ist, speichert [!INCLUDE[ssDE](../../includes/ssde-md.md)] statt des vollständigen kompilierten Plans einen kleinen Stub des kompilierten Plans in dem Plancache, wenn ein Batch erstmalig ausgeführt wird. Dadurch wird die Auslastung des Arbeitsspeichers reduziert, indem verhindert wird, dass der Plancache mit kompilierten Plänen gefüllt wird, die nicht wiederverwendet werden.  
  
 Der Stub des kompilierten Plans ermöglicht [!INCLUDE[ssDE](../../includes/ssde-md.md)] zu erkennen, dass dieser Ad-hoc-Batch bereits kompiliert worden ist, jedoch nur ein Stub des kompilierten Plans gespeichert worden ist, sodass [!INCLUDE[ssDE](../../includes/ssde-md.md)] den Batch kompiliert, wenn er erneut aufgerufen (kompiliert oder ausgeführt) wird, dann den Stub des kompilierten Plans aus dem Plancache entfernt und den vollständigen kompilierten Plan zum Plancache hinzufügt. 
  
 Der Stub des kompilierten Plans ist einer der cacheobjtypes, die von der sys.dm_exec_cached_plans-Katalogsicht angezeigt werden. Er verfügt über einen eindeutigen SQL-Handle und Planhandle. Dem Stub des kompilierten Plans ist kein Ausführungsplan zugeordnet, und die Abfrage des Planhandles gibt keinen XML-Showplan zurück.  
  
 [Ablaufverfolgungsflag 8032](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) setzt die Cachelimitparameter auf die RTM-Einstellung von [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] zurück, die im Allgemeinen einen größeren Cache zulässt. Verwenden Sie diese Einstellung, wenn häufig wiederverwendete Cacheeinträge nicht in den Cache passen, und wenn das Problem mit dem Plancache durch die Serverkonfigurations-Option „Optimierung für Ad-hoc-Arbeitsauslastung“ nicht behoben werden konnte.  
  
> [!WARNING]  
>  Ablaufverfolgungsflag 8032 kann die Leistung mindern, wenn große Caches weniger Arbeitsspeicher für andere Arbeitsspeicherconsumer, z. B. den Pufferpool, verfügbar machen.  

## <a name="recommendations"></a>Empfehlungen
Wenn die Anzahl von einmal genutzten Plänen einen beträchtlichen Teil des Speichers für [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] in einem OLTP-Server beansprucht, und wenn diese Pläne Ad-hoc-Pläne sind, verwenden Sie diese Serveroption, um die Speichernutzung mit diesen Objekten zu verringern.
Um die Anzahl von zwischengespeicherten einmal genutzten Plänen zu ermitteln, führen Sie die folgende Abfrage aus:

```sql
SELECT objtype, cacheobjtype, 
  AVG(usecounts) AS Avg_UseCount, 
  SUM(refcounts) AS AllRefObjects, 
  SUM(CAST(size_in_bytes AS bigint))/1024/1024 AS Size_MB
FROM sys.dm_exec_cached_plans
WHERE objtype = 'Adhoc' AND usecounts = 1
GROUP BY objtype, cacheobjtype;
```

> [!IMPORTANT]
> Wenn **Optimieren für Ad-hoc-Arbeitsauslastungen** auf 1 festgelegt wird, wirkt sich dies ausschließlich auf neue Pläne aus. Pläne, die sich bereits im Plancache befinden, sind davon nicht betroffen.
> Um bereits zwischengespeicherte Abfragepläne sofort zu beeinflussen, muss der Plancache mit [ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) gelöscht oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] neu gestartet werden.

## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)   
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  

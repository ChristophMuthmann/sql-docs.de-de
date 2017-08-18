---
title: "Für Ad-hoc-Arbeitsauslastungen optimieren (Serverkonfigurationsoption) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- optimize for ad hoc workloads option
ms.assetid: 0972e028-3a8e-454b-a186-e814a1d431f2
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 60ee2b5b7f262fb33e0cece8ae619d4b4bb1c87d
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="optimize-for-ad-hoc-workloads-server-configuration-option"></a>Für Ad-hoc-Arbeitsauslastungen optimieren (Serverkonfigurationsoption)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die Option **Optimieren für Ad-hoc-Arbeitsauslastung** wird zum Verbessern der Effizienz des Plancaches für Arbeitsauslastungen verwendet, die viele Ad-hoc-Batches für die einmalige Verwendung enthalten. Wenn diese Option auf 1 festgelegt ist, speichert [!INCLUDE[ssDE](../../includes/ssde-md.md)] statt des vollständigen kompilierten Plans einen kleinen Stub des kompilierten Plans in dem Plancache, wenn ein Batch erstmalig ausgeführt wird. Dadurch wird die Auslastung des Arbeitsspeichers reduziert, indem verhindert wird, dass der Plancache mit kompilierten Plänen gefüllt wird, die nicht wiederverwendet werden.  
  
 Der Stub des kompilierten Plans ermöglicht [!INCLUDE[ssDE](../../includes/ssde-md.md)] zu erkennen, dass dieser Ad-hoc-Batch bereits kompiliert worden ist, jedoch nur ein Stub des kompilierten Plans gespeichert worden ist, sodass [!INCLUDE[ssDE](../../includes/ssde-md.md)] den Batch kompiliert, wenn er erneut aufgerufen (kompiliert oder ausgeführt) wird, dann den Stub des kompilierten Plans aus dem Plancache entfernt und den vollständigen kompilierten Plan zum Plancache hinzufügt.  
  
 Wenn **Optimieren für Ad-hoc-Arbeitsauslastungen** auf 1 festgelegt wird, wirkt sich dies ausschließlich auf neue Pläne aus. Pläne, die sich bereits im Plancache befinden, sind davon nicht betroffen.  
  
 Der Stub des kompilierten Plans ist einer der cacheobjtypes, die von der sys.dm_exec_cached_plans-Katalogsicht angezeigt werden. Er verfügt über einen eindeutigen SQL-Handle und Planhandle. Dem Stub des kompilierten Plans ist kein Ausführungsplan zugeordnet, und die Abfrage des Planhandles gibt keinen XML-Showplan zurück.  
  
 Ablaufverfolgungsflag 8032 setzt die Cachelimitparameter auf die RTM-Einstellung von [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] zurück, die im Allgemeinen einen größeren Cache zulässt. Verwenden Sie diese Einstellung, wenn häufig wiederverwendete Cacheeinträge nicht in den Cache passen, und wenn das Problem mit dem Plancache durch die Serverkonfigurations-Option „Optimierung für Ad-hoc-Arbeitsauslastung“ nicht behoben werden konnte.  
  
> [!WARNING]  
>  Ablaufverfolgungsflag 8032 kann die Leistung mindern, wenn große Caches weniger Arbeitsspeicher für andere Arbeitsspeicherconsumer, z. B. den Pufferpool, verfügbar machen.  
  
## <a name="see-also"></a>Siehe auch  
 [sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)   
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  


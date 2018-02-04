---
title: dm_clr_tasks (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_clr_tasks
- sys.dm_clr_tasks_TSQL
- dm_clr_tasks
- dm_clr_tasks_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_clr_tasks dynamic management view
ms.assetid: 462b9061-09fa-4858-9707-03d6cc19c769
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2a3c99ffd172c97c5738ed2dd19bc8b07f303470
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmclrtasks-transact-sql"></a>sys.dm_clr_tasks (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt eine Zeile für alle CLR-Tasks (Common Language Runtime) zurück, die zurzeit ausgeführt werden. Ein [!INCLUDE[tsql](../../includes/tsql-md.md)] Batch, der einen Verweis auf eine CLR-Routine enthält erstellt einen separaten Task für die Ausführung des gesamten verwalteten Codes in diesem Batch. Mehrere Anweisungen im Batch, die die Ausführung von verwaltetem Code benötigen, verwenden denselben CLR-Task. Der CLR-Task ist zuständig für die Verwaltung von Objekten und Status bezieht sich auf die Ausführung von verwaltetem Code sowie der Übergänge zwischen der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und die common Language Runtime.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**task_address**|**varbinary(8)**|Adresse des CLR-Tasks.|  
|**sos_task_address**|**varbinary(8)**|Adresse des zugrunde liegenden [!INCLUDE[tsql](../../includes/tsql-md.md)] batchtasks.|  
|**appdomain_address**|**varbinary(8)**|Adresse der Anwendungsdomäne, in der dieser Task ausgeführt wird.|  
|**state**|**nvarchar(128)**|Aktueller Status des Tasks.|  
|**abort_state**|**nvarchar(128)**|Status, in dem sich der Abbruch zurzeit befindet (falls der Task abgebrochen wurde). Beim Abbrechen eines Tasks durchläuft dieser einen Status nach dem anderen.|  
|**type**|**nvarchar(128)**|Tasktyp.|  
|**affinity_count**|**int**|Affinität des Tasks.|  
|**forced_yield_count**|**int**|Häufigkeit, mit der der Task gezwungen war, seine Position freizugeben.|  
  
## <a name="permissions"></a>Berechtigungen  
 Auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erfordert die VIEW SERVER STATE-Berechtigung auf dem Server.  
  
 Auf [!INCLUDE[ssSDS](../../includes/sssds-md.md)] benötigen Premium-Ebenen die VIEW DATABASE STATE-Berechtigung in der Datenbank. Auf [!INCLUDE[ssSDS](../../includes/sssds-md.md)] Standard und grundlegenden Organisationsebenen erfordert die [!INCLUDE[ssSDS](../../includes/sssds-md.md)] -Administratorkonto ein.  
  
## <a name="see-also"></a>Siehe auch  
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Common Language Runtime in Verbindung mit dynamischen Verwaltungssichten &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/common-language-runtime-related-dynamic-management-views-transact-sql.md)  
  
  


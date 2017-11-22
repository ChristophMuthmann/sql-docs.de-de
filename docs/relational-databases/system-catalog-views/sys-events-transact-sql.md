---
title: Sys.Events (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.events_TSQL
- sys.events
- events_TSQL
- events
dev_langs: TSQL
helpviewer_keywords: sys.events catalog view
ms.assetid: f245a97a-80fc-43fb-a6e4-139420c9a47a
caps.latest.revision: "38"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b975acfb9ee4134eb768055bd9a012678681dc4b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="sysevents-transact-sql"></a>sys.events (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Enthält eine Zeile für jedes Ereignis, durch das ein Trigger oder eine Ereignisbenachrichtigung ausgelöst wird. Diese Ereignisse stellen die Ereignistypen, die angegeben werden, wenn der Trigger oder eine ereignisbenachrichtigung erstellt wird, mithilfe von [CREATE TRIGGER](../../t-sql/statements/create-trigger-transact-sql.md) oder [CREATE EVENT NOTIFICATION](../../t-sql/statements/create-event-notification-transact-sql.md).  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID des Triggers oder der Ereignisbenachrichtigung. Dieser Wert kennzeichnet zusammen mit **type**die Zeile eindeutig.|  
|**Typ**|**int**|Ereignis, das den Trigger auslöst.|  
|**type_desc**|**nvarchar(60)**|Beschreibung des Ereignisses, das einen Trigger auslöst.|  
|**is_trigger_event**|**bit**|1 = Triggerereignis.<br /><br /> 0 = Benachrichtigungsereignis.|  
|**event_group_type**|**int**|Ereignisgruppe, für die der Trigger oder die Ereignisbenachrichtigung erstellt wurde, bzw. NULL, wenn sie nicht für eine Ereignisgruppe erstellt wurden.|  
|**event_group_type_desc**|**nvarchar(60)**|Beschreibung der Ereignisgruppe, für die der Trigger oder die Ereignisbenachrichtigung erstellt wurde, bzw. NULL, wenn sie nicht für eine Ereignisgruppe erstellt wurden.|  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten für Objekte &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  

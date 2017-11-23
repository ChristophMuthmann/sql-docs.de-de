---
title: Sys. server_event_session_events (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- server_event_session_events
- server_event_session_events_TSQL
- sys.server_event_session_events
- sys.server_event_session_events_TSQL
dev_langs: TSQL
helpviewer_keywords:
- sys.server_event_session_events catalog view
- xe
ms.assetid: 75986e91-1fc7-4f14-98ac-4e90154a74db
caps.latest.revision: "15"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6d08bd1c56949420971b6f68828b9b0ca9387393
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="sysservereventsessionevents-transact-sql"></a>sys.server_event_session_events (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt für jedes Ereignis in einer Ereignissitzung eine Zeile zurück.  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|event_session_id|**int**|Die ID der Ereignissitzung. Lässt keine NULL-Werte zu.|  
|event_id|**int**|Die ID des Ereignisses. Diese ID ist innerhalb eines Ereignissitzungsobjekts eindeutig. Lässt keine NULL-Werte zu.|  
|name|**sysname**|Der Name des Ereignisses. Lässt keine NULL-Werte zu.|  
|Paket|**sysname**|Der Name des Pakets, welches das Ereignis enthält. Lässt keine NULL-Werte zu.|  
|Modul|**sysname**|Der Name des Moduls, welches das Ereignis enthält. Lässt keine NULL-Werte zu.|  
|predicate|**nvarchar(3000)**|Der Prädikatausdruck, der auf das Ereignis angewendet wird. Lässt NULL-Werte zu.|  
|predicate_xml|**nvarchar(3000)**|Der XML-Prädikatausdruck, der auf das Ereignis angewendet wird. Lässt NULL-Werte zu.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW SERVER STATE-Berechtigung auf dem Server.  
  
## <a name="remarks"></a>Hinweise  
 Diese Sicht hat die folgende Kardinalität der Beziehungen.  
  
||||  
|-|-|-|  
|Von|Aktion|Beziehung|  
|sys.server_event_session_events.event_session_id|Sys.server_event_sessions.event_session_id|n:1|  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Katalogsichten für erweiterte Ereignisse &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)   
 [Erweiterte Ereignisse](../../relational-databases/extended-events/extended-events.md)  
  
  

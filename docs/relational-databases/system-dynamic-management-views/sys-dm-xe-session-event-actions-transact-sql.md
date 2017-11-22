---
title: dm_xe_session_event_actions (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_xe_session_event_actions_TSQL
- sys.dm_xe_session_event_actions_TSQL
- dm_xe_session_event_actions
- sys.dm_xe_session_event_actions
dev_langs: TSQL
helpviewer_keywords:
- extended events [SQL Server], views
- sys.dm_xe_session_event_actions dynamic management view
ms.assetid: 0c22a546-683e-4c84-ab97-1e9e95304b03
caps.latest.revision: "16"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5f9c3e5f37d4a515d4a413002c09e13c0c4eb76d
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmxesessioneventactions-transact-sql"></a>sys.dm_xe_session_event_actions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt Informationen zu Ereignissitzungsaktionen zurück. Aktionen werden ausgeführt, wenn Ereignisse ausgelöst werden. Diese Verwaltungssicht aggregiert Statistiken über die Anzahl der Ausführungen einer Aktion und die Gesamtausführungszeit der Aktion.  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary(8)**|Die Speicheradresse der Ereignissitzung. Lässt keine NULL-Werte zu.|  
|action_name|**nvarchar(60)**|Der Name der Aktion. Lässt keine NULL-Werte zu.|  
|action_package_guid|**uniqueidentifier**|Die GUID für das Paket, das die Aktion enthält. Lässt keine NULL-Werte zu.|  
|event_name|**nvarchar(60)**|Der Name des Ereignisses, an das die Aktion gebunden ist Lässt keine NULL-Werte zu.|  
|event_package_guid|**uniqueidentifier**|Die GUID für das Paket, das das Ereignis enthält Lässt keine NULL-Werte zu.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW SERVER STATE-Berechtigung auf dem Server.  
  
### <a name="relationship-cardinalities"></a>Kardinalität der Beziehungen  
  
|Von|Aktion|Beziehung|  
|----------|--------|------------------|  
|sys.dm_xe_session_event_actions.event_session_address|sys.dm_xe_sessions.address|n:1|  
|sys.dm_xe_session_event_actions.action_name<br /><br /> sys.dm_xe_session_event_actions.action_package_guid|sys.dm_xe_objects.name<br /><br /> sys.dm_xe_session_events.event_package_guid|n:1|  
|sys.dm_xe_session_event_actions.event_name<br /><br /> sys.dm_xe_session_event_actions.event_package_guid|sys.dm_xe_objects.name<br /><br /> sys.dm_xe_objects.package_guid|n:1|  
  
## <a name="change-history"></a>Änderungsverlauf  
  
|Aktualisierter Inhalt|  
|---------------------|  
|Die Tabelle "Kardinalität der Beziehungen" wurde mit den richtigen Namen der dynamischen Verwaltungssicht und den richtigen Spaltennamen aktualisiert.|  
  
## <a name="see-also"></a>Siehe auch  
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  


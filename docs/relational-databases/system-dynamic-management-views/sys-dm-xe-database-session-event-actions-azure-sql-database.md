---
title: Sys.dm_xe_database_session_event_actions (Azure SQL-Datenbank) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: dmv's
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: 48519fd9-c7c2-434b-848d-ccbf41133fdd
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: e1f7ed8904d6309f015069a93a47900bc427da4d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmxedatabasesessioneventactions-azure-sql-database"></a>Sys.dm_xe_database_session_event_actions (Azure SQL-Datenbank)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Gibt Informationen zu Ereignissitzungsaktionen zurück. Aktionen werden ausgeführt, wenn Ereignisse ausgelöst werden. Diese Verwaltungssicht aggregiert Statistiken über die Anzahl der Ausführungen einer Aktion und die Gesamtausführungszeit der Aktion.  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 und alle zukünftigen Versionen.|  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary(8)**|Die Speicheradresse der Ereignissitzung. Lässt keine NULL-Werte zu.|  
|action_name|**nvarchar(60)**|Der Name der Aktion. Lässt keine NULL-Werte zu.|  
|action_package_guid|**uniqueidentifier**|Die GUID für das Paket, das die Aktion enthält. Lässt keine NULL-Werte zu.|  
|event_name|**nvarchar(60)**|Der Name des Ereignisses, an das die Aktion gebunden ist Lässt keine NULL-Werte zu.|  
|event_package_guid|**uniqueidentifier**|Die GUID für das Paket, das das Ereignis enthält Lässt keine NULL-Werte zu.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW DATABASE STATE-Berechtigung.  
  
### <a name="relationship-cardinalities"></a>Kardinalität der Beziehungen  
  
|Von|Aktion|Beziehung|  
|----------|--------|------------------|  
|Sys.dm_xe_database_session_event_actions.event_session_address|sys.dm_xe_database_sessions.address|n:1|  
|sys.dm_xe_database_session_event_actions.action_name<br /><br /> sys.dm_xe_session_event_actions.action_package_guid|sys.dm_xe_objects.name<br /><br /> sys.dm_xe_database_session_events.event_package_guid|n:1|  
|Sys.dm_xe_database_session_event_actions.event_name<br /><br /> Sys.dm_xe_database_session_event_actions.event_package_guid|sys.dm_xe_objects.name<br /><br /> sys.dm_xe_objects.package_guid|n:1|  
  
## <a name="see-also"></a>Siehe auch  
 [Erweiterte Ereignisse](../../relational-databases/extended-events/extended-events.md)  
  
  

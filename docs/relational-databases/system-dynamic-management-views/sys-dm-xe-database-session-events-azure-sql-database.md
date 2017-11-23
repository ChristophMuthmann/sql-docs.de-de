---
title: Sys.dm_xe_database_session_events (Azure SQL-Datenbank) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: 
ms.prod_service: sql-database
ms.reviewer: 
ms.service: sql-database
ms.component: dmv's
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 9e985a19-f93f-4c56-b644-12c529298011
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f2381dff2f63662f17712271be6327aeed73d26c
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmxedatabasesessionevents-azure-sql-database"></a>Sys.dm_xe_database_session_events (Azure SQL-Datenbank)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Gibt Informationen zu Sitzungsereignissen zurück. Ereignisse sind einzelne Ausführungspunkte. Auf Ereignisse können Prädikate angewendet werden, damit sie nicht mehr ausgelöst werden, wenn sie nicht die erforderlichen Informationen enthalten.  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 und alle späteren Versionen.|  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary(8)**|Die Speicheradresse der Ereignissitzung. Lässt keine NULL-Werte zu.|  
|event_name|**nvarchar(60)**|Der Name des Ereignisses, an das eine Aktion gebunden ist. Lässt keine NULL-Werte zu.|  
|event_package_guid|**uniqueidentifier**|Die GUID für das Paket, das das Ereignis enthält. Lässt keine NULL-Werte zu.|  
|event_predicate|**nvarchar(2048)**|Eine XML-Darstellung der Prädikatstruktur, die auf das Ereignis angewendet wird. Lässt NULL-Werte zu.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW DATABASE STATE-Berechtigung.  
  
### <a name="relationship-cardinalities"></a>Kardinalität der Beziehungen  
  
|Von|Aktion|Beziehung|  
|----------|--------|------------------|  
|Sys.dm_xe_database_session_events.event_session_address|Sys.dm_xe_database_sessions.Address|n:1|  
|Sys.dm_xe_database_session_events.event_package_guid, sys.dm_xe_database_session_events.event_name|sys.dm_xe_objects.name, sys.dm_xe_objects.package_guid|n:1|  
  
  

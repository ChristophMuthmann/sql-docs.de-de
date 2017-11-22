---
title: Sys.database_event_session_events (Azure SQL-Datenbank) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.reviewer: 
ms.service: 
ms.component: system-catalog-views
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: Azure SQL Database
ms.assetid: f4c9eb0a-173c-4c66-8dd8-6f7176b2657f
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: deb6b14739b47dda369c457ad7a2bddc70ca3fcc
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysdatabaseeventsessionevents-azure-sql-database"></a>Sys.database_event_session_events (Azure SQL-Datenbank)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Gibt für jedes Ereignis in einer Ereignissitzung eine Zeile zurück.  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 und alle späteren Versionen.|  
  
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
 Erfordert die VIEW DATABASE STATE-Berechtigung auf dem Server.  
  
## <a name="remarks"></a>Hinweise  
 Diese Sicht hat die folgende Kardinalität der Beziehungen.  
  
||||  
|-|-|-|  
|Von|Aktion|Beziehung|  
|Sys.database_event_session_events.event_session_id|Sys.database_event_sessions.event_session_id|n:1|  
  
## <a name="see-also"></a>Siehe auch  
 [Erweiterte Ereignisse](../../relational-databases/extended-events/extended-events.md)  
  
  

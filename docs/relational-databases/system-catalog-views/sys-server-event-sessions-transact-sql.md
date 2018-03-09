---
title: Sys. server_event_sessions (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- server_event_sessions
- server_event_sessions_TSQL
- sys.server_event_sessions_TSQL
- sys.server_event_sessions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_event_sessions catalog view
- xe
ms.assetid: 796f3093-6a3e-4d67-8da6-b9810ae9ef5b
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fd3b975a1f19481a2a6ee4c5efcd2cfd4558cf1a
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="sysservereventsessions-transact-sql"></a>sys.server_event_sessions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Listet alle Ereignissitzungsdefinitionen auf, die in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vorhanden sind.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|event_session_id|**int**|Die eindeutige ID der Ereignissitzung. Lässt keine NULL-Werte zu.|  
|name|**sysname**|Der benutzerdefinierte Name zum Identifizieren der Ereignissitzung. Name ist eindeutig. Lässt keine NULL-Werte zu.|  
|event_retention_mode|**NCHAR(1)-Wert**|Bestimmt, wie Ereignisverluste behandelt werden. Der Standardwert ist S. NULL ist nicht zulässig. Ist einer der folgenden Werte:<br /><br /> S. Zugeordnet zu Event_retention_mode_desc = ALLOW_SINGLE_EVENT_LOSS<br /><br /> M. Zugeordnet zu Event_retention_mode_desc = ALLOW_MULTIPLE_EVENT_LOSS<br /><br /> N. Zugeordnet zu Event_retention_mode_desc = NO_EVENT_LOSS|  
|event_retention_mode_desc|**sysname**|Beschreibt, wie Ereignisverluste behandelt werden. Der Standardwert ist ALLOW_SINGLE_EVENT_LOSS. Lässt keine NULL-Werte zu. Ist einer der folgenden Werte:<br /><br /> ALLOW_SINGLE_EVENT_LOSS. Ereignisse der Sitzung dürfen verloren gehen. Einzelne Ereignisse werden nur gelöscht, wenn alle Ereignispuffer gefüllt sind. Wenn bei gefüllten Ereignispuffern nur einzelne Ereignisse verloren gehen, sind akzeptable [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Leistungsmerkmale möglich, während Datenverluste im verarbeiteten Ereignisdatenstrom minimiert werden.<br /><br /> ALLOW_MULTIPLE_EVENT_LOSS. Volle Ereignispuffer dürfen in der Sitzung verloren gehen. Die Anzahl verloren gegangener Ereignisse hängt von der Größe des Speichers ab, der der Sitzung zugeordnet ist, der Partitionierung des Speichers und der Größe der Ereignisse im Puffer. Mit dieser Option wird Serverleistung nur minimal beeinträchtigt, wenn Ereignispuffer schnell gefüllt werden. Es können jedoch zahlreiche Ereignisse der Sitzung verloren gehen.<br /><br /> NO_EVENT_LOSS. Verluste von Ereignissen sind nicht zulässig. Diese Option stellt sicher, dass alle ausgelösten Ereignisse beibehalten werden. Wenn diese Option verwendet wird, müssen alle Tasks, die Ereignisse auslösen, warten, bis in einem Ereignispuffer Platz verfügbar wird. Dies kann zu einem spürbaren Zurückgehen der Leistung führen, während die Ereignissitzung aktiv ist.|  
|max_dispatch_latency|**int**|Gibt in Millisekunden an, wie lange Ereignisse zwischengespeichert werden, bevor sie an Sitzungsziele gesendet werden. Gültige Werte liegen zwischen 1 bis 2147483648 und -1. Der Wert -1 gibt an, dass die Sendelatenzzeit unendlich ist. Lässt NULL-Werte zu.|  
|max_memory|**int**|Die Größe des Arbeitsspeichers, der der Sitzung für die Ereignispufferung zugeordnet wird. Der Standardwert ist 4 MB. Lässt NULL-Werte zu.|  
|max_event_size|**int**|Der Arbeitsspeicher, der für Ereignisse reserviert wird, die nicht in Ereignissitzungspuffer passen. Wenn max_event_size die berechnete Puffergröße überschreitet, werden für die Ereignissitzung zwei zusätzliche Puffer für max_event_size zugeordnet. Lässt NULL-Werte zu.|  
|memory_partition_mode|**NCHAR(1)-Wert**|Die Position im Arbeitsspeicher, an der Ereignispuffer erstellt werden. Der Standardpartitionsmodus ist G. NULL ist nicht zulässig. MEMORY_PARTITION_MODE sind möglich:<br /><br /> G - NONE<br /><br /> C - PER_CPU<br /><br /> N - PER_NODE|  
|memory_partition_mode_desc|**sysname**|Der Standardwert ist NONE. Lässt keine NULL-Werte zu. Ist einer der folgenden Werte:<br /><br /> NONE. Innerhalb einer SQL Server-Instanz wird ein einzelner Satz von Puffern erstellt.<br /><br /> PER_CPU. Ein Satz von Puffern wird für jede CPU erstellt.<br /><br /> PER_NODE. Ein Satz von Puffern wird für jeden nicht einheitlichen Speicherzugriffsknoten (Non-Uniform Memory Access, NUMA) erstellt.|  
|track_causality|**bit**|Aktiviert oder deaktiviert die Kausalitätsverfolgung. Bei einem Wert von 1 (ON) ist die Verfolgung aktiviert, und ähnliche Ereignisse auf verschiedenen Serververbindungen können korreliert werden. Die Standardeinstellung ist 0 (OFF). Lässt keine NULL-Werte zu.|  
|startup_state|**bit**|Der Wert bestimmt, ob die Sitzung beim Start des Servers automatisch gestartet wird. Die Standardeinstellung ist 0. Lässt keine NULL-Werte zu. kann einen der folgenden Werte aufweisen:<br /><br /> 0 (OFF). Die Sitzung wird beim Start des Servers nicht gestartet.<br /><br /> 1 (ON). Die Ereignissitzung wird beim Start des Servers gestartet.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW SERVER STATE-Berechtigung auf dem Server.  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Katalogsichten für erweiterte Ereignisse &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)   
 [Erweiterte Ereignisse](../../relational-databases/extended-events/extended-events.md)  
  
  

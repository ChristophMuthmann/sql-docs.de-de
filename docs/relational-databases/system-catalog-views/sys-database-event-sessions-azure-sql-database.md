---
title: Sys.database_event_sessions (Azure SQL-Datenbank) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: system-catalog-views
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: 02c2cd71-d35e-4d4c-b844-92b240f768f4
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 4af0c2866cd7dcb00feca99ad14b0fa6a80c21b4
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="sysdatabaseeventsessions-azure-sql-database"></a>Sys.database_event_sessions (Azure SQL-Datenbank)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Listet alle ereignissitzungsdefinitionen auf, die in der aktuellen Datenbank vorhanden, im sind [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
> [!NOTE]  
>  Ähnliche-Katalogsicht, das mit dem Namen `sys.server_event_sessions` gilt nur für [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)], und alle späteren Versionen.|  
  
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
  
  

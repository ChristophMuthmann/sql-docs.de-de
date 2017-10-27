---
title: Catalog. execution_component_phases | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 07a9a163-4787-40f7-b371-ac5c6cb4b095
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: c3e47e4a5ae297202ba43679fba393421880a7ea
ms.openlocfilehash: b3459ce6d7e9eb0b9580ffa54e3b87e16f3e8fb0
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="catalogexecutioncomponentphases"></a>catalog.execution_component_phases
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Zeigt die von einer Datenflusskomponente in jeder Ausführungsphase benötigte Zeit an.  
  
|Spaltenname|Datentyp|Beschreibung|  
|-----------------|---------------|-----------------|  
|phase_stats_id|**bigint**|Eindeutiger Bezeichner (ID) der Phase.|  
|execution_id|**bigint**|Eindeutige ID für die Instanz der Ausführung.|  
|package_name|**nvarchar(260)**|Der Name des ersten Pakets, das während der Ausführung gestartet wurde.|  
|task_name|**nvarchar(4000)**|Der Name des Datenflusstask.|  
|subcomponent_name|**nvarchar(4000)**|Der Name der Datenflusskomponente.|  
|phase|**vom Datentyp nvarchar(128)**|Der Name der Ausführungsphase.|  
|start_time|**DateTimeOffset(7)**|Der Zeitpunkt, zu dem die Phase gestartet wurde.|  
|end_time|**DateTimeOffset(7)**|Der Zeitpunkt, zu dem die Phase beendet wurde.|  
|execution_path|**nvarchar(max)**|Der Ausführungspfad der Datenflusstask.|  
  
## <a name="remarks"></a>Hinweise  
 In dieser Sicht wird für jede Ausführungsphase einer Datenflusskomponente eine Zeile angezeigt, z. B. Überprüfen, Vor der Ausführung, Nach der Ausführung, PrimeOutput und ProcessInput. Jede Zeile zeigt die Start- und Endzeit einer bestimmten Ausführungsphase an.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird die catalog.execution_component_phases-Sicht verwendet, um die Gesamtzeit zu suchen, die für die Ausführung eines bestimmten Pakets in allen Phasen benötigt wurde (**active_time**), sowie die insgesamt verstrichene Zeit für das Paket (**total_time**).  
  
> [!WARNING]  
>  Die catalog.execution_component_phases-Sicht enthält diese Informationen, wenn der Protokolliergrad der Paketausführung auf "Leistung" oder "Ausführlich" festgelegt wird. Weitere Informationen finden Sie unter [Enable Logging for Package Execution on the SSIS Server](../../integration-services/performance/integration-services-ssis-logging.md#server_logging).  
  
```sql
use SSISDB  
select package_name, task_name, subcomponent_name, execution_path,  
    SUM(DATEDIFF(ms,start_time,end_time)) as active_time,  
    DATEDIFF(ms,min(start_time), max(end_time)) as total_time  
from catalog.execution_component_phases  
where execution_id = 1841  
group by package_name, task_name, subcomponent_name, execution_path  
order by package_name, task_name, subcomponent_name, execution_path  
```  
  
## <a name="permissions"></a>Berechtigungen  
 Diese Sicht erfordert eine der folgenden Berechtigungen:  
  
-   READ-Berechtigung für die Instanz der Ausführung  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
  
> [!NOTE]  
>  Wenn Sie über die Berechtigung verfügen, einen Vorgang auf dem Server auszuführen, verfügen Sie auch über die Berechtigung, Informationen zu dem Vorgang anzuzeigen. Sicherheit auf Zeilenebene wird erzwungen. Es werden nur Zeilen angezeigt, zu deren Anzeige Sie berechtigt sind.  
  
  

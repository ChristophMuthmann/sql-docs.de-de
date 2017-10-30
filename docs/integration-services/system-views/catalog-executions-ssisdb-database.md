---
title: Catalog.executions (SSISDB-Datenbank) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- executions view [Integration Services]
- catalog.executions view [Integration Services]
ms.assetid: 879f13b0-331d-4dee-a079-edfaca11ae5b
caps.latest.revision: 32
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 5e60664352054cd8f62250cc7c6b8082e84f607f
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="catalogexecutions-ssisdb-database"></a>catalog.executions (SSISDB-Datenbank)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Zeigt die Instanzen der Paketausführung im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog an. Die Ausführung von Paketen mit dem Task "Paket ausführen" erfolgt in der gleichen Ausführungsinstanz wie die Ausführung des übergeordneten Pakets.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|execution_id|**bigint**|Der eindeutige Bezeichner (ID) der Ausführungsinstanz.|  
|Ordnername|**sysname(nvarchar(128))**|Der Name des Ordners, der das Projekt enthält.|  
|PROJECT_NAME|**sysname(nvarchar(128))**|Der Name des Projekts.|  
|package_name|**nvarchar(260)**|Der Name des ersten Pakets, das während der Ausführung gestartet wurde.|  
|reference_id|**bigint**|Die Umgebung, auf die von der Instanz der Ausführung verwiesen wird.|  
|reference_type|**char(1)**|Gibt an, ob sich die Umgebung im gleichen Ordner wie das Projekt (relativer Verweis) oder in einem anderen Ordner (absoluter Verweis) befinden kann. Wenn der Wert `R`ist, wird der Speicherort der Umgebung mit einem relativen Verweis angegeben. Wenn der Wert `A`ist, wird die Umgebung mit einem absoluten Verweis angegeben.|  
|environment_folder_name|**vom Datentyp nvarchar(128)**|Der Name des Ordners, der die Umgebung enthält.|  
|environment_name|**vom Datentyp nvarchar(128)**|Der Name der Umgebung, auf die während der Ausführung verwiesen wurde.|  
|project_lsn|**bigint**|Die Version des Projekts, die der Instanz der Ausführung entspricht. Diese Nummer ist nicht unbedingt eine fortlaufende Nummer.|  
|executed_as_sid|**varbinary (85)**|Die SID des Benutzers, der die Instanz der Ausführung gestartet hat.|  
|executed_as_name|**vom Datentyp nvarchar(128)**|Der Name des Datenbankprinzipals, mit dem die Instanz der Ausführung gestartet wurde.|  
|use32bitruntime|**bit**|Gibt an, ob die 32-Bit-Laufzeit verwendet wird, um das Paket unter einem 64-Bit-Betriebssystem auszuführen. Wenn der Wert ist `1`, die Ausführung mit der 32-Bit-Laufzeit ausgeführt wird. Wenn der Wert `0` ist, erfolgt die Ausführung mit der 64-Bit-Laufzeit.|  
|object_type|**smallint**|Der Typ des Objekts. Das Objekt kann ein Projekt (`20`) oder ein Paket (`30`) sein.|  
|object_id|**bigint**|Die ID des von dem Vorgang betroffenen Objekts.|  
|status|**int**|Der Status des Vorgangs. Die möglichen Werte lauten "erstellt" (`1`), "wird ausgeführt" (`2`), "abgebrochen" (`3`), "fehlerhaft" (`4`), "ausstehend" (`5`), "unerwartet beendet" (`6`), "erfolgreich" (`7`), "wird beendet" (`8`) und "abgeschlossen" (`9`).|  
|start_time|**datetimeoffset**|Der Zeitpunkt, zu dem die Instanz der Ausführung gestartet wurde.|  
|end_time|**datetimeoffsset**|Der Zeitpunkt, zu dem die Instanz der Ausführung beendet wurde.|  
|caller_sid|**varbinary (85)**|Die Sicherheits-ID (SID) des Benutzers, wenn für die Anmeldung Windows-Authentifizierung verwendet wurde.|  
|caller_name|**vom Datentyp nvarchar(128)**|Der Name des Kontos, das den Vorgang ausgeführt hat.|  
|process_id|**int**|Ggf. die Prozess-ID des externen Prozesses.|  
|stopped_by_sid|**varbinary (85)**|Die Sicherheits-ID (SID) des Benutzers, der die Instanz der Ausführung beendet hat.|  
|stopped_by_name|**vom Datentyp nvarchar(128)**|Der Name des Benutzers, der die Instanz der Ausführung beendet hat.|  
|total_physical_memory_kb|**bigint**|Der gesamte physische Speicher (in Megabyte) auf dem Server, wenn die Ausführung gestartet wird.|  
|available_physical_memory_kb|**bigint**|Der verfügbare physische Speicher (in Megabyte) auf dem Server, wenn die Ausführung gestartet wird.|  
|total_page_file_kb|**bigint**|Der gesamte Arbeitsspeicher für Seiten (in Megabyte) auf dem Server, wenn die Ausführung gestartet wird.|  
|available_page_file_kb|**bigint**|Der verfügbare Arbeitsspeicher für Seiten (in Megabyte) auf dem Server, wenn die Ausführung gestartet wird.|  
|cpu_count|**int**|Die Anzahl der logischen CPUs auf dem Server, wenn die Ausführung gestartet wird.|  
|server_name|**vom Datentyp nvarchar(128)**|Informationen zu Windows Server- und Instanznamen für eine angegebene Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|machine_name|**vom Datentyp nvarchar(128)**|Der Name des Computers, auf dem die Serverinstanz ausgeführt wird.|  
|dump_id|**uniqueidentifier**|Die ID eines Ausführungsdumps.|  
  
## <a name="remarks"></a>Hinweise  
 In dieser Sicht wird eine Zeile für jede Instanz der Ausführung im Katalog angezeigt.  
  
## <a name="permissions"></a>Berechtigungen  
 Diese Sicht erfordert eine der folgenden Berechtigungen:  
  
-   READ-Berechtigung für die Instanz der Ausführung  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
  
> [!NOTE]  
>  Sicherheit auf Zeilenebene wird erzwungen. Es werden nur Zeilen angezeigt, zu deren Anzeige Sie berechtigt sind.  
  
  


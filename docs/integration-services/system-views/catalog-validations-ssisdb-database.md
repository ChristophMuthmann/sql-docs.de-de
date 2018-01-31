---
title: catalog.validations (SSISDB-Datenbank) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: dbafe110-b480-48f3-b45f-31d71ca68f62
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8c5a94903b6cac800063e9c6c437dc1926385976
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="catalogvalidations-ssisdb-database"></a>catalog.validations (SSISDB-Datenbank)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Zeigt die Details aller Projekt- und Paketüberprüfungen im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog an.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|validation_id|**bigint**|Der eindeutige Bezeichner (ID) der Überprüfung.|  
|environment_scope|**Char(1)**|Gibt die Umgebungsverweise an, die bei der Überprüfung beachtet werden. Wenn der Wert `A` ist, werden alle dem Projekt zugeordneten Umgebungsverweise in die Überprüfung eingeschlossen. Wenn der Wert `S` ist, wird nur ein einzelner Umgebungsverweis eingeschlossen. Wenn der Wert `D` ist, werden keine Umgebungsverweise eingeschlossen, und jeder Parameter muss für eine erfolgreiche Überprüfung über einen Standardliteralwert verfügen.|  
|validate_type|**Char(1)**|Der Typ der auszuführenden Überprüfung. Die möglichen Typen der Überprüfung sind Abhängigkeitsüberprüfung (`D`) und vollständige Überprüfung (`F`). Die Paketüberprüfung ist immer eine vollständige Überprüfung.|  
|folder_name|**nvarchar(128)**|Der Name des Ordners, der das entsprechende Projekt enthält.|  
|project_name|**nvarchar(128)**|Der Name des Projekts.|  
|project_lsn|**bigint**|Die Version des Projekts, anhand dessen überprüft wird.|  
|use32bitruntime|**bit**|Gibt an, ob die 32-Bit-Laufzeit verwendet wird, um das Paket unter einem 64-Bit-Betriebssystem auszuführen. Wenn der Wert `1` ist, erfolgt die Ausführung mit der 32-Bit-Runtime. Wenn der Wert `0` ist, erfolgt die Ausführung mit der 64-Bit-Laufzeit.|  
|reference_id|**bigint**|Eindeutige ID des Projektumgebungsverweises, mit dem das Projekt auf eine Umgebung verweist.|  
|operation_type|**smallint**|Der Typ des Vorgangs. Die in dieser Sicht angezeigten Vorgänge umfassen Projektüberprüfung und (`300`) Paketüberprüfung (`301`).|  
|object_name|**nvarhcar(260)**|Der Name des Objekts.|  
|object_type|**smallint**|Der Typ des Objekts. Das Objekt kann ein Projekt (`20`) oder ein Paket (`30`) sein.|  
|object_id|**bigint**|Die ID des von dem Vorgang betroffenen Objekts.|  
|start_time|**datetimeoffset(7)**|Der Zeitpunkt, zu dem der Vorgang begonnen wurde.|  
|end_time|**datetimeoffsset(7)**|Der Zeitpunkt, zu dem der Vorgang beendet wurde.|  
|status|**int**|Der Status des Vorgangs. Die möglichen Werte lauten "erstellt" (`1`), "wird ausgeführt" (`2`), "abgebrochen" (`3`), "fehlerhaft" (`4`), "ausstehend" (`5`), "unerwartet beendet" (`6`), "erfolgreich" (`7`), "wird beendet" (`8`) und "abgeschlossen" (`9`).|  
|caller_sid|**varbinary(85)**|Die Sicherheits-ID (SID) des Benutzers, wenn für die Anmeldung Windows-Authentifizierung verwendet wurde.|  
|caller_name|**nvarchar(128)**|Der Name des Kontos, das den Vorgang ausgeführt hat.|  
|process_id|**int**|Ggf. die Prozess-ID des externen Prozesses.|  
|stopped_by_sid|**varbinary(85)**|Die SID des Benutzers, der den Vorgang beendet hat.|  
|stopped_by_name|**nvarchar(128)**|Der Name des Benutzers, der den Vorgang beendet hat.|  
|server_name|**nvarchar(128)**|Die Informationen zu Windows Server und zu Instanzen für eine angegebene Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|machine_name|**nvarchar(128)**|Der Name des Computers, auf dem die Serverinstanz ausgeführt wird.|  
|dump_id|**uniqueidentifier**|Die ID des Ausführungsdumps.|  
  
## <a name="remarks"></a>Remarks  
 In dieser Sicht wird eine Zeile für jede Überprüfung im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog angezeigt.  
  
## <a name="permissions"></a>Berechtigungen  
 Diese Sicht erfordert eine der folgenden Berechtigungen:  
  
-   READ-Berechtigung für den entsprechenden Vorgang  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
  
> [!NOTE]  
>  Wenn Sie über die Berechtigung verfügen, einen Vorgang auf dem Server auszuführen, verfügen Sie auch über die Berechtigung, Informationen zu dem Vorgang anzuzeigen. Sicherheit auf Zeilenebene wird erzwungen. Es werden nur Zeilen angezeigt, zu deren Anzeige Sie berechtigt sind.  
  
  

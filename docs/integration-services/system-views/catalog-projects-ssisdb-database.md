---
title: Catalog.Projects (SSISDB-Datenbank) | Microsoft Docs
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
ms.assetid: a6b595e1-5227-47ce-8ee2-a28c1e1d5645
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 668890ae464deb8dfa029eab38b608fee12af0ca
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="catalogprojects-ssisdb-database"></a>catalog.projects (SSISDB-Datenbank)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Zeigt die Details für alle Projekte an, die im **SSISDB** -Katalog angezeigt werden.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|project_id|**bigint**|Der eindeutige Bezeichner (ID) des Projekts.|  
|folder_id|**bigint**|Die eindeutige ID des Ordners, in dem sich das Projekt befindet.|  
|name|**sysname**|Der Name des Projekts.|  
|Beschreibung|**nvarchar(1024)**|Die optionale Beschreibung des Projekts.|  
|project_format_version|**int**|Die Version des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , die zum Entwickeln des Projekts verwendet wurde.|  
|deployed_by_sid|**varbinary (85)**|Die Sicherheits-ID (SID) des Benutzers, der das Projekt installiert hat.|  
|deployed_by_name|**vom Datentyp nvarchar(128)**|Der Name des Benutzers, der das Projekt installiert hat.|  
|last_deployed_time|**DateTimeOffset(7)**|Datum und Uhrzeit der Bereitstellung oder erneuten Bereitstellung des Projekts.|  
|created_time|**DateTimeOffset(7)**|Datum und Uhrzeit der Projekterstellung.|  
|"object_version_lsn"|**bigint**|Die Version des Projekts. Diese Nummer ist nicht unbedingt eine fortlaufende Nummer.|  
|validation_status|**char(1)**|Der Überprüfungsstatus.|  
|last_validation_time|**DateTimeOffset(7)**|Der Zeitpunkt der letzten Überprüfung.|  
  
## <a name="remarks"></a>Hinweise  
 In dieser Sicht wird eine Zeile für jedes Projekt im Katalog angezeigt.  
  
## <a name="permissions"></a>Berechtigungen  
 Diese Sicht erfordert eine der folgenden Berechtigungen:  
  
-   READ-Berechtigung für das Projekt  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
  
> [!NOTE]  
>  Wenn Sie über die READ-Berechtigung für ein Projekt verfügen, verfügen Sie auch über die READ-Berechtigung für alle Pakete und Umgebungsverweise, die diesem Projekt zugeordnet sind. Sicherheit auf Zeilenebene wird erzwungen. Es werden nur Zeilen angezeigt, zu deren Anzeige Sie berechtigt sind.  
  
  


---
title: catalog.packages (SSISDB-Datenbank) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: system-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- packages view [Integration Services]
- catalog.packages view [Integration Services]
ms.assetid: a634e94d-f492-4dfd-9611-a35f545106a1
caps.latest.revision: 32
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f794745ed1482f1d4978f775f6f001478a2c0a28
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="catalogpackages-ssisdb-database"></a>catalog.packages (SSISDB-Datenbank)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Zeigt die Details für alle Pakete an, die im **SSISDB** -Katalog angezeigt werden.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|package_id|**bigint**|Der eindeutige Bezeichner (ID) des Pakets.|  
|NAME|**nvarchar(256)**|Der eindeutige Name des Pakets.|  
|package_guid|**uniqueidentifier**|Der global eindeutige Bezeichner (Globally Unique Identifier, GUID) für das Paket.|  
|description|**nvarchar(1024)**|Eine optionale Beschreibung des Pakets.|  
|package_format_version|**int**|Die Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], mit der das Paket entwickelt wurde.|  
|version_major|**int**|Die Hauptversion des Pakets.|  
|version_minor|**int**|Die Nebenversion des Pakets.|  
|version_build|**int**|Die Buildversion des Pakets.|  
|version_comments|**nvarchar(1024)**|Optionale Kommentare zur Paketversion.|  
|version_guid|**uniqueidentifier**|Die GUID, die die Paketversion eindeutig identifiziert.|  
|project_id|**bigint**|Die eindeutige ID des Projekts.|  
|entry_point|**bit**|Der Wert `1` gibt an, dass das Paket direkt gestartet werden soll. Der Wert `0` gibt an, dass das Paket von einem anderen Paket mit dem Task Paket ausführen gestartet werden soll. Der Standardwert lautet `1`.|  
|validation_status|**char(1)**|Der Status der Überprüfung.|  
|last_validation_time|**datetimeoffset(7)**|Der Zeitpunkt der letzten Überprüfung.|  
  
## <a name="remarks"></a>Remarks  
 In dieser Sicht wird eine Zeile für jedes Paket im Katalog angezeigt.  
  
## <a name="permissions"></a>Berechtigungen  
 Diese Sicht erfordert eine der folgenden Berechtigungen:  
  
-   READ-Berechtigung für das entsprechende Projekt  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
  
> [!NOTE]  
>  Wenn Sie über die READ-Berechtigung für ein Projekt verfügen, verfügen Sie auch über die READ-Berechtigung für alle Pakete und Umgebungsverweise, die diesem Projekt zugeordnet sind. Sicherheit auf Zeilenebene wird erzwungen. Es werden nur Zeilen angezeigt, zu deren Anzeige Sie berechtigt sind.  
  
  

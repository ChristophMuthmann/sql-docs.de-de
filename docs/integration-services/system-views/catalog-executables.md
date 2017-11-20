---
title: Catalog.Executables | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
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
ms.assetid: bae22d0c-e190-426f-a074-c1d1170e8dd8
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: aa0d2d5df7c3c39b1ad33794ae11c1a34ffe72d4
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="catalogexecutables"></a>catalog.executables
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  In dieser Sicht wird eine Zeile für jede ausführbare Datei in der angegebenen Ausführung angezeigt.  
  
 Eine ausführbare Datei ist ein Task oder ein Container, den Sie der Ablaufsteuerung eines Pakets hinzufügen.  
  
|Spaltenname|**Datentyp**|Description|  
|-----------------|-------------------|-----------------|  
|executable_id|**bigint**|Der eindeutige Bezeichner für die ausführbare Datei.|  
|execution_id|**bigint**|Der eindeutige Bezeichner für die Instanz der Ausführung.|  
|executable_name|**nvarchar(4000)**|Der Name der ausführbaren Datei.|  
|executable_guid|**nvarchar(38)**|Die GUID der ausführbaren Datei.|  
|package_name|**nvarchar(260)**|Der Name des Pakets.|  
|package_path|**nvarchar(max)**|Der Pfad des Pakets.|  
  
## <a name="permissions"></a>Berechtigungen  
 Diese Sicht erfordert eine der folgenden Berechtigungen:  
  
-   READ-Berechtigung für die Instanz der Ausführung  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
  
> [!NOTE]  
>  Wenn Sie über die Berechtigung verfügen, einen Vorgang auf dem Server auszuführen, verfügen Sie auch über die Berechtigung, Informationen zu dem Vorgang anzuzeigen. Sicherheit auf Zeilenebene wird erzwungen. Es werden nur Zeilen angezeigt, zu deren Anzeige Sie berechtigt sind.  
  
## <a name="remarks"></a>Hinweise  
  


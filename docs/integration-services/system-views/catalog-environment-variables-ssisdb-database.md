---
title: Catalog. environment_variables (SSISDB-Datenbank) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 45f5aacd-505a-443b-8fc2-c7929e78cff8
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 40e31b9697c453f6a9d60dfcc8d9302dfefe0ac4
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="catalogenvironmentvariables-ssisdb-database"></a>catalog.environment_variables (SSISDB-Datenbank)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Zeigt die umgebungsvariablendetails für alle Umgebungen, in der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Katalog.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|variable_id|**bigint**|Der eindeutige Bezeichner (ID) der Umgebungsvariablen.|  
|environment_id|**bigint**|Die eindeutige ID der Umgebung, der die Variable zugeordnet ist.|  
|name|**sysname**|Der Name der Umgebungsvariablen.|  
|Beschreibung|**nvarchar(1024)**|Die Beschreibung der Umgebungsvariablen.|  
|Typ|**vom Datentyp nvarchar(128)**|Der Datentyp der Umgebungsvariablen.|  
|sensitive|**bit**|Wenn der Wert `1`lautet, ist die Variable vertraulich und wird beim Speichern verschlüsselt. Lautet der Wert `0`, ist die Variable nicht vertraulich, und der Wert wird als Nur-Text gespeichert.|  
|value|**sql_variant**|Der Wert der Umgebungsvariablen. Wenn vertrauliche ist `0`, die nur-Text-Wert wird angezeigt. Wenn vertrauliche ist `1`, **NULL** Wert wird angezeigt.|  
  
## <a name="remarks"></a>Hinweise  
 In dieser Sicht wird eine Zeile für jede Umgebungsvariable im Katalog angezeigt.  
  
## <a name="permissions"></a>Berechtigungen  
 Diese Sicht erfordert eine der folgenden Berechtigungen:  
  
-   READ-Berechtigung für die entsprechende Umgebung  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
  
> [!NOTE]  
>  Wenn Sie über die Berechtigung verfügen, einen Vorgang auf dem Server auszuführen, verfügen Sie auch über die Berechtigung, Informationen zu dem Vorgang anzuzeigen. Sicherheit auf Zeilenebene wird erzwungen. Es werden nur Zeilen angezeigt, zu deren Anzeige Sie berechtigt sind.  
  
  


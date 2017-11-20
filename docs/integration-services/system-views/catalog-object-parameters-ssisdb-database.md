---
title: Catalog. object_parameters (SSISDB-Datenbank) | Microsoft Docs
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
ms.assetid: d7b04903-2d61-4159-9456-475942d1f732
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9d538e5b55ef4e8880afb2d008b11c17d9a03189
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="catalogobjectparameters-ssisdb-database"></a>catalog.object_parameters (SSISDB-Datenbank)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Zeigt die Parameter für alle Pakete und Projekte in der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Katalog.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|parameter_id|**bigint**|Der eindeutige Bezeichner (ID) des Parameters.|  
|project_id|**bigint**|Die eindeutige ID des Projekts.|  
|object_type|**smallint**|Der Typ des Parameters. Für einen Projektparameter ist der Wert `20` , und für einen Paketparameter ist der Wert `30` .|  
|object_name|**sysname**|Der Name des entsprechenden Projekts oder Pakets.|  
|parameter_name|**sysname(nvarchar(128))**|Der Name des Parameters.|  
|data_type|**vom Datentyp nvarchar(128)**|Der Datentyp des Parameters.|  
|erforderlich|**bit**|Wenn der Wert `1`lautet, ist der Parameterwert erforderlich, um die Ausführung zu starten. Wenn der Wert `0`lautet, ist der Parameterwert nicht erforderlich, um die Ausführung zu starten.|  
|sensitive|**bit**|Wenn der Wert `1`lautet, ist der Parameterwert vertraulich. Wenn der Wert `0`lautet, ist der Parameterwert nicht vertraulich.|  
|Beschreibung|**nvarchar(1024)**|Eine optionale Beschreibung des Pakets.|  
|design_default_value|**sql_variant**|Der Standardwert für den Parameter, der während des Entwurfs des Projekts oder Pakets zugewiesen wurde.|  
|default_value|**sql_variant**|Der Standardwert, der derzeit auf dem Server verwendet wird.|  
|value_type|**char(1)**|Gibt den Typ des Parameterwerts an. Dieses Feld zeigt `V` Wenn Parameter_value ein Literalwert ist und `R` Wenn der Wert durch Verweisen auf eine Umgebungsvariable zugewiesen wird.|  
|value_set|**bit**|Wenn der Wert `1`ist, wurde der Parameterwert zugewiesen. Wenn der Wert `0`ist, wurde der Parameterwert nicht zugewiesen.|  
|referenced_variable_name|**vom Datentyp nvarchar(128)**|Der Name der Umgebungsvariablen, die dem Wert des Parameters zugewiesen wird. Der Standardwert ist **NULL**.|  
|validation_status|**char(1)**|Nur für Informationszwecke identifiziert. Nicht im verwendet [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|last_validation_time|**DateTimeOffset(7)**|Nur für Informationszwecke identifiziert. Nicht im verwendet [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
  
## <a name="permissions"></a>Berechtigungen  
 Zum Anzeigen von Zeilen in dieser Sicht benötigten Sie eine der folgenden Berechtigungen:  
  
-   READ-Berechtigung für das Projekt  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
  
 Sicherheit auf Zeilenebene wird erzwungen. Es werden nur Zeilen angezeigt, zu deren Anzeige Sie berechtigt sind.  
  
  


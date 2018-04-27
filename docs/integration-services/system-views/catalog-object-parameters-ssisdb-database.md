---
title: catalog.object_parameters (SSISDB-Datenbank) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/04/2017
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
ms.assetid: d7b04903-2d61-4159-9456-475942d1f732
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4d8ed8dd1f14990107d7dc7d7ec27e70eb13151b
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="catalogobjectparameters-ssisdb-database"></a>catalog.object_parameters (SSISDB-Datenbank)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Zeigt die Parameter für alle Pakete und Projekte im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog an.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|parameter_id|**bigint**|Der eindeutige Bezeichner (ID) des Parameters.|  
|project_id|**bigint**|Die eindeutige ID des Projekts.|  
|object_type|**smallint**|Der Typ des Parameters. Für einen Projektparameter ist der Wert `20` , und für einen Paketparameter ist der Wert `30` .|  
|object_name|**sysname**|Der Name des entsprechenden Projekts oder Pakets.|  
|parameter_name|**sysname(nvarchar(128))**|Der Name des Parameters.|  
|data_type|**nvarchar(128)**|Der Datentyp des Parameters.|  
|erforderlich|**bit**|Wenn der Wert `1`lautet, ist der Parameterwert erforderlich, um die Ausführung zu starten. Wenn der Wert `0`lautet, ist der Parameterwert nicht erforderlich, um die Ausführung zu starten.|  
|sensitive|**bit**|Wenn der Wert `1`lautet, ist der Parameterwert vertraulich. Wenn der Wert `0`lautet, ist der Parameterwert nicht vertraulich.|  
|description|**nvarchar(1024)**|Eine optionale Beschreibung des Pakets.|  
|design_default_value|**sql_variant**|Der Standardwert für den Parameter, der während des Entwurfs des Projekts oder Pakets zugewiesen wurde.|  
|default_value|**sql_variant**|Der Standardwert, der derzeit auf dem Server verwendet wird.|  
|value_type|**char(1)**|Gibt den Typ des Parameterwerts an. In diesem Feld wird `V` angezeigt, wenn „parameter_value“ ein Literalwert ist, und `R` wird angezeigt, wenn der Wert durch Verweis auf eine Umgebungsvariable zugewiesen wird.|  
|value_set|**bit**|Wenn der Wert `1`ist, wurde der Parameterwert zugewiesen. Wenn der Wert `0`ist, wurde der Parameterwert nicht zugewiesen.|  
|referenced_variable_name|**nvarchar(128)**|Der Name der Umgebungsvariablen, die dem Wert des Parameters zugewiesen wird. Der Standardwert ist **NULL**.|  
|validation_status|**char(1)**|Nur für Informationszwecke identifiziert. Wird in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] nicht verwendet.|  
|last_validation_time|**datetimeoffset(7)**|Nur für Informationszwecke identifiziert. Wird in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] nicht verwendet.|  
  
## <a name="permissions"></a>Berechtigungen  
 Zum Anzeigen von Zeilen in dieser Sicht benötigten Sie eine der folgenden Berechtigungen:  
  
-   READ-Berechtigung für das Projekt  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
  
 Sicherheit auf Zeilenebene wird erzwungen. Es werden nur Zeilen angezeigt, zu deren Anzeige Sie berechtigt sind.  
  
  

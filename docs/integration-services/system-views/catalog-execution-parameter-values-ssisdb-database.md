---
title: Catalog. execution_parameter_values (SSISDB-Datenbank) | Microsoft Docs
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
ms.assetid: ec93e67b-04ce-4aae-ab96-3ad20e9793ad
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 60907a82f3d0bb9f273355fd6bfbd7378ce72c9f
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="catalogexecutionparametervalues-ssisdb-database"></a>catalog.execution_parameter_values (SSISDB-Datenbank)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Zeigt die tatsächlichen Parameterwerte an, die von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Paketen während einer Instanz der Ausführung verwendet werden.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|execution_parameter_id|**bigint**|Eindeutiger Bezeichner (ID) des Ausführungsparameters.|  
|execution_id|**bigint**|Eindeutige ID für die Instanz der Ausführung.|  
|object_type|**smallint**|Wenn der Wert `20`ist, ist der Parameter ein Projektparameter. Wenn der Wert `30`ist, ist der Parameter ein Paketparameter. Wenn der Wert ist `50`, der Parameter ist eine der folgenden:<br /><br /> **LOGGING_LEVEL**<br /><br /> **DUMP_ON_ERROR**<br /><br /> **DUMP_ON_EVENT**<br /><br /> **DUMP_EVENT_CODE**<br /><br /> **CALLER_INFO**<br /><br /> **SYNCHRONISIERT**|  
|parameter_data_type|**vom Datentyp nvarchar(128)**|Der Datentyp des Parameters.|  
|parameter_name|**sysname**|Der Name des Parameters.|  
|parameter_value|**sql_variant**|Der Wert des Parameters. Wenn vertrauliche ist `0`, die nur-Text-Wert wird angezeigt. Wenn vertrauliche ist `1`, **NULL** Wert wird angezeigt.|  
|sensitive|**bit**|Wenn der Wert `1`lautet, ist der Parameterwert vertraulich. Wenn der Wert `0`lautet, ist der Parameterwert nicht vertraulich.|  
|erforderlich|**bit**|Wenn der Wert `1`lautet, ist der Parameterwert erforderlich, um die Ausführung zu starten. Wenn der Wert `0`lautet, ist der Parameterwert nicht erforderlich, um die Ausführung zu starten.|  
|value_set|**bit**|Wenn der Wert `1`ist, wurde der Parameterwert zugewiesen. Wenn der Wert `0`ist, wurde der Parameterwert nicht zugewiesen.|  
|runtime_override|**bit**|Wenn der Wert `1`ist, wurde der ursprüngliche Parameterwert geändert, bevor die Ausführung gestartet wurde. Wenn der Wert `0`lautet, ist der Parameterwert der ursprünglich festgelegte Wert.|  
  
## <a name="remarks"></a>Hinweise  
 In dieser Sicht wird eine Zeile für jeden Ausführungsparameter im Katalog angezeigt. Ein Ausführungsparameterwert ist der Wert, der einem Projektparameter oder Paketparameter während einer einzelnen Instanz der Ausführung zugewiesen wird.  
  
## <a name="permissions"></a>Berechtigungen  
 Diese Sicht erfordert eine der folgenden Berechtigungen:  
  
-   READ-Berechtigung für die Instanz der Ausführung  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
  
> [!NOTE]  
>  Wenn Sie über die Berechtigung verfügen, einen Vorgang auf dem Server auszuführen, verfügen Sie auch über die Berechtigung, Informationen zu dem Vorgang anzuzeigen. Sicherheit auf Zeilenebene wird erzwungen. Es werden nur Zeilen angezeigt, zu deren Anzeige Sie berechtigt sind.  
  
  


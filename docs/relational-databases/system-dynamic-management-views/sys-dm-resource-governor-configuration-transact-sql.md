---
title: Sys. dm_resource_governor_configuration (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_resource_governor_configuration_TSQL
- dm_resource_governor_configuration
- sys.dm_resource_governor_configuration
- sys.dm_resource_governor_configuration_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_resource_governor_configuration dynamic management view
ms.assetid: c89aab6a-0434-4ce6-af8c-f8a1a3284e38
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 552b1ecbfd01afddf8671c05dcdf528f3edccb6a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmresourcegovernorconfiguration-transact-sql"></a>sys.dm_resource_governor_configuration (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt eine Zeile mit dem aktuellen Konfigurationsstatus der Ressourcenkontrolle im Arbeitsspeicher zurück.  
  

|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|classifier_function_id|**int**|Die ID der Klassifizierungsfunktion, die zurzeit von der Ressourcenkontrolle verwendet wird. Gibt den Wert 0 (null) zurück, wenn keine Funktion verwendet wird. Lässt keine NULL-Werte zu.<br /><br /> **Hinweis:** diese Funktion dient zur Klassifizierung neuer Anforderungen und verwendet Regeln, um diese Anforderungen an die entsprechende Arbeitsauslastungsgruppe weiterzuleiten. Weitere Informationen finden Sie unter [Resource Governor](../../relational-databases/resource-governor/resource-governor.md).|  
|is_reconfiguration_pending|**bit**|Gibt an, ob mit der ALTER RESOURCE GOVERNOR RECONFIGURE-Anweisung Änderungen an einer Gruppe oder einem Pool vorgenommen wurden, die jedoch noch nicht auf die Konfiguration im Arbeitsspeicher angewendet wurden. Einer der folgenden Werte wird zurückgegeben:<br /><br /> 0 - Eine Anweisung zur Neukonfiguration ist nicht erforderlich.<br /><br /> 1 - Es ist eine Anweisung zur Neukonfiguration oder ein Serverneustart erforderlich, damit ausstehende Konfigurationsänderungen übernommen werden können.<br /><br /> **Hinweis:** zurückgegebene Wert ist immer 0, wenn die Ressourcenkontrolle deaktiviert ist.<br /><br /> Lässt keine NULL-Werte zu.|  
|max_outstanding_io_per_volume|**int**|**Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Die maximale Anzahl der ausstehenden E/A-Vorgänge pro Volume.|  
  
## <a name="remarks"></a>Hinweise  
 Diese dynamische Verwaltungssicht zeigt die Konfiguration im Arbeitsspeicher an. Verwenden Sie die entsprechende Katalogsicht, um die gespeicherten Konfigurationsmetadaten anzuzeigen.  
  
 Das folgende Beispiel veranschaulicht, wie die gespeicherten Metadatenwerte und die Arbeitsspeicherwerte der Ressourcenkontrollenkonfiguration abgerufen und verglichen werden.  
  
```  
USE master;  
go  
-- Get the stored metadata.  
SELECT   
object_schema_name(classifier_function_id) AS 'Classifier UDF schema in metadata',   
object_name(classifier_function_id) AS 'Classifier UDF name in metadata'  
FROM   
sys.resource_governor_configuration;  
go  
-- Get the in-memory configuration.  
SELECT   
object_schema_name(classifier_function_id) AS 'Active classifier UDF schema',   
object_name(classifier_function_id) AS 'Active classifier UDF name'  
FROM   
sys.dm_resource_governor_configuration;  
go  
```  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW SERVER STATE-Berechtigung.  
  
## <a name="see-also"></a>Siehe auch  
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [resource_governor_configuration &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-configuration-transact-sql.md)   
 [Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor.md)  
  
  


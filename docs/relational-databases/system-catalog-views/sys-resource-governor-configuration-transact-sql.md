---
title: resource_governor_configuration (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.resource_governor_configuration_TSQL
- sys.resource_governor_configuration
- resource_governor_configuration_TSQL
- resource_governor_configuration
dev_langs: TSQL
helpviewer_keywords: sys.resource_governor_configuration catalog view
ms.assetid: 89099668-1dc6-4b07-9d8b-49bc95c7bfc0
caps.latest.revision: "24"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a1a02e4e7b26ec1c86f10f13632ade9c3bd3d264
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysresourcegovernorconfiguration-transact-sql"></a>sys.resource_governor_configuration (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt den gespeicherten Status der Ressourcenkontrolle zurück.  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|classifier_function_id|**int**|Die ID der Klassifizierungsfunktion, wie sie in den Metadaten gespeichert ist. Lässt keine NULL-Werte zu.<br /><br /> **Hinweis** diese Funktion wird verwendet, um neue Sitzungen zu klassifizieren und verwendet Regeln, um die arbeitsauslastung an die entsprechende Arbeitsauslastungsgruppe weiterzuleiten. Weitere Informationen finden Sie unter [Resource Governor](../../relational-databases/resource-governor/resource-governor.md).|  
|is_enabled|**bit**|Gibt den aktuellen Status der Ressourcenkontrolle an:<br /><br /> 0 = die Ressourcenkontrolle ist nicht aktiviert.<br /><br /> 1 = die Ressourcenkontrolle aktiviert ist.<br /><br /> Lässt keine NULL-Werte zu.|  
|max_outstanding_io_per_volume|**int**|**Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Die maximale Anzahl der ausstehenden E/A-Vorgänge pro Volume.|  
  
## <a name="remarks"></a>Hinweise  
 Die Katalogsicht zeigt die Konfiguration der Ressourcenkontrolle an, wie sie in den Metadaten gespeichert ist. Um die Konfiguration im Arbeitsspeicher anzuzeigen, verwenden Sie die entsprechende dynamische Verwaltungssicht.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW ANY DEFINITION-Berechtigung, um Inhalte anzuzeigen, und erfordert die CONTROL SERVER-Berechtigung, um Inhalte zu ändern.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel veranschaulicht, wie die gespeicherten Metadatenwerte und die Arbeitsspeicherwerte der Ressourcenkontrollenkonfiguration abgerufen und verglichen werden.  
  
```  
USE master;  
GO  
-- Get the stored metadata.  
SELECT   
object_schema_name(classifier_function_id) AS 'Classifier UDF schema in metadata',   
object_name(classifier_function_id) AS 'Classifier UDF name in metadata'  
FROM   
sys.resource_governor_configuration;  
GO  
-- Get the in-memory configuration.  
SELECT   
object_schema_name(classifier_function_id) AS 'Active classifier UDF schema',   
object_name(classifier_function_id) AS 'Active classifier UDF name'  
FROM   
sys.dm_resource_governor_configuration;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten der Ressourcenkontrolle &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)   
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Sys. dm_resource_governor_configuration &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-configuration-transact-sql.md)   
 [Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor.md)  
  
  

---
title: Sys. dm_db_missing_index_groups (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_db_missing_index_groups
- sys.dm_db_missing_index_groups_TSQL
- dm_db_missing_index_groups
- dm_db_missing_index_groups_TSQL
dev_langs: TSQL
helpviewer_keywords:
- sys.dm_db_missing_index_groups dynamic management view
- missing indexes feature [SQL Server], sys.dm_db_missing_index_groups dynamic management view
ms.assetid: 9cc00acd-d83d-49f8-be72-5b2aebed246b
caps.latest.revision: "39"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 977f1b4de407b86d3e23bb297a66bf9e62207859
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmdbmissingindexgroups-transact-sql"></a>sys.dm_db_missing_index_groups (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt Informationen zu fehlenden Indizes, die in einer bestimmten Gruppe fehlender Indizes enthalten sind (außer räumliche Indizes), zurück.  
  
 In [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]können dynamische Verwaltungssichten keine Informationen verfügbar machen, die sich auf die Datenbankkapselung auswirken würden oder die sich auf andere Datenbanken beziehen, auf die der Benutzer Zugriff hat. Um zu vermeiden, dass diese Informationen verfügbar gemacht werden, wird jede Zeile mit Daten, die zum verbundenen Mandanten gehören, herausgefiltert.  
   
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**index_group_handle**|**int**|Identifiziert eine Gruppe fehlender Indizes.|  
|**index_handle**|**int**|Identifiziert einen fehlenden Index, zu der angegebenen Gruppe gehört **Index_group_handle**.<br /><br /> Eine Indexgruppe enthält nur einen Index.|  
  
## <a name="remarks"></a>Hinweise  
 Zurückgegebene Informationen **Sys. dm_db_missing_index_groups** wird aktualisiert, wenn eine Abfrage vom Abfrageoptimierer optimiert wird, und wird nicht beibehalten. Informationen zu fehlenden Indizes werden nur bis zum Neustart von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aufbewahrt. Datenbankadministratoren sollten regelmäßig Sicherungskopien der Informationen zu fehlenden Indizes erstellen, wenn Sie sie nach dem Wiederverwenden des Servers beibehalten möchten.  
  
 Keine Spalte des Ausgaberesultsets stellt einen Schlüssel dar, gemeinsam bilden sie jedoch einen Indexschlüssel.  
  
## <a name="permissions"></a>Berechtigungen  
 Zum Abfragen dieser dynamischen Verwaltungssicht muss den Benutzern die VIEW SERVER STATE-Berechtigung oder eine Berechtigung, die die VIEW SERVER STATE-Berechtigung impliziert, erteilt werden.  
  
## <a name="see-also"></a>Siehe auch  
 [Sys. dm_db_missing_index_columns &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-columns-transact-sql.md)   
 [Sys. dm_db_missing_index_details &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)   
 [Sys. dm_db_missing_index_group_stats &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-group-stats-transact-sql.md)  
  
  

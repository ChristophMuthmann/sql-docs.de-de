---
title: sys.dm_db_rda_schema_update_status (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_db_rda_schema_update_status
- sys.dm_db_rda_schema_update_status_TSQL
- dm_db_rda_schema_update_status
- dm_db_rda_schema_update_status_TSQL
helpviewer_keywords:
- sys.dm_db_rda_schema_update_status dynamic management view
ms.assetid: 364e3caa-a7c6-4be5-a029-0b19da34de3e
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f3889c9985bad47e192937f7ee8c2608be225ed1
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="stretch-database---sysdmdbrdaschemaupdatestatus"></a>Stretch Database - sys.dm_db_rda_schema_update_status
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Enthält eine Zeile für jedes Update Schemaaufgabe für die remotedatenarchiv jeder Stretch-aktivierte Tabelle in der aktuellen Datenbank. Aufgaben werden durch ihre Aufgaben-Ids identifiziert.  
  
 **dm_db_rda_schema_update_status** is scoped to the current database context. Stellen Sie sicher, dass Sie im Kontext Datenbank der Stretch-aktivierte Tabelle sind für die Sie Schema Updatestatus anzeigen möchten.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**table_id**|**int**|Die ID der die lokale Stretch-aktivierte Tabelle, deren remotedatenarchiv Schema, wird aktualisiert.|  
|**database_id**|**int**|Die ID der Datenbank, die die lokale Stretch-aktivierte Tabelle enthält.|  
|**task_id**|**bigint**|Die ID des Tasks "remote Data Archive Schema aktualisieren".|  
|**task_type**|**int**|Der Typ des Tasks "remote Data Archive Schema aktualisieren".|  
|**task_type_desc**|**nvarchar**|Die Beschreibung des Typs des Tasks "remote Data Archive Schema aktualisieren".|  
|**task_state**|**int**|Der Status des Tasks "remote Data Archive Schema aktualisieren".|  
|**task_state_des**|**nvarchar**|Die Beschreibung des Status des Tasks "remote Data Archive Schema aktualisieren".|  
|**start_time_utc**|**datetime**|Die UTC-Zeit, an der die Remotedaten Schemaupdate gestartet archivieren.|  
|**end_time_utc**|**datetime**|Die UTC-Zeit, an der das Schemaupdate remotedatenarchiv, wurde abgeschlossen.|  
|**error_number**|**int**|Wenn die Aktualisierung des Schemas remote Data Archive, die Fehlernummer des Fehlers, die aufgetreten sind fehlschlägt. Andernfalls wird null verwendet.|  
|**error_severity**|**int**|Wenn der remote Data Archive-Schemaupdate, den Schweregrad des Fehlers, die aufgetreten sind fehlschlägt. Andernfalls wird null verwendet.|  
|**error_state**|**int**|Wenn der remote Data Archive-Schemaupdate, den Zustand des Fehlers, die aufgetreten sind fehlschlägt. Andernfalls wird null verwendet. Die Error_state gibt an, die Bedingung oder den Speicherort, in dem der Fehler aufgetreten ist.|  
  
## <a name="see-also"></a>Siehe auch  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  

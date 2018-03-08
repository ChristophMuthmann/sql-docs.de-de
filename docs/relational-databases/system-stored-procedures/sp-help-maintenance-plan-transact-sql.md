---
title: Sp_help_maintenance_plan (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_help_maintenance_plan_TSQL
- sp_help_maintenance_plan
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_maintenance_plan
ms.assetid: e972a510-960e-41d6-93c5-c71cd581a585
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e5669438c159010e1b5011418df913c3c2743aff
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="sphelpmaintenanceplan-transact-sql"></a>sp_help_maintenance_plan (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt Informationen zum angegebenen Wartungsplan zurück. Wenn kein Plan angegeben ist, gibt die gespeicherte Prozedur Informationen zu allen Wartungsplänen zurück.  
  
> **Hinweis:** diese gespeicherte Prozedur wird mit Datenbankwartungsplänen verwendet. Diese Funktion wurde durch Wartungspläne ersetzt, die nicht diese gespeicherte Prozedur verwenden. Verwenden Sie diese Prozedur, um Datenbankwartungspläne für Installationen bereitzustellen, die von einer früheren Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aktualisiert wurden.  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_help_maintenance_plan [ [ @plan_id = ] 'plan_id' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@plan_id =**] **'***plan_id***'**  
 Gibt die Plan-ID des Wartungsplans an. *"Plan_id"* ist **"uniqueidentifier"**. Die Standardeinstellung ist NULL.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 Keine  
  
## <a name="result-sets"></a>Resultsets  
 Wenn *"Plan_id"* angegeben wird, **Sp_help_maintenance_plan** drei Tabellen zurück: Plan, Datenbank und Auftrag.  
  
### <a name="plan-table"></a>Plan-Tabelle  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**plan_id**|**uniqueidentifier**|ID des Wartungsplans.|  
|**plan_name**|**sysname**|Name des Wartungsplans.|  
|**date_created**|**datetime**|Erstellungsdatum des Wartungsplans.|  
|**Besitzer**|**sysname**|Besitzer des Wartungsplans.|  
|**max_history_rows**|**int**|Maximale Anzahl von Zeilen, die für das Aufzeichnen des Wartungsplanverlaufs in der Systemtabelle zugeordnet werden.|  
|**remote_history_server**|**int**|Der Name des Remoteservers, auf die der Verlaufsbericht geschrieben werden konnte.|  
|**max_remote_history_rows**|**int**|Maximale Anzahl von Zeilen, die in der Systemtabelle auf einem Remoteserver zugeordnet wurden und in die der Verlaufsbericht geschrieben werden konnte.|  
|**user_defined_1**|**int**|Der Standardwert ist NULL.|  
|**user_defined_2**|**nvarchar(100)**|Der Standardwert ist NULL.|  
|**user_defined_3**|**datetime**|Der Standardwert ist NULL.|  
|**user_defined_4**|**uniqueidentifier**|Der Standardwert ist NULL.|  
  
### <a name="database-table"></a>Database-Tabelle  
  
|Spaltenname|Description|  
|-----------------|-----------------|  
|**database_name**|Der Name jeder Datenbank, die dem Wartungsplan zugeordnet ist. *database_name* ist **sysname**|  
  
### <a name="job-table"></a>Job-Tabelle  
  
|Spaltenname|Description|  
|-----------------|-----------------|  
|**job_id**|Die ID jedes Auftrags, der dem Wartungsplan zugeordnet ist. *Job_id* ist **"uniqueidentifier"**.|  
  
## <a name="remarks"></a>Hinweise  
 **Sp_help_maintenance_plan** befindet sich in der **Msdb** Datenbank.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der **Sysadmin** -Serverrolle kann ausführen **Sp_help_maintenance_plan**.  
  
## <a name="examples"></a>Beispiele  
 Dieses Beispiel enthält beschreibende Informationen zum Wartungsplan FAD6F2AB-3571-11D3-9D4A-00C04FB925FC.  
  
```  
EXECUTE   sp_help_maintenance_plan   
   N'FAD6F2AB-3571-11D3-9D4A-00C04FB925FC';  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Wartungspläne](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [Datenbank-Wartungsplan gespeicherte Systemprozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-maintenance-plan-stored-procedures-transact-sql.md)  
  
  

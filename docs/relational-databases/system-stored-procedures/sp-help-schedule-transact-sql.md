---
title: Sp_help_schedule (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_help_schedule
- sp_help_schedule_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_help_schedule
ms.assetid: b2fc4ce1-0a8e-44d2-b206-7dc7b258d8c9
caps.latest.revision: "35"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c7f3e942063e67a1aa896e14a2f195696572ef63
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sphelpschedule-transact-sql"></a>sp_help_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Listet Informationen zu Zeitplänen auf.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_help_schedule   
     [ @schedule_id = ] id ,  
     [ @schedule_name = ] 'schedule_name'   
     [ , [ @attached_schedules_only = ] attached_schedules_only ]  
     [ , [ @include_description = ] include_description ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@schedule_id =** ] *Id*  
 Der Bezeichner des Zeitplans, der aufgelistet werden soll. *Schedule_name* ist **Int**, hat keinen Standardwert. Entweder *Schedule_id* oder *Schedule_name* kann angegeben werden.  
  
 [  **@schedule_name =** ] **"***Schedule_name***"**  
 Der Name des Zeitplans, der aufgelistet werden soll. *Schedule_name* ist **Sysname**, hat keinen Standardwert. Entweder *Schedule_id* oder *Schedule_name* kann angegeben werden.  
  
 [  **@attached_schedules_only**  =] *Attached_schedules_only* ]  
 Gibt an, ob nur Zeitpläne angezeigt werden sollen, denen ein Auftrag angefügt ist. *Attached_schedules_only* ist **Bit**, hat den Standardwert **0**. Wenn *Attached_schedules_only* ist **0**, alle Zeitpläne angezeigt. Wenn *Attached_schedules_only* ist **1**, das Resultset enthält nur Zeitpläne, die einem Auftrag angefügt sind.  
  
 [  **@include_description**  =] *Include_description*  
 Gibt an, ob das Resultset Beschreibungen enthalten soll. *Include_description* ist **Bit**, hat den Standardwert **0**. Wenn *Include_description* ist **0**, *Schedule_description* Spalte des Resultsets enthält einen Platzhalter. Wenn *Include_description* ist **1**, ist die Beschreibung des Zeitplans im Resultset enthalten.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Diese Prozedur gibt das folgende Resultset zurück:  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**schedule_id**|**int**|ID des Zeitplans.|  
|**schedule_uid**|**uniqueidentifier**|Bezeichner für den Zeitplan.|  
|**schedule_name**|**sysname**|Name des Zeitplans.|  
|**aktiviert**|**int**|Ob der Zeitplan aktiviert (**1**) oder nicht aktiviert (**0**).|  
|**freq_type**|**int**|Der Wert, der angibt, wann der Auftrag ausgeführt werden.<br /><br /> **1** = einmal<br /><br /> **4** = täglich<br /><br /> **8** = wöchentlich<br /><br /> **16** = monatlich<br /><br /> **32** = monatlich, relativ zu den **Freq_interval**<br /><br /> **64** = Ausführung, wenn der SQLServerAgent-Dienst gestartet wird.|  
|**freq_interval**|**int**|Tage, wenn der Auftrag ausgeführt wird. Der Wert hängt vom Wert der **Freq_type**. Weitere Informationen finden Sie unter [Sp_add_schedule &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md).|  
|**freq_subday_type**|**int**|Einheiten für **Freq_subday_interval**. Weitere Informationen finden Sie unter [Sp_add_schedule &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md).|  
|**freq_subday_interval**|**int**|Anzahl der **Freq_subday_type** -Perioden zwischen den einzelnen Ausführungen des Auftrags auftreten. Weitere Informationen finden Sie unter [Sp_add_schedule &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md).|  
|**freq_relative_interval**|**int**|Auftreten des geplanten Auftrags von der **Freq_interval** in jedem Monat. Weitere Informationen finden Sie unter [Sp_add_schedule &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md).|  
|**freq_recurrence_factor**|**int**|Anzahl der Monate zwischen der geplanten Ausführung des Auftrags|  
|**active_start_date**|**int**|Datum, an dem der Zeitplan aktiviert wird.|  
|**active_end_date**|**int**|Enddatum für den Zeitplan.|  
|**active_start_time**|**int**|Uhrzeit, zu der der Zeitplan gestartet wird.|  
|**active_end_time**|**int**|Uhrzeit, zu der der Zeitplan beendet wird.|  
|**date_created**|**datetime**|Datum, an dem der Zeitplan erstellt wird|  
|**schedule_description**|**nvarchar(4000)**|Eine Beschreibung des Zeitplans in englischer Sprache (falls angefordert).|  
|**job_count**|**int**|Gibt die Anzahl von Aufträgen zurück, die auf diesen Zeitplan verweisen.|  
  
## <a name="remarks"></a>Hinweise  
 Wenn keine Parameter angegeben sind, **Sp_help_schedule** listet Informationen für alle Zeitpläne in der Instanz.  
  
## <a name="permissions"></a>Berechtigungen  
 Standardmäßig können nur Mitglieder der festen Serverrolle **sysadmin** diese gespeicherte Prozedur ausführen. Andere Benutzer müssen Mitglieder der festen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Datenbankrollen in der **msdb** -Datenbank sein:  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Weitere Informationen zu den Berechtigungen dieser Rollen finden Sie unter [Feste Datenbankrollen des SQL Server-Agents](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
 Mitglieder der **SQLAgentUserRole** sehen nur die Zeitpläne, die sie besitzen.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-listing-information-for-all-schedules-in-the-instance"></a>A. Auflisten der Informationen für alle Zeitpläne in der Instanz  
 Im folgenden Beispiel werden die Informationen für alle Zeitpläne in der Instanz aufgelistet.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_schedule ;  
GO  
```  
  
### <a name="b-listing-information-for-a-specific-schedule"></a>B. Auflisten der Informationen für einen bestimmten Zeitplan  
 Im folgenden Beispiel werden Informationen zum Zeitplan `NightlyJobs` aufgelistet.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_schedule  
    @schedule_name = N'NightlyJobs' ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_add_schedule &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [Sp_attach_schedule &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)   
 [Sp_delete_schedule &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [Sp_detach_schedule &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-detach-schedule-transact-sql.md)  
  
  

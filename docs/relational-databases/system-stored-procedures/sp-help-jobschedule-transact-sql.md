---
title: Sp_help_jobschedule (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_help_jobschedule
- sp_help_jobschedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_jobschedule
ms.assetid: 2cded902-9272-4667-ac4b-a4f95a9f008e
caps.latest.revision: 34
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 731857bc70bcda1c7817db6e2cdc7eed3ad68236
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sphelpjobschedule-transact-sql"></a>sp_help_jobschedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt Informationen zur Zeitplanung von Aufträgen zurück, mit denen [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] automatisierte Aktivitäten ausführt.  
 
 
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_help_jobschedule { [ @job_id = ] job_id | [ @job_name = ] 'job_name' }  
     [ , [ @schedule_name = ] 'schedule_name' ]  
     [ , [ @schedule_id = ] schedule_id ]  
     [ , [ @include_description = ] include_description ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@job_id=** ] *job_id*  
 Die Auftrags-ID *Job_id*ist **"uniqueidentifier"**, hat den Standardwert NULL.  
  
 [  **@job_name=** ] **"***Job_name***"**  
 Der Name des Auftrags. *Job_name*ist **Sysname**, hat den Standardwert NULL.  
  
> **Hinweis:** entweder *Job_id* oder *Job_name* muss angegeben werden, aber beide können nicht angegeben werden.  
  
 [  **@schedule_name=** ] **"***Schedule_name***"**  
 Der Name des Zeitplanelements für den Auftrag. *Schedule_name*ist **Sysname**, hat den Standardwert NULL.  
  
 [  **@schedule_id=** ] *Schedule_id*  
 Die Identifikationsnummer des Zeitplanelements für den Auftrag. *Schedule_id*ist **Int**, hat den Standardwert NULL.  
  
 [ **@include_description=** ] *include_description*  
 Gibt an, ob die Beschreibung des Zeitplans in das Resultset eingeschlossen werden soll. *Include_description* ist **Bit**, hat den Standardwert **0**. Wenn *Include_description* ist **0**, die Beschreibung des Zeitplans ist nicht im Resultset enthalten. Wenn *Include_description* ist **1**, ist die Beschreibung des Zeitplans im Resultset enthalten.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**schedule_id**|**int**|ID des Zeitplans.|  
|**schedule_name**|**sysname**|Name des Zeitplans.|  
|**Aktiviert**|**int**|Ob der Zeitplan aktiviert (**1**) oder nicht aktiviert (**0**).|  
|**freq_type**|**int**|Der Wert, der angibt, wann der Auftrag ausgeführt werden.<br /><br /> **1** = einmal<br /><br /> **4** = täglich<br /><br /> **8** = wöchentlich<br /><br /> **16** = monatlich<br /><br /> **32** = monatlich, relativ zu den **Freq_interval**<br /><br /> **64** = ausgeführt werden, wenn **SQLServerAgent** -Dienst gestartet wird.|  
|**freq_interval**|**int**|Tage, wenn der Auftrag ausgeführt wird. Der Wert hängt vom Wert der **Freq_type**. Weitere Informationen finden Sie unter [Sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md).|  
|**freq_subday_type**|**int**|Einheiten für **Freq_subday_interval**. Weitere Informationen finden Sie unter [Sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md).|  
|**freq_subday_interval**|**int**|Anzahl der **Freq_subday_type** -Perioden zwischen den einzelnen Ausführungen des Auftrags auftreten. Weitere Informationen finden Sie unter [Sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md).|  
|**freq_relative_interval**|**int**|Auftreten des geplanten Auftrags von der **Freq_interval** in jedem Monat. Weitere Informationen finden Sie unter [Sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md).|  
|**freq_recurrence_factor**|**int**|Anzahl der Monate zwischen der geplanten Ausführung des Auftrags|  
|**active_start_date**|**int**|Datum, an dem der Zeitplan aktiviert wird.|  
|**active_end_date**|**int**|Enddatum für den Zeitplan.|  
|**active_start_time**|**int**|Uhrzeit, zu der der Zeitplan gestartet wird.|  
|**active_end_time**|**int**|Uhrzeit, zu der der Zeitplan beendet wird.|  
|**date_created**|**datetime**|Datum, an dem der Zeitplan erstellt wird|  
|**schedule_description**|**nvarchar(4000)**|Eine Beschreibung des Zeitplans, der Werte in abgeleitet ist **msdb.dbo.sysschedules**. Wenn *Include_description* ist **0**, enthält diese Spalte Text, der besagt, dass die Beschreibung nicht angefordert wurde.|  
|**next_run_date**|**int**|Datum, an dem der Zeitplan die nächste Ausführung des Auftrags bewirken wird|  
|**next_run_time**|**int**|Uhrzeit, zu der der Zeitplan die nächste Ausführung des Auftrags bewirken wird|  
|**schedule_uid**|**uniqueidentifier**|Bezeichner für den Zeitplan.|  
|**job_count**|**int**|Die Anzahl der zurückgegebenen Aufträge.|  
  
> **Hinweis:****Sp_help_jobschedule** gibt Werte aus der **dbo.sysjobschedules** und **dbo.sysschedules** -Systemtabellen in **Msdb** .   **Sysjobschedules** wird alle 20 Minuten aktualisiert. Dies kann Auswirkungen auf die Werte haben, die von dieser gespeicherten Prozedur zurückgegeben werden.  
  
## <a name="remarks"></a>Hinweise  
 Die Parameter der **Sp_help_jobschedule** können nur in bestimmten Kombinationen verwendet werden. Wenn *Schedule_id* angegeben ist, weder *Job_id* noch *Job_name* kann angegeben werden. Andernfalls die *Job_id* oder *Job_name* Parameter können verwendet werden, mit *Schedule_name*.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der festen Serverrolle **sysadmin** . Andere Benutzer müssen Mitglieder der festen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Datenbankrollen in der **msdb** -Datenbank sein:  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Weitere Informationen zu den Berechtigungen dieser Rollen finden Sie unter [Feste Datenbankrollen des SQL Server-Agents](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
 Mitglieder der **SQLAgentUserRole** können nur Eigenschaften von Auftragszeitplänen, deren Besitzer, anzeigen.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-returning-the-job-schedule-for-a-specific-job"></a>A. Zurückgeben des Auftragszeitplans für einen bestimmten Auftrag  
 Im folgenden Beispiel werden die Zeitplaninformationen für einen Auftrag namens `BackupDatabase` zurückgegeben  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobschedule  
    @job_name = N'BackupDatabase' ;  
GO  
```  
  
### <a name="b-returning-the-job-schedule-for-a-specific-schedule"></a>B. Zurückgeben des Auftragszeitplans für einen bestimmten Zeitplan  
 Im folgenden Beispiel werden die Informationen für den Zeitplan `NightlyJobs` und den Auftrag `RunReports` zurückgegeben.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobschedule   
    @job_name = N'RunReports',  
    @schedule_name = N'NightlyJobs' ;  
GO  
```  
  
### <a name="c-returning-the-job-schedule-and-schedule-description-for-a-specific-schedule"></a>C. Zurückgeben des Auftragszeitplans und der Zeitplanbeschreibung für einen bestimmten Zeitplan  
 Im folgenden Beispiel werden die Informationen für den Zeitplan `NightlyJobs` und den Auftrag `RunReports` zurückgegeben. Das zurückgegebene Resultset schließt eine Beschreibung des Zeitplans ein.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobschedule  
    @job_name = N'RunReports',  
    @schedule_name = N'NightlyJobs',  
    @include_description = 1 ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_delete_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [sp_update_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-schedule-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

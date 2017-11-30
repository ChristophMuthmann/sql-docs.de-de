---
title: Sp_help_jobstep (Transact-SQL) | Microsoft Docs
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
- sp_help_jobstep_TSQL
- sp_help_jobstep
dev_langs: TSQL
helpviewer_keywords: sp_help_jobstep
ms.assetid: 4a13b804-45f2-4f82-987f-42d9a57dd6db
caps.latest.revision: "40"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 316436c8c2607ef6c759efaa444d7f78e2de6834
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="sphelpjobstep-transact-sql"></a>sp_help_jobstep (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt Informationen zu den Schritten eines Auftrags zurück, die der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent-Dienst verwendet, um automatisierte Aktivitäten auszuführen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_help_jobstep { [ @job_id = ] 'job_id' | [ @job_name = ] 'job_name' }  
     [ , [ @step_id = ] step_id ]   
     [ , [ @step_name = ] 'step_name' ]   
     [ , [ @suffix = ] suffix ]   
```  
  
## <a name="arguments"></a>Argumente  
 [  **@job_id =**] **"***Job_id***"**  
 Die ID des Auftrags, zu dem Auftragsinformationen zurückgegeben werden sollen. *Job_id* ist **"uniqueidentifier"**, hat den Standardwert NULL.  
  
 [  **@job_name =**] **"***Job_name***"**  
 Der Name des Auftrags. *Job_name* ist **Sysname**, hat den Standardwert NULL.  
  
> [!NOTE]  
>  Entweder *Job_id* oder *Job_name* muss angegeben werden, aber beide können nicht angegeben werden.  
  
 [  **@step_id =**] *Step_id*  
 Die ID des Auftragsschritts. Wenn diese nicht angegeben wird, sind alle Schritte im Auftrag eingeschlossen. *Step_id* ist **Int**, hat den Standardwert NULL.  
  
 [  **@step_name =**] **"***Step_name***"**  
 Der Name des Schritts im Auftrag. *Step_name* ist **Sysname**, hat den Standardwert NULL.  
  
 [  **@suffix =**] *Suffix*  
 Ein Flag, das angibt, ob eine textbeschreibung, um angefügt wird die **Flags** Spalte in der Ausgabe. *Suffix*ist **Bit**, hat den Standardwert **0**. Wenn *Suffix* ist **1**, eine Beschreibung angefügt.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**step_id**|**int**|Eindeutiger Bezeichner für den Schritt.|  
|**step_name**|**sysname**|Name des Auftragsschritts.|  
|**Subsystem**|**nvarchar(40)**|Subsystem, in dem der Schrittbefehl ausgeführt werden soll|  
|**Befehl**|**nvarchar(max)**|Befehl, der in dem Schritt ausgeführt wird.|  
|**Flags**|**int**|Bitmaske der Werte, die das Schrittverhalten steuern.|  
|**cmdexec_success_code**|**int**|Für eine **CmdExec** Schritt, dies ist der Prozessexitcode eines erfolgreichen Befehls.|  
|**on_success_action**|**tinyint**|Auszuführende Aktion, wenn der Schritt erfolgreich ist:<br /><br /> **1** = Auftrag mit Erfolgsmeldung beenden.<br /><br /> **2** = Auftrag mit Fehlermeldung beenden.<br /><br /> **3** = weiter mit dem nächsten Schritt fort.<br /><br /> **4** = Gehe zu Schritt.|  
|**on_success_step_id**|**int**|Wenn **On_success_action** 4 ist, wird hiermit der nächste auszuführende Schritt.|  
|**on_fail_action**|**tinyint**|Was tun, wenn der Schritt fehlschlägt. Werte sind identisch mit **On_success_action**.|  
|**on_fail_step_id**|**int**|Wenn **On_fail_action** 4 ist, wird hiermit der nächste auszuführende Schritt.|  
|**server**|**sysname**|Reserviert.|  
|**database_name**|**sysname**|Für einen [!INCLUDE[tsql](../../includes/tsql-md.md)]-Schritt ist dies die Datenbank, in der der Befehl ausgeführt wird.|  
|**database_user_name**|**sysname**|Für einen [!INCLUDE[tsql](../../includes/tsql-md.md)]-Schritt ist dies der Datenbank-Benutzerkontext, in dem der Befehl ausgeführt wird.|  
|**retry_attempts**|**int**|Die maximale Anzahl von Wiederholungsversuchen für den Befehl (falls er nicht erfolgreich ist).|  
|**retry_interval**|**int**|Das Intervall (in Minuten) zwischen den Wiederholungsversuchen.|  
|**os_run_priority**|**int**|Reserviert.|  
|**Ausgabedateiname**|**nvarchar(200)-Datentyp gepackt ist**|Datei in die Befehlsausgabe geschrieben werden soll ([!INCLUDE[tsql](../../includes/tsql-md.md)], **CmdExec**, und **PowerShell** nur Schritte).|  
|**last_run_outcome**|**int**|Ergebnis der letzten Ausführung des Schritts:<br /><br /> **0** = Fehler<br /><br /> **1** = war erfolgreich<br /><br /> **2** = wiederholen<br /><br /> **3** = abgebrochen<br /><br /> **5** = unbekannt|  
|**last_run_duration**|**int**|Die Ausführungsdauer (in Sekunden) des Schritts bei der letzten Ausführung.|  
|**last_run_retries**|**int**|Anzahl der Wiederholungsversuche für den Befehl bei der letzten Ausführung des Schritts|  
|**last_run_date**|**int**|Datum, an dem die Ausführung des Schritts zuletzt gestartet wurde|  
|**last_run_time**|**int**|Uhrzeit, zu der die Ausführung des Schritts zuletzt gestartet wurde|  
|**proxy_id**|**int**|Proxy für den Auftragsschritt.|  
  
## <a name="remarks"></a>Hinweise  
 **Sp_help_jobstep** befindet sich in der **Msdb** Datenbank.  
  
## <a name="permissions"></a>Berechtigungen  
 Standardmäßig können nur Mitglieder der festen Serverrolle **sysadmin** diese gespeicherte Prozedur ausführen. Andere Benutzer müssen Mitglieder der festen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Datenbankrollen in der **msdb** -Datenbank sein:  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Weitere Informationen zu den Berechtigungen dieser Rollen finden Sie unter [Feste Datenbankrollen des SQL Server-Agents](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
 Mitglieder der **SQLAgentUserRole** Auftragsschritte für Aufträge, deren Besitzer, können nur anzeigen.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-return-information-for-all-steps-in-a-specific-job"></a>A. Zurückgeben von Informationen für alle Schritte in einem bestimmten Auftrag  
 Im folgenden Beispiel werden alle Auftragsschritte für den Auftrag `Weekly Sales Data Backup` zurückgegeben.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobstep  
    @job_name = N'Weekly Sales Data Backup' ;  
GO  
```  
  
### <a name="b-return-information-about-a-specific-job-step"></a>B. Zurückgeben von Informationen zu einem bestimmten Auftragsschritt  
 Im folgenden Beispiel werden Informationen zum ersten Auftragsschritt des Auftrags `Weekly Sales Data Backup` zurückgegeben.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobstep  
    @job_name = N'Weekly Sales Data Backup',  
    @step_id = 1 ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_add_jobstep &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)   
 [Sp_delete_jobstep &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql.md)   
 [Sp_help_job &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [Sp_update_jobstep &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-update-jobstep-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

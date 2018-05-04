---
title: Sp_help_job (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
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
- sp_help_job_TSQL
- sp_help_job
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_job
ms.assetid: 8a8b6104-e0e4-4d07-a2c3-f4243ee0d6fa
caps.latest.revision: 27
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5bcebdb4e6bdca021480e8b889228fc95b109a0d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sphelpjob-transact-sql"></a>sp_help_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt Informationen zu Aufträgen zurück, mit denen der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent automatisierte Aktivitäten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausführt.  
  
 
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_help_job { [ @job_id = ] job_id  
[ @job_name = ] 'job_name' }   
     [ , [ @job_aspect = ] 'job_aspect' ]   
     [ , [ @job_type = ] 'job_type' ]   
     [ , [ @owner_login_name = ] 'login_name' ]   
     [ , [ @subsystem = ] 'subsystem' ]   
     [ , [ @category_name = ] 'category' ]   
     [ , [ @enabled = ] enabled ]   
     [ , [ @execution_status = ] status ]   
     [ , [ @date_comparator = ] 'date_comparison' ]   
     [ , [ @date_created = ] date_created ]   
     [ , [ @date_last_modified = ] date_modified ]   
     [ , [ @description = ] 'description_pattern' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@job_id =**] *job_id*  
 Die Auftrags-ID *Job_id* ist **"uniqueidentifier"**, hat den Standardwert NULL.  
  
 [ **@job_name =**] **'***job_name***'**  
 Der Name des Auftrags. *Job_name* ist **Sysname**, hat den Standardwert NULL.  
  
> [!NOTE]  
>  So zeigen Sie einen bestimmten Auftrag können entweder an *Job_id* oder *Job_name* muss angegeben werden.  Lassen Sie beide *Job_id* und *Job_name* zum Zurückgeben von Informationen zu allen Aufträgen.
  
 [ **@job_aspect =**] **'***job_aspect***'**  
 Das Auftragsattribut, das angezeigt werden soll. *Job_aspect* ist **varchar(9)**, hat den Standardwert NULL und kann einen der folgenden Werte sein.  
  
|Wert|Description|  
|-----------|-----------------|  
|**ALL**|Auftragsaspektinformationen|  
|**JOB**|Auftragsinformationen|  
|**ZEITPLÄNE**|Zeitplaninformationen|  
|**SCHRITTE**|Auftragsschrittinformationen|  
|**ZIELE**|Zielinformationen|  
  
 [ **@job_type =**] **'***job_type***'**  
 Der Typ von Aufträgen, die im Bericht enthalten sein sollen. *Der Standardwert ist* ist **varchar(12)**, hat den Standardwert NULL. *Der Standardwert ist* kann **lokale** oder **mit mehreren Servern**.  
  
 [  **@owner_login_name =**] **"***Login_name***"**  
 Der Anmeldename für den Besitzer des Auftrags. *Login_name* ist **Sysname**, hat den Standardwert NULL.  
  
 [ **@subsystem =**] **'***subsystem***'**  
 Der Name des Subsystems. *Subsystem* ist **nvarchar(40)**, hat den Standardwert NULL.  
  
 [ **@category_name =**] **'***category***'**  
 Der Name der Kategorie. *Kategorie* ist **Sysname**, hat den Standardwert NULL.  
  
 [ **@enabled =**] *enabled*  
 Eine Zahl, die angibt, ob Informationen für aktivierte oder deaktivierte Aufträge angezeigt werden. *aktiviert* ist **"tinyint"**, hat den Standardwert NULL. **1** zeigt aktivierte Aufträge und **0** zeigt deaktivierte Aufträge.  
  
 [ **@execution_status =**] *status*  
 Der Ausführungsstatus der Aufträge. *Status* ist **Int**, hat den Standardwert NULL und kann einen der folgenden Werte sein.  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|**0**|Nur die Aufträge werden zurückgegeben, die sich nicht im Leerlauf befinden oder unterbrochen sind.|  
|**1**|Wird ausgeführt.|  
|**2**|Wartet auf Thread|  
|**3**|Zwischen Wiederholungen|  
|**4**|Im Leerlauf.|  
|**5**|Unterbrochen|  
|**7**|Abschlussaktionen werden ausgeführt|  
  
 [ **@date_comparator =**] **'***date_comparison***'**  
 Der Vergleichsoperator, Vergleiche von *Date_created* und *Date_modified*. *Date_comparison* ist **char(1)**, und kann =, \<, oder >.  
  
 [ **@date_created =**] *date_created*  
 Das Datum, an dem der Auftrag erstellt wurde. *Date_created*ist **"DateTime"**, hat den Standardwert NULL.  
  
 [  **@date_last_modified =**] *Date_modified*  
 Das Datum, an dem der Auftrag zuletzt geändert wurde. *DATE_MODIFIED* ist **"DateTime"**, hat den Standardwert NULL.  
  
 [  **@description =**] **"***ist NULL***"**  
 Die Beschreibung des Auftrags. *ist NULL* ist **vom Datentyp nvarchar(512)**, hat den Standardwert NULL. *ist NULL* kann die SQL Server-Platzhalterzeichen für den Mustervergleich enthalten.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Wenn keine Argumente angegeben werden, **Sp_help_job** gibt dieses Resultset zurück.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**job_id**|**uniqueidentifier**|Die eindeutige ID des Auftrags.|  
|**originating_server**|**nvarchar(30)**|Name des Servers, von dem der Auftrag stammt|  
|**name**|**sysname**|Name des Auftrags.|  
|**Aktiviert**|**tinyint**|Zeigt an, ob der Auftrag für die Ausführung aktiviert ist.|  
|**description**|**nvarchar(512)**|Beschreibung für den Auftrag.|  
|**start_step_id**|**int**|ID des Schrittes in dem Auftrag, bei dem die Ausführung beginnen soll.|  
|**category**|**sysname**|Auftragskategorie|  
|**Besitzer**|**sysname**|Auftragsbesitzer|  
|**notify_level_eventlog**|**int**|**Bitmaske** , der angibt, unter welchen Umständen ein Benachrichtigungsereignis in das Microsoft Windows-Anwendungsprotokoll protokolliert werden sollen. Einer der folgenden Werte sind möglich:<br /><br /> **0** = Nie<br /><br /> **1** = bei erfolgreicher Ausführung des Auftrags<br /><br /> **2** = Bei Fehlschlagen des Auftrags<br /><br /> **3** = Immer, wenn der Auftrag abgeschlossen ist (unabhängig vom Ergebnis des Auftrags)|  
|**notify_level_email**|**int**|**Bitmaske** , der angibt, unter welchen Umständen bei Abschluss eines Auftrags eine Benachrichtigung per E-mail gesendet werden soll. Mögliche Werte sind die gleichen wie für **Notify_level_eventlog**.|  
|**notify_level_netsend**|**int**|**Bitmaske** , der angibt, unter welchen Umständen bei Abschluss eines Auftrags eine Netzwerknachricht gesendet werden soll. Mögliche Werte sind die gleichen wie für **Notify_level_eventlog**.|  
|**notify_level_page**|**int**|**Bitmaske** , der angibt, unter welchen Umständen bei Abschluss eines Auftrags eine Seite gesendet werden soll. Mögliche Werte sind die gleichen wie für **Notify_level_eventlog**.|  
|**notify_email_operator**|**sysname**|E-Mail-Name des Operators, der benachrichtigt werden soll.|  
|**notify_netsend_operator**|**sysname**|Name des Computers oder Benutzers, der beim Senden von Netzwerkmeldungen verwendet wird|  
|**notify_page_operator**|**sysname**|Name des Computers oder Benutzers, der beim Senden einer Pagerbenachrichtigung verwendet wird|  
|**delete_level**|**int**|**Bitmaske** , der angibt, unter welchen Umständen bei Abschluss eines Auftrags der Auftrag gelöscht werden soll. Mögliche Werte sind die gleichen wie für **Notify_level_eventlog**.|  
|**date_created**|**datetime**|Datum, an dem der Auftrag erstellt wurde.|  
|**date_modified**|**datetime**|Datum, an dem der Auftrag zuletzt geändert wurde.|  
|**version_number**|**int**|Version des Auftrags (wird automatisch jedes Mal aktualisiert, wenn der Auftrag geändert wird)|  
|**last_run_date**|**int**|Datum, an dem die Ausführung des Auftrags zuletzt gestartet wurde|  
|**last_run_time**|**int**|Uhrzeit, zu der die Ausführung des Auftrags zuletzt gestartet wurde|  
|**last_run_outcome**|**int**|Ergebnis des Auftrags bei der letzten Ausführung:<br /><br /> **0** = Fehler<br /><br /> **1** = war erfolgreich<br /><br /> **3** = abgebrochen<br /><br /> **5** = unbekannt|  
|**next_run_date**|**int**|Datum, für das die nächste Ausführung des Auftrags geplant ist|  
|**next_run_time**|**int**|Uhrzeit, zu der die nächste Ausführung des Auftrags geplant ist|  
|**next_run_schedule_id**|**int**|Zeitplan-ID für nächste Ausführung|  
|**current_execution_status**|**int**|Aktueller Ausführungsstatus|  
|**current_execution_step**|**sysname**|Aktueller Ausführungsschritt des Auftrags|  
|**current_retry_attempt**|**int**|Wenn der Auftrag ausgeführt wird und der Schritt wiederholt wurde, ist dies der aktuelle Wiederholungsversuch|  
|**has_step**|**int**|Anzahl der Auftragsschritte des Auftrags|  
|**has_schedule**|**int**|Anzahl der Auftragszeitpläne des Auftrags|  
|**has_target**|**int**|Die Anzahl der Zielserver des Auftrags.|  
|**type**|**int**|Auftragstyp:<br /><br /> 1 = Lokaler Auftrag<br /><br /> **2** = Multiserverauftrag.<br /><br /> **0** = Auftrag hat keine Zielserver.|  
  
 Wenn *Job_id* oder *Job_name* angegeben wird, **Sp_help_job** gibt die folgenden zusätzlichen Resultsets für Auftragsschritte, Auftragszeitpläne und Auftragszielserver zurück.  
  
 Im Folgenden wird das Resultset für Auftragsschritte aufgeführt.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**step_id**|**int**|Eindeutiger Bezeichner (für diesen Auftrag) für den Schritt|  
|**step_name**|**sysname**|Name des Schritts|  
|**subsystem**|**nvarchar(40)**|Subsystem, in dem der Schrittbefehl ausgeführt werden soll|  
|**Befehl**|**nvarchar(3200)**|Auszuführender Befehl|  
|**flags**|**nvarchar(4000)**|**Bitmaske** von Werten, die das Schrittverhalten steuern.|  
|**cmdexec_success_code**|**int**|Für eine **CmdExec** Schritt, dies ist der Prozessexitcode eines erfolgreichen Befehls.|  
|**on_success_action**|**nvarchar(4000)**|Mögliche Aktionen, wenn der Schritt erfolgreich durchgeführt wird:<br /><br /> **1** = beenden mit Erfolg.<br /><br /> **2** = beenden mit Fehler.<br /><br /> **3** = Gehe zum nächsten Schritt fort.<br /><br /> **4** = Gehe zu Schritt.|  
|**on_success_step_id**|**int**|Wenn **On_success_action** ist **4**, dadurch wird der nächste auszuführende Schritt angegeben.|  
|**on_fail_action**|**nvarchar(4000)**|Auszuführende Aktion, wenn der Schritt einen Fehler erzeugt. Werte sind die gleichen wie für **On_success_action**.|  
|**on_fail_step_id**|**int**|Wenn **On_fail_action** ist **4**, dadurch wird der nächste auszuführende Schritt angegeben.|  
|**server**|**sysname**|Reserviert.|  
|**database_name**|**sysname**|Für eine [!INCLUDE[tsql](../../includes/tsql-md.md)] Schritt, Hierbei handelt es sich um die Datenbank, in dem der Befehl ausgeführt wird.|  
|**database_user_name**|**sysname**|Für einen [!INCLUDE[tsql](../../includes/tsql-md.md)]-Schritt ist dies der Datenbank-Benutzerkontext, in dem der Befehl ausgeführt wird.|  
|**retry_attempts**|**int**|Die maximale Anzahl von Wiederholungsversuchen für den Befehl (falls er nicht erfolgreich ist), bevor der Schritt als fehlgeschlagen angesehen wird|  
|**retry_interval**|**int**|Das Intervall (in Minuten) zwischen den Wiederholungsversuchen|  
|**os_run_priority**|**varchar(4000)**|Reserviert.|  
|**output_file_name**|**varchar(200)**|Datei in die Befehlsausgabe geschrieben werden soll ([!INCLUDE[tsql](../../includes/tsql-md.md)] und **CmdExec** nur Schritte).|  
|**last_run_outcome**|**int**|Ergebnis der letzten Ausführung des Schritts:<br /><br /> **0** = Fehler<br /><br /> **1** = war erfolgreich<br /><br /> **3** = abgebrochen<br /><br /> **5** = unbekannt|  
|**last_run_duration**|**int**|Die Ausführungsdauer (in Sekunden) des Schritts bei der letzten Ausführung.|  
|**last_run_retries**|**int**|Anzahl der Wiederholungsversuche für den Befehl bei der letzten Ausführung des Schritts|  
|**last_run_date**|**int**|Datum, an dem die Ausführung des Schritts zuletzt gestartet wurde|  
|**last_run_time**|**int**|Uhrzeit, zu der die Ausführung des Schritts zuletzt gestartet wurde|  
|**proxy_id**|**int**|Proxy für den Auftragsschritt.|  
  
 Im Folgenden wird das Resultset für Auftragszeitpläne aufgeführt.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**schedule_id**|**int**|Bezeichner des Zeitplans (eindeutig für alle Aufträge)|  
|**schedule_name**|**sysname**|Name des Zeitplans (eindeutig nur für diesen Auftrag)|  
|**Aktiviert**|**int**|Gibt an, ob der Zeitplan aktiv ist (**1**) oder nicht (**0**).|  
|**freq_type**|**int**|Zeigt an, wann der Auftrag ausgeführt werden soll:<br /><br /> **1** = einmal<br /><br /> **4** = täglich<br /><br /> **8** = wöchentlich<br /><br /> **16** = monatlich<br /><br /> **32** = monatlich, relativ zu den **Freq_interval**<br /><br /> **64** = ausgeführt werden, wenn **SQLServerAgent** -Dienst gestartet wird.|  
|**freq_interval**|**int**|Tage, wenn der Auftrag ausgeführt wird. Der Wert hängt vom Wert der **Freq_type**. Weitere Informationen finden Sie unter [Sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)|  
|**freq_subday_type**|**Int**|Einheiten für **Freq_subday_interval**. Weitere Informationen finden Sie unter [Sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)|  
|**freq_subday_interval**|**int**|Anzahl der **Freq_subday_type** -Perioden zwischen den einzelnen Ausführungen des Auftrags auftreten. Weitere Informationen finden Sie unter [Sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)|  
|**freq_relative_interval**|**int**|Auftreten des geplanten Auftrags von der **Freq_interval** in jedem Monat. Weitere Informationen finden Sie unter [Sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)|  
|**freq_recurrence_factor**|**int**|Anzahl der Monate zwischen der geplanten Ausführung des Auftrags|  
|**active_start_date**|**int**|Datum, an dem die Ausführung des Auftrags beginnen soll|  
|**active_end_date**|**int**|Datum, an dem die Ausführung des Auftrags beendet werden soll|  
|**active_start_time**|**int**|Zeitpunkt für den Beginn der Ausführung des Auftrags auf **Active_start_date.**|  
|**active_end_time**|**int**|Uhrzeit, zu der die Ausführung des Auftrags auf **Active_end_date**.|  
|**date_created**|**datetime**|Datum, an dem der Zeitplan erstellt wird|  
|**schedule_description**|**nvarchar(4000)**|Eine Beschreibung des Zeitplans in englischer Sprache (falls angefordert).|  
|**next_run_date**|**int**|Datum, an dem der Zeitplan die nächste Ausführung des Auftrags bewirken wird|  
|**next_run_time**|**int**|Uhrzeit, zu der der Zeitplan die nächste Ausführung des Auftrags bewirken wird|  
|**schedule_uid**|**uniqueidentifier**|Bezeichner für den Zeitplan.|  
|**job_count**|**int**|Gibt die Anzahl Aufträge zurück, die auf diesen Zeitplan verweisen|  
  
 Im Folgenden wird das Resultset für Auftragszielserver aufgeführt.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**server_id**|**int**|Bezeichner des Zielservers|  
|**server_name**|**nvarchar(30)**|Computername des Zielservers|  
|**enlist_date**|**datetime**|Datum, an dem der Zielserver auf dem Masterserver eingetragen wurde|  
|**last_poll_date**|**datetime**|Datum, an dem der Zielserver den Masterserver zuletzt abgerufen hat|  
|**last_run_date**|**int**|Datum, an dem die Ausführung des Auftrags auf diesem Zielserver zuletzt gestartet wurde|  
|**last_run_time**|**int**|Uhrzeit, zu der die Ausführung des Auftrags auf diesem Zielserver zuletzt gestartet wurde|  
|**last_run_duration**|**int**|Dauer des Auftrags bei der letzten Ausführung auf diesem Zielserver|  
|**last_run_outcome**|**tinyint**|Ergebnis des Auftrags bei der letzten Ausführung auf diesem Server:<br /><br /> **0** = Fehler<br /><br /> **1** = war erfolgreich<br /><br /> **3** = abgebrochen<br /><br /> **5** = unbekannt|  
|**last_outcome_message**|**nvarchar(1024)**|Ergebnismeldung des Auftrags bei der letzten Ausführung auf diesem Zielserver|  
  
## <a name="permissions"></a>Berechtigungen  
 Standardmäßig können nur Mitglieder der festen Serverrolle **sysadmin** diese gespeicherte Prozedur ausführen. Andere Benutzer müssen Mitglieder der festen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Datenbankrollen in der **msdb** -Datenbank sein:  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Weitere Informationen zu den Berechtigungen dieser Rollen finden Sie unter [Feste Datenbankrollen des SQL Server-Agents](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
 Mitglieder der **SQLAgentUserRole** können nur ihren eigenen Aufträgen anzeigen. Mitglieder der **Sysadmin**, **SQLAgentReaderRole**, und **SQLAgentOperatorRole** können alle lokalen und Multiserveraufträge Aufträge anzeigen.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-list-information-for-all-jobs"></a>A. Auflisten von Informationen für alle Aufträge  
 Das folgende Beispiel führt die `sp_help_job`-Prozedur ohne Parameter aus, um Informationen für alle aktuell in der `msdb`-Datenbank definierten Aufträge zurückzugeben.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_job ;  
GO  
```  
  
### <a name="b-listing-information-for-jobs-matching-a-specific-criteria"></a>B. Auflisten von Informationen für Aufträge, die ein bestimmtes Kriterium erfüllen  
 Im folgenden Beispiel werden Auftragsinformationen für die Multiserveraufträge im Besitz von `françoisa` aufgelistet, wenn der Auftrag aktiviert und ausgeführt wird.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_job   
   @job_type = N'MULTI-SERVER',  
   @owner_login_name = N'françoisa',  
   @enabled = 1,  
   @execution_status = 1 ;  
GO  
```  
  
### <a name="c-listing-all-aspects-of-information-for-a-job"></a>C. Auflisten aller Aspekte der Informationen für einen Auftrag  
 Im folgenden Beispiel werden alle Aspekte der Informationen für den Auftrag `NightlyBackups` aufgelistet.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_job  
    @job_name = N'NightlyBackups',  
    @job_aspect = N'ALL' ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sp_add_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-job-transact-sql.md)   
 [sp_delete_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [sp_update_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

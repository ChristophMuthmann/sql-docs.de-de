---
title: Sp_add_job (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- sp_add_job_TSQL
- sp_add_job
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_job
ms.assetid: 6ca8fe2c-7b1c-4b59-b4c7-e3b7485df274
caps.latest.revision: 31
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a71f128947a3e8acc08760ed19c31af949210384
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spaddjob-transact-sql"></a>sp_add_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Fügt einen neuen Auftrag hinzu, der vom SQLServerAgent-Dienst ausgeführt wird.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_add_job [ @job_name = ] 'job_name'  
     [ , [ @enabled = ] enabled ]   
     [ , [ @description = ] 'description' ]   
     [ , [ @start_step_id = ] step_id ]   
     [ , [ @category_name = ] 'category' ]   
     [ , [ @category_id = ] category_id ]   
     [ , [ @owner_login_name = ] 'login' ]   
     [ , [ @notify_level_eventlog = ] eventlog_level ]   
     [ , [ @notify_level_email = ] email_level ]   
     [ , [ @notify_level_netsend = ] netsend_level ]   
     [ , [ @notify_level_page = ] page_level ]   
     [ , [ @notify_email_operator_name = ] 'email_name' ]   
          [ , [ @notify_netsend_operator_name = ] 'netsend_name' ]   
     [ , [ @notify_page_operator_name = ] 'page_name' ]   
     [ , [ @delete_level = ] delete_level ]   
     [ , [ @job_id = ] job_id OUTPUT ]   
```  
  
## <a name="arguments"></a>Argumente  
 [  **@job_name =** ] **"***Job_name***"**  
 Der Name des Auftrags. Der Name muss eindeutig sein und dürfen nicht den Prozentsatz (**%**) Zeichen. *Job_name*ist **vom Datentyp nvarchar(128)**, hat keinen Standardwert.  
  
 [ **@enabled =** ] *enabled*  
 Gibt den Status des hinzugefügten Auftrags an. *aktiviert*ist **"tinyint"**, hat den Standardwert 1 (aktiviert). Wenn **0**, der Auftrag nicht aktiviert ist und nicht gemäß dem Zeitplan ausgeführt; allerdings er manuell ausgeführt werden kann.  
  
 [ **@description =** ] **'***description***'**  
 Die Beschreibung des Auftrags. *Beschreibung* ist **vom Datentyp nvarchar(512)**, hat den Standardwert NULL. Wenn *Beschreibung* wird weggelassen, wird "Keine Beschreibung verfügbar" verwendet.  
  
 [ **@start_step_id =** ] *step_id*  
 Die ID des ersten Schritts zum Ausführen des Auftrags. *Step_id*ist **Int**, hat den Standardwert 1.  
  
 [ **@category_name =** ] **'***category***'**  
 Die Kategorie für den Auftrag. *Kategorie*ist **Sysname**, hat den Standardwert NULL.  
  
 [ **@category_id =** ] *category_id*  
 Ein sprachenunabhängiger Mechanismus zum Angeben einer Auftragskategorie. *Category_id*ist **Int**, hat den Standardwert NULL.  
  
 [ **@owner_login_name =** ] **'***login***'**  
 Der Name der Anmeldung, die im Besitz des Auftrags ist. *Anmeldung*ist **Sysname**, hat den Standardwert NULL, die als der aktuelle Anmeldename interpretiert wird. Nur Mitglieder der **Sysadmin** festen Serverrolle "" festlegen oder ändern Sie den Wert für **@owner_login_name**. Wenn Benutzer, die keine Mitglieder sind von der **Sysadmin** Rolle festlegen oder ändern Sie den Wert der **@owner_login_name**, Ausführung dieser gespeicherten Prozedur ein Fehler auftritt und ein Fehler zurückgegeben.  
  
 [ **@notify_level_eventlog =** ] *eventlog_level*  
 Ein Wert, der angibt, wann im Microsoft Windows-Anwendungsprotokoll ein Eintrag für diesen Auftrag hinzugefügt werden soll. *ist NULL*ist **Int**, und kann einen der folgenden Werte sein.  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|**0**|Never|  
|**1**|Bei Erfolg|  
|**2** (Standardwert)|Bei einem Fehler|  
|**3**|Always|  
  
 [ **@notify_level_email =** ] *email_level*  
 Ein Wert, der angibt, wann nach dem Abschluss dieses Auftrags eine E-Mail gesendet werden soll. *Email_level*ist **Int**, hat den Standardwert **0**, die "nie" bedeutet. *Email_level*verwendet die gleichen Werte wie *ist NULL*.  
  
 [ **@notify_level_netsend =** ] *netsend_level*  
 Ein Wert, der angibt, wann nach dem Abschluss dieses Auftrags eine Netzwerknachricht gesendet werden soll. *Netsend_level*ist **Int**, hat den Standardwert **0**, die "nie" bedeutet. *Netsend_level* verwendet die gleichen Werte wie *ist NULL*.  
  
 [ **@notify_level_page =** ] *page_level*  
 Ein Wert, der angibt, wann nach dem Abschluss dieses Auftrags eine Pagernachricht gesendet werden soll. *Page_level*ist **Int**, hat den Standardwert **0**, die "nie" bedeutet. *Page_level*verwendet die gleichen Werte wie *ist NULL*.  
  
 [  **@notify_email_operator_name =** ] **"***e-Mail-Name***"**  
 Der e-Mail-Name der Person, die für das Senden von E-mail, wenn *Email_level* erreicht ist. *e-Mail-Name* ist **Sysname**, hat den Standardwert NULL.  
  
 [ **@notify_netsend_operator_name =** ] **'***netsend_name***'**  
 Der Name des Operators, an den nach dem Abschluss dieses Auftrags die Netzwerknachricht gesendet wird. *Netsend_name*ist **Sysname**, hat den Standardwert NULL.  
  
 [  **@notify_page_operator_name =** ] **"***Seitenname***"**  
 Der Name der Person, die nach dem Abschluss dieses Auftrags per Pager benachrichtigt werden soll. *Seitenname*ist **Sysname**, hat den Standardwert NULL.  
  
 [ **@delete_level =** ] *delete_level*  
 Ein Wert, der angibt, wann der Auftrag gelöscht werden soll. *delete_level*ist **Int**, hat den Standardwert 0, womit nie. *Auftrag nie gelöscht*verwendet die gleichen Werte wie *ist NULL*.  
  
> [!NOTE]  
>  Wenn *Auftrag nie gelöscht* ist **3**, dem der Auftrag nur einmal ausgeführt wird, unabhängig von Zeitplänen für den Auftrag definierten. Darüber hinaus wird, wenn sich ein Auftrag selbst löscht, auch der gesamte Verlauf für diesen Auftrag gelöscht.  
  
 [ **@job_id =** ] *job_id***OUTPUT**  
 Die Auftrags-ID, die dem Auftrag zugewiesen wird, wenn er erfolgreich erstellt wurde. *Job_id*ist eine Ausgabevariable vom Typ **"uniqueidentifier"**, hat den Standardwert NULL.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="remarks"></a>Hinweise  
 **@originating_server** vorhanden ist, **Sp_add_job** jedoch nicht unter den Argumenten aufgeführt. **@originating_server** ist für die interne Verwendung reserviert.  
  
 Nach dem **Sp_add_job** wurde ausgeführt, um einen Auftrag hinzuzufügen **Sp_add_jobstep** zum Hinzufügen von Schritten, mit denen die Aktivitäten für den Auftrag verwendet werden können. **Sp_add_jobschedule** können den Zeitplan zu erstellen, die die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienst verwendet wird, um den Auftrag ausführt. Verwendung **Sp_add_jobserver** festzulegende der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instanz, in dem der Auftrag ausgeführt wird, und **Sp_delete_jobserver** So entfernen Sie den Auftrag aus der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instanz.  
  
 Wenn der Auftrag auf mindestens einem Zielserver in einer Umgebung mit mehreren Servern ausgeführt wird, verwenden Sie **Sp_apply_job_to_targets** legen Sie die ausgewählten Zielservern oder Zielservergruppen für den Auftrag. Verwenden Sie zum Entfernen von Aufträgen von Zielservern oder Zielservergruppen **Sp_remove_job_from_targets**.  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] können Aufträge problemlos mithilfe einer grafischen Oberfläche verwaltet werden. Dies ist die empfohlene Vorgehensweise für die Erstellung und Verwaltung der Auftragsinfrastruktur.  
  
## <a name="permissions"></a>Berechtigungen  
 Um diese gespeicherte Prozedur auszuführen, müssen Benutzer Mitglied sein der **Sysadmin** festen Serverrolle oder über eine der folgenden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Datenbankrollen, die sich im befinden der **Msdb** Datenbank:  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Informationen über die spezifischen Berechtigungen, die mit jeder dieser festen einhergehen-Datenbankrollen, finden Sie unter [SQL Server Agent Fixed Database Roles](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
 Nur Mitglieder der **Sysadmin** festen Serverrolle "" festlegen oder ändern Sie den Wert für **@owner_login_name**. Wenn Benutzer, die keine Mitglieder sind von der **Sysadmin** Rolle festlegen oder ändern Sie den Wert der **@owner_login_name**, Ausführung dieser gespeicherten Prozedur ein Fehler auftritt und ein Fehler zurückgegeben.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-adding-a-job"></a>A. Hinzufügen eines Auftrags  
 Im folgenden Beispiel wird ein neuer Auftrag mit dem Namen `NightlyBackups` hinzugefügt.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_job  
    @job_name = N'NightlyBackups' ;  
GO  
```  
  
### <a name="b-adding-a-job-with-pager-e-mail-and-net-send-information"></a>B. Hinzufügen eines Auftrags mit Pager-, E-Mail- und NET SEND-Informationen  
 Im folgenden Beispiel wird der Auftrag `Ad hoc Sales Data Backup` erstellt, mit dem `François Ajenstat` (per Pager, E-Mail oder Netzwerk-Popupnachricht) benachrichtigt wird, falls der Auftrag einen Fehler erzeugt. Wenn der Auftrag erfolgreich ausgeführt wurde, wird er gelöscht.  
  
> [!NOTE]  
>  Im Rahmen dieses Beispiels wird davon ausgegangen, dass der Operator `François Ajenstat` und der Anmeldename `françoisa` bereits vorhanden sind.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_job  
    @job_name = N'Ad hoc Sales Data Backup',   
    @enabled = 1,  
    @description = N'Ad hoc backup of sales data',  
    @owner_login_name = N'françoisa',  
    @notify_level_eventlog = 2,  
    @notify_level_email = 2,  
    @notify_level_netsend = 2,  
    @notify_level_page = 2,  
    @notify_email_operator_name = N'François Ajenstat',  
    @notify_netsend_operator_name = N'François Ajenstat',   
    @notify_page_operator_name = N'François Ajenstat',  
    @delete_level = 1 ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_add_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)   
 [sp_add_jobserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md)   
 [sp_apply_job_to_targets &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-apply-job-to-targets-transact-sql.md)   
 [sp_delete_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [sp_delete_jobserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)   
 [sp_remove_job_from_targets &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-remove-job-from-targets-transact-sql.md)   
 [sp_help_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_help_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql.md)   
 [sp_update_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

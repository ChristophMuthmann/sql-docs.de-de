---
title: Sp_update_job (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2016
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
- sp_update_job
- sp_update_job_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_update_job
ms.assetid: cbdfea38-9e42-47f3-8fc8-5978b82e2623
caps.latest.revision: "39"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 772cfb0f8f4a05c2db42e650601f837d12ffeb81
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="spupdatejob-transact-sql"></a>sp_update_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ändert die Attribute eines Auftrags.  
  

  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_update_job [ @job_id =] job_id | [@job_name =] 'job_name'  
     [, [@new_name =] 'new_name' ]   
     [, [@enabled =] enabled ]  
     [, [@description =] 'description' ]   
     [, [@start_step_id =] step_id ]  
     [, [@category_name =] 'category' ]   
     [, [@owner_login_name =] 'login' ]  
     [, [@notify_level_eventlog =] eventlog_level ]  
     [, [@notify_level_email =] email_level ]  
     [, [@notify_level_netsend =] netsend_level ]  
     [, [@notify_level_page =] page_level ]  
     [, [@notify_email_operator_name =] 'operator_name' ]  
     [, [@notify_netsend_operator_name =] 'netsend_operator' ]  
     [, [@notify_page_operator_name =] 'page_operator' ]  
     [, [@delete_level =] delete_level ]   
     [, [@automatic_post =] automatic_post ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@job_id =**] *Job_id*  
 Die ID des Auftrags, der aktualisiert werden soll. *Job_id*ist **"uniqueidentifier"**.  
  
 [  **@job_name =**] **"***Job_name***"**  
 Der Name des Auftrags. *Job_name*ist **vom Datentyp nvarchar(128)**.  
  
> **Hinweis:** entweder *Job_id* oder *Job_name* muss angegeben werden, aber beide können nicht angegeben werden.  
  
 [  **@new_name =**] **"***New_name***"**  
 Der neue Name des Auftrags. *New_name*ist **vom Datentyp nvarchar(128)**.  
  
 [  **@enabled =**] *aktiviert*  
 Gibt an, ob der Auftrag aktiviert ist (**1**) oder nicht aktiviert (**0**). *aktiviert*ist **"tinyint"**.  
  
 [  **@description =**] **"***Beschreibung***"**  
 Die Beschreibung des Auftrags. *Beschreibung* ist **vom Datentyp nvarchar(512)**.  
  
 [  **@start_step_id =**] *Step_id*  
 Die ID des ersten Schritts zum Ausführen des Auftrags. *Step_id*ist **Int**.  
  
 [  **@category_name =**] **"***Kategorie***"**  
 Die Auftragskategorie. *Kategorie*ist **vom Datentyp nvarchar(128)**.  
  
 [  **@owner_login_name =**] **"***Anmeldung***"**  
 Der Name der Anmeldung, die im Besitz des Auftrags ist. *Anmeldung*ist **vom Datentyp nvarchar(128)** nur Mitglieder der der **Sysadmin** festen Serverrolle kann den Auftragsbesitz ändern.  
  
 [  **@notify_level_eventlog =**] *ist NULL*  
 Gibt an, wann für diesen Auftrag ein Eintrag im Microsoft Windows-Anwendungsprotokoll eingefügt werden soll. *ist NULL*ist **Int**, und kann einen der folgenden Werte sein.  
  
|Wert|Beschreibung (Aktion)|  
|-----------|----------------------------|  
|**0**|Never|  
|**1**|Bei Erfolg|  
|**2**|Bei einem Fehler|  
|**3**|Always|  
  
 [  **@notify_level_email =**] *Email_level*  
 Gibt an, wann nach dem Abschluss dieses Auftrags eine E-Mail gesendet werden soll. *Email_level*ist **Int**. *Email_level*verwendet die gleichen Werte wie *ist NULL*.  
  
 [  **@notify_level_netsend =**] *Netsend_level*  
 Gibt an, wann nach dem Abschluss dieses Auftrags eine Netzwerkmeldung gesendet werden soll. *Netsend_level*ist **Int**. *Netsend_level*verwendet die gleichen Werte wie *ist NULL*.  
  
 [  **@notify_level_page =**] *Page_level*  
 Gibt an, wann nach dem Abschluss dieses Auftrags eine Seite gesendet werden soll. *Page_level*ist **Int**. *Page_level*verwendet die gleichen Werte wie *ist NULL*.  
  
 [  **@notify_email_operator_name =**] **"***Operatorname***"**  
 Der Name des Operators, an die e-Mail-Nachricht, wenn gesendet wird *Email_level* erreicht ist. *e-Mail-Name* ist **vom Datentyp nvarchar(128)**.  
  
 [  **@notify_netsend_operator_name =**] **"***Netsend_operator***"**  
 Der Name des Operators, an den die Netzwerknachricht gesendet wird. *Netsend_operator* ist **vom Datentyp nvarchar(128)**.  
  
 [  **@notify_page_operator_name =**] **"***Page_operator***"**  
 Der Name des Operators, an den eine Seite gesendet wird. *Page_operator* ist **vom Datentyp nvarchar(128)**.  
  
 [  **@delete_level =**] *Auftrag nie gelöscht*  
 Gibt an, wann der Auftrag gelöscht werden soll. *delete_level*ist **Int**. *Auftrag nie gelöscht*verwendet die gleichen Werte wie *ist NULL*.  
  
 [  **@automatic_post =**] *Automatic_post*  
 Reserviert.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_update_job** muss ausgeführt werden, aus der **Msdb** Datenbank.  
  
 **Sp_update_job** ändert nur die Einstellungen für die Parameterwerte angegeben werden. Wird ein Parameter nicht angegeben, wird die aktuelle Einstellung beibehalten.  
  
## <a name="permissions"></a>Berechtigungen  
 Standardmäßig können nur Mitglieder der festen Serverrolle **sysadmin** diese gespeicherte Prozedur ausführen. Andere Benutzer müssen Mitglieder der festen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Datenbankrollen in der **msdb** -Datenbank sein:  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Weitere Informationen zu den Berechtigungen dieser Rollen finden Sie unter [Feste Datenbankrollen des SQL Server-Agents](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
 Nur Mitglieder der **Sysadmin** können diese gespeicherte Prozedur verwenden, um Attribute von Aufträgen zu bearbeiten, die von anderen Benutzern gehören.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden der Name, die Beschreibung und der aktivierte Status des Auftrags `NightlyBackups` geändert.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_job  
    @job_name = N'NightlyBackups',  
    @new_name = N'NightlyBackups -- Disabled',  
    @description = N'Nightly backups disabled during server migration.',  
    @enabled = 0 ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sp_add_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-job-transact-sql.md)   
 [Sp_delete_job &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [Sp_help_job &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

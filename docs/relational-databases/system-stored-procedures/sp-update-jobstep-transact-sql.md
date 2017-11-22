---
title: Sp_update_jobstep (Transact-SQL) | Microsoft Docs
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
- sp_update_jobstep
- sp_update_jobstep_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_update_jobstep
ms.assetid: e158802c-c347-4a5d-bf75-c03e5ae56e6b
caps.latest.revision: "33"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 4708d2cfe45f192a80836f592e3f774378eeb03e
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="spupdatejobstep-transact-sql"></a>sp_update_jobstep (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ändert die Einstellung für einen Schritt eines Auftrags, mit dem automatische Aktivitäten ausgeführt werden.  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_update_jobstep   
     {   [@job_id =] job_id   
       | [@job_name =] 'job_name' } ,  
     [@step_id =] step_id  
     [ , [@step_name =] 'step_name' ]  
     [ , [@subsystem =] 'subsystem' ]   
     [ , [@command =] 'command' ]  
     [ , [@additional_parameters =] 'parameters' ]  
     [ , [@cmdexec_success_code =] success_code ]  
     [ , [@on_success_action =] success_action ]   
     [ , [@on_success_step_id =] success_step_id ]  
     [ , [@on_fail_action =] fail_action ]   
     [ , [@on_fail_step_id =] fail_step_id ]  
     [ , [@server =] 'server' ]   
     [ , [@database_name =] 'database' ]  
     [ , [@database_user_name =] 'user' ]   
     [ , [@retry_attempts =] retry_attempts ]  
     [ , [@retry_interval =] retry_interval ]   
     [ , [@os_run_priority =] run_priority ]  
     [ , [@output_file_name =] 'file_name' ]   
     [ , [@flags =] flags ]  
     [ ,  {   [ @proxy_id = ] proxy_id   
            | [ @proxy_name = ] 'proxy_name' }   
```  
  
## <a name="arguments"></a>Argumente  
 [  **@job_id =**] *Job_id*  
 Die ID des Auftrags, zu dem der Schritt gehört. *Job_id*ist **"uniqueidentifier"**, hat den Standardwert NULL. Entweder *Job_id* oder *Job_name* muss angegeben werden, aber beide können nicht angegeben werden.  
  
 [  **@job_name =**] **"***Job_name***"**  
 Der Name des Auftrags, zu dem der Schritt gehört. *Job_name*ist **Sysname**, hat den Standardwert NULL. Entweder *Job_id* oder *Job_name* muss angegeben werden, aber beide können nicht angegeben werden.  
  
 [  **@step_id =**] *Step_id*  
 Die ID des Auftragsschrittes, der geändert werden soll. Diese ID kann nicht geändert werden. *Step_id*ist **Int**, hat keinen Standardwert.  
  
 [  **@step_name =**] **"***Step_name***"**  
 Ein neuer Name für den Schritt. *Step_name*ist **Sysname**, hat den Standardwert NULL.  
  
 [  **@subsystem =**] **"***Subsystem***"**  
 Das Subsystem, das zum Ausführen von Microsoft SQL Server-Agent verwendet *Befehl*. *Subsystem* ist **nvarchar(40)**, hat den Standardwert NULL.  
  
 [  **@command =**] **"***Befehl***"**  
 Die Befehle, die über auszuführenden *Subsystem*. *Befehl* ist **nvarchar(max)**, hat den Standardwert NULL.  
  
 [  **@additional_parameters =**] **"***Parameter***"**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@cmdexec_success_code =**] *Success_code*  
 Der zurückgegebene Wert eine **CmdExec** -Subsystembefehl gibt an, dass *Befehl* erfolgreich ausgeführt wurde. *Success_code* ist **Int**, hat den Standardwert NULL.  
  
 [  **@on_success_action =**] *Success_action*  
 Die Aktion ausführen, wenn der Schritt erfolgreich ausgeführt wurde. *Success_action* ist **"tinyint"**, hat den Standardwert NULL und kann einen der folgenden Werte sein.  
  
|Wert|Beschreibung (Aktion)|  
|-----------|----------------------------|  
|**1**|Beenden mit Erfolg|  
|**2**|Beenden mit Fehler|  
|**3**|Gehe zum nächsten Schritt|  
|**4**|Wechseln Sie zu Schritt *Success_step_id.*|  
  
 [  **@on_success_step_id =**] *Success_step_id*  
 Die ID des Schritts in diesem Auftrag, der ausgeführt werden, wenn der Schritt erfolgreich ausgeführt wurde und *Success_action* ist **4**. *Success_step_id* ist **Int**, hat den Standardwert NULL.  
  
 [  **@on_fail_action =**] *fail_action gleich*  
 Die Aktion, die ausgeführt werden soll, wenn der Schritt fehlschlägt. *fail_action gleich* ist **"tinyint"**, hat den Standardwert NULL und kann einen der folgenden Werte aufweisen.  
  
|Wert|Beschreibung (Aktion)|  
|-----------|----------------------------|  
|**1**|Beenden mit Erfolg|  
|**2**|Beenden mit Fehler|  
|**3**|Gehe zum nächsten Schritt|  
|**4**|Wechseln Sie zu Schritt *Fail_step_id**.*|  
  
 [  **@on_fail_step_id =**] *Fail_step_id*  
 Die ID des Schritts in diesem Auftrag, der ausgeführt werden, wenn der Schritt fehlschlägt und *fail_action gleich* ist **4**. *Fail_step_id* ist **Int**, hat den Standardwert NULL.  
  
 [  **@server =**] **"***Server***"**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]*Server* ist **vom Datentyp nvarchar(128)**, hat den Standardwert NULL.  
  
 [  **@database_name =**] **"***Datenbank***"**  
 Der Name der Datenbank, in der ein [!INCLUDE[tsql](../../includes/tsql-md.md)]-Schritt ausgeführt werden soll. *Datenbank*ist **Sysname**. In eckige Klammern ([ ]) eingeschlossene Namen sind nicht zulässig. Der Standardwert ist NULL.  
  
 [  **@database_user_name =**] **"***Benutzer***"**  
 Der Name des Benutzerkontos, das beim Ausführen eines [!INCLUDE[tsql](../../includes/tsql-md.md)]-Schritts verwendet werden soll. *Benutzer*ist **Sysname**, hat den Standardwert NULL.  
  
 [  **@retry_attempts =**] *Retry_attempts*  
 Die Anzahl der Wiederholungsversuche für den Fall, dass dieser Schritt fehlschlägt. *Retry_attempts*ist **Int**, hat den Standardwert NULL.  
  
 [  **@retry_interval =**] *Retry_interval*  
 Der Zeitraum in Minuten zwischen zwei Wiederholungsversuchen. *Retry_interval* ist **Int**, hat den Standardwert NULL.  
  
 [  **@os_run_priority =**] *Run_priority*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@output_file_name =**] **"***File_name***"**  
 Der Name der Datei, in der die Ausgabe dieses Schritts gespeichert wird. *File_name* ist **nvarchar(200)-Datentyp gepackt ist**, hat den Standardwert NULL. Dieser Parameter ist nur mit Befehlen gültig, die in [!INCLUDE[tsql](../../includes/tsql-md.md)]- oder CmdExec-Subsystemen ausgeführt werden.  
  
 Ausgabedateiname zurück auf NULL festlegen möchten, müssen Sie festlegen *Ausgabedateiname* auf eine leere Zeichenfolge ("") oder in eine Zeichenfolge mit Leerzeichen, aber Sie können keine der **CHAR(32)** Funktion. Sie können dieses Argument z. B. wie folgt auf eine leere Zeichenfolge festlegen:  
  
 **@output_file_name = ' '**  
  
 [  **@flags =**] *Flags*  
 Eine Option, die das Verhalten steuert. *Flags* ist **Int**, und kann einen der folgenden Werte sein.  
  
|Wert|Description|  
|-----------|-----------------|  
|**0** (Standardwert)|Ausgabedatei überschreiben.|  
|**2**|An Ausgabedatei anfügen|  
|**4**|Ausgabe des Transact-SQL-Auftragsschrittes in Schrittverlauf schreiben|  
|**8**|Protokoll in Tabelle schreiben (vorhandenen Verlauf überschreiben)|  
|**16**|Protokoll in Tabelle schreiben (an vorhandenen Verlauf anfügen)|  
  
 [  **@proxy_id** =] *Proxy_id*  
 Die ID des Proxys, als der der Auftragsschritt ausgeführt wird. *Proxy_id* Typ **Int**, hat den Standardwert NULL. Wenn kein *Proxy_id* angegeben wird, keine *Proxy_name* angegeben wird, und es wird kein *User_name* angegeben ist, wird der Auftragsschritt ausgeführt wird, als das Dienstkonto für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
 [  **@proxy_name** =] **"***Proxy_name***"**  
 Der Name des Proxys, als der der Auftragsschritt ausgeführt wird. *Proxy_name* Typ **Sysname**, hat den Standardwert NULL. Wenn kein *Proxy_id* angegeben wird, keine *Proxy_name* angegeben wird, und es wird kein *User_name* angegeben ist, wird der Auftragsschritt ausgeführt wird, als das Dienstkonto für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_update_jobstep** muss ausgeführt werden, aus der **Msdb** Datenbank.  
  
 Beim Aktualisieren eines Auftragsschrittes wird die Versionsnummer des Auftrags erhöht.  
  
## <a name="permissions"></a>Berechtigungen  
 Standardmäßig können nur Mitglieder der festen Serverrolle **sysadmin** diese gespeicherte Prozedur ausführen. Andere Benutzer müssen Mitglieder der festen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Datenbankrollen in der **msdb** -Datenbank sein:  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Weitere Informationen zu den Berechtigungen dieser Rollen finden Sie unter [Feste Datenbankrollen des SQL Server-Agents](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
 Nur Mitglieder der **Sysadmin** ein Auftragsschritts, der Besitz eines anderen Benutzers aktualisieren können.  
  
 Falls für den Auftragsschritt der Zugriff auf einen Proxy erforderlich ist, muss der Ersteller des Auftragsschrittes Zugriff auf den Proxy für den Auftragsschritt haben. Alle Subsysteme außer Transact-SQL erfordern ein Proxykonto. Mitglieder der **Sysadmin** haben Zugriff auf alle Proxys und können die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienstkonto für den Proxy.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die Anzahl der Wiederholungsversuche für den ersten Schritt des `Weekly Sales Data Backup`-Auftrags geändert. Nach Ausführung dieses Beispiels ist die Anzahl der Wiederholungsversuche auf `10` festgelegt.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_jobstep  
    @job_name = N'Weekly Sales Data Backup',  
    @step_id = 1,  
    @retry_attempts = 10 ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Anzeigen oder Ändern von Aufträgen](http://msdn.microsoft.com/library/57f649b8-190c-4304-abd7-7ca5297deab7)   
 [Sp_delete_jobstep &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql.md)   
 [Sp_help_jobstep &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

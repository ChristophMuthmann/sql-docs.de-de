---
title: Sp_add_jobstep (Transact-SQL) | Microsoft Docs
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
- sp_add_jobstep_TSQL
- sp_add_jobstep
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_jobstep
ms.assetid: 97900032-523d-49d6-9865-2734fba1c755
caps.latest.revision: 80
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: eea1729d2f33cffb37ffdd803739f9b65d77fc83
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spaddjobstep-transact-sql"></a>sp_add_jobstep (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Fügen einem Auftrag einen Schritt (Vorgang) hinzu.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_add_jobstep [ @job_id = ] job_id | [ @job_name = ] 'job_name'   
     [ , [ @step_id = ] step_id ]   
     { , [ @step_name = ] 'step_name' }   
     [ , [ @subsystem = ] 'subsystem' ]   
     [ , [ @command = ] 'command' ]   
     [ , [ @additional_parameters = ] 'parameters' ]   
          [ , [ @cmdexec_success_code = ] code ]   
     [ , [ @on_success_action = ] success_action ]   
          [ , [ @on_success_step_id = ] success_step_id ]   
          [ , [ @on_fail_action = ] fail_action ]   
          [ , [ @on_fail_step_id = ] fail_step_id ]   
     [ , [ @server = ] 'server' ]   
     [ , [ @database_name = ] 'database' ]   
     [ , [ @database_user_name = ] 'user' ]   
     [ , [ @retry_attempts = ] retry_attempts ]   
     [ , [ @retry_interval = ] retry_interval ]   
     [ , [ @os_run_priority = ] run_priority ]   
     [ , [ @output_file_name = ] 'file_name' ]   
     [ , [ @flags = ] flags ]   
     [ , { [ @proxy_id = ] proxy_id   
         | [ @proxy_name = ] 'proxy_name' } ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@job_id =** ] *job_id*  
 Die ID des Auftrags, dem der Schritt hinzugefügt werden soll. *Job_id* ist **"uniqueidentifier"**, hat den Standardwert NULL.  
  
 [  **@job_name =** ] **"***Job_name***"**  
 Der Name des Auftrags, dem der Schritt hinzugefügt werden soll. *Job_name* ist **Sysname**, hat den Standardwert NULL.  
  
> [!NOTE]  
>  Entweder *Job_id* oder *Job_name* muss angegeben werden, aber beide können nicht angegeben werden.  
  
 [ **@step_id =** ] *step_id*  
 Die Sequenz-ID des Auftragsschritts. Schritt-IDs beginnen bei **1** und lückenlos erhöht. Wenn ein Schritt in eine vorhandene Sequenz eingefügt wird, werden die Sequenznummern automatisch angepasst. Ein Wert angegeben wird, wenn *Step_id* nicht angegeben wird. *Step_id*ist **Int**, hat den Standardwert NULL.  
  
 [  **@step_name =** ] **"***Step_name***"**  
 Der Name des Schrittes. *Step_name*ist **Sysname**, hat keinen Standardwert.  
  
 [  **@subsystem =** ] **"***Subsystem***"**  
 Das Subsystem verwendet werden, indem Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienst ausführen *Befehl*. *Subsystem* ist **nvarchar(40)**, und kann einen der folgenden Werte sein.  
  
|Wert|Description|  
|-----------|-----------------|  
|"**ACTIVESCRIPTING**"|Active Script<br /><br /> **\*\* Wichtig \*\*** [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]|  
|"**CMDEXEC**"|Betriebssystembefehl oder ausführbares Programm|  
|"**VERTEILUNG**"|Auftrag des Replikationsverteilungs-Agents|  
|"**MOMENTAUFNAHME**"|Auftrag des Replikationsmomentaufnahme-Agents|  
|"**PROTOKOLLLESER**"|Auftrag des Replikationsprotokolllese-Agents|  
|"**MERGE**"|Auftrag des Replikationsmerge-Agents|  
|"**QueueReader**"|Warteschlangenlese-Agent-Auftrag der Replikation|  
|"**DAS ANALYSISQUERY**"|Analysis Services-Abfrage (MDX, DMX)|  
|"**DAS ANALYSISCOMMAND**"|Analysis Services-Befehl (XMLA)|  
|"**Dts**"|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Paketausführung|  
|"**PowerShell**"|PowerShell-Skript|  
|"**TSQL**" (Standard)|[!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung|  
  
 [  **@command=** ] **"***Befehl***"**  
 Die Befehle von auszuführenden **SQLServerAgent** -Dienst über *Subsystem*. *Befehl* ist **nvarchar(max)**, hat den Standardwert NULL. Vom SQL Server-Agent wird eine Tokenersetzung bereitgestellt, die Ihnen beim Schreiben von Softwareprogrammen dieselbe Flexibilität wie Variablen bietet.  
  
> [!IMPORTANT]  
>  Damit Auftragsschritte fehlerfrei ausgeführt werden können, müssen alle in Auftragsschritten verwendeten Token von einem Escapemakro begleitet werden. Darüber hinaus müssen Sie Tokennamen nun in runde Klammern einschließen und ein Dollarzeichen (`$`) an den Anfang der Tokensyntax setzen. Beispiel:  
>   
>  `$(ESCAPE_`*Makronamen*`(DATE))`  
  
 Weitere Informationen zu diesen Token und Aktualisieren der Auftragsschritte, um die neue Tokensyntax finden Sie unter [Verwenden von Token in Auftragsschritten](http://msdn.microsoft.com/library/105bbb66-0ade-4b46-b8e4-f849e5fc4d43).  
  
> [!IMPORTANT]  
>  Jeder Windows-Benutzer mit Schreibberechtigungen für das Windows-Ereignisprotokoll kann auf Auftragsschritte zugreifen, die durch [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Warnungen oder WMI-Warnungen aktiviert werden. Zur Vermeidung dieses Sicherheitsrisikos sind [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Tokens, die in von Warnungen aktivierten Aufträgen verwendet werden können, standardmäßig deaktiviert. Dabei handelt es sich um folgende Token: **A-DBN**, **A-SVR**, **A-ERR**, **A-SEV**, **A-MSG**und **WMI(***Eigenschaft***)**. Beachten Sie, dass in dieser Version die Verwendung von Token auf alle Warnungen ausgeweitet ist.  
>   
>  Wenn Sie diese Token verwenden müssen, stellen Sie zuvor sicher, dass ausschließlich Mitglieder von vertrauenswürdigen Windows-Sicherheitsgruppen, wie der Administratorengruppe, über Schreibberechtigungen für das Ereignisprotokoll des Computers verfügen, auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird. Klicken Sie dann zum Aktivieren dieser Token im Objekt-Explorer mit der rechten Maustaste auf **SQL Server-Agent** , wählen Sie **Eigenschaften**, und wählen Sie anschließend auf der Seite **Warnungssystem** die Option **Token für alle Auftragsantworten auf Warnungen ersetzen** aus.  
  
 [ **@additional_parameters=** ] **'***parameters***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] *Parameter* ist **Ntext**, hat den Standardwert NULL.  
  
 [ **@cmdexec_success_code =** ] *code*  
 Der zurückgegebene Wert eine **CmdExec** -Subsystembefehl gibt an, dass *Befehl* erfolgreich ausgeführt wurde. *Code*ist **Int**, hat den Standardwert **0**.  
  
 [ **@on_success_action=** ] *success_action*  
 Die Aktion, die ausgeführt werden soll, wenn der Schritt erfolgreich ausgeführt wird. *Success_action*ist **"tinyint"**, und kann einen der folgenden Werte sein.  
  
|Wert|Beschreibung (Aktion)|  
|-----------|----------------------------|  
|**1** (Standard)|Beenden mit Erfolg|  
|**2**|Beenden mit Fehler|  
|**3**|Zum nächsten Schritt wechseln|  
|**4**|Wechseln Sie zu Schritt *On_success_step_id*|  
  
 [  **@on_success_step_id =** ] *Success_step_id*  
 Die ID des Schritts in diesem Auftrag ausführt, wenn der Schritt erfolgreich ausgeführt wurde und *Success_action*ist **4**. *Success_step_id*ist **Int**, hat den Standardwert **0**.  
  
 [  **@on_fail_action=** ] *fail_action gleich*  
 Die Aktion, die ausgeführt werden soll, wenn der Schritt fehlschlägt. *fail_action gleich*ist **"tinyint"**, und kann einen der folgenden Werte sein.  
  
|Wert|Beschreibung (Aktion)|  
|-----------|----------------------------|  
|**1**|Beenden mit Erfolg|  
|**2** (Standardwert)|Beenden mit Fehler|  
|**3**|Zum nächsten Schritt wechseln|  
|**4**|Wechseln Sie zu Schritt *On_fail_step_id*|  
  
 [ **@on_fail_step_id=** ] *fail_step_id*  
 Die ID des Schritts in diesem Auftrag ausführt, wenn der Schritt fehlschlägt und *fail_action gleich*ist **4**. *Fail_step_id*ist **Int**, hat den Standardwert **0**.  
  
 [ **@server =**] **'***server***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] *Server*ist **nvarchar(30)**, hat den Standardwert NULL.  
  
 [  **@database_name=** ] **"***Datenbank***"**  
 Der Name der Datenbank, in der ein [!INCLUDE[tsql](../../includes/tsql-md.md)]-Schritt ausgeführt werden soll. *Datenbank* ist **Sysname**, hat den Standardwert NULL, in diesem Fall die **master** Datenbank verwendet wird. In eckige Klammern ([ ]) eingeschlossene Namen sind nicht zulässig. Für ein ActiveX-Auftragsschritt der *Datenbank* ist der Name der Skriptsprache, die der Schritt verwendet.  
  
 [  **@database_user_name=** ] **"***Benutzer***"**  
 Der Name des Benutzerkontos, das beim Ausführen eines [!INCLUDE[tsql](../../includes/tsql-md.md)]-Schritts verwendet werden soll. *Benutzer* ist **Sysname**, hat den Standardwert NULL. Wenn *Benutzer* NULL ist, die Schritt ausgeführt wird, in einem Benutzerkontext des Auftragsbesitzers auf *Datenbank*.  SQL Server-Agent schließt nur diesen Parameter ein, wenn der Auftragsbesitzer ein SQL Server sysadmin ist. In diesem Fall wird der angegebene Transact-SQL-Schritt im Kontext des angegebenen SQL Server-Benutzernamens ausgeführt. Wenn der Besitzer des Auftrags ist kein der Rolle Sysadmin SQL Server, der Transact-SQL-Schritt immer im Kontext der Anmeldung, die diesen Auftrag besitzt ausgeführt und die @database_user_name -Parameter wird ignoriert.  
  
 [  **@retry_attempts=** ] *Retry_attempts*  
 Die Anzahl der Wiederholungsversuche für den Fall, dass dieser Schritt fehlschlägt. *Retry_attempts*ist **Int**, hat den Standardwert **0**, die keine Wiederholungsversuche.  
  
 [  **@retry_interval=** ] *Retry_interval*  
 Der Zeitraum in Minuten zwischen zwei Wiederholungsversuchen. *Retry_interval*ist **Int**, hat den Standardwert **0**, wodurch eine **0**-Minuten-Intervall.  
  
 [  **@os_run_priority =** ] *Run_priority*  
 Reserviert.  
  
 [  **@output_file_name=** ] **"***File_name***"**  
 Der Name der Datei, in der die Ausgabe dieses Schritts gespeichert wird. *File_name*ist **nvarchar(200)-Datentyp gepackt ist**, hat den Standardwert NULL. *File_name*kann eine oder mehrere der unter aufgeführten Token enthalten *Befehl*. Dieser Parameter gilt nur mit Befehlen, die auf die [!INCLUDE[tsql](../../includes/tsql-md.md)], **CmdExec**, **PowerShell**, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], oder [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Subsysteme.  
  
 [  **@flags=** ] *Flags*  
 Ist eine Option, die das Verhalten steuert. *Flags* ist **Int**, und kann einen der folgenden Werte sein.  
  
|Wert|Description|  
|-----------|-----------------|  
|**0** (Standardwert)|Ausgabedatei überschreiben|  
|**2**|An Ausgabedatei anfügen|  
|**4**|Ausgabe des [!INCLUDE[tsql](../../includes/tsql-md.md)]-Auftragsschritts in Schrittverlauf schreiben|  
|**8**|Protokoll in Tabelle schreiben (vorhandenen Verlauf überschreiben)|  
|**16**|Protokoll in Tabelle schreiben (an vorhandenen Verlauf anfügen)|  
|**32**|Schreiben der gesamten Ausgabe in den Auftragsverlauf|  
|**64**|Erstellen eines Windows-Ereignisses, das für den Cmd-Jobstep als Signal als Signal zum Abbruch verwendet werden soll|  
  
 [ **@proxy_id** = ] *proxy_id*  
 Die ID des Proxys, die als der Auftragsschritt ausgeführt wird. *Proxy_id* Typ **Int**, hat den Standardwert NULL. Wenn kein *Proxy_id* angegeben wird, keine *Proxy_name* angegeben wird, und es wird kein *User_name* angegeben ist, wird der Auftragsschritt ausgeführt wird, als das Dienstkonto für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
 [ **@proxy_name** =] **"***Proxy_name***"**  
 Der Name des Proxys, als der der Auftragsschritt ausgeführt wird. *Proxy_name* Typ **Sysname**, hat den Standardwert NULL. Wenn kein *Proxy_id* angegeben wird, keine *Proxy_name* angegeben wird, und es wird kein *User_name* angegeben ist, wird der Auftragsschritt ausgeführt wird, als das Dienstkonto für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="remarks"></a>Hinweise  
 **Sp_add_jobstep** muss ausgeführt werden, aus der **Msdb** Datenbank.  
  
 SQL Server Management Studio bietet eine einfache grafische Möglichkeit zum Verwalten von Aufträgen. Es handelt sich hierbei um die empfohlene Art und Weise zum Erstellen und Verwalten der Auftragsinfrastruktur.  
  
 Ein Auftragsschritt muss ein Proxy angegeben, es sei denn, der Ersteller des Auftragsschritts Mitglied ist die **Sysadmin** festen Sicherheitsrolle.  
  
 Ein Proxy kann identifiziert werden *Proxy_name* oder *Proxy_id*.  
  
## <a name="permissions"></a>Berechtigungen  
 Standardmäßig können nur Mitglieder der festen Serverrolle **sysadmin** diese gespeicherte Prozedur ausführen. Andere Benutzer müssen Mitglieder der festen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Datenbankrollen in der **msdb** -Datenbank sein:  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Weitere Informationen zu den Berechtigungen dieser Rollen finden Sie unter [Feste Datenbankrollen des SQL Server-Agents](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
 Der Ersteller des Auftragsschritts muss Zugriff auf den für den Auftragsschritt verwendeten Proxy haben. Mitglieder der **Sysadmin** -Serverrolle haben Zugriff auf alle Proxys. Anderen Benutzern muss der Zugriff auf einen Proxy explizit erteilt werden.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird ein Auftragsschritt erstellt, der für die Sales-Datenbank den Schreibschutz aktiviert. Zudem werden in diesem Beispiel 5 Wiederholungsversuche festgelegt, wobei jede Wiederholung nach einer Wartezeit von 5 Minuten auftritt.  
  
> [!NOTE]  
>  In diesem Beispiel wird vorausgesetzt, dass die `Weekly Sales Data Backup` Auftrag ist bereits vorhanden.  
  
```  
USE msdb;  
GO  
EXEC sp_add_jobstep  
    @job_name = N'Weekly Sales Data Backup',  
    @step_name = N'Set database to read only',  
    @subsystem = N'TSQL',  
    @command = N'ALTER DATABASE SALES SET READ_ONLY',   
    @retry_attempts = 5,  
    @retry_interval = 5 ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Anzeigen oder Ändern von Aufträgen](http://msdn.microsoft.com/library/57f649b8-190c-4304-abd7-7ca5297deab7)   
 [sp_add_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-job-transact-sql.md)   
 [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_delete_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql.md)   
 [sp_help_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_help_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql.md)   
 [sp_update_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-jobstep-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

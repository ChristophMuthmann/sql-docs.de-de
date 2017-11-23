---
title: Sp_add_jobserver (Transact-SQL) | Microsoft Docs
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
- sp_add_jobserver
- sp_add_jobserver_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_add_jobserver
ms.assetid: 485252cc-0081-490a-9bd1-cbbd68eea286
caps.latest.revision: "24"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 218df38c0ba4bb1583560f483e488c8898925496
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="spaddjobserver-transact-sql"></a>sp_add_jobserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Weist einem Auftrag einen bestimmten Zielserver zu.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_add_jobserver [ @job_id = ] job_id | [ @job_name = ] 'job_name'  
     [ , [ @server_name = ] 'server' ]   
```  
  
## <a name="arguments"></a>Argumente  
 [  **@job_id =** ] *Job_id*  
 Die ID des Auftrags. *Job_id* ist **"uniqueidentifier"**, hat den Standardwert NULL.  
  
 [  **@job_name =** ] **"***Job_name***"**  
 Der Name des Auftrags. *Job_name* ist **Sysname**, hat den Standardwert NULL.  
  
> [!NOTE]  
>  Entweder *Job_id* oder *Job_name* muss angegeben werden, aber beide können nicht angegeben werden.  
  
 [  **@server_name =** ] **"***Server***"**  
 Der Name des Servers für das Ziel des Auftrags. *Server* ist **nvarchar(30)**, hat den Standardwert ist N'(Local)' ". *Server*kann es sich um **(LOCAL)** für einen lokalen Server oder den Namen eines vorhandenen Zielservers.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="remarks"></a>Hinweise  
 **@automatic_post**vorhanden ist, **Sp_add_jobserver**, jedoch nicht unter den Argumenten aufgeführt. **@automatic_post**ist für die interne Verwendung reserviert.  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] können Aufträge problemlos mithilfe einer grafischen Oberfläche verwaltet werden. Dies ist die empfohlene Vorgehensweise für die Erstellung und Verwaltung der Auftragsinfrastruktur.  
  
## <a name="permissions"></a>Berechtigungen  
 Standardmäßig können nur Mitglieder der festen Serverrolle **sysadmin** diese gespeicherte Prozedur ausführen. Andere Benutzer müssen Mitglieder der festen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Datenbankrollen in der **msdb** -Datenbank sein:  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Weitere Informationen zu den Berechtigungen dieser Rollen finden Sie unter [Feste Datenbankrollen des SQL Server-Agents](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
 Nur Mitglieder der der **Sysadmin** -Serverrolle kann ausführen **Sp_add_jobserver** für Aufträge, die mehrere Server einbeziehen.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-assigning-a-job-to-the-local-server"></a>A. Zuweisen eines Auftrags zum lokalen Server  
 Im folgenden Beispiel wird die Ausführung des Auftrags `NightlyBackups` dem lokalen Server zugewiesen.  
  
> [!NOTE]  
>  In diesem Beispiel wird vorausgesetzt, dass die `NightlyBackups` Auftrag ist bereits vorhanden.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_jobserver  
    @job_name = N'NightlyBackups' ;  
GO  
```  
  
### <a name="b-assigning-a-job-to-run-on-a-different-server"></a>B. Zuweisen eines Auftrags zu einem anderen Server  
 Im folgenden Beispiel wird der Multiserverauftrag `Weekly Sales Backups` dem Server `SEATTLE2` zugewiesen.  
  
> [!NOTE]  
>  Bei diesem Beispiel wird vorausgesetzt, dass der Auftrag `Weekly Sales Backups` bereits vorhanden ist und dass der Server `SEATTLE2` als Zielserver für die aktuelle Instanz registriert ist.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_jobserver  
    @job_name = N'Weekly Sales Backups',  
    @server_name = N'SEATTLE2' ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_apply_job_to_targets &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-apply-job-to-targets-transact-sql.md)   
 [Sp_delete_jobserver &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

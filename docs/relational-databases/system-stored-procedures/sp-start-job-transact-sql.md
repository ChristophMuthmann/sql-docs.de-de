---
title: Sp_start_job (Transact-SQL) | Microsoft Docs
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
- sp_start_job
- sp_start_job_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_start_job
ms.assetid: 8a91df6a-eb84-4512-9a17-4a6e32a9538a
caps.latest.revision: "36"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 115e4738a6cca1b0578bf2edb86859f2e7b2a7d5
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="spstartjob-transact-sql"></a>sp_start_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Weist den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent an, einen Auftrag sofort auszuführen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_start_job   
     {   [@job_name =] 'job_name'  
       | [@job_id =] job_id }  
     [ , [@error_flag =] error_flag]  
     [ , [@server_name =] 'server_name']  
     [ , [@step_name =] 'step_name']  
     [ , [@output_flag =] output_flag]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@job_name=** ] **"***Job_name***"**  
 Der Name des Auftrags, der gestartet werden soll. Entweder *Job_id* oder *Job_name* muss angegeben werden, aber beide können nicht angegeben werden. *Job_name* ist **Sysname**, hat den Standardwert NULL.  
  
 [  **@job_id=** ] *Job_id*  
 Die ID des Auftrags, der gestartet werden soll. Entweder *Job_id* oder *Job_name* muss angegeben werden, aber beide können nicht angegeben werden. *Job_id* ist **"uniqueidentifier"**, hat den Standardwert NULL.  
  
 [  **@error_flag=** ] *Error_flag*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@server_name=** ] **"***Server_name***"**  
 Der Zielserver, auf dem der Auftrag gestartet werden soll. *Server_name* ist **vom Datentyp nvarchar(128)**, hat den Standardwert NULL. *Server_name* muss eines der Zielserver, dem der Auftrag derzeit gerichtet, sein.  
  
 [  **@step_name=** ] **"***Step_name***"**  
 Der Name des Schritts, mit dem die Ausführung des Auftrags beginnen soll. Gilt nur für lokale Aufträge. *Step_name* ist **Sysname**, hat den Standardwert NULL  
  
 [  **@output_flag=** ] *Output_flag*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="remarks"></a>Hinweise  
 Diese gespeicherte Prozedur wird in der **msdb** -Datenbank gespeichert.  
  
## <a name="permissions"></a>Berechtigungen  
 Standardmäßig können nur Mitglieder der festen Serverrolle **sysadmin** diese gespeicherte Prozedur ausführen. Andere Benutzer müssen Mitglieder der festen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Datenbankrollen in der **msdb** -Datenbank sein:  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Weitere Informationen zu den Berechtigungen dieser Rollen finden Sie unter [Feste Datenbankrollen des SQL Server-Agents](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
 Mitglieder der **SQLAgentUserRole** und **SQLAgentReaderRole** können nur Aufträge, deren Besitzer sie, starten. Mitglieder der **SQLAgentOperatorRole** können alle lokalen Aufträge einschließlich derjenigen, die von anderen Benutzern gehören starten. Mitglieder der **Sysadmin** können Aufträge für alle lokalen und Multiserveraufträge starten.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird ein Auftrag mit dem Namen `Weekly Sales Data Backup` gestartet.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_start_job N'Weekly Sales Data Backup' ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_delete_job &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [Sp_help_job &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [Sp_stop_job &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-stop-job-transact-sql.md)   
 [Sp_update_job &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

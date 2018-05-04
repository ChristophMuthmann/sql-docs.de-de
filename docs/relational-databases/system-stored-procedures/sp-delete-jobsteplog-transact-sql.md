---
title: Sp_delete_jobsteplog (Transact-SQL) | Microsoft Docs
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
- sp_delete_jobsteplog
- sp_delete_jobsteplog_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_jobsteplog
ms.assetid: e9ef4c99-abde-4038-b6a3-a25dcbaf0958
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 99f60818976dc3c89e11d2fd1256a7aecd7d8b63
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spdeletejobsteplog-transact-sql"></a>sp_delete_jobsteplog (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Entfernt alle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent-Auftragsschrittprotokolle, die mit den Argumenten angegeben sind. Verwenden Sie diese gespeicherte Prozedur zum Verwalten der **Sysjobstepslogs** -Tabelle in der **Msdb** Datenbank.  
  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_delete_jobsteplog { [ @job_id = ] 'job_id' | [ @job_name = ] 'job_name' }  
       [ , [ @step_id = ] step_id | [ @step_name = ] 'step_name' ]  
       [ , [ @older_than = ] 'date' ]  
       [ , [ @larger_than = ] 'size_in_bytes' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@job_id =**] **'***job_id***'**  
 Die ID des Auftrags, der das zu entfernende Auftragsschrittprotokoll enthält. *Job_id* ist **Int**, hat den Standardwert NULL.  
  
 [ **@job_name =**] **'***job_name***'**  
 Der Name des Auftrags. *Job_name* ist **Sysname**, hat den Standardwert NULL.  
  
> **Hinweis:** entweder *Job_id* oder *Job_name* muss angegeben werden, aber beide können nicht angegeben werden.  
  
 [ **@step_id =**] *step_id*  
 Die ID des Schritts im Auftrag, für den das Auftragsschrittprotokoll gelöscht werden soll. Wenn nicht angegeben ist, werden alle Auftragsschrittprotokolle im Auftrag gelöscht, es sei denn, **@older_than** oder **@larger_than** angegeben werden. *Step_id* ist **Int**, hat den Standardwert NULL.  
  
 [ **@step_name =**] **'***step_name***'**  
 Der Name des Schritts im Auftrag, für den das Auftragsschrittprotokoll gelöscht werden soll. *Step_name* ist **Sysname**, hat den Standardwert NULL.  
  
> **Hinweis:** entweder *Step_id* oder *Step_name* kann angegeben werden, aber beide können nicht angegeben werden.  
  
 [ **@older_than =**] **'***date***'**  
 Das Datum und die Uhrzeit des ältesten Auftragsschrittprotokolls, das beibehalten werden soll. Alle Auftragsschrittprotokolle vor diesem Datum und dieser Uhrzeit werden entfernt. *Datum* ist **"DateTime"**, hat den Standardwert NULL. Beide **@older_than** und **@larger_than** kann angegeben werden.  
  
 [ **@larger_than =**] **'***size_in_bytes***'**  
 Die maximale Größe in Byte für das Auftragsschrittprotokoll, das beibehalten werden soll. Alle Auftragsschrittprotokolle, die diese Größe überschreiten, werden entfernt. Beide **@larger_than** und **@older_than** kann angegeben werden.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="remarks"></a>Hinweise  
 **Sp_delete_jobsteplog** befindet sich in der **Msdb** Datenbank.  
  
 Wenn keine Argumente, außer **@job_id** oder **@job_name** angegeben ist, werden alle Auftragsschrittprotokolle für den angegebenen Auftrag gelöscht.  
  
## <a name="permissions"></a>Berechtigungen  
 Standardmäßig können nur Mitglieder der festen Serverrolle **sysadmin** diese gespeicherte Prozedur ausführen. Andere Benutzer müssen Mitglieder der festen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Datenbankrollen in der **msdb** -Datenbank sein:  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Weitere Informationen zu den Berechtigungen dieser Rollen finden Sie unter [Feste Datenbankrollen des SQL Server-Agents](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
 Nur Mitglieder der **Sysadmin** können löschen ein auftragsschrittprotokolls, das von einem anderen Benutzer gehört.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-removing-all-job-step-logs-from-a-job"></a>A. Entfernen aller Auftragsschrittprotokolle aus einem Auftrag  
 Im folgenden Beispiel werden alle Auftragsschrittprotokolle für den `Weekly Sales Data Backup`-Auftrag entfernt.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_jobsteplog  
    @job_name = N'Weekly Sales Data Backup';  
GO  
```  
  
### <a name="b-removing-the-job-step-log-for-a-particular-job-step"></a>B. Entfernen des Auftragsschrittprotokolls für einen bestimmten Auftragsschritt  
 Im folgenden Beispiel wird das Auftragsschrittprotokoll für Schritt 2 im `Weekly Sales Data Backup`-Auftrag entfernt.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_jobsteplog  
    @job_name = N'Weekly Sales Data Backup',  
    @step_id = 2;  
GO  
```  
  
### <a name="c-removing-all-job-step-logs-based-on-age-and-size"></a>C. Entfernen aller Auftragsschrittprotokolle auf Grundlage von Alter und Größe  
 Im folgenden Beispiel werden alle Auftragsschrittprotokolle aus dem `Weekly Sales Data Backup`-Auftrag entfernt, die älter sind als 12 Uhr mittags, 25. Oktober 2005, und die größer sind als 100 MB (Megabyte).  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_jobsteplog  
    @job_name = N'Weekly Sales Data Backup',  
    @older_than = '10/25/2005 12:00:00',  
    @larger_than = 104857600;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sp_help_jobsteplog &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-jobsteplog-transact-sql.md)   
 [SQL Server-Agent-Prozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)  
  
  

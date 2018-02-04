---
title: Sp_attach_schedule (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_attach_schedule_TSQL
- sp_attach_schedule
dev_langs:
- TSQL
helpviewer_keywords:
- sp_attach_schedule
ms.assetid: 80c80eaf-cf23-4ed8-b8dd-65fe59830dd1
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d78d6c73d28325771460a1c055a6fb0b491c264c
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="spattachschedule-transact-sql"></a>sp_attach_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Legt einen Zeitplan für einen Auftrag fest.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_attach_schedule  
     { [ @job_id = ] job_id | [ @job_name = ] 'job_name' } ,   
     { [ @schedule_id = ] schedule_id   
     | [ @schedule_name = ] 'schedule_name' }  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@job_id=** ] *job_id*  
 Die Auftrags-ID des Auftrags, zu dem der Zeitplan hinzugefügt wird. *Job_id*ist **"uniqueidentifier"**, hat den Standardwert NULL.  
  
 [ **@job_name =** ] **'***job_name***'**  
 Der Name des Auftrags, zu dem der Zeitplan hinzugefügt wird. *Job_name*ist **Sysname**, hat den Standardwert NULL.  
  
> [!NOTE]  
>  Entweder *Job_id* oder *Job_name* muss angegeben werden, aber beide können nicht angegeben werden.  
  
 [ **@schedule_id =** ] *schedule_id*  
 Die Zeitplan-ID des für den Auftrag festgelegten Zeitplans. *Schedule_id*ist **Int**, hat den Standardwert NULL.  
  
 [ **@schedule_name =** ] **'***schedule_name***'**  
 Der Name des für den Auftrag festzulegenden Zeitplans. *Schedule_name*ist **Sysname**, hat den Standardwert NULL.  
  
> [!NOTE]  
>  Entweder *Schedule_id* oder *Schedule_name* muss angegeben werden, aber beide können nicht angegeben werden.  
  
## <a name="remarks"></a>Hinweise  
 Der Zeitplan und der Auftrag müssen denselben Besitzer aufweisen.  
  
 Ein Zeitplan kann für mehrere Aufträge festgelegt werden. Ein Auftrag kann auf der Basis mehrerer Zeitpläne ausgeführt werden.  
  
 Diese gespeicherte Prozedur muss von der **msdb** -Datenbank aus ausgeführt werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Standardmäßig können nur Mitglieder der festen Serverrolle **sysadmin** diese gespeicherte Prozedur ausführen. Andere Benutzer müssen Mitglieder der festen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Datenbankrollen in der **msdb** -Datenbank sein:  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Hinweis: Der Auftragsbesitzer kann einem Zeitplan einen Auftrag anfügen oder diesen von ihm trennen, und zwar ohne der Zeitplanbesitzer sein zu müssen. Allerdings kann kein Zeitplan gelöscht werden, wenn das Trennen keine Aufträge lassen würde, wenn der Aufrufer der Zeitplanbesitzer ist.  
  
 Weitere Informationen zu den Berechtigungen dieser Rollen finden Sie unter [Feste Datenbankrollen des SQL Server-Agents](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] überprüft, ob der Benutzer den Auftrag und den Zeitplan besitzt.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird ein Zeitplan mit dem Namen `NightlyJobs` erstellt. Aufträge, die diesen Zeitplan verwenden, werden jeden Tag zur Serveruhrzeit `01:00` Uhr ausgeführt. Im Beispiel wird der Zeitplan den Aufträgen `BackupDatabase` und `RunReports` angefügt.  
  
> [!NOTE]  
>  Bei diesem Beispiel wird davon ausgegangen, dass die Aufträge `BackupDatabase` und `RunReports` bereits vorhanden sind.  
  
```  
USE msdb ;  
GO  
  
EXEC sp_add_schedule  
    @schedule_name = N'NightlyJobs' ,  
    @freq_type = 4,  
    @freq_interval = 1,  
    @active_start_time = 010000 ;  
GO  
  
EXEC sp_attach_schedule  
   @job_name = N'BackupDatabase',  
   @schedule_name = N'NightlyJobs' ;  
GO  
  
EXEC sp_attach_schedule  
   @job_name = N'RunReports',  
   @schedule_name = N'NightlyJobs' ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_detach_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-detach-schedule-transact-sql.md)   
 [sp_delete_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)  
  
  

---
title: Sp_detach_schedule (Transact-SQL) | Microsoft Docs
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
- sp_detach_schedule
- sp_detach_schedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_detach_schedule
ms.assetid: 9a1fc335-1bef-4638-a33a-771c54a5dd19
caps.latest.revision: 34
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 82fd73eb4b5959659f57216dbba9d12c90cf3354
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spdetachschedule-transact-sql"></a>sp_detach_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Entfernt eine Zuordnung zwischen einem Zeitplan und einem Auftrag.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_detach_schedule   
     { [ @job_id = ] job_id | [ @job_name = ] 'job_name' } ,  
       { [ @schedule_id = ] schedule_id | [ @schedule_name = ] 'schedule_name' } ,  
     [ @delete_unused_schedule = ] delete_unused_schedule   
```  
  
## <a name="arguments"></a>Argumente  
 [ **@job_id=** ] *job_id*  
 Die ID des Auftrags, aus dem der Zeitplan entfernt werden soll. *Job_id* ist **"uniqueidentifier"**, hat den Standardwert NULL.  
  
 [  **@job_name=** ] **"***Job_name***"**  
 Der Name des Auftrags, aus dem der Zeitplan entfernt werden soll. *Job_name* ist **Sysname**, hat den Standardwert NULL.  
  
> [!NOTE]  
>  Entweder *Job_id* oder *Job_name* muss angegeben werden, aber beide können nicht angegeben werden.  
  
 [  **@schedule_id=** ] *Schedule_id*  
 Die ID des Zeitplans, der aus dem Auftrag entfernt werden soll. *Schedule_id* ist **Int**, hat den Standardwert NULL.  
  
 [  **@schedule_name=** ] **"***Schedule_name***"**  
 Der Name des Zeitplans, der aus dem Auftrag entfernt werden soll. *Schedule_name* ist **Sysname**, hat den Standardwert NULL.  
  
> [!NOTE]  
>  Entweder *Schedule_id* oder *Schedule_name* muss angegeben werden, aber beide können nicht angegeben werden.  
  
 [  **@delete_unused_schedule=** ] *Delete_unused_schedule*  
 Gibt an, ob nicht verwendete Auftragszeitpläne gelöscht werden sollen. *Delete_unused_schedule* ist **Bit**, hat den Standardwert **0**, was bedeutet, dass alle Zeitpläne beibehalten werden, auch wenn keine Aufträge auf sie verweist. Wenn auf festgelegt **1**, werden nicht verwendete Auftragszeitpläne gelöscht, wenn keine Aufträge auf sie verweist.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="permissions"></a>Berechtigungen  
 Standardmäßig können nur Mitglieder der festen Serverrolle **sysadmin** diese gespeicherte Prozedur ausführen. Andere Benutzer müssen Mitglieder der festen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Datenbankrollen in der **msdb** -Datenbank sein:  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Hinweis: Der Auftragsbesitzer kann einem Zeitplan einen Auftrag anfügen oder diesen von ihm trennen, und zwar ohne der Zeitplanbesitzer sein zu müssen. Ein Zeitplan kann jedoch nicht gelöscht werden, wenn durch das Trennen keine Aufträge mehr vorhanden wären, außer der Aufrufer ist der Zeitplanbesitzer.  
  
 Weitere Informationen zu den Berechtigungen dieser Rollen finden Sie unter [Feste Datenbankrollen des SQL Server-Agents](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] überprüft, ob der Benutzer der Besitzer des Zeitplans ist. Nur Mitglieder der **Sysadmin** -Serverrolle kann Zeitpläne von Aufträgen, die im Besitz eines anderen Benutzers trennen.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine Zuordnung zwischen einem `'NightlyJobs'`-Zeitplan und einem `'BackupDatabase'`-Auftrag entfernt.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_detach_schedule  
    @job_name = 'BackupDatabase',  
    @schedule_name = 'NightlyJobs' ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_attach_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)   
 [sp_delete_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)  
  
  

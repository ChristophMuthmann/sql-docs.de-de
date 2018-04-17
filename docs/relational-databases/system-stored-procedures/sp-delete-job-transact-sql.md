---
title: Sp_delete_job (Transact-SQL) | Microsoft Docs
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
- sp_delete_job
- sp_delete_job_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_job
ms.assetid: b85db6e4-623c-41f1-9643-07e5ea38db09
caps.latest.revision: 43
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c578243ec78605216a3cb5c640e6779e712fec46
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="spdeletejob-transact-sql"></a>sp_delete_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Löscht einen Auftrag.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_delete_job { [ @job_id = ] job_id | [ @job_name = ] 'job_name' } ,  
     [ , [ @originating_server = ] 'server' ]   
     [ , [ @delete_history = ] delete_history ]  
     [ , [ @delete_unused_schedule = ] delete_unused_schedule ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@job_id=** ] *job_id*  
 Die ID des Auftrags, der gelöscht werden soll. *Job_id* ist **"uniqueidentifier"**, hat den Standardwert NULL.  
  
 [  **@job_name=** ] **"***Job_name***"**  
 Der Name des Auftrags, der gelöscht werden soll. *Job_name* ist **Sysname**, hat den Standardwert NULL.  
  
> [!NOTE]  
>  Entweder *Job_id* oder *Job_name*muss angegeben werden, beide können nicht angegeben werden.  
  
 [  **@originating_server=** ] **"***Server***"**  
 Für die interne Verwendung.  
  
 [ **@delete_history=** ] *delete_history*  
 Gibt an, ob der Verlauf für den Auftrag gelöscht werden soll. *Delete_history* ist **Bit**, hat den Standardwert **1**. Wenn *Delete_history* ist **1**, wird der Auftragsverlauf für den Auftrag gelöscht. Wenn *Delete_history* ist **0**, wird der Auftragsverlauf nicht gelöscht.  
  
 Beachten Sie, dass wenn ein Auftrag wird gelöscht, und der Verlauf wird nicht gelöscht, die Verlaufsinformationen für den Auftrag nicht in angezeigt werden die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] grafische Schnittstelle im Auftragsverlauf-Agents, aber die Informationen noch befindet sich in der **Sysjobhistory**-Tabelle in der **Msdb** Datenbank.  
  
 [  **@delete_unused_schedule=** ] *Delete_unused_schedule*  
 Gibt an, ob die an diesen Auftrag angefügten Zeitpläne gelöscht werden sollen, falls sie nicht an einen anderen Auftrag angefügt sind. *Delete_unused_schedule* ist **Bit**, hat den Standardwert **1**. Wenn *Delete_unused_schedule* ist **1**, diesen Auftrag angefügten Zeitpläne werden gelöscht, wenn keine anderen Aufträge mit Verweisen auf den Zeitplan. Wenn *Delete_unused_schedule* ist **0**, die Zeitpläne werden nicht gelöscht.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="remarks"></a>Hinweise  
 Die **@originating_server** Argument ist für die interne Verwendung reserviert.  
  
 Die **@delete_unused_schedule** Argument bietet Abwärtskompatibilität mit früheren Versionen von SQL Server, indem Sie Zeitpläne, die nicht an einen beliebigen Auftrag angefügt sind, automatisch entfernt werden. Beachten Sie, dass dieser Parameter standardmäßig das Verhalten der Abwärtskompatibilität bietet. Zum Beibehalten der Zeitpläne, die nicht mit einem Auftrag angefügt sind, geben Sie den Wert **0** als die **@delete_unused_schedule** Argument.  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] können Aufträge problemlos mithilfe einer grafischen Oberfläche verwaltet werden. Dies ist die empfohlene Vorgehensweise für die Erstellung und Verwaltung der Auftragsinfrastruktur.  
  
 Mit dieser gespeicherten Prozedur können keine Wartungspläne oder Aufträge, die Teil von Wartungsplänen sind, gelöscht werden. Zum Löschen von Wartungsplänen müssen Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] verwenden.  
  
## <a name="permissions"></a>Berechtigungen  
 Standardmäßig können nur Mitglieder der festen Serverrolle **sysadmin** diese gespeicherte Prozedur ausführen. Andere Benutzer müssen Mitglieder der festen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Datenbankrollen in der **msdb** -Datenbank sein:  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Weitere Informationen zu den Berechtigungen dieser Rollen finden Sie unter [Feste Datenbankrollen des SQL Server-Agents](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
 Nur Mitglieder der festen Serverrolle **sysadmin** können **sp_delete_job** ausführen, um einen beliebigen Auftrag zu löschen. Ein Benutzer, der kein Mitglied der festen Serverrolle **sysadmin** ist, kann nur Aufträge löschen, deren Besitzer er ist.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird der Auftrag `NightlyBackups` gelöscht.  
  
```  
USE msdb ;  
GO  
  
EXEC sp_delete_job  
    @job_name = N'NightlyBackups' ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sp_add_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-job-transact-sql.md)   
 [sp_help_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_update_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

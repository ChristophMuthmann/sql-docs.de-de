---
title: Sp_apply_job_to_targets (Transact-SQL) | Microsoft Docs
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
- sp_apply_job_to_targets
- sp_apply_job_to_targets_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_apply_job_to_targets
ms.assetid: 4a3e9173-7e3c-4100-a9ac-2f5d2c60a8b0
caps.latest.revision: "34"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4f0c7c788370e25f3fe7000bc4481005f4224dda
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="spapplyjobtotargets-transact-sql"></a>sp_apply_job_to_targets (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Wendet einen Auftrag auf einen oder mehrere Zielserver oder auf die Zielserver an, die einer oder mehreren Zielservergruppen angehören.  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_apply_job_to_targets { [ @job_id = ] job_id | [ @job_name = ] 'job_name' }  
     [ , [ @target_server_groups = ] 'target_server_groups' ]   
     [ , [ @target_servers = ] 'target_servers' ]   
     [ , [ @operation = ] 'operation' ]   
```  
  
## <a name="arguments"></a>Argumente  
 [  **@job_id =**] *Job_id*  
 Die ID des Auftrags, der für die angegebenen Zielserver oder Zielservergruppen ausgeführt werden sollen. *Job_id* ist **"uniqueidentifier"**, hat den Standardwert NULL.  
  
 [  **@job_name =**] **"***Job_name***"**  
 Der Name des Auftrags, der für die angegebenen Zielserver oder Zielservergruppen ausgeführt werden sollen. *Job_name* ist **Sysname**, hat den Standardwert NULL.  
  
> [!NOTE]  
>  Entweder *Job_id* oder *Job_name* muss angegeben werden, aber beide können nicht angegeben werden.  
  
 [  **@target_server_groups =**] **"***Target_server_groups***"**  
 Eine durch Trennzeichen getrennte Liste von Zielservergruppen, für die der angegebene Auftrag ausgeführt werden soll. *Target_server_groups* ist **nvarchar(2048)**, hat den Standardwert NULL.  
  
 [  **@target_servers=** ] **"***target_server***"**  
 Eine durch Trennzeichen getrennte Liste von Zielservern, für die der angegebene Auftrag ausgeführt werden soll. *target_server*ist **nvarchar(2048)**, hat den Standardwert NULL.  
  
 [  **@operation=** ] **"***Vorgang***"**  
 Gibt an, ob der angegebene Auftrag für die genannten Zielserver oder Zielservergruppen ausgeführt oder davon entfernt werden soll. *Vorgang*ist **vom Datentyp varchar(7)**, hat den Standardwert übernehmen. Gültige Vorgänge sind **übernehmen** und **entfernen**.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_apply_job_to_targets** bietet eine einfache Möglichkeit anzuwenden (oder entfernen) ein Auftrags von mehrere Zielserver aus, und ist eine Alternative zum Aufruf **Sp_add_jobserver** (oder **Sp_delete_jobserver** ) einmal für jeden erforderlichen Zielserver.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der **Sysadmin** -Serverrolle kann diese Prozedur ausführen.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird der zuvor erstellte Auftrag `Backup Customer Information` auf alle Zielserver in der Gruppe `Servers Maintaining Customer Information` angewendet.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_apply_job_to_targets  
    @job_name = N'Backup Customer Information',  
    @target_server_groups = N'Servers Maintaining Customer Information',   
    @operation = N'APPLY' ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_add_jobserver &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md)   
 [Sp_delete_jobserver &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)   
 [Sp_remove_job_from_targets &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-remove-job-from-targets-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

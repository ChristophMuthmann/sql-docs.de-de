---
title: Sp_remove_job_from_targets (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
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
- sp_remove_job_from_targets_TSQL
- sp_remove_job_from_targets
dev_langs:
- TSQL
helpviewer_keywords:
- sp_remove_job_from_targets
ms.assetid: b8171fb1-c11d-4244-8618-a12e28a150ce
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4449e4879254f183329f6df0040687ca69981669
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spremovejobfromtargets-transact-sql"></a>sp_remove_job_from_targets (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Entfernt den angegebenen Auftrag auf den jeweiligen Zielservern oder Zielservergruppen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_remove_job_from_targets [ @job_id = ] job_id   
     | [ @job_name = ] 'job_name'   
     [ , [ @target_server_groups = ] 'target_server_groups' ]   
     [ , [ @target_servers = ] 'target_servers' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@job_id =**] *job_id*  
 Die Auftrags-ID des Auftrags, aus dem die angegebenen Zielserver oder Zielservergruppen entfernt werden sollen. Entweder *Job_id* oder *Job_name* muss angegeben werden, aber beide können nicht angegeben werden. *Job_id* ist **"uniqueidentifier"**, hat den Standardwert NULL.  
  
 [ **@job_name =**] **'***job_name***'**  
 Der Name des Auftrags, aus dem die angegebenen Zielserver oder Zielservergruppen entfernt werden sollen. Entweder *Job_id* oder *Job_name* muss angegeben werden, aber beide können nicht angegeben werden. *Job_name* ist **Sysname**, hat den Standardwert NULL.  
  
 [ **@target_server_groups =**] **'***target_server_groups***'**  
 Eine durch Trennzeichen getrennte Liste der Zielservergruppen, die aus dem angegebenen Auftrag entfernt werden sollen. *Target_server_groups* ist **nvarchar(1024)**, hat den Standardwert NULL.  
  
 [ **@target_servers =**] **'***target_servers***'**  
 Eine durch Trennzeichen getrennte Liste der Zielserver, die aus dem angegebenen Auftrag entfernt werden sollen. *target_server* ist **nvarchar(1024)**, hat den Standardwert NULL.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="permissions"></a>Berechtigungen  
 Standardmäßig verfügen Mitglieder der festen Serverrolle **sysadmin** über die Berechtigungen zum Ausführen dieser Prozedur.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird der zuvor erstellte Auftrag `Weekly Sales Backups` aus der Zielservergruppe `Servers Processing Customer Orders` und von den Servern `SEATTLE1` und `SEATTLE2` entfernt.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_remove_job_from_targets  
    @job_name = N'Weekly Sales Backups',  
    @target_server_groups = N'Servers Processing Customer Orders',   
    @target_servers = N'SEATTLE2,SEATTLE1' ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sp_apply_job_to_targets &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-apply-job-to-targets-transact-sql.md)   
 [sp_delete_jobserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

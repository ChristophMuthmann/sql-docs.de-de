---
title: Sp_delete_jobstep (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2016
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
- sp_delete_jobstep
- sp_delete_jobstep_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_delete_jobstep
ms.assetid: 421ede8e-ad57-474a-9fb9-92f70a3e77e3
caps.latest.revision: "35"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9134c1f50a3ce1e9aaee8456db4f076193271ca9
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="spdeletejobstep-transact-sql"></a>sp_delete_jobstep (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Entfernt einen Auftragsschritt aus einem Auftrag.  
  
 
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_delete_jobstep { [ @job_id = ] job_id | [ @job_name = ] 'job_name' } ,   
     [ @step_id = ] step_id   
```  
  
## <a name="arguments"></a>Argumente  
 [  **@job_id=** ] *Job_id*  
 Der ID des Auftrags, aus dem der Schritt entfernt wird. *Job_id*ist **"uniqueidentifier"**, hat den Standardwert NULL.  
  
 [  **@job_name=** ] **"***Job_name***"**  
 Der Name des Auftrags, aus dem der Schritt entfernt wird. *Job_name*ist **Sysname**, hat den Standardwert NULL.  
  
> **Hinweis:** entweder *Job_id* oder *Job_name* muss angegeben werden, beide können nicht angegeben werden.  
  
 [  **@step_id=** ] *Step_id*  
 Die ID des Schritts, der entfernt wird. *Step_id*ist **Int**, hat keinen Standardwert.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="remarks"></a>Hinweise  
 Durch das Entfernen eines Auftragsschritts werden die anderen Auftragsschritte, die auf den gelöschten Schritt verweisen, automatisch aktualisiert.  
  
 Führen Sie für Weitere Informationen zu den Schritten, die mit einem bestimmten Auftrag verknüpften **Sp_help_jobstep**.  
  
> **Hinweis:** Aufrufen **Sp_delete_jobstep** mit einem *Step_id* Wert von NULL werden alle Auftragsschritte für den Auftrag gelöscht.  
  
 Mit Microsoft SQL Server Management Studio lassen sich Aufträge auf einfache Weise über eine grafische Oberfläche verwalten. Dies ist die empfohlene Vorgehensweise, um die Auftragsinfrastruktur zu erstellen und zu verwalten.  
  
## <a name="permissions"></a>Berechtigungen  
 Standardmäßig können nur Mitglieder der festen Serverrolle **sysadmin** diese gespeicherte Prozedur ausführen. Andere Benutzer müssen Mitglieder der festen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Datenbankrollen in der **msdb** -Datenbank sein:  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Weitere Informationen zu den Berechtigungen dieser Rollen finden Sie unter [Feste Datenbankrollen des SQL Server-Agents](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
 Nur Mitglieder der **Sysadmin** können löschen ein Auftragsschritts ausgeführt, die von einem anderen Benutzer gehört.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird Auftragsschritt `1` aus dem Auftrag `Weekly Sales Data Backup` entfernt.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_jobstep  
    @job_name = N'Weekly Sales Data Backup',  
    @step_id = 1 ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Anzeigen oder Ändern von Aufträgen](http://msdn.microsoft.com/library/57f649b8-190c-4304-abd7-7ca5297deab7)   
 [Sp_add_jobstep &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)   
 [Sp_update_jobstep &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-update-jobstep-transact-sql.md)   
 [Sp_help_jobstep &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

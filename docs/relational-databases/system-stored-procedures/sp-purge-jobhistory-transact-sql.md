---
title: Sp_purge_jobhistory (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_purge_jobhistory_TSQL
- sp_purge_jobhistory
dev_langs:
- TSQL
helpviewer_keywords:
- sp_purge_jobhistory
ms.assetid: 237f9bad-636d-4262-9bfb-66c034a43e88
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 7f50228e089d71a6cf3a8d74225e1e26f42844fd
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="sppurgejobhistory-transact-sql"></a>sp_purge_jobhistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Entfernt die Verlaufsdatensätze für einen Auftrag.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_purge_jobhistory   
   {   [ @job_name = ] 'job_name' |   
     | [ @job_id = ] job_id }  
   [ , [ @oldest_date = ] oldest_date ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@job_name=** ] **'***job_name***'**  
 Der Name des Auftrags, für den die Verlaufsdatensätze gelöscht werden sollen. *Job_name*ist **Sysname**, hat den Standardwert NULL. Entweder *Job_id* oder *Job_name* muss angegeben werden, aber beide können nicht angegeben werden.  
  
> [!NOTE]  
>  Mitglieder der **Sysadmin** -Serverrolle oder Mitglieder der der **SQLAgentOperatorRole** feste Datenbankrolle können ausführen **Sp_purge_jobhistory** ohne Angabe einer *Job_name* oder *Job_id*. Wenn **Sysadmin** -Benutzer diese Argumente nicht angeben, wird der Auftragsverlauf für alle lokalen und Multiserveraufträge innerhalb der angegebenen Zeit gelöscht *Oldest_date*. Wenn **SQLAgentOperatorRole** -Benutzer diese Argumente nicht angeben, wird der Auftragsverlauf für alle lokalen Aufträge innerhalb der angegebenen Zeit gelöscht *Oldest_date*.  
  
 [ **@job_id=** ] *job_id*  
 Die ID des Auftrags für die zu löschenden Datensätze. *Job_id*ist **"uniqueidentifier"**, hat den Standardwert NULL. Entweder *Job_id* oder *Job_name* muss angegeben werden, aber beide können nicht angegeben werden. Siehe den Hinweis in der Beschreibung der  **@job_name**  Informationen **Sysadmin** oder **SQLAgentOperatorRole** Benutzer dieses Argument verwenden können.  
  
 [ **@oldest_date** = ] *oldest_date*  
 Der älteste Datensatz, der im Verlauf beibehalten werden soll. *Oldest_date* ist **"DateTime"**, hat den Standardwert NULL. Wenn *Oldest_date* angegeben wird, **Sp_purge_jobhistory** entfernt nur Datensätze, die älter sind als der angegebene Wert ist.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="remarks"></a>Hinweise  
 Wenn **Sp_purge_jobhistory** wird erfolgreich abgeschlossen, eine Nachricht zurückgegeben.  
  
## <a name="permissions"></a>Berechtigungen  
 Standardmäßig sind nur Mitglieder der der **Sysadmin** festen Serverrolle oder die **SQLAgentOperatorRole** festen Datenbankrolle kann diese gespeicherte Prozedur ausführen. Mitglieder der **Sysadmin** können den Auftragsverlauf für alle lokalen und Multiserveraufträge leeren. Mitglieder der **SQLAgentOperatorRole** können den Auftragsverlauf für alle lokalen Aufträge nur löschen.  
  
 Anderen Benutzern, einschließlich Elementen der **SQLAgentUserRole** und Mitglieder der **SQLAgentReaderRole**, muss explizit gewährt werden die EXECUTE-Berechtigung auf **Sp_purge_jobhistory**. Nachdem die EXECUTE-Berechtigung für diese gespeicherte Prozedur erteilt wurde, können dieses Benutzer nur den Verlauf für Aufträge leeren, deren Besitzer sie sind.  
  
 Die **SQLAgentUserRole**, **SQLAgentReaderRole**, und **SQLAgentOperatorRole** feste Datenbankrollen sind der **Msdb** Datenbank. Einzelheiten zu deren Berechtigungen finden Sie unter [SQL Server Agent Fixed Database Roles](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-remove-history-for-a-specific-job"></a>A. Entfernen des Verlaufs für einen bestimmten Auftrag  
 Im folgenden Beispiel wird der Verlauf eines Auftrags mit dem Namen `NightlyBackups` entfernt.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_purge_jobhistory  
    @job_name = N'NightlyBackups' ;  
GO  
```  
  
### <a name="b-remove-history-for-all-jobs"></a>B. Entfernen des Verlaufs für alle Aufträge  
  
> [!NOTE]  
>  Nur Mitglieder der der **Sysadmin** -Serverrolle und Mitglieder der festen der **SQLAgentOperatorRole** Verlaufsprotokolle für alle Aufträge entfernen können. Wenn **Sysadmin** -Benutzer diese gespeicherte Prozedur ohne Parameter ausführen, wird der Auftragsverlauf für alle lokalen und Multiserveraufträge geleert. Wenn **SQLAgentOperatorRole** -Benutzer diese gespeicherte Prozedur ohne Parameter ausführen, wird nur der Auftragsverlauf für alle lokalen Aufträge geleert.  
  
 Im folgenden Beispiel wird die Prozedur ohne Parameter ausgeführt, um alle Verlaufsdatensätze zu entfernen.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_purge_jobhistory ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sp_help_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_help_jobhistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-jobhistory-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Erteilen von Objektberechtigungen &#40; Transact-SQL &#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)  
  
  

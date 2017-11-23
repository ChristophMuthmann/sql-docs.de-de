---
title: Sp_help_jobsteplog (Transact-SQL) | Microsoft Docs
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
- sp_help_jobsteplog_TSQL
- sp_help_jobsteplog
dev_langs: TSQL
helpviewer_keywords: sp_help_jobsteplog
ms.assetid: 1a0be7b1-8f31-4b4c-aadb-586c0e00ed04
caps.latest.revision: "18"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2c6c6e778a416f6e8e5d615a435a2be6c1e6a097
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sphelpjobsteplog-transact-sql"></a>sp_help_jobsteplog (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt Metadaten zu einem bestimmten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auftragsschrittprotokoll-Agents. **Sp_help_jobsteplog** gibt nicht das eigentliche Protokoll zurück.  

  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_help_jobsteplog { [ @job_id = ] 'job_id' | [ @job_name = ] 'job_name' }  
     [ , [ @step_id = ] step_id ]  
     [ , [ @step_name = ] 'step_name' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@job_id =**] **"***Job_id***"**  
 Die ID des Auftrags, zu dem Auftragsschritt-Protokollinformationen zurückgegeben werden sollen. *Job_id* ist **Int**, hat den Standardwert NULL.  
  
 [  **@job_name =**] **"***Job_name***"**  
 Der Name des Auftrags. *Job_name* ist **Sysname**, hat den Standardwert NULL.  
  
> [!NOTE]  
>  Entweder *Job_id* oder *Job_name* muss angegeben werden, aber beide können nicht angegeben werden.  
  
 [  **@step_id =**] *Step_id*  
 Die ID des Auftragsschritts. Wenn diese nicht angegeben wird, sind alle Schritte im Auftrag eingeschlossen. *Step_id* ist **Int**, hat den Standardwert NULL.  
  
 [  **@step_name =**] **"***Step_name***"**  
 Der Name des Schritts im Auftrag. *Step_name* ist **Sysname**, hat den Standardwert NULL.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**job_id**|**uniqueidentifier**|Eindeutiger Bezeichner des Auftrags.|  
|**job_name**|**sysname**|Name des Auftrags.|  
|**step_id**|**int**|Bezeichner des Schritts innerhalb des Auftrags. Angenommen, wenn der Schritt im Auftrag, der erste Schritt ist die *Step_id* ist 1.|  
|**step_name**|**sysname**|Name des Auftragsschritts.|  
|**step_uid**|**uniqueidentifier**|Eindeutiger Bezeichner des Schritts (systemgeneriert) im Auftrag.|  
|**date_created**|**datetime**|Datum, an dem der Schritt erstellt wurde.|  
|**DATE_MODIFIED**|**datetime**|Datum, an dem der Schritt zuletzt geändert wurde.|  
|**log_size**|**float**|Größe des Auftragsschrittprotokolls in MB.|  
|**Protokoll**|**nvarchar(max)**|Ausgabe des Auftragsschrittprotokolls.|  
  
## <a name="remarks"></a>Hinweise  
 **Sp_help_jobsteplog** befindet sich in der **Msdb** Datenbank.  
  
## <a name="permissions"></a>Berechtigungen  
 Standardmäßig können nur Mitglieder der festen Serverrolle **sysadmin** diese gespeicherte Prozedur ausführen. Andere Benutzer müssen Mitglieder der festen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Datenbankrollen in der **msdb** -Datenbank sein:  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Weitere Informationen zu den Berechtigungen dieser Rollen finden Sie unter [Feste Datenbankrollen des SQL Server-Agents](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
 Mitglieder der **SQLAgentUserRole** können die Metadaten des auftragsschrittprotokolls für Auftragsschritte, die sie besitzen nur anzeigen.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-returns-job-step-log-information-for-all-steps-in-a-specific-job"></a>A. Gibt Auftragsschritt-Protokollinformationen für alle Schritte in einem bestimmten Auftrag zurück  
 Im folgenden Beispiel werden alle Auftragsschrittinformationen für den Auftrag namens `Weekly Sales Data Backup` zurückgegeben.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobsteplog  
    @job_name = N'Weekly Sales Data Backup' ;  
GO  
```  
  
### <a name="b-return-job-step-log-information-about-a-specific-job-step"></a>B. Zurückgeben von Auftragsschritt-Protokollinformationen zu einem bestimmten Auftragsschritt  
 Im folgenden Beispiel werden Auftragsschrittinformationen zum ersten Auftragsschritt des Auftrags namens `Weekly Sales Data Backup` zurückgegeben.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobsteplog  
    @job_name = N'Weekly Sales Data Backup',  
    @step_id = 1 ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_add_jobstep &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)   
 [Sp_delete_jobstep &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql.md)   
 [Sp_help_jobstep &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql.md)   
 [Sp_delete_jobstep &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql.md)   
 [Sp_delete_jobsteplog &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-jobsteplog-transact-sql.md)   
 [SQL Server-Agent-gespeicherte Prozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)  
  
  

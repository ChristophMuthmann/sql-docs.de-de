---
title: Sp_stop_job (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/01/2016
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
- sp_stop_job_TSQL
- sp_stop_job
dev_langs:
- TSQL
helpviewer_keywords:
- sp_stop_job
ms.assetid: 64b4cc75-99a0-421e-b418-94e37595bbb0
caps.latest.revision: 38
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b90ea52e3a64f245633b19f23382b9a147fd1639
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spstopjob-transact-sql"></a>sp_stop_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Weist den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent an, die Ausführung des Auftrags zu beenden.  

  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_stop_job   
      [@job_name =] 'job_name'  
    | [@job_id =] job_id   
    | [@originating_server =] 'master_server'  
    | [@server_name =] 'target_server'  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@job_name =**] **'***job_name***'**  
 Der Name des Auftrags, der beendet werden soll. *Job_name* ist **Sysname**, hat den Standardwert NULL.  
  
 [ **@job_id =**] *job_id*  
 Die ID des Auftrags, der beendet werden soll. *Job_id* ist **"uniqueidentifier"**, hat den Standardwert NULL.  
  
 [ **@originating_server =**] **'***master_server***'**  
 Der Name des Masterservers. Wenn angegeben, werden alle Multiserveraufträge beendet. *Master_server* ist **vom Datentyp nvarchar(128)**, hat den Standardwert NULL. Geben Sie diesen Parameter nur, wenn aufgerufen **Sp_stop_job** an einen Zielserver.  
  
> [!NOTE]  
>  Es kann jeweils nur einer der ersten drei Parameter angegeben werden.  
  
 [ **@server_name =**] **'***target_server***'**  
 Der Name des Zielservers, auf dem ein Multiserverauftrag beendet werden soll. *Target_server* ist **vom Datentyp nvarchar(128)**, hat den Standardwert NULL. Geben Sie diesen Parameter nur, wenn aufgerufen **Sp_stop_job** auf einem Masterserver für einen Multiserverauftrag.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="remarks"></a>Hinweise  
 **Sp_stop_job** sendet ein stoppsignal an die Datenbank. Einige Prozesse können sofort beendet werden und einige muss einen stabilen Punkt (oder einen Einstiegspunkt zum Codepfad) erreichen, bevor sie beenden können. Bei einigen zeitaufwändigen [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen, etwa BACKUP, RESTORE oder einigen DBCC-Befehlen, kann es längere Zeit dauern, bis sie abgeschlossen sind. Wenn diese ausgeführt werden, kann es eine Weile dauern, bis der Auftrag abgebrochen wird. Der Abbruch eines Auftrags führt dazu, dass ein entsprechender Eintrag im Auftragsverlauf aufgezeichnet wird.  
  
 Wenn ein Auftrag einen Schritt des Typs derzeit ausgeführten **CmdExec** oder **PowerShell**, der ausgeführte Prozess (z. B. MyProgram.exe) vorzeitig beendet erzwungen wird. Ein vorzeitiger Abbruch kann unvorhersehbare Folgen haben, z. B. dass Dateien, die von dem Prozess verwendet wurden, geöffnet bleiben. Folglich **Sp_stop_job** sollte nur in Ausnahmesituationen verwendet werden, wenn der Auftrag Schritte des Typs enthält **CmdExec** oder **PowerShell**.  
  
## <a name="permissions"></a>Berechtigungen  
 Standardmäßig können nur Mitglieder der festen Serverrolle **sysadmin** diese gespeicherte Prozedur ausführen. Andere Benutzer müssen Mitglieder der festen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Datenbankrollen in der **msdb** -Datenbank sein:  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Weitere Informationen zu den Berechtigungen dieser Rollen finden Sie unter [Feste Datenbankrollen des SQL Server-Agents](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
 Mitglieder der **SQLAgentUserRole** und **SQLAgentReaderRole** können nur Aufträge, deren Besitzer er, beendet. Mitglieder der **SQLAgentOperatorRole** können alle lokalen Aufträge einschließlich derjenigen, die von anderen Benutzern gehören beenden. Mitglieder der **Sysadmin** können Aufträge für alle lokalen und Multiserveraufträge beenden.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird der Auftrag `Weekly Sales Data Backup` beendet.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_stop_job  
    N'Weekly Sales Data Backup' ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sp_delete_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [sp_help_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_start_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md)   
 [sp_update_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

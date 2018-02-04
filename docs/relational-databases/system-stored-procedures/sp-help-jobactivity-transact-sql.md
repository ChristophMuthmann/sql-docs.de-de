---
title: Sp_help_jobactivity (Transact-SQL) | Microsoft Docs
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
- sp_help_jobactivity_TSQL
- sp_help_jobactivity
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_jobactivity
ms.assetid: d344864f-b4d3-46b1-8933-b81dec71f511
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a4b1b81a94f272ffed56c26f4ede9080f80527c7
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="sphelpjobactivity-transact-sql"></a>sp_help_jobactivity (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Listet Informationen zum Laufzeitstatus von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent-Aufträgen auf.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_help_jobactivity { [ @job_id = ] job_id | [ @job_name = ] 'job_name' }  
     [ , [ @session_id = ] session_id ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@job_id =**] *job_id*  
 Die Auftrags-ID *Job_id*ist **"uniqueidentifier"**, hat den Standardwert NULL.  
  
 [ **@job_name =**] **'***job_name***'**  
 Der Name des Auftrags. *Job_name*ist **Sysname**, hat den Standardwert NULL.  
  
> [!NOTE]  
>  Entweder *Job_id* oder *Job_name* muss angegeben werden, aber beide können nicht angegeben werden.  
  
 [ **@session_id** = ] *session_id*  
 Die Sitzungs-ID, zu der Informationen erstellt werden sollen. *Session_id* ist **Int**, hat den Standardwert NULL.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Gibt das folgende Resultset zurück:  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|Agent-Sitzungs-ID.|  
|**job_id**|**uniqueidentifier**|ID für den Auftrag.|  
|**job_name**|**sysname**|Name des Auftrags.|  
|**run_requested_date**|**datetime**|Datum, zu dem die Ausführung des Auftrags angefordert wurde.|  
|**run_requested_source**|**sysname**|Die Quelle der Anforderung zum Ausführen des Auftrags. Folgende Angaben sind möglich:<br /><br /> **1** = ausführen nach einem Zeitplan<br /><br /> **2** = Ausführen als Antwort auf eine Warnung<br /><br /> **3** = ausführen beim Start<br /><br /> **4** = ausführen durch einen Benutzer<br /><br /> **6** = ausführen nach CPU im Leerlauf Zeitplan|  
|**queued_date**|**datetime**|Datum, an dem die Anforderung in die Warteschlange aufgenommen wurde. NULL, wenn der Auftrag direkt ausgeführt wurde.|  
|**start_execution_date**|**datetime**|Datum, an dem der Auftrag einem ausführbaren Thread zugewiesen wurde.|  
|**last_executed_step_id**|**int**|Die Schritt-ID des zuletzt ausgeführten Auftragsschritts.|  
|**last_exectued_step_date**|**datetime**|Uhrzeit, zu der die Ausführung des zuletzt ausgeführten Auftragsschritts begonnen hat.|  
|**stop_execution_date**|**datetime**|Uhrzeit, zu der die Ausführung des Auftrags beendet wurde.|  
|**next_scheduled_run_date**|**datetime**|Datum, an dem die nächste Ausführung des Auftrags geplant ist.|  
|**job_history_id**|**int**|ID für den Auftragsverlauf in der Auftragsverlaufstabelle.|  
|**Nachricht**|**nvarchar(1024)**|Meldung, die während der letzten Ausführung des Auftrags ausgegeben wurde.|  
|**run_status**|**int**|Status, der während der letzten Ausführung des Auftrags zurückgegeben wurde:<br /><br /> **0** = Fehler<br /><br /> **1** = war erfolgreich<br /><br /> **3** = abgebrochen<br /><br /> **5** = Status unbekannt|  
|**operator_id_emailed**|**int**|ID des Operators, der durch eine E-Mail-Nachricht bei Beendigung des Auftrags benachrichtigt wurde.|  
|**operator_id_netsent**|**int**|ID des Operators, der benachrichtigt über **net Send** nach Abschluss des Auftrags.|  
|**operator_id_paged**|**int**|ID des Operators, der durch einen Pager bei Beendigung des Auftrags benachrichtigt wurde.|  
  
## <a name="remarks"></a>Hinweise  
 Diese Prozedur stellt eine Momentaufnahme des aktuellen Status des Auftrags bereit. Die zurückgegebenen Ergebnisse stellen Informationen zu dem Zeitpunkt der Anforderungsverarbeitung dar.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent erstellt eine Sitzungs-Id jedes Mal, die der Agent-Dienst gestartet wird. Die Sitzungs-Id ist in der Tabelle gespeicherten **msdb.dbo.syssessions**.  
  
 Wenn kein *Session_id* bereitgestellt wird, werden Informationen zur letzten Sitzung aufgelistet.  
  
 Wenn kein *Job_name* oder *Job_id* bereitgestellt wird, werden Informationen für alle Aufträge aufgeführt.  
  
## <a name="permissions"></a>Berechtigungen  
 Standardmäßig können Mitglieder von der **Sysadmin** -Serverrolle kann diese gespeicherte Prozedur ausführen. Andere Benutzer müssen Mitglieder der festen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Datenbankrollen in der **msdb** -Datenbank sein:  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Weitere Informationen zu den Berechtigungen dieser Rollen finden Sie unter [Feste Datenbankrollen des SQL Server-Agents](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
 Nur Mitglieder der **Sysadmin** können die Aktivität für Aufträge, deren Besitzer andere Benutzer anzeigen.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel ist die Aktivität für alle Aufträge aufgeführt, zu deren Anzeige der Benutzer berechtigt ist.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobactivity ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server-Agent-gespeicherte Prozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)  
  
  

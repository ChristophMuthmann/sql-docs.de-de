---
title: Sp_help_jobs_in_schedule (Transact-SQL) | Microsoft Docs
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
- sp_help_jobs_in_schedule_TSQL
- sp_help_jobs_in_schedule
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_jobs_in_schedule
ms.assetid: 1168aa2c-136b-4ba3-b18e-9070d95a26fa
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: aac7c4d1cb1199f17e060c9c9d0d4437d8a3220c
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="sphelpjobsinschedule-transact-sql"></a>sp_help_jobs_in_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt Informationen zu den Aufträgen zurück, an die ein bestimmter Zeitplan angefügt ist.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_help_jobs_in_schedule   
     [ @schedule_name = ] 'schedule_name' ,  
     [ @schedule_id = ] schedule_id   
```  
  
## <a name="arguments"></a>Argumente  
 [ **@schedule_id =** ] *schedule_id*  
 Der Bezeichner des Zeitplans, für den Informationen aufgelistet werden sollen. *Schedule_id* ist **Int**, hat keinen Standardwert. Entweder *Schedule_id* oder *Schedule_name* kann angegeben werden.  
  
 [ **@schedule_name =** ] **'***schedule_name***'**  
 Der Name des Zeitplans, für den Informationen aufgelistet werden sollen. *Schedule_name* ist **Sysname**, hat keinen Standardwert. Entweder *Schedule_id* oder *Schedule_name* kann angegeben werden.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Gibt das folgende Resultset zurück:  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**job_id**|**uniqueidentifier**|Die eindeutige ID des Auftrags.|  
|**originating_server**|**nvarchar(30)**|Name des Servers, von dem der Auftrag stammt|  
|**name**|**sysname**|Name des Auftrags.|  
|**enabled**|**tinyint**|Zeigt an, ob der Auftrag für die Ausführung aktiviert ist.|  
|**description**|**nvarchar(512)**|Beschreibung für den Auftrag.|  
|**start_step_id**|**int**|ID des Schrittes in dem Auftrag, bei dem die Ausführung beginnen soll.|  
|**category**|**sysname**|Auftragskategorie|  
|**Besitzer**|**sysname**|Auftragsbesitzer|  
|**notify_level_eventlog**|**int**|Bitmaske, die anzeigt, unter welchen Umständen ein Benachrichtigungsereignis im Microsoft Windows-Anwendungsprotokoll protokolliert werden soll. Einer der folgenden Werte sind möglich:<br /><br /> **0** = Nie<br /><br /> **1** = bei erfolgreicher Ausführung des Auftrags<br /><br /> **2** = Bei Fehlschlagen des Auftrags<br /><br /> **3** = Immer, wenn der Auftrag abgeschlossen ist (unabhängig vom Ergebnis des Auftrags)|  
|**notify_level_email**|**int**|Bitmaske, die anzeigt, unter welchen Umständen bei Abschluss eines Auftrags eine Benachrichtigungs-E-Mail gesendet werden soll. Mögliche Werte sind die gleichen wie für **Notify_level_eventlog**.|  
|**notify_level_netsend**|**int**|Bitmaske, die anzeigt, unter welchen Umständen bei Abschluss eines Auftrags eine Netzwerkmeldung gesendet werden soll. Mögliche Werte sind die gleichen wie für **Notify_level_eventlog**.|  
|**notify_level_page**|**int**|Bitmaske, die anzeigt, unter welchen Umständen bei Abschluss eines Auftrags eine Benachrichtigung per Pager gesendet werden soll. Mögliche Werte sind die gleichen wie für **Notify_level_eventlog**.|  
|**notify_email_operator**|**sysname**|E-Mail-Name des Operators, der benachrichtigt werden soll.|  
|**notify_netsend_operator**|**sysname**|Name des Computers oder Benutzers, der beim Senden von Netzwerkmeldungen verwendet wird|  
|**notify_page_operator**|**sysname**|Name des Computers oder Benutzers, der beim Senden einer Pagerbenachrichtigung verwendet wird|  
|**delete_level**|**int**|Bitmaske, die anzeigt, unter welchen Umständen der Auftrag bei Abschluss eines Auftrags gelöscht werden soll. Mögliche Werte sind die gleichen wie für **Notify_level_eventlog**.|  
|**date_created**|**datetime**|Datum, an dem der Auftrag erstellt wurde.|  
|**date_modified**|**datetime**|Datum, an dem der Auftrag zuletzt geändert wurde.|  
|**version_number**|**int**|Version des Auftrags (wird automatisch jedes Mal aktualisiert, wenn der Auftrag geändert wird)|  
|**last_run_date**|**int**|Datum, an dem die Ausführung des Auftrags zuletzt gestartet wurde|  
|**last_run_time**|**int**|Uhrzeit, zu der die Ausführung des Auftrags zuletzt gestartet wurde|  
|**last_run_outcome**|**int**|Ergebnis des Auftrags bei der letzten Ausführung:<br /><br /> **0** = Fehler<br /><br /> **1** = war erfolgreich<br /><br /> **3** = abgebrochen<br /><br /> **5** = unbekannt|  
|**next_run_date**|**int**|Datum, für das die nächste Ausführung des Auftrags geplant ist|  
|**next_run_time**|**int**|Uhrzeit, zu der die nächste Ausführung des Auftrags geplant ist|  
|**next_run_schedule_id**|**int**|Zeitplan-ID für nächste Ausführung|  
|**current_execution_status**|**int**|Aktueller Ausführungsstatus|  
|**current_execution_step**|**sysname**|Aktueller Ausführungsschritt des Auftrags|  
|**current_retry_attempt**|**int**|Wenn der Auftrag ausgeführt wird und der Schritt wiederholt wurde, ist dies der aktuelle Wiederholungsversuch|  
|**has_step**|**int**|Anzahl der Auftragsschritte des Auftrags|  
|**has_schedule**|**int**|Anzahl der Auftragszeitpläne des Auftrags|  
|**has_target**|**int**|Die Anzahl der Zielserver des Auftrags.|  
|**type**|**int**|Der Typ des Auftrags:<br /><br /> **1** = Lokaler Auftrag.<br /><br /> **2** = Multiserverauftrag.<br /><br /> **0** = Auftrag hat keine Zielserver.|  
  
## <a name="remarks"></a>Hinweise  
 In dieser Prozedur werden Informationen aufgelistet, die an den bestimmten Zeitplan angefügt sind.  
  
## <a name="permissions"></a>Berechtigungen  
 Standardmäßig können nur Mitglieder der festen Serverrolle **sysadmin** diese gespeicherte Prozedur ausführen. Andere Benutzer müssen Mitglieder der festen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Datenbankrollen in der **msdb** -Datenbank sein:  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Weitere Informationen zu den Berechtigungen dieser Rollen finden Sie unter [Feste Datenbankrollen des SQL Server-Agents](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
 Mitglieder der **SQLAgentUserRole** sehen Sie nur den Status von Aufträgen, die sie besitzen.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden die dem Zeitplan `NightlyJobs` angefügten Aufträge aufgelistet.  
  
```  
USE msdb ;  
GO  
  
EXEC sp_help_jobs_in_schedule  
    @schedule_name = N'NightlyJobs' ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server-Agent-gespeicherte Prozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_attach_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)   
 [sp_delete_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [sp_detach_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-detach-schedule-transact-sql.md)  
  
  

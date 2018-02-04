---
title: Sp_update_alert (Transact-SQL) | Microsoft Docs
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
- sp_update_alert_TSQL
- sp_update_alert
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_alert
ms.assetid: 4bbaeaab-8aca-4c9e-abc1-82ce73090bd3
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7d39736eed19992c5fa20bb1231aed3bcb20e3b0
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="spupdatealert-transact-sql"></a>sp_update_alert (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aktualisiert die Einstellungen einer vorhandenen Warnung.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_update_alert   
     [ @name =] 'name'   
     [ , [ @new_name =] 'new_name']   
     [ , [ @enabled =] enabled]   
     [ , [ @message_id =] message_id]   
     [ , [ @severity =] severity]   
     [ , [ @delay_between_responses =] delay_between_responses]   
     [ , [ @notification_message =] 'notification_message']   
     [ , [ @include_event_description_in =] include_event_description_in]   
     [ , [ @database_name =] 'database']   
     [ , [ @event_description_keyword =] 'event_description_keyword']   
     [ , [ @job_id =] job_id | [@job_name =] 'job_name']   
     [ , [ @occurrence_count = ] occurrence_count]   
     [ , [ @count_reset_date =] count_reset_date]   
     [ , [ @count_reset_time =] count_reset_time]   
     [ , [ @last_occurrence_date =] last_occurrence_date]   
     [ , [ @last_occurrence_time =] last_occurrence_time]   
     [ , [ @last_response_date =] last_response_date]   
     [ , [ @last_response_time =] last_response _time]  
     [ , [ @raise_snmp_trap =] raise_snmp_trap]  
     [ , [ @performance_condition =] 'performance_condition' ]   
     [ , [ @category_name =] 'category']  
     [ , [ @wmi_namespace = ] 'wmi_namespace' ]  
     [ , [ @wmi_query = ] 'wmi_query' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@name =**] **'***name***'**  
 Der Name der Warnung, die aktualisiert werden soll. *Namen* ist **Sysname**, hat keinen Standardwert.  
  
 [ **@new_name =**] **'***new_name***'**  
 Ein neuer Name für die Warnung. Der Name muss eindeutig sein. *New_name* ist **Sysname**, hat den Standardwert NULL.  
  
 [ **@enabled =**] *enabled*  
 Gibt an, ob die Warnung aktiviert ist (**1**) oder nicht aktiviert (**0**). *aktiviert* ist **"tinyint"**, hat den Standardwert NULL. Eine Warnung muss aktiviert sein, um ausgelöst werden zu können.  
  
 [ **@message_id =**] *message_id*  
 Eine neue Meldungs- oder Fehlernummer für die Warnungsdefinition. In der Regel *Message_id* entspricht einer Fehlernummer in der **Sysmessages** Tabelle. *Message_id* ist **Int**, hat den Standardwert NULL. Eine Nachricht, die ID verwendet werden, kann nur, wenn die Einstellung der Schweregrad der Warnung **0**.  
  
 [ **@severity =**] *severity*  
 Ein neuer Schweregrad (von **1** über **25**) für die Warnungsdefinition. Alle [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Nachrichten an das Windows-Anwendungsprotokoll mit dem angegebenen Schweregrad wird die Warnung aktiviert. *Schweregrad* ist **Int**, hat den Standardwert NULL. Ein Schweregrad kann verwendet werden, nur dann, wenn die Nachrichten-ID-Einstellung für die Warnung ist **0**.  
  
 [ **@delay_between_responses =**] *delay_between_responses*  
 Die neue Wartezeit zwischen Antworten auf die Warnung in Sekunden. *Delay_between_responses* ist **Int**, hat den Standardwert NULL.  
  
 [  **@notification_message =**] **"***Notification_message***"**  
 Der überarbeitete Text einer zusätzlichen Nachricht, die an den Operator gesendet werden, als Teil der e-Mail- **net Send**,- oder Pagerbenachrichtigung. *Notification_message* ist **vom Datentyp nvarchar(512)**, hat den Standardwert NULL.  
  
 [ **@include_event_description_in =**] *include_event_description_in*  
 Gibt an, ob die Beschreibung des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Fehlers aus dem Windows-Anwendungsprotokoll in die Benachrichtigungsmeldung eingeschlossen werden soll. *Include_event_description_in* ist **"tinyint"**, hat den Standardwert NULL, und eine oder mehrere der folgenden Werte sind möglich.  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|**0**|Keine|  
|**1**|E-Mail|  
|**2**|Pager|  
|**4**|**net send**|  
|**7**|Alle|  
  
 [ **@database_name =**] **'***database***'**  
 Der Name der Datenbank, in der der Fehler auftreten muss, damit die Warnung ausgelöst wird. *Datenbank* ist **Sysname.** In eckige Klammern ([ ]) eingeschlossene Namen sind nicht zulässig. Der Standardwert ist NULL.  
  
 [ **@event_description_keyword =**] **'***event_description_keyword***'**  
 Eine Folge von Zeichen, die in der Beschreibung des Fehlers im Fehlermeldungsprotokoll enthalten sein muss. Zulässig sind Zeichen, die dem Muster des LIKE-Ausdrucks von [!INCLUDE[tsql](../../includes/tsql-md.md)] entsprechen. *event_description_keyword* is **nvarchar(100)**, with a default of NULL. Dieser Parameter ist hilfreich beim Filtern von Objektnamen (z. B. **%customer_table%**).  
  
 [ **@job_id =**] *job_id*  
 Die Auftrags-ID *Job_id* ist **"uniqueidentifier"**, hat den Standardwert NULL. Wenn *Job_id* angegeben wird, *Job_name* muss weggelassen werden.  
  
 [ **@job_name =**] **'***job_name***'**  
 Der Name des Auftrags, der als Reaktion auf die Warnung ausgeführt wird. *Job_name* ist **Sysname**, hat den Standardwert NULL. Wenn *Job_name* angegeben wird, *Job_id* muss weggelassen werden.  
  
 [ **@occurrence_count =** ] *occurrence_count*  
 Setzt die Häufigkeit zurück, mit der die Warnung aufgetreten ist. *Occurrence_count* ist **Int**, hat den Standardwert NULL und kann nur festgelegt werden, **0**.  
  
 [ **@count_reset_date =**] *count_reset_date*  
 Setzt das Datum zurück, an dem die Anzahl der Vorkommen zuletzt zurückgesetzt wurde. *Count_reset_date* ist **Int**, hat den Standardwert NULL.  
  
 [ **@count_reset_time =**] *count_reset_time*  
 Setzt die Uhrzeit zurück, zu der die Anzahl der Vorkommen zuletzt zurückgesetzt wurde. *Count_reset_time* ist **Int**, hat den Standardwert NULL.  
  
 [ **@last_occurrence_date =**] *last_occurrence_date*  
 Setzt das Datum zurück, an dem die Warnung zuletzt aufgetreten ist. *Last_occurrence_date* ist **Int**, hat den Standardwert NULL und kann nur festgelegt werden, **0**.  
  
 [ **@last_occurrence_time =**] *last_occurrence_time*  
 Setzt die Uhrzeit zurück, zu der die Warnung zuletzt aufgetreten ist. *Last_occurrence_time* ist **Int**, hat den Standardwert NULL und kann nur festgelegt werden, **0**.  
  
 [ **@last_response_date =**] *last_response_date*  
 Setzt das Datum zurück, an dem der SQLSERVERAGENT-Dienst zuletzt auf die Warnung reagiert hat. *Last_response_date* ist **Int**, hat den Standardwert NULL und kann nur festgelegt werden, **0**.  
  
 [ **@last_response_time =**] *last_response_time*  
 Setzt die Uhrzeit zurück, zu der der SQLSERVERAGENT-Dienst zuletzt auf die Warnung reagiert hat. *Last_response_time* ist **Int**, hat den Standardwert NULL und kann nur festgelegt werden, **0**.  
  
 [ **@raise_snmp_trap =**] *raise_snmp_trap*  
 Reserviert.  
  
 [ **@performance_condition =**] **'***performance_condition***'**  
 Ein Wert im Format **"***Itemcomparatorvalue***"**. *Performance_condition* ist **vom Datentyp nvarchar(512)**, hat den Standardwert NULL, und diese Elemente besteht.  
  
|Format-Element|Description|  
|--------------------|-----------------|  
|*Element*|Ein Leistungsobjekt, ein Leistungsindikator oder die benannte Instanz des Indikators|  
|*Comparator*|Einer dieser Operatoren:  **>** ,  **<** ,**=**|  
|*Wert*|Numerischer Wert des Indikators|  
  
 [ **@category_name =**] **'***category***'**  
 Der Name der Warnungskategorie. *Kategorie* ist **Sysname** hat den Standardwert NULL.  
  
 [ **@wmi_namespace**= ] **'***wmi_namespace***'**  
 Der WMI-Namespace zum Abfragen der Ereignisse. *Wmi_namespace* ist **Sysname**, hat den Standardwert NULL.  
  
 [ **@wmi_query**= ] **'***wmi_query***'**  
 Die Abfrage, die das WMI-Ereignis für die Warnung angibt. *Wmi_query* ist **vom Datentyp nvarchar(512)**, hat den Standardwert NULL.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 Nur **Sysmessages** geschrieben werden, um die [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Anwendungsprotokoll kann eine Warnung auslösen.  
  
 **Sp_update_alert** ändert nur die warnungseinstellungen an, die für die Parameterwerte angegeben werden. Wird ein Parameter nicht angegeben, wird die aktuelle Einstellung beibehalten.  
  
## <a name="permissions"></a>Berechtigungen  
 Um diese gespeicherte Prozedur auszuführen, müssen Benutzer Mitglied werden die **Sysadmin** festen Serverrolle "".  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die Aktivierungseinstellung von `Test Alert` in `0` geändert.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_alert  
    @name = N'Test Alert',  
    @enabled = 0 ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sp_add_alert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-alert-transact-sql.md)   
 [sp_help_alert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-alert-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

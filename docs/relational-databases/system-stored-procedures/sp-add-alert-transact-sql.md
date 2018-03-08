---
title: Sp_add_alert (Transact-SQL) | Microsoft Docs
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
- sp_add_alert
- sp_add_alert_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_alert
ms.assetid: d9b41853-e22d-4813-a79f-57efb4511f09
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e66b0fd7fffb92a9646e99f84576651e4dd8b70e
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="spaddalert-transact-sql"></a>sp_add_alert (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Erstellt eine Warnung.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_add_alert [ @name = ] 'name'   
     [ , [ @message_id = ] message_id ]   
     [ , [ @severity = ] severity ]   
     [ , [ @enabled = ] enabled ]  
     [ , [ @delay_between_responses = ] delay_between_responses ]   
     [ , [ @notification_message = ] 'notification_message' ]   
     [ , [ @include_event_description_in = ] include_event_description_in ]   
     [ , [ @database_name = ] 'database' ]   
     [ , [ @event_description_keyword = ] 'event_description_keyword_pattern' ]   
     [ , { [ @job_id = ] job_id | [ @job_name = ] 'job_name' } ]   
     [ , [ @raise_snmp_trap = ] raise_snmp_trap ]   
     [ , [ @performance_condition = ] 'performance_condition' ]   
     [ , [ @category_name = ] 'category' ]   
     [ , [ @wmi_namespace = ] 'wmi_namespace' ]  
     [ , [ @wmi_query = ] 'wmi_query' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@name =** ] **'***name***'**  
 Der Name der Warnung. Der Name wird in der E-Mail- oder Pagernachricht angezeigt, die als Reaktion auf die Warnung gesendet wird. Er muss eindeutig sein und darf kein Prozentzeichen (**%**) Zeichen. *Namen* ist **Sysname**, hat keinen Standardwert.  
  
 [ **@message_id =** ] *message_id*  
 Die Fehlernummer der Meldung, die die Warnung definiert. (Dies entspricht normalerweise einer Fehlernummer in der **Sysmessages** Tabelle.) *Message_id* ist **Int**, hat den Standardwert **0**. Wenn *Schweregrad* wird verwendet, um die Definition der Warnung *Message_id* muss **0** oder NULL.  
  
> [!NOTE]  
>  Nur **Sysmessages** Fehler in der Microsoft Windows-Anwendungsprotokoll geschrieben können dazu führen, dass eine Warnung gesendet werden.  
  
 [ **@severity =** ] *severity*  
 Der Schweregrad (von **1** über **25**), die die Warnung definiert. Alle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Nachrichten gespeichert werden, der **Sysmessages** Tabelle gesendet, um die [!INCLUDE[msCoName](../../includes/msconame-md.md)] bewirkt, dass Windows-Anwendungsprotokoll mit dem angegebenen Schweregrad der Warnung gesendet werden. *Schweregrad* ist **Int**, hat den Standardwert 0. Wenn *Message_id* wird verwendet, um die Definition der Warnung *Schweregrad* muss **0**.  
  
 [ **@enabled =** ] *enabled*  
 Gibt den aktuellen Status der Warnung an. *aktiviert* ist **"tinyint"**, hat den Standardwert 1 (aktiviert). Wenn **0**, der die Warnung ist nicht aktiviert und wird nicht ausgelöst.  
  
 [ **@delay_between_responses =** ] *delay_between_responses*  
 Die Wartezeit zwischen Antworten auf die Warnung in Sekunden. *Delay_between_responses*ist **Int**, hat den Standardwert **0**, was bedeutet, dass keine Wartezeit zwischen Antworten (jedes Vorkommen der Warnung generiert eine Antwort). Die Reaktion kann in einer oder beiden der folgenden Formen erfolgen:  
  
-   Als eine oder mehrere per E-Mail oder Pager gesendete Benachrichtigungen.  
  
-   Als auszuführender Auftrag.  
  
 Mit dem Festlegen dieses Werts kann beispielsweise verhindert werden, dass unerwünschte E-Mail-Nachrichten gesendet werden, wenn eine Warnung in kurzen Zeitabständen wiederholt auftritt.  
  
 [  **@notification_message =** ] **"***Notification_message***"**  
 Ist eine optionale zusätzliche Meldung, die an den Operator gesendet werden, als Teil der e-Mail- **net Send**,- oder Pagerbenachrichtigung. *Notification_message* ist **vom Datentyp nvarchar(512)**, hat den Standardwert NULL. Angeben von *Notification_message* eignet sich für spezielle Anmerkungen, z. B. Hilfsmaßnahmen hinzuzufügen.  
  
 [ **@include_event_description_in =** ] *include_event_description_in*  
 Gibt an, ob die Beschreibung des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Fehlers in die Benachrichtigungsmeldung eingeschlossen werden soll. *include_event_description_in*is **tinyint**, with a default of **5** (e-mail and **net send**), and can have one or more of these values combined with an **OR** logical operator.  
  
> [!IMPORTANT]  
>  Die Pager- und **net send** -Optionen werden in zukünftigen Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht mehr im [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Nutzen Sie diese Funktionen bei Neuentwicklungen nicht mehr, und planen Sie die Änderung von Anwendungen, die diese Funktionen zurzeit verwenden.  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|**0**|Keine|  
|**1**|E-Mail|  
|**2**|Pager|  
|**4**|**net send**|  
  
 [ **@database_name =** ] **'***database***'**  
 Die Datenbank, in der der Fehler auftreten muss, damit die Warnung ausgelöst wird. Wenn *Datenbank*nicht angegeben wird, wird die Warnung ausgelöst, unabhängig davon, wo der Fehler aufgetreten ist. *Datenbank* ist **Sysname**. In eckige Klammern ([ ]) eingeschlossene Namen sind nicht zulässig. Der Standardwert ist NULL.  
  
 [ **@event_description_keyword =** ] **'***event_description_keyword_pattern***'**  
 Die Zeichenfolge, der die Beschreibung des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Fehlers entsprechen muss. Zulässig sind Zeichen, die dem Muster des LIKE-Ausdrucks von [!INCLUDE[tsql](../../includes/tsql-md.md)] entsprechen. *event_description_keyword_pattern* is **nvarchar(100)**, with a default of NULL. Dieser Parameter ist hilfreich beim Filtern von Objektnamen (z. B. **%customer_table%**).  
  
 [ **@job_id =** ] *job_id*  
 Die Auftrags-ID des Auftrags, der als Reaktion auf diese Warnung ausgeführt werden soll. *Job_id* ist **"uniqueidentifier"**, hat den Standardwert NULL.  
  
 [ **@job_name =** ] **'***job_name***'**  
 Der Name des Auftrags, der als Reaktion auf diese Warnung ausgeführt werden soll. *Job_name*ist **Sysname**, hat den Standardwert NULL.  
  
> [!NOTE]  
>  Entweder *Job_id* oder *Job_name* muss angegeben werden, aber beide können nicht angegeben werden.  
  
 [ **@raise_snmp_trap =** ] *raise_snmp_trap*  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Version 7.0, nicht implementiert. *Raise_snmp_trap* ist **"tinyint"**, hat den Standardwert 0.  
  
 [ **@performance_condition =** ] **'***performance_condition***'**  
 Ein Wert im Format "*Itemcomparatorvalue*". *Performance_condition* ist **vom Datentyp nvarchar(512)** hat den Standardwert NULL, und diese Elemente besteht.  
  
|Format-Element|Description|  
|--------------------|-----------------|  
|*Element*|Ein Leistungsobjekt, ein Leistungsindikator oder die benannte Instanz des Indikators|  
|*Comparator*|Einer dieser Operatoren: >, < oder =|  
|*Wert*|Numerischer Wert des Indikators|  
  
 [ **@category_name =** ] **'***category***'**  
 Der Name der Warnungskategorie. *Kategorie* ist **Sysname**, hat den Standardwert NULL.  
  
 [ **@wmi_namespace**= ] **'***wmi_namespace***'**  
 Der WMI-Namespace zum Abfragen der Ereignisse. *Wmi_namespace* ist **Sysname**, hat den Standardwert NULL. Es werden nur Namespaces auf dem lokalen Server unterstützt.  
  
 [ **@wmi_query**= ] **'***wmi_query***'**  
 Die Abfrage, die das WMI-Ereignis für die Warnung angibt. *Wmi_query* ist **vom Datentyp nvarchar(512)**, hat den Standardwert NULL.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="remarks"></a>Hinweise  
 **Sp_add_alert** muss ausgeführt werden, aus der **Msdb** Datenbank.  
  
 Unter den folgenden Umständen werden von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anwendungen generierte Fehler bzw. Meldungen an das Windows-Anwendungsprotokoll gesendet und können somit Warnungen auslösen:  
  
-   Der Schweregrad 19 oder höher **sys.messages** Fehler  
  
-   Jede RAISERROR-Anweisung, die mit der WITH LOG-Syntax aufgerufen wurde.  
  
-   Alle **sys.messages** Fehler geändert oder mithilfe der **Sp_altermessage**  
  
-   Jedes Ereignis protokolliert mit **Xp_logevent**  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] lässt sich das gesamte Warnungssystem auf einfache Weise mit einer grafischen Oberfläche verwalten. Dies ist die empfohlene Vorgehensweise, um eine Warnungsinfrastruktur zu konfigurieren.  
  
 Überprüfen Sie die folgenden Punkte, wenn eine Warnung nicht ordnungsgemäß funktioniert:  
  
-   Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agentdienst wird ausgeführt.  
  
-   Das Ereignis wird im Windows-Anwendungsprotokoll angezeigt.  
  
-   Die Warnung ist aktiviert.  
  
-   Ereignisse, die mit **xp_logevent** generiert werden, treten in der master-Datenbank auf. Daher wird von **xp_logevent** erst dann eine Warnung ausgegeben, wenn der **@database_name** -Wert für die Warnung den Wert **'master'** oder NULL hat.  
  
## <a name="permissions"></a>Berechtigungen  
 Standardmäßig können nur Mitglieder der festen Serverrolle **sysadmin** die Prozedur **sp_add_alert**ausführen.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine Warnung (Test Alert) hinzugefügt, die den `Back up the AdventureWorks2012 Database`-Auftrag ausführt, wenn sie ausgegeben wird.  
  
> [!NOTE]  
>  Bei diesem Beispiel wird vorausgesetzt, dass die Meldung 55001 und der `Back up the AdventureWorks2012 Database`-Auftrag vorhanden sind. Dieses Beispiel dient lediglich zu Illustrationszwecken.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_alert  
    @name = N'Test Alert',  
    @message_id = 55001,   
   @severity = 0,   
   @notification_message = N'Error 55001 has occurred. The database will be backed up...',   
   @job_name = N'Back up the AdventureWorks2012 Database' ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sp_add_notification &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-notification-transact-sql.md)   
 [sp_altermessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-altermessage-transact-sql.md)   
 [sp_delete_alert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-alert-transact-sql.md)   
 [sp_help_alert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-alert-transact-sql.md)   
 [sp_update_alert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-alert-transact-sql.md)   
 [sys.sysperfinfo &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysperfinfo-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

---
title: Sp_help_alert (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2016
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
- sp_help_alert
- sp_help_alert_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_alert
ms.assetid: 850cef4e-6348-4439-8e79-fd1bca712091
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7f1dc2217a34afadc5a105709ac294325ac9e80a
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="sphelpalert-transact-sql"></a>sp_help_alert (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt Informationen zu den für einen Server definierten Warnungen zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_help_alert [ [ @alert_name = ] 'alert_name' ]   
     [ , [ @order_by = ] 'order_by' ]   
     [ , [ @alert_id = ] alert_id ]   
     [ , [ @category_name = ] 'category' ]   
     [ , [ @legacy_format = ] legacy_format ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@alert_name =**] **'***alert_name***'**  
 Der Name der Warnung. *Alert_name* ist **vom Datentyp nvarchar(128)**. Wenn *Alert_name* ist nicht angegeben wird, werden Informationen zu allen Warnungen zurückgegeben.  
  
 [ **@order_by =**] **'***order_by***'**  
 Die Sortierreihenfolge, die zum Erzeugen der Ergebnisse verwendet werden soll. *Order_by*ist **Sysname**, hat den Standardwert N '*Namen*".  
  
 [ **@alert_id =**] *alert_id*  
 Die ID der Warnung, zu der Informationen gemeldet werden sollen. *Alert_id*ist **Int**, hat den Standardwert NULL.  
  
 [ **@category_name =**]  **'***category***'**  
 Die Kategorie für die Warnung. *Kategorie* ist **Sysname**, hat den Standardwert NULL.  
  
 [ **@legacy_format**=] *legacy_format*  
 Gibt an, ob ein Legacyresultset erzeugt werden soll. *Legacy_format* ist **Bit**, hat den Standardwert **0**. Wenn *Legacy_format* ist **1**, **Sp_help_alert** zurückgegebene Resultset gibt **Sp_help_alert** in Microsoft SQL Server 2000.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Wenn  **@legacy_format**  ist **0**, **Sp_help_alert** erzeugt das folgende Resultset.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Vom System zugewiesener eindeutiger, ganzzahliger Bezeichner.|  
|**name**|**sysname**|Name der Warnung (z. B. Demo: Full **Msdb** Log).|  
|**event_source**|**nvarchar(100)**|Quelle des Ereignisses. Es werden immer **MSSQLServer** für [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Version 7.0|  
|**event_category_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**event_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**message_id**|**int**|Fehlernummer der Meldung, die die Warnung definiert. (Entspricht normalerweise einer Fehlernummer in der **Sysmessages** Tabelle). Wenn der Schweregrad verwendet wird, um die Definition der Warnung **Message_id** ist **0** oder NULL.|  
|**severity**|**int**|Schweregrad (von **9** über **25**, **110**, **120**, **130**, oder **140**) die die Warnung definiert.|  
|**enabled**|**tinyint**|Status Gibt an, ob die Warnung zurzeit aktiviert (**1**) oder nicht (**0**). Eine nicht aktivierte Warnung wird nicht gesendet.|  
|**delay_between_responses**|**int**|Wartezeit in Sekunden zwischen Antworten auf die Warnung.|  
|**last_occurrence_date**|**int**|Datum, an dem die Warnung zuletzt aufgetreten ist.|  
|**last_occurrence_time**|**int**|Uhrzeit, zu der die Warnung zuletzt aufgetreten ist.|  
|**last_response_date**|**int**|Datum, die die Warnung zuletzt beantwortet von der **SQLServerAgent** Dienst.|  
|**last_response_time**|**int**|Zeit, die die Warnung zuletzt beantwortet von der **SQLServerAgent** Dienst.|  
|**notification_message**|**nvarchar(512)**|Optionale zusätzliche Meldung, die als Teil einer Benachrichtigung per E-Mail oder Pager an den Operator gesendet wird.|  
|**include_event_description**|**tinyint**|Gibt an, ob die Beschreibung des SQL Server-Fehlers in das Microsoft Windows-Anwendungsprotokoll als Teil der Benachrichtigungsmeldung eingeschlossen werden soll.|  
|**database_name**|**sysname**|Datenbank, in der der Fehler auftreten muss, damit die Warnung ausgelöst wird. Wenn der Datenbankname gleich NULL ist, wird die Warnung unabhängig von der Datenbank ausgelöst, in der der Fehler aufgetreten ist.|  
|**event_description_keyword**|**nvarchar(100)**|Beschreibung des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Fehlers im Windows-Anwendungsprotokoll, die der angegebenen Zeichenfolge entsprechen muss.|  
|**occurrence_count**|**int**|Gibt an, wie oft die Warnung aufgetreten ist.|  
|**count_reset_date**|**int**|Datum der **Occurrence_count** zuletzt zurückgesetzt wurde.|  
|**count_reset_time**|**int**|Zeit der **Occurrence_count** zuletzt zurückgesetzt wurde.|  
|**job_id**|**uniqueidentifier**|ID des Auftrags, der als Antwort auf eine Warnung ausgeführt werden soll.|  
|**job_name**|**sysname**|Name des Auftrags, der als Antwort auf eine Warnung ausgeführt werden soll.|  
|**has_notification**|**int**|Ungleich 0, wenn einer oder mehrere Operatoren für diese Warnung benachrichtigt werden. Der Wert kann einen oder mehrere der folgenden Werte (zusammen ORed):<br /><br /> **1**= e-Mail-Benachrichtigung<br /><br /> **2**= Pagerbenachrichtigung<br /><br /> **4**= hat **net Send** Benachrichtigung.|  
|**flags**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**performance_condition**|**nvarchar(512)**|Wenn **Typ** ist **2**, diese Spalte die Definition des Leistungsstatus angezeigt; andernfalls ist die Spalte NULL.|  
|**category_name**|**sysname**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] Immer '[Uncategorized]' für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0.|  
|**wmi_namespace**|**sysname**|Wenn **Typ** ist **3**, diese Spalte zeigt den Namespace für das WMI-Ereignis.|  
|**wmi_query**|**nvarchar(512)**|Wenn **Typ** ist **3**, diese Spalte zeigt die Abfrage für das WMI-Ereignis.|  
|**type**|**int**|Der Typ des Ereignisses:<br /><br /> **1**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -ereigniswarnung<br /><br /> **2**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] leistungswarnung<br /><br /> **3** = WMI-ereigniswarnung|  
  
 Wenn  **@legacy_format**  ist **1**, **Sp_help_alert** erzeugt das folgende Resultset.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Vom System zugewiesener eindeutiger, ganzzahliger Bezeichner.|  
|**name**|**sysname**|Name der Warnung (z. B. Demo: Full **Msdb** Log).|  
|**event_source**|**nvarchar(100)**|Quelle des Ereignisses. Es werden immer **MSSQLServer** für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Version 7.0|  
|**event_category_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**event_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**message_id**|**int**|Fehlernummer der Meldung, die die Warnung definiert. (Entspricht normalerweise einer Fehlernummer in der **Sysmessages** Tabelle). Wenn der Schweregrad verwendet wird, um die Definition der Warnung **Message_id** ist **0** oder NULL.|  
|**severity**|**int**|Schweregrad (von **9** über **25**, **110**, **120**, **130**, oder 1**40**) die die Warnung definiert.|  
|**enabled**|**tinyint**|Status Gibt an, ob die Warnung zurzeit aktiviert (**1**) oder nicht (**0**). Eine nicht aktivierte Warnung wird nicht gesendet.|  
|**delay_between_responses**|**int**|Wartezeit in Sekunden zwischen Antworten auf die Warnung.|  
|**last_occurrence_date**|**int**|Datum, an dem die Warnung zuletzt aufgetreten ist.|  
|**last_occurrence_time**|**int**|Uhrzeit, zu der die Warnung zuletzt aufgetreten ist.|  
|**last_response_date**|**int**|Datum, die die Warnung zuletzt beantwortet von der **SQLServerAgent** Dienst.|  
|**last_response_time**|**int**|Zeit, die die Warnung zuletzt beantwortet von der **SQLServerAgent** Dienst.|  
|**notification_message**|**nvarchar(512)**|Optionale zusätzliche Meldung, die als Teil einer Benachrichtigung per E-Mail oder Pager an den Operator gesendet wird.|  
|**include_event_description**|**tinyint**|Gibt an, ob die Beschreibung des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Fehlers in das Windows-Anwendungsprotokoll als Teil der Benachrichtigungsmeldung eingeschlossen werden soll.|  
|**database_name**|**sysname**|Datenbank, in der der Fehler auftreten muss, damit die Warnung ausgelöst wird. Wenn der Datenbankname gleich NULL ist, wird die Warnung unabhängig von der Datenbank ausgelöst, in der der Fehler aufgetreten ist.|  
|**event_description_keyword**|**nvarchar(100)**|Beschreibung des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Fehlers im Windows-Anwendungsprotokoll, die der angegebenen Zeichenfolge entsprechen muss.|  
|**occurrence_count**|**int**|Gibt an, wie oft die Warnung aufgetreten ist.|  
|**count_reset_date**|**int**|Datum der **Occurrence_count** zuletzt zurückgesetzt wurde.|  
|**count_reset_time**|**int**|Zeit der **Occurrence_count** zuletzt zurückgesetzt wurde.|  
|**job_id**|**uniqueidentifier**|ID des Auftrags.|  
|**job_name**|**sysname**|Ein bedarfsgesteuerter Auftrag, der als Antwort auf eine Warnung ausgeführt werden soll.|  
|**has_notification**|**int**|Ungleich 0, wenn einer oder mehrere Operatoren für diese Warnung benachrichtigt werden. Einer oder mehrere der folgenden Werte sind möglich (mit OR verknüpft):<br /><br /> **1**= e-Mail-Benachrichtigung<br /><br /> **2**= Pagerbenachrichtigung<br /><br /> **4**= hat **net Send** Benachrichtigung.|  
|**flags**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]aus.|  
|**performance_condition**|**nvarchar(512)**|Wenn **Typ** ist **2**, diese Spalte die Definition des Leistungsstatus angezeigt. Wenn **Typ** ist **3**, diese Spalte zeigt die Abfrage für das WMI-Ereignis. Andernfalls weist die Spalte den Wert NULL auf.|  
|**category_name**|**sysname**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] Immer "**[nicht kategorisiert]**" für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0.|  
|**type**|**int**|Warnungstyp:<br /><br /> **1**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -ereigniswarnung<br /><br /> **2**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] leistungswarnung<br /><br /> **3** = WMI-ereigniswarnung|  
  
## <a name="remarks"></a>Hinweise  
 **Sp_help_alert** muss ausgeführt werden, aus der **Msdb** Datenbank.  
  
## <a name="permissions"></a>Berechtigungen  
 Standardmäßig können nur Mitglieder der festen Serverrolle **sysadmin** diese gespeicherte Prozedur ausführen. Andere Benutzer müssen Mitglieder der festen Datenbankrolle **SQLAgentOperatorRole** in der **msdb** -Datenbank sein.  
  
 Weitere Informationen zu **SQLAgentOperatorRole**, finden Sie unter [SQL Server Agent Fixed Database Roles](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden Informationen zur Warnung `Demo: Sev. 25 Errors` abgerufen.  
  
```  
USE msdb ;  
GO  
  
EXEC sp_help_alert @alert_name = 'Demo: Sev. 25 Errors';  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sp_add_alert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-alert-transact-sql.md)   
 [sp_update_alert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-alert-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

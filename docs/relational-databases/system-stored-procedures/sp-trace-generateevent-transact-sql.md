---
title: "\"sp_trace_generateevent\" (Transact-SQL) | Microsoft Docs"
ms.custom: ''
ms.date: 08/09/2016
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
- sp_trace_generateevent_TSQL
- sp_trace_generateevent
dev_langs:
- TSQL
helpviewer_keywords:
- sp_trace_generateevent
ms.assetid: 3ef05bfb-b467-4403-89cc-6e77ef9247dd
caps.latest.revision: 35
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4e0cf34c1efe4d5eee7bb1f531067ccc0f05d291
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sptracegenerateevent-transact-sql"></a>sp_trace_generateevent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Erstellt ein benutzerdefiniertes Ereignis in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
>**Hinweis:** diese gespeicherte Prozedur ist **nicht** als veraltet markiert. Alle anderen ablaufverfolgungsbezogenen gespeicherten Prozeduren sind veraltet.  
  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_trace_generateevent [ @eventid = ] event_id   
     [ , [ @userinfo = ] 'user_info' ]  
     [ , [ @userdata = ] user_data ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@eventid=**] *event_id*  
 Die ID des Ereignisses, das aktiviert werden soll. *event_id* ist vom Datentyp **int**und hat keinen Standardwert. Die ID muss eine der Ereignisnummern von 82 bis 91 sein, die als Gruppe, benutzerdefinierte Ereignisse darstellen [Sp_trace_setevent](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md).  
  
 [ **@userinfo**=] **"***User_info***"**  
 Die optionale benutzerdefinierte Zeichenfolge, die den Grund des Ereignisses identifiziert. *user_info* ist vom Datentyp **nvarchar(128)** und hat den Standardwert NULL.  
  
 [ **@userdata**=] *User_data*  
 Die optionalen benutzerdefinierten Daten für das Ereignis. *user_data* ist vom Datentyp **varbinary(8000)** und hat den Standardwert NULL.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 In der folgenden Tabelle werden die Codewerte beschrieben, die die Benutzer nach Abschluss der gespeicherten Prozedur möglicherweise erhalten.  
  
|Rückgabecode|Description|  
|-----------------|-----------------|  
|**0**|Kein Fehler.|  
|**1**|Unbekannter Fehler.|  
|**3**|Das angegebene Ereignis ist ungültig. Das Ereignis ist möglicherweise nicht vorhanden oder nicht für die gespeicherte Prozedur geeignet.|  
|**13**|Nicht genügend Arbeitsspeicher. Wird zurückgegeben, wenn nicht genügend Arbeitsspeicher zum Ausführen der angegebenen Aktion verfügbar ist.|  
  
## <a name="remarks"></a>Hinweise  
 **"sp_trace_generateevent"** führt viele der Aktionen, die zuvor ausgeführt werden, indem die **Xp_trace_\***  erweiterten gespeicherten Prozeduren. Verwenden Sie **sp_trace_generateevent** anstelle von **xp_trace_generate_event**.  
  
 Mit **sp_trace_generateevent**können nur die ID-Nummern von benutzerdefinierten Ereignissen verwendet werden. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird ein Fehler ausgelöst, wenn andere Ereignis-ID-Nummern verwendet werden.  
  
 Parameter aller gespeicherten Prozeduren der SQL-Ablaufverfolgung (**sp_trace_xx**) haben eine strikte Typbindung. Wenn diese Parameter nicht mit den richtigen Datentypen für Eingabeparameter aufgerufen werden, wie in der Argumentbeschreibung angegeben, gibt die gespeicherte Prozedur einen Fehler zurück.  
  
## <a name="permissions"></a>Berechtigungen  
 Benutzer müssen über die ALTER TRACE-Berechtigung verfügen.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird ein vom Benutzer konfigurierbares Ereignis in einer Beispieltabelle erstellt.  
  
```  
--Create a sample table.  
CREATE TABLE user_config_test(col1 int, col2 char(10));  
  
--DROP the trigger if it already exists.  
IF EXISTS  
   (SELECT * FROM sysobjects WHERE name = 'userconfig_trg')  
   DROP TRIGGER userconfig_trg;  
  
--Create an ON INSERT trigger on the sample table.  
CREATE TRIGGER userconfig_trg  
   ON user_config_test FOR INSERT;  
AS  
EXEC master..sp_trace_generateevent  
   @event_class = 82, @userinfo = N'Inserted row into user_config_test';  
  
--When an insert action happens, the user-configurable event fires. If   
you were capturing the event id=82, you will see it in the Profiler output.  
INSERT INTO user_config_test VALUES(1, 'abc');  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sys.fn_trace_geteventinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-geteventinfo-transact-sql.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [SQL-Ablaufverfolgung](../../relational-databases/sql-trace/sql-trace.md)  
  
  

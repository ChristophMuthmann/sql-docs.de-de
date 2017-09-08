---
title: DROP EVENT NOTIFICATION (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP EVENT NOTIFICATION
- DROP_EVENT_NOTIFICATION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- event notifications [SQL Server], removing
- deleting event notifications
- dropping event notifications
- DROP EVENT NOTIFICATION statement
- removing event notifications
ms.assetid: 0ffd8f47-4ea3-4238-9e73-c318df710cf7
caps.latest.revision: 33
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ab32a9ffadce83635e8ef987607af913fe0f2472
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="drop-event-notification-transact-sql"></a>DROP EVENT NOTIFICATION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Entfernt einen Ereignisbenachrichtigungstrigger aus der aktuellen Datenbank.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
DROP EVENT NOTIFICATION notification_name [ ,...n ]  
ON { SERVER | DATABASE | QUEUE queue_name }  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumente  
 *notification_name*  
 Der Name der zu entfernenden Ereignisbenachrichtigung. Es können mehrere Ereignisbenachrichtigungen angegeben werden. Um eine Liste der aktuell erstellten ereignisbenachrichtigungen anzuzeigen, verwenden [event_notifications &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-event-notifications-transact-sql.md).  
  
 SERVER  
 Gibt den Bereich der Ereignisbenachrichtigungsanwendungen auf den aktuellen Server an. SERVER muss angegeben werden, wenn SERVER beim Erstellen der Ereignisbenachrichtigung angegeben wurde.  
  
 DATABASE  
 Gibt den Bereich der Ereignisbenachrichtigungsanwendungen auf die aktuelle Datenbank an. DATABASE muss angegeben werden, wenn DATABASE beim Erstellen der Ereignisbenachrichtigung angegeben wurde.  
  
 Warteschlange *Warteschlangenname*  
 Gibt an, der Bereich der ereignisbenachrichtigung gilt, an die Warteschlange, die vom angegebenen *Warteschlangenname*. QUEUE musst angegebenen werden, wenn das Element beim Erstellen der Ereignisbenachrichtigung angegeben wurde. *Warteschlangenname* ist der Name der Warteschlange und muss auch angegeben werden.  
  
## <a name="remarks"></a>Hinweise  
 Wenn eine Ereignisbenachrichtigung innerhalb einer Transaktion ausgelöst und innerhalb derselben Transaktion gelöscht wird, wird die Ereignisbenachrichtigungsinstanz gesendet und die Ereignisbenachrichtigung dann gelöscht.  
  
## <a name="permissions"></a>Berechtigungen  
 Zum Löschen einer Ereignisbenachrichtigung, deren Bereich auf Datenbankebene definiert ist, muss ein Benutzer mindestens Besitzer der Ereignisbenachrichtigung sein oder über die ALTER ANY DATABASE EVENT NOTIFICATION-Berechtigung für die aktuelle Datenbank verfügen.  
  
 Zum Löschen einer Ereignisbenachrichtigung, deren Bereich auf Serverebene definiert ist, muss ein Benutzer mindestens Besitzer der Ereignisbenachrichtigung sein oder über die ALTER ANY EVENT NOTIFICATION-Berechtigung für den Server verfügen.  
  
 Um eine Ereignisbenachrichtigung für eine bestimmte Warteschlange zu löschen, muss ein Benutzer mindestens Besitzer der Ereignisbenachrichtigung sein oder über die ALTER-Berechtigung für die übergeordnete Warteschlange verfügen.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine Ereignisbenachrichtigung erstellt und dann gelöscht, deren Bereich eine bestimmte Datenbank ist.  
  
```tsql  
USE AdventureWorks2012;  
GO  
CREATE EVENT NOTIFICATION NotifyALTER_T1  
ON DATABASE  
FOR ALTER_TABLE  
TO SERVICE 'NotifyService',  
    '8140a771-3c4b-4479-8ac0-81008ab17984';  
GO  
DROP EVENT NOTIFICATION NotifyALTER_T1  
ON DATABASE;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen Sie EVENT NOTIFICATION &#40; Transact-SQL &#41;](../../t-sql/statements/create-event-notification-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [Sys. event_notifications &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-event-notifications-transact-sql.md)   
 [Sys.Events &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-events-transact-sql.md)  
  
  

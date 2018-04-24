---
title: BEGIN CONVERSATION TIMER (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CONVERSATION
- BEGIN_CONVERSATION_TSQL
- TIMER_TSQL
- TIMER
- CONVERSATION TIMER
- CONVERSATION_TIMER_TSQL
- BEGIN CONVERSATION TIMER
- BEGIN_CONVERSATION_TIMER_TSQL
- CONVERSATION_TSQL
- BEGIN CONVERSATION
dev_langs:
- TSQL
helpviewer_keywords:
- BEGIN CONVERSATION TIMER statement
- DialogTimer message
- dialogs [Service Broker], beginning
- timeouts [Service Broker]
- timer messages [Service Broker]
- conversations [Service Broker], timers
- starting timers [Service Broker]
- http://schemas.microsoft.com/SQL/ServiceBroker/DialogTimer message
ms.assetid: 98e49b3f-a38f-4180-8171-fa9cb30db4cb
caps.latest.revision: 28
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1b8a88a664b5e89882a60b478a1f3444c6115073
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="begin-conversation-timer-transact-sql"></a>BEGIN CONVERSATION TIMER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Startet einen Zeitgeber. Wenn das Timeout abläuft, stellt [!INCLUDE[ssSB](../../includes/sssb-md.md)] eine Nachricht des Typs `http://schemas.microsoft.com/SQL/ServiceBroker/DialogTimer` in die lokale Warteschlange für die Konversation.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
BEGIN CONVERSATION TIMER ( conversation_handle )  
   TIMEOUT = timeout   
[ ; ]  
```  
  
## <a name="arguments"></a>Argumente  
 BEGIN CONVERSATION TIMER **(***conversation_handle***)**  
 Gibt die Konversation an, für die ein Zeitgeber festgelegt werden soll. *conversation_handle* muss dem Typ **uniqueidentifier** entsprechen.  
  
 TIMEOUT  
 Gibt die Zeitdauer in Sekunden an, die gewartet wird, bevor die Nachricht in der Warteschlange platziert wird.  
  
## <a name="remarks"></a>Remarks  
 Mithilfe eines Konversationszeitgebers kann eine Anwendung nach einem bestimmten Zeitraum eine Nachricht zu einer Konversation empfangen. Wird BEGIN CONVERSATION TIMER für eine Konversation vor Ablauf des Zeitgebers aufgerufen, wird das Timeout auf den neuen Wert festgelegt. Anders als bei der Lebensdauer der Konversation verfügt jede Seite der Konversation über einen unabhängigen Konversationszeitgeber. Die **DialogTimer**-Nachricht kommt in der lokalen Warteschlange an, ohne dass dies Auswirkungen auf die Remoteseite der Konversation hat. Daher kann eine Zeitgebernachricht zu jedem beliebigen Zweck von einer Anwendung verwendet werden.  
  
 Sie können z. B. mithilfe des Konversationszeitgebers verhindern, dass eine Anwendung zu lang auf eine überfällige Antwort wartet. Wenn die Anwendung einen Dialog innerhalb von 30 Sekunden beenden soll, können Sie den Konversationszeitgeber für diesen Dialog auf 60 Sekunden festlegen (30 Sekunden plus einem Zeitraum von 30 Sekunden als Puffer). Falls der Dialog nach 60 Sekunden immer noch geöffnet ist, empfängt die Anwendung eine Timeoutnachricht in der Warteschlange für diesen Dialog.  
  
 Alternativ hierzu kann eine Anwendung auch mithilfe eines Konversationszeitgebers die Aktivierung zu einer bestimmten Zeit anfordern. Sie können z. B. einen Dienst erstellen, der alle fünf Minuten die Anzahl der aktiven Verbindungen angibt, oder einen Dienst, der jeden Abend die Anzahl der offenen Bestellungen angibt. Der Dienst legt einen Konversationstimer fest, der zu der gewünschten Zeit abläuft. Bei Ablauf des Zeitgebers sendet [!INCLUDE[ssSB](../../includes/sssb-md.md)] eine **DialogTimer**-Nachricht. Mit der **DialogTimer**-Nachricht startet [!INCLUDE[ssSB](../../includes/sssb-md.md)] die gespeicherte Aktivierungsprozedur für die Warteschlange. Von der gespeicherten Prozedur wird eine Nachricht an den Remotedienst gesendet und ein Neustart des Konversationszeitgebers ausgeführt.  
  
 BEGIN CONVERSATION TIMER ist in einer benutzerdefinierten Funktion nicht gültig.  
  
## <a name="permissions"></a>Berechtigungen  
 Die Berechtigung zum Festlegen eines Konversationstimers erhalten standardmäßig die Benutzer, die über SEND-Berechtigungen für den Dienst der Konversation verfügen, die Mitglieder der festen Serverrolle **sysadmin** und die Mitglieder der festen Datenbankrolle **db_owner**.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird ein Timeout von zwei Minuten für den durch `@dialog_handle` identifizierten Dialog festgelegt.  
  
```  
-- @dialog_handle is of type uniqueidentifier and  
-- contains a valid conversation handle.  
  
BEGIN CONVERSATION TIMER (@dialog_handle)  
TIMEOUT = 120 ;  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [BEGIN DIALOG CONVERSATION &#40;Transact-SQL&#41;](../../t-sql/statements/begin-dialog-conversation-transact-sql.md)   
 [END CONVERSATION &#40;Transact-SQL&#41;](../../t-sql/statements/end-conversation-transact-sql.md)   
 [RECEIVE &#40;Transact-SQL&#41;](../../t-sql/statements/receive-transact-sql.md)  
  
  

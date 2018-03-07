---
title: END CONVERSATION-Anweisung (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- END DIALOG
- END CONVERSATION
- END_DIALOG_TSQL
- END_CONVERSATION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- errors [Service Broker], conversations
- dialogs [Service Broker], ending
- closing conversations
- END CONVERSATION statement
- conversations [Service Broker], ending
- ending conversations [SQL Server]
ms.assetid: 4415a126-cd22-4a5e-b84a-d8c68515c83b
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d68dcecf84cb24b0c06876d40742c8f5ffe8124d
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="end-conversation-transact-sql"></a>END CONVERSATION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Beendet eine bestehende Konversation auf einer Seite.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
END CONVERSATION conversation_handle  
   [   [ WITH ERROR = failure_code DESCRIPTION = 'failure_text' ]  
     | [ WITH CLEANUP ]  
    ]  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumente  
 *conversation_handle*  
 Bezeichnet das Konversationshandle für die zu beendende Konversation.  
  
 Fehler =*Failure_code*  
 Bezeichnet den Fehlercode. Die *Failure_code* ist vom Typ **Int**. Beim Fehlercode handelt es sich um einen benutzerdefinierten Code, der in der Fehlermeldung eingeschlossen ist, die an die andere Seite der Konversation gesendet wird. Der Fehlercode muss größer als 0 sein.  
  
 DESCRIPTION =*failure_text*  
 Bezeichnet die Fehlermeldung. Die *Failure_text* ist vom Typ **nvarchar(3000)**. Beim Fehlertext handelt es sich um benutzerdefinierten Text, der in der Fehlermeldung eingeschlossen ist, die an die andere Seite der Konversation gesendet wird.  
  
 WITH CLEANUP  
 Entfernt alle Nachrichten und Katalogsichteinträge für eine Seite einer Konversation, die nicht regulär abgeschlossen werden kann. Die andere Seite der Konversation wird nicht über die Bereinigung informiert. [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] löscht den Konversationsendpunkt, alle Nachrichten für die Konversation in der Übertragungswarteschlange sowie alle Nachrichten für die Konversation in der Dienstwarteschlange. Mithilfe dieser Option können Administratoren Konversationen entfernen, die nicht regulär abgeschlossen werden können. Wenn beispielsweise der Remotedienst dauerhaft entfernt wurde, kann ein Administrator mithilfe von WITH CLEANUP Konversationen mit diesem Dienst entfernen. Verwenden Sie WITH CLEANUP nicht im Code eine [!INCLUDE[ssSB](../../includes/sssb-md.md)] Anwendung. Wenn END CONVERSATION WITH CLEANUP ausgeführt wird, bevor der empfangende Endpunkt den Eingang der Nachricht bestätigt, wird die Nachricht vom sendenden Endpunkt erneut gesendet. Möglicherweise wird dadurch der Dialog erneut ausgeführt.  
  
## <a name="remarks"></a>Hinweise  
 Beenden einer Konversation sperren die Konversationsgruppe, die der bereitgestellten *Conversation_handle* angehört. Wenn eine Konversation beendet wird, entfernt [!INCLUDE[ssSB](../../includes/sssb-md.md)] alle Nachrichten für die Konversation aus der Dienstwarteschlange.  
  
 Nach dem Ende einer Konversation kann eine Anwendung keine Nachrichten für diese Konversation mehr senden oder empfangen. Beide Teilnehmer an einer Konversation müssen END CONVERSATION aufrufen, damit die Konversation abgeschlossen wird. Wenn [!INCLUDE[ssSB](../../includes/sssb-md.md)] keine Nachricht über das Beenden des Dialogs oder eine Fehlermeldung des anderen Teilnehmers an der Konversation erhalten hat, benachrichtigt [!INCLUDE[ssSB](../../includes/sssb-md.md)] den anderen Teilnehmer, dass die Konversation beendet wurde. Obwohl das Konversationshandle für die Konversation nicht mehr gültig ist, bleibt in diesem Fall der Konversationsendpunkt so lange aktiv, bis die Instanz, die als Host für den Remotedienst dient, die Nachricht anerkennt.  
  
 Wenn [!INCLUDE[ssSB](../../includes/sssb-md.md)] noch keine Nachricht über das Beenden des Dialogs oder eine Fehlermeldung für die Konversation verarbeitet hat, benachrichtigt [!INCLUDE[ssSB](../../includes/sssb-md.md)] die Remoteseite der Konversation, dass die Konversation beendet wurde. Die von [!INCLUDE[ssSB](../../includes/sssb-md.md)] an den Remotedienst gesendeten Nachrichten hängen von den angegebenen Optionen ab:  
  
-   Beendet die Konversation ohne Fehler und die Konversation mit der Remotedienst weiterhin aktiv ist, wird [!INCLUDE[ssSB](../../includes/sssb-md.md)] sendet eine Nachricht vom Typ `http://schemas.microsoft.com/SQL/ServiceBroker/EndDialog` an den Remotedienst. [!INCLUDE[ssSB](../../includes/sssb-md.md)] fügt diese Meldung der Übertragungswarteschlange in der Reihenfolge der Konversation hinzu. [!INCLUDE[ssSB](../../includes/sssb-md.md)] sendet alle Nachrichten für diese Konversation, die sich derzeit in der Übertragungswarteschlange befinden, bevor diese Nachricht gesendet wird.  
  
-   Wenn die Konversation mit einem Fehler beendet, und die Konversation mit dem Remotedienst weiterhin aktiv ist, wird [!INCLUDE[ssSB](../../includes/sssb-md.md)] sendet eine Nachricht vom Typ `http://schemas.microsoft.com/SQL/ServiceBroker/Error` an den Remotedienst. [!INCLUDE[ssSB](../../includes/sssb-md.md)] löscht alle anderen Nachrichten für diese Konversation, die sich derzeit in der Übertragungswarteschlange befinden.  
  
-   Die WITH CLEANUP-Klausel ermöglicht einem Datenbankadministrator das Entfernen von Konversationen, die nicht regulär abgeschlossen werden können. Mit dieser Option werden alle Nachrichten und Katalogsichteinträge für die Konversation entfernt. In diesem Fall empfängt die Remoteseite der Konversation keinen Hinweis auf das Ende der Konversation und empfängt möglicherweise Nachrichten nicht, die von einer Anwendung gesendet, jedoch noch nicht über das Netzwerk übermittelt wurden. Sie sollten diese Option nur dann auswählen, wenn die Konversation nicht regulär abgeschlossen werden kann.  
  
 Nach dem Ende einer Konversation verursacht eine [!INCLUDE[tsql](../../includes/tsql-md.md)]-SEND-Anweisung, die das Konversationshandle angibt, einen [!INCLUDE[tsql](../../includes/tsql-md.md)]-Fehler. Wenn Nachrichten für diese Konversation von der anderen Seite der Konversation eintreffen, werden diese von [!INCLUDE[ssSB](../../includes/sssb-md.md)] verworfen.  
  
 Wenn eine Konversation endet, während noch ungesendete Nachrichten für die Konversation beim Remotedienst vorliegen, löscht der Remotedienst die ungesendeten Nachrichten. Dies wird nicht als Fehler betrachtet, und der Remotedienst erhält keine Benachrichtigung, dass Nachrichten gelöscht wurden.  
  
 Fehlercodes in der WITH ERROR-Klausel müssen positive Zahlen sein. Negative Zahlen sind für Fehlermeldungen von [!INCLUDE[ssSB](../../includes/sssb-md.md)] vorbehalten.  
  
 END CONVERSATION ist in einer benutzerdefinierten Funktion ungültig.  
  
## <a name="permissions"></a>Berechtigungen  
 Zum Beenden einer aktiven Konversation muss der aktuelle Benutzer Besitzer der Konversation, Mitglied der festen Serverrolle sysadmin oder Mitglied der festen Datenbankrolle db_owner sein.  
  
 Ein Mitglied der festen Serverrolle sysadmin oder der festen Datenbankrolle db_owner kann mithilfe von WITH CLEANUP die Metadaten einer bereits abgeschlossenen Konversation entfernen.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-ending-a-conversation"></a>A. Beenden einer Konversation  
 Im folgenden Beispiel wird der von `@dialog_handle` angegebene Dialog beendet.  
  
```  
END CONVERSATION @dialog_handle ;  
```  
  
### <a name="b-ending-a-conversation-with-an-error"></a>B. Beenden einer Konversation mit einem Fehler  
 Im folgenden Beispiel wird der von `@dialog_handle` angegebene Dialog mit einem Fehler beendet, wenn die verarbeitende Anweisung einen Fehler meldet. Dieser Ansatz der Fehlerbehandlung ist stark vereinfachend und möglicherweise nicht für alle Anwendungen geeignet.  
  
```  
DECLARE @dialog_handle UNIQUEIDENTIFIER,  
        @ErrorSave INT,  
        @ErrorDesc NVARCHAR(100) ;  
BEGIN TRANSACTION ;  
  
<receive and process message>  
  
SET @ErrorSave = @@ERROR ;  
  
IF (@ErrorSave <> 0)  
  BEGIN  
      ROLLBACK TRANSACTION ;  
      SET @ErrorDesc = N'An error has occurred.' ;  
      END CONVERSATION @dialog_handle   
      WITH ERROR = @ErrorSave DESCRIPTION = @ErrorDesc ;  
  END  
ELSE  
  
COMMIT TRANSACTION ;  
```  
  
### <a name="c-cleaning-up-a-conversation-that-cannot-complete-normally"></a>C. Bereinigen einer Konversation, die nicht normal abgeschlossen werden kann  
 Im folgenden Beispiel wird der von `@dialog_handle` angegebene Dialog beendet. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entfernt alle Nachrichten unmittelbar aus der Dienstwarteschlange und der Übertragungswarteschlange ohne den Remotedienst zu benachrichtigen. Da Beenden eines Dialogs mit Cleanup den Remotedienst nicht benachrichtigt wird, Sie sollten nur verwenden, dies in Fällen, in denen der Remotedienst nicht verfügbar ist, erhalten eine **"EndDialog"** oder **Fehler** Nachricht.  
  
```  
END CONVERSATION @dialog_handle WITH CLEANUP ;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [BEGIN CONVERSATION TIMER &#40; Transact-SQL &#41;](../../t-sql/statements/begin-conversation-timer-transact-sql.md)   
 [BEGIN DIALOG CONVERSATION &#40; Transact-SQL &#41;](../../t-sql/statements/begin-dialog-conversation-transact-sql.md)   
 [sys.conversation_endpoints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-conversation-endpoints-transact-sql.md)  
  
  

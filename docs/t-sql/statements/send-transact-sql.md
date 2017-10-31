---
title: SEND (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SEND_ON_CONVERSATION_TSQL
- ON_CONVERSATION_TSQL
- SEND
- SEND_TSQL
- SEND ON CONVERSATION
- ON CONVERSATION
dev_langs:
- TSQL
helpviewer_keywords:
- conversations [Service Broker], message sending
- SEND statement
- messages [Service Broker], sending
- sending messages
ms.assetid: b6e66aeb-1714-4c2b-b7c2-d386d77b0d46
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b149c44df4fb417ed143147cd38b4ae838318ece
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="send-transact-sql"></a>SEND (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Sendet eine Nachricht mit einer oder mehreren vorhandenen Konversation.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SEND  
   ON CONVERSATION [(]conversation_handle [,.. @conversation_handle_n][)]  
   [ MESSAGE TYPE message_type_name ]  
   [ ( message_body_expression ) ]  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumente  
 IN der KONVERSATION *Conversation_handle [... @conversation_handle_n]*  
 Gibt die Konversationen an, zu der die Nachricht gehört. Die *Conversation_handle* muss eine gültige Konversations-ID enthalten. Das gleiche Konversationshandle kann jeweils nur einmal verwendet werden.  
  
 NACHRICHTENTYP *Message_type_name*  
 Gibt den Nachrichtentyp der gesendeten Nachricht an. Der Nachrichtentyp muss in den von den Konversationen verwendeten Dienstverträgen enthalten sein. Diese Verträge müssen das Senden des Nachrichtentyps von dieser Seite der Konversation zulassen. Die Zieldienste der Konversationen können beispielsweise nur Nachrichten senden, die im Vertrag als SENT BY TARGET oder SENT BY ANY angegeben sind. Wird diese Klausel ausgelassen, ist die Nachricht vom Nachrichtentyp DEFAULT.  
  
 *message_body_expression*  
 Stellt einen Ausdruck bereit, der den Nachrichtentext darstellt. Die *Message_body_expression* ist optional. Jedoch, wenn die *Message_body_expression* vorhanden ist der Ausdruck muss ein Typ, der konvertiert werden kann **varbinary(max)**. Der Ausdruck kann nicht NULL sein. Wird diese Klausel ausgelassen, ist der Nachrichtentext leer.  
  
## <a name="remarks"></a>Hinweise  
  
> [!IMPORTANT]  
>  Wenn es sich bei der SEND-Anweisung nicht um die erste Anweisung in einem Batch oder in einer gespeicherten Prozedur handelt, muss die vorhergehende Anweisung mit einem Semikolon (;) abgeschlossen werden.  
  
 Die SEND-Anweisung sendet eine Meldung von der Dienste an einem Ende einen oder mehrere [!INCLUDE[ssSB](../../includes/sssb-md.md)] Konversationen an die Dienste am anderen Ende dieser Konversationen. Mit der RECEIVE-Anweisung wird die gesendete Nachricht dann aus den Warteschlangen abgerufen, die den Zieldiensten zugeordnet sind.  
  
 Die in der ON CONVERSATION-Klausel angegebenen Konversationshandles stammt aus einer der folgenden Quellen:  
  
-   Beim Senden einer Nachricht, die keine Antwort auf eine von einem anderen Dienst empfangene Nachricht darstellt, verwenden Sie das Konversationshandle, das von der BEGIN DIALOG-Anweisung zurückgegeben wurde, mit der die Konversation erstellt wurde.  
  
-   Beim Senden einer Nachricht, die eine Antwort auf eine zuvor von einem anderen Dienst empfangene Nachricht darstellt, verwenden Sie das Konversationshandle, das von der RECEIVE-Anweisung zurückgegeben wurde, mit der die ursprüngliche Nachricht zurückgegeben wurde.  
  
 In vielen Fällen liegt der Code, der die SEND-Anweisung enthält, getrennt von dem Code vor, der die BEGIN DIALOG-Anweisung bzw. die RECEIVE–Anweisung enthält, welche das Konversationshandle liefert. In diesen Fällen muss das Konversationshandle als Datenelement der Statusinformationen an den Code übergeben werden, der die SEND-Anweisung enthält.  
  
 Nachrichten, die an Dienste in anderen Instanzen von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] gesendet werden, werden in einer Übertragungswarteschlange in der aktuellen Datenbank gespeichert, bis sie an die Dienstwarteschlangen in den Remoteinstanzen übertragen werden können. Nachrichten, die an Dienste in derselben Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] gesendet werden, werden direkt in den Warteschlangen abgelegt, die den betreffenden Diensten zugeordnet sind. Wenn eine Bedingung verhindert, dass der eine Nachricht direkt in der Ziel-Service-Warteschlange abgelegt wird, können in der Übertragungswarteschlange gespeichert werden, bis die Bedingung behoben ist. Dies kann beispielsweise auftreten, wenn bestimmte Typen von Fehlern vorliegen oder wenn die Zieldienstwarteschlange inaktiv ist. Sie können die **Sys. transmission_queue** -Systemsicht die in der Übertragungswarteschlange vorhandenen Nachrichten anzeigen.  
  
 Senden ist ein atomic-Anweisung, d. h., wenn eine SEND-Anweisung, die Senden einer Nachricht an mehrere Konversationen z. B. ein Fehler auftritt, da eine Konversation in einem fehlerhaften Zustand ist, keine Nachrichten in der Übertragungswarteschlange gespeichert oder werden in den zieldienstwarteschlangen abgelegt.  
  
 Mit Service Broker wird das Speichern und Übertragen von Nachrichten an mehrere Konversationen in der gleichen SEND-Anweisung optimiert.  
  
 Nachrichten in den Übertragungswarteschlangen für eine Instanz werden anhand folgender Kriterien der Reihe nach übertragen:  
  
-   Prioritätsstufe ihres zugeordneten Konversationsendpunkts  
  
-   Innerhalb der Prioritätsstufe die Sendereihenfolge in der Konversation  
  
 Prioritätsstufen, die in Konversationsprioritäten angegeben werden, gelten nur für Nachrichten in der Übertragungswarteschlange, wenn die HONOR_BROKER_PRIORITY-Datenbankoption auf ON festgelegt wird. Wenn HONOR_BROKER_PRIORITY auf OFF festgelegt wird, wird allen Nachrichten in der Übertragungswarteschlange für diese Datenbank die Standardprioritätsstufe 5 zugewiesen. Die Prioritätsstufe hat für diejenigen SEND-Anweisungen keine Bedeutung, mit denen Nachrichten direkt in eine Dienstwarteschlange in derselben Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] eingefügt werden.  
  
 Die einzelnen Konversationen, an die eine Nachricht gesendet werden soll, werden von der SEND-Anweisung separat gesperrt, damit die Nachrichten ordnungsgemäß zugestellt werden können.  
  
 SEND ist in einer benutzerdefinierten Funktion ungültig.  
  
## <a name="permissions"></a>Berechtigungen  
 Um eine Nachricht zu senden, muss der aktuelle Benutzer über die RECEIVE-Berechtigung für die Warteschlange aller Dienste verfügen, mit denen die Nachricht gesendet wird.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird ein Dialog gestartet und eine XML-Nachricht im Dialog gesendet. Zum Senden der Nachricht im Beispiel wird das XML-Objekt, das konvertiert **varbinary(max)**.  
  
```  
DECLARE @dialog_handle UNIQUEIDENTIFIER,  
        @ExpenseReport XML ;  
  
SET @ExpenseReport = < construct message as appropriate for the application > ;  
  
BEGIN DIALOG @dialog_handle  
FROM SERVICE [//Adventure-Works.com/Expenses/ExpenseClient]  
TO SERVICE '//Adventure-Works.com/Expenses'  
ON CONTRACT [//Adventure-Works.com/Expenses/ExpenseProcessing] ;  
  
SEND ON CONVERSATION @dialog_handle  
    MESSAGE TYPE [//Adventure-Works.com/Expenses/SubmitExpense]  
    (@ExpenseReport) ;  
```  
  
 Im folgenden Beispiel werden drei Dialoge gestartet, und es wird jeweils eine XML-Nachricht gesendet.  
  
```  
DECLARE @dialog_handle1 UNIQUEIDENTIFIER,  
        @dialog_handle2 UNIQUEIDENTIFIER,  
        @dialog_handle3 UNIQUEIDENTIFIER,  
        @OrderMsg XML ;  
  
SET @OrderMsg = < construct message as appropriate for the application > ;  
  
BEGIN DIALOG @dialog_handle1  
FROM SERVICE [//InitiatorDB/InitiatorService]  
TO SERVICE '//TargetDB1/TargetService’  
ON CONTRACT [//AllDBs/OrderProcessing] ;  
  
BEGIN DIALOG @dialog_handle2  
FROM SERVICE [//InitiatorDB/InitiatorService]  
TO SERVICE '//TargetDB2/TargetService’  
ON CONTRACT [//AllDBs/OrderProcessing] ;  
  
BEGIN DIALOG @dialog_handle3  
FROM SERVICE [//InitiatorDB/InitiatorService]  
TO SERVICE '//TargetDB3/TargetService’  
ON CONTRACT [//AllDBs/OrderProcessing] ;  
  
SEND ON CONVERSATION (@dialog_handle1, @dialog_handle2, @dialog_handle3)  
    MESSAGE TYPE [//AllDBs/OrderMsg]  
    (@OrderMsg) ;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [BEGIN DIALOG CONVERSATION &#40; Transact-SQL &#41;](../../t-sql/statements/begin-dialog-conversation-transact-sql.md)   
 [END CONVERSATION-Anweisung &#40; Transact-SQL &#41;](../../t-sql/statements/end-conversation-transact-sql.md)   
 [Empfangen von &#40; Transact-SQL &#41;](../../t-sql/statements/receive-transact-sql.md)   
 [Sys. transmission_queue &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-transmission-queue-transact-sql.md)  
  
  


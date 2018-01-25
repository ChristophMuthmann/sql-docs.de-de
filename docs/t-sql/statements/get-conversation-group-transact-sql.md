---
title: GET CONVERSATION GROUP (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- GET
- CONVERSATION_GROUP_TSQL
- GET_TSQL
- GET_CONVERSATION_GROUP_TSQL
- GET CONVERSATION GROUP
- CONVERSATION GROUP
- GET CONVERSATION
- GET_CONVERSATION_TSQL
dev_langs: TSQL
helpviewer_keywords:
- GET CONVERSATION GROUP statement
- conversations [Service Broker], groups
ms.assetid: 4da8a855-33c0-43b2-a49d-527487cb3b5c
caps.latest.revision: "39"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 04035a9ccbe406b9fa50b5003ab109c3f1ff997d
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="get-conversation-group-transact-sql"></a>GET CONVERSATION GROUP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt den Bezeichner der Konversationsgruppe für die nächste zu empfangende Nachricht zurück und sperrt die Konversationsgruppe für die Konversation, die die Nachricht enthält. Der Konversationsgruppenbezeichner kann zum Abrufen der Informationen zum Konversationsstatus vor dem Abrufen der eigentlichen Nachricht verwendet werden.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
[ WAITFOR ( ]  
   GET CONVERSATION GROUP @conversation_group_id  
      FROM <queue>  
[ ) ] [ , TIMEOUT timeout ]  
[ ; ]  
  
<queue> ::=  
{  
    [ database_name . [ schema_name ] . | schema_name . ] queue_name  
}  
```  
  
## <a name="arguments"></a>Argumente  
 WAITFOR  
 Gibt an, dass die GET CONVERSATION GROUP-Anweisung darauf wartet, dass eine Nachricht in der Warteschlange eintrifft, wenn zurzeit keine Nachrichten vorhanden sind.  
  
 *@conversation_group_id*  
 Eine Variable zum Speichern der Konversationsgruppen-ID, die von der GET CONVERSATION GROUP-Anweisung zurückgegeben wird. Die Variable muss vom Typ **"uniqueidentifier"**. Sind keine Konversationsgruppen verfügbar, wird die Variable auf NULL festgelegt.  
  
 FROM  
 Gibt die Warteschlange an, aus der die Konversationsgruppe abgerufen werden soll.  
  
 *database_name*  
 Der Name der Datenbank, die die Warteschlange enthält, aus der die Konversationsgruppe abgerufen werden soll. Wenn kein *Database_name* angegeben ist, wird der Standardwert ist der aktuellen Datenbank.  
  
 *schema_name*  
 Der Name des Schemas, das die Warteschlange besitzt, aus der die Konversationsgruppe abgerufen werden soll. Wenn kein *Schema_name* angegeben ist, wird der Standardwert ist das Standardschema für den aktuellen Benutzer.  
  
 *queue_name*  
 Der Name der Warteschlange, aus der die Konversationsgruppe abgerufen werden soll.  
  
 TIMEOUT *Timeout*  
 Gibt die Zeitdauer (in Millisekunden) an, die Service Broker auf das Eintreffen einer Nachricht in der Warteschlange wartet. Diese Klausel darf nur zusammen mit der WAITFOR-Klausel verwendet werden. Wenn eine Anweisung, die WAITFOR verwendet diese Klausel nicht enthalten ist oder die *Timeout* ist-1, die Wartezeit ist unbegrenzt. Wenn es sich bei Ablauf des Timeouts legt GET CONVERSATION GROUP die  *@conversation_group_id*  -Variable auf NULL.  
  
## <a name="remarks"></a>Hinweise  
  
> [!IMPORTANT]  
>  Wenn die GET CONVERSATION GROUP-Anweisung nicht die erste Anweisung in einem Batch oder einer gespeicherten Prozedur ist, muss die vorhergehende Anweisung mit einem Semikolon abgeschlossen werden (**;**), wird die [!INCLUDE[tsql](../../includes/tsql-md.md)] anweisungsabschlusszeichen.  
  
 Steht die in der Warteschlange angegebene GET CONVERSATION GROUP-Anweisung nicht zur Verfügung, wird für die Anweisung ein [!INCLUDE[tsql](../../includes/tsql-md.md)]-Fehler erzeugt.  
  
 Diese Anweisung gibt die nächste Konversationsgruppe zurück, wobei Folgendes gilt:  
  
-   Die Konversationsgruppe kann erfolgreich gesperrt werden.  
  
-   Die Konversationsgruppe verfügt in der Warteschlange über Nachrichten.  
  
-   Die Konversationsgruppe weist von allen Konversationsgruppen, die die zuvor genannten Kriterien erfüllen, die höchste Prioritätsebene auf. Die Prioritätsebene einer Konversationsgruppe ist die höchste Prioritätsebene, die einer Konversation zugeordnet ist, die der Gruppe angehört und in der Warteschlange Nachrichten aufweist.  
  
 Aufeinander folgende Aufrufe von GET CONVERSATION GROUP innerhalb derselben Transaktion können mehr als eine Konversationsgruppe sperren. Steht keine Konversationsgruppe zur Verfügung, gibt die Anweisung NULL als Bezeichner der Konversationsgruppe zurück.  
  
 Wenn die WAITFOR-Klausel angegeben wird, wartet die Anweisung bis zum Ablauf des angegebenen Timeouts oder so lange, bis eine Konversationsgruppe verfügbar ist. Wird die Warteschlange gelöscht, während die Anweisung wartet, gibt die Anweisung sofort einen Fehler zurück.  
  
 GET CONVERSATION GROUP ist in einer benutzerdefinierten Funktion ungültig.  
  
## <a name="permissions"></a>Berechtigungen  
 Zum Abrufen des Bezeichners einer Konversationsgruppe aus einer Warteschlange benötigt der aktuelle Benutzer die RECEIVE-Berechtigung für die Warteschlange.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-getting-a-conversation-group-waiting-indefinitely"></a>A. Abrufen einer Konversationsgruppe ohne Begrenzung der Wartezeit  
 Im folgenden Beispiel wird `@conversation_group_id` auf den Konversationsgruppenbezeichner für die nächste verfügbare Nachricht in `ExpenseQueue` festgelegt. Der Befehl wartet so lange, bis eine Nachricht verfügbar ist.  
  
```  
DECLARE @conversation_group_id UNIQUEIDENTIFIER ;  
  
WAITFOR (  
 GET CONVERSATION GROUP @conversation_group_id  
     FROM ExpenseQueue  
) ;  
```  
  
### <a name="b-getting-a-conversation-group-waiting-one-minute"></a>B. Abrufen einer Konversationsgruppe mit einer Wartezeit von einer Minute  
 Im folgenden Beispiel wird `@conversation_group_id` auf den Konversationsgruppenbezeichner für die nächste verfügbare Nachricht in `ExpenseQueue` festgelegt. Ist keine Nachricht innerhalb einer Minute verfügbar, wird GET CONVERSATION GROUP ohne Änderung des Werts von `@conversation_group_id` zurückgegeben.  
  
```  
DECLARE @conversation_group_id UNIQUEIDENTIFIER  
  
WAITFOR (  
    GET CONVERSATION GROUP @conversation_group_id   
    FROM ExpenseQueue ),  
TIMEOUT 60000 ;  
```  
  
### <a name="c-getting-a-conversation-group-returning-immediately"></a>C. Abrufen einer Konversationsgruppe mit unmittelbarer Rückgabe  
 Im folgenden Beispiel wird `@conversation_group_id` auf den Konversationsgruppenbezeichner für die nächste verfügbare Nachricht in `ExpenseQueue` festgelegt. Wenn keine Nachricht verfügbar ist, wird `GET CONVERSATION GROUP` sofort ohne Änderung des Werts von `@conversation_group_id` zurückgegeben.  
  
```  
DECLARE @conversation_group_id UNIQUEIDENTIFIER ;  
  
GET CONVERSATION GROUP @conversation_group_id  
FROM AdventureWorks.dbo.ExpenseQueue ;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [BEGIN DIALOG CONVERSATION &#40; Transact-SQL &#41;](../../t-sql/statements/begin-dialog-conversation-transact-sql.md)   
 [MOVE CONVERSATION &#40; Transact-SQL &#41;](../../t-sql/statements/move-conversation-transact-sql.md)  
  
  

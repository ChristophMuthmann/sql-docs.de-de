---
title: MOVE CONVERSATION (Transact-SQL) | Microsoft Docs
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
- MOVE_CONVERSATION_TSQL
- MOVE CONVERSATION
- MOVE_TSQL
- MOVE
dev_langs: TSQL
helpviewer_keywords:
- moving conversations
- MOVE CONVERSATION statement
- relocating conversations
- conversations [Service Broker], groups
- conversations [Service Broker], moving
ms.assetid: 1da4d2c9-e767-434e-b49b-615711a7f626
caps.latest.revision: "28"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cd8c5e548bf45fe4a2fc6bf0638ebb5282981263
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="move-conversation-transact-sql"></a>MOVE CONVERSATION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Verschiebt eine Konversation in eine andere Konversationsgruppe.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
MOVE CONVERSATION conversation_handle  
   TO conversation_group_id  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumente  
 *conversation_handle*  
 Eine Variable oder Konstante mit dem Handle der Konversation, die verschoben werden soll. *Conversation_handle* muss vom Typ **"uniqueidentifier"**.  
  
 UM *Conversation_group_id*  
 Eine Variable oder Konstante mit dem Bezeichner der Konversationsgruppe, in die die Konversation verschoben werden soll. *Conversation_group_id* muss vom Typ **"uniqueidentifier"**.  
  
## <a name="remarks"></a>Hinweise  
 Die MOVE CONVERSATION-Anweisung geht die Konversation, die vom angegebenen *Conversation_handle* auf die identifizierte Konversationsgruppe *Conversation_group_id*. Dialoge können nur zwischen Konversationsgruppen umgeleitet werden, die derselben Warteschlange zugeordnet sind.  
  
> [!IMPORTANT]  
>  Wenn die MOVE CONVERSATION-Anweisung nicht die erste Anweisung in einem Batch oder einer gespeicherten Prozedur ist, muss die vorhergehende Anweisung mit einem Semikolon abgeschlossen werden (**;**), wird die [!INCLUDE[tsql](../../includes/tsql-md.md)] anweisungsabschlusszeichen.  
  
 Die MOVE CONVERSATION-Anweisung sperrt die Konversationsgruppe zugeordnete *Conversation_handle* und der Konversationsgruppe gemäß *Conversation_group_id* bis die Transaktion mit der Anweisung ein Commit oder Rollback.  
  
 MOVE CONVERSATION ist in einer benutzerdefinierten Funktion ungültig.  
  
## <a name="permissions"></a>Berechtigungen  
 Zum Verschieben einer Konversation muss der aktuelle Benutzer Besitzer der Konversation und der Konversationsgruppe oder Mitglied der festen Serverrolle sysadmin oder Mitglied der festen Datenbankrolle db_owner sein.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine Konversation in eine andere Konversationsgruppe verschoben.  
  
```  
DECLARE @conversation_handle UNIQUEIDENTIFIER,  
        @conversation_group_id UNIQUEIDENTIFIER ;  
  
SET @conversation_handle =  
    <retrieve conversation handle from database> ;  
SET @conversation_group_id =  
    <retrieve conversation group ID from database> ;  
  
MOVE CONVERSATION @conversation_handle TO @conversation_group_id ;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [BEGIN DIALOG CONVERSATION &#40; Transact-SQL &#41;](../../t-sql/statements/begin-dialog-conversation-transact-sql.md)   
 [GET CONVERSATION GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/get-conversation-group-transact-sql.md)   
 [END CONVERSATION &#40;Transact-SQL&#41;](../../t-sql/statements/end-conversation-transact-sql.md)   
 [sys.conversation_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-conversation-groups-transact-sql.md)   
 [sys.conversation_endpoints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-conversation-endpoints-transact-sql.md)  
  
  

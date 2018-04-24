---
title: MOVE CONVERSATION (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/26/2017
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
- MOVE_CONVERSATION_TSQL
- MOVE CONVERSATION
- MOVE_TSQL
- MOVE
dev_langs:
- TSQL
helpviewer_keywords:
- moving conversations
- MOVE CONVERSATION statement
- relocating conversations
- conversations [Service Broker], groups
- conversations [Service Broker], moving
ms.assetid: 1da4d2c9-e767-434e-b49b-615711a7f626
caps.latest.revision: 28
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 250abee7aad3195a87e04512b63a0d45f32fcb89
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
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
 Eine Variable oder Konstante mit dem Handle der Konversation, die verschoben werden soll. *conversation_handle* muss dem Typ **uniqueidentifier** entsprechen.  
  
 TO *conversation_group_id*  
 Eine Variable oder Konstante mit dem Bezeichner der Konversationsgruppe, in die die Konversation verschoben werden soll. *conversation_group_id* muss dem Typ **uniqueidentifier** entsprechen.  
  
## <a name="remarks"></a>Remarks  
 Mit der MOVE CONVERSATION-Anweisung wird die durch *conversation_handle* angegebene Konversation in die durch *conversation_group_id* identifizierte Konversationsgruppe verschoben. Dialoge können nur zwischen Konversationsgruppen umgeleitet werden, die derselben Warteschlange zugeordnet sind.  
  
> [!IMPORTANT]  
>  Falls die MOVE CONVERSATION-Anweisung nicht die erste Anweisung in einem Batch oder einer gespeicherten Prozedur ist, muss die vorherige Anweisung mit einem Semikolon (**;**) enden, dem Abschlusszeichen für [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen.  
  
 Mit der MOVE CONVERSATION-Anweisung werden die *conversation_handle* zugeordnete Konversationsgruppe sowie die durch *conversation_group_id* angegebene Konversationsgruppe gesperrt, bis ein Commit oder ein Rollback für die Transaktion, die die Anweisung enthält, ausgeführt wird.  
  
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
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [BEGIN DIALOG CONVERSATION &#40;Transact-SQL&#41;](../../t-sql/statements/begin-dialog-conversation-transact-sql.md)   
 [GET CONVERSATION GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/get-conversation-group-transact-sql.md)   
 [END CONVERSATION &#40;Transact-SQL&#41;](../../t-sql/statements/end-conversation-transact-sql.md)   
 [sys.conversation_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-conversation-groups-transact-sql.md)   
 [sys.conversation_endpoints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-conversation-endpoints-transact-sql.md)  
  
  

---
title: DROP BROKER PRIORITY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
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
- DROP_BROKER_PRIORITY_TSQL
- DROP BROKER PRIORITY
dev_langs: TSQL
helpviewer_keywords: DROP BROKER PRIORITY statement
ms.assetid: 09ee6c5b-af94-4a4b-a0e2-f9eac50e43aa
caps.latest.revision: "15"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3724d9ad6724ef35b4514ab515b42a56ff9e8d43
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="drop-broker-priority-transact-sql"></a>DROP BROKER PRIORITY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Entfernt eine Konversationspriorität aus der aktuellen Datenbank.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
DROP BROKER PRIORITY ConversationPriorityName  
[;]  
```  
  
## <a name="arguments"></a>Argumente  
 *ConversationPriorityName*  
 Gibt den Namen der zu entfernenden Konversationspriorität an.  
  
## <a name="remarks"></a>Hinweise  
 Wenn Sie eine Konversationspriorität löschen, werden vorhandene Konversationen mit den Prioritätsebenen fortgesetzt, die von der Konversationspriorität zugewiesen wurden.  
  
## <a name="permissions"></a>Berechtigungen  
 Die Berechtigung zum Erstellen einer Konversationspriorität erhalten standardmäßig die Mitglieder der festen Datenbankrolle db_ddladmin oder db_owner und die feste Serverrolle sysadmin. Erfordert die ALTER-Berechtigung für die Datenbank.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die Konversationspriorität mit dem Namen `InitiatorAToTargetPriority`gelöscht.  
  
```  
DROP BROKER PRIORITY InitiatorAToTargetPriority;  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER BROKER PRIORITY &#40; Transact-SQL &#41;](../../t-sql/statements/alter-broker-priority-transact-sql.md)   
 [Erstellen Sie die BROKERPRIORITÄT &#40; Transact-SQL &#41;](../../t-sql/statements/create-broker-priority-transact-sql.md)   
 [Sys. conversation_priorities &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-conversation-priorities-transact-sql.md)  
  
  

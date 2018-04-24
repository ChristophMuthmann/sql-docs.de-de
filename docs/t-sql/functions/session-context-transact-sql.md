---
title: SESSION_CONTEXT (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/22/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- SESSION_CONTEXT
- sys.SESSION_CONTEXT
- SESSION_CONTEXT_TSQL
- sys.SESSION_CONTEXT_TSQL
helpviewer_keywords:
- SESSION_CONTEXT function
ms.assetid: b6bdbc54-331a-43cc-ab3d-3872d6a12100
caps.latest.revision: 11
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 9f27e101de22ee92b912febfbb33c907a62aae4f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sessioncontext-transact-sql"></a>SESSION_CONTEXT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Gibt den Wert des angegebenen Schlüssels im aktuellen Sitzungskontext zurück. Der Wert wird mithilfe der [sp_set_session_context &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-set-session-context-transact-sql.md)-Prozedur festgelegt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
SESSION_CONTEXT(N'key')  
```  
  
## <a name="arguments"></a>Argumente  
 'key'  
 Der Schlüssel (vom Typ „sysname“) des Werts, der abgerufen wird.  
  
## <a name="return-type"></a>Rückgabetyp  
 **sql_variant**  
  
## <a name="return-value"></a>Rückgabewert  
 Der Wert, der dem angegebenen Schlüssel im Sitzungskontext zugeordnet ist oder NULL, wenn für diesen Schlüssel kein Wert festgelegt wurde.  
  
## <a name="permissions"></a>Berechtigungen  
 Jeder Benutzer kann den Sitzungskontext für seine Sitzung lesen.  
  
## <a name="remarks"></a>Remarks  
 Das MARS-Verhalten von SESSION_CONTEXT ist dem von CONTEXT_INFO ähnlich. Wenn ein MARS-Batch ein Schlüssel-Wert-Paar festlegt, wird der neue Wert nicht in anderen MARS-Batches auf derselben Verbindung zurückgegeben, es sei denn, sie beginnen nach dem Batch, der den neuen Wert festgelegt hat. Wenn MARS-Batches auf einer Verbindung aktiv sind, können Werte nicht als „read_only“ festgelegt werden. Dadurch werden Racebedingungen und nicht deterministische Funktionen darüber vermieden, welcher Wert „gewinnt“.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden, einfachen Beispiel wird der Sitzungkontextwert für den Schlüssel `user_id` auf 4 festgelegt und der Wert dann mithilfe der **SESSION_CONTEXT**-Funktion abgerufen.  
  
```  
EXEC sp_set_session_context 'user_id', 4;  
SELECT SESSION_CONTEXT(N'user_id');  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [sp_set_session_context &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-set-session-context-transact-sql.md)   
 [CURRENT_TRANSACTION_ID &#40;Transact-SQL&#41;](../../t-sql/functions/current-transaction-id-transact-sql.md)   
 [Sicherheit auf Zeilenebene](../../relational-databases/security/row-level-security.md)   
 [CONTEXT_INFO  &#40;Transact-SQL&#41;](../../t-sql/functions/context-info-transact-sql.md)   
 [SET CONTEXT_INFO &#40;Transact-SQL&#41;](../../t-sql/statements/set-context-info-transact-sql.md)  
  
  

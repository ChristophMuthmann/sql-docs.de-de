---
title: SESSION_CONTEXT (Transact-SQL) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 06/22/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 23eea4b51009272ae06987ee2e9c1730750b3d6d
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="sessioncontext-transact-sql"></a>SESSION_CONTEXT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Gibt den Wert des angegebenen Schlüssels in den Kontext der aktuellen Sitzung zurück. Der Wert wird festgelegt, mit der [Sp_set_session_context &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-set-session-context-transact-sql.md) Prozedur.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
SESSION_CONTEXT(N'key')  
```  
  
## <a name="arguments"></a>Argumente  
 "Key"  
 Der Schlüssel (Typ Sysname) der Wert abgerufen wird.  
  
## <a name="return-type"></a>Rückgabetyp  
 **sql_variant**  
  
## <a name="return-value"></a>Rückgabewert  
 Der Wert verknüpft sind mit dem angegebenen Schlüssel in der Sitzungskontext oder NULL, wenn kein Wert für diesen Schlüssel festgelegt wurde.  
  
## <a name="permissions"></a>Berechtigungen  
 Jeder Benutzer kann Sitzungskontext für ihre Sitzung gelesen werden.  
  
## <a name="remarks"></a>Hinweise  
 SESSION_CONTEXT der MARS-Verhalten ähnelt dem CONTEXT_INFO. Wenn ein MARS-Batch ein Schlüssel-Wert-Paar festlegt, wird der neue Wert nicht in anderen MARS-Batches über dieselbe Verbindung zurückgegeben werden, wenn die Aufträge gestartet wurden, nach Abschluss des Batches, der den neuen Wert festgelegt. Falls mehrere MARS-Batches für eine Verbindung aktiv sind, können die Werte als "Read_only." festgelegt werden Dies verhindert, dass Racebedingungen und Nichtdeterminismus über den Wert "Wins".  
  
## <a name="examples"></a>Beispiele  
 Das folgende einfache Beispiel legt die sitzungskontextwert für Schlüssel `user_id` , 4, und klicken Sie dann mithilfe der **SESSION_CONTEXT** Funktion zum Abrufen des Werts.  
  
```  
EXEC sp_set_session_context 'user_id', 4;  
SELECT SESSION_CONTEXT(N'user_id');  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sp_set_session_context &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-set-session-context-transact-sql.md)   
 [CURRENT_TRANSACTION_ID &#40; Transact-SQL &#41;](../../t-sql/functions/current-transaction-id-transact-sql.md)   
 [Sicherheit auf Zeilenebene](../../relational-databases/security/row-level-security.md)   
 [CONTEXT_INFO &#40; Transact-SQL &#41;](../../t-sql/functions/context-info-transact-sql.md)   
 [SET CONTEXT_INFO &#40; Transact-SQL &#41;](../../t-sql/statements/set-context-info-transact-sql.md)  
  
  


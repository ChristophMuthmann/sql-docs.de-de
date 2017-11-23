---
title: DROP MESSAGE TYPE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
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
- DROP_MESSAGE_TYPE_TSQL
- DROP MESSAGE TYPE
dev_langs: TSQL
helpviewer_keywords:
- message types [Service Broker], removing
- deleting message types
- dropping message types
- DROP MESSAGE TYPE statement
- removing message types
ms.assetid: 805e8ad5-8a93-49f0-88e5-e6fca8814dd5
caps.latest.revision: "24"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8fca6b9d58d281d246fe441ff9586cad83a39392
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="drop-message-type-transact-sql"></a>DROP MESSAGE TYPE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Löscht einen vorhandenen Nachrichtentyp.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
DROP MESSAGE TYPE message_type_name  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumente  
 *message_type_name*  
 Der Name des Nachrichtentyps, der gelöscht werden soll. Server-, Datenbank- und Schemaname können nicht angegeben werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Standardmäßig verfügen Mitglieder der festen Datenbankrollen db_ddladmin oder db_owner sowie Mitglieder der festen Serverrolle sysadmin über die Berechtigung zum Löschen eines Nachrichtentyps.  
  
## <a name="remarks"></a>Hinweise  
 Sie können einen Nachrichtentyp nicht löschen, wenn sich Verträge auf diesen Nachrichtentyp beziehen.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird der Nachrichtentyp `//Adventure-Works.com/Expenses/SubmitExpense` aus der Datenbank gelöscht.  
  
```  
DROP MESSAGE TYPE [//Adventure-Works.com/Expenses/SubmitExpense] ;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER MESSAGE TYPE &#40; Transact-SQL &#41;](../../t-sql/statements/alter-message-type-transact-sql.md)   
 [Erstellen Sie NACHRICHTENTYP &#40; Transact-SQL &#41;](../../t-sql/statements/create-message-type-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

---
title: DROP QUEUE (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/06/2017
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
- DROP QUEUE
- DROP_QUEUE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dropping queues
- queues [Service Broker], removing
- deleting queues
- DROP QUEUE statement
- removing queues
ms.assetid: fd866520-ca00-477d-b2e9-0110e9610ed4
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3be4f36943d6e25bb520a28593d009e7a8373c48
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="drop-queue-transact-sql"></a>DROP QUEUE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Löscht eine vorhandene Warteschlange.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
DROP QUEUE <object>  
[ ; ]  
  
<object> ::=  
{  
    [ database_name . [ schema_name ] . | schema_name . ]  
        queue_name  
}  
```  
  
## <a name="arguments"></a>Argumente  
 *database_name*  
 Der Name der Datenbank, die die zu löschende Warteschlange enthält. Wenn *database_name* nicht bereitgestellt wird, wird standardmäßig die aktuelle Datenbank verwendet.  
  
 *schema_name (Objekt)*  
 Der Name des Schemas, das die zu löschende Warteschlange besitzt. Wenn *schema_name* nicht angegeben wird, wird standardmäßig das Standardschema für den aktuellen Benutzer verwendet.  
  
 *queue_name*  
 Der Name der zu löschenden Warteschlange.  
  
## <a name="remarks"></a>Remarks  
 Sie können eine Warteschlange nicht löschen, wenn Dienste auf sie verweisen.  
  
## <a name="permissions"></a>Berechtigungen  
 Standardmäßig verfügen der Besitzer der Warteschlange, Mitglieder der festen Datenbankrollen **db_ddladmin** oder **db_owner** und Mitglieder der festen Datenbankrolle **sysadmin** über die Berechtigung zum Löschen einer Warteschlange.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die Warteschlange **ExpenseQueue** aus der aktuellen Datenbank gelöscht.  
  
```  
DROP QUEUE ExpenseQueue ;  
  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [CREATE QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/create-queue-transact-sql.md)   
 [ALTER QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-queue-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

---
title: DROP WORKLOAD GROUP (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
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
- DROP_WORKLOAD_GROUP_TSQL
- DROP WORKLOAD GROUP
dev_langs:
- TSQL
helpviewer_keywords:
- DROP WORKLOAD GROUP statement
ms.assetid: 1cd68450-5b58-4106-a2bc-54197ced8616
caps.latest.revision: 23
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ee8b62303440dd47169d8063f39571a23834ad7e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="drop-workload-group-transact-sql"></a>DROP WORKLOAD GROUP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Löscht eine vorhandene benutzerdefinierte Arbeitsauslastungsgruppe der Ressourcenkontrolle.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
DROP WORKLOAD GROUP group_name  
[;]  
```  
  
## <a name="arguments"></a>Argumente  
 *group_name*  
 Der Name einer vorhandenen benutzerdefinierten Arbeitsauslastungsgruppe.  
  
## <a name="remarks"></a>Remarks  
 Die DROP WORKLOAD GROUP-Anweisung ist für die internen oder Standard-Gruppen der Ressourcenkontrolle nicht zulässig.  
  
 Sie sollten bei der Ausführung von DDL-Anweisungen mit dem Status der Ressourcenkontrolle vertraut sein. Weitere Informationen finden Sie unter [Resource Governor](../../relational-databases/resource-governor/resource-governor.md).  
  
 Falls eine Arbeitsauslastungsgruppe aktive Sitzungen enthält, tritt beim Löschen bzw. Verschieben der Arbeitsauslastungsgruppe in einen anderen Ressourcenpool ein Fehler auf, wenn Sie die ALTER RESOURCE GOVERNOR RECONFIGURE-Anweisung aufrufen, um die Änderung zu übernehmen. Führen Sie eine der folgenden Aktionen aus, um dieses Problem zu umgehen:  
  
-   Warten Sie, bis die Verbindungen für alle Sitzungen der entsprechenden Gruppe geschlossen wurden, und führen Sie dann die ALTER RESOURCE GOVERNOR RECONFIGURE-Anweisung noch einmal aus.  
  
-   Stoppen Sie die Sitzungen in der betreffenden Gruppe explizit mit dem KILL-Befehl, und führen Sie die ALTER RESOURCE GOVERNOR RECONFIGURE-Anweisung noch einmal aus.  
  
-   Starten Sie den Server neu. Nach Abschluss des Neustarts wird die gelöschte Gruppe nicht erstellt und die neue Ressourcenpoolzuordnung wird von einer verschobenen Gruppe verwendet.  
  
-   Falls Sie nach Ausgabe der DROP WORKLOAD GROUP-Anweisung beschließen, dass Sie keine Sitzungen explizit stoppen möchten, um die Änderung zu übernehmen, können Sie die Gruppe mit dem gleichen Namen, den sie vor Ausgabe der DROP-Anweisung hatte, neu erstellen und dann in den ursprünglichen Ressourcenpool verschieben. Um die Änderungen zu übernehmen, führen Sie die ALTER RESOURCE GOVERNOR RECONFIGURE-Anweisung aus.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CONTROL SERVER-Berechtigung.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel löscht die Arbeitsauslastungsgruppe namens `adhoc`.  
  
```  
DROP WORKLOAD GROUP adhoc;  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)   
 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)   
 [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md)   
 [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)   
 [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)   
 [DROP RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  

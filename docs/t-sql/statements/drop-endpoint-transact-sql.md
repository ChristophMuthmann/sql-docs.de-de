---
title: DROP ENDPOINT (Transact-SQL) | Microsoft Docs
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
- DROP_ENDPOINT_TSQL
- DROP ENDPOINT
dev_langs: TSQL
helpviewer_keywords:
- removing endpoints
- endpoints [SQL Server], removing
- deleting endpoints
- DROP ENDPOINT statement
- dropping endpoints
ms.assetid: 6aca7412-66a5-4fa4-86b2-061512ff2080
caps.latest.revision: "32"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a5f08fbbb767d5272d0cb5999c68359eaab7fb7b
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="drop-endpoint-transact-sql"></a>DROP ENDPOINT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Löscht einen vorhandenen Endpunkt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
DROP ENDPOINT endPointName  
```  
  
## <a name="arguments"></a>Argumente  
 *endPointName*  
 Der Name des Endpunkts, der entfernt werden soll.  
  
## <a name="remarks"></a>Hinweise  
 ENDPOINT DDL-Anweisungen können nicht innerhalb einer Benutzertransaktion ausgeführt werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Benutzer muss ein Mitglied der **Sysadmin** festen Serverrolle, der Besitzer des Endpunktes sein, oder die CONTROL-Berechtigung für den Endpunkt erteilt worden.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird ein zuvor erstellter Endpunkt namens `sql_endpoint` entfernt.  
  
```  
DROP ENDPOINT sql_endpoint;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md)   
 [ALTER ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-endpoint-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

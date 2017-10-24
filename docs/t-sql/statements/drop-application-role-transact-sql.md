---
title: DROP APPLICATION ROLE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_APPLICATION_ROLE_TSQL
- DROP APPLICATION ROLE
dev_langs:
- TSQL
helpviewer_keywords:
- dropping application roles
- deleting application roles
- removing application roles
- application roles [SQL Server], removing
- DROP APPLICATION ROLE statement
ms.assetid: 44121ee7-ef40-405d-b03b-f8ddb4e3c559
caps.latest.revision: 24
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 326c0bb53e995aeacb807a91b83d69f59d034d2f
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="drop-application-role-transact-sql"></a>DROP APPLICATION ROLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Entfernt eine Anwendungsrolle aus der aktuellen Datenbank  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
DROP APPLICATION ROLE rolename  
```  
  
## <a name="arguments"></a>Argumente  
 *roleName*  
 Gibt den Namen der zu löschenden Anwendungsrolle an.  
  
## <a name="remarks"></a>Hinweise  
 Wenn die Anwendungsrolle sicherbare Elemente besitzt, kann sie nicht gelöscht werden. Vor dem Löschen einer Anwendungsrolle, die sicherungsfähige Elemente besitzt, muss zunächst der Besitz an den sicherungsfähigen Elementen übertragen werden, oder sie müssen gelöscht werden.  
  
> [!CAUTION]  
>  [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die ALTER ANY APPLICATION ROLE-Berechtigung in der Datenbank.  
  
## <a name="examples"></a>Beispiele  
 Löschen Sie die Anwendungsrolle "weekly_ledger" aus der Datenbank.  
  
```  
DROP APPLICATION ROLE weekly_ledger;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Anwendungsrollen](../../relational-databases/security/authentication-access/application-roles.md)   
 [Erstellen Sie APPLICATION ROLE &#40; Transact-SQL &#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [ALTER APPLICATION ROLE &#40; Transact-SQL &#41;](../../t-sql/statements/alter-application-role-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  


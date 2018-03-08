---
title: Sp_dropsrvrolemember (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_dropsrvrolemember
- sp_dropsrvrolemember_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_dropsrvrolemember
ms.assetid: 7be99181-d221-49d0-9cb2-c930d8c044a0
caps.latest.revision: "20"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dc66cffd56d8eebf31f50ce784be407292261b89
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="spdropsrvrolemember-transact-sql"></a>sp_dropsrvrolemember (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Entfernt einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen oder einen Windows-Benutzer bzw. eine -Gruppe aus einer festen Serverrolle.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Verwendung [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md) stattdessen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_dropsrvrolemember [ @loginame = ] 'login' , [ @rolename = ] 'role'  
```  
  
## <a name="arguments"></a>Argumente  
 [ @loginame  **=**  ] **"***Anmeldung***"**  
 Der Name einer Anmeldung, die aus der festen Serverrolle entfernt werden soll. *login* ist vom Datentyp **sysname**und hat keinen Standardwert. *Anmeldung* muss vorhanden sein.  
  
 [ @rolename  **=**  ] **"***Rolle***"**  
 Der Name einer Serverrolle. *role* ist vom Datentyp **sysname**und hat den Standardwert NULL. *Rolle* muss eines der folgenden Werte sein:  
  
-   sysadmin  
  
-   securityadmin  
  
-   serveradmin  
  
-   setupadmin  
  
-   processadmin  
  
-   diskadmin  
  
-   dbcreator  
  
-   bulkadmin 
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 Nur Sp_dropsrvrolemember kann verwendet werden, um eine Anmeldung aus einer festen Serverrolle zu entfernen. Verwenden Sie ' sp_droprolemember ', um ein Mitglied aus einer Datenbankrolle zu entfernen.  
  
 Die Anmeldenamens "sa" kann nicht aus einer festen Serverrolle entfernt werden.  
  
 Sp_dropsrvrolemember kann nicht innerhalb einer benutzerdefinierten Transaktion ausgeführt werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der festen Sysadmin-Serverrolle, oder beide ALTER ANY LOGIN-Berechtigung auf dem Server und die Mitgliedschaft in der Rolle, von der das Element abgelegt wird.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird der Anmeldename `JackO` aus der festen Serverrolle `sysadmin` entfernt.  
  
```  
EXEC sp_dropsrvrolemember 'JackO', 'sysadmin';  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen Sie SERVER ROLE &#40; Transact-SQL &#41;](../../t-sql/statements/create-server-role-transact-sql.md)   
 [DROP SERVER ROLE &#40; Transact-SQL &#41;](../../t-sql/statements/drop-server-role-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addsrvrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md)   
 [Sp_droprolemember &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Sicherheitsfunktionen &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  

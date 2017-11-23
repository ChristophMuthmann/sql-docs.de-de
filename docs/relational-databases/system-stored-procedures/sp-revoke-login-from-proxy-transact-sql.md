---
title: Sp_revoke_login_from_proxy (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- sp_revoke_login_from_proxy_TSQL
- sp_revoke_login_from_proxy
dev_langs: TSQL
helpviewer_keywords: sp_revoke_login_from_proxy
ms.assetid: e4546c13-9fba-4bab-8b42-d6f18b33ec25
caps.latest.revision: "20"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: efb329d4bdbdaef250e9843ed1f4641d0a679181
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sprevokeloginfromproxy-transact-sql"></a>sp_revoke_login_from_proxy (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Entfernt den Zugriff auf einen Proxy für ein Sicherheitsprinzipal.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_revoke_login_from_proxy   
    [ @name = ] 'name' ,  
    [ @proxy_id = ] id ,  
    [ @proxy_name = ] 'proxy_name'  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@name=** ] **"***Namen***"**  
 Der Name des der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldung, Serverrolle oder **Msdb** -Datenbankrolle, für den Zugriff für zu entfernen. *Namen* ist **nvarchar(256)** hat keinen Standardwert.  
  
 [  **@proxy_id=** ] *Id*  
 Die ID des Proxys, für den der Zugriff entfernt werden soll. Entweder *Id* oder *Proxy_name* muss angegeben werden, aber beide können nicht angegeben werden. *id* ist vom Datentyp **int**und hat den Standardwert NULL.  
  
 [  **@proxy_name=** ] **"***Proxy_name***"**  
 Der Name des Proxys, für den der Zugriff entfernt werden soll. Entweder *Id* oder *Proxy_name* muss angegeben werden, aber beide können nicht angegeben werden. Die *Proxy_name* ist **Sysname**, hat den Standardwert NULL.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 Aufträge im Besitz des Anmeldenamens, der auf diesen Proxy verweist, schlagen fehl.  
  
## <a name="permissions"></a>Berechtigungen  
 Zum Ausführen dieser gespeicherten Prozedur muss ein Benutzer Mitglied der festen Serverrolle **sysadmin** sein.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird der Zugriff auf den Proxy `terrid` für den Anmeldenamen `Catalog application proxy` aufgehoben.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_revoke_login_from_proxy  
    @name = N'terrid',  
    @proxy_name = N'Catalog application proxy' ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server-Agent-gespeicherte Prozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [Sp_grant_login_to_proxy &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md)   
 [Sp_help_proxy &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-proxy-transact-sql.md)  
  
  

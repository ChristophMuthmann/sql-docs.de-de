---
title: Sp_update_proxy (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_update_proxy
- sp_update_proxy_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER PROXY statement
- sp_update_proxy
ms.assetid: 864fd0e6-9d61-4f07-92ef-145318d2f881
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 402bdaa7ad89675cfaefec39cc8e36312e78d359
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spupdateproxy-transact-sql"></a>sp_update_proxy (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ändert die Eigenschaften eines vorhandenen Proxys.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_update_proxy   
    [ @proxy_id = ] id,  
    [ @proxy_name = ] 'proxy_name',  
    [ @credential_name = ] 'credential_name' ,  
    [ @credential_id = ] credential_id ,  
    [ @new_name = ] 'new_name' ,  
    [ @enabled = ] is_enabled ,  
    [ @description = ] 'description'  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@proxy_id**= ] *id*  
 Die Proxy-ID des Proxys, der geändert werden soll. Die *Proxy_id* ist **Int**, hat den Standardwert NULL.  
  
 [ **@proxy_name**=] **"***Proxy_name***"**  
 Der Name des Proxys, der geändert werden soll. Die *Proxy_name* ist **Sysname**, hat den Standardwert NULL.  
  
 [ **@credential_name** =] **"***Credential_name***"**  
 Der Name der neuen Anmeldeinformationen für den Proxy. Die *Credential_name* ist **Sysname**, hat den Standardwert NULL. Entweder *Credential_name* oder *Credential_id* kann angegeben werden.  
  
 [ **@credential_id** = ] *credential_id*  
 Die ID der neuen Anmeldeinformationen für den Proxy. Die *Credential_id* ist **Int**, hat den Standardwert NULL. Entweder *Credential_name* oder *Credential_id* kann angegeben werden.  
  
 [ **@new_name**=] **"***New_name***"**  
 Der neue Name des Proxys. Die *New_name* ist **Sysname**, hat den Standardwert NULL. Wenn angegeben, wird die Prozedur ändert den Namen des Proxys, für *New_name*. Wenn für das Argument NULL festgelegt wird, bleibt der Name des Proxys unverändert.  
  
 [ **@enabled** =] *Is_enabled*  
 Gibt an, ob der Proxy aktiviert ist: Die *Is_enabled* Flag **"tinyint"**, hat den Standardwert NULL. Wenn *Is_enabled* ist **0**, der Proxy nicht aktiviert und kann nicht von einem Auftragsschritt verwendet werden. Wird für das Argument NULL festgelegt, bleibt der Status des Proxys unverändert.  
  
 [ **@description**=] **"***Beschreibung***"**  
 Die neue Beschreibung des Proxys. Die *Beschreibung* ist **vom Datentyp nvarchar(512)**, hat den Standardwert NULL. Wenn für das Argument NULL festgelegt wird, bleibt die Beschreibung des Proxys unverändert.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 Entweder **@proxy_name** oder **@proxy_id** muss angegeben werden. Wenn beide Argumente angegeben werden, müssen sie sich beide auf denselben Proxy beziehen. Andernfalls erzeugt die gespeicherte Prozedur einen Fehler.  
  
 Entweder **@credential_name** oder **@credential_id** muss angegeben werden, um die Anmeldeinformationen für den Proxy zu ändern. Wenn beide Argumente angegeben werden, müssen sich beide auf dieselben Anmeldeinformationen beziehen, andernfalls erzeugt die gespeicherte Prozedur einen Fehler.  
  
 Mit dieser Prozedur wird der Proxy geändert, jedoch nicht der Zugriff auf den Proxy. Um den Zugriff auf einen Proxy zu ändern, verwenden Sie **Sp_grant_login_to_proxy** und **Sp_revoke_login_from_proxy**.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der **Sysadmin** festen Sicherheitsrolle kann diese Prozedur ausführen.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird der aktivierte Wert für den Proxy `Catalog application proxy` auf `0` festgelegt.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_proxy  
    @proxy_name = 'Catalog application proxy',  
    @enabled = 0;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server-Agent-Prozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [Implementieren von Sicherheit für SQL Server-Agent](http://msdn.microsoft.com/library/d770d35c-c8de-4e00-9a85-7d03f45a0f0d)   
 [sp_add_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md)   
 [sp_delete_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-proxy-transact-sql.md)   
 [sp_grant_login_to_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md)   
 [sp_revoke_login_from_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revoke-login-from-proxy-transact-sql.md)  
  
  

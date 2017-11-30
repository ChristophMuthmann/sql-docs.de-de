---
title: Sp_enum_login_for_proxy (Transact-SQL) | Microsoft Docs
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
- sp_enum_login_for_proxy_TSQL
- sp_enum_login_for_proxy
dev_langs: TSQL
helpviewer_keywords: sp_enum_login_for_proxy
ms.assetid: 62a75019-248a-44c8-a5cc-c79f55ea3acf
caps.latest.revision: "18"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c3c19ebb2104500b3d394a10cabb8589bc4ded0b
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="spenumloginforproxy-transact-sql"></a>sp_enum_login_for_proxy (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Listet Zuordnungen zwischen Sicherheitsprinzipalen und Proxys auf.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_enum_login_for_proxy  
    [ @name = ] 'name'  
    [ @proxy_id = ] id,  
    [ @proxy_name = ] 'proxy_name'  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@name** =] '*Namen*"  
 Der Name des eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Prinzipal, Anmeldung, Serverrolle oder **Msdb** -Datenbankrolle, für die Proxys aufgelistet werden sollen. Der Name ist **nvarchar(256)**, hat den Standardwert NULL.  
  
 [  **@proxy_id** =] *Id*  
 Die Proxy-ID des Proxys, zu dem die Informationen aufgelistet werden sollen. Die *Proxy_id* ist **Int**, hat den Standardwert NULL. Entweder die *Id* oder *Proxy_name* kann angegeben werden.  
  
 [  **@proxy_name** =] **"***Proxy_name***"**  
 Der Name des Proxys, zu dem Informationen aufgelistet werden sollen. Die *Proxy_name* ist **Sysname**, hat den Standardwert NULL. Entweder die *Id* oder *Proxy_name* kann angegeben werden.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**proxy_id**|**int**|ID des Proxys.|  
|**proxy_name**|**sysname**|Der Name des Proxys.|  
|**name**|**sysname**|Name des Sicherheitsprinzipals für die Zuordnung|  
|**Flags**|**int**|Typ des Sicherheitsprinzipals.<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldung<br /><br /> **1** = feste Systemrolle<br /><br /> **2** = Datenbankrolle in **Msdb**|  
  
## <a name="remarks"></a>Hinweise  
 Wenn keine Parameter angegeben sind, **Sp_enum_login_for_proxy** listet Informationen zu allen Anmeldenamen in der Instanz für alle Proxys.  
  
 Wenn eine Proxy-Id oder ein Proxyname angegeben wird, **Sp_enum_login_for_proxy** Anmeldungen, die Zugriff auf den Proxy haben aufgelistet sind. Wenn ein Anmeldename angegeben wird, **Sp_enum_login_for_proxy** Listen die Proxys, die der Anmeldename hat Zugriff auf.  
  
 Wenn sowohl ein Proxy als auch ein Anmeldename angegeben wird, gibt das Resultset eine Zeile zurück, falls der angegebene Anmeldename auf den angegebenen Proxy zugreifen kann.  
  
 Diese gespeicherte Prozedur befindet sich im **Msdb**.  
  
## <a name="permissions"></a>Berechtigungen  
 Ausführungsberechtigungen für diese Prozedur erhalten standardmäßig Mitglieder der **Sysadmin** festen Serverrolle "".  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-listing-all-associations"></a>A. Auflisten aller Zuordnungen  
 Mit dem folgenden Beispiel werden alle Berechtigungen aufgelistet, die in der aktuellen Instanz zwischen Anmeldenamen und Proxys eingerichtet wurden.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_enum_login_for_proxy ;  
GO  
```  
  
### <a name="b-listing-proxies-for-a-specific-login"></a>B. Auflisten von Proxys für einen bestimmten Anmeldenamen  
 Mit dem folgenden Beispiel werden die Proxys aufgelistet, auf die der Anmeldename `terrid` zugreifen kann.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_enum_login_for_proxy  
    @name = 'terrid' ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_help_proxy &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-proxy-transact-sql.md)   
 [Sp_grant_login_to_proxy &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md)   
 [Sp_revoke_login_from_proxy &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-revoke-login-from-proxy-transact-sql.md)  
  
  

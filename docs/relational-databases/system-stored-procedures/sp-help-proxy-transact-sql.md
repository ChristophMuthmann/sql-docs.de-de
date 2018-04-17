---
title: Sp_help_proxy (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
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
- sp_help_proxy
- sp_help_proxy_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_proxy
ms.assetid: a2fce164-2b64-40c2-8f35-6eeb7844abf1
caps.latest.revision: 38
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 314eeb6365afafce64ff85aa822e9b2be8c64770
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sphelpproxy-transact-sql"></a>sp_help_proxy (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Listet Informationen zu mindestens einem Proxy auf.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_help_proxy   
    [ @proxy_id = ] id,  
    [ @proxy_name = ] 'proxy_name' ,  
    [ @subsystem_name = ] 'subsystem_name' ,  
    [ @name = ] 'name'  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@proxy_id** = ] *id*  
 Die Proxy-ID des Proxys, zu dem die Informationen aufgelistet werden sollen. Die *Proxy_id* ist **Int**, hat den Standardwert NULL. Entweder die *Id* oder *Proxy_name* kann angegeben werden.  
  
 [ **@proxy_name** =] **"***Proxy_name***"**  
 Der Name des Proxys, zu dem Informationen aufgelistet werden sollen. Die *Proxy_name* ist **Sysname**, hat den Standardwert NULL. Entweder die *Id* oder *Proxy_name* kann angegeben werden.  
  
 [ **@subsystem_name** =] '*Subsystem_name*"  
 Der Name des Subsystems, für den Proxys aufgelistet werden sollen. Die *Subsystem_name* ist **Sysname**, hat den Standardwert NULL. Wenn *Subsystem_name* angegeben wird, *Namen* muss auch angegeben werden.  
  
 In der folgenden Tabelle werden die Werte für jedes Subsystem aufgelistet.  
  
|Wert|Description|  
|-----------|-----------------|  
|ActiveScripting|ActiveX-Skript|  
|CmdExec|Betriebssystem (CmdExec)|  
|Momentaufnahme|Replikationsmomentaufnahme-Agent|  
|LogReader|Replikationsprotokolllese-Agent|  
|Distribution|Replikationsverteilungs-Agent|  
|Merge|Replikationsmerge-Agent|  
|QueueReader|Warteschlangenlese-Agent der Microsoft SQL Server-Replikation|  
|ANALYSISQUERY|Analysis Services-Befehl|  
|ANALYSISCOMMAND|Analysis Services-Abfrage|  
|Dts|SSIS-Paketausführung|  
|PowerShell|PowerShell-Skript|  
  
 [ **@name** =] '*Namen*"  
 Der Name einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldung, für die Proxys aufgelistet werden sollen. Der Name ist **nvarchar(256)**, hat den Standardwert NULL. Wenn *Namen* angegeben wird, *Subsystem_name* muss auch angegeben werden.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**proxy_id**|**int**|ID des Proxys.|  
|**name**|**sysname**|Der Name des Proxys.|  
|**credential_identity**|**sysname**|Der Microsoft Windows-Domänenname und -Benutzername für die dem Proxy zugeordneten Anmeldeinformationen.|  
|**Aktiviert**|**tinyint**|Gibt an, ob dieser Proxy aktiviert ist. { **0** = nicht aktiviert, **1** = aktiviert}|  
|**description**|**nvarchar(1024)**|Die Beschreibung des Proxys.|  
|**user_sid**|**varbinary(85)**|Die Windows-SID des Windows-Benutzers für diesen Proxy.|  
|**credential_id**|**int**|Die ID für die dem Proxy zugeordneten Anmeldeinformationen.|  
|**credential_identity_exists**|**int**|Gibt an, ob credential_identity vorhanden ist. { 0 = ist nicht vorhanden, 1 = ist vorhanden }|  
  
## <a name="remarks"></a>Hinweise  
 Wenn keine Parameter angegeben sind, **Sp_help_proxy** werden Informationen zu allen Proxys in der Instanz aufgelistet.  
  
 Um zu bestimmen, welche Proxys eine Anmeldung für ein bestimmtes Subsystem verwenden können, geben Sie *Namen* und *Subsystem_name*. Wenn diese Argumente angegeben werden, **Sp_help_proxy** Proxys, die die Anmeldung angegeben möglicherweise den Zugriff und kann verwendet werden für das angegebene Subsystem aufgelistet.  
  
## <a name="permissions"></a>Berechtigungen  
 Standardmäßig können nur Mitglieder der festen Serverrolle **sysadmin** diese gespeicherte Prozedur ausführen. Andere Benutzer müssen Mitglieder der festen Datenbankrolle **SQLAgentOperatorRole** in der **msdb** -Datenbank sein.  
  
 Weitere Informationen zu **SQLAgentOperatorRole**, finden Sie unter [SQL Server Agent Fixed Database Roles](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
> [!NOTE]  
>  Die **Credential_identity** und **User_sid** Spalten werden nur zurückgegeben, das Ergebnis festgelegt, wenn Mitglieder der **Sysadmin** diese gespeicherte Prozedur ausführen.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-listing-information-for-all-proxies"></a>A. Auflistungsinformationen für alle Proxys  
 Im folgenden Beispiel werden die Informationen zu allen Proxys in der Instanz aufgelistet.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_proxy ;  
GO  
```  
  
### <a name="b-listing-information-for-a-specific-proxy"></a>B. Auflistungsinformationen für einen bestimmten Proxy  
 Im folgenden Beispiel werden die Informationen zum Proxy `Catalog application proxy` aufgelistet.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_proxy  
    @proxy_name = N'Catalog application proxy' ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server-Agent-Prozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_add_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md)   
 [sp_delete_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-proxy-transact-sql.md)  
  
  

---
title: Sp_revoke_proxy_from_subsystem (Transact-SQL) | Microsoft Docs
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
- sp_revoke_login_from_subsystem
- sp_revoke_login_from_subsystem_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_revoke_proxy_from_subsystem
ms.assetid: b87bc8ba-3ea8-4aed-b54b-32c3d82d9d2a
caps.latest.revision: "37"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 475b036aae17e29f2ebac4333198671cdd42e675
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sprevokeproxyfromsubsystem-transact-sql"></a>sp_revoke_proxy_from_subsystem (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Hebt den Zugriff auf ein Subsystem für einen Proxy auf.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_revoke_proxy_from_subsystem   
    [ @proxy_id = ] proxy_id,  
    [ @proxy_name = ] 'proxy_name',  
    [ @subsystem_id = ] subsystem_id,  
    [ @subsystem_name = ] 'subsystem_name'  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@proxy_id**  =] *Id*  
 Die Proxy-ID des Proxys, für den der Zugriff aufgehoben werden soll. Die *Proxy_id* ist **Int**, hat den Standardwert NULL. Entweder *Proxy_id* oder *Proxy_name* muss angegeben werden, aber beide können nicht angegeben werden.  
  
 [  **@proxy_name**  =] **"***Proxy_name***"**  
 Der Name des Proxys, für den der Zugriff aufgehoben werden soll. Die *Proxy_name* ist **Sysname**, hat den Standardwert NULL. Entweder *Proxy_id* oder *Proxy_name* muss angegeben werden, aber beide können nicht angegeben werden.  
  
 [  **@subsystem_id**  =] *Id*  
 Die ID des Subsystems, für das der Zugriff aufgehoben werden soll. Die *Subsystem_id* ist **Int**, hat den Standardwert NULL. Entweder *Subsystem_id* oder *Subsystem_name* muss angegeben werden, aber beide können nicht angegeben werden. In der folgenden Tabelle werden die Werte für jedes Subsystem aufgelistet.  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|**2**|ActiveX-Skript<br /><br /> **\*\*Wichtige \* \***  das ActiveX Scripting-Subsystem daraus [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agents in einer zukünftigen Version von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Nutzen Sie diese Funktionen bei Neuentwicklungen nicht mehr, und planen Sie die Änderung von Anwendungen, die diese Funktion zurzeit verwenden.|  
|**3**|Betriebssystem (CmdExec)|  
|**4**|Replikationsmomentaufnahme-Agent|  
|**5**|Replikationsprotokolllese-Agent|  
|**6**|Replikationsverteilungs-Agent|  
|**7**|Replikationsmerge-Agent|  
|**8**|Warteschlangenlese-Agent der Microsoft SQL Server-Replikation|  
|**9**|Analysis Services-Befehl|  
|**10**|Analysis Services-Abfrage|  
|**11**|[!INCLUDE[ssIS](../../includes/ssis-md.md)]-Paketausführung|  
|**12**|PowerShell-Skript|  
  
 [  **@subsystem_name** =] **"***Subsystem_name***"**  
 Der Name des Subsystems, für das der Zugriff aufgehoben werden soll. Die *Subsystem_name* ist **Sysname**, hat den Standardwert NULL. Entweder *Subsystem_id* oder *Subsystem_name* muss angegeben werden, aber beide können nicht angegeben werden. In der folgenden Tabelle werden die Werte für jedes Subsystem aufgelistet.  
  
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
|Dts|[!INCLUDE[ssIS](../../includes/ssis-md.md)]-Paketausführung|  
|PowerShell|PowerShell-Skript|  
  
## <a name="remarks"></a>Hinweise  
 Mit dem Aufheben des Zugriffs auf ein Subsystem werden nicht die Berechtigungen für den im Proxy angegebenen Prinzipal geändert.  
  
> [!NOTE]  
>  Um zu bestimmen, welche Auftragsschritte auf einen Proxy verweisen, Maustaste die **Proxys** Knoten unter **SQL Server-Agent** in Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], und klicken Sie dann auf **Eigenschaften**. In der **Proxyeigenschaften** wählen Sie im Dialogfeld die **Verweise** Seite, um alle Auftragsschritte anzuzeigen, die diesen Proxy verweisen.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der **Sysadmin** -Serverrolle kann ausführen **Sp_revoke_proxy_from_subsystem**.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird der Zugriff auf das [!INCLUDE[ssIS](../../includes/ssis-md.md)]-Subsystem für den Proxy `Catalog application proxy` aufgehoben.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_revoke_proxy_from_subsystem  
    @proxy_name = 'Catalog application proxy',  
    @subsystem_name = N'Dts';  
```  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server-Agent-gespeicherte Prozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [Implementieren von Sicherheit für SQL Server-Agent](http://msdn.microsoft.com/library/d770d35c-c8de-4e00-9a85-7d03f45a0f0d)   
 [Sp_grant_proxy_to_subsystem &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-grant-proxy-to-subsystem-transact-sql.md)  
  
  

---
title: Sp_addlogreader_agent (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_addlogreader_agent
- sp_addlogreader_agent_TSQL
helpviewer_keywords: sp_addlogreader_agent
ms.assetid: d83096b9-96ee-4789-bde0-940d4765b9ed
caps.latest.revision: "37"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 53f2e42d92c9e100dfe90ae0b46ec2e2c2eef969
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spaddlogreaderagent-transact-sql"></a>sp_addlogreader_agent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Fügt einen Protokolllese-Agent für eine bestimmte Datenbank hinzu. Diese gespeicherte Prozedur wird auf dem Verleger für die Veröffentlichungsdatenbank ausgeführt.  
  
> [!IMPORTANT]  
>  Beim Konfigurieren eines Verlegers mit einem Remoteverteiler werden die Werte, die für alle Parameter, einschließlich *job_login* und *job_password*, bereitgestellt werden, als Nur-Text an den Verteiler gesendet. Sie sollten die Verbindung zwischen dem Verleger und dem zugehörigen Remoteverteiler verschlüsseln, bevor Sie diese gespeicherte Prozedur ausführen. Weitere Informationen finden Sie unter [Aktivieren von verschlüsselten Verbindungen zum Datenbankmodul &#40;SQL Server-Konfigurations-Manager&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_addlogreader_agent [ @job_login = ] 'job_login'  
        , [ @job_password = ] 'job_password'  
    [ , [ @job_name = ] 'job_name' ]  
    [ , [ @publisher_security_mode = ] publisher_security_mode ]  
    [ , [ @publisher_login = ] 'publisher_login' ]  
    [ , [ @publisher_password = ] 'publisher_password' ]   
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@job_login** =] **"***Job_login***"**  
 Der Anmeldename für das [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Konto, unter dem der Agent ausgeführt wird. *Job_login* ist **nvarchar(257)**, hat den Standardwert NULL. Das Windows-Konto wird stets für Agent-Verbindungen mit dem Verteiler verwendet.  
  
> [!NOTE]  
>  Für nicht-[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Herausgeber, diese Angabe muss die gleiche Anmeldung im angegebenen [Sp_adddistpublisher &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md).  
  
 [  **@job_password** =] **"***Job_password***"**  
 Das Kennwort für das Windows-Konto, unter dem der Agent ausgeführt wird. *Job_password* ist **Sysname**, hat den Standardwert NULL.  
  
> [!IMPORTANT]  
>  Speichern Sie keine Authentifizierungsinformationen in Skriptdateien. Für die optimale Sicherheit sollten Anmeldenamen und Kennwörter zur Laufzeit bereitgestellt werden.  
  
 [  **@job_name** =] **"***Job_name***"**  
 Der Name eines vorhandenen Agentauftrags. *Job_name* ist **Sysname**, hat den Standardwert NULL. Dieser Parameter wird nur dann angegeben, wenn der Agent mit einem vorhandenen Auftrag anstatt mit einem neu erstellten Auftrag (Standard) gestartet wird.  
  
 [  **@publisher_security_mode** =] *Publisher_security_mode*  
 Der vom Agent beim Herstellen der Verbindung mit dem Verleger verwendete Sicherheitsmodus. *Publisher_security_mode* ist **"smallint"**, hat den Standardwert **1**. **0** gibt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung und **1** gibt die Windows-Authentifizierung. Der Wert **0** muss angegeben werden, für nicht -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Herausgeber.  
  
 [  **@publisher_login** =] **"***Publisher_login***"**  
 Der Anmeldename, der beim Herstellen der Verbindung mit dem Verleger verwendet wird. *Publisher_login* ist **Sysname**, hat den Standardwert NULL. *Publisher_login* muss angegeben werden, wenn *Publisher_security_mode* ist **0**. Wenn *Publisher_login* ist NULL und *Publisher_security_mode* ist **1**, und klicken Sie dann das Windows-Konto im angegebenen *Job_login* verwendet werden Wenn eine Verbindung mit dem Verleger herstellen.  
  
 [  **@publisher_password** =] **"***Publisher_password***"**  
 Das Kennwort, das beim Herstellen der Verbindung mit dem Verleger verwendet wird. *Publisher_password* ist **Sysname**, hat den Standardwert NULL.  
  
> [!IMPORTANT]  
>  Speichern Sie keine Authentifizierungsinformationen in Skriptdateien. Für die optimale Sicherheit sollten Anmeldenamen und Kennwörter zur Laufzeit bereitgestellt werden.  
  
 [  **@publisher** =] **"***Publisher***"**  
 Der Name des nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Verleger. *Publisher* ist **Sysname**, hat den Standardwert NULL.  
  
> [!NOTE]  
>  Sie sollten diesen Parameter nicht für einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Verleger festlegen.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_addlogreader_agent** wird bei der Transaktionsreplikation verwendet.  
  
 Müssen Sie ausführen, **Sp_addlogreader_agent** einen Protokolllese-Agent hinzufügen, wenn Sie ein Upgrade eine Datenbank, die für die Replikation auf diese Version von aktiviert wurde [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , bevor eine Veröffentlichung erstellt wurde, die die Datenbank verwendet.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** feste Serverrolle oder die **Db_owner** feste Datenbankrolle können ausführen **Sp_addlogreader_agent**.  
  
## <a name="example"></a>Beispiel  
 [!code-sql[HowTo#sp_AddTranPub](../../relational-databases/replication/codesnippet/tsql/sp-addlogreader-agent-tr_1.sql)]  
  
## <a name="see-also"></a>Siehe auch  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Sp_addpublication &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [Sp_changelogreader_agent &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-changelogreader-agent-transact-sql.md)   
 [Gespeicherte Automatisierungsprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  

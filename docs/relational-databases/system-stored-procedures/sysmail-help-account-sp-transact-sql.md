---
title: Sysmail_help_account_sp (Transact-SQL) | Microsoft Docs
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
- sysmail_help_account_sp_TSQL
- sysmail_help_account_sp
dev_langs: TSQL
helpviewer_keywords: sysmail_help_account_sp
ms.assetid: 87c7c39c-8e05-4e68-9272-45f908809c3b
caps.latest.revision: "48"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b586334d1b725922ec38b3ed63e6cfc8eb0847a7
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysmailhelpaccountsp-transact-sql"></a>sysmail_help_account_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Listet Informationen (mit Ausnahme von Kennwörtern) zu Datenbank-E-Mail-Konten auf.  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sysmail_help_account_sp [ [ @account_id = ] account_id | [ @account_name = ] 'account_name' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@account_id**  =] *Account_id*  
 Die Konto-ID des Kontos, für das Informationen aufgelistet werden sollen. *account_id* ist vom Datentyp **int**und hat den Standardwert NULL.  
  
 [  **@account_name**  =] **"***Account_name***"**  
 Der Name des Kontos, für das Informationen aufgelistet werden sollen. *account_name* ist vom Datentyp **sysname**und hat den Standardwert NULL.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Gibt ein Resultset mit den nachfolgend aufgelisteten Spalten zurück.  
  
||||  
|-|-|-|  
|Spaltenname|Datentyp|Description|  
|**account_id**|**int**|ID des Kontos|  
|**name**|**sysname**|Der Name des Kontos.|  
|**Beschreibung**|**nvarchar(256)**|Beschreibung des Kontos|  
|**email_address**|**vom Datentyp nvarchar(128)**|E-Mail-Adresse, von der aus Nachrichten versandt werden|  
|**Anzeigename**|**vom Datentyp nvarchar(128)**|Der Anzeigename des Kontos.|  
|**replyto_address**|**vom Datentyp nvarchar(128)**|Adresse, an die Antworten auf die Nachrichten von diesem Konto versandt werden|  
|**Servertyp**|**sysname**|Typ des E-Mail-Servers für das Konto|  
|**Servername**|**sysname**|Name des E-Mail-Servers für das Konto|  
|**port**|**int**|Portnummer, die der E-Mail-Server verwendet|  
|**Benutzername**|**vom Datentyp nvarchar(128)**|Der Benutzername für die Anmeldung am E-Mail-Server, wenn der E-Mail-Server eine Authentifizierung verwendet. Wenn **username** den Wert NULL hat, verwendet Datenbank-E-Mail keine Authentifizierung für dieses Konto.|  
|**use_default_credentials**|**bit**|Gibt an, ob E-Mail mithilfe der Anmeldeinformationen von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] an den SMTP-Server gesendet wird. **use_default_credentials** ist vom Datentyp bit und hat keinen Standardwert. Wenn dieser Parameter 1 ist, verwendet Datenbank-Mail die Anmeldeinformationen des der [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] Dienst. Wenn dieser Parameter 0 ist, Database Mail verwendet die  **@username**  und  **@password**  für die Authentifizierung auf dem SMTP-Server. Wenn  **@username**  und  **@password**  NULL sind, und klicken Sie dann Database Mail anonyme Authentifizierung verwendet. Wenden Sie sich an Ihren SMTP-Administrator, bevor Sie diesen Parameter angeben.|  
|**enable_ssl**|**bit**|Gibt an, ob Datenbank-E-Mail die Kommunikation mithilfe von SSL (Secure Sockets Layer) verschlüsselt. Verwenden Sie diese Option, wenn auf dem SMTP-Server SSL erforderlich ist. **enable_ssl** ist vom Datentyp bit und hat keinen Standardwert. 1 gibt an, dass Datenbank-E-Mail die Kommunikation mit SSL verschlüsselt. 0 gibt an, dass Datenbank-E-Mail die E-Mail ohne SSL-Verschlüsselung sendet.|  
  
## <a name="remarks"></a>Hinweise  
 Wenn keine *account_id* - oder *account_name* -Parameter bereitgestellt werden, listet **sysmail_help_account** Informationen für alle Datenbank-E-Mail-Konten in der Microsoft SQL Server-Instanz auf.  
  
 Die gespeicherte Prozedur **sysmail_help_account_sp** wird in der **msdb** -Datenbank gespeichert und befindet sich im Besitz des **dbo** -Schemas. Handelt es sich bei der aktuellen Datenbank nicht um **msdb**, muss die Prozedur mit einem dreiteiligen Namen ausgeführt werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Über die Ausführungsberechtigungen für diese Prozedur verfügen standardmäßig die Mitglieder der festen Serverrolle **sysadmin** .  
  
## <a name="examples"></a>Beispiele  
 **A. Auflisten der Informationen für alle Konten**  
  
 Im folgenden Beispiel werden die Kontodaten für alle Konten in der Instanz aufgelistet.  
  
```  
EXECUTE msdb.dbo.sysmail_help_account_sp ;  
```  
  
 Es folgt ein Beispielresultset, das auf Zeilenlänge umformatiert wurde:  
  
```  
account_id  name                         description                             email_address             display_name                     replyto_address servertype servername                port        username use_default_credentials enable_ssl  
----------- ---------------------------- --------------------------------------- ------------------------- -------------------------------- --------------- ---------- ------------------------- ----------- -------- ----------------------- ----------  
148         AdventureWorks Administrator Mail account for administrative e-mail. dba@Adventure-Works.com   AdventureWorks Automated Mailer  NULL            SMTP       smtp.Adventure-Works.com  25          NULL 0                          0        
149         Audit Account                Account for audit e-mail.               audit@Adventure-Works.com Automated Mailer (Audit)         NULL            SMTP       smtp.Adventure-Works.com  25          NULL 0                          0        
```  
  
 **B. Auflisten der Informationen für ein spezifisches Konto**  
  
 Im folgenden Beispiel werden die Kontodaten für das Konto mit dem Namen `AdventureWorks Administrator`aufgelistet.  
  
```  
EXECUTE msdb.dbo.sysmail_help_account_sp  
    @account_name = 'AdventureWorks Administrator' ;  
```  
  
 Es folgt ein Beispielresultset, das auf Zeilenlänge umformatiert wurde:  
  
```  
account_id  name                         description                             email_address             display_name                     replyto_address servertype servername                port        username use_default_credentials enable_ssl  
----------- ---------------------------- ------------------------------------------------------ ------------------------- ---------------- ---------- ------------------------- ----------- -------- ----------------------- ----------  
148         AdventureWorks Administrator Mail account for administrative e-mail. dba@Adventure-Works.com   AdventureWorks Automated Mailer  NULL            SMTP       smtp.Adventure-Works.com  25          NULL     0                       0       
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbank-E-Mail](../../relational-databases/database-mail/database-mail.md)   
 [Erstellen eines Datenbank-Mail-Kontos](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Database Mail gespeicherte Systemprozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  

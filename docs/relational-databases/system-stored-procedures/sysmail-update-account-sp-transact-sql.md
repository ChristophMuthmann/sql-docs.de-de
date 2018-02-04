---
title: Sysmail_update_account_sp (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 11/17/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysmail_update_account_sp
- sysmail_update_account_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_update_account_sp
ms.assetid: ba2fdccc-5ed4-40ef-a479-79497b4d61aa
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4be8c0c87771f89d92cc0344c207149467c4554c
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="sysmailupdateaccountsp-transact-sql"></a>sysmail_update_account_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ändert die Informationen in einem vorhandenen Konto für Datenbank-E-Mail.  
 
 
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sysmail_update_account_sp [ [ @account_id = ] account_id ] [ , ] [ [ @account_name = ] 'account_name' ] ,  
    [ @email_address = ] 'email_address' ,   
    [ @display_name = ] 'display_name' ,   
    [ @replyto_address = ] 'replyto_address' ,  
    [ @description = ] 'description' ,   
    [ @mailserver_name = ] 'server_name' ,   
    [ @mailserver_type = ] 'server_type' ,   
    [ @port = ] port_number ,   
    [ @timeout = ] 'timeout' ,  
    [ @username = ] 'username' ,  
    [ @password = ] 'password' ,  
    [ @use_default_credentials = ] use_default_credentials ,  
    [ @enable_ssl = ] enable_ssl   
```  
  
## <a name="arguments"></a>Argumente  
 [ **@account_id** = ] *account_id*  
 Die ID des Kontos, das aktualisiert werden soll. *account_id* ist vom Datentyp **int**und hat den Standardwert NULL. Mindestens eine der *Account_id* oder *Account_name* muss angegeben werden. Wenn beide Argumente angegeben werden, ändert die Prozedur den Namen des Kontos.  
  
 [  **@account_name**  =] **"***Account_name***"**  
 Der Name des zu aktualisierenden Kontos. *account_name* ist vom Datentyp **sysname**und hat den Standardwert NULL. Mindestens eine der *Account_id* oder *Account_name* muss angegeben werden. Wenn beide Argumente angegeben werden, ändert die Prozedur den Namen des Kontos.  
  
 [ **@email_address** = ] **'***email_address***'**  
 Die neue E-Mail-Adresse, von der die Nachricht gesendet werden soll. Bei dieser Adresse muss es sich um eine Internet-E-Mail-Adresse handeln. Der Servername ist die Adresse des Servers, der von Datenbank-E-Mail zum Senden von E-Mails von diesem Konto verwendet wird. *Email_address* ist **vom Datentyp nvarchar(128)**, hat den Standardwert NULL.  
  
 [ **@display_name** = ] **'***display_name***'**  
 Der neue Anzeigename, der in E-Mail-Nachrichten verwendet werden soll, die von diesem Konto gesendet werden. *Display_name* ist **vom Datentyp nvarchar(128)**, hat keinen Standardwert.  
  
 [ **@replyto_address** = ] **'***replyto_address***'**  
 Die neue Adresse, die im Antwortheader von E-Mail-Nachrichten verwendet werden soll, die von diesem Konto gesendet werden. *Replyto_address* ist **vom Datentyp nvarchar(128)**, hat keinen Standardwert.  
  
 [ **@description** = ] **'***description***'**  
 Die neue Beschreibung des Kontos. *Beschreibung* ist **nvarchar(256)**, hat den Standardwert NULL.  
  
 [ **@mailserver_name** = ] **'***server_name***'**  
 Der neue Name des SMTP-Mailservers, der für dieses Konto verwendet werden soll. Der Computer mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muss in der Lage, beheben Sie die *Server_name* in eine IP-Adresse. *Server_name* ist **Sysname**, hat keinen Standardwert.  
  
 [ **@mailserver_type** = ] **'***server_type***'**  
 Der neue Typ des E-Mail-Servers. *Server_type* ist **Sysname**, hat keinen Standardwert. Nur ein Wert von **'SMTP'** wird unterstützt.  
  
 [  **@port**  =] *Port_number*  
 Die neue Portnummer des E-Mail-Servers. *Port_number* ist **Int**, hat keinen Standardwert.  
  
 [  **@timeout**  =] **"***Timeout***"**  
 Timeoutparameter für SmtpClient. Senden einer einzelnen E-Mail-Nachricht. *Timeout* ist **Int** in Sekunden und hat keinen Standardwert.  
  
 [  **@username**  =] **"***Benutzername***"**  
 Der neue Benutzername, der für die Anmeldung beim E-Mail-Server verwendet werden soll. *Benutzername* ist **Sysname**, hat keinen Standardwert.  
  
 [ **@password** = ] **'***password***'**  
 Das neue Kennwort, das für die Anmeldung beim E-Mail-Server verwendet werden soll. *Kennwort* ist **Sysname**, hat keinen Standardwert.  
  
 [ **@use_default_credentials** = ] use_default_credentials  
 Gibt an, ob E-Mail mit den Anmeldeinformationen des [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]-Diensts an den SMTP-Server gesendet werden soll. **use_default_credentials** ist vom Datentyp bit und hat keinen Standardwert. Wenn dieser Parameter 1 ist, verwendet Datenbank-E-Mail die Anmeldeinformationen von [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Wenn dieser Parameter 0 ist, Database Mail verwendet die  **@username**  und  **@password**  für die Authentifizierung auf dem SMTP-Server. Wenn  **@username**  und  **@password**  NULL sind, verwendet das anonyme Authentifizierung. Besprechen Sie die geeignete Angabe für diesen Parameter mit Ihrem SMTP-Administrator.  
  
 [ **@enable_ssl** = ] enable_ssl  
 Gibt an, ob Datenbank-E-Mail die Kommunikation mithilfe von SSL (Secure Sockets Layer) verschlüsselt. Verwenden Sie diese Option, wenn auf dem SMTP-Server SSL erforderlich ist. **enable_ssl** ist vom Datentyp bit und hat keinen Standardwert.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 Wenn sowohl Kontoname als auch Konto-ID angegeben wird, aktualisiert die gespeicherte Prozedur nicht nur die Informationen für das Konto, sondern ändert auch noch den Kontonamen. Die Änderung des Kontonamens kann hilfreich sein, wenn ein fehlerhafter Kontoname korrigiert werden soll.  
  
 Die gespeicherte Prozedur **Sysmail_update_account_sp** befindet sich in der **Msdb** Datenbank und im Besitz der **Dbo** Schema. Handelt es sich bei der aktuellen Datenbank nicht um **msdb**, muss die Prozedur mit einem dreiteiligen Namen ausgeführt werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der festen Serverrolle **sysadmin** .  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-changing-the-information-for-an-account"></a>A. Ändern der Informationen für ein Konto  
 Das folgende Beispiel aktualisiert das Konto `AdventureWorks Administrator` In der **Msdb** Datenbank. Die Informationen für dieses Konto werden auf die bereitgestellten Werte festgelegt.  
  
```  
EXECUTE msdb.dbo.sysmail_update_account_sp  
     @account_name = 'AdventureWorks Administrator'  
    ,@description = 'Mail account for administrative e-mail.'  
    ,@email_address = 'dba@Adventure-Works.com'  
    ,@display_name = 'AdventureWorks Automated Mailer'  
    ,@replyto_address = NULL  
    ,@mailserver_name = 'smtp.Adventure-Works.com'  
    ,@mailserver_type = 'SMTP'  
    ,@port = 25  
    ,@timeout = 60  
    ,@username = NULL  
    ,@password = NULL  
    ,@use_default_credentials = 0  
    ,@enable_ssl = 0;  
```  
  
### <a name="b-changing-the-name-of-an-account-and-the-information-for-an-account"></a>B. Ändern des Namens eines Kontos und der Informationen für ein Konto  
 Im folgenden Beispiel wird der Name des Kontos mit der Konto-ID `125` geändert, und die Informationen für dieses Konto werden aktualisiert. Der Name des Kontos lautet `Backup Mail Server`.  
  
```  
EXECUTE msdb.dbo.sysmail_update_account_sp  
     @account_id = 125  
    ,@account_name = 'Backup Mail Server'  
    ,@description = 'Mail account for administrative e-mail.'  
    ,@email_address = 'dba@Adventure-Works.com'  
    ,@display_name = 'AdventureWorks Automated Mailer'  
    ,@replyto_address = NULL  
    ,@mailserver_name = 'smtp-backup.Adventure-Works.com'  
    ,@mailserver_type = 'SMTP'  
    ,@port = 25  
    ,@timeout = 60  
    ,@username = NULL  
    ,@password = NULL  
    ,@use_default_credentials = 0  
    ,@enable_ssl = 0;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbank-E-Mail](../../relational-databases/database-mail/database-mail.md)   
 [Erstellen eines Datenbank-Mail-Kontos](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Database Mail gespeicherte Systemprozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  

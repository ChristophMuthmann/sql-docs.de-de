---
title: Sysmail_add_account_sp (Transact-SQL) | Microsoft Docs
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
- sysmail_add_account_sp
- sysmail_add_account_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_add_account_sp
ms.assetid: 65e15e2e-107c-49c3-b12c-f4edf0eb1617
caps.latest.revision: 40
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0387b4dac0a8d0419b5ffccb8ac8520a0bc1bd0c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysmailaddaccountsp-transact-sql"></a>sysmail_add_account_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Erstellt ein neues Datenbank-E-Mail-Konto, in dem Informationen zu einem SMTP-Konto gespeichert sind.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sysmail_add_account_sp  [ @account_name = ] 'account_name',  
    [ @email_address = ] 'email_address' ,  
    [ [ @display_name = ] 'display_name' , ]  
    [ [ @replyto_address = ] 'replyto_address' , ]  
    [ [ @description = ] 'description' , ]  
    [ @mailserver_name = ] 'server_name'   
    [ , [ @mailserver_type = ] 'server_type' ]  
    [ , [ @port = ] port_number ]  
    [ , [ @username = ] 'username' ]  
    [ , [ @password = ] 'password' ]  
    [ , [ @use_default_credentials = ] use_default_credentials ]  
    [ , [ @enable_ssl = ] enable_ssl ]  
    [ , [ @account_id = ] account_id OUTPUT ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@account_name** =] **"***Account_name***"**  
 Der Name des hinzuzufügenden Kontos. *account_name* ist vom Datentyp **sysname**und hat keinen Standardwert.  
  
 [ **@email_address** =] **"***Email_address***"**  
 Die E-Mail-Adresse, von der die Nachricht gesendet werden soll. Bei dieser Adresse muss es sich um eine Internet-E-Mail-Adresse handeln. *Email_address* ist **vom Datentyp nvarchar(128)**, hat keinen Standardwert. Angenommen, ein Konto für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent könnte e-Mails von der Adresse **SqlAgent@Adventure-Works.com**.  
  
 [ **@display_name** =] **"***Display_name***"**  
 Der Anzeigename, der in E-Mail-Nachrichten verwendet werden soll, die von diesem Konto gesendet werden. *Display_name* ist **vom Datentyp nvarchar(128)**, hat den Standardwert NULL. Angenommen, ein Konto für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] den Namen anzeigen **SQL Server Agent Automated Mailer** e-Mail-Nachrichten.  
  
 [ **@replyto_address** =] **"***Replyto_address***"**  
 Die Adresse, an die Antworten auf Nachrichten von diesem Konto gesendet werden. *Replyto_address* ist **vom Datentyp nvarchar(128)**, hat den Standardwert NULL. Z. B. Antworten auf ein Konto für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent an den Datenbankadministrator gehen möglicherweise **danw@Adventure-Works.com**.  
  
 [ **@description** = ] **'***description***'**  
 Eine Beschreibung des Kontos *Beschreibung* ist **nvarchar(256)**, hat den Standardwert NULL.  
  
 [ **@mailserver_name** =] **"***Server_name***"**  
 Der Name oder die IP-Adresse des SMTP-Mailservers, der für dieses Konto verwendet werden soll. Der Computer mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muss in der Lage, beheben Sie die *Server_name* in eine IP-Adresse. *Server_name* ist **Sysname**, hat keinen Standardwert.  
  
 [ **@mailserver_type** =] '*Server_type*"  
 Der Typ des e-Mail-Server. *Server_type* ist **Sysname**, hat den Standardwert **'SMTP'**...  
  
 [ **@port** =] *Port_number*  
 Die Portnummer für den E-Mail-Server. *Port_number* ist **Int**, Standardwert ist 25.  
  
 [ **@username** =] **"***Benutzername***"**  
 Der zum Anmelden beim E-Mail-Server zu verwendende Benutzername. *Benutzername* ist **vom Datentyp nvarchar(128)**, hat den Standardwert NULL. Wenn dieser Parameter NULL ist, verwendet Datenbank-E-Mail keine Authentifizierung für dieses Konto. Wenn für den Mailserver keine Authentifizierung erforderlich ist, verwenden Sie NULL als Wert für den Benutzernamen.  
  
 [ **@password** =] **"***Kennwort***"**  
 Das Kennwort, das für die Anmeldung beim E-Mail-Server verwendet werden soll. *Kennwort* ist **vom Datentyp nvarchar(128)**, hat den Standardwert NULL. Ein Kennwort muss nur bereitgestellt werden, wenn ein Benutzername angegeben wird.  
  
 [ **@use_default_credentials** =] Use_default_credentials  
 Gibt an, ob E-Mail mithilfe der Anmeldeinformationen von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] an den SMTP-Server gesendet wird. **Use_default_credentials** bit und hat den Standardwert 0. Wenn dieser Parameter 1 ist, verwendet Datenbank-E-Mail die Anmeldeinformationen von [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Wenn dieser Parameter 0 ist, sendet Datenbank-Mail die **@username** und **@password** Parameter, soweit vorhanden, andernfalls sendet e-Mail ohne **@username**und **@password** Parameter.  
  
 [ **@enable_ssl** =] Enable_ssl  
 Gibt an, ob Database Mail die Kommunikation über Secure Sockets Layer verschlüsselt. **Enable_ssl** bit und hat den Standardwert 0.  
  
 [ **@account_id** =] *Account_id* Ausgabe  
 Gibt die Konto-ID für das neue Konto zurück. *account_id* ist vom Datentyp **int**und hat den Standardwert NULL.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 Database Mail stellt separate Parameter für **@email_address**, **@display_name**, und **@replyto_address**. Die **@email_address** Parameter ist die Adresse, von dem die Nachricht gesendet wird. Die **@display_name** Parameter gibt den Namen der **aus:** -Feld der e-Mail-Nachricht. Die **@replyto_address** Parameter ist die Adresse, an die e-Mail-Nachricht Antworten gesendet werden. Beispiel: Ein Konto, das für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent verwendet wird, soll E-Mail-Nachrichten von einer E-Mail-Adresse senden, die nur für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent verwendet wird. Nachrichten von dieser Adresse sollen über einen Anzeigenamen verfügen, sodass die Empfänger problemlos feststellen können, dass die Nachricht vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent gesendet wurde. Wenn ein Empfänger auf die Nachricht antwortet, soll die Antwort an den Datenbankadministrator und nicht an die vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent verwendete Adresse gesendet werden. In diesem Szenario verwendet das Konto **SqlAgent@Adventure-Works.com** als e-Mail-Adresse. Der Anzeigename wird festgelegt, um **SQL Server Agent Automated Mailer**. Verwendet das Konto **danw@Adventure-Works.com** als Antwortadresse, sodass Antworten auf die von diesem Konto versendeten Nachrichten wechseln Sie zur Datenbankadministrator und nicht auf die e-Mail-Adresse für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Durch die Bereitstellung unabhängiger Einstellungen für diese drei Parameter ermöglicht es Datenbank-E-Mail Ihnen, die Konfiguration von Nachrichten an Ihre Anforderungen anzupassen.  
  
 Die **@mailserver_type** -Parameter unterstützt den Wert **'SMTP'**.  
  
 Wenn **@use_default_credentials** 1 Mail wird gesendet, mit dem SMTP-Server mit den Anmeldeinformationen des ist die [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Wenn **@use_default_credentials** 0 ist und ein **@username** und **@password** sind für ein Konto angegeben, verwendet das Konto SMTP-Authentifizierung. Die **@username** und **@password** sind die Anmeldeinformationen für den SMTP-Server nicht die Anmeldeinformationen für die von diesem Konto verwendet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oder das Netzwerk, das der Computer befindet.  
  
 Die gespeicherte Prozedur **Sysmail_add_account_sp** befindet sich in der **Msdb** Datenbank und im Besitz der **Dbo** Schema. Handelt es sich bei der aktuellen Datenbank nicht um **msdb**, muss die Prozedur mit einem dreiteiligen Namen ausgeführt werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Über die Ausführungsberechtigungen für diese Prozedur verfügen standardmäßig die Mitglieder der festen Serverrolle **sysadmin** .  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird ein Konto mit dem Namen `AdventureWorks Administrator` erstellt. Das Konto verwendet die E-Mail-Adresse `dba@Adventure-Works.com` und sendet E-Mail-Nachrichten an den SMTP-Mailserver `smtp.Adventure-Works.com`. E-Mail-Nachrichten aus diesem Konto zeigen `AdventureWorks Automated Mailer` auf die **aus:** Zeile einer Nachricht. Antworten auf Nachrichten von diesem Konto werden an `danw@Adventure-Works.com` gesendet.  
  
```  
EXECUTE msdb.dbo.sysmail_add_account_sp  
    @account_name = 'AdventureWorks Administrator',  
    @description = 'Mail account for administrative e-mail.',  
    @email_address = 'dba@Adventure-Works.com',  
    @display_name = 'AdventureWorks Automated Mailer',  
    @mailserver_name = 'smtp.Adventure-Works.com' ;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbank-E-Mail](../../relational-databases/database-mail/database-mail.md)   
 [Erstellen eines Datenbank-Mail-Kontos](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Database Mail gespeicherte Prozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  

---
title: Sysmail_add_profileaccount_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
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
- sysmail_add_profileaccount_sp
- sysmail_add_profileaccount_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_add_profileaccount_sp
ms.assetid: 7cbf430f-1997-45ea-9707-0086184de744
caps.latest.revision: 42
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 095d532c5b7506b62389a927f00b9da168c4b63f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysmailaddprofileaccountsp-transact-sql"></a>sysmail_add_profileaccount_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Fügt einem Profil für die Datenbank-E-Mail ein Konto für die Datenbank-E-Mail hinzu. Führen Sie **Sysmail_add_profileaccount_sp** nach Erstellen eines Datenbankkontos mit [Sysmail_add_account_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-add-account-sp-transact-sql.md), und eines Profils für Datenbank wird erstellt, mit [Sysmail_add_profile_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-add-profile-sp-transact-sql.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sysmail_add_profileaccount_sp { [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' } ,  
    { [ @account_id = ] account_id | [ @account_name = ] 'account_name' }  
    [ , [ @sequence_number = ] sequence_number ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@profile_id** =] *Profile_id*  
 Die Profil-ID, der das Konto hinzugefügt wird. *profile_id* ist vom Datentyp **int**und hat den Standardwert NULL. Es muss entweder *profile_id* oder *profile_name* angegeben werden.  
  
 [ **@profile_name** =] **"***Profile_name***"**  
 Der Profilname, dem das Konto hinzugefügt wird. *profile_name* ist vom Datentyp **sysname**und hat den Standardwert NULL. Es muss entweder *profile_id* oder *profile_name* angegeben werden.  
  
 [ **@account_id** =] *Account_id*  
 Die Konto-ID, die dem Profil hinzugefügt wird. *account_id* ist vom Datentyp **int**und hat den Standardwert NULL. Es muss entweder *account_id* oder *account_name* angegeben werden.  
  
 [ **@account_name** =] **"***Account_name***"**  
 Der Name des Kontos, das dem Profil hinzugefügt wird. *account_name* ist vom Datentyp **sysname**und hat den Standardwert NULL. Es muss entweder *account_id* oder *account_name* angegeben werden.  
  
 [ **@sequence_number** =] *Sequence_number*  
 Die Sequenznummer des Kontos innerhalb des Profils. *sequence_number* ist vom Datentyp **int**und hat keinen Standardwert. Über die Sequenznummer wird die Reihenfolge festgelegt, in der Konten im Profil verwendet werden.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 Sowohl das Profil als auch das Konto müssen bereits vorhanden sein. Andernfalls gibt die gespeicherte Prozedur einen Fehler zurück.  
  
 Beachten Sie, dass diese gespeicherte Prozedur nicht die Sequenznummer eines Kontos ändert, das bereits dem angegebenen Profil zugeordnet ist. Weitere Informationen zum Aktualisieren der Sequenznummer eines Kontos finden Sie unter [Sysmail_update_profileaccount_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-update-profileaccount-sp-transact-sql.md).  
  
 Über die Sequenznummer wird die Reihenfolge festgelegt, in der Konten im Profil von Datenbank-E-Mail verwendet werden. Für eine neue E-Mail-Nachricht beginnt Datenbank-E-Mail mit dem Konto mit der niedrigsten Sequenznummer. Wenn dieses Konto fehlschlägt, verwendet Datenbank-E-Mail das Konto mit der nächsthöheren Sequenznummer usw., bis entweder Datenbank-E-Mail die Nachricht erfolgreich versendet oder das Konto mit der höchsten Sequenznummer fehlschlägt. Wenn das Konto mit der höchsten Sequenznummer fehlschlägt, unterbricht die Datenbank-E-Mail die Versuche zum Senden der E-Mail für den Zeitraum, der im *AccountRetryDelay* -Parameter von **sysmail_configure_sp**konfiguriert ist. Danach wird das Senden der E-Mail erneut gestartet, wobei mit der niedrigsten Sequenznummer begonnen wird. Verwenden Sie den *AccountRetryAttempts* -Parameter von **sysmail_configure_sp**, um zu konfigurieren, wie oft der externe Mailprozess versuchen soll, die E-Mail-Nachricht mithilfe der einzelnen Konten im angegebenen Profil zu senden.  
  
 Sind mehrere Konten mit der gleichen Sequenznummer vorhanden, verwendet die Datenbank-E-Mail nur eines dieser Konten für eine bestimmte E-Mail-Nachricht. In diesem Fall kann Datenbank-E-Mail nicht sicherstellen, welches der Konten für diese Sequenznummer verwendet wird oder dass für die einzelnen Nachrichten jeweils dasselbe Konto verwendet wird.  
  
 Die gespeicherte Prozedur **sysmail_add_profileaccount_sp** befindet sich in der **msdb** -Datenbank mit dem **dbo** -Schema als Besitzer. Handelt es sich bei der aktuellen Datenbank nicht um **msdb**, muss die Prozedur mit einem dreiteiligen Namen ausgeführt werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Über die Ausführungsberechtigungen für diese Prozedur verfügen standardmäßig die Mitglieder der festen Serverrolle **sysadmin** .  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird das Profil `AdventureWorks Administrator` dem Konto `Audit Account`zugeordnet. Das Konto für die Überwachung weist die Sequenznummer 1 auf.  
  
```  
EXECUTE msdb.dbo.sysmail_add_profileaccount_sp  
    @profile_name = 'AdventureWorks Administrator',  
    @account_name = 'Audit Account',  
    @sequence_number = 1 ;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbank-E-Mail](../../relational-databases/database-mail/database-mail.md)   
 [Erstellen eines Datenbank-Mail-Kontos](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Database Mail Configuration Objects](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Database Mail gespeicherte Prozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  

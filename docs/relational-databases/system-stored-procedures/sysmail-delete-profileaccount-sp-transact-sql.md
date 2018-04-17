---
title: Sysmail_delete_profileaccount_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
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
- sysmail_delete_profileaccount_sp
- sysmail_delete_profileaccount_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_delete_profileaccount_sp
ms.assetid: b58d06f2-d6c9-4c8e-95bd-027c50f4621a
caps.latest.revision: 45
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0f80f3e20b32cb7571e1be5e77aa9eba1256dc74
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysmaildeleteprofileaccountsp-transact-sql"></a>sysmail_delete_profileaccount_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Entfernt ein Konto aus einem Datenbank-E-Mail-Profil.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sysmail_delete_profileaccount_sp  {   [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' } ,  
    {   [ @account_id = ] account_id | [ @account_name = ] 'account_name' }  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@profile_id** =] *Profile_id*  
 Die Profil-ID des Profils, das gelöscht werden soll. *profile_id* ist vom Datentyp **int**und hat den Standardwert NULL. Es kann entweder *profile_id* oder *profile_name* angegeben werden.  
  
 [ **@profile_name** =] **"***Profile_name***"**  
 Der Name des Profils, das gelöscht werden soll. *profile_name* ist vom Datentyp **sysname**und hat den Standardwert NULL. Es kann entweder *profile_id* oder *profile_name* angegeben werden.  
  
 [ **@account_id** =] *Account_id*  
 Die zu löschende Konto-ID. *account_id* ist vom Datentyp **int**und hat den Standardwert NULL. Es kann entweder *account_id* oder *account_name* angegeben werden.  
  
 [ **@account_name** =] **"***Account_name***"**  
 Der Name des zu löschenden Kontos. *account_name* ist vom Datentyp **sysname**und hat den Standardwert NULL. Es kann entweder *account_id* oder *account_name* angegeben werden.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="remarks"></a>Hinweise  
 Gibt einen Fehler zurück, wenn das angegebene Konto dem angegebenen Profil nicht zugeordnet ist.  
  
 Ist ein Konto angegeben, jedoch kein Profil, entfernt diese gespeicherte Prozedur das angegebene Konto aus allen Profilen. Wenn Sie z. B. das Herunterfahren eines vorhandenen SMTP-Servers vorbereiten, entfernen Sie Konten, die diesen SMTP-Server verwenden, aus allen Profilen, anstatt jedes Konto aus jedem einzelnen Profil zu entfernen.  
  
 Ist ein Profil angegeben, jedoch kein Konto, entfernt diese gespeicherte Prozedur alle Konten aus dem angegebenen Profil. Wenn Sie z. B. die von einem Profil verwendeten SMTP-Server ändern, können Sie alle Konten aus dem Profil entfernen und dann bei Bedarf neue Konten hinzufügen.  
  
 Die gespeicherte Prozedur **sysmail_delete_profileaccount_sp** wird in der **msdb** -Datenbank gespeichert und befindet sich im Besitz des **dbo** -Schemas. Handelt es sich bei der aktuellen Datenbank nicht um **msdb**, muss die Prozedur mit einem dreiteiligen Namen ausgeführt werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Über die Ausführungsberechtigungen für diese Prozedur verfügen standardmäßig die Mitglieder der festen Serverrolle **sysadmin** .  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird das Konto `Audit Account` aus dem Profil `AdventureWorks Administrator`entfernt.  
  
```  
EXECUTE msdb.dbo.sysmail_delete_profileaccount_sp  
    @profile_name = 'AdventureWorks Administrator',  
    @account_name = 'Audit Account' ;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbank-E-Mail](../../relational-databases/database-mail/database-mail.md)   
 [Erstellen eines Datenbank-Mail-Kontos](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Database Mail Configuration Objects](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Database Mail gespeicherte Prozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  

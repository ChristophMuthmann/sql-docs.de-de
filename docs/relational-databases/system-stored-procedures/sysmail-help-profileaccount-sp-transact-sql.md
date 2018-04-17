---
title: Sysmail_help_profileaccount_sp (Transact-SQL) | Microsoft Docs
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
- sysmail_help_profileaccount_sp_TSQL
- sysmail_help_profileaccount_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_help_profileaccount_sp
ms.assetid: 3ea68271-0a6b-4d77-991c-4757f48f747a
caps.latest.revision: 43
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 652fa8630640233427df040b155ca283b7041d74
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysmailhelpprofileaccountsp-transact-sql"></a>sysmail_help_profileaccount_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Listet die Konten auf, die einem oder mehreren Datenbank-E-Mail-Profilen zugeordnet sind.  
    
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sysmail_help_profileaccount_sp  
   {   [ @profile_id = ] profile_id   
      | [ @profile_name = ] 'profile_name' }  
   [ , {   [ @account_id = ] account_id  
         | [ @account_name = ] 'account_name' } ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@profile_id** =] *Profile_id*  
 Die ID des Profils, das aufgelistet werden soll. *profile_id* ist vom Datentyp **int**und hat den Standardwert NULL. Es muss entweder *profile_id* oder *profile_name* angegeben werden.  
  
 [ **@profile_name** =] **"***Profile_name***"**  
 Der Name des Profils, das aufgelistet werden soll. *profile_name* ist vom Datentyp **sysname**und hat den Standardwert NULL. Es muss entweder *profile_id* oder *profile_name* angegeben werden.  
  
 [ **@account_id** =] *Account_id*  
 Die ID des Kontos, das aufgelistet werden soll. *account_id* ist vom Datentyp **int**und hat den Standardwert NULL. Wenn *account_id* sowie *account_name* NULL sind, werden alle Konten im Profil aufgelistet.  
  
 [ **@account_name** =] **"***Account_name***"**  
 Der Name des Kontos, das aufgelistet werden soll. *account_name* ist vom Datentyp **sysname**und hat den Standardwert NULL. Wenn *account_id* sowie *account_name* NULL sind, werden alle Konten im Profil aufgelistet.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Gibt ein Resultset mit den folgenden Spalten zurück.  
  
||||  
|-|-|-|  
|Spaltenname|Datentyp|Description|  
|**profile_id**|**int**|Die Profil-ID des Profils.|  
|**profile_name**|**sysname**|Der Name des Profils.|  
|**account_id**|**int**|Die Konto-ID des Kontos.|  
|**account_name**|**sysname**|Der Name des Kontos.|  
|**sequence_number**|**int**|Die Sequenznummer des Kontos innerhalb des Profils.|  
  
## <a name="remarks"></a>Hinweise  
 Wird weder *profile_id* noch *profile_name* angegeben, gibt diese gespeicherte Prozedur Informationen für jedes Profil in der Instanz zurück.  
  
 Die gespeicherte Prozedur **sysmail_help_profileaccount_sp** wird in der **msdb** -Datenbank gespeichert und befindet sich im Besitz des **dbo** -Schemas. Handelt es sich bei der aktuellen Datenbank nicht um **msdb**, muss die Prozedur mit einem dreiteiligen Namen ausgeführt werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Über die Ausführungsberechtigungen für diese Prozedur verfügen standardmäßig die Mitglieder der festen Serverrolle **sysadmin** .  
  
## <a name="examples"></a>Beispiele  
 **A. Auflisten der Konten für ein spezifisches Profil anhand des Namens**  
  
 Im folgenden Beispiel werden die Informationen für das `AdventureWorks Administrator` -Profil durch Angeben des Profilnamens aufgelistet.  
  
```  
EXECUTE msdb.dbo.sysmail_help_profileaccount_sp  
   @profile_name = 'AdventureWorks Administrator';  
```  
  
 Es folgt ein Beispielresultset, das auf Zeilenlänge umformatiert wurde:  
  
```  
profile_id  profile_name                 account_id  account_name         sequence_number  
----------- ---------------------------- ----------- -------------------- ---------------  
131         AdventureWorks Administrator 197         Admin-MainServer     1  
131         AdventureWorks Administrator 198         Admin-BackupServer   2  
```  
  
 **B. Auflisten der Konten für ein spezifisches Profil anhand der Profil-ID**  
  
 Im folgenden Beispiel werden die Informationen für das `AdventureWorks Administrator` -Profil durch Angeben der Profil-ID für das Profil aufgelistet.  
  
```  
EXECUTE msdb.dbo.sysmail_help_profileaccount_sp  
    @profile_id = 131 ;  
```  
  
 Es folgt ein Beispielresultset, das auf Zeilenlänge umformatiert wurde:  
  
```  
profile_id  profile_name                 account_id  account_name         sequence_number  
----------- ---------------------------- ----------- -------------------- ---------------  
131         AdventureWorks Administrator 197         Admin-MainServer     1  
131         AdventureWorks Administrator 198         Admin-BackupServer   2  
```  
  
 **C. Auflisten der Konten für alle Profile**  
  
 Im folgenden Beispiel werden die Informationen für alle Profile in der Instanz aufgelistet.  
  
```  
EXECUTE msdb.dbo.sysmail_help_profileaccount_sp;  
```  
  
 Es folgt ein Beispielresultset, das auf Zeilenlänge umformatiert wurde:  
  
```  
profile_id  profile_name                 account_id  account_name         sequence_number  
----------- ---------------------------- ----------- -------------------- ---------------  
131         AdventureWorks Administrator 197         Admin-MainServer     1  
131         AdventureWorks Administrator 198         Admin-BackupServer   2  
106         AdventureWorks Operator      210         Operator-MainServer  1  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbank-E-Mail](../../relational-databases/database-mail/database-mail.md)   
 [Erstellen eines Datenbank-Mail-Kontos](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Database Mail Configuration Objects](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Database Mail gespeicherte Prozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  

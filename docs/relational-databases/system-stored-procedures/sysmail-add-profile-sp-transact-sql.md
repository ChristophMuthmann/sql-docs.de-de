---
title: Sysmail_add_profile_sp (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
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
- sysmail_add_profile_sp_TSQL
- sysmail_add_profile_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_add_profile_sp
ms.assetid: a828e55c-633a-41cf-9769-a0698b446e6c
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6295b1f239f136c43e00e047186ce408ab9a4a93
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="sysmailaddprofilesp-transact-sql"></a>sysmail_add_profile_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Erstellt ein neues Profil für Datenbank-E-Mail.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sysmail_add_profile_sp [ @profile_name = ] 'profile_name'  
    [ , [ @description = ] 'description' ]  
    [ , [ @profile_id = ] new_profile_id OUTPUT ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@profile_name** = ] **'***profile_name***'**  
 Der Name des neuen Profils. *profile_name* ist vom Datentyp **sysname**und hat keinen Standardwert.  
  
 [ **@description** = ] **'***description***'**  
 Die optionale Beschreibung für das neue Profil. *Beschreibung* ist **nvarchar(256)**, hat keinen Standardwert.  
  
 [ **@profile_id** = ] *new_profile_id***OUTPUT**  
 Gibt die ID für das neue Profil zurück. *New_profile_id* ist **Int**, hat den Standardwert NULL.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 Ein Datenbank-E-Mail-Profil kann eine beliebige Anzahl von Datenbank-E-Mail-Konten enthalten. Gespeicherte Prozeduren von Datenbank-E-Mail können nach dem Profilnamen oder der von dieser Prozedur generierten Profil-ID auf ein Profil verweisen. Weitere Informationen zum Hinzufügen eines Kontos zu einem Profil finden Sie unter [Sysmail_add_profileaccount_sp &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sysmail-add-profileaccount-sp-transact-sql.md).  
  
 Der Profilname und Beschreibung können mit der gespeicherten Prozedur geändert werden **Sysmail_update_profile_sp**, während die Profil-Id für die Lebensdauer des Profils konstant bleibt.  
  
 Der Profilname muss für Microsoft [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] eindeutig sein. Andernfalls wird von der gespeicherten Prozedur ein Fehler zurückgegeben.  
  
 Die gespeicherte Prozedur **Sysmail_add_profile_sp** befindet sich in der **Msdb** Datenbank und im Besitz der **Dbo** Schema. Handelt es sich bei der aktuellen Datenbank nicht um **msdb**, muss die Prozedur mit einem dreiteiligen Namen ausgeführt werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Über die Ausführungsberechtigungen für diese Prozedur verfügen standardmäßig die Mitglieder der festen Serverrolle **sysadmin** .  
  
## <a name="examples"></a>Beispiele  
 **A. Erstellen eines neuen Profils**  
  
 Im folgenden Beispiel wird ein neues Datenbank-E-Mail-Profil mit dem Namen `AdventureWorks Administrator` erstellt.  
  
```  
EXECUTE msdb.dbo.sysmail_add_profile_sp  
       @profile_name = 'AdventureWorks Administrator',  
       @description = 'Profile used for administrative mail.' ;  
```  
  
 **B. Erstellen eines neuen Profils und speichern die Profil-Id in einer Variablen**  
  
 Im folgenden Beispiel wird ein neues Datenbank-E-Mail-Profil mit dem Namen `AdventureWorks Administrator` erstellt. Im folgenden Beispiel wird die Profil-ID in der Variablen `@profileId` gespeichert, und es wird ein Resultset mit der Profil-ID für das neue Profil zurückgegeben.  
  
```  
DECLARE @profileId INT ;  
  
EXECUTE msdb.dbo.sysmail_add_profile_sp  
       @profile_name = 'AdventureWorks Administrator',  
       @description = 'Profile used for administrative mail.',  
       @profile_id = @profileId OUTPUT ;  
  
SELECT @profileId ;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbank-E-Mail](../../relational-databases/database-mail/database-mail.md)   
 [Erstellen eines Datenbank-Mail-Kontos](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Database Mail Configuration Objects](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Database Mail gespeicherte Systemprozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  

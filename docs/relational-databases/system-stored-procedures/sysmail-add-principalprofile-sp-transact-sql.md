---
title: sysmail_add_profileaccount_sp (Transact-SQL) | Microsoft Docs
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
- sysmail_add_principalprofile_sp_TSQL
- sysmail_add_principalprofile_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_add_principalprofile_sp
ms.assetid: b2a0b313-abb9-4c23-8511-db77ca8172b3
caps.latest.revision: 36
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 177f6ea8ab1fa62c61b56b8e020fbb8288aad7c5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysmailaddprincipalprofilesp-transact-sql"></a>sysmail_add_principalprofile_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gewährt für einen Datenbankbenutzer oder eine Rolle die Berechtigung zum Verwenden eines Datenbank-E-Mail-Profils.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sysmail_add_principalprofile_sp  { [ @principal_id = ] principal_id | [ @principal_name = ] 'principal_name' } ,  
    { [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' }  
    [ , [ @is_default ] = 'is_default' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@principal_id** =] *Principal_id*  
 Die ID des Datenbankbenutzers oder der Datenbankrolle in der **msdb** -Datenbank für die Zuordnung. *principal_id* ist vom Datentyp **int**und hat den Standardwert NULL. Es muss entweder *principal_id* oder *principal_name* angegeben werden. Wenn *principal_id* auf **0** festgelegt ist, wird dieses Profil öffentlich, wobei der Zugriff auf alle Prinzipale in der Datenbank erteilt wird.  
  
 [ **@principal_name** =] **"***Principal_name***"**  
 Der Name des Datenbankbenutzers oder der Datenbankrolle in der **msdb** -Datenbank für die Zuordnung. *principal_name* ist vom Datentyp **sysname**und hat den Standardwert NULL. Es muss entweder *principal_id* oder *principal_name* angegeben werden. Wenn *principal_name* auf **'public'** festgelegt ist, wird dieses Profil öffentlich, wobei der Zugriff auf alle Prinzipale in der Datenbank erteilt wird.  
  
 [ **@profile_id** =] *Profile_id*  
 Die ID des Profils für die Zuordnung. *profile_id* ist vom Datentyp **int**und hat den Standardwert NULL. Es muss entweder *profile_id* oder *profile_name* angegeben werden.  
  
 [ **@profile_name** =] **"***Profile_name***"**  
 Die Name des Profils für die Zuordnung. *profile_name* ist vom Datentyp **sysname**und hat keinen Standardwert. Es muss entweder *profile_id* oder *profile_name* angegeben werden.  
  
 [ **@is_default** =] *Is_default*  
 Gibt an, ob dieses Profil das Standardprofil für den Prinzipal ist. Ein Prinzipal muss genau ein Standardprofil haben. *is_default* ist vom Datentyp **bit**und hat keinen Standardwert.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 Um ein Profil öffentlich zu machen, geben Sie einen **@principal_id** von **0** oder ein **@principal_name** von **öffentlichen**. Ein öffentliches Profil ist für alle Benutzer der **msdb** -Datenbank verfügbar. Allerdings müssen diese Benutzer auch Mitglieder von **DatabaseMailUserRole** sein, wenn sie **sp_send_dbmail**ausführen können sollen.  
  
 Ein Datenbankbenutzer kann nur ein Standardprofil besitzen. Wenn **@is_default** ist "**1**" und der Benutzer ist bereits einem oder mehreren Profilen zugeordnet, das angegebene Profil als Standardprofil für den Benutzer. Das zuvor als Standardprofil verwendete Profil ist dem Benutzer weiter zugeordnet, es ist jedoch nicht mehr als Standardprofil festgelegt.  
  
 Wenn **@is_default** ist "**0**" und keine andere Zuordnung vorhanden ist, wird die gespeicherte Prozedur gibt einen Fehler zurück.  
  
 Die gespeicherte Prozedur **sysmail_add_principalprofile_sp** befindet sich in der **msdb** -Datenbank mit dem **dbo** -Schema als Besitzer. Handelt es sich bei der aktuellen Datenbank nicht um **msdb**, muss die Prozedur mit einem dreiteiligen Namen ausgeführt werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Über die Ausführungsberechtigungen für diese Prozedur verfügen standardmäßig die Mitglieder der festen Serverrolle **sysadmin** .  
  
## <a name="examples"></a>Beispiele  
 **A. Erstellen einer Zuordnung und Festlegen des Standardprofils**  
  
 Im folgenden Beispiel wird eine Zuordnung zwischen dem Profil `AdventureWorks Administrator Profile` und dem **msdb** -Datenbankbenutzer `ApplicationUser`erstellt. Als Profil wird das Standardprofil des Benutzers verwendet.  
  
```  
EXECUTE msdb.dbo.sysmail_add_principalprofile_sp  
    @principal_name = 'ApplicationUser',  
    @profile_name = 'AdventureWorks Administrator Profile',  
    @is_default = 1 ;  
```  
  
 **B. Festlegen eines Profils als öffentliches Standardprofil**  
  
 In diesem Beispiel wird das Profil `AdventureWorks Public Profile` als öffentliches Standardprofil für Benutzer in der **msdb** -Datenbank festgelegt.  
  
```  
EXECUTE msdb.dbo.sysmail_add_principalprofile_sp  
    @principal_name = 'public',  
    @profile_name = 'AdventureWorks Public Profile',  
    @is_default = 1 ;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbank-E-Mail](../../relational-databases/database-mail/database-mail.md)   
 [Database Mail Configuration Objects](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Database Mail gespeicherte Prozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  

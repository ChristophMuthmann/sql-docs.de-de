---
title: Sysmail_update_profile_sp (Transact-SQL) | Microsoft Docs
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
- sysmail_update_profile_sp
- sysmail_update_profile_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_update_profile_sp
ms.assetid: eaedf7ce-a8d5-4ab9-99e0-d77d5be19e90
caps.latest.revision: 29
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f16d17779ed6c60ef91b89503f69259eb2093d74
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysmailupdateprofilesp-transact-sql"></a>sysmail_update_profile_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ändert die Beschreibung oder den Namen eines Datenbank-E-Mail-Profils.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sysmail_update_profile_sp [ [ @profile_id = ] profile_id , ] [ [ @profile_name = ] 'profile_name' , ]  
    [ [ @description = ] 'description' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@profile_id** =] *Profile_id*  
 Die zu aktualisierende Profil-ID. *profile_id* ist vom Datentyp **int**und hat den Standardwert NULL. Mindestens eine der *Profile_id* oder *Profile_name* muss angegeben werden. Werden beide Werte angegeben, wird der Name des Profils geändert.  
  
 [ **@profile_name** =] **"***Profile_name***"**  
 Der Name des zu aktualisierenden Profils oder der neue Name für das Profil. *profile_name* ist vom Datentyp **sysname**und hat den Standardwert NULL. Mindestens eine der *Profile_id* oder *Profile_name* muss angegeben werden. Werden beide Werte angegeben, wird der Name des Profils geändert.  
  
 [ **@description** = ] **'***description***'**  
 Die neue Beschreibung für das Profil. *Beschreibung* ist **nvarchar(256)**, hat den Standardwert NULL.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 Wenn sowohl die Profil-ID als auch der Profilname angegeben werden, wird der Name des Profils zum bereitgestellten Namen geändert und die Beschreibung des Profils aktualisiert. Wenn nur eins dieser Argumente bereitgestellt wird, wird die Beschreibung des Profils aktualisiert.  
  
 Die gespeicherte Prozedur **Sysmail_update_profile_sp** befindet sich in der **Msdb** Datenbank und im Besitz der **Dbo** Schema. Handelt es sich bei der aktuellen Datenbank nicht um **msdb**, muss die Prozedur mit einem dreiteiligen Namen ausgeführt werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Über die Ausführungsberechtigungen für diese Prozedur verfügen standardmäßig die Mitglieder der festen Serverrolle **sysadmin** .  
  
## <a name="examples"></a>Beispiele  
 **A. Ändern der Beschreibung eines Profils**  
  
 Im folgende Beispiel ändert die Beschreibung für das Profil mit dem Namen `AdventureWorks Administrator` in der **Msdb** Datenbank.  
  
```  
EXECUTE msdb.dbo.sysmail_update_profile_sp  
    @profile_name = 'AdventureWorks Administrator'  
    ,@description = 'Administrative mail profile.';  
```  
  
 **B. Ändern des Namens und der Beschreibung eines Profils**  
  
 Im folgenden Beispiel wird der Name und die Beschreibung des Profils mit der Profil-ID `750` geändert.  
  
```  
EXECUTE msdb.dbo.sysmail_update_profile_sp  
    @profile_id = 750  
    ,@profile_name = 'Operator'  
    ,@description = 'Profile to send alert e-mail to operators.';  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbank-E-Mail](../../relational-databases/database-mail/database-mail.md)   
 [Database Mail Configuration Objects](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Erstellen eines Datenbank-Mail-Kontos](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Database Mail gespeicherte Prozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  

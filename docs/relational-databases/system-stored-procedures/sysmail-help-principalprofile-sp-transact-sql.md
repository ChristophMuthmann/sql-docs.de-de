---
title: Sysmail_help_principalprofile_sp (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/02/2016
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
- sysmail_help_principalprofile_sp_TSQL
- sysmail_help_principalprofile_sp
dev_langs: TSQL
helpviewer_keywords: sysmail_help_principalprofile_sp
ms.assetid: 0cfd6464-09c7-4f03-9d25-58001c096a9e
caps.latest.revision: "43"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 322984b88e879adb952a1168b17178b8ffe20ae2
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysmailhelpprincipalprofilesp-transact-sql"></a>sysmail_help_principalprofile_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Führt Informationen zu Zuordnungen zwischen Datenbank-E-Mail-Profilen und Datenbankprinzipalen auf.  
  
 
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sysmail_help_principalprofile_sp [ {   [ @principal_id = ] principal_id | [ @principal_name = ] 'principal_name' } ]  
    [ [ , ] {   [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' } ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@principal_id=** ] *Principal_id*  
 Die ID des Datenbankbenutzers oder der Rolle in der **Msdb** Datenbank für die Zuordnung, die aufgelistet. *principal_id* ist vom Datentyp **int**und hat den Standardwert NULL. Es kann entweder *principal_id* oder *principal_name* angegeben werden.  
  
 [  **@principal_name=** ] **"***Principal_name***"**  
 Der Name des Datenbankbenutzers oder der Rolle in der **Msdb** Datenbank für die Zuordnung, die aufgelistet. *principal_name* ist vom Datentyp **sysname**und hat den Standardwert NULL. Es kann entweder *principal_id* oder *principal_name* angegeben werden.  
  
 [  **@profile_id=** ] *Profile_id*  
 Die ID des Profils für die Zuordnung, die aufgelistet werden soll. *profile_id* ist vom Datentyp **int**und hat den Standardwert NULL. Entweder *Profile_id* oder *Profile_name* kann angegeben werden.  
  
 [  **@profile_name=** ] **"***Profile_name***"**  
 Der Name des Profils für die Zuordnung, die aufgelistet werden soll. *profile_name* ist vom Datentyp **sysname**und hat den Standardwert NULL. Entweder *Profile_id* oder *Profile_name* kann angegeben werden.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Gibt ein Resultset zurück, das die in der folgenden Tabelle aufgelisteten Spalten enthält.  
  
||||  
|-|-|-|  
|Spaltenname|Datentyp|Description|  
|**principal_id**|**int**|Die ID des Datenbankbenutzers.|  
|**principal_name**|**sysname**|Der Name des Datenbankbenutzers.|  
|**profile_id**|**int**|Die ID des Datenbank-E-Mail-Profils.|  
|**Profilname**|**sysname**|Der Name des Datenbank-E-Mail-Profils.|  
|**is_default**|**bit**|Das Flag, das besagt, ob es sich bei dem Profil um das Standardprofil des Benutzers handelt.|  
  
## <a name="remarks"></a>Hinweise  
 Wenn **Sysmail_help_principalprofile_sp** wird aufgerufen, ohne Angabe von Parametern das zurückgegebene Resultset enthält alle Zuordnungen in der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Andernfalls enthält das Resultset Informationen zu Zuordnungen, die mit den bereitgestellten Parametern übereinstimmen. So listet beispielsweise die Prozedur alle Zuordnungen für ein Profil auf, wenn der Profilname bereitgestellt wird.  
  
 **Sysmail_help_principalprofile_sp** befindet sich in der **Msdb** Datenbank und im Besitz der **Dbo** Schema. Handelt es sich bei der aktuellen Datenbank nicht um **msdb**, muss die Prozedur mit einem dreiteiligen Namen ausgeführt werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der festen Serverrolle **sysadmin** .  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-listing-information-for-a-specific-association"></a>A. Auflisten von Informationen für eine bestimmte Zuordnung  
 Im folgenden Beispiel werden die Informationen für alle Zuordnungen zwischen dem Profil `AdventureWorks Administrator` und dem Prinzipal `ApplicationLogin` in der `msdb`-Datenbank aufgelistet.  
  
```  
EXECUTE msdb.dbo.sysmail_help_principalprofile_sp  
    @principal_name = 'danw',  
    @profile_name = 'AdventureWorks Administrator' ;  
```  
  
 Es folgt ein Beispielresultset, das auf Zeilenlänge umformatiert wurde.  
  
```  
principal_id principal_name     profile_id  profile_name                   is_default  
------------ ------------------ ----------- ------------------------------ ----------  
5            danw               9           AdventureWorks Administrator   1  
```  
  
### <a name="b-listing-information-for-all-associations"></a>B. Auflisten von Informationen für alle Zuordnungen  
 Im folgenden Beispiel werden die Informationen für alle Zuordnungen in der Instanz aufgelistet.  
  
```  
EXECUTE msdb.dbo.sysmail_help_principalprofile_sp ;  
```  
  
 Es folgt ein Beispielresultset, das auf Zeilenlänge umformatiert wurde.  
  
```  
principal_id principal_name     profile_id  profile_name                   is_default  
------------ ------------------ ----------- ------------------------------ ----------  
6            terrid             3           Product Update Profile         1  
5            danw               9           AdventureWorks Administrator   1  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbank-E-Mail](../../relational-databases/database-mail/database-mail.md)   
 [Database Mail gespeicherte Systemprozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  

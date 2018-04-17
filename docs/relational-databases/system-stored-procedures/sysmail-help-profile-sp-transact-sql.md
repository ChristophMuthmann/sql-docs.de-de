---
title: Sysmail_help_profile_sp (Transact-SQL) | Microsoft Docs
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
- sysmail_help_profile_sp_TSQL
- sysmail_help_profile_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_help_profile_sp
ms.assetid: d7169a8e-92b1-49eb-9124-3b2f69755ddb
caps.latest.revision: 41
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6673c252203235679464950af1fdf019ecaf843e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysmailhelpprofilesp-transact-sql"></a>sysmail_help_profile_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Führt Informationen zu mindestens einem Mailprofil auf.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sysmail_help_profile_sp  [   [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@profile_id** =] *Profile_id*  
 Die Profil-ID, zu der Informationen zurückgegeben werden sollen. *profile_id* ist vom Datentyp **int**und hat den Standardwert NULL.  
  
 [ **@profile_name** =] **"***Profile_name***"**  
 Der Profilname, zu dem Informationen zurückgegeben werden sollen. *profile_name* ist vom Datentyp **sysname**und hat den Standardwert NULL.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Gibt ein Resultset mit den folgenden Spalten zurück.  
  
||||  
|-|-|-|  
|Spaltenname|Datentyp|Description|  
|**profile_id**|**int**|Die Profil-ID des Profils.|  
|**name**|**sysname**|Der Profilname des Profils.|  
|**description**|**nvarchar(256)**|Die Beschreibung des Profils.|  
  
## <a name="remarks"></a>Hinweise  
 Wenn ein Profilname oder eine Profil-ID angegeben ist, gibt **sysmail_help_profile_sp** Informationen zu diesem Profil zurück. Andernfalls **Sysmail_help_profile_sp** gibt Informationen zu jedem Profil in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instanz.  
  
 Die gespeicherte Prozedur **sysmail_help_profile_sp** befindet sich in der **msdb** -Datenbank und im Besitz des **dbo** -Schemas. Handelt es sich bei der aktuellen Datenbank nicht um **msdb**, muss die Prozedur mit einem dreiteiligen Namen ausgeführt werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Über die Ausführungsberechtigungen für diese Prozedur verfügen standardmäßig die Mitglieder der festen Serverrolle **sysadmin** .  
  
## <a name="examples"></a>Beispiele  
 **A. Auflisten aller Profile**  
  
 Im folgenden Beispiel werden alle Profile in der Instanz aufgelistet.  
  
```  
EXECUTE msdb.dbo.sysmail_help_profile_sp;  
```  
  
 Es folgt ein Beispielresultset, das auf Zeilenlänge umformatiert wurde:  
  
```  
profile_id  name                          description  
----------- ----------------------------- ------------------------------  
56          AdventureWorks Administrator  Administrative mail profile.    
57          AdventureWorks Operator       Operator mail profile.          
```  
  
 **B. Auflisten eines bestimmten Profils**  
  
 Im folgenden Beispiel werden Informationen für das `AdventureWorks Administrator`-Profil aufgelistet.  
  
```  
EXECUTE msdb.dbo.sysmail_help_profile_sp  
    @profile_name = 'AdventureWorks Administrator' ;  
```  
  
 Es folgt ein Beispielresultset, das auf Zeilenlänge umformatiert wurde:  
  
```  
profile_id  name                          description  
----------- ----------------------------- ------------------------------  
56          AdventureWorks Administrator  Administrative mail profile.    
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbank-E-Mail](../../relational-databases/database-mail/database-mail.md)   
 [Database Mail gespeicherte Prozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  

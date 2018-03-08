---
title: Sp_helpsrvrolemember (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- sp_helpsrvrolemember
- sp_helpsrvrolemember_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_helpsrvrolemember
ms.assetid: d0714913-8d6b-4de3-b042-3ae9934f839d
caps.latest.revision: "27"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 36c1ac793a550b453508928b6544e95ed20b37b5
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="sphelpsrvrolemember-transact-sql"></a>sp_helpsrvrolemember (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt Informationen zu Mitgliedern einer festen Serverrolle von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_helpsrvrolemember [ [ @srvrolename = ] 'role' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@srvrolename =** ] **"***Rolle***"**  
 Der Name einer festen Serverrolle. *role* ist vom Datentyp **sysname**und hat den Standardwert NULL. Wenn *Rolle*nicht angegeben ist, enthält das Resultset Informationen zu allen festen Serverrollen.  
  
 *Rolle* kann eines der folgenden Werte sein.  
  
|Feste Serverrolle|Description|  
|-----------------------|-----------------|  
|sysadmin|Systemadministratoren|  
|securityadmin|Sicherheitsadministratoren|  
|serveradmin|Serveradministratoren|  
|setupadmin|Setupadministratoren|  
|processadmin|Prozessadministratoren|  
|diskadmin|Datenträgeradministratoren|  
|dbcreator|Datenbankersteller|  
|bulkadmin|Kann BULK INSERT-Anweisungen ausführen|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Beschreibung|  
|-----------------|---------------|-----------------|  
|ServerRole|**sysname**|Name der Serverrolle.|  
|MemberName|**sysname**|Name eines Mitglieds von ServerRole|  
|MemberSID|**varbinary (85)**|Sicherheits-ID von MemberName|  
  
## <a name="remarks"></a>Hinweise  
 Verwenden Sie Sp_helprolemember, um die Mitglieder einer Datenbankrolle anzuzeigen.  
  
 Alle Anmeldenamen sind Mitglied der Public. Sp_helpsrvrolemember erkennt die public-Rolle nicht, da intern, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht öffentlichen als Rolle implementiert.  
  
 Hinzufügen oder Entfernen von Serverrollen, Mitgliedern finden Sie unter [ALTER SERVER ROLE &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-server-role-transact-sql.md).  
  
 Sp_helpsrvrolemember akzeptiert eine benutzerdefinierte Serverrolle als Argument. Um die Mitglieder einer benutzerdefinierten Serverrolle zu ermitteln, finden Sie unter den Beispielen in [ALTER SERVER ROLE &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-server-role-transact-sql.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der public-Rolle.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel listet die Mitglieder der festen Serverrolle `sysadmin` auf.  
  
```  
EXEC sp_helpsrvrolemember 'sysadmin';  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_helprole &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helprole-transact-sql.md)   
 [Sp_helprolemember &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helprolemember-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [Sicherheitsfunktionen &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  

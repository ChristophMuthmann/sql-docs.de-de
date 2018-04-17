---
title: Sp_helpsrvrole (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
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
- sp_helpsrvrole_TSQL
- sp_helpsrvrole
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpsrvrole
ms.assetid: 5c7f39f3-c261-4f70-8beb-08242d4ac242
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d9427712cb6a55ae5b42962b8a117d11db1c5268
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sphelpsrvrole-transact-sql"></a>sp_helpsrvrole (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt eine Liste der festen Serverrollen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_helpsrvrole [ [ @srvrolename = ] 'role' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@srvrolename=** ] **"***Rolle***"**  
 Der Name der festen Serverrolle. *role* ist vom Datentyp **sysname**und hat den Standardwert NULL. *Rolle* kann einen der folgenden Werte sein.  
  
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
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|ServerRole|**sysname**|Name der Serverrolle.|  
|Description|**sysname**|Beschreibung des ServerRole|  
  
## <a name="remarks"></a>Hinweise  
 Feste Serverrollen werden auf Serverebene definiert und haben Berechtigungen, um spezifische Verwaltungsfunktionen auf Serverebene auszuführen. Feste Serverrollen können nicht hinzugefügt, entfernt oder geändert werden.  
  
 Hinzufügen oder Entfernen von Serverrollen, Mitgliedern finden Sie unter [ALTER SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-role-transact-sql.md).  
  
 Alle Anmeldenamen sind Mitglied der Public. Sp_helpsrvrole erkennt die public-Rolle nicht, da intern, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht öffentlichen als Rolle implementiert.  
  
 Sp_helpsrvrole akzeptiert eine benutzerdefinierte Serverrolle als Argument. So Listen Sie die benutzerdefinierten Serverrollen finden Sie unter den Beispielen in [ALTER SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-role-transact-sql.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der public-Rolle.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-listing-the-fixed-server-roles"></a>A. Auflisten der festen Serverrollen  
 Die folgende Abfrage gibt eine Liste fester Serverrollen zurück.  
  
```  
EXEC sp_helpsrvrole ;  
```  
  
### <a name="b-listing-fixed-and-user-defined-server-roles"></a>B. Auflisten fester und benutzerdefinierter Serverrollen  
 Die folgende Abfrage gibt eine Liste fester und benutzerdefinierter Serverrollen zurück.  
  
```  
SELECT * FROM sys.server_principals WHERE type = 'R' ;  
```  
  
### <a name="c-returning-a-description-of-a-fixed-server-role"></a>C. Zurückgeben einer Beschreibung für eine feste Serverrolle  
 Die folgende Abfrage gibt den Namen und den Speicherort der festen Serverrollen von `diskadmin` zurück.  
  
```  
sp_helpsrvrole 'diskadmin' ;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Security Stored Procedures &#40;Transact-SQL&#41; (Gespeicherte Sicherheitsprozeduren (Transact-SQL))](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [Rollen auf Serverebene](../../relational-databases/security/authentication-access/server-level-roles.md)   
 [sp_addsrvrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md)   
 [Sp_dropsrvrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsrvrolemember-transact-sql.md)   
 [Sp_helpsrvrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsrvrolemember-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

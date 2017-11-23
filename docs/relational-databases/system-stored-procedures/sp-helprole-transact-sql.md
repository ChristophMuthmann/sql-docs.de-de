---
title: Sp_helprole (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_helprole_TSQL
- sp_helprole
dev_langs: TSQL
helpviewer_keywords: sp_helprole
ms.assetid: b023103f-ccf3-44e2-b418-4be9bdd49f4a
caps.latest.revision: "27"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3a912cb79346ea35e7da110ed336138231e28ee1
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="sphelprole-transact-sql"></a>sp_helprole (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt Informationen zu den Rollen in der aktuellen Datenbank zurück.  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_helprole [ [ @rolename = ] 'role' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@rolename =** ] **"***Rolle***"**  
 Der Name der Datenbankrolle in der aktuellen Datenbank. *role* ist vom Datentyp **sysname**und hat den Standardwert NULL. *role* muss in der aktuellen Datenbank vorhanden sein. Falls *role* nicht angegeben wird, werden Informationen zu allen Rollen in der aktuellen Datenbank zurückgegeben.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**RoleName**|**sysname**|Name der Rolle in der aktuellen Datenbank.|  
|**RoleID-Wert**|**smallint**|ID von **RoleName**.|  
|**IsAppRole**|**int**|0 = **RoleName** ist keine Anwendungsrolle.<br /><br /> 1 = **RoleName** ist eine Anwendungsrolle.|  
  
## <a name="remarks"></a>Hinweise  
 Mithilfe von **sp_helprotect**zeigen Sie die Berechtigungen an, die einer Rolle zugeordnet sind. Mithilfe von **sp_helprolemember**zeigen Sie die Mitglieder einer Datenbankrolle an.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **public** -Rolle.  
  
## <a name="examples"></a>Beispiele  
 Die folgende Abfrage gibt alle Rollen in der aktuellen Datenbank zurück.  
  
```  
EXEC sp_helprole  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Systemprozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [Rollen auf Serverebene](../../relational-databases/security/authentication-access/server-level-roles.md)   
 [Rollen auf Datenbankebene](../../relational-databases/security/authentication-access/database-level-roles.md)   
 [Sp_addapprole &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addapprole-transact-sql.md)   
 [sp_addrole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrole-transact-sql.md)   
 [sp_droprole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droprole-transact-sql.md)   
 [Sp_helprolemember &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helprolemember-transact-sql.md)   
 [Sp_helpsrvrolemember &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpsrvrolemember-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

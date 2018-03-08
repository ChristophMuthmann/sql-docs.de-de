---
title: Sp_droprolemember (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_droprolemember_TSQL
- sp_droprolemember
dev_langs: TSQL
helpviewer_keywords: sp_droprolemember
ms.assetid: c2f19ab1-e742-4d56-ba8e-8ffd40cf4925
caps.latest.revision: "39"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f261d0908232bd9d1f61214b0af87b732a27974d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spdroprolemember-transact-sql"></a>sp_droprolemember (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Entfernt ein Sicherheitskonto aus einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Rolle in der aktuellen Datenbank.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Verwendung [ALTER ROLE](../../t-sql/statements/alter-role-transact-sql.md) stattdessen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
sp_droprolemember [ @rolename = ] 'role' ,   
     [ @membername = ] 'security_account'  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_droprolemember 'role' ,  
     'security_account'  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@rolename =** ] **"***Rolle***"**  
 Der Name der Rolle, aus der das Element entfernt wird. *Rolle* ist **Sysname**, hat keinen Standardwert. *role* muss in der aktuellen Datenbank vorhanden sein.  
  
 [  **@membername =** ] **"***Security_account***"**  
 Der Name des Sicherheitskontos, das aus der Rolle entfernt wird. *Security_account* ist **Sysname**, hat keinen Standardwert. *Security_account* kann ein Datenbankbenutzer, eine andere Datenbankrolle, ein Windows-Anmeldename oder eine Windows-Gruppe sein. *Security_account* muss in der aktuellen Datenbank vorhanden sein.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 Sp_droprolemember entfernt ein Mitglied aus einer Datenbankrolle, durch das Löschen einer Zeile aus der Tabelle Sysmembers. Wenn ein Mitglied aus einer Rolle entfernt wird, verliert das Mitglied alle Berechtigungen, die es aufgrund seiner Mitgliedschaft in dieser Rolle hat.  
  
 Um einen Benutzer aus einer festen Serverrolle zu entfernen, verwenden Sie Sp_dropsrvrolemember. Benutzer können nicht entfernt werden, von der public-Rolle und Dbo kann aus keiner Rolle entfernt werden.  
  
 Sp_helpuser verwenden, um die Mitglieder einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Rolle, und verwenden Sie ALTER ROLE, ein Mitglied einer Rolle hinzuzufügen.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die ALTER-Berechtigung für die Rolle.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird der Benutzer `JonB` aus der `Sales`-Rolle entfernt.  
  
```  
EXEC sp_droprolemember 'Sales', 'Jonb';  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 Im folgenden Beispiel wird der Benutzer `JonB` aus der `Sales`-Rolle entfernt.  
  
```  
EXEC sp_droprolemember 'Sales', 'JonB'  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Systemprozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sp_droprole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droprole-transact-sql.md)   
 [Sp_dropsrvrolemember &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropsrvrolemember-transact-sql.md)   
 [Sp_helpuser &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  


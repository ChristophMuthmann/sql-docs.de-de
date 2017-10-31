---
title: Erstellen der Rolle "(Transact-SQL)" | Microsoft Docs
ms.custom: 
ms.date: 04/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE ROLE
- DATABASE ROLE
- ROLE_TSQL
- DATABASE_ROLE_TSQL
- CREATE_ROLE_TSQL
- CREATE DATABASE ROLE
- ROLE
- CREATE_DATABASE_ROLE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database roles [SQL Server], creating
- CREATE DATABASE ROLE statement
- roles [SQL Server], creating
- CREATE ROLE statement
ms.assetid: b0cd54ad-e81d-4d71-acec-8a6d7261ca08
caps.latest.revision: 54
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 21e3cca3d07d7f53d646b5dd052fd40d0fa2cc1a
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="create-role-transact-sql"></a>CREATE ROLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Erstellt eine neue Datenbankrolle in der aktuellen Datenbank.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
CREATE ROLE role_name [ AUTHORIZATION owner_name ]  
```  
  
## <a name="arguments"></a>Argumente  
 *Rollenname*  
 Ist der Name der zu erstellenden Rolle.  
  
 Autorisierung *Owner_name*  
 Der Datenbankbenutzer oder die Datenbankrolle, der bzw. die die neue Rolle besitzen soll. Wenn kein Benutzer angegeben wird, besitzt der Benutzer, der CREATE ROLE ausführt, diese Rolle.  
  
## <a name="remarks"></a>Hinweise  
 Rollen sind auf Datenbankebene sicherungsfähige Elemente. Nachdem Sie eine Rolle erstellt haben, konfigurieren Sie die Berechtigungen der Rolle auf Datenbankebene mithilfe von GRANT, DENY und REVOKE. Verwenden Sie zum Hinzufügen von Mitgliedern zu einer Datenbankrolle [ALTER ROLE &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-role-transact-sql.md). Weitere Informationen finden Sie unter [Datenbankrollen](../../relational-databases/security/authentication-access/database-level-roles.md).  
  
 Datenbankrollen werden in den Katalogsichten sys.database_role_members und sys.database_principals angezeigt.  
  
 Informationen zum Entwerfen eines Berechtigungssystems finden Sie unter [Getting Started with Database Engine Permissions](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md).  
  
> [!CAUTION]  
>  [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert **CREATE ROLE** -Berechtigung für die Datenbank oder die Mitgliedschaft in der **Db_securityadmin** festen Datenbankrolle "". Bei Verwendung der **Autorisierung** Option, die folgenden Berechtigungen sind auch erforderlich:  
  
-   Um einer Rolle einen anderen Benutzer als Besitzer zuzuweisen, ist die IMPERSONATE-Berechtigung für diesen Benutzer erforderlich.  
  
-   Um einer Rolle eine andere Rolle als Besitzer zuzuweisen, ist die Mitgliedschaft in der Empfängerrolle oder die ALTER-Berechtigung für diese Rolle erforderlich.  
  
-   Um einer Rolle eine Anwendungsrolle als Besitzer zuzuweisen, ist die ALTER-Berechtigung für diese Anwendungsrolle erforderlich.  
  
## <a name="examples"></a>Beispiele  
Allen folgenden Beispielen verwenden die AdventureWorks-Datenbank.   

### <a name="a-creating-a-database-role-that-is-owned-by-a-database-user"></a>A. Erstellen einer Datenbankrolle, deren Besitzer ein Datenbankbenutzer ist  
 Im folgenden Beispiel wird die `buyers`-Datenbankrolle erstellt, deren Besitzer der Benutzer `BenMiller` ist.  
  
```  
CREATE ROLE buyers AUTHORIZATION BenMiller;  
GO  
```  
  
### <a name="b-creating-a-database-role-that-is-owned-by-a-fixed-database-role"></a>B. Erstellen einer Datenbankrolle, deren Besitzer eine feste Datenbankrolle ist  
 Im folgenden Beispiel wird die `auditors`-Datenbankrolle erstellt, deren Besitzer die feste Datenbankrolle `db_securityadmin` ist.  
  
```  
CREATE ROLE auditors AUTHORIZATION db_securityadmin;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Prinzipale &#40;Datenbankmodul&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [ALTER ROLE &#40; Transact-SQL &#41;](../../t-sql/statements/alter-role-transact-sql.md)   
 [DROP ROLE &#40; Transact-SQL &#41;](../../t-sql/statements/drop-role-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sys.database_role_members &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [Erste Schritte mit Berechtigungen für das Datenbankmodul](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)  
  
  




---
title: ALTER ROLE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/01/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_ROLE_TSQL
- ALTER ROLE
dev_langs:
- TSQL
helpviewer_keywords:
- modifying database roles
- ALTER ROLE statement
- renaming database roles
- database roles [SQL Server], modifying
- names [SQL Server], database roles
ms.assetid: e1e83caa-17cc-4871-b2db-2711339fb64f
caps.latest.revision: 64
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3eaee2d346eda964545caa60cd7168b531f47ad9
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="alter-role-transact-sql"></a>ALTER ROLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Fügt Elemente an, oder aus einer Datenbankrolle entfernt oder ändert den Namen einer benutzerdefinierten Datenbankrolle.  
  
> [!NOTE]  
>  Zum Ändern der Rollen in [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] oder [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], verwenden Sie [Sp_addrolemember &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md) und [Sp_droprolemember &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server (starting with 2012) and Azure SQL Database  
  
ALTER ROLE  role_name  
{  
       ADD MEMBER database_principal  
    |  DROP MEMBER database_principal  
    |  WITH NAME = new_name  
}  
[;]  
```  
  
 
```  
-- Syntax for SQL Server 2008 only  
  
-- Change the name of a user-defined database role  
ALTER ROLE role_name   
    WITH NAME = new_name  
[;]  
```  
  
## <a name="arguments"></a>Argumente  
 *Rollenname*  
 **GILT für:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (ab 2008)  [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
 Gibt die Datenbankrolle zu ändern.  
  
 Mitglied hinzufügen *Database_principal*l  
 **GILT für:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (ab 2012)  [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
 Gibt an, um der Datenbankprinzipal, der Mitglied einer Datenbankrolle hinzuzufügen.  
  
-   *Database_principal* einen Datenbankbenutzer oder eine benutzerdefinierte Datenbankrolle ist.  
  
-   *Database_principal* nicht mit einer festen Datenbankrolle oder ein Serverprinzipal.  
  
DROP MEMBER *Database_principal*  
 **GILT für:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (ab 2012)  [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
 Gibt an, um einen Datenbankprinzipal aus der Mitgliedschaft einer Datenbankrolle zu entfernen.  
  
-   *Database_principal* einen Datenbankbenutzer oder eine benutzerdefinierte Datenbankrolle ist.  
  
-   *Database_principal* nicht mit einer festen Datenbankrolle oder ein Serverprinzipal.  
  
MIT dem Namen = *Neuer_Name*  
 **GILT für:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (ab 2008)  [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
 Gibt an, um den Namen einer benutzerdefinierten Datenbankrolle ändern. Der neue Name darf nicht bereits in der Datenbank vorhanden sein.  
  
 Durch das Ändern des Namens einer Datenbankrolle werden die ID-Nummer, der Besitzer oder Berechtigungen der Rolle nicht geändert.  
  
## <a name="permissions"></a>Berechtigungen  
 Zum Ausführen dieses Befehls benötigen Sie mindestens eine dieser Berechtigungen oder Gruppenmitgliedschaften:  
  
-   **ALTER** -Berechtigung für die Rolle ""  
-   **ALTER ANY ROLE** Berechtigung für die Datenbank  
-   Mitgliedschaft in der **Db_securityadmin** festen Datenbankrolle ""  
  
So ändern Sie die Mitgliedschaft in einer festen Datenbankrolle müssen Sie darüber hinaus:  
  
-   Mitgliedschaft in der **Db_owner** festen Datenbankrolle ""  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
 Sie können nicht den Namen einer festen Datenbankrolle ändern.  
  
## <a name="metadata"></a>Metadaten  
 Diese Systemsichten enthalten Informationen zu Datenbankrollen und datenbankprinzipale.  
  
-   [sys.database_role_members &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)  
  
-   [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-change-the-name-of-a-database-role"></a>A. Ändern Sie den Namen einer Datenbankrolle  
 **GILT für:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (ab 2008)  [!INCLUDE[ssSDS](../../includes/sssds-md.md)]  
  
 Im folgenden Beispiel wird der Name der `buyers`-Rolle in `purchasing` geändert. [!INCLUDE[AdWorks-example](../../includes/adworks-example-md.md)]  
  
```tsql  
ALTER ROLE buyers WITH NAME = purchasing;  
```  
  
### <a name="b-add-or-remove-role-members"></a>B. Hinzufügen oder Entfernen von Mitgliedern der Rolle  
 **GILT für:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (ab 2012)  [!INCLUDE[ssSDS](../../includes/sssds-md.md)]  
  
 Dieses Beispiel erstellt eine Datenbankrolle mit dem Namen `Sales`. Es fügt einen Datenbankbenutzer mit dem Namen "Barry", um die Mitgliedschaft, und anschließend wird gezeigt, wie das Element "Barry" zu entfernen. [!INCLUDE[AdWorks-example](../../includes/adworks-example-md.md)]  
  
```tsql  
CREATE ROLE Sales;  
ALTER ROLE Sales ADD MEMBER Barry;  
ALTER ROLE Sales DROP MEMBER Barry;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen Sie die Rolle "" &#40; Transact-SQL &#41;](../../t-sql/statements/create-role-transact-sql.md)   
 [Prinzipale &#40;Datenbankmodul&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [DROP ROLE &#40; Transact-SQL &#41;](../../t-sql/statements/drop-role-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sys.database_role_members &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)  
  
  


---
title: ALTER USER (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/05/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_USER_TSQL
- ALTER USER
dev_langs: TSQL
helpviewer_keywords:
- modifying database users
- ALTER USER statement
- renaming databases
- schemas [SQL Server], default
- database user names [SQL Server]
- names [SQL Server], database users
- default schemas
- modifying default schemas
ms.assetid: 344fc6ce-a008-47c8-a02e-47fae66cc590
caps.latest.revision: "75"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 61984e16244a32a28449a099b2e03b5916d2c2db
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="alter-user-transact-sql"></a>ALTER USER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Benennt einen Datenbankbenutzer um oder ändert sein Standardschema.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server  
  
ALTER USER userName    
     WITH <set_item> [ ,...n ]  
[;]  
  
<set_item> ::=   
      NAME = newUserName   
    | DEFAULT_SCHEMA = { schemaName | NULL }  
    | LOGIN = loginName  
    | PASSWORD = 'password' [ OLD_PASSWORD = 'oldpassword' ]  
    | DEFAULT_LANGUAGE = { NONE | <lcid> | <language name> | <language alias> }  
    | ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ ON | OFF ]  
```  
  
```  
-- Syntax for Azure SQL Database  
  
ALTER USER userName    
     WITH <set_item> [ ,...n ]  
  
<set_item> ::=   
      NAME = newUserName   
    | DEFAULT_SCHEMA = schemaName  
    | LOGIN = loginName  
    | ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ ON | OFF ]   
[;]  
  
-- Azure SQL Database Update Syntax  
ALTER USER userName    
     WITH <set_item> [ ,...n ]  
[;]  
  
<set_item> ::=   
      NAME = newUserName   
    | DEFAULT_SCHEMA = { schemaName | NULL }  
    | LOGIN = loginName  
    | PASSWORD = 'password' [ OLD_PASSWORD = 'oldpassword' ]  
    | ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ ON | OFF ]   
  
-- SQL Database syntax when connected to a federation member  
ALTER USER userName  
     WITH <set_item> [ ,… n ]   
[;]  
  
<set_item> ::=   
     NAME = newUserName  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
ALTER USER userName    
     WITH <set_item> [ ,...n ]  
  
<set_item> ::=   
     NAME =newUserName   
     | LOGIN =loginName  
     | DEFAULT_SCHEMA = schema_name  
[;]  
```  
  
## <a name="arguments"></a>Argumente  
 *Benutzername*  
 Gibt den Namen an, mit dem der Benutzer innerhalb dieser Datenbank identifiziert wird.  
  
 Anmeldung  **=**  *LoginName*  
 Ordnet einen Benutzer einer anderen Anmeldung neu zu. Dazu wird die Sicherheits-ID (SID) des Benutzers in die SID der Anmeldung geändert.  
  
 Wenn ALTER USER die einzige Anweisung in einem SQL-Batch ist, unterstützt Windows Azure SQL-Datenbank die WITH LOGIN-Klausel. Wenn ALTER USER nicht die einzige Anweisung in einem SQL-Batch ist oder in dynamischem SQL-Code ausgeführt wird, wird die WITH LOGIN-Klausel nicht unterstützt.  
  
 Namen  **=**  *neuer Benutzername*  
 Gibt den neuen Namen für diesen Benutzer an. *Neuer Benutzername* muss nicht in der aktuellen Datenbank bereits vorhanden sein.  
  
 DEFAULT_SCHEMA  **=**  { *SchemaName* | NULL}  
 Gibt das erste Schema an, das vom Server beim Auflösen der Namen von Objekten für diesen Benutzer durchsucht wird. Wenn das Standardschema auf NULL festgelegt wird, wird ein Standardschema aus einer Windows-Gruppe entfernt.   Die NULL-Option kann nicht in Verbindung mit einem Windows-Benutzer verwendet werden.  
  
 Kennwort  **=**  "*Kennwort*"  
 **Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Gibt das Kennwort für den Benutzer an, der geändert wird. Bei Kennwörtern wird nach Groß- und Kleinschreibung unterschieden.  
  
> [!NOTE]  
>  Diese Option ist nur für enthaltene Benutzer verfügbar. Finden Sie unter [Contained Databases](../../relational-databases/databases/contained-databases.md) und [Sp_migrate_user_to_contained &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-migrate-user-to-contained-transact-sql.md) für Weitere Informationen.  
  
 OLD_PASSWORD  **=**  *"Oldpassword"*  
 **Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Das aktuelle Benutzerkennwort, das von zu ersetzenden "*Kennwort*". Bei Kennwörtern wird nach Groß- und Kleinschreibung unterschieden. *OLD_PASSWORD* so ändern Sie ein Kennwort erforderlich, es sei denn, Sie haben **ALTER ANY USER** Berechtigung. Erfordern *OLD_PASSWORD* verhindert, dass Benutzer mit **IDENTITÄTSWECHSEL** Berechtigung Ändern des Kennworts.  
  
> [!NOTE]  
>  Diese Option ist nur für enthaltene Benutzer verfügbar.  
  
 DEFAULT_LANGUAGE  **=**  *{NONE | \<Lcid > | \<Sprachenname > | \<Sprachenalias >}*  
 **Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt eine Standardsprache an, die dem Benutzer zugewiesen werden soll. Wenn diese Option auf NONE festgelegt wird, wird die aktuelle Standardsprache der Datenbank als Standardsprache festgelegt. Wenn die Standardsprache der Datenbank später geändert wird, bleibt die Standardsprache des Benutzers unverändert. *DEFAULT_LANGUAGE* kann die lokale ID (Lcid), den Namen der Sprache oder der sprachalias sein.  
  
> [!NOTE]  
>  Diese Option kann nur in einer eigenständigen Datenbank und nur für eigenständige Benutzer angegeben werden.  
  
 ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ON | **OFF** ]]  
 **Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Unterdrückt kryptografische metadatenüberprüfungen auf dem Server bei Massenkopiervorgängen. Dadurch kann der Benutzer verschlüsselte Daten zwischen Tabellen oder Datenbanken, ohne die Daten zu entschlüsseln. Der Standardwert ist OFF.  
  
> [!WARNING]  
>  Die falsche Verwendung dieser Option kann zur Datenbeschädigung führen. Weitere Informationen finden Sie unter [migrieren geschützten sensiblen Daten durch Always Encrypted](../../relational-databases/security/encryption/migrate-sensitive-data-protected-by-always-encrypted.md).  
  
## <a name="remarks"></a>Hinweise  
 Das Standardschema ist das erste Schema, das vom Server beim Auflösen der Namen von Objekten für diesen Datenbankbenutzer durchsucht wird. Wenn nicht anders angegeben, ist das Standardschema der Besitzer von Objekten, die von diesem Datenbankbenutzer erstellt werden.  
  
 Wenn der Benutzer ein Standardschema hat, wird dieses Standardschema verwendet. Wenn der Benutzer kein Standardschema hat, aber Mitglied einer Gruppe mit einem Standardschema ist, wird das Standardschema der Gruppe verwendet. Wenn der Benutzer kein Standardschema hat und Mitglied von mehreren Gruppen ist, ist das Standardschema für den Benutzer das Schema der Windows-Gruppe mit der niedrigsten principal_id und explizit festgelegt. Wenn für einen Benutzer kein Standardschema bestimmt werden kann die **Dbo** Schema verwendet werden.  
  
 DEFAULT_SCHEMA kann auf ein Schema festgelegt werden, das zurzeit nicht in der Datenbank vorhanden ist. Deshalb können Sie DEFAULT_SCHEMA einem Benutzer zuweisen, bevor das Schema erstellt wird.  
  
 DEFAULT_SCHEMA kann nicht für einen Benutzer angegeben werden, der einem Zertifikat oder einem asymmetrischen Schlüssel zugeordnet ist.  
  
> [!IMPORTANT]  
>  Der Wert von DEFAULT_SCHEMA wird ignoriert, wenn der Benutzer Mitglied ist die **Sysadmin** festen Serverrolle "". Alle Mitglieder der **Sysadmin** -Serverrolle verfügen über das Standardschema des `dbo`.  
  
 Sie können den Namen eines einer Windows-Anmeldung oder -Gruppe zugeordneten Benutzers ändern, wenn die SID des neuen Benutzernamens mit der SID in der Datenbank übereinstimmt. Diese Überprüfung trägt dazu bei, das Spoofing von Windows-Anmeldungen in der Datenbank zu verhindern.  
  
 Mit der WITH LOGIN-Klausel kann ein Benutzer einer anderen Anmeldung neu zugeordnet werden. Benutzer ohne Anmeldung, einem Zertifikat zugeordnete Benutzer oder einem asymmetrischen Schlüssel zugeordnete Benutzer können mithilfe dieser Klausel nicht neu zugeordnet werden. Nur SQL-Benutzer und Windows-Benutzer (oder -Gruppen) können neu zugeordnet werden. Mit der WITH LOGIN-Klausel kann nicht der Benutzertyp geändert werden, beispielsweise kann ein Windows-Konto nicht in eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldung geändert werden.  
  
 Der Name des Benutzers wird automatisch in den Anmeldenamen umbenannt, wenn die folgenden Voraussetzungen erfüllt sind.  
  
-   Der Benutzer ist ein Windows-Benutzer.  
  
-   Der Name ist ein Windows-Name (enthält einen umgekehrten Schrägstrich).  
  
-   Es wurde kein neuer Name angegeben.  
  
-   Der aktuelle Name unterscheidet sich vom Benutzernamen.  
  
 Andernfalls wird der Benutzer nicht umbenannt, es sei denn, der Aufrufer ruft zusätzlich die NAME-Klausel auf.  
  
Der Name des ein zugeordneter Benutzer eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldung, einem Zertifikat oder einem asymmetrischen Schlüssel kann nicht den umgekehrten Schrägstrich enthalten (\\).  
  
> [!CAUTION]  
>  [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]  
  
## <a name="security"></a>Sicherheit  
  
> [!NOTE]  
>  Ein Benutzer mit **ALTER ANY USER** Berechtigung kann das Standardschema jedes Benutzers ändern. Ein Benutzer mit einem geänderten Schema könnte dann versehentlich Daten aus der falschen Tabelle auswählen oder Code aus dem falschen Schema ausführen.  
  
### <a name="permissions"></a>Berechtigungen  
 Zum Ändern des Namens eines Benutzers erfordert die **ALTER ANY USER** Berechtigung.  
  
 So ändern Sie die zielanmeldung eines Benutzers erfordert die **Steuerelement** Berechtigung für die Datenbank.  
  
 So ändern Sie den Benutzernamen, der ein Benutzer mit **Steuerelement** Berechtigung für die Datenbank benötigt die **Steuerelement** Berechtigung für die Datenbank.  
  
 So ändern Sie das Standardschema oder Ihre Sprache erfordert **ALTER** Berechtigung für den Benutzer. Benutzer können ihr eigenes Standardschema oder ihre eigene Sprache ändern.  
  
## <a name="examples"></a>Beispiele  

Alle Beispiele, die in einer Benutzerdatenbank ausgeführt werden.  

### <a name="a-changing-the-name-of-a-database-user"></a>A. Ändern des Namens eines Datenbankbenutzers  
 Im folgenden Beispiel wird der Name des Datenbankbenutzers `Mary5` in `Mary51` geändert.  
  
```  
ALTER USER Mary5 WITH NAME = Mary51;  
GO  
```  
  
### <a name="b-changing-the-default-schema-of-a-user"></a>B. Ändern des Standardschemas eines Benutzers  
 Im folgenden Beispiel wird das Standardschema des Benutzers `Mary51` in `Purchasing` geändert.  
  
```  
ALTER USER Mary51 WITH DEFAULT_SCHEMA = Purchasing;  
GO  
```  
  
### <a name="c-changing-several-options-at-once"></a>C. Gleichzeitiges Ändern mehrerer Optionen  
 Im folgenden Beispiel werden mehrere Optionen für einen Benutzer einer eigenständigen Datenbank in einer Anweisung geändert.  
  
**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
ALTER USER Philip   
WITH  NAME = Philipe   
    , DEFAULT_SCHEMA = Development   
    , PASSWORD = 'W1r77TT98%ab@#’ OLD_PASSWORD = 'New Devel0per'   
    , DEFAULT_LANGUAGE  = French ;  
GO  
```  
  
  
## <a name="see-also"></a>Siehe auch  
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [DROP USER &#40; Transact-SQL &#41;](../../t-sql/statements/drop-user-transact-sql.md)   
 [Eigenständige Datenbanken](../../relational-databases/databases/contained-databases.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [Sp_migrate_user_to_contained &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-migrate-user-to-contained-transact-sql.md)  
  
  



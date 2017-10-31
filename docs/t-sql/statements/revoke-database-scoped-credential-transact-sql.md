---
title: REVOKE-Datenbankweiter Anmeldeinformationen (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- REVOKE DATABASE SCOPED CREDENTIAL
- REVOKE_DATABASE_SCOPED_CREDENTIAL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- REVOKE statements, database scoped credentials
- revoking permissions [SQL Server], database scoped credentials
ms.assetid: b73233c5-9afa-48ca-ba34-a9f86b9b1d2e
caps.latest.revision: 2
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d05f1829878d31593c56f65dd25660bec9dfa23e
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="revoke-database-scoped-credential-transact-sql"></a>REVOKE-Datenbankweiter Anmeldeinformationen (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssvNxt-asdb-xxxx-xxx](../../includes/tsql-appliesto-ssvnxt-asdb-xxxx-xxx.md)]

  Hebt Berechtigungen für datenbankweit gültigen Anmeldeinformationen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
REVOKE [ GRANT OPTION FOR ] permission  [ ,...n ]   
    ON DATABASE SCOPED CREDENTIAL :: credential_name   
    { TO | FROM } database_principal [ ,...n ]  
    [ CASCADE ]  
    [ AS revoking_principal ]  
```  
  
## <a name="arguments"></a>Argumente  
 GRANT OPTION FOR  
 Gibt an, dass die Fähigkeit, die angegebene Berechtigung zu erteilen, aufgehoben wird. Die Berechtigung selbst wird nicht aufgehoben.  
  
> [!IMPORTANT]  
>  Falls der Prinzipal die angegebene Berechtigung ohne GRANT OPTION besitzt, wird die Berechtigung selbst aufgehoben.  
  
 *Berechtigung*  
 Gibt eine Berechtigung aufgehoben werden kann, die datenbankweit gültigen Anmeldeinformationen. Unten aufgeführt.  
  
 ON Zertifikat **::***Credential_name*  
 Gibt die datenbankweite Anmeldeinformationen für die die Berechtigung aufgehoben wird. Der Bereichsqualifizierer "::" ist erforderlich.  
  
 *database_principal*  
 Gibt den Prinzipal an, für den die Berechtigung aufgehoben wird. Einer der folgenden Typen:  
  
-   Datenbankbenutzer  
  
-   Datenbankrolle (database role)  
  
-   Anwendungsrolle  
  
-   Einem Windows-Anmeldenamen zugeordneter Datenbankbenutzer  
  
-   Einer Windows-Gruppe zugeordneter Datenbankbenutzer  
  
-   Einem Zertifikat zugeordneter Datenbankbenutzer  
  
-   Einem asymmetrischen Schlüssel zugeordneter Datenbankbenutzer  
  
-   Keinem Serverprinzipal zugeordneter Datenbankbenutzer.  
  
 CASCADE  
 Gibt an, dass die aufgehobene Berechtigung auch für andere Prinzipale aufgehoben wird, denen diese Berechtigung vom Prinzipal erteilt wurde.  
  
> [!CAUTION]  
>  Durch ein kaskadiertes Aufheben einer Berechtigung, die mit GRANT OPTION erteilt wurde, werden sowohl GRANT als auch DENY für diese Berechtigung aufgehoben.  
  
 AS *Revoking_principal*  
 Gibt einen Prinzipal an, von dem der Prinzipal, der diese Abfrage ausführt, sein Recht zum Aufheben der Berechtigung ableitet. Einer der folgenden Typen:  
  
-   Datenbankbenutzer  
  
-   Datenbankrolle (database role)  
  
-   Anwendungsrolle  
  
-   Einem Windows-Anmeldenamen zugeordneter Datenbankbenutzer  
  
-   Einer Windows-Gruppe zugeordneter Datenbankbenutzer  
  
-   Einem Zertifikat zugeordneter Datenbankbenutzer  
  
-   Einem asymmetrischen Schlüssel zugeordneter Datenbankbenutzer  
  
-   Keinem Serverprinzipal zugeordneter Datenbankbenutzer.  
  
## <a name="remarks"></a>Hinweise  
 Datenbankweit gültigen Anmeldeinformationen ist eine Datenbankebene sicherungsfähiges Element in der Datenbank, die das übergeordnete Element in der Berechtigungshierarchie ist enthalten. Die spezifischsten und restriktivsten Berechtigungen, die für datenbankweit gültigen Anmeldeinformationen aufgehoben werden können sind aufgeführt, zusammen mit den allgemeineren Berechtigungen, die sie implizit enthalten.  
  
|Datenbankweit gültige Credential-Berechtigung|Impliziert durch die datenbankweite Credential-Berechtigung|Impliziert durch Datenbankberechtigung|  
|----------------------------|---------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|CONTROL|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CONTROL-Berechtigung für die datenbankbezogenen Anmeldeinformationen.  
  
## <a name="see-also"></a>Siehe auch  
 [REVOKE (Transact-SQL)](../../t-sql/statements/revoke-transact-sql.md)      
 [GRANT datenbankweit gültige Anmeldeinformationen (Transact-SQL)](../../t-sql/statements/grant-database-scoped-credential-transact-sql.md)   
 [VERWEIGERTE datenbankweit gültige Anmeldeinformationen (Transact-SQL)](../../t-sql/statements/deny-database-scoped-credential-transact-sql.md)   
 [Berechtigungen &#40;Datenbankmodul&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Prinzipale &#40;Datenbankmodul&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Verschlüsselungshierarchie](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  


---
title: "Verweigern von Berechtigungen für symmetrische Schlüssel (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 06/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- denying permissions [SQL Server], symmetric keys
- symmetric keys [SQL Server], permissions
- permissions [SQL Server], symmetric keys
- DENY statement, symmetric keys
- encryption [SQL Server], symmetric keys
- cryptography [SQL Server], symmetric keys
ms.assetid: 52d4b12d-17be-4cbd-aa78-65332a4883b0
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d6497a6bcf298736b3ad6c497ea26088e9fdf0a1
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="deny-symmetric-key-permissions-transact-sql"></a>DENY (Berechtigungen für symmetrische Schlüssel) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Verweigert Berechtigungen für einen symmetrischen Schlüssel.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
DENY permission [ ,...n ]    
    ON SYMMETRIC KEY :: symmetric_key_name   
        TO <database_principal> [ ,...n ] [ CASCADE ]  
    [ AS <database_principal> ]   
  
<database_principal> ::=   
        Database_user   
    | Database_role   
    | Application_role   
    | Database_user_mapped_to_Windows_User   
    | Database_user_mapped_to_Windows_Group   
    | Database_user_mapped_to_certificate   
    | Database_user_mapped_to_asymmetric_key   
    | Database_user_with_no_login   
```  
  
## <a name="arguments"></a>Argumente  
 *Berechtigung*  
 Gibt eine Berechtigung an, die für einen symmetrischen Schlüssel verweigert werden kann. Eine Liste der Berechtigungen finden Sie im Abschnitt zu den Hinweisen weiter unten in diesem Thema.  
  
 ON SYMMETRIC KEY::*Asymmetric_key_name*  
 Gibt den symmetrischen Schlüssel an, für den die Berechtigung verweigert wird. Der Bereichsqualifizierer (::) ist erforderlich.  
  
 UM \< *Database_principal*>  
 Gibt den Prinzipal an, für den die Berechtigung aufgehoben wird.  
  
 CASCADE  
 Gibt an, dass die verweigerte Berechtigung auch anderen Prinzipalen verweigert wird, denen diese Berechtigung von diesem Prinzipal erteilt wurde.  
  
 AS \<Database_principal >  
 Gibt einen Prinzipal an, von dem der Prinzipal, der diese Abfrage ausführt, das Recht zum Verweigern der Berechtigung ableitet.  
  
 *Database_user*  
 Gibt einen Datenbankbenutzer an.  
  
 *Database_role*  
 Gibt eine Datenbankrolle an.  
  
 *Application_role*  
 Gibt eine Anwendungsrolle an.  
  
 *Database_user_mapped_to_Windows_User*  
 Gibt einen Datenbankbenutzer an, der einem Windows-Benutzer zugeordnet ist.  
  
 *Database_user_mapped_to_Windows_Group*  
 Gibt einen Datenbankbenutzer an, der einer Windows-Gruppe zugeordnet ist.  
  
 *Database_user_mapped_to_certificate*  
 Gibt einen Datenbankbenutzer an, der einem Zertifikat zugeordnet ist.  
  
 *Database_user_mapped_to_asymmetric_key*  
 Gibt einen Datenbankbenutzer an, der einem asymmetrischen Schlüssel zugeordnet ist.  
  
 *Database_user_with_no_login*  
 Gibt einen Datenbankbenutzer ohne entsprechenden Prinzipal auf Serverebene an.  
  
## <a name="remarks"></a>Hinweise  
 Informationen zu symmetrischen Schlüsseln werden in der [symmetric_keys](../../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md) -Katalogsicht angezeigt.  
  
 Ein symmetrischer Schlüssel ist ein sicherungsfähiges Element auf Datenbankebene in der Datenbank, die das übergeordnete Element in der Berechtigungshierarchie ist. Die spezifischsten und restriktivsten Berechtigungen, die für einen symmetrischen Schlüssel verweigert werden können, sind unten aufgeführt. Auch die allgemeineren Berechtigungen sind aufgeführt, die diese implizit enthalten.  
  
|Berechtigung für symmetrische Schlüssel|Impliziert durch die Berechtigung für symmetrische Schlüssel|Impliziert durch Datenbankberechtigung|  
|------------------------------|-----------------------------------------|------------------------------------|  
|ALTER|CONTROL|ALTER ANY SYMMETRIC KEY|  
|CONTROL|CONTROL|CONTROL|  
|REFERENCES|CONTROL|REFERENCES|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CONTROL-Berechtigung für den symmetrischen Schlüssel oder die ALTER ANY SYMMETRIC KEY-Berechtigung für die Datenbank. Falls die AS-Option verwendet wird, muss der angegebene Prinzipal den symmetrischen Schlüssel besitzen.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die `ALTER`-Berechtigung für den symmetrischen Schlüssel `SamInventory42` für den Datenbankbenutzer `HamidS` verweigert.  
  
```  
USE AdventureWorks2012;  
DENY ALTER ON SYMMETRIC KEY::SamInventory42 TO HamidS;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Sys. symmetric_keys &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md)   
 [Erteilen Sie Berechtigungen für symmetrische Schlüssel &#40; Transact-SQL &#41;](../../t-sql/statements/grant-symmetric-key-permissions-transact-sql.md)   
 [REVOKE-Berechtigungen für symmetrische Schlüssel &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-symmetric-key-permissions-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [Berechtigungen &#40;Datenbankmodul&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Prinzipale &#40;Datenbankmodul&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Verschlüsselungshierarchie](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  


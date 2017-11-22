---
title: "WIDERRUFEN Sie Berechtigungen für asymmetrische Schlüssel (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- permissions [SQL Server], asymmetric keys
- asymmetric keys [SQL Server], permissions
- REVOKE statement, asymmetric keys
ms.assetid: 1a1063e8-ffc7-4775-a40d-e155740ad7b2
caps.latest.revision: "16"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ae298d40c75f35df8ed93c850ecadd797155656b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="revoke-asymmetric-key-permissions-transact-sql"></a>REVOKE (Berechtigungen für asymmetrische Schlüssel) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Hebt die Berechtigungen für einen asymmetrischen Schlüssel auf.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
REVOKE [ GRANT OPTION FOR ] { permission  [ ,...n ] }   
    ON ASYMMETRIC KEY :: asymmetric_key_name   
    { TO | FROM } database_principal [ ,...n ]  
    [ CASCADE ]  
    [ AS revoking_principal ]  
```  
  
## <a name="arguments"></a>Argumente  
 GRANT OPTION FOR  
 Gibt an, dass die Fähigkeit, die angegebene Berechtigung zu erteilen, aufgehoben wird.  
  
> [!IMPORTANT]  
>  Falls der Prinzipal die angegebene Berechtigung ohne GRANT OPTION besitzt, wird die Berechtigung selbst aufgehoben.  
  
 *Berechtigung*  
 Gibt eine Berechtigung an, die für eine Assembly aufgehoben werden kann. Unten aufgeführt.  
  
 FÜR ASYMMETRISCHEN Schlüssel **::***Asymmetric_key_name*  
 Gibt den asymmetrischen Schlüssel an, für den die Berechtigung aufgehoben wird. Der bereichsqualifizierer **::** ist erforderlich.  
  
 *database_principal*  
 Gibt den Prinzipal an, für den die Berechtigung aufgehoben wird. Einer der folgenden Typen:  
  
-   Datenbankbenutzer  
  
-   Datenbankrolle  
  
-   Anwendungsrolle  
  
-   Einem Windows-Anmeldenamen zugeordneter Datenbankbenutzer  
  
-   Einer Windows-Gruppe zugeordneter Datenbankbenutzer  
  
-   Einem Zertifikat zugeordneter Datenbankbenutzer  
  
-   Einem asymmetrischen Schlüssel zugeordneter Datenbankbenutzer  
  
-   Datenbankbenutzer, der nicht einem Serverprinzipal zugeordnet ist.  
  
 CASCADE  
 Gibt an, dass die aufgehobene Berechtigung auch für andere Prinzipale aufgehoben wird, denen sie von diesem Prinzipal erteilt oder verweigert wurde. Die Berechtigung selbst wird nicht aufgehoben.  
  
> [!CAUTION]  
>  Durch ein kaskadiertes Aufheben einer Berechtigung, die mit GRANT OPTION erteilt wurde, werden sowohl GRANT als auch DENY für diese Berechtigung aufgehoben.  
  
 AS *Revoking_principal*  
 Gibt einen Prinzipal an, von dem der Prinzipal, der diese Abfrage ausführt, sein Recht zum Aufheben der Berechtigung ableitet. Einer der folgenden Typen:  
  
-   Datenbankbenutzer  
  
-   Datenbankrolle  
  
-   Anwendungsrolle  
  
-   Einem Windows-Anmeldenamen zugeordneter Datenbankbenutzer  
  
-   Einer Windows-Gruppe zugeordneter Datenbankbenutzer  
  
-   Einem Zertifikat zugeordneter Datenbankbenutzer  
  
-   Einem asymmetrischen Schlüssel zugeordneter Datenbankbenutzer  
  
-   Datenbankbenutzer, der nicht einem Serverprinzipal zugeordnet ist.  
  
## <a name="remarks"></a>Hinweise  
 Ein asymmetrischer Schlüssel ist ein sicherungsfähiges Element auf Datenbankebene, das in der Datenbank enthalten ist, die dem Element in der Berechtigungshierarchie übergeordnet ist. Die spezifischsten und restriktivsten Berechtigungen, die für einen asymmetrischen Schlüssel aufgehoben werden können, sind im Folgenden aufgeführt, zusammen mit den allgemeineren Berechtigungen, die sie implizit enthalten.  
  
|Berechtigung für asymmetrische Schlüssel|Impliziert durch Berechtigung für asymmetrischen Schlüssel|Impliziert durch Datenbankberechtigung|  
|-------------------------------|------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY ASYMMETRIC KEY|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CONTROL-Berechtigung für den asymmetrischen Schlüssel.  
  
## <a name="see-also"></a>Siehe auch  
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [Berechtigungen &#40;Datenbankmodul&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Prinzipale &#40;Datenbankmodul&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [Erstellen Sie APPLICATION ROLE &#40; Transact-SQL &#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [Verschlüsselungshierarchie](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  

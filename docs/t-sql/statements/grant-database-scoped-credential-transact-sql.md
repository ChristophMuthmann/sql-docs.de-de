---
title: "GRANT datenbankweit gültige Anmeldeinformationen (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 06/19/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- GRANT DATABASE SCOPED CREDENTIAL
- GRANT_DATABASE_SCOPED_CREDENTIAL_TSQL
dev_langs: TSQL
helpviewer_keywords:
- granting permissions [SQL Server], database scoped credential
- permissions [SQL Server], database scoped credential
- database scoped credential [SQL Server], permissions
- GRANT statement, database scoped credentials
ms.assetid: 501f2c8a-6aeb-41af-bf0b-974d17af33c0
caps.latest.revision: "3"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6dbd261334e580904e9c6ad3b12ff761d8c909ab
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="grant-database-scoped-credential-permissions-transact-sql"></a>GRANT Database Scoped Credential-Berechtigung (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  Erteilt Berechtigungen für eine Datenbank im Bereich einer Anmeldeinformationen aus. 
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
GRANT permission  [ ,...n ]    
    ON DATABASE SCOPED CREDENTIAL :: credential_name   
    TO principal [ ,...n ] [ WITH GRANT OPTION ]   
    [ AS granting_principal ]   
```  
  
## <a name="arguments"></a>Argumente  
 *Berechtigung*  
 Gibt an, eine Berechtigung, die möglich gewährt Anmeldeinformationen für eine Datenbank beschränkt. Unten aufgeführt.  
  
 AUF der DATENBANKWEITEN Anmeldeinformationen **::***Credential_name*  
 Gibt die datenbankweite Anmeldeinformationen auf der die Berechtigung erteilt wird. Der Bereichsqualifizierer "::" ist erforderlich.  
  
 *database_principal*  
 Gibt den Prinzipal an, für den die Berechtigung erteilt wird. Einer der folgenden Typen:  
  
-   Datenbankbenutzer  
-   Datenbankrolle (database role)  
-   Anwendungsrolle  
-   Einem Windows-Anmeldenamen zugeordneter Datenbankbenutzer  
-   Einer Windows-Gruppe zugeordneter Datenbankbenutzer  
-   Einem Zertifikat zugeordneter Datenbankbenutzer  
-   Einem asymmetrischen Schlüssel zugeordneter Datenbankbenutzer  
-   Keinem Serverprinzipal zugeordneter Datenbankbenutzer.  
  
GRANT OPTION  
 Gibt an, dass der Prinzipal die angegebene Berechtigung auch anderen Prinzipalen erteilen kann.  
  
AS *Granting_principal*  
 Gibt einen Prinzipal an, von dem der Prinzipal, der diese Abfrage ausführt, sein Recht zum Erteilen der Berechtigung ableitet. Einer der folgenden Typen:  
  
-   Datenbankbenutzer  
-   Datenbankrolle (database role)  
-   Anwendungsrolle  
-   Einem Windows-Anmeldenamen zugeordneter Datenbankbenutzer  
-   Einer Windows-Gruppe zugeordneter Datenbankbenutzer  
-   Einem Zertifikat zugeordneter Datenbankbenutzer  
-   Einem asymmetrischen Schlüssel zugeordneter Datenbankbenutzer  
-   Keinem Serverprinzipal zugeordneter Datenbankbenutzer.  
  
## <a name="remarks"></a>Hinweise  
 Datenbankweit gültigen Anmeldeinformationen ist eine Datenbankebene sicherungsfähiges Element in der Datenbank, die das übergeordnete Element in der Berechtigungshierarchie ist enthalten. Die spezifischsten und restriktivsten Berechtigungen, die sein können werden gewährt auf datenbankweit gültigen Anmeldeinformationen aufgeführt, zusammen mit den allgemeineren Berechtigungen, die sie implizit enthalten.  
  
|Datenbankweit gültige Credential-Berechtigung|Impliziert durch die datenbankweite Credential-Berechtigung|Impliziert durch Datenbankberechtigung|  
|----------------------------|---------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|CONTROL|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Berechtigungen  
 Der Berechtigende (oder der mit der AS-Option angegebene Prinzipal) benötigt entweder die Berechtigung selbst mit GRANT OPTION oder eine höhere Berechtigung, die die erteilte Berechtigung impliziert.  
  
 Wenn Sie die Option AS verwenden, gelten die folgenden zusätzlichen Anforderungen.  
  
|AS *Granting_principal*|Zusätzliche Berechtigung erforderlich|  
|------------------------------|------------------------------------|  
|Datenbankbenutzer|IMPERSONATE-Berechtigung für den Benutzer, Mitgliedschaft in der **Db_securityadmin** festen Datenbankrolle, Mitgliedschaft in der **Db_owner** feste Datenbankrolle oder die Mitgliedschaft in der **Sysadmin** festen Serverrolle "".|  
|Einem Windows-Anmeldenamen zugeordneter Datenbankbenutzer|IMPERSONATE-Berechtigung für den Benutzer, Mitgliedschaft in der **Db_securityadmin** festen Datenbankrolle, Mitgliedschaft in der **Db_owner** feste Datenbankrolle oder die Mitgliedschaft in der **Sysadmin** festen Serverrolle "".|  
|Einer Windows-Gruppe zugeordneter Datenbankbenutzer|Mitgliedschaft in der Windows-Gruppe, Mitgliedschaft in der **Db_securityadmin** festen Datenbankrolle, Mitgliedschaft in der **Db_owner** feste Datenbankrolle oder die Mitgliedschaft in der **Sysadmin**festen Serverrolle "".|  
|Einem Zertifikat zugeordneter Datenbankbenutzer|Mitgliedschaft in der **Db_securityadmin** festen Datenbankrolle, Mitgliedschaft in der **Db_owner** feste Datenbankrolle oder die Mitgliedschaft in der **Sysadmin** festen Serverrolle "".|  
|Einem asymmetrischen Schlüssel zugeordneter Datenbankbenutzer|Mitgliedschaft in der **Db_securityadmin** festen Datenbankrolle, Mitgliedschaft in der **Db_owner** feste Datenbankrolle oder die Mitgliedschaft in der **Sysadmin** festen Serverrolle "".|  
|Einem Serverprinzipal zugeordneter Datenbankbenutzer|IMPERSONATE-Berechtigung für den Benutzer, Mitgliedschaft in der **Db_securityadmin** festen Datenbankrolle, Mitgliedschaft in der **Db_owner** feste Datenbankrolle oder die Mitgliedschaft in der **Sysadmin** festen Serverrolle "".|  
|Datenbankrolle|ALTER-Berechtigung für die Rolle, Mitgliedschaft in der **Db_securityadmin** festen Datenbankrolle, Mitgliedschaft in der **Db_owner** feste Datenbankrolle oder die Mitgliedschaft in der **Sysadmin**festen Serverrolle "".|  
|Anwendungsrolle|ALTER-Berechtigung für die Rolle, Mitgliedschaft in der **Db_securityadmin** festen Datenbankrolle, Mitgliedschaft in der **Db_owner** feste Datenbankrolle oder die Mitgliedschaft in der **Sysadmin**festen Serverrolle "".|  
  
 Objektbesitzer können Berechtigungen für die Objekte erteilen, die sie besitzen. Prinzipale mit CONTROL-Berechtigung für ein sicherungsfähiges Element können die Berechtigung für dieses sicherungsfähige Element erteilen.  
  
 Empfänger der CONTROL SERVER-Berechtigung, z. B. Mitglieder der der **Sysadmin** feste Serverrolle, können beliebige Berechtigungen für ein beliebiges erteilen sicherungsfähige Element auf dem Server. Berechtigte der CONTROL-Berechtigung für eine Datenbank, z. B. Mitglieder der der **Db_owner** festen Datenbankrolle können beliebige Berechtigungen für ein beliebiges erteilen sicherungsfähiges Element in der Datenbank. Empfänger der CONTROL-Berechtigung für ein Schema können jede beliebige Berechtigung für jedes Objekt innerhalb des Schemas erteilen.  
  
## <a name="see-also"></a>Siehe auch  
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [REVOKE-Datenbankweiter Anmeldeinformationen (Transact-SQL)](../../t-sql/statements/revoke-database-scoped-credential-transact-sql.md)   
 [VERWEIGERTE datenbankweit gültige Anmeldeinformationen (Transact-SQL)](../../t-sql/statements/deny-database-scoped-credential-transact-sql.md)   
 [Berechtigungen &#40;Datenbankmodul&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Prinzipale &#40;Datenbankmodul&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Verschlüsselungshierarchie](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  

---
title: GRANT-Assemblyberechtigungen (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/12/2017
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
- granting permissions [SQL Server], assemblies
- assemblies [CLR integration], permissions
- GRANT statement, assemblies
ms.assetid: dce1e027-f859-4967-bdda-16a95ae460d0
caps.latest.revision: "29"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d163245f90ce50defdea4b7a075ef9d0fb9b5afd
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="grant-assembly-permissions-transact-sql"></a>GRANT-Assemblyberechtigungen (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Erteilt Berechtigungen für eine Assembly.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
GRANT { permission [ ,...n ] } ON ASSEMBLY :: assembly_name  
    TO database_principal [ ,...n ]  
    [ WITH GRANT OPTION ]  
    [ AS granting_principal ]  
```  
  
## <a name="arguments"></a>Argumente  
 *Berechtigung*  
 Gibt eine Berechtigung an, die für eine Assembly erteilt werden kann. Unten aufgeführt.  
  
 AUF die ASSEMBLY **::***Assembly_name*  
 Gibt die Assembly an, für die die Berechtigung erteilt wird. Der Bereichsqualifizierer "::" ist erforderlich.  
  
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
 Eine Assembly ist ein auf der Datenbankebene sicherungsfähiges Element, das in der Datenbank enthalten ist, die das übergeordnete Element in der Berechtigungshierarchie darstellt. Die spezifischsten und restriktivsten Berechtigungen, die für eine Assembly erteilt werden können, sind im Folgenden aufgeführt, zusammen mit den allgemeineren Berechtigungen, die sie implizit enthalten.  
  
|Assemblyberechtigung|Impliziert durch Assemblyberechtigung|Impliziert durch Datenbankberechtigung|  
|-------------------------|------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY ASSEMBLY|  
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
 [Berechtigungen &#40;Datenbankmodul&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Prinzipale &#40;Datenbankmodul&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [Erstellen Sie APPLICATION ROLE &#40; Transact-SQL &#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [Verschlüsselungshierarchie](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  

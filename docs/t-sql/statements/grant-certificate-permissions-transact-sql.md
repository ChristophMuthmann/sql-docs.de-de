---
title: GRANT (Zertifikatberechtigungen) (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/12/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- granting permissions [SQL Server], certificates
- certificates [SQL Server], permissions
- permissions [SQL Server], certificates
- GRANT statement, certificates
ms.assetid: 77270245-a24b-4a20-b481-e6a5ea05b499
caps.latest.revision: 15
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 06cd8f6b6b9e6a05326bad54319961a2120b979d
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="grant-certificate-permissions-transact-sql"></a>GRANT (Zertifikatberechtigungen) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Erteilt Berechtigungen für ein Zertifikat in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```
GRANT permission  [ ,...n ]    
    ON CERTIFICATE :: certificate_name   
    TO principal [ ,...n ] [ WITH GRANT OPTION ]   
    [ AS granting_principal ]   
```  
  
## <a name="arguments"></a>Argumente  
 *Berechtigung*  
 Gibt eine Berechtigung an, die für ein Zertifikat erteilt werden kann. Unten aufgeführt.  
  
 ON Zertifikat **::***Name*  
 Gibt das Zertifikat an, für das die Berechtigung erteilt wird. Der Bereichsqualifizierer "::" ist erforderlich.  
  
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
 Ein Zertifikat ist ein sicherbares Element auf Datenbankebene in der Datenbank, die dessen übergeordnetes Element in der Berechtigungshierarchie ist. Die spezifischsten und am meisten beschränkten Berechtigungen, die für ein Zertifikat erteilt werden können, sind unten aufgeführt. Auch die allgemeineren Berechtigungen sind aufgeführt, die diese implizit enthalten.  
  
|Zertifikatsberechtigung|Impliziert durch die Zertifikatsberechtigung|Impliziert durch Datenbankberechtigung|  
|----------------------------|---------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY CERTIFICATE|  
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
  
  


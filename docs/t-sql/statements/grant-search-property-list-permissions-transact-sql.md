---
title: GRANT-Sucheigenschaftenlisten-Berechtigungen (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- full-text search [SQL Server], permissions
- search property lists [SQL Server], permissions
- granting permissions [SQL Server], search property lists
- GRANT statement, search property list permissions
ms.assetid: bb2d2550-9c0e-4a88-b50c-12e481d4d3ae
caps.latest.revision: "10"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5af3884c41ad4f240ed53215b0d0e807cacf64a4
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="grant-search-property-list-permissions-transact-sql"></a>GRANT-Sucheigenschaftenlisten-Berechtigungen (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  Erteilt erechtigungen für eine Sucheigenschaftenliste.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
GRANT permission [ ,...n ] ON   
    SEARCH PROPERTY LIST :: search_property_list_name  
    TO database_principal [ ,...n ]  
    [ WITH GRANT OPTION ]  
    [ AS granting_principal ]  
```  
  
## <a name="arguments"></a>Argumente  
 *Berechtigung*  
 Der Name einer Berechtigung. Die gültigen Zuordnungen von Berechtigungen zu sicherungsfähigen Elementen werden im Abschnitt mit den Hinweisen weiter unten in diesem Thema beschrieben.  
  
 AUF SEARCH PROPERTY LIST **::***Search_property_list_name*  
 Gibt die Sucheigenschaftenliste an, für die die Berechtigung erteilt wird. Der bereichsqualifizierer **::** ist erforderlich.  
  
 **Listet die vorhandenen sucheigenschaftenlisten anzeigen**  
  
-   [sys.registered_search_property_lists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)  
  
 *database_principal*  
 Gibt den Prinzipal an, für den die Berechtigung erteilt wird. Die folgenden Prinzipale sind möglich:  
  
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
 Gibt einen Prinzipal an, von dem der Prinzipal, der diese Abfrage ausführt, sein Recht zum Erteilen der Berechtigung ableitet. Die folgenden Prinzipale sind möglich:  
  
-   Datenbankbenutzer  
  
-   Datenbankrolle (database role)  
  
-   Anwendungsrolle  
  
-   Einem Windows-Anmeldenamen zugeordneter Datenbankbenutzer  
  
-   Einer Windows-Gruppe zugeordneter Datenbankbenutzer  
  
-   Einem Zertifikat zugeordneter Datenbankbenutzer  
  
-   Einem asymmetrischen Schlüssel zugeordneter Datenbankbenutzer  
  
-   Keinem Serverprinzipal zugeordneter Datenbankbenutzer.  
  
## <a name="remarks"></a>Hinweise  
  
## <a name="search-property-list-permissions"></a>SEARCH PROPERTY LIST-Berechtigungen  
 Eine Sucheigenschaftenliste ist ein sicherungsfähiges Element auf Datenbankebene in der Datenbank, die das übergeordnete Element in der Berechtigungshierarchie ist. Die spezifischsten und restriktivsten Berechtigungen, die für eine Sucheigenschaftenliste erteilt werden können, sind unten aufgeführt. Auch die allgemeineren Berechtigungen sind aufgeführt, die diese implizit enthalten.  
  
|Sucheigenschaftenlisten-Berechtigung|Impliziert durch Sucheigenschaftenlisten-Berechtigung|Impliziert durch Datenbankberechtigung|  
|-------------------------------------|------------------------------------------------|------------------------------------|  
|ALTER|CONTROL|ALTER ANY FULLTEXT CATALOG|  
|CONTROL|CONTROL|CONTROL|  
|REFERENCES|CONTROL|REFERENCES|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Berechtigungen  
 Der Berechtigende (oder der mit der AS-Option angegebene Prinzipal) benötigt entweder die Berechtigung selbst mit GRANT OPTION oder eine höhere Berechtigung, die die erteilte Berechtigung impliziert.  
  
 Wenn die Option AS verwenden, gelten die folgenden zusätzlichen Anforderungen.  
  
|AS *Granting_principal*|Zusätzliche Berechtigung erforderlich|  
|------------------------------|------------------------------------|  
|Datenbankbenutzer|IMPERSONATE-Berechtigung für den Benutzer, Mitgliedschaft in der festen Datenbankrolle db_securityadmin, Mitgliedschaft in der festen Datenbankrolle db_owner oder Mitgliedschaft in der festen Serverrolle sysadmin.|  
|Einem Windows-Anmeldenamen zugeordneter Datenbankbenutzer|IMPERSONATE-Berechtigung für den Benutzer, Mitgliedschaft in der festen Datenbankrolle db_securityadmin, Mitgliedschaft in der festen Datenbankrolle db_owner oder Mitgliedschaft in der festen Serverrolle sysadmin.|  
|Einer Windows-Gruppe zugeordneter Datenbankbenutzer|Mitgliedschaft in der Windows-Gruppe, Mitgliedschaft in der festen Datenbankrolle db_securityadmin, Mitgliedschaft in der festen Datenbankrolle db_owner oder Mitgliedschaft in der festen Serverrolle sysadmin.|  
|Einem Zertifikat zugeordneter Datenbankbenutzer|Mitgliedschaft in der festen Datenbankrolle db_securityadmin, Mitgliedschaft in der festen Datenbankrolle db_owner oder Mitgliedschaft in der festen Serverrolle sysadmin.|  
|Einem asymmetrischen Schlüssel zugeordneter Datenbankbenutzer|Mitgliedschaft in der festen Datenbankrolle db_securityadmin, Mitgliedschaft in der festen Datenbankrolle db_owner oder Mitgliedschaft in der festen Serverrolle sysadmin.|  
|Einem Serverprinzipal zugeordneter Datenbankbenutzer|IMPERSONATE-Berechtigung für den Benutzer, Mitgliedschaft in der festen Datenbankrolle db_securityadmin, Mitgliedschaft in der festen Datenbankrolle db_owner oder Mitgliedschaft in der festen Serverrolle sysadmin.|  
|Datenbankrolle|ALTER-Berechtigung für die Rolle, Mitgliedschaft in der festen Datenbankrolle db_securityadmin, Mitgliedschaft in der festen Datenbankrolle db_owner oder Mitgliedschaft in der festen Serverrolle sysadmin.|  
|Anwendungsrolle|ALTER-Berechtigung für die Rolle, Mitgliedschaft in der festen Datenbankrolle db_securityadmin, Mitgliedschaft in der festen Datenbankrolle db_owner oder Mitgliedschaft in der festen Serverrolle sysadmin.|  
  
 Objektbesitzer können Berechtigungen für die Objekte erteilen, die sie besitzen. Prinzipale mit CONTROL-Berechtigung für ein sicherungsfähiges Element können die Berechtigung für dieses sicherungsfähige Element erteilen.  
  
 Empfänger der CONTROL SERVER-Berechtigung, wie z. B. Mitglieder der festen Serverrolle sysadmin, können jede beliebige Berechtigung für jedes beliebige sicherungsfähige Element auf dem Server erteilen. Empfänger der CONTROL-Berechtigung in einer Datenbank, z. B. Mitglieder der festen Datenbankrolle db_owner, können jede Berechtigung für ein beliebiges sicherungsfähiges Element in der Datenbank erteilen. Empfänger der CONTROL-Berechtigung für ein Schema können jede beliebige Berechtigung für jedes Objekt innerhalb des Schemas erteilen.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="granting-permissions-to-a-search-property-list"></a>Gewähren von Berechtigungen für eine Sucheigenschaftenliste  
 Im folgenden Beispiel wird `Mary` die `VIEW DEFINITION`-Berechtigung für die `DocumentTablePropertyList`-Sucheigenschaftenliste erteilt.  
  
```  
GRANT VIEW DEFINITION  
    ON SEARCH PROPERTY LIST :: DocumentTablePropertyList  
    TO Mary ;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen Sie APPLICATION ROLE &#40; Transact-SQL &#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [Erstellen Sie die SEARCH PROPERTY LIST &#40; Transact-SQL &#41;](../../t-sql/statements/create-search-property-list-transact-sql.md)   
 [DENY Sucheigenschaftenlisten-Berechtigungen &#40; Transact-SQL &#41;](../../t-sql/statements/deny-search-property-list-permissions-transact-sql.md)   
 [Verschlüsselungshierarchie](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [fn_my_permissions &#40; Transact-SQL &#41;](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [HAS_PERMS_BY_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/has-perms-by-name-transact-sql.md)   
 [Prinzipale &#40;Datenbankmodul&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [WIDERRUFEN Sie die Sucheigenschaftenlisten-Berechtigungen &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-search-property-list-permissions-transact-sql.md)   
 [sys.fn_builtin_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [Sys. registered_search_property_lists &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)   
 [Suchen von Dokumenteigenschaften mithilfe von Sucheigenschaftenlisten](../../relational-databases/search/search-document-properties-with-search-property-lists.md)  
  
  

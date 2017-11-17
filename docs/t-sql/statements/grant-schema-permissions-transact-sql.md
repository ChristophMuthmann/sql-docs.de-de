---
title: GRANT-Schemaberechtigungen (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/19/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
- schemas [SQL Server], permissions
- permissions [SQL Server], schemas
- GRANT statement, schemas
- granting permissions [SQL Server], schemas
ms.assetid: b2aa1fc8-e7af-45d2-9f80-737543c8aa95
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d2a4583b14e8b7ed869a67536718683e33162447
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="grant-schema-permissions-transact-sql"></a>GRANT-Schemaberechtigungen (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Erteilt Berechtigungen für ein Schema.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
GRANT permission  [ ,...n ] ON SCHEMA :: schema_name  
    TO database_principal [ ,...n ]  
    [ WITH GRANT OPTION ]  
    [ AS granting_principal ]  
```  
  
## <a name="arguments"></a>Argumente  
 *Berechtigung*  
 Gibt eine Berechtigung an, die für ein Schema erteilt werden kann. Eine Liste der Berechtigungen finden Sie im Abschnitt "Hinweise" weiter unten in diesem Thema...  
  
 ON SCHEMA **::** Schema*_name*  
 Gibt das Schema an, für das die Berechtigung erteilt wird. Der bereichsqualifizierer **::** ist erforderlich.  
  
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
  
> [!IMPORTANT]  
>  Durch eine Kombination von ALTER- und REFERENCE-Berechtigungen würde in manchen Fällen zugelassen, dass der Empfänger Daten anzeigt oder Funktionen ausführt, für die er nicht autorisiert ist. Beispiel: Ein Benutzer mit ALTER-Berechtigung für eine Tabelle und REFERENCE-Berechtigung für eine Funktion kann eine berechnete Spalte über eine Funktion erstellen und ausführen lassen. In diesem Fall benötigt der Benutzer auch die SELECT-Berechtigung für die berechnete Spalte.  
  
 Ein Schema ist ein auf der Datenbankebene sicherungsfähiges Element, das in der Datenbank enthalten ist, die das übergeordnete Element in der Berechtigungshierarchie darstellt. Die spezifischsten und restriktivsten Berechtigungen, die für ein Schema erteilt werden können, sind im Folgenden aufgeführt, zusammen mit den allgemeineren Berechtigungen, die implizit enthalten sind.  
  
|Schemaberechtigung|Impliziert durch die Schemaberechtigung|Impliziert durch Datenbankberechtigung|  
|-----------------------|----------------------------------|------------------------------------|  
|ALTER|CONTROL|ALTER ANY SCHEMA|  
|CONTROL|CONTROL|CONTROL|  
|CREATE SEQUENCE|ALTER|ALTER ANY SCHEMA|  
|DELETE|CONTROL|DELETE|  
|EXECUTE|CONTROL|EXECUTE|  
|INSERT|CONTROL|INSERT|  
|REFERENCES|CONTROL|REFERENCES|  
|SELECT|CONTROL|SELECT|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|UPDATE|CONTROL|UPDATE|  
|VIEW CHANGE TRACKING|CONTROL|CONTROL|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
> [!CAUTION]  
>  Ein Benutzer mit ALTER-Berechtigung für ein Schema kann mithilfe von Besitzverkettung auf sicherungsfähige Elemente in anderen Schemas zugreifen, auch wenn dem Benutzer für diese Elemente explizit der Zugriff verweigert wurde. Der Grund ist, dass durch die Besitzverkettung Berechtigungsüberprüfungen für referenzierte Objekte umgangen werden, wenn ihr Besitzer derselbe Prinzipal ist, der die auf sie verweisenden Objekte besitzt. Ein Benutzer mit ALTER-Berechtigung für ein Schema kann Prozeduren, Synonyme und Sichten erstellen, die dem Besitzer des Schemas gehören. Diese Objekte haben (per Besitzverkettung) Zugriff auf Informationen in anderen Schemas, die dem Besitzer des Schemas gehören. Vermeiden Sie es nach Möglichkeit, die ALTER-Berechtigung für ein Schema zu erteilen, wenn dem Besitzer des Schemas auch andere Schemas gehören.  
  
 Das Problem kann beispielsweise in den folgenden Szenarien auftreten. Bei diesen Szenarien wird angenommen, dass ein Benutzer U1 über die ALTER-Berechtigung für das S1-Schema verfügt. Dem Benutzer U1 wird der Zugriff auf ein Tabellenobjekt mit dem Namen T1 im S2-Schema verweigert. Das S1-Schema und das S2-Schema gehören demselben Besitzer.  
  
 Benutzer U1 verfügt über die CREATE PROCEDURE-Berechtigung für die Datenbank und die EXECUTE-Berechtigung für das S1-Schema. Daher kann Benutzer U1 eine gespeicherte Prozedur erstellen und dann in der gespeicherten Prozedur auf das ihm verweigerte Objekt T1 zugreifen.  
  
 Benutzer U1 verfügt über die CREATE SYNONYM-Berechtigung für die Datenbank und die SELECT-Berechtigung für das S1-Schema. Daher kann Benutzer U1 ein Synonym im S1-Schema für das ihm verweigerte Objekt T1 erstellen und dann mit dem Synonym auf das ihm verweigerte Objekt T1 zugreifen.  
  
 Benutzer U1 verfügt über die CREATE VIEW-Berechtigung für die Datenbank und die SELECT-Berechtigung für das S1-Schema. Daher kann Benutzer U1 eine Sicht im S1-Schema erstellen, um Daten für das ihm verweigerte Objekt T1 abzufragen, und dann mit der Sicht auf das ihm verweigerte Objekt T1 zugreifen.  
  
 Weitere Informationen finden Sie im Microsoft Knowledge Base-Artikel 914847.  
  
## <a name="permissions"></a>Berechtigungen  
 Der Berechtigende (oder der mit der AS-Option angegebene Prinzipal) benötigt entweder die Berechtigung selbst mit GRANT OPTION oder eine höhere Berechtigung, die die erteilte Berechtigung impliziert.  
  
 Wenn Sie die Option AS verwenden, gelten die folgenden zusätzlichen Anforderungen.  
  
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
  
### <a name="a-granting-insert-permission-on-schema-humanresources-to-guest"></a>A. Erteilen der INSERT-Berechtigung für das HumanResources-Schema an "guest"  
  
```  
GRANT INSERT ON SCHEMA :: HumanResources TO guest;  
```  
  
### <a name="b-granting-select-permission-on-schema-person-to-database-user-wiljo"></a>B. Erteilen der SELECT-Berechtigung für das Person-Schema an den Datenbankbenutzer "WilJo"  
  
```  
GRANT SELECT ON SCHEMA :: Person TO WilJo WITH GRANT OPTION;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Verweigern von Schemaberechtigungen für &#40; Transact-SQL &#41;](../../t-sql/statements/deny-schema-permissions-transact-sql.md)   
 [REVOKE (Schemaberechtigungen) &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-schema-permissions-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [Berechtigungen &#40;Datenbankmodul&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Prinzipale &#40;Datenbankmodul&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [Erstellen Sie APPLICATION ROLE &#40; Transact-SQL &#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [Verschlüsselungshierarchie](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [sys.fn_builtin_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [fn_my_permissions &#40; Transact-SQL &#41;](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)   
 [HAS_PERMS_BY_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/has-perms-by-name-transact-sql.md)  
  
  


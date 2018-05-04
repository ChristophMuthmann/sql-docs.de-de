---
title: Sys. fn_builtin_permissions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- fn_builtin_permissions
- sys.fn_builtin_permissions_TSQL
- fn_builtin_permissions_TSQL
- sys.fn_builtin_permissions
dev_langs:
- TSQL
helpviewer_keywords:
- compact permissions types
- viewing permission hierarchy
- hierarchies [SQL Server], permissions
- built-in permissions hierarchy [SQL Server]
- fn_builtin_permissions function
- permissions [SQL Server], hierarchy
- displaying permission hierarchy
- sys.fn_builtin_permissions function
ms.assetid: 704b1ad3-3534-4cf3-aff4-9fb70064b6cc
caps.latest.revision: 42
author: rothja
ms.author: jroth
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: f4b193be24b752f49ba3e9d0133af8981c4bb422
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysfnbuiltinpermissions-transact-sql"></a>sys.fn_builtin_permissions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt eine Beschreibung der integrierten Berechtigungshierarchie des Servers zurück. `sys.fn_builtin_permissions` kann nur aufgerufen werden, auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], und es gibt alle Berechtigungen, unabhängig davon, ob sie auf der aktuellen Plattform unterstützt werden. Die meisten Berechtigungen – jedoch nicht alle – gelten für alle Plattformen. Beispielsweise können keine Berechtigungen auf Serverebene für SQL-Datenbank erteilt werden. Informationen darüber, welche Plattformen jede Berechtigung unterstützt finden Sie unter [Berechtigungen &#40;Datenbankmodul&#41;](../../relational-databases/security/permissions-database-engine.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sys.fn_builtin_permissions ( [ DEFAULT | NULL ]  
    | empty_string | '<securable_class>' } )  
  
<securable_class> ::=   
      APPLICATION ROLE | ASSEMBLY | ASYMMETRIC KEY | AVAILABILITY GROUP  
    | CERTIFICATE | CONTRACT | DATABASE | DATABASE SCOPED CREDENTIAL    
    | ENDPOINT | FULLTEXT CATALOG | FULLTEXT STOPLIST | LOGIN      
    | MESSAGE TYPE | OBJECT | REMOTE SERVICE BINDING | ROLE | ROUTE    
    | SCHEMA | SEARCH PROPERTY LIST | SERVER | SERVER ROLE | SERVICE    
    | SYMMETRIC KEY | TYPE | USER | XML SCHEMA COLLECTION  
```  
  
## <a name="arguments"></a>Argumente  
 DEFAULT  
 Wenn sie mit der Option "DEFAULT" (ohne Anführungszeichen) aufgerufen wird, wird die Funktion eine vollständige Liste der integrierten Berechtigungen zurück.  
  
 NULL  
 Entspricht der Option DEFAULT.  
  
 *empty_string*  
 Entspricht der Option DEFAULT.  
  
 **'**<securable_class>**'**  
 Wenn sie mit dem Namen einer sicherungsfähigen Klasse aufgerufen wird, gibt Sys. fn_builtin_permissions alle Berechtigungen zurück, die für die Klasse gelten. < Securable_class > ist ein Zeichenfolgenliteral, das Anführungszeichen erfordert. **nvarchar(60)**  
  
## <a name="tables-returned"></a>Zurückgegebene Tabellen  
  
|Spaltenname|Datentyp|Sortierung|Description|  
|-----------------|---------------|---------------|-----------------|  
|class_desc|**nvarchar(60)**|Sortierung des Servers.|Beschreibung der sicherbaren Klasse.|  
|permission_name|**nvarchar(60)**|Sortierung des Servers.|Berechtigungsname.|  
|Typ|**varchar(4)**|Sortierung des Servers.|Kompakter Berechtigungstypcode. Siehe Tabelle weiter unten.|  
|covering_permission_name|**nvarchar(60)**|Sortierung des Servers.|Falls ungleich NULL, gibt dieser Wert den Namen der Berechtigung für diese Klasse an, die die anderen Berechtigungen für diese Klasse impliziert.|  
|parent_class_desc|**nvarchar(60)**|Sortierung des Servers.|Falls ungleich NULL, gibt dieser Wert den Namen der übergeordneten Klasse an, in der die aktuelle Klasse enthalten ist.|  
|parent_covering_permission_name|**nvarchar(60)**|Sortierung des Servers.|Falls ungleich NULL, gibt dieser Wert den Namen der Berechtigung für die übergeordnete Klasse an, die alle anderen Berechtigungen für diese Klasse impliziert.|  
  
### <a name="permission-types"></a>Typen von Berechtigungen  
  
|Berechtigungstyp|Berechtigungsname|Ist für das sicherbare Element oder die Klasse gültig|  
|---------------------|---------------------|-----------------------------------|  
|AADS|ALTER ANY DATABASE EVENT SESSION<br /> **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [aktuelle Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|DATABASE|  
|AAES|ALTER ANY EVENT SESSION|SERVER|  
|AAMK|ALTER ANY MASK<br /> **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [aktuelle Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|DATABASE|  
|ADBO|ADMINISTER BULK OPERATIONS|SERVER|  
|AEDS|ALTER ANY EXTERNAL DATA SOURCE<br /> **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [aktuelle Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|DATABASE|  
|AEFF|ALTER ANY EXTERNAL FILE FORMAT<br /> **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [aktuelle Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|DATABASE|  
|AL|ALTER|APPLICATION ROLE|  
|AL|ALTER|ASSEMBLY|  
|AL|ALTER<br />**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [aktuelle Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|AVAILABILITY GROUP|  
|AL|ALTER|ASYMMETRIC KEY|  
|AL|ALTER|CERTIFICATE|  
|AL|ALTER|CONTRACT|  
|AL|ALTER|DATABASE|  
|AL|ALTER<br /> **Wendet t o**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] und [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]. |DATABASE SCOPED CREDENTIAL|
|AL|ALTER|ENDPOINT|  
|AL|ALTER|FULLTEXT CATALOG|  
|AL|ALTER|FULLTEXT STOPLIST|  
|AL|ALTER|Anmeldung|  
|AL|ALTER|MESSAGE TYPE|  
|AL|ALTER|OBJECT|  
|AL|ALTER|REMOTE SERVICE BINDING|  
|AL|ALTER|ROLE|  
|AL|ALTER|ROUTE|  
|AL|ALTER|SCHEMA|  
|AL|ALTER|SEARCH PROPERTY LIST|  
|AL|ALTER<br /> **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [aktuelle Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|SERVER ROLE|  
|AL|ALTER|SERVICE|  
|AL|ALTER|SYMMETRIC KEY|  
|AL|ALTER|Benutzer|  
|AL|ALTER|XML SCHEMA COLLECTION|  
|ALAA|ALTER ANY SERVER AUDIT|SERVER|  
|ALAG|ALTER ANY AVAILABILITY GROUP<br /> **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [aktuelle Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|SERVER|  
|ALAK|ALTER ANY ASYMMETRIC KEY|DATABASE|  
|ALAR|ALTER ANY APPLICATION ROLE|DATABASE|  
|ALAS|ALTER ANY ASSEMBLY|DATABASE|  
|ALCD|ALTER ANY CREDENTIAL|SERVER|  
|ALCF|ALTER ANY CERTIFICATE|DATABASE|  
|ALCK|ALTER ANY COLUMN ENCRYPTION KEY<br />**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [aktuelle Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|DATABASE|  
|ALCM|ALTER ANY COLUMN MASTER KEY<br />**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [aktuelle Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|DATABASE|  
|ALCO|ALTER ANY CONNECTION|SERVER|  
|ALDA|ALTER ANY DATABASE AUDIT|DATABASE|  
|ALDB|ALTER ANY DATABASE|SERVER|  
|ALDC|ALTER ANY DATABASE SCOPED CONFIGURATION<br /> **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [aktuelle Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|DATABASE|  
|ALDS|ALTER ANY DATASPACE|DATABASE|  
|ALED|ALTER ANY DATABASE EVENT NOTIFICATION|DATABASE|  
|ALES|ALTER ANY EVENT NOTIFICATION|SERVER|  
|ALFT|ALTER ANY FULLTEXT CATALOG|DATABASE|  
|ALHE|ALTER ANY ENDPOINT|SERVER|  
|ALLG|ALTER ANY LOGIN|SERVER|  
|ALLS|ALTER ANY LINKED SERVER|SERVER|  
|ALMT|ALTER ANY MESSAGE TYPE|DATABASE|  
|ALRL|ALTER ANY ROLE|DATABASE|  
|ALRS|ALTER RESOURCES|SERVER|  
|ALRT|ALTER ANY ROUTE|DATABASE|  
|ALSB|ALTER ANY REMOTE SERVICE BINDING|DATABASE|  
|ALSC|ALTER ANY CONTRACT|DATABASE|  
|ALSK|ALTER ANY SYMMETRIC KEY|DATABASE|  
|ALSM|ALTER ANY SCHEMA|DATABASE|  
|ALSP|ALTER ANY SECURITY POLICY<br />**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [aktuelle Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|DATABASE|  
|ALSR|ALTER ANY SERVER ROLE<br /> **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [aktuelle Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|SERVER|  
|ALSS|ALTER SERVER STATE|SERVER|  
|ALST|ALTER SETTINGS|SERVER|  
|ALSV|ALTER ANY SERVICE|DATABASE|  
|ALTG|ALTER ANY DATABASE DDL TRIGGER|DATABASE|  
|ALTR|ALTER TRACE|SERVER|  
|ALUS|ALTER ANY USER|DATABASE|  
|AUTH|AUTHENTICATE|DATABASE|  
|AUTH|AUTHENTICATE SERVER|SERVER|  
|BADB|BACKUP DATABASE|DATABASE|  
|BALO|BACKUP LOG|DATABASE|  
|CADB|CONNECT ANY DATABASE<br /> **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [aktuelle Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|SERVER|  
|CL|CONTROL|APPLICATION ROLE|  
|CL|CONTROL|ASSEMBLY|  
|CL|CONTROL|ASYMMETRIC KEY|  
|CL|CONTROL<br />**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [aktuelle Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|AVAILABILITY GROUP|  
|CL|CONTROL|CERTIFICATE|  
|CL|CONTROL|CONTRACT|  
|CL|CONTROL|DATABASE|  
|CL|CONTROL<br /> **Gilt für**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] und [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]. |DATABASE SCOPED CREDENTIAL|
|CL|CONTROL|ENDPOINT|  
|CL|CONTROL|FULLTEXT CATALOG|  
|CL|CONTROL|FULLTEXT STOPLIST|  
|CL|CONTROL|Anmeldung|  
|CL|CONTROL|MESSAGE TYPE|  
|CL|CONTROL|OBJECT|  
|CL|CONTROL|REMOTE SERVICE BINDING|  
|CL|CONTROL|ROLE|  
|CL|CONTROL|ROUTE|  
|CL|CONTROL|SCHEMA|  
|CL|CONTROL|SEARCH PROPERTY LIST|  
|CL|CONTROL SERVER|SERVER|  
|CL|CONTROL<br />**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [aktuelle Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|SERVER ROLE|  
|CL|CONTROL|SERVICE|  
|CL|CONTROL|SYMMETRIC KEY|  
|CL|CONTROL|TYPE|  
|CL|CONTROL|Benutzer|  
|CL|CONTROL|XML SCHEMA COLLECTION|  
|CO|CONNECT|DATABASE|  
|CO|CONNECT|ENDPOINT|  
|CORP|CONNECT REPLICATION|DATABASE|  
|COSQ|CONNECT SQL|SERVER|  
|CP|CHECKPOINT|DATABASE|  
|CRAC|Erstellen der Verfügbarkeitsgruppe<br /> **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [aktuelle Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|SERVER|  
|CRAG|CREATE AGGREGATE|DATABASE|  
|CRAK|CREATE ASYMMETRIC KEY|DATABASE|  
|CRAS|CREATE ASSEMBLY|DATABASE|  
|CRCF|CREATE CERTIFICATE|DATABASE|  
|CRDB|CREATE ANY DATABASE|SERVER|  
|CRDB|CREATE DATABASE|DATABASE|  
|CRDE|CREATE DDL EVENT NOTIFICATION|SERVER|  
|CRDF|CREATE DEFAULT|DATABASE|  
|CRED|CREATE DATABASE DDL EVENT NOTIFICATION|DATABASE|  
|CRFN|CREATE FUNCTION|DATABASE|  
|CRFT|CREATE FULLTEXT CATALOG|DATABASE|  
|CRHE|CREATE ENDPOINT|SERVER|  
|CRMT|CREATE MESSAGE TYPE|DATABASE|  
|CRPR|CREATE PROCEDURE|DATABASE|  
|CRQU|CREATE QUEUE|DATABASE|  
|CRRL|CREATE ROLE|DATABASE|  
|CRRT|CREATE ROUTE|DATABASE|  
|CRRU|CREATE RULE|DATABASE|  
|CRSB|CREATE REMOTE SERVICE BINDING|DATABASE|  
|CRSC|CREATE CONTRACT|DATABASE|  
|CRSK|CREATE SYMMETRIC KEY|DATABASE|  
|CRSM|CREATE SCHEMA|DATABASE|  
|CRSN|CREATE SYNONYM|DATABASE|  
|CRSO|CREATE SEQUENCE|SCHEMA|  
|CRSR|CREATE SERVER ROLE<br /> **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [aktuelle Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|SERVER|  
|CRSV|CREATE SERVICE|DATABASE|  
|CRTB|CREATE TABLE|DATABASE|  
|CRTE|CREATE TRACE EVENT NOTIFICATION|SERVER|  
|CRTY|CREATE TYPE|DATABASE|  
|CRVW|CREATE VIEW|DATABASE|  
|CRXS|CREATE XML SCHEMA COLLECTION|DATABASE|  
|DABO|ADMINISTER DATABASE BULK OPERATIONS<br /> **Gilt für**: [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].|DATABASE|  
|DL|DELETE|DATABASE|  
|DL|DELETE|OBJECT|  
|DL|DELETE|SCHEMA|  
|EAES|EXECUTE ANY EXTERNAL SCRIPT<br />**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [aktuelle Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|DATABASE|  
|EX|Führen Sie|DATABASE|  
|EX|Führen Sie|OBJECT|  
|EX|Führen Sie|SCHEMA|  
|EX|Führen Sie|TYPE|  
|EX|Führen Sie|XML SCHEMA COLLECTION|  
|IAL|IMPERSONATE ANY LOGIN<br /> **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [aktuelle Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|SERVER|  
|IM|IMPERSONATE|Anmeldung|  
|IM|IMPERSONATE|Benutzer|  
|IN|INSERT|DATABASE|  
|IN|INSERT|OBJECT|  
|IN|INSERT|SCHEMA|  
|KIDC|KILL DATABASE CONNECTION<br />**Gilt für**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|DATABASE|  
|RC|RECEIVE|OBJECT|  
|RF|REFERENCES|ASSEMBLY|  
|RF|REFERENCES|ASYMMETRIC KEY|  
|RF|REFERENCES|CERTIFICATE|  
|RF|REFERENCES|CONTRACT|  
|RF|REFERENCES|DATABASE|  
|RF|REFERENCES<br /> **Gilt für**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] und [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]. |DATABASE SCOPED CREDENTIAL|
|RF|REFERENCES|FULLTEXT CATALOG|  
|RF|REFERENCES|FULLTEXT STOPLIST|  
|RF|REFERENCES|SEARCH PROPERTY LIST|  
|RF|REFERENCES|MESSAGE TYPE|  
|RF|REFERENCES|OBJECT|  
|RF|REFERENCES|SCHEMA|  
|RF|REFERENCES|SYMMETRIC KEY|  
|RF|REFERENCES|TYPE|  
|RF|REFERENCES|XML SCHEMA COLLECTION|  
|SHDN|SHUTDOWN|SERVER|  
|SL|SELECT|DATABASE|  
|SL|SELECT|OBJECT|  
|SL|SELECT|SCHEMA|  
|SN|SEND|SERVICE|  
|SPLN|SHOWPLAN|DATABASE|  
|SUQN|SUBSCRIBE QUERY NOTIFICATIONS|DATABASE|  
|SUS|SELECT ALL USER SECURABLES<br /> **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [aktuelle Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|SERVER|  
|TO|TAKE OWNERSHIP|ASSEMBLY|  
|TO|TAKE OWNERSHIP|ASYMMETRIC KEY|  
|TO|TAKE OWNERSHIP<br />**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [aktuelle Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|AVAILABILITY GROUP|  
|TO|TAKE OWNERSHIP|CERTIFICATE|  
|TO|TAKE OWNERSHIP|CONTRACT|  
|TO|TAKE OWNERSHIP|DATABASE|  
|TO|TAKE OWNERSHIP<br /> **Gilt für**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] und [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]. |DATABASE SCOPED CREDENTIAL|
|TO|TAKE OWNERSHIP|ENDPOINT|  
|TO|TAKE OWNERSHIP|FULLTEXT CATALOG|  
|TO|TAKE OWNERSHIP|FULLTEXT STOPLIST|  
|TO|TAKE OWNERSHIP|SEARCH PROPERTY LIST|  
|TO|TAKE OWNERSHIP|MESSAGE TYPE|  
|TO|TAKE OWNERSHIP|OBJECT|  
|TO|TAKE OWNERSHIP|REMOTE SERVICE BINDING|  
|TO|TAKE OWNERSHIP|ROLE|  
|TO|TAKE OWNERSHIP|ROUTE|  
|TO|TAKE OWNERSHIP|SCHEMA|  
|TO|TAKE OWNERSHIP<br /> **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [aktuelle Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|SERVER ROLE|  
|TO|TAKE OWNERSHIP|SERVICE|  
|TO|TAKE OWNERSHIP|SYMMETRIC KEY|  
|TO|TAKE OWNERSHIP|TYPE|  
|TO|TAKE OWNERSHIP|XML SCHEMA COLLECTION|  
|UMSK|UNMASK<br /> **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [aktuelle Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|DATABASE|  
|UP|UPDATE|DATABASE|  
|UP|UPDATE|OBJECT|  
|UP|UPDATE|SCHEMA|  
|VW|VIEW DEFINITION|APPLICATION ROLE|  
|VW|VIEW DEFINITION|ASSEMBLY|  
|VW|VIEW DEFINITION|ASYMMETRIC KEY|  
|VW|VIEW DEFINITION<br />**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [aktuelle Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|AVAILABILITY GROUP|  
|VW|VIEW DEFINITION|CERTIFICATE|  
|VW|VIEW DEFINITION|CONTRACT|  
|VW|VIEW DEFINITION|DATABASE|  
|VW|VIEW DEFINITION<br /> **Gilt für**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] und [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]. |DATABASE SCOPED CREDENTIAL|
|VW|VIEW DEFINITION|ENDPOINT|  
|VW|VIEW DEFINITION|FULLTEXT CATALOG|  
|VW|VIEW DEFINITION|FULLTEXT STOPLIST|  
|VW|VIEW DEFINITION|Anmeldung|  
|VW|VIEW DEFINITION|MESSAGE TYPE|  
|VW|VIEW DEFINITION|OBJECT|  
|VW|VIEW DEFINITION|REMOTE SERVICE BINDING|  
|VW|VIEW DEFINITION|ROLE|  
|VW|VIEW DEFINITION|ROUTE|  
|VW|VIEW DEFINITION|SCHEMA|  
|VW|VIEW DEFINITION|SEARCH PROPERTY LIST|  
|VW|VIEW DEFINITION<br /> **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [aktuelle Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|SERVER ROLE|  
|VW|VIEW DEFINITION|SERVICE|  
|VW|VIEW DEFINITION|SYMMETRIC KEY|  
|VW|VIEW DEFINITION|TYPE|  
|VW|VIEW DEFINITION|Benutzer|  
|VW|VIEW DEFINITION|XML SCHEMA COLLECTION|  
|VWAD|VIEW ANY DEFINITION|SERVER|  
|VWCK|VIEW ANY COLUMN ENCRYPTION KEY DEFINITION<br /> **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [aktuelle Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|DATABASE|  
|VWCM|VIEW ANY COLUMN MASTER KEY DEFINITION<br /> **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [aktuelle Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|DATABASE|  
|VWCT|VIEW CHANGE TRACKING|OBJECT|  
|VWCT|VIEW CHANGE TRACKING|SCHEMA|  
|VWDB|VIEW ANY DATABASE|SERVER|  
|VWDS|VIEW DATABASE STATE|DATABASE|  
|VWSS|VIEW SERVER STATE|SERVER|  
|XA|EXTERNAL ACCESS ASSEMBLY|SERVER|  
|XU|UNSAFE ASSEMBLY|SERVER|  
  
## <a name="remarks"></a>Hinweise  
 `sys.fn_builtin_permissions` ist eine Tabellenwertfunktion, die eine Kopie der vordefinierten Berechtigungshierarchie ausgibt. Diese Hierarchie schließt die abdeckenden Berechtigungen ein. Die `DEFAULT` Resultset beschreibt ein gerichtetes, azyklisches Diagramm der Berechtigungshierarchie, von denen der Stamm ist (Klasse = SERVER, Permission = CONTROL SERVER).  
  
 `sys.fn_builtin_permissions` nimmt keine korrelierten Parameter an.  
  
 `sys.fn_builtin_permissions` gibt ein leeres Resultset zurück, wenn beim Aufruf ein ungültiger Klassenname angegeben wird.  
 
[!INCLUDE[database-engine-permissions](../../includes/paragraph-content/database-engine-permissions.md)]
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der public-Rolle.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-listing-all-built-in-permissions"></a>A. Auflisten aller integrierten Berechtigungen   
Verwendung `DEFAULT` oder eine leere Zeichenfolge ein, um alle Berechtigungen zurück.   
```sql  
SELECT * FROM sys.fn_builtin_permissions(DEFAULT);
SELECT * FROM sys.fn_builtin_permissions('');  
```  
  
### <a name="b-listing-permissions-that-can-be-set-on-a-symmetric-key"></a>B. Auflisten der Berechtigungen, die für einen symmetrischen Schlüssel festgelegt werden können   
Geben Sie eine Klasse, um alle möglichen Berechtigungen für diese Klasse zurück.   
```sql  
SELECT * FROM sys.fn_builtin_permissions(N'SYMMETRIC KEY');  
```  
  
### <a name="c-listing-classes-on-which-there-is-a-select-permission"></a>C. Auflisten von Klassen, für die eine SELECT-Berechtigung vorhanden ist   
  
```sql  
SELECT * FROM sys.fn_builtin_permissions(DEFAULT)   
    WHERE permission_name = 'SELECT';  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Berechtigungshierarchie &#40;Datenbankmodul &#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [CREATE SCHEMA &#40;Transact-SQL&#41;](../../t-sql/statements/create-schema-transact-sql.md)   
 [DROP SCHEMA &#40;Transact-SQL&#41;](../../t-sql/statements/drop-schema-transact-sql.md)   
 [Berechtigungen &#40;Datenbankmodul&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [sys.fn_my_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)   
 [HAS_PERMS_BY_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/has-perms-by-name-transact-sql.md)  
  
  



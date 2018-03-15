---
title: CREATE USER (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 07/28/2017
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
f1_keywords:
- WITHOUT_LOGIN_TSQL
- CREATE_USER_TSQL
- SQL13.SWB.DATABASEUSER.OWNEDSCHEMAS.F1
- WITHOUT LOGIN
- CREATE USER
- ALLOW_ENCRYPTED_VALUE_MODIFICATIONS
- ALLOW_ENCRYPTED_VALUE_MODIFICATIONS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- adding users
- WITHOUT LOGIN [SQL Server]
- CREATE USER statement
- database user additions [SQL Server]
- USER WITHOUT LOGIN [SQL Server]
- users [SQL Server], adding
- users [SQL Server]
ms.assetid: 01de7476-4b25-4d58-85b7-1118fe64aa80
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: cc1b66f561ce413016e154bc329384566a8384b8
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="create-user-transact-sql"></a>CREATE USER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Fügt der aktuellen Datenbank einen Benutzer hinzu. Die elf Typen von Benutzern werden im Folgenden mit einem Beispiel der grundlegendsten Syntax aufgelistet:  
  
**Benutzer mit Anmeldenamen in der master-Datenbank** Dies ist der häufigste Benutzertyp.  
  
-   Benutzer mit Anmeldenamen auf Basis eines Windows Active Directory-Kontos. `CREATE USER [Contoso\Fritz];`     
-   Benutzer mit Anmeldenamen auf Basis einer Windows-Gruppe. `CREATE USER [Contoso\Sales];`   
-   Benutzer mit Anmeldenamen unter Verwendung der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung. `CREATE USER Mary;`  
  
**Benutzer, die sich in der Datenbank authentifizieren** Empfohlen, um Ihre Datenbank portierbarer zu machen.  
 Immer in [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] zugelassen. Nur in einer eigenständigen Datenbank in [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] zugelassen.  
  
-   Benutzer auf Basis eine Windows-Benutzers ohne Anmeldenamen. `CREATE USER [Contoso\Fritz];`    
-   Benutzer auf Basis einer Windows-Gruppe ohne Anmeldenamen. `CREATE USER [Contoso\Sales];`  
-   Benutzer in [!INCLUDE[ssSDS](../../includes/sssds-md.md)] oder [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] basierend auf einem Azure Active Directory-Benutzer. `CREATE USER [Contoso\Fritz] FROM EXTERNAL PROVIDER;`     

-   Benutzer einer eigenständigen Datenbank mit Kennwort. (Nicht in [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] verfügbar.) `CREATE USER Mary WITH PASSWORD = '********';`   
  
**Benutzer auf Basis von Windows-Prinzipalen, die eine Verbindung über Windows-Gruppenanmeldenamen herstellen**  
  
-   Benutzer auf Basis eines Windows-Benutzers ohne Anmeldenamen, die über die Mitgliedschaft in einer Windows-Gruppe eine Verbindung mit [!INCLUDE[ssDE](../../includes/ssde-md.md)] herstellen können. `CREATE USER [Contoso\Fritz];`  
  
-   Benutzer auf Basis einer Windows-Gruppe ohne Anmeldenamen, die über die Mitgliedschaft in einer anderen Windows-Gruppe eine Verbindung mit [!INCLUDE[ssDE](../../includes/ssde-md.md)] herstellen können. `CREATE USER [Contoso\Fritz];`  
  
**Benutzer ohne Authentifizierungsmöglichkeit** Diese Benutzer können sich nicht bei [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oder [!INCLUDE[ssSDS](../../includes/sssds-md.md)] anmelden.  
  
-   Benutzer ohne Anmeldenamen. Können sich nicht anmelden, jedoch Berechtigungen erhalten. `CREATE USER CustomApp WITHOUT LOGIN;`    
-   Benutzer auf Basis eines Zertifikats. Können sich nicht anmelden, jedoch Berechtigungen erhalten und Module signieren. `CREATE USER TestProcess FOR CERTIFICATE CarnationProduction50;`  
-   Benutzer auf Basis eines asymmetrischen Schlüssels. Können sich nicht anmelden, jedoch Berechtigungen erhalten und Module signieren. `CREATE User TestProcess FROM ASYMMETRIC KEY PacificSales09;`   
 
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
-- Syntax Users based on logins in master  
CREATE USER user_name   
    [   
        { FOR | FROM } LOGIN login_name   
    ]  
    [ WITH <limited_options_list> [ ,... ] ]   
[ ; ]  
  
--Users that authenticate at the database  
CREATE USER   
    {  
      windows_principal [ WITH <options_list> [ ,... ] ]  
  
    | user_name WITH PASSWORD = 'password' [ , <options_list> [ ,... ]   
    | Azure_Active_Directory_principal FROM EXTERNAL PROVIDER   
    }  
  
 [ ; ]  
  
--Users based on Windows principals that connect through Windows group logins  
CREATE USER   
    {   
          windows_principal [ { FOR | FROM } LOGIN windows_principal ]  
        | user_name { FOR | FROM } LOGIN windows_principal  
}  
    [ WITH <limited_options_list> [ ,... ] ]   
[ ; ]  
  
--Users that cannot authenticate   
CREATE USER user_name   
    {  
         WITHOUT LOGIN [ WITH <limited_options_list> [ ,... ] ]  
       | { FOR | FROM } CERTIFICATE cert_name   
       | { FOR | FROM } ASYMMETRIC KEY asym_key_name   
    }  
 [ ; ]  
  
<options_list> ::=  
      DEFAULT_SCHEMA = schema_name  
    | DEFAULT_LANGUAGE = { NONE | lcid | language name | language alias }  
    | SID = sid   
    | ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ ON | OFF ] ]  
  
<limited_options_list> ::=  
      DEFAULT_SCHEMA = schema_name ]   
    | ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ ON | OFF ] ]  
  
-- SQL Database syntax when connected to a federation member  
CREATE USER user_name  
[;]  
```  

```  
-- Syntax for Azure SQL Data Warehouse  
  
CREATE USER user_name   
    [ { { FOR | FROM } { LOGIN login_name }   
      | WITHOUT LOGIN  
    ]   
    [ WITH DEFAULT_SCHEMA = schema_name ]  
[;]

CREATE USER Azure_Active_Directory_principal FROM EXTERNAL PROVIDER  
    [ WITH DEFAULT_SCHEMA = schema_name ]  
[;]
``` 
  
```  
-- Syntax for Parallel Data Warehouse  
  
CREATE USER user_name   
    [ { { FOR | FROM }  
      {   
        LOGIN login_name   
      }   
      | WITHOUT LOGIN  
    ]   
    [ WITH DEFAULT_SCHEMA = schema_name ]  
[;]  
```  
  
## <a name="arguments"></a>Argumente  
 *user_name*  
 Gibt den Namen an, mit dem der Benutzer innerhalb dieser Datenbank identifiziert wird. *user_name* ist vom Datentyp **sysname**. Der Name kann bis zu 128 Zeichen lang sein. Wenn Sie einen Benutzer auf Basis eines Windows-Prinzipals erstellen, wird der Prinzipalname von Windows als Benutzername verwendet, es sei denn, ein abweichender Benutzername wird angegeben.  
  
 LOGIN *login_name*  
 Gibt die Anmeldung an, für die der Datenbankbenutzer erstellt wird. *login_name* muss ein gültiger Anmeldename im Server sein. Dies kann ein Anmeldename auf Basis eines Windows-Prinzipals (Benutzer oder Gruppe) oder ein Anmeldename mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung sein. Wird dieser [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldename zur Anmeldung in der Datenbank verwendet, erhält er den Namen und die ID des Datenbankbenutzers, der erstellt wird. Verwenden Sie das Format **[***\<domainName>***\\***\<loginName>***]**, wenn Sie einen von einem Windows-Prinzipal zugeordneten Anmeldenamen erstellen. Beispiele finden Sie unter [Syntaxzusammenfassung](#SyntaxSummary).  
  
 Wenn CREATE USER die einzige Anweisung in einem SQL-Batch ist, unterstützt Windows Azure SQL-Datenbank die WITH LOGIN-Klausel. Wenn CREATE USER nicht die einzige Anweisung in einem SQL-Batch ist oder in dynamischem SQL-Code ausgeführt wird, wird die WITH LOGIN-Klausel nicht unterstützt.  
  
 WITH DEFAULT_SCHEMA = *schema_name*  
 Gibt das erste Schema an, das vom Server beim Auflösen der Namen von Objekten für diesen Datenbankbenutzer durchsucht wird.  
  
 '*windows_principal*'  
 Gibt den Windows-Prinzipal an, für den der Datenbankbenutzer erstellt wird. *windows_principal* kann ein Windows-Benutzer oder eine Windows-Gruppe sein. Der Benutzer wird auch dann erstellt, wenn kein Anmeldename für *windows_principal* vorhanden ist. Wenn *windows_principal* beim Herstellen einer Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht über einen Anmeldenamen verfügt, muss vom Windows-Prinzipal über die Mitgliedschaft in einer Windows-Gruppe mit einem Anmeldenamen eine Authentifizierung bei [!INCLUDE[ssDE](../../includes/ssde-md.md)] durchgeführt werden, oder die eigenständige Datenbank muss in der Verbindungszeichenfolge als Anfangskatalog angegeben sein. Verwenden Sie das Format **[***\<domainName>***\\***\<loginName>***]**, wenn Sie einen Benutzer aus einem Windows-Prinzipal erstellen. Beispiele finden Sie unter [Syntaxzusammenfassung](#SyntaxSummary). Auf Active Directory-Benutzer basierende Benutzer sind auf Namen mit weniger als 21 Zeichen beschränkt.    
  
 '*Azure_Active_Directory_principal*'  
 **Gilt für**: [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)], [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)].  
  
 Gibt den Azure Active Directory-Prinzipal an, für den der Datenbankbenutzer erstellt wird. *Azure_Active_Directory_principal* kann ein Azure Active Directory-Benutzer oder eine Azure Active Directory-Gruppe sein. (Azure Active Directory-Benutzer können in [!INCLUDE[ssSDS](../../includes/sssds-md.md)] nicht über Windows-Authentifizierungsanmeldungen verfügen. Nur Datenbankbenutzer können dies tun.) Die Verbindungszeichenfolge muss die eigenständige Datenbank als den Anfangskatalog angeben. 

 Verwenden Sie für Benutzer den vollständigen Alias ihres Domänenprinzipals.   
 
-   `CREATE USER [bob@contoso.com] FROM EXTERNAL PROVIDER;`  
  
-   `CREATE USER [alice@fabrikam.onmicrosoft.com] FROM EXTERNAL PROVIDER;`

 Verwenden Sie für Sicherheitsgruppen den *Anzeigenamen* der Sicherheitsgruppe. Für die Sicherheitsgruppe *Nurses* verwenden Sie also Folgendes:  
  
-   `CREATE USER [Nurses] FROM EXTERNAL PROVIDER;`  
  
 Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit SQL-Datenbank unter Verwendung der Azure Active Directory-Authentifizierung](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication).  
  
WITH PASSWORD = '*password*'  
 **Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Kann nur in einer eigenständigen Datenbank verwendet werden. Gibt das Kennwort für den Benutzer an, der erstellt wird. Ab [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] werden gespeicherte Kennwortinformationen mithilfe der SHA-512-Komponente des mit Salt verschlüsselten Kennworts berechnet.  
  
WITHOUT LOGIN  
 Gibt an, dass der Benutzer keinem vorhandenen Anmeldenamen zugeordnet werden sollte.  
  
CERTIFICATE *cert_name*  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Gibt das Zertifikat an, für das der Datenbankbenutzer erstellt wird.  
  
ASYMMETRIC KEY *asym_key_name*  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Gibt den asymmetrischen Schlüssel an, für den der Datenbankbenutzer erstellt wird.  
  
DEFAULT_LANGUAGE = *{ NONE | \<lcid> | \<language name> | \<language alias> }*  
 **Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Gibt die Standardsprache für den neuen Benutzer an. Wenn eine Standardsprache für den Benutzer angegeben und die Standardsprache der Datenbank später geändert wird, hat dies keine Auswirkungen auf die Standardsprache des Benutzers. Wenn keine Standardsprache angegeben wird, entspricht die Standardsprache des Benutzers der Standardsprache der Datenbank. Wenn die Standardsprache des Benutzers nicht angegeben und die Standardsprache der Datenbank später geändert wird, wird die Standardsprache des Benutzers in die neue Standardsprache der Datenbank geändert.  
  
> [!IMPORTANT]  
>  *DEFAULT_LANGUAGE* wird nur für Benutzer von eigenständigen Datenbanken verwendet.  
  
SID = *sid*  
 **Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gilt nur für Benutzer mit Kennwörtern ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung) in einer eigenständigen Datenbank. Gibt die SID des neuen Datenbankbenutzers an. Wenn diese Option nicht ausgewählt wird, wird von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] automatisch ein SID zugewiesen. Erstellen Sie mit dem SID-Parameter Benutzer in mehreren Datenbanken, die die gleiche Identität (SID) aufweisen. Dies ist beim Erstellen von Benutzern in mehreren Datenbanken für die Vorbereitung eines Always On-Failovers hilfreich. Fragen Sie zum Bestimmen der SID eines Benutzers sys.database_principals ab.  
  
ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ ON | **OFF** ] ]  
 **Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Verhindert bei Massenkopiervorgängen kryptografische Metadatenüberprüfungen auf dem Server. Dadurch kann der Benutzer durch Massenkopiervorgänge Daten zwischen Tabellen oder Datenbanken austauschen, ohne dabei die Daten zu verschlüsseln. Der Standardwert ist OFF.  
  
> [!WARNING]  
>  Die falsche Verwendung dieser Option kann zur Datenbeschädigung führen. Weitere Informationen finden Sie unter [Migrieren von durch Always Encrypted geschützten sensiblen Daten](../../relational-databases/security/encryption/migrate-sensitive-data-protected-by-always-encrypted.md).  
  
## <a name="remarks"></a>Remarks  
 Wird FOR LOGIN ausgelassen, wird der neue Datenbankbenutzer dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen mit demselben Namen zugeordnet.  
  
 Das Standardschema ist das erste Schema, das vom Server beim Auflösen der Namen von Objekten für diesen Datenbankbenutzer durchsucht wird. Wenn nicht anders angegeben, ist das Standardschema der Besitzer von Objekten, die von diesem Datenbankbenutzer erstellt werden.  
  
 Wenn der Benutzer ein Standardschema hat, wird dieses Standardschema verwendet. Wenn der Benutzer kein Standardschema hat, aber Mitglied einer Gruppe mit einem Standardschema ist, wird das Standardschema der Gruppe verwendet. Wenn der Benutzer kein Standardschema hat und Mitglied von mehreren Gruppen ist, ist das Standardschema für den Benutzer das Schema der Windows-Gruppe mit der niedrigsten principal_id und explizit festgelegt. (Es ist nicht möglich, eines der verfügbaren Standardschemas als bevorzugtes Schema explizit auszuwählen.) Wenn für einen Benutzer kein Standardschema bestimmt werden kann, wird das Schema **dbo** verwendet.  
  
 DEFAULT_SCHEMA kann vor dem Erstellen des Schemas, auf das DEFAULT_SCHEMA zeigt, festgelegt werden.  
  
 DEFAULT_SCHEMA kann nicht angegeben werden, wenn Sie einen Benutzer erstellen, der einem Zertifikat oder einem asymmetrischen Schlüssel zugeordnet ist.  
  
 Der Wert von DEFAULT_SCHEMA wird ignoriert, wenn der Benutzer ein Mitglied der festen Serverrolle sysadmin ist. Alle Mitglieder der festen Serverrolle sysadmin verfügen über das Standardschema `dbo`.  
  
 Durch die WITHOUT LOGIN-Klausel wird ein Benutzer erstellt, der keiner SQL Server-Anmeldung zugeordnet ist. Er kann als guest Verbindungen mit anderen Datenbanken herstellen. Dem Benutzer ohne Anmeldung können Berechtigungen zugewiesen werden, und wenn der Sicherheitskontext in einen Benutzer ohne Anmeldung geändert wird, erhalten die ursprünglichen Benutzer die Berechtigungen des Benutzers ohne Anmeldung. Siehe Beispiel [D: Erstellen und Verwenden eines Benutzers ohne Anmeldename](#withoutLogin).  
  
 Nur Benutzernamen, die Windows-Prinzipalen zugeordnet sind, können den umgekehrten Schrägstrich (**\\**) enthalten.  
  
 Mithilfe von CREATE USER kann kein guest-Benutzer erstellt werden, da der guest-Benutzer bereits in jeder Datenbank vorhanden ist. Sie können den guest-Benutzer durch Erteilen der CONNECT-Berechtigung aktivieren (siehe Beispiel):  
  
```  
GRANT CONNECT TO guest;  
GO  
```  
  
 Informationen zu Datenbankbenutzern werden in der Katalogsicht [sys.database_principals](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md) angezeigt.  
  
##  <a name="SyntaxSummary"></a> Syntaxzusammenfassung  
 **Benutzer mit Anmeldenamen in der master-Datenbank**  
  
 Die folgende Liste enthält mögliche Syntaxen für Benutzer auf Basis von Anmeldenamen. Die Standardschemaoptionen sind nicht aufgeführt.  
  
-   `CREATE USER [Domain1\WindowsUserBarry]`  
-   `CREATE USER [Domain1\WindowsUserBarry] FOR LOGIN Domain1\WindowsUserBarry`  
-   `CREATE USER [Domain1\WindowsUserBarry] FROM LOGIN Domain1\WindowsUserBarry`  
-   `CREATE USER [Domain1\WindowsGroupManagers]`  
-   `CREATE USER [Domain1\WindowsGroupManagers] FOR LOGIN [Domain1\WindowsGroupManagers]`  
-   `CREATE USER [Domain1\WindowsGroupManagers] FROM LOGIN [Domain1\WindowsGroupManagers]`  
-   `CREATE USER SQLAUTHLOGIN`  
-   `CREATE USER SQLAUTHLOGIN FOR LOGIN SQLAUTHLOGIN`  
-   `CREATE USER SQLAUTHLOGIN FROM LOGIN SQLAUTHLOGIN`  
  
**Benutzer mit Authentifizierung bei der Datenbank**  
  
 Die folgende Liste enthält mögliche Syntaxen für Benutzer, die nur in einer eigenständigen Datenbank verwendet werden können. Die erstellten Benutzer weisen keine Beziehung zu Anmeldenamen in der **master**-Datenbank auf. Das Standardschema und die Sprachoptionen sind nicht aufgeführt.  
  
> [!IMPORTANT]  
>  Diese Syntax gewährt Benutzern Zugriff auf die Datenbank sowie neuen Zugriff auf [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
-   `CREATE USER [Domain1\WindowsUserBarry]`  
-   `CREATE USER [Domain1\WindowsGroupManagers]`  
-   `CREATE USER Barry WITH PASSWORD = 'sdjklalie8rew8337!$d'`  
  
**Benutzer auf Basis eines Windows-Prinzipals ohne Anmeldenamen in der master-Datenbank**  
  
 Die folgende Liste enthält verschiedene Syntaxmöglichkeiten für Benutzer mit Zugriff auf [!INCLUDE[ssDE](../../includes/ssde-md.md)] über eine Windows-Gruppe, die nicht über einen Anmeldenamen in der **master**-Datenbank verfügen. Diese Syntax kann in allen Datenbanktypen verwendet werden. Das Standardschema und die Sprachoptionen sind nicht aufgeführt.  
  
 Diese Syntax ähnelt der von Benutzern mit Anmeldenamen in der master-Datenbank; im Unterschied dazu fehlt hier jedoch der Anmeldename für die master-Datenbank. Der Benutzer muss über den Anmeldenamen einer Windows-Gruppe Zugriff auf [!INCLUDE[ssDE](../../includes/ssde-md.md)] haben.  
  
 Diese Syntax ähnelt der von Benutzern eigenständiger Datenbanken auf Basis von Windows-Prinzipalen, im Unterschied dazu fehlt hier jedoch der neue Zugriff auf [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
-   `CREATE USER [Domain1\WindowsUserBarry]`  
-   `CREATE USER [Domain1\WindowsUserBarry] FOR LOGIN Domain1\WindowsUserBarry`  
-   `CREATE USER [Domain1\WindowsUserBarry] FROM LOGIN Domain1\WindowsUserBarry`  
-   `CREATE USER [Domain1\WindowsGroupManagers]`  
-   `CREATE USER [Domain1\WindowsGroupManagers] FOR LOGIN [Domain1\WindowsGroupManagers]`  
-   `CREATE USER [Domain1\WindowsGroupManagers] FROM LOGIN [Domain1\WindowsGroupManagers]`  
  
**Benutzer ohne Authentifizierungsmöglichkeit**  
  
 Die folgende Liste enthält mögliche Syntaxen für Benutzer, die sich nicht bei [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anmelden können.  
  
-   `CREATE USER RIGHTSHOLDER WITHOUT LOGIN`  
-   `CREATE USER CERTUSER FOR CERTIFICATE SpecialCert`  
-   `CREATE USER CERTUSER FROM CERTIFICATE SpecialCert`  
-   `CREATE USER KEYUSER FOR ASYMMETRIC KEY SecureKey`  
-   `CREATE USER KEYUSER FROM ASYMMETRIC KEY SecureKey`  
  
## <a name="security"></a>Security  
 Wenn Sie einen Benutzer erstellen, erhält dieser zwar Zugriff auf eine Datenbank, nicht jedoch notwendigerweise auch auf die darin enthaltenen Objekte. Nach dem Erstellen eines Benutzers wird dieser daher häufig einer oder mehreren Datenbankrollen hinzugefügt, die über Zugriffsberechtigungen für entsprechende Objekte verfügen, oder dem Benutzer werden Berechtigungen für einzelne Objekte erteilt. Informationen zum Entwerfen eines Berechtigungssystems finden Sie unter [Getting Started with Database Engine Permissions](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md).  
  
### <a name="special-considerations-for-contained-databases"></a>Spezielle Überlegungen zu eigenständigen Datenbanken  
 Wenn ein Benutzer beim Herstellen einer Verbindung mit einer eigenständigen Datenbank nicht über einen Anmeldenamen in der **master**-Datenbank verfügt, muss die Verbindungszeichenfolge den Namen der eigenständigen Datenbank als Anfangskatalog beinhalten. Der Anfangskatalogparameter ist für Benutzer von eigenständigen Datenbanken mit Kennwort stets erforderlich.  
  
 In einer eigenständigen Datenbank hilft das Erstellen von Benutzern, eine Trennung zwischen der Datenbank und der Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] herzustellen, damit die Datenbank leichter in eine andere Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verschoben werden kann. Weitere Informationen finden Sie unter [Eigenständige Datenbanken](../../relational-databases/databases/contained-databases.md) und [Eigenständige Datenbankbenutzer – machen Sie Ihre Datenbank portabel](../../relational-databases/security/contained-database-users-making-your-database-portable.md). Informationen zum Ändern eines Datenbankbenutzers von einem Benutzer mit Anmeldenamen auf Basis einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung in den Benutzer einer eigenständigen Datenbank mit Kennwort finden Sie unter [sp_migrate_user_to_contained &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-migrate-user-to-contained-transact-sql.md).  
  
 Benutzer in einer eigenständigen Datenbank müssen nicht über Anmeldenamen in der **master**-Datenbank verfügen. Administratoren von [!INCLUDE[ssDE](../../includes/ssde-md.md)] sollten wissen, dass der Zugriff auf eine eigenständige Datenbank auf Datenbankebene und nicht auf der Ebene von [!INCLUDE[ssDE](../../includes/ssde-md.md)] gesteuert wird. Weitere Informationen finden Sie unter [Security Best Practices with Contained Databases](../../relational-databases/databases/security-best-practices-with-contained-databases.md).  
  
 Bei Verwendung der in Datenbanken enthaltenen Benutzern auf [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] konfigurieren Sie den Zugriff mithilfe einer Firewallregel auf Datenbankebene, anstatt einer Firewallregel auf Serverebene. Weitere Informationen finden Sie unter [sp_set_database_firewall_rule &#40;Azure SQL-Datenbank&#41;](../../relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database.md).
 
Für eigenständige Datenbankbenutzer in [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] und [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] kann SSMS Multi-Factor Authentication unterstützen. Weitere Informationen hierzu finden Sie unter [SSMS-Unterstützung für Azure AD MFA mit SQL-Datenbank und SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-database-ssms-mfa-authentication/).  
  
### <a name="permissions"></a>Berechtigungen  
 Erfordert die ALTER ANY USER-Berechtigung in der Datenbank.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-creating-a-database-user-based-on-a-sql-server-login"></a>A. Erstellen eines Datenbankbenutzers auf Basis einer SQL Server-Anmeldung  
 Im folgenden Beispiel wird zunächst der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldename `AbolrousHazem` und anschließend der zugehörige Datenbankbenutzer `AbolrousHazem` in `AdventureWorks2012` erstellt.  
  
```  
CREATE LOGIN AbolrousHazem   
    WITH PASSWORD = '340$Uuxwp7Mcxo7Khy';  
```   
Wechseln Sie zu einer Benutzerdatenbank. Verwenden Sie zum Beispiel in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Anweisung `USE AdventureWorks2012`. In [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] müssen Sie eine neue Verbindung zur Benutzerdatenbank herstellen.

```   
CREATE USER AbolrousHazem FOR LOGIN AbolrousHazem;  
GO   
```  
  
### <a name="b-creating-a-database-user-with-a-default-schema"></a>B. Erstellen eines Datenbankbenutzers mit einem Standardschema  
 Im folgenden Beispiel wird zunächst ein Serveranmeldename namens `WanidaBenshoof` mit einem Kennwort und dann der entsprechende Datenbankbenutzer `Wanida` mit dem Standardschema `Marketing` erstellt.  
  
```  
CREATE LOGIN WanidaBenshoof   
    WITH PASSWORD = '8fdKJl3$nlNv3049jsKK';  
USE AdventureWorks2012;  
CREATE USER Wanida FOR LOGIN WanidaBenshoof   
    WITH DEFAULT_SCHEMA = Marketing;  
GO  
```  
  
### <a name="c-creating-a-database-user-from-a-certificate"></a>C. Erstellen eines Datenbankbenutzers über ein Zertifikat  
 Im folgenden Beispiel wird der Datenbankbenutzer `JinghaoLiu` über das `CarnationProduction50`-Zertifikat erstellt.  
  
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
USE AdventureWorks2012;  
CREATE CERTIFICATE CarnationProduction50  
    WITH SUBJECT = 'Carnation Production Facility Supervisors',  
    EXPIRY_DATE = '11/11/2011';  
GO  
CREATE USER JinghaoLiu FOR CERTIFICATE CarnationProduction50;  
GO   
```  
  
###  <a name="withoutLogin"></a> D. Erstellen und Verwenden eines Benutzers ohne Anmeldename  
 Im folgenden Beispiel wird ein `CustomApp`-Datenbankbenutzer erstellt, dem kein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldename zugeordnet wird. Anschließend wird einem Benutzer die `adventure-works\tengiz0`-Berechtigung zugewiesen, um die Identität des `CustomApp`-Benutzers anzunehmen.  
  
```  
USE AdventureWorks2012 ;  
CREATE USER CustomApp WITHOUT LOGIN ;  
GRANT IMPERSONATE ON USER::CustomApp TO [adventure-works\tengiz0] ;  
GO   
```  
  
 Zur Verwendung der `CustomApp`-Anmeldeinformationen führt der `adventure-works\tengiz0`-Benutzer die folgende Anweisung aus.  
  
```  
EXECUTE AS USER = 'CustomApp' ;  
GO  
```  
  
 Zur Wiederherstellung der `adventure-works\tengiz0`-Anmeldeinformationen führt der Benutzer die folgende Anweisung aus.  
  
```  
REVERT ;  
GO  
```  
  
### <a name="e-creating-a-contained-database-user-with-password"></a>E. Erstellen eines Benutzers einer eigenständigen Datenbank mit Kennwort  
 Im folgenden Beispiel wird der Benutzer einer eigenständigen Datenbank mit Kennwort erstellt. Dieses Beispiel kann nur in einer eigenständigen Datenbank ausgeführt werden.  
  
**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Dieses Beispiel funktioniert in [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)], wenn DEFAULT_LANGUAGE entfernt wird.  
  
```  
USE AdventureWorks2012 ;  
GO  
CREATE USER Carlo  
WITH PASSWORD='RN92piTCh%$!~3K9844 Bl*'  
    , DEFAULT_LANGUAGE=[Brazilian]  
    , DEFAULT_SCHEMA=[dbo]  
GO   
```  
  
### <a name="f-creating-a-contained-database-user-for-a-domain-login"></a>F. Erstellen eines Benutzers einer eigenständigen Datenbank für eine Domänenanmeldung  
 Im folgenden Beispiel wird ein Benutzer für eine eigenständige Datenbank mit dem Anmeldenamen „Fritz“ in der Domäne „Contoso“ erstellt. Dieses Beispiel kann nur in einer eigenständigen Datenbank ausgeführt werden.  
  
**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
USE AdventureWorks2012 ;  
GO  
CREATE USER [Contoso\Fritz] ;  
GO   
```  
  
### <a name="g-creating-a-contained-database-user-with-a-specific-sid"></a>G. Erstellen eines Benutzers einer eigenständigen Datenbank mit einer bestimmten SID  
 Im folgenden Beispiel wird ein authentifizierter SQL Server-Benutzer einer eigenständigen Datenbank mit dem Namen CarmenW erstellt. Dieses Beispiel kann nur in einer eigenständigen Datenbank ausgeführt werden.  
  
**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
USE AdventureWorks2012 ;  
GO  
CREATE USER CarmenW WITH PASSWORD = 'a8ea v*(Rd##+'  
, SID = 0x01050000000000090300000063FF0451A9E7664BA705B10E37DDC4B7;  
  
```  
  
### <a name="h-creating-a-user-to-copy-encrypted-data"></a>H. Erstellen eines Benutzers zum Kopieren von verschlüsselten Daten  
 Im folgenden Beispiel wird ein Benutzer erstellt, der durch das Feature „Always Encrypted“ geschützte Daten aus einem Tabellensatz mit verschlüsselten Spalten in einen anderen Tabellensatz mit verschlüsselten Spalten kopieren kann (innerhalb derselben oder zu einer anderen Datenbank).  Weitere Informationen finden Sie unter [Migrieren von durch Always Encrypted geschützten sensiblen Daten](../../relational-databases/security/encryption/migrate-sensitive-data-protected-by-always-encrypted.md).  
  
**Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
```  
CREATE USER [Chin]   
WITH   
      DEFAULT_SCHEMA = dbo  
    , ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = ON ;  
```  
  

## <a name="next-steps"></a>Nächste Schritte  
Ziehen Sie in Betracht, den Benutzer mithilfe der Anweisung [ALTER ROLE](../../t-sql/statements/alter-role-transact-sql.md) einer Datenbankrolle hinzuzufügen, sobald dieser erstellt wurde.  
Möglicherweise möchten Sie der Rolle [GRANT-Objektberechtigungen](../../t-sql/statements/grant-object-permissions-transact-sql.md) zuweisen, damit sie auf Tabellen zugreifen können. Allgemeine Informationen über das Sicherheitsmodell von SQL Server finden Sie unter [Berechtigungen](../../relational-databases/security/permissions-database-engine.md).   
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erstellen eines Datenbankbenutzers](../../relational-databases/security/authentication-access/create-a-database-user.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [ALTER USER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-user-transact-sql.md)   
 [DROP USER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-user-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [Eigenständige Datenbanken](../../relational-databases/databases/contained-databases.md)   
 [Herstellen einer Verbindung mit SQL-Datenbank unter Verwendung der Azure Active Directory-Authentifizierung](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication)   
 [Erste Schritte mit Berechtigungen für das Datenbankmodul](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)  
  
  



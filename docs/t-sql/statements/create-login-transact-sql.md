---
title: ANMELDUNGSERSTELLUNG (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/15/2017
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
- CREATE_LOGIN_TSQL
- CREATE LOGIN
- LOGIN_TSQL
- LOGIN
dev_langs:
- TSQL
helpviewer_keywords:
- passwords [SQL Server], logins
- mapping logins [SQL Server]
- logins [SQL Server], creating
- CREATE LOGIN statement
- permissions [SQL Server], logins
- Windows domain accounts [SQL Server]
- re-hashing passwords
- certificates [SQL Server], logins
ms.assetid: eb737149-7c92-4552-946b-91085d8b1b01
caps.latest.revision: 101
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: e0b84743a9c3c578954560613c69f2863af8aa01
ms.contentlocale: de-de
ms.lasthandoff: 10/24/2017

---
# <a name="create-login-transact-sql"></a>CREATE LOGIN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Erstellt eine [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Anmeldung für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server  
  
CREATE LOGIN login_name { WITH <option_list1> | FROM <sources> }  
  
<option_list1> ::=   
    PASSWORD = { 'password' | hashed_password HASHED } [ MUST_CHANGE ]  
    [ , <option_list2> [ ,... ] ]  
  
<option_list2> ::=    
    SID = sid  
    | DEFAULT_DATABASE = database      
    | DEFAULT_LANGUAGE = language  
    | CHECK_EXPIRATION = { ON | OFF}  
    | CHECK_POLICY = { ON | OFF}  
    | CREDENTIAL = credential_name   
  
<sources> ::=  
    WINDOWS [ WITH <windows_options>[ ,... ] ]  
    | CERTIFICATE certname  
    | ASYMMETRIC KEY asym_key_name  
  
<windows_options> ::=        
    DEFAULT_DATABASE = database  
    | DEFAULT_LANGUAGE = language  
```  
  
```  
-- Syntax for Azure SQL Database and Azure SQL Data Warehouse  
  
CREATE LOGIN login_name  
 { WITH <option_list3> }  
  
<option_list3> ::=   
    PASSWORD = { 'password' }  
    [ SID = sid ]  
```  
  
```  
-- Syntax for Parallel Data Warehouse  
  
CREATE LOGIN loginName { WITH <option_list1> | FROM WINDOWS }  
  
<option_list1> ::=   
    PASSWORD = { 'password' } [ MUST_CHANGE ]  
    [ , <option_list2> [ ,... ] ]  
  
<option_list2> ::=    
      CHECK_EXPIRATION = { ON | OFF}  
    | CHECK_POLICY = { ON | OFF}  
```  
  
## <a name="arguments"></a>Argumente  
 *login_name*  
 Gibt den Anmeldenamen an, der erstellt wird. Es gibt vier Arten von Anmeldenamen: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen, Windows-Anmeldenamen, Anmeldenamen mit zugeordneten Zertifikaten sowie Anmeldenamen mit zugeordneten asymmetrischen Schlüsseln. Beim Erstellen von Anmeldungen, die zugeordnet werden von einem Windows-Domänenkonto ausführen, müssen Sie den Benutzeranmeldenamen ein Prä-Windows 2000 verwenden, im Format [\<DomainName >\\< Login_name >]. Können keine UPN im Format login_name@DomainName. Ein Beispiel hierzu finden Sie unter "Beispiel D" weiter unten in diesem Thema. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-authentifizierungsanmeldungen sind vom Typ **Sysname** und entsprechen den Regeln für [Bezeichner](http://msdn.microsoft.com/library/ms175874.aspx) und darf keine enthalten eine "**\\**". Windows-Anmeldenamen darf eine '**\\**". Anmeldungen auf Grundlage von Active Directory-Benutzer sind Namen von weniger als 21 Zeichen beschränkt.  
  
 Kennwort **= "***Kennwort***"**  
 Gilt nur für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen. Gibt das Kennwort für den Anmeldenamen an, der erstellt wird. Sie sollten ein sicheres Kennwort verwenden. Weitere Informationen finden Sie unter [Strong Passwords](../../relational-databases/security/strong-passwords.md) und [Kennwortrichtlinie](../../relational-databases/security/password-policy.md). Beginnend mit [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]gespeicherten Kennwortinformationen wird mithilfe von SHA-512, des Kennworts nach dem Zufallsprinzip gewählter berechnet.  
  
 Bei Kennwörtern wird nach Groß- und Kleinschreibung unterschieden. Kennwörter sollten immer mindestens 8 Zeichen lang sein und dürfen 128 Zeichen nicht überschreiten.  Kennwörter dürfen a-z, A-Z, 0-9 und die meisten nicht alphanumerischen Zeichen einschließen. Kennwörter sind keine einfachen Anführungszeichen oder *Login_name*.  
  
 Kennwort  **=**  *Hashed_password*  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gilt nur für das HASHED-Schlüsselwort. Gibt den Hashwert des Kennworts für den Anmeldenamen an, der erstellt wird.  
  
 HASHED  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gilt nur für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen. Gibt an, dass das nach dem PASSWORD-Argument eingegebene Kennwort bereits einen Hashwert darstellt. Wenn diese Option nicht ausgewählt wird, wird aus der als Kennwort eingegebenen Zeichenfolge vor dem Speichern in der Datenbank ein Hashwert erstellt. Diese Option sollte nur verwendet werden, um Datenbanken von einem Server auf einen anderen zu migrieren. Verwenden Sie die HASHED-Option nicht, um neue Anmeldenamen zu erstellen. Die HASHED-Option kann nicht mit Hashes verwendet werden, die in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7 oder einer früheren Version erstellt wurden.  
  
 MUST_CHANGE  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gilt nur für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen. Wenn diese Option angegeben wird, wird der Benutzer von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zur Eingabe eines neuen Kennworts aufgefordert, wenn der neue Anmeldename zum ersten Mal verwendet wird.  
  
 Anmeldeinformationen  **=**  *Credential_name*  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Die Anmeldeinformationen, die dem neuen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen zugeordnet werden sollen. Die Anmeldeinformationen müssen bereits auf dem Server vorhanden sein. Momentan verknüpft diese Option nur die Anmeldeeinformationen mit einem Anmeldenamen. Anmeldeinformationen kann der Systemadministrator (sa)-Anmeldung zugeordnet werden.  
  
 SID = *Sid*  
 Wird verwendet, um eine Anmeldung neu zu erstellen. Gilt für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nur-authentifizierungsanmeldungen, nicht Windows-authentifizierungsanmeldungen. Gibt die SID des neuen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -authentifizierungsanmeldung. Wenn diese Option nicht verwendet wird, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] automatisch ein SID zugewiesen. Die SID-Struktur hängt die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Version.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Anmelde-SID: ein 16-Byte (**binary(16)**) Literalwert basierend auf einer GUID. Beispiel: `SID = 0x14585E90117152449347750164BA00A7`.  
  
-   [!INCLUDE[ssSDS](../../includes/sssds-md.md)]Anmelde-SID: eine SID-Struktur gültig für [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. Dies ist normalerweise ein 32-Byte (**binary(32)**) Literalwert bestehend `0x01060000000000640000000000000000` plus 16 Bytes, die eine GUID darstellt. Beispiel: `SID = 0x0106000000000064000000000000000014585E90117152449347750164BA00A7`.  
  
DEFAULT_DATABASE  **=**  *Datenbank*  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt die Standarddatenbank an, die dem Anmeldenamen zugewiesen werden soll. Die Standarddatenbank wird festgelegt, wenn diese Option nicht enthalten ist, um Master.  
  
DEFAULT_LANGUAGE  **=**  *Sprache*  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt die Standardsprache an, die dem Anmeldenamen zugewiesen werden soll. Wenn diese Option nicht enthalten ist, wird die aktuelle Standardsprache des Servers als Standardsprache festgelegt. Wenn die Standardsprache des Servers zu einem späteren Zeitpunkt geändert wird, wird die Standardsprache des Anmeldenamens nicht geändert.  
  
CHECK_EXPIRATION  **=**  {ON | **OFF** }  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gilt nur für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen. Gibt an, ob die Richtlinie für das Ablaufen von Kennwörtern für diesen Anmeldenamen erzwungen werden soll. Der Standardwert ist OFF.  
  
CHECK_POLICY  **=**  { **ON** | {OFF}  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gilt nur für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen. Gibt an, dass die Windows-Kennwortrichtlinien des Computers, auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird, für diesen Anmeldenamen erzwungen werden sollen. Der Standardwert ist ON.  
  
 Wenn die Windows-Richtlinie sichere Kennwörter erfordert, müssen Kennwörter mindestens drei der folgenden vier Eigenschaften aufweisen:  
  
-   Ein Großbuchstabe (A-Z).  
-   Ein Kleinbuchstabe (a-z).  
-   Eine Ziffer (0-9).  
-   Ein nicht alphanumerisches Zeichen, z. B. ein Leerzeichen, _, @, *, ^,%, !, $, # oder &.  
  
WINDOWS  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt an, dass der Anmeldename einem Windows-Anmeldenamen zugeordnet wird.  
  
Zertifikat *Certname*  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt den Namen eines Zertifikats an, das diesem Anmeldenamen zugeordnet werden soll. Dieses Zertifikat muss bereits in der master-Datenbank auftreten.  
  
ASYMMETRISCHE Schlüssel *Asym_key_name*  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt den Namen eines asymmetrischen Schlüssels an, der diesem Anmeldenamen zugeordnet werden soll. Dieser Schlüssel muss bereits in der master-Datenbank auftreten.  
  
## <a name="remarks"></a>Hinweise  
 Bei Kennwörtern wird nach Groß- und Kleinschreibung unterschieden.  
  
 Das vorherige Erstellen von Hashwerten für Kennwörter wird nur unterstützt, wenn Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen erstellen.  
  
 Falls MUST_CHANGE angegeben wird, müssen CHECK_EXPIRATION und CHECK_POLICY auf ON festgelegt werden. Andernfalls erzeugt die Anweisung einen Fehler.  
  
 Die Kombination aus CHECK_POLICY = OFF und CHECK_EXPIRATION = ON wird nicht unterstützt.  
  
 Wenn CHECK_POLICY auf OFF gesetzt ist *Lockout_time* zurückgesetzt und CHECK_EXPIRATION auf OFF festgelegt ist.  
  
> [!IMPORTANT]  
>  CHECK_EXPIRATION und CHECK_POLICY werden nur unter [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] und höher erzwungen. Weitere Informationen finden Sie unter [Password Policy](../../relational-databases/security/password-policy.md).  
  
 Aus Zertifikaten oder asymmetrischen Schlüsseln erstellte Anmeldenamen werden nur zum Signieren von Code verwendet. Sie können nicht verwendet werden, um eine Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herzustellen. Sie können eine Anmeldung aus einem Zertifikat oder asymmetrischen Schlüssel erstellen, nur, wenn das Zertifikat oder den asymmetrischen Schlüssel bereits in der Masterdatenbank vorhanden ist.  
  
 Ein Skript zum Übertragen von Anmeldungen, finden Sie unter [zum Übertragen von Benutzernamen und Kennwörter zwischen Instanzen von SQL Server 2005 und SQL Server 2008](http://support.microsoft.com/kb/918992).  
  
 Automatisch beim Erstellen eines Anmeldenamens ermöglicht es den neuen Anmeldenamen und erteilt ihm die Serverebene **CONNECT SQL** Berechtigung.  
  
 Informationen zum Entwerfen eines Berechtigungssystems finden Sie unter [Getting Started with Database Engine Permissions](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md).  
  
## <a name="includesssdsfullincludessssdsfull-mdmd-and-includesssdwincludessssdw-mdmd-logins"></a>[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]und [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] Anmeldungen  
 In [!INCLUDE[ssSDS](../../includes/sssds-md.md)], **CREATE LOGIN** Anweisung muss die einzige Anweisung in einem Batch sein.  
  
 Bei einigen Methoden zur verbindungsherstellung mit [!INCLUDE[ssSDS](../../includes/sssds-md.md)], wie z. B. **Sqlcmd**, muss angefügt der [!INCLUDE[ssSDS](../../includes/sssds-md.md)] Servernamen, um den Anmeldenamen in der Verbindungszeichenfolge mittels der  *\<Anmeldung >* @  *\<Server >* Notation. Lautet die Anmeldung also beispielsweise `login1` und den vollqualifizierten Namen des der [!INCLUDE[ssSDS](../../includes/sssds-md.md)] Server `servername.database.windows.net`, die *Benutzername* Parameter der Verbindungszeichenfolge muss `login1@servername`. Da die Gesamtlänge der der *Benutzername* Parameter beträgt 128 Zeichen *Login_name* ist auf 127 Zeichen abzüglich der Länge des Servernamens beschränkt. Im Beispiel darf `login_name` nur 117 Zeichen lang sein, da `servername` 10 Zeichen enthält.  
  
 In [!INCLUDE[ssSDS](../../includes/sssds-md.md)] und [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] müssen Sie mit der Masterdatenbank eine Anmeldung verbunden werden.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Regeln erstellen Sie eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -authentifizierungsanmeldung im Format \<Loginname > @\<Servername >. Wenn Ihre [!INCLUDE[ssSDS](../../includes/sssds-md.md)] Server **Myazureserver** und der Anmeldename  **myemail@live.com** , und Sie Sie den Anmeldenamen als geben müssen  **myemail@live.com @myazureserver**  .  
  
 In [!INCLUDE[ssSDS](../../includes/sssds-md.md)], Anmeldedaten erforderlich, um eine Verbindung zu authentifizieren und Firewallregeln auf Serverebene werden in jeder Datenbank vorübergehend zwischengespeichert. Dieser Cache wird in regelmäßigen Abständen aktualisiert. Führen Sie zum Erzwingen einer Aktualisierung des Authentifizierungscache und stellen Sie sicher, dass eine Datenbank die aktuelle Version der Tabelle Anmeldungen verfügt, [DBCC FLUSHAUTHCACHE &#40; Transact-SQL &#41; ](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md).  
  
 Weitere Informationen zu [!INCLUDE[ssSDS](../../includes/sssds-md.md)] anzeigen Anmeldenamen [Verwalten von Datenbanken und Anmeldungen in Windows Azure SQL-Datenbank](http://msdn.microsoft.com/library/ee336235.aspx).  
  
## <a name="permissions"></a>Berechtigungen  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], erfordert **ALTER ANY LOGIN** Berechtigung auf dem Server oder die Mitgliedschaft in der **"securityadmin"** festen Serverrolle "".  
  
 In [!INCLUDE[ssSDS](../../includes/sssds-md.md)] können nur die Prinzipalanmeldenamen auf Serverebene (vom Bereitstellungsprozess erstellt) oder die Mitglieder der Datenbankrolle `loginmanager` in der master-Datenbank neue Anmeldenamen erstellen.  
  
 Wenn die **Anmeldeinformationen** Option verwendet wird, erfordert auch **ALTER ANY CREDENTIAL** Berechtigung auf dem Server.  
  
## <a name="next-steps"></a>Nächste Schritte  
 Nach dem Erstellen einer Anmeldung, die Anmeldung kann eine Verbindung mit der [!INCLUDE[ssDE](../../includes/ssde-md.md)] oder [!INCLUDE[ssSDS](../../includes/sssds-md.md)] aber nur über die Berechtigungen für die **öffentlichen** Rolle. Ziehen Sie das Ausführen einiger der folgenden Aktivitäten in Betracht.  
  
-   Erstellen Sie zum Herstellen einer Verbindung mit einer Datenbank einen Datenbankbenutzer für den Anmeldenamen. Weitere Informationen finden Sie unter [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md).  
  
-   Erstellen Sie eine benutzerdefinierte Serverrolle mit [CREATE SERVER ROLE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-server-role-transact-sql.md). Verwendung **ALTER SERVER ROLE** ... **ADD MEMBER** der benutzerdefinierten Serverrolle den neuen Anmeldenamen hinzu. Weitere Informationen finden Sie unter [CREATE SERVER ROLE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-server-role-transact-sql.md) und [ALTER SERVER ROLE &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-server-role-transact-sql.md).  
  
-   Verwendung **Sp_addsrvrolemember** so der Anmeldename einer festen Serverrolle hinzu. Weitere Informationen finden Sie unter [Rollen auf Serverebene](../../relational-databases/security/authentication-access/server-level-roles.md) und [Sp_addsrvrolemember &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md).  
  
-   Verwenden der **GRANT** Anweisung ein, um Berechtigungen auf Serverebene mit dem neuen Anmeldenamen oder einer Rolle mit der Anmeldung zu gewähren. Weitere Informationen finden Sie unter [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md).  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-creating-a-login-with-a-password"></a>A. Erstellen einer Anmeldung mit einem Kennwort  
 Im folgenden Beispiel wird ein Anmeldename für einen bestimmten Benutzer erstellt, und es wird ein Kennwort zugewiesen.  
  
```  
CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>';  
GO  
```  
  
### <a name="b-creating-a-login-with-a-password"></a>B. Erstellen einer Anmeldung mit einem Kennwort  
 Im folgenden Beispiel wird ein Anmeldename für einen bestimmten Benutzer erstellt, und es wird ein Kennwort zugewiesen. Die Option `MUST_CHANGE` erfordert, dass Benutzer dieses Kennwort ändern, wenn sie das erste Mal eine Verbindung mit dem Server herstellen.  
  
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>' MUST_CHANGE;  
GO  
```  
  
### <a name="c-creating-a-login-mapped-to-a-credential"></a>C. Erstellen eines Anmeldenamens, der Anmeldeinformationen zugeordnet ist  
 Im folgenden Beispiel wird unter Verwendung des Benutzers der Anmeldename für einen bestimmten Benutzer erstellt. Dieser Anmeldename wird den Anmeldeinformationen zugeordnet.  
  
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>',   
    CREDENTIAL = <credentialName>;  
GO  
```  
  
### <a name="d-creating-a-login-from-a-certificate"></a>D. Erstellen eines Anmeldenamens aus einem Zertifikat  
 Das folgende Beispiel erstellt Anmeldename für einen bestimmten Benutzer aus einem Zertifikat in der Masterdatenbank.  
  
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
USE MASTER;  
CREATE CERTIFICATE <certificateName>  
    WITH SUBJECT = '<login_name> certificate in master database',  
    EXPIRY_DATE = '12/05/2025';  
GO  
CREATE LOGIN <login_name> FROM CERTIFICATE <certificateName>;  
GO  
```  
  
### <a name="e-creating-a-login-from-a-windows-domain-account"></a>E. Erstellen eines Anmeldenamens von einem Windows-Domänenkonto  
 Im folgenden Beispiel wird ein Anmeldename von einem Windows-Domänenkonto erstellt.  
  
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
CREATE LOGIN [<domainName>\<login_name>] FROM WINDOWS;  
GO  
```  
  
### <a name="f-creating-a-login-from-a-sid"></a>F. Erstellen eines Anmeldenamens aus einer SID  
 Das folgende Beispiel erstellt zuerst eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldenamen für die Authentifizierung und bestimmt die SID des Anmeldenamens.  
  
```  
CREATE LOGIN TestLogin WITH PASSWORD = 'SuperSecret52&&';  
  
SELECT name, sid FROM sys.sql_logins WHERE name = 'TestLogin';  
GO  
```  
  
 Meine Abfrage gibt 0x241C11948AEEB749B0D22646DB1A19F2 als SID zurück. Die Abfrage gibt einen anderen Wert zurück. Die folgenden Anweisungen löschen den Anmeldenamen und erstellen dann erneut die Anmeldung. Verwenden Sie die SID aus der vorherigen Abfrage.  
  
```  
DROP LOGIN TestLogin;  
GO  
  
CREATE LOGIN TestLogin   
WITH PASSWORD = 'SuperSecret52&&', SID = 0x241C11948AEEB749B0D22646DB1A19F2;  
  
SELECT * FROM sys.sql_logins WHERE name = 'TestLogin';  
GO  
```  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>Beispiele:[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="g-creating-a-sql-server-authentication-login-with-a-password"></a>G. Erstellen eine SQL Server-authentifizierungsanmeldung mit einem Kennwort  
 Im folgenden Beispiel wird die Anmeldung `Mary7` mit Kennwort `A2c3456`.  
  
```tsql  
CREATE LOGIN Mary7 WITH PASSWORD = 'A2c3456$#' ;  
```  
  
### <a name="h-using-options"></a>H. Mithilfe der Optionen  
 Im folgenden Beispiel wird die Anmeldung `Mary8` mit Kennwort und einige der optionalen Argumente.  
  
```  
CREATE LOGIN Mary8 WITH PASSWORD = 'A2c3456$#' MUST_CHANGE,  
CHECK_EXPIRATION = ON,  
CHECK_POLICY = ON;  
```  
  
### <a name="i-creating-a-login-from-a-windows-domain-account"></a>I. Erstellen eines Anmeldenamens von einem Windows-Domänenkonto  
 Das folgende Beispiel erstellt eine Anmeldung von einem Windows-Domänenkonto mit dem Namen `Mary` in die `Contoso` Domäne.  
  
```  
CREATE LOGIN [Contoso\Mary] FROM WINDOWS;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Erste Schritte mit Berechtigungen für das Datenbankmodul](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)   
 [Prinzipale &#40;Datenbankmodul&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Kennwortrichtlinie](../../relational-databases/security/password-policy.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [DROP LOGIN &#40; Transact-SQL &#41;](../../t-sql/statements/drop-login-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [Erstellen eines Anmeldenamens](../../relational-databases/security/authentication-access/create-a-login.md)  
  
  


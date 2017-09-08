---
title: ALTER LOGIN (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/01/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_LOGIN_TSQL
- ALTER LOGIN
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER LOGIN statement
- change password
- mapping logins [SQL Server]
- logins [SQL Server], modifying
- passwords [SQL Server], modifying
- names [SQL Server], logins
- modifying login accounts
ms.assetid: e247b84e-c99e-4af8-8b50-57586e1cb1c5
caps.latest.revision: 68
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9dd47cb63c56dbbfb5f31ea3f7b2c8d4f45e9d73
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="alter-login-transact-sql"></a>ALTER LOGIN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Ändert die Eigenschaften eines [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldekontos.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server  
  
ALTER LOGIN login_name   
    {   
    <status_option>   
    | WITH <set_option> [ ,... ]  
    | <cryptographic_credential_option>  
    }   
[;]  
  
<status_option> ::=  
        ENABLE | DISABLE  
  
<set_option> ::=              
    PASSWORD = 'password' | hashed_password HASHED  
    [   
      OLD_PASSWORD = 'oldpassword'  
      | <password_option> [<password_option> ]   
    ]  
    | DEFAULT_DATABASE = database  
    | DEFAULT_LANGUAGE = language  
    | NAME = login_name  
    | CHECK_POLICY = { ON | OFF }  
    | CHECK_EXPIRATION = { ON | OFF }  
    | CREDENTIAL = credential_name  
    | NO CREDENTIAL  
  
<password_option> ::=   
    MUST_CHANGE | UNLOCK  
  
<cryptographic_credentials_option> ::=   
    ADD CREDENTIAL credential_name  
  | DROP CREDENTIAL credential_name  
```  
  
```  
-- Syntax for Azure SQL Database  
  
ALTER LOGIN login_name   
  {   
      <status_option>   
    | WITH <set_option> [ ,.. .n ]   
  }   
[;]  
  
<status_option> ::=  
    ENABLE | DISABLE  
  
<set_option> ::=   
    PASSWORD ='password'   
    [  
      OLD_PASSWORD ='oldpassword'  
    ]   
    | NAME = login_name  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
ALTER LOGIN login_name   
    {   
    <status_option>   
    | WITH <set_option> [ ,... ]  
    }   
  
<status_option> ::=ENABLE | DISABLE  
  
<set_option> ::=              
    PASSWORD ='password'   
    [   
      OLD_PASSWORD ='oldpassword'  
      | <password_option> [<password_option> ]   
    ]  
    | NAME = login_name  
    | CHECK_POLICY = { ON | OFF }  
    | CHECK_EXPIRATION = { ON | OFF }   
      
<password_option> ::=   
    MUST_CHANGE | UNLOCK  
```  
  
## <a name="arguments"></a>Argumente  
 *login_name*  
 Gibt den Namen der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldung an, die geändert wird. Domänenanmeldungen müssen in Klammern eingeschlossen werden: [Domäne\Benutzer].  
  
 ENABLE | DISABLE  
 Aktiviert oder deaktiviert diese Anmeldung. Das Deaktivieren einer Anmeldung wirkt sich nicht auf das Verhalten der bereits verbundenen Anmeldungen aus. (Verwenden der `KILL` Anweisung um eine vorhandene Verbindungen zu beenden.) Deaktivierte Anmeldungen behalten ihre Berechtigungen bei und sind weiterhin für den Identitätswechsel verfügbar.  
  
 Kennwort **= "***Kennwort***"**  
 Gilt nur für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldungen. Gibt das Kennwort für die Anmeldung an, die geändert wird. Bei Kennwörtern wird nach Groß- und Kleinschreibung unterschieden.  
  
 Aktive Verbindungen zur SQL-Datenbank erfordern fortlaufend erneute Autorisierung (die vom Datenbankmodul ausgeführt wird) mindestens alle 10 Stunden. Das Datenbankmodul versucht erneute Autorisierung mit dem ursprünglich gesendeten Kennwort, und keine Benutzereingaben erforderlich sind. Aus Gründen der Leistung beim Zurücksetzen eines Kennworts in SQL-Datenbank wird die Verbindung werden nicht erneut authentifiziert, auch wenn die Verbindung aufgrund von Verbindungspooling zurückgesetzt wird. Dies unterscheidet sich vom Verhalten von einer lokalen SQL Server. Wenn das Kennwort geändert wurde, da die Verbindung ursprünglich autorisiert wurde, muss die Verbindung beendet und eine neue Verbindung hergestellt werden mit dem neuen Kennwort. Ein Benutzer mit der KILL DATABASE CONNECTION-Berechtigung kann explizit eine Verbindung mit SQL-Datenbank mithilfe des KILL-Befehls beendet werden. Weitere Informationen finden Sie unter [KILL &#40; Transact-SQL &#41; ](../../t-sql/language-elements/kill-transact-sql.md).  
  
 Kennwort  **=**  *Hashed_password*  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gilt nur für das HASHED-Schlüsselwort. Gibt den Hashwert des Kennworts für den Anmeldenamen an, der erstellt wird.  
  
> [!IMPORTANT]  
>  Wenn für eine Anmeldung (oder den Benutzer einer eigenständigen Datenbank) eine Verbindung hergestellt und diese authentifiziert wird, werden von der Verbindung Identitätsinformationen zur Anmeldung zwischengespeichert. Bei einer Anmeldung unter Verwendung der Windows-Authentifizierung umfassen die Informationen Angaben zur Mitgliedschaft in Windows-Gruppen. Die Identität der Anmeldung bleibt für die Dauer der Verbindung authentifiziert. Um Identitätsänderungen zu erzwingen, z. B. das Zurücksetzen eines Kennworts oder eine Änderung der Windows-Gruppenmitgliedschaft, muss die Anmeldung von der Authentifizierungsstelle (Windows oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) abgemeldet und erneut angemeldet werden. Ein Mitglied der festen Serverrolle **sysadmin** oder eine beliebige Anmeldung mit der **ALTER ANY CONNECTION** -Berechtigung kann den **KILL** -Befehl verwenden, um eine Verbindung zu beenden und zu erzwingen, dass für eine Anmeldung eine erneute Verbindung hergestellt wird. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ist in der Lage, Verbindungsinformationen wiederzuverwenden, wenn mehrere Verbindungen mit dem Fenster Objekt-Explorer und Abfrage-Editor hergestellt werden. Schließen Sie alle Verbindungen, um eine erneute Verbindung zu erzwingen.  
  
 HASHED  
   
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gilt nur für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen. Gibt an, dass das nach dem PASSWORD-Argument eingegebene Kennwort bereits einen Hashwert darstellt. Wenn diese Option nicht ausgewählt wird, wird aus dem Kennwort vor dem Speichern in der Datenbank ein Hashwert erstellt. Diese Option sollte nur für die Anmeldungssynchronisierung zwischen zwei Servern verwendet werden. Verwenden Sie die HASHED-Option nicht, um Kennwörter routinemäßig zu ändern.  
  
 OLD_PASSWORD **= "***Oldpassword***"**  
 Gilt nur für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldungen. Das aktuelle Kennwort der Anmeldung, der ein neues Kennwort zugewiesen wird. Bei Kennwörtern wird nach Groß- und Kleinschreibung unterschieden.  
  
 MUST_CHANGE  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gilt nur für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldungen. Falls diese Option angegeben wird, fordert [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zur Eingabe eines aktualisierten Kennworts auf, wenn die geänderte Anmeldung zum ersten Mal verwendet wird.  
  
 DEFAULT_DATABASE  **=**  *Datenbank*  
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt eine Standarddatenbank an, die der Anmeldung zugewiesen werden soll.  
  
 DEFAULT_LANGUAGE  **=**  *Sprache*  
 
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt eine Standardsprache an, die der Anmeldung zugewiesen werden soll. Die Standardsprache für alle SQL-Datenbank-Anmeldenamen steht für Englisch und kann nicht geändert werden. Die Standardsprache der `sa` Anmeldung auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unter Linux steht für Englisch, jedoch geändert werden kann.  
  
 NAME = *Login_name*  
 Der neue Name der Anmeldung, die umbenannt wird. Falls es sich dabei um eine Windows-Anmeldung handelt, muss die SID des entsprechenden Windows-Prinzipals für den neuen Namen mit der SID übereinstimmen, die der Anmeldung in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zugeordnet ist. Der neue Name des eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldung kann keinen umgekehrten Schrägstrich enthalten (\\).  
  
 CHECK_EXPIRATION = {ON | **OFF** }  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gilt nur für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldungen. Gibt an, ob die Richtlinie für das Ablaufen von Kennwörtern für diesen Anmeldenamen erzwungen werden soll. Der Standardwert ist OFF.  
  
 CHECK_POLICY  **=**  { **ON** | {OFF}  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gilt nur für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldungen. Gibt an, dass die Windows-Kennwortrichtlinien des Computers, auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird, für diesen Anmeldenamen erzwungen werden sollen. Der Standardwert ist ON.  
  
 Anmeldeinformationen = *Credential_name*  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Die Anmeldeinformationen, die einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldung zugeordnet werden sollen. Die Anmeldeinformationen müssen bereits auf dem Server vorhanden sein. Weitere Informationen finden Sie unter [Anmeldeinformationen &#40; Datenbankmodul &#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md). Anmeldeinformationen kann nicht für die sa-Anmeldung zugeordnet werden.  
  
 NO CREDENTIAL  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Entfernt vorhandene Zuordnungen der Anmeldung zu Serveranmeldeinformationen. Weitere Informationen finden Sie unter [Anmeldeinformationen &#40; Datenbankmodul &#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md).  
  
 UNLOCK  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gilt nur für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldungen. Gibt an, dass die Sperre einer Anmeldung aufgehoben wird.  
  
 ADD CREDENTIAL  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Fügt der Anmeldung Anmeldeinformationen eines EKM-Anbieters (Extensible Key Management, erweiterbare Schlüsselverwaltung) hinzu. Weitere Informationen finden Sie unter [erweiterbare Schlüsselverwaltung &#40; Erweiterbare Schlüsselverwaltung &#41; ](../../relational-databases/security/encryption/extensible-key-management-ekm.md).  
  
 DROP CREDENTIAL  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
Entfernt die Anmeldeinformationen eines Extensible Key Management (EKM)-Anbieters von der Anmeldung. Weitere Informationen finden Sie unter [erweiterbare Schlüsselverwaltung &#40; Erweiterbare Schlüsselverwaltung &#41; ](../../relational-databases/security/encryption/extensible-key-management-ekm.md).  
  
## <a name="remarks"></a>Hinweise  
 Wenn CHECK_POLICY auf ON festgelegt ist, kann das HASHED-Argument nicht verwendet werden.  
  
 Wenn CHECK_POLICY in ON geändert wird, passiert Folgendes:  
  
-   Der Kennwortverlauf wird mit dem Wert des aktuellen Kennworthashes initialisiert.  
  
 Wenn CHECK_POLICY in OFF geändert wird, passiert Folgendes:  
  
-   CHECK_EXPIRATION wird ebenfalls auf OFF festgelegt.  
  
-   Der Kennwortverlauf wird gelöscht.  
  
-   Der Wert der *Lockout_time* wird zurückgesetzt.  
  
Falls MUST_CHANGE angegeben wird, müssen CHECK_EXPIRATION und CHECK_POLICY auf ON festgelegt werden. Andernfalls erzeugt die Anweisung einen Fehler.  
  
Falls CHECK_POLICY auf OFF festgelegt ist, kann CHECK_EXPIRATION nicht auf ON festgelegt werden. Eine ALTER LOGIN-Anweisung mit dieser Kombination von Optionen erzeugt einen Fehler.  
  
Sie können ALTER_LOGIN mit dem DISABLE-Argument nicht dazu verwenden, den Zugriff auf eine Windows-Gruppe zu verweigern. Beispielsweise ALTER_LOGIN [*Domain\group*] DISABLE Gibt die folgende Fehlermeldung zurück:  
  
 "Meldung 15151, Ebene 16, Status 1, Zeile 1"  
  
 "Die Anmeldung kann nicht geändert werden"*Domain\Group*", da er nicht vorhanden, oder Sie keine Berechtigung haben."  
  
 Dies ist beabsichtigt.  
  
In [!INCLUDE[ssSDS](../../includes/sssds-md.md)], Anmeldedaten erforderlich, um eine Verbindung zu authentifizieren und Firewallregeln auf Serverebene werden in jeder Datenbank vorübergehend zwischengespeichert. Dieser Cache wird in regelmäßigen Abständen aktualisiert. Führen Sie zum Erzwingen einer Aktualisierung des Authentifizierungscache und stellen Sie sicher, dass eine Datenbank die aktuelle Version der Tabelle Anmeldungen verfügt, [DBCC FLUSHAUTHCACHE &#40; Transact-SQL &#41; ](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die ALTER ANY LOGIN-Berechtigung.  
  
 Falls die CREDENTIAL-Option verwendet wird, ist auch die ALTER ANY CREDENTIAL-Berechtigung erforderlich.  
  
 Wenn der Anmeldename, der geändert wird, ein Mitglied ist die **Sysadmin** feste Serverrolle oder Empfänger der CONTROL SERVER-Berechtigung erfordert CONTROL SERVER-Berechtigung auch wenn Sie die folgenden Änderungen vornehmen:  
  
-   Zurücksetzen des Kennworts ohne Eingabe des alten Kennworts.  
  
-   Aktivieren von MUST_CHANGE, CHECK_POLICY oder CHECK_EXPIRATION.  
  
-   Ändern des Anmeldenamens.  
  
-   Aktivieren oder Deaktivieren der Anmeldung.  
  
-   Zuordnen der Anmeldung zu anderen Anmeldeinformationen.  
  
 Ein Prinzipal kann das Kennwort, die Standardsprache und die Standarddatenbank für seine eigene Anmeldung ändern.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-enabling-a-disabled-login"></a>A. Aktivieren einer deaktivierten Anmeldung  
 Im folgenden Beispiel wird die Anmeldung `Mary5` aktiviert.  
  
```tsql  
ALTER LOGIN Mary5 ENABLE;  
```  
  
### <a name="b-changing-the-password-of-a-login"></a>B. Ändern des Kennworts einer Anmeldung  
 Im folgenden Beispiel wird das Kennwort der Anmeldung `Mary5` in ein sicheres Kennwort geändert.  
  
```tsql  
ALTER LOGIN Mary5 WITH PASSWORD = '<enterStrongPasswordHere>';  
```  
  
### <a name="c-changing-the-name-of-a-login"></a>C. Ändern des Namens einer Anmeldung  
 Im folgenden Beispiel wird der Name der Anmeldung `Mary5` in `John2` geändert.  
  
```tsql  
ALTER LOGIN Mary5 WITH NAME = John2;  
```  
  
### <a name="d-mapping-a-login-to-a-credential"></a>D. Zuordnen einer Anmeldung zu Anmeldeinformationen  
 Im folgenden Beispiel wird die Anmeldung `John2` den Anmeldeinformationen `Custodian04` zugeordnet.  
  
```tsql  
ALTER LOGIN John2 WITH CREDENTIAL = Custodian04;  
```  
  
### <a name="e-mapping-a-login-to-an-extensible-key-management-credential"></a>E. Zuordnen einer Anmeldung zu Anmeldeinformationen der erweiterbaren Schlüsselverwaltung  
 Im folgenden Beispiel wird die Anmeldung `Mary5` den EKM-Anmeldeinformationen `EKMProvider1` zugeordnet.  
  
 
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```tsql  
ALTER LOGIN Mary5  
ADD CREDENTIAL EKMProvider1;  
GO  
```  
  
### <a name="f-unlocking-a-login"></a>F. Entsperren einer Anmeldung  
 Um eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldung zu entsperren, führen Sie die folgende Anweisung aus und ersetzen **** durch das gewünschte Kontokennwort.  
  
  
```tsql  
ALTER LOGIN [Mary5] WITH PASSWORD = '****' UNLOCK ;  

GO  
```  
  
 Um eine Anmeldung zu entsperren, ohne das Kennwort zu ändern, deaktivieren Sie die Überprüfungsrichtlinie, und aktivieren Sie diese dann erneut.  
  
```tsql  
ALTER LOGIN [Mary5] WITH CHECK_POLICY = OFF;  
ALTER LOGIN [Mary5] WITH CHECK_POLICY = ON;  
GO  
```  
  
### <a name="g-changing-the-password-of-a-login-using-hashed"></a>G. Ändern des Kennworts für eine Anmeldung mit HASHED  
 Im folgenden Beispiel wird das Kennwort für die `TestUser`-Anmeldung in einen bereits vorhandenen Hashwert geändert.  
  
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```tsql  
ALTER LOGIN TestUser WITH   
PASSWORD = 0x01000CF35567C60BFB41EBDE4CF700A985A13D773D6B45B90900 HASHED ;  
GO  
```  
  
 
  
## <a name="see-also"></a>Siehe auch  
 [Anmeldeinformationen &#40; Datenbankmodul &#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [DROP LOGIN &#40; Transact-SQL &#41;](../../t-sql/statements/drop-login-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [Erweiterbare Schlüsselverwaltung &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)  
  
  




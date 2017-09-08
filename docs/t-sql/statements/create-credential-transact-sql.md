---
title: Erstellen von Anmeldeinformationen (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 01/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREDENTIAL_TSQL
- SQL13.SWB.CREDENTIAL.GENERAL.F1
- CREATE CREDENTIAL
- CREATE_CREDENTIAL_TSQL
- CREDENTIAL
dev_langs:
- TSQL
helpviewer_keywords:
- SECRET clause
- authentication [SQL Server], credentials
- CREATE CREDENTIAL statement
- credentials [SQL Server], CREATE CREDENTIAL statement
ms.assetid: d5e9ae69-41d9-4e46-b13d-404b88a32d9d
caps.latest.revision: 51
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 556fa0262696075d63ee549730f2d9824c482dd4
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="create-credential-transact-sql"></a>CREATE CREDENTIAL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Anmeldeinformationen auf Serverebene erstellt. Anmeldeinformationen sind ein Datensatz, der die Authentifizierungsinformationen enthalten, die für die Verbindung zu einer Ressource außerhalb von SQL Server erforderlich ist. Die meisten Anmeldeinformationen schließen einen Windows-Benutzer und ein Kennwort ein. Speichern eine datenbanksicherung an einem Ort erfordert z. B. möglicherweise SQL-Server für die spezielle Anmeldeinformationen für den Zugriff auf diesen Speicherort. Weitere Informationen finden Sie unter [Anmeldeinformationen (Datenbankmodul)](../../relational-databases/security/authentication-access/credentials-database-engine.md).
  
> [!NOTE]  
>  Die Anmeldeinformationen auf der Datenbankebene verwenden vornehmen [CREATE DATABASE SCOPED CREDENTIAL &#40; Transact-SQL &#41; ](../../t-sql/statements/create-database-scoped-credential-transact-sql.md). Verwenden Sie Anmeldeinformationen auf Serverebene, wenn Sie die gleiche Anmeldeinformationen für mehrere Datenbanken auf dem Server verwenden müssen. Verwenden Sie datenbankbezogenen Anmeldeinformationen, um die Datenbank besser portierbar machen. Wenn eine Datenbank auf einen neuen Server verschoben wird, wird die datenbankbezogenen Anmeldeinformationen mit verschoben. Verwendung datenbankweit gültige Anmeldeinformationen auf [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
CREATE CREDENTIAL credential_name   
WITH IDENTITY = 'identity_name'  
    [ , SECRET = 'secret' ]  
        [ FOR CRYPTOGRAPHIC PROVIDER cryptographic_provider_name ]  
```  
  
## <a name="arguments"></a>Argumente  
 *credential_name*  
 Gibt den Namen für die zu erstellenden Anmeldeinformationen an. *Credential_name* darf nicht mit dem Nummernzeichen (#) beginnen. Systemanmeldeinformationen beginnen mit zwei Nummernzeichen (##).  Wenn Sie eine shared Access Signature (SAS) zu verwenden, muss dieser Name dem Containerpfad übereinstimmen mit Https beginnen und darf keinen Schrägstrich. Siehe Beispiel D weiter unten.  
  
 Identität **= "***Identity_name***"**  
 Gibt den Namen des Kontos an, das beim Herstellen einer Verbindung außerhalb des Servers verwendet wird. Wenn die Anmeldeinformationen verwendet wird, um Zugriff auf den Azure-Schlüsseltresor die **Identität** ist der Name des schlüsseltresors. Weitere Informationen finden Sie unten im Beispiel C. Wenn die Anmeldeinformationen eine shared Access Signature (SAS), verwendet der **Identität** ist *SHARED ACCESS SIGNATURE*. Siehe Beispiel D weiter unten.  
  
 Geheime Schlüssel **= "***geheimen***"**  
 Gibt den geheimen Bereich an, der für die ausgehende Authentifizierung erforderlich ist.  
  
 Wenn die Anmeldeinformationen zum Zugriff auf den Azure-Schlüsseltresor verwendet wird die **GEHEIMEN** Argument **CREATE CREDENTIAL** erfordert die  *\<Client-ID >* (ohne Bindestriche) und  *\<geheime Schlüssel >* von einem **Dienstprinzipal** in Azure Active Directory zusammen ohne Leerzeichen dazwischen übergeben werden. Weitere Informationen finden Sie unten im Beispiel C. Wenn die Anmeldeinformationen eine SAS verwendet die **GEHEIMEN** wird die SAS-Token. Siehe Beispiel D weiter unten.  Informationen zum Erstellen einer gespeicherten Zugriffsrichtlinie und eine shared Access Signature auf ein Azure-Container, finden Sie unter [Lektion 1: Erstellen einer gespeicherten Zugriffsrichtlinie und eine shared Access Signature für ein Azure-Container](../../relational-databases/lesson-1-create-stored-access-policy-and-shared-access-signature.md).  
  
 FOR CRYPTOGRAPHIC PROVIDER *Cryptographic_provider_name*  
 Gibt den Namen des ein *Enterprise Key Management Provider (EKM)*. Weitere Informationen zur Schlüsselverwaltung finden Sie unter [erweiterbare Schlüsselverwaltung &#40; Erweiterbare Schlüsselverwaltung &#41; ](../../relational-databases/security/encryption/extensible-key-management-ekm.md).  
  
## <a name="remarks"></a>Hinweise  

 Falls für IDENTITY ein Windows-Benutzer angegeben ist, kann der geheime Bereich das Kennwort enthalten. Der geheime Bereich wird mithilfe des Diensthauptschlüssels verschlüsselt. Falls der Diensthauptschlüssel neu generiert wird, wird der geheime Bereich mithilfe des neuen Diensthauptschlüssels neu verschlüsselt.  
  
 Nach dem Erstellen von Anmeldeinformationen, ordnen Sie ihn einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldung mit [CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md) oder [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md). Ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldung kann nur einer Anmeldeinformation zugeordnet werden, aber eine einzelne Anmeldung zugeordnet werden kann, um mehrere [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldungen. Weitere Informationen finden Sie unter [Anmeldeinformationen &#40; Datenbankmodul &#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md). Anmeldeinformationen auf Serverebene kann nur zu einem Anmeldenamen nicht zu einem Datenbankbenutzer zugeordnet werden. 
  
 Informationen zu Anmeldeinformationen werden in der [sys.credentials](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md) -Katalogsicht angezeigt.  
  
 Falls für den Anbieter kein mit einem Anmeldenamen verknüpfter Identitätsnachweis vorliegt, werden die dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienstkonto zugeordneten Anmeldeinformationen verwendet.  
  
 Einem Anmeldenamen können mehrere Anmeldeinformationen zugeordnet werden, solange sie für unterschiedliche Anbieter verwendet werden. Pro Anbieter und Anmeldung darf es jedoch nur einen zugeordneten Identitätsnachweis geben. Die gleichen Anmeldeinformationen können jedoch auch anderen Anmeldenamen zugeordnet werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert **ALTER ANY CREDENTIAL** Berechtigung.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-basic-example"></a>A. Elementares Beispiel  
 Im folgenden Beispiel werden die Anmeldeinformationen namens `AlterEgo` erstellt. Die Anmeldeinformationen enthalten den Windows-Benutzer `Mary5` und ein Kennwort.  
  
```  
CREATE CREDENTIAL AlterEgo WITH IDENTITY = 'Mary5',   
    SECRET = '<EnterStrongPasswordHere>';  
GO  
```  
  
### <a name="b-creating-a-credential-for-ekm"></a>B. Erstellen von Anmeldeinformationen für EKM  
 Im folgenden Beispiel wird ein zuvor erstelltes Konto namens `User1OnEKM` auf einem EKM-Modul mithilfe der EKM-Verwaltungstools mit einem Standardkontotyp und Kennwort verwendet. Die **Sysadmin** Konto auf dem Server erstellt Anmeldeinformationen, die zur Verbindung mit des EKM-Kontos verwendet wird, und weist sie der `User1` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Konto:  
  
```  
CREATE CREDENTIAL CredentialForEKM  
    WITH IDENTITY='User1OnEKM', SECRET='<EnterStrongPasswordHere>'  
    FOR CRYPTOGRAPHIC PROVIDER MyEKMProvider;  
GO  
  
/* Modify the login to assign the cryptographic provider credential */  
ALTER LOGIN Login1  
ADD CREDENTIAL CredentialForEKM;  
  
/* Modify the login to assign a non cryptographic provider credential */   
ALTER LOGIN Login1  
WITH CREDENTIAL = AlterEgo;  
GO  
```  
  
### <a name="c-creating-a-credential-for-ekm-using-the-azure-key-vault"></a>C. Erstellen von Anmeldeinformationen für EKM unter Verwendung des Azure-Schlüsseltresors  
 Das folgende Beispiel erstellt eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldeinformationen für die [!INCLUDE[ssDE](../../includes/ssde-md.md)] verwendet beim Zugriff auf den Azure Key Vault mithilfe der **SQL Server-Connector für Microsoft Azure Key Vault**. Ein vollständiges Beispiel der Verwendung der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Connector finden Sie unter [erweiterbare Schlüsselverwaltung mithilfe von Azure Key Vault &#40; SQLServer &#41; ](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md).  
  
> [!IMPORTANT]  
>  Das **IDENTITY** -Argument von **CREATE CREDENTIAL** erfordert den Schlüsseltresornamen. Die **GEHEIMEN** Argument **CREATE CREDENTIAL** erfordert die  *\<Client-ID >* (ohne Bindestriche) und  *\<geheime Schlüssel >*  zusammen ohne Leerzeichen dazwischen übergeben werden.  
  
 Im folgenden Beispiel wird die **Client-ID** (`EF5C8E09-4D2A-4A76-9998-D93440D8115D`) von den Bindestrichen bereinigt und als Zeichenfolge `EF5C8E094D2A4A769998D93440D8115D` eingegeben. Der **geheime Schlüssel** wird durch die Zeichenfolge *SECRET_DBEngine*dargestellt.  
  
```  
USE master;  
CREATE CREDENTIAL Azure_EKM_TDE_cred   
    WITH IDENTITY = 'ContosoKeyVault',   
    SECRET = 'EF5C8E094D2A4A769998D93440D8115DSECRET_DBEngine'   
    FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov ;  
```  
  
 Das folgende Beispiel erstellt die gleiche Anmeldeinformationen unter Verwendung von Variablen für die **Clientkennung** und **geheimen** Zeichenfolgen, die Formular dann verkettet werden die **GEHEIMEN** Argument. Die **ersetzen** Funktion dient zum Entfernen der Bindestriche aus der Client-ID  
  
```  
DECLARE @AuthClientId uniqueidentifier = 'EF5C8E09-4D2A-4A76-9998-D93440D8115D';  
DECLARE @AuthClientSecret varchar(200) = 'SECRET_DBEngine';  
DECLARE @pwd varchar(max) = REPLACE(CONVERT(varchar(36), @AuthClientId) , '-', '') + @AuthClientSecret;  
  
EXEC ('CREATE CREDENTIAL Azure_EKM_TDE_cred   
    WITH IDENTITY = 'ContosoKeyVault', SECRET = ''' + @PWD + '''   
    FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov ;');  
```  
  
### <a name="d-creating-a-credential-using-a-sas-token"></a>D. Erstellen von Anmeldeinformationen mithilfe von SAS-Token  
 **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] über [aktuelle Version](http://go.microsoft.com/fwlink/p/?LinkId=299658).  
  
 Das folgende Beispiel erstellt eine SAS Signatur-Anmeldeinformationen mit einem SAS-Token.  Ein Lernprogramm zum Erstellen einer gespeicherten Zugriffsrichtlinie und eine shared Access Signature auf ein Azure-Container und erstellen dann mithilfe der SAS-Anmeldeinformationen, finden Sie unter [Lernprogramm: SQL Server 2016 mit Microsoft Azure Blob-Speicherdienst Datenbanken](Tutorial:%20Using%20the%20Microsoft%20Azure%20Blob%20storage%20service%20with%20SQL%20Server%202016%20databases.md).  
  
> [!IMPORTANT]  
>  DIE **ANMELDEINFORMATIONSNAME** Argument erfordert, dass der Name dem Containerpfad übereinstimmen, mit Https beginnen und enthält keinen nachgestellten Schrägstrich. Die **Identität** Argument erfordert den Namen *SHARED ACCESS SIGNATURE*. Die **GEHEIMEN** Argument erfordert das SAS-Token.  
  
```  
USE master  
CREATE CREDENTIAL [https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>] -- this name must match the container path, start with https and must not contain a trailing forward slash.  
   WITH IDENTITY='SHARED ACCESS SIGNATURE' -- this is a mandatory string and do not change it.   
   , SECRET = 'sharedaccesssignature' –- this is the shared access signature token   
GO    
```  
  
## <a name="see-also"></a>Siehe auch  
 [Anmeldeinformationen &#40; Datenbankmodul &#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [ALTER CREDENTIAL &#40; Transact-SQL &#41;](../../t-sql/statements/alter-credential-transact-sql.md)   
 [DROP CREDENTIAL &#40; Transact-SQL &#41;](../../t-sql/statements/drop-credential-transact-sql.md)   
 [Erstellen Sie die Datenbank ausgelegte CREDENTIAL &#40; Transact-SQL &#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)   
 [Lektion 2: Erstellen einer SQL Server-Anmeldeinformationen, die mit einer SAS](../../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)   
 [SAS](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)  
  
  


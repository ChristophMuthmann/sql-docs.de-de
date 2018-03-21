---
title: CREATE CREDENTIAL (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/09/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 200adf6302cb0c86f487a7480579a173403ed14c
ms.sourcegitcommit: 3ed9be04cc7fb9ab1a9ec230c298ad2932acc71b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/17/2018
---
# <a name="create-credential-transact-sql"></a>CREATE CREDENTIAL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Erstellt Anmeldeinformationen auf Serverebene. Anmeldeinformationen sind in einem Datensatz gespeichert, in dem die Authentifizierungsinformationen enthalten sind, die zum Herstellen einer Verbindung mit einer Ressource außerhalb von SQL Server erforderlich sind. Die meisten Anmeldeinformationen schließen einen Windows-Benutzer und ein Kennwort ein. Wenn Sie z.B. eine Datensicherung an einem beliebigen Speicherort speichern, erfordert SQL Server möglicherweise die Eingabe von besonderen Anmeldeinformationen, damit auf diesen Speicherort zugegriffen werden kann. Weitere Informationen finden Sie unter [Anmeldeinformationen (Datenbank-Engine)](../../relational-databases/security/authentication-access/credentials-database-engine.md).

[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)]

> [!NOTE]  
>  Verwenden Sie [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md) zum Erstellen der Anmeldeinformationen auf Datenbankebene. Verwenden Sie Anmeldeinformationen auf Serverebene, wenn Sie dieselben Anmeldeinformationen für mehrere Datenbanken auf demselben Server verwenden müssen. Verwenden Sie datenbankbezogene Anmeldeinformationen, um die Datenbank portierbarer zu machen. Wenn eine Datenbank auf einen neuen Server verschoben wird, werden gleichzeitig auch diese datenbankbezogenen Anmeldeinformationen verschoben. Verwenden Sie datenbankbezogene Anmeldeinformationen in [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
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
 Gibt den Namen für die zu erstellenden Anmeldeinformationen an. *credential_name* darf nicht mit dem Nummernzeichen (#) beginnen. Systemanmeldeinformationen beginnen mit zwei Nummernzeichen (##).  Wenn eine Shared Access Signature (SAS) verwendet wird, muss dieser Name dem Containerpfad zugeordnet werden können, mit „https“ beginnen und einen Schrägstrich enthalten. Siehe Beispiel D.  
  
 IDENTITY **='***identity_name***'**  
 Gibt den Namen des Kontos an, das beim Herstellen einer Verbindung außerhalb des Servers verwendet wird. Wenn die Anmeldeinformationen zum Zugreifen auf Azure Key Vault verwendet werden, ist **IDENTITY** der Name des Schlüsseltresors. Weitere Informationen finden Sie unten im Beispiel C. Wenn die Anmeldeinformationen eine Shared Access Signature (SAS) verwenden, lautet **IDENTITY** *SHARED ACCESS SIGNATURE*. Siehe Beispiel D.  
  
 SECRET **='***secret***'**  
 Gibt den geheimen Bereich an, der für die ausgehende Authentifizierung erforderlich ist.  
  
 Wenn die Anmeldeinformationen zum Zugreifen auf Azure Key Vault verwendet werden, müssen an das **SECRET**-Argument von **CREATE CREDENTIAL** die *\<Client-ID>* (ohne Bindestriche) und der *\<geheime Schlüssel>* eines **Dienstprinzipals** in Azure Active Directory zusammen, ohne Leerzeichen dazwischen, übergeben werden. Weitere Informationen finden Sie unten im Beispiel C. Wenn die Anmeldeinformationen eine Shared Access Signature (SAS) verwenden, ist **SECRET** das freigegebene SAS-Token. Siehe Beispiel D.  Weitere Informationen zum Erstellen einer gespeicherten Zugriffsrichtlinie und einer SAS auf einem Azure-Container finden Sie unter [Lektion 1: Erstellen einer gespeicherten Zugriffsrichtlinie und SAS](../../relational-databases/lesson-1-create-stored-access-policy-and-shared-access-signature.md).  
  
 FOR CRYPTOGRAPHIC PROVIDER *cryptographic_provider_name*  
 Gibt den Namen eines *Anbieters für die Schlüsselverwaltung in Unternehmen* (Enterprise Key Management Provider (EKM)) an. Weitere Informationen zum Verwalten von Schlüsseln finden Sie unter [Erweiterbare Schlüsselverwaltung &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md).  
  
## <a name="remarks"></a>Remarks  

 Falls für IDENTITY ein Windows-Benutzer angegeben ist, kann der geheime Bereich das Kennwort enthalten. Der geheime Bereich wird mithilfe des Diensthauptschlüssels verschlüsselt. Falls der Diensthauptschlüssel neu generiert wird, wird der geheime Bereich mithilfe des neuen Diensthauptschlüssels neu verschlüsselt.  
  
 Nach der Erstellung von Anmeldeinformationen können Sie diese einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen zuordnen, indem Sie [CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md) oder [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md) verwenden. Ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldename kann nur einem Satz Anmeldeinformationen zugeordnet werden, ein Satz Anmeldeinformationen kann jedoch mehreren [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen zugeordnet sein. Weitere Informationen finden Sie unter [Anmeldeinformationen &#40;Datenbank-Engine&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md). Anmeldeinformationen auf Serverebene können nur einem Anmeldenamen und keinem Datenbankbenutzer zugeordnet werden. 
  
 Informationen zu Anmeldeinformationen werden in der [sys.credentials](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)-Katalogsicht angezeigt.  
  
 Falls für den Anbieter kein mit einem Anmeldenamen verknüpfter Identitätsnachweis vorliegt, werden die dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienstkonto zugeordneten Anmeldeinformationen verwendet.  
  
 Einem Anmeldenamen können mehrere Anmeldeinformationen zugeordnet werden, solange sie für unterschiedliche Anbieter verwendet werden. Pro Anbieter und Anmeldung darf es jedoch nur einen zugeordneten Identitätsnachweis geben. Die gleichen Anmeldeinformationen können jedoch auch anderen Anmeldenamen zugeordnet werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die **ALTER ANY CREDENTIAL**-Berechtigung.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-basic-example"></a>A. Elementares Beispiel  
 Im folgenden Beispiel werden die Anmeldeinformationen namens `AlterEgo` erstellt. Die Anmeldeinformationen enthalten den Windows-Benutzer `Mary5` und ein Kennwort.  
  
```  
CREATE CREDENTIAL AlterEgo WITH IDENTITY = 'Mary5',   
    SECRET = '<EnterStrongPasswordHere>';  
GO  
```  
  
### <a name="b-creating-a-credential-for-ekm"></a>B. Erstellen von Anmeldeinformationen für EKM  
 Im folgenden Beispiel wird ein zuvor erstelltes Konto namens `User1OnEKM` auf einem EKM-Modul mithilfe der EKM-Verwaltungstools mit einem Standardkontotyp und Kennwort verwendet. Das **sysadmin**-Konto auf dem Server erstellt die Anmeldeinformationen, mit denen die Verbindung mit dem EKM-Konto hergestellt wird, und weist diese dem `User1`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konto zu:  
  
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
 Im folgenden Beispiel werden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldeinformationen erstellt, die das [!INCLUDE[ssDE](../../includes/ssde-md.md)] beim Zugreifen auf Azure Key Vault mit dem **SQL Server-Connector für Microsoft Azure Key Vault** verwenden soll. Ein vollständiges Beispiel zur Verwendung des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Connectors finden Sie unter [Erweiterbare Schlüsselverwaltung mit Azure Key Vault &#40;SQL Server&#41;](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md).  
  
> [!IMPORTANT]  
>  Das **IDENTITY** -Argument von **CREATE CREDENTIAL** erfordert den Schlüsseltresornamen. An das **SECRET**-Argument von **CREATE CREDENTIAL** müssen die *\<Client-ID>* (ohne Bindestriche) und der *\<geheime Schlüssel>* zusammen, ohne Leerzeichen dazwischen, übergeben werden.  
  
 Im folgenden Beispiel wird die **Client-ID** (`EF5C8E09-4D2A-4A76-9998-D93440D8115D`) von den Bindestrichen bereinigt und als Zeichenfolge `EF5C8E094D2A4A769998D93440D8115D` eingegeben. Der **geheime Schlüssel** wird durch die Zeichenfolge *SECRET_DBEngine*dargestellt.  
  
```  
USE master;  
CREATE CREDENTIAL Azure_EKM_TDE_cred   
    WITH IDENTITY = 'ContosoKeyVault',   
    SECRET = 'EF5C8E094D2A4A769998D93440D8115DSECRET_DBEngine'   
    FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov ;  
```  
  
 Im folgenden Beispiel werden die gleichen Anmeldeinformationen unter Verwendung von Variablen für die Zeichenfolgen der **Client-ID** und des **geheimem Schlüssels** erstellt, die dann verkettet werden, um das **SECRET**-Argument zu bilden. Mit der **REPLACE**-Funktion werden die Bindestriche aus der Client-ID entfernt.  
  
```  
DECLARE @AuthClientId uniqueidentifier = 'EF5C8E09-4D2A-4A76-9998-D93440D8115D';  
DECLARE @AuthClientSecret varchar(200) = 'SECRET_DBEngine';  
DECLARE @pwd varchar(max) = REPLACE(CONVERT(varchar(36), @AuthClientId) , '-', '') + @AuthClientSecret;  
  
EXEC ('CREATE CREDENTIAL Azure_EKM_TDE_cred   
    WITH IDENTITY = 'ContosoKeyVault', SECRET = ''' + @PWD + '''   
    FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov ;');  
```  
  
### <a name="d-creating-a-credential-using-a-sas-token"></a>D. Erstellen von Anmeldeinformationen mithilfe eines SAS-Token  
 **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658).  
  
 Das folgende Beispiel erstellt SAS-Anmeldinformationen mit dem SAS-Token.  Ein Tutorial zum Erstellen einer gespeicherten Zugriffsrichtlinie und einer SAS für einen Azure-Container und das anschließende Erstellen von Anmeldeinformationen unter Verwendung dieser SAS finden Sie unter [Tutorial: Verwenden des Microsoft Azure BLOB-Speicherdiensts mit SQL Server 2016](Tutorial:%20Using%20the%20Microsoft%20Azure%20Blob%20storage%20service%20with%20SQL%20Server%202016%20databases.md).  
  
> [!IMPORTANT]  
>  Das **CREDENTIAL NAME**-Argument erfordert, dass der Name dem Containerpfad zugeordnet werden kann, mit „https“ beginnt und keinen nachgestellten Schrägstrich enthält. Das **IDENTITY**-Argument erfordert den Namen *SHARED ACCESS SIGNATURE*. Das **SECRET**-Argument erfordert das SAS-Token.  
  
```  
USE master  
CREATE CREDENTIAL [https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>] -- this name must match the container path, start with https and must not contain a trailing forward slash.  
   WITH IDENTITY='SHARED ACCESS SIGNATURE' -- this is a mandatory string and do not change it.   
   , SECRET = 'sharedaccesssignature' –- this is the shared access signature token   
GO    
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Anmeldeinformationen &#40;Datenbank-Engine&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [ALTER CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-credential-transact-sql.md)   
 [DROP CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-credential-transact-sql.md)   
 [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)   
 [Lektion 2: Erstellen von SQL Server-Anmeldeinformationen mit einer Shared Access Signature (SAS)](../../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)   
 [Shared Access Signatures](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)  
  
  

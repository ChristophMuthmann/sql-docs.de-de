---
title: CREATE COLUMN MASTER KEY (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 07/18/2016
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
f1_keywords:
- SQL13.SWB.NEWCOLUMNMASTERKEYDEF.GENERAL.F1
- SQL13.SWB.COLUMNMASTERKEYDEF.GENERAL.F1
- CREATE COLUMN MASTER KEY
- COLUMN MASTER KEY
- CREATE_COLUMN_MASTER_KEY_TSQL
- COLUMN_MASTER_KEY_TSQL
- SQL13.SWB.NEWCOLUMNMASTERKEY.GENERAL.F1
- SQL13.SWB.COLUMNMASTERKEY.GENERAL.F1
dev_langs:
- TSQL
helpviewer_keywords:
- column master key definition
- column master key, create
- CREATE COLUMN MASTER KEY statement
- Always Encrypted, create column master key
ms.assetid: f8926b95-e146-4e3f-b56b-add0c0d0a30e
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 30cf5c83de208992cb36692c0b4b7b07fabf5cb6
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="create-column-master-key-transact-sql"></a>CREATE COLUMN MASTER KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Erstellt ein Spaltenhauptschlüssel-Metadatenobjekt in einer Datenbank. Ein Metadateneintrag für einen Spaltenhauptschlüssel, der in einem externen Schlüsselspeicher gespeichert ist und zum Schützen (Verschlüsseln) von Spaltenverschlüsselungsschlüsseln verwendet wird, wenn Sie das Feature [Always Encrypted &#40;Datenbank-Engine&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md) verwenden. Durch mehrere Spaltenhauptschlüssel wird die Schlüsselrotation ermöglicht, und durch regelmäßiges Ändern des Schlüssels wird die Sicherheit erhöht. Sie können einen Spaltenhauptschlüssel in einem Schlüsselspeicher und das zugehörige Metadatenobjekt in der Datenbank erstellen, indem Sie den Objekt-Explorer in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder PowerShell verwenden. Weitere Informationen finden Sie unter [Overview of Key Management for Always Encrypted (Übersicht über die Schlüsselverwaltung für Always Encrypted)](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
CREATE COLUMN MASTER KEY key_name   
    WITH (  
        KEY_STORE_PROVIDER_NAME = 'key_store_provider_name',  
        KEY_PATH = 'key_path'   
         )   
[;]  
```  
  
## <a name="arguments"></a>Argumente  
 *key_name*  
 Der Name des Spaltenhauptschlüssels in der Datenbank.  
  
 *key_store_provider_name*  
 Gibt den Namen eines Schlüsselspeicheranbieters an, der eine clientseitige Softwarekomponente darstellt, die einen Schlüsselspeicher mit dem Spaltenhauptschlüssel beinhaltet. Ein für Always Encrypted aktivierter Clienttreiber verwendet den Namen eines Schlüsselspeicheranbieters, um nach einem Schlüsselspeicheranbieter in der Registrierung der Schlüsselspeicheranbieter des Treibers zu suchen. Der Treiber verwendet den Anbieter, um Spaltenverschlüsselungsschlüssel zu entschlüsseln, die von einem Spaltenhauptschlüssel geschützt und im zugrunde liegenden Schlüsselspeicher gespeichert sind. Anschließend wird ein Klartextwert des Spaltenverschlüsselungsschlüssels verwendet, um Abfrageparameter zu entschlüsseln, die verschlüsselten Datenbankspalten entsprechen, oder um Abfrageergebnisse aus verschlüsselten Spalten zu entschlüsseln.  
  
 Für Always Encrypted aktivierte Clienttreiberbibliotheken enthalten Schlüsselspeicheranbieter für beliebte Schlüsselspeicher.   
  
Die verfügbaren Anbieter hängen vom Typ und von der Version des Clienttreibers ab. Weitere Informationen zu bestimmten Treibern finden Sie in der Always Encrypted-Dokumentation:

[Entwickeln von Anwendungen unter Verwendung von Always Encrypted mit dem .NET Framework-Anbieter für SQL Server](../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)


In folgender Tabelle werden die Namen der Systemanbieter erfasst:  
  
|Name des Schlüsselspeicheranbieters|Zugrunde liegender Schlüsselspeicher|  
    |-----------------------------|--------------------------|
    |'MSSQL_CERTIFICATE_STORE'|Windows-Zertifikatspeicher| 
    |'MSSQL_CSP_PROVIDER'|Ein Speicher, z.B. ein Hardwaresicherheitsmodul (HSM), der Microsoft CryptoAPI unterstützt.|
    |'MSSQL_CNG_STORE'|Ein Speicher, z.B. ein Hardwaresicherheitsmodul (HSM), der Cryptography API: Next Generation unterstützt.|  
    |'Azure_Key_Vault'|Weitere Informationen finden Sie unter [Erste Schritte mit Azure Key Vault](https://azure.microsoft.com/documentation/articles/key-vault-get-started/).|  
  

 Sie können einen benutzerdefinierten Schlüsselspeicheranbieter implementieren, um Spaltenhauptschlüssel in einem Speicher zu speichern, für den keine integrierten Schlüsselspeicheranbieter in Ihrem für Always Encrypted aktivierten Clienttreiber vorhanden sind.  Beachten Sie, dass die Namen der benutzerdefinierten Schlüsselspeicheranbieter nicht mit „MSSQL_“ beginnen dürfen. Dieses Präfix ist für [!INCLUDE[msCoName](../../includes/msconame-md.md)]-Schlüsselspeicheranbieter reserviert. 

  
 key_path  
 Der Pfad des Schlüssels im Speicher des Spaltenhauptschlüssels. Der Schlüsselpfad muss im Kontext jeder Clientanwendung gültig sein, die Daten verschlüsseln oder entschlüsseln soll, die in einer Spalte gespeichert sind, die (indirekt) vom Spaltenhauptschlüssel geschützt wird, auf den verwiesen wird. Zudem muss der Clientanwendung gewährt werden, auf den Schlüssel zuzugreifen. Das Format des Schlüsselpfads hängt vom Schlüsselspeicheranbieter ab. In der folgenden Liste werden die Formate der Schlüsselpfade für bestimmte System-Schlüsselspeicheranbieter von Microsoft beschrieben:  
  
-   **Anbietername:** MSSQL_CERTIFICATE_STORE  
  
     **Format des Schlüsselpfads:** *CertificateStoreName*/*CertificateStoreLocation*/*CertificateThumbprint*  
  
     Erläuterungen:  
  
     *CertificateStoreLocation*  
     Der Zertifikatspeicherort, der dem aktuellen Benutzer oder dem lokalen Computer entsprechen muss. Weitere Informationen finden Sie unter [Local Machine and Current User Certificate Stores (Zertifikatspeicher des lokalen Computers bzw. des aktuellen Benutzers)](https://msdn.microsoft.com/library/windows/hardware/ff548653.aspx).  
  
     *CertificateStore*  
     Der Name des Zertifikatspeichers, z.B. „My“.  
  
     *CertificateThumbprint*  
     Zertifikatfingerabdruck.  
  
     **Beispiele:**  
  
    ```  
    N'CurrentUser/My/BBF037EC4A133ADCA89FFAEC16CA5BFA8878FB94'  
  
    N'LocalMachine/My/CA5BFA8878FB94BBF037EC4A133ADCA89FFAEC16'  
    ```  
  
-   **Anbietername:** MSSQL_CSP_PROVIDER  
  
     **Format des Schlüsselpfads:** *ProviderName*/*KeyIdentifier*  
  
     Erläuterungen:  
  
     *ProviderName*  
     Der Name des Kryptografiedienstanbieters (Cryptography Service Provider, CSP), der CAPI implementiert, für den Speicher des Spaltenhauptschlüssels. Wenn Sie ein HSM als Schlüsselspeicher verwenden, muss dieser dem Namen des CSP entsprechen, den Ihr HSM-Anbieter bereitstellt. Der Anbieter muss auf einem Clientcomputer installiert sein.  
  
     *KeyIdentifier*  
     Der Bezeichner des Schlüssels im Schlüsselspeicher, der als Spaltenhauptschlüssel verwendet wird.  
  
     **Beispiele:**  
  
    ```  
    N'My HSM CSP Provider/AlwaysEncryptedKey1'  
    ```  
  
-   **Anbietername:** MSSQL_CNG_STORE  
  
     **Format des Schlüsselpfads:** *ProviderName*/*KeyIdentifier*  
  
     Erläuterungen:  
  
     *ProviderName*  
     Der Name des Schlüsselspeicheranbieters (Key Storage Provider, KSP), der die CNG-API (Cryptography: Next Generation) implementiert, für den Speicher des Spaltenhauptschlüssels. Wenn Sie ein HSM als Schlüsselspeicher verwenden, muss dieser dem Namen des KSP entsprechen, den Ihr HSM-Anbieter bereitstellt. Der Anbieter muss auf einem Clientcomputer installiert sein.  
  
     *KeyIdentifier*  
     Der Bezeichner des Schlüssels im Schlüsselspeicher, der als Spaltenhauptschlüssel verwendet wird.  
  
     **Beispiele:**  
  
    ```  
    N'My HSM CNG Provider/AlwaysEncryptedKey1'  
    ```  

-   **Anbietername:** AZURE_KEY_STORE  
  
     **Format des Schlüsselpfads:** *KeyUrl*  
  
     Erläuterungen:  
  
     *KeyUrl*  
     Die URL des Schlüssels in Azure Key Vault


Beispiel:
 
`N'https://myvault.vault.azure.net:443/keys/MyCMK/4c05f1a41b12488f9cba2ea964b6a700'`  
  
## <a name="remarks"></a>Remarks  

Das Erstellen eines Metadateneintrags für einen Spaltenhauptschlüssel ist erforderlich, bevor ein Metadateneintrag für einen Spaltenverschlüsselungsschlüssel in der Datenbank erstellt werden kann, und bevor Spalten in der Datenbank mithilfe von Always Encrypted verschlüsselt werden können. Beachten Sie, dass ein Metadateneintrag für einen Spaltenhauptschlüssel nicht den tatsächlichen Spaltenhauptschlüssel enthält. Dieser muss in einem externen Spaltenschlüsselspeicher (außerhalb von SQL Server) gespeichert werden. Der Name des Schlüsselspeicheranbieters und der Pfad des Spaltenhauptschlüssels in den Metadaten müssen für eine Clientanwendung gültig sein, damit der Spaltenhauptschlüssel verwendet werden kann, um einen Spaltenverschlüsselungsschlüssel zu entschlüsseln, der mit dem Spaltenhauptschlüssel verschlüsselt ist, sowie zum Abfragen von verschlüsselten Spalten.


  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Berechtigung **ALTER ANY COLUMN MASTER KEY**.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-creating-a-column-master-key"></a>A. Erstellen eines Spaltenhauptschlüssels  
 Erstellen eines Metadateneintrags für einen Spaltenhauptschlüssels, der im Zertifikatspeicher gespeichert ist, für Clientanwendungen, die den Anbieter „MSSQL_CERTIFICATE_STORE“ verwenden, um auf den Spaltenhauptschlüssel zuzugreifen:  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
     KEY_STORE_PROVIDER_NAME = N'MSSQL_CERTIFICATE_STORE',   
     KEY_PATH = 'Current User/Personal/f2260f28d909d21c642a3d8e0b45a830e79a1420'  
   );  
```  
  
 Erstellen eines Metadateneintrags für einen Spaltenhauptschlüssel, auf den von Clientanwendungen zugegriffen wird, die den Anbieter „MSSQL_CNG_STORE“ verwenden:  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
    KEY_STORE_PROVIDER_NAME = N'MSSQL_CNG_STORE',    
    KEY_PATH = N'My HSM CNG Provider/AlwaysEncryptedKey'  
);  
```  
  
 Erstellen eines Spaltenhauptschlüssels, der in Azure Key Vault gespeichert wird, für Clientanwendungen, die den Anbieter „AZURE_KEY_VAULT“ verwenden, um auf den Spaltenhauptschlüssel zuzugreifen:  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
    KEY_STORE_PROVIDER_NAME = N'AZURE_KEY_VAULT',  
    KEY_PATH = N'https://myvault.vault.azure.net:443/keys/  
        MyCMK/4c05f1a41b12488f9cba2ea964b6a700');  
```  
  
 Erstellen eines Spaltenhauptschlüssels, der in einem benutzerdefinierten Speicher für Spaltenhauptschlüssel gespeichert ist:  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
    KEY_STORE_PROVIDER_NAME = 'CUSTOM_KEY_STORE',    
    KEY_PATH = 'https://contoso.vault/sales_db_tce_key'  
);  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter
 
* [DROP COLUMN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-column-master-key-transact-sql.md)   
* [CREATE COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-encryption-key-transact-sql.md)
* [sys.column_master_keys (Transact-SQL)](../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)
* [Always Encrypted &#40;Datenbankmodul&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)  
* [Overview of Key Management for Always Encrypted (Übersicht über die Schlüsselverwaltung für Always Encrypted)](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)
  

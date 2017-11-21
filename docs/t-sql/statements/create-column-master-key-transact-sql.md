---
title: Erstellen von COLUMN MASTER KEY (Transact-SQL) | Microsoft Docs
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
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 871acb46898a9a62b25062f69d4e51bf28658f06
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="create-column-master-key-transact-sql"></a>CREATE COLUMN MASTER KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Erstellt einen spaltenhauptschlüssel-Metadaten-Objekt in einer Datenbank an. Master Key-Spalte Metadateneintrag, der einen Schlüssel darstellt gespeichert, in einem externen Schlüsselspeicher, die verwendet wird, um zu schützen (verschlüsseln) Spalte Verschlüsselungsschlüssel bei Verwendung der [Always Encrypted &#40; Datenbankmodul &#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md) Funktion. Mehrere spaltenhauptschlüssel ermöglichen Schlüsselrotation; der Schlüssel zur Erhöhung der Sicherheit ändern in regelmäßigen Abständen. Sie können einen spaltenhauptschlüssel in einem Schlüsselspeicher und das zugehörige Metadatenobjekt in der Datenbank erstellen, indem Sie im Objekt-Explorer mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder PowerShell. Weitere Informationen finden Sie unter [Übersicht über die Schlüsselverwaltung für Always Encrypted](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md).  
  
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
 *Key_name*  
 Ist der Name, der durch den Hauptschlüssel der Spalte in der Datenbank bekannt ist.  
  
 *key_store_provider_name*  
 Gibt den Namen eines Anbieters Schlüsselspeicher, also eine clientseitige Softwarekomponente, die einen Schlüsselspeicher mit dem spaltenhauptschlüssel kapselt. Ein Always Encrypted aktivierten Clienttreiber verwendet ein Name des Schlüsselspeicheranbieters, um einen Schlüsselspeicheranbieter in der Registrierung des Treibers, der Schlüsselspeicheranbieter nachzuschlagen. Der Treiber verwendet den Anbieter zum Entschlüsseln von spaltenverschlüsselungsschlüsseln, die durch eine in der zugrunde liegenden Schlüsselspeicher gespeicherten spaltenhauptschlüssel geschützt. Ein Klartextwert eines spaltenverschlüsselungsschlüssels wird dann verwendet, um Abfrageparameter, verschlüsselten Datenbankspalten entsprechend zu verschlüsseln oder Entschlüsseln der Abfrageergebnisse von verschlüsselten Spalten.  
  
 Always Encrypted-fähigen clienttreiberbibliotheken umfassen Schlüsselspeicher-Anbieter für beliebte Schlüsselspeicher.   
  
Ein Satz der verfügbaren Anbieter richten sich nach den Typ und die Version des Client-Treiber. Finden Sie in der Always Encrypted-Dokumentation für bestimmte Treiber:

[Entwickeln Sie Anwendungen mit Always Encrypted mit dem .NET Framework-Datenanbieter für SQL Server](../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)


Die folgenden Tabellen erfasst die Namen der Systemanbieter:  
  
|Name des Schlüsselspeicheranbieters|Zugrunde liegende Schlüsselspeicher|  
    |-----------------------------|--------------------------|
    |"MSSQL_CERTIFICATE_STORE"|Windows-Zertifikatspeicher| 
    |"MSSQL_CSP_PROVIDER"|Ein Speicher, z. B. ein Hardwaresicherheitsmodul (HSM), ein, die Microsoft CryptoAPI unterstützt.|
    |"MSSQL_CNG_STORE"|Ein Speicher, z. B. ein Hardwaresicherheitsmodul (HSM), ein, die Kryptografie-API unterstützt: Next Generation.|  
    |"Azure_Key_Vault"|Finden Sie unter [erste Schritte mit Azure Key Vault.](https://azure.microsoft.com/documentation/articles/key-vault-get-started/)|  
  

 Sie können einen benutzerdefinierte Schlüsselspeicheranbieter implementieren, damit speichern spaltenhauptschlüssel in einem Speicher für die kein integriertes Schlüssel vorhanden ist, speichern Sie Anbieter in Ihrer Always Encrypted aktivierten Clienttreiber.  Beachten Sie, die die Namen der benutzerdefinierten Schlüsselspeicheranbieter darf nicht mit "MSSQL_", ein Präfix ist beginnen reserviert für [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Schlüsselspeicheranbieter. 

  
 key_path  
 Der Pfad des Schlüssels in den spaltenhauptschlüssel speichern. Der Schlüsselpfad muss im Kontext der jede Clientanwendung, die zum Verschlüsseln oder Entschlüsseln von Daten in eine Spalte mit dem Hauptschlüssel für die Spalte verwiesen wird (indirekt) geschützt sein gültig sein und die Clientanwendung muss zulässig sein, um Zugriff auf den Schlüssel. Das Format des Schlüsselpfads bezieht sich auf den Schlüsselspeicher-Anbieter. Die folgende Liste beschreibt das Format von schlüsselpfaden für bestimmte Microsoft-System-Schlüsselspeicher-Anbieter.  
  
-   **Anbietername:** MSSQL_CERTIFICATE_STORE  
  
     **Format des Schlüsselpfads:** *Zertifikatspeichername*/*CertificateStoreLocation*/*CertificateThumbprint*  
  
     Erläuterungen:  
  
     *CertificateStoreLocation*  
     Zertifikatsspeicherort an, in der aktuellen Benutzer oder den lokalen Computer sein muss. Weitere Informationen finden Sie unter [des lokalen Computers und aktuellen Benutzerzertifikatspeichern](https://msdn.microsoft.com/library/windows/hardware/ff548653.aspx).  
  
     *CertificateStore*  
     Zertifikatsspeichername angegeben, z. B. "My".  
  
     *CertificateThumbprint*  
     Fingerabdruck des Zertifikats.  
  
     **Beispiele:**  
  
    ```  
    N'CurrentUser/My/BBF037EC4A133ADCA89FFAEC16CA5BFA8878FB94'  
  
    N'LocalMachine/My/CA5BFA8878FB94BBF037EC4A133ADCA89FFAEC16'  
    ```  
  
-   **Anbietername:** MSSQL_CSP_PROVIDER  
  
     **Format des Schlüsselpfads:** *ProviderName*/*KeyIdentifier*  
  
     Erläuterungen:  
  
     *ProviderName*  
     Der Name einer Cryptography Service Provider (CSP), die für die spaltenhauptschlüsselspeicher CAPI implementiert. Wenn Sie eine HSM als einen Schlüsselspeicher verwenden, muss dies der Name des CSP den HSM-Anbieter bereitstellt. Der Anbieter muss auf einem Clientcomputer installiert werden.  
  
     *KeyIdentifier*  
     Bezeichner des Schlüssels wird als ein spaltenhauptschlüssel im Schlüsselspeicher verwendet.  
  
     **Beispiele:**  
  
    ```  
    N'My HSM CSP Provider/AlwaysEncryptedKey1'  
    ```  
  
-   **Anbietername:** MSSQL_CNG_STORE  
  
     **Format des Schlüsselpfads:** *ProviderName*/*KeyIdentifier*  
  
     Erläuterungen:  
  
     *ProviderName*  
     Name der der Schlüssel Schlüsselspeicheranbieter (KSP), der die Kryptografie implementiert: Next Generation (CNG)-API für die spaltenhauptschlüsselspeicher. Wenn Sie eine HSM als einen Schlüsselspeicher verwenden, muss dies der Name des den KSP den HSM-Anbieter bereitstellt. Der Anbieter muss auf einem Clientcomputer installiert werden.  
  
     *KeyIdentifier*  
     Bezeichner des Schlüssels wird als ein spaltenhauptschlüssel im Schlüsselspeicher verwendet.  
  
     **Beispiele:**  
  
    ```  
    N'My HSM CNG Provider/AlwaysEncryptedKey1'  
    ```  

-   **Anbietername:** AZURE_KEY_STORE  
  
     **Format des Schlüsselpfads:** *KeyUrl*  
  
     Erläuterungen:  
  
     *KeyUrl*  
     Die URL des Schlüssels im Azure Key Vault


Beispiel:
 
`N'https://myvault.vault.azure.net:443/keys/MyCMK/4c05f1a41b12488f9cba2ea964b6a700'`  
  
## <a name="remarks"></a>Hinweise  

Erstellen einen Eintrag in der Spalte Hauptschlüssel Metadaten ist erforderlich, bevor ein Eintrag in der Spalte Verschlüsselung schlüsselmetadaten in der Datenbank und vor jeder Spalte in der Datenbank verschlüsselt werden kann, mit "immer verschlüsselt" erstellt werden kann. Beachten Sie, dass ein Eintrag in der Spalte Hauptschlüssel in den Metadaten nicht den tatsächlichen spaltenhauptschlüssel enthalten, die in einem Schlüsselspeicher der externen Spalte (außerhalb von SQL Server) gespeichert werden müssen. Der Name des Schlüsselspeicheranbieters und den Pfad des Hauptschlüssels Spalte in den Metadaten müssen für eine Clientanwendung auf den spaltenhauptschlüssel zum Entschlüsseln eines spaltenverschlüsselungsschlüssels mit dem spaltenhauptschlüssel verschlüsselt und zum Abfragen von verschlüsselten Spalten verwenden, können gültig sein.


  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die **ALTER ANY COLUMN MASTER KEY** Berechtigung.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-creating-a-column-master-key"></a>A. Erstellen einen spaltenhauptschlüssel  
 Erstellen einen Spalte Hauptschlüssel-Metadateneintrag für eine Spalte im Schlüsselspeicher gespeicherten spaltenhauptschlüssel Zertifikatspeicher für Clientanwendungen, die den MSSQL_CERTIFICATE_STORE-Anbieter zu verwenden, um den spaltenhauptschlüssel zuzugreifen:  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
     KEY_STORE_PROVIDER_NAME = N'MSSQL_CERTIFICATE_STORE',   
     KEY_PATH = 'Current User/Personal/f2260f28d909d21c642a3d8e0b45a830e79a1420'  
   );  
```  
  
 Erstellen einen Spalte Hauptschlüssel-Metadateneintrag für einen spaltenhauptschlüssel, die von Clientanwendungen zugegriffen wird, den Anbieter MSSQL_CNG_STORE verwenden:  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
    KEY_STORE_PROVIDER_NAME = N'MSSQL_CNG_STORE',    
    KEY_PATH = N'My HSM CNG Provider/AlwaysEncryptedKey'  
);  
```  
  
 Erstellen einen spaltenhauptschlüssel in Azure Key Vault für Clientanwendungen, die den Anbieter AZURE_KEY_VAULT zu verwenden, um den spaltenhauptschlüssel zuzugreifen gespeichert.  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
    KEY_STORE_PROVIDER_NAME = N'AZURE_KEY_VAULT',  
    KEY_PATH = N'https://myvault.vault.azure.net:443/keys/  
        MyCMK/4c05f1a41b12488f9cba2ea964b6a700');  
```  
  
 Erstellen einen CMK in eine benutzerdefinierte spaltenhauptschlüsselspeicher gespeichert:  
  
```  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
    KEY_STORE_PROVIDER_NAME = 'CUSTOM_KEY_STORE',    
    KEY_PATH = 'https://contoso.vault/sales_db_tce_key'  
);  
```  
  
## <a name="see-also"></a>Siehe auch
 
* [DROP COLUMN MASTER KEY &#40; Transact-SQL &#41;](../../t-sql/statements/drop-column-master-key-transact-sql.md)   
* [CREATE COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-encryption-key-transact-sql.md)
* [sys.column_master_keys (Transact-SQL)](../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)
* [Always Encrypted &#40;Datenbankmodul&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)  
* [Overview of Key Management for Always Encrypted (Übersicht über die Schlüsselverwaltung für Always Encrypted)](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)
  


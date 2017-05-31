---
title: "Verwenden von SQL Server-Connector mit SQL-Verschlüsselungsfunktionen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Connector, using
- EKM, with SQL Server Connector
ms.assetid: 58fc869e-00f1-4d7c-a49b-c0136c9add89
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: e24c6b23aeafcbeebf5cf5515803c7eb909a65db
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="use-sql-server-connector-with-sql-encryption-features"></a>Verwenden von SQL Server-Connector mit SQL-Verschlüsselungsfunktionen
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gebräuchliche [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Verschlüsselungsaktivitäten unter Verwendung eines asymmetrischen Schlüssels, der von Azure Key Vault geschützt wird, finden sich in den folgenden drei Bereichen.  
  
-   Transparente Datenverschlüsselung mithilfe eines asymmetrischen Schlüssels aus Azure Key Vault  
  
-   Verschlüsseln von Sicherungen mit einem asymmetrischen Schlüssel aus dem Schlüsseltresor  
  
-   Verschlüsselung auf Spaltenebene mit einem asymmetrischen Schlüssel aus dem Schlüsseltresor  
  
 Schließen Sie die Teile I bis IV des Themas [Installationsschritte für die Erweiterbare Schlüsselverwaltung mit Azure Key Vault](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md)ab, bevor Sie die Schritte in diesem Thema ausführen.  
 
> [!NOTE]  
>  Die Versionen 1.0.0.440 und älter wurden ersetzt und werden nicht länger in Produktionsumgebungen unterstützt. Führen Sie ein Upgrade auf Version 1.0.1.0 oder höher durch, indem Sie das [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=45344) besuchen und die Anweisungen auf der Seite [SQL Server-Connector Wartung & Problembehandlung](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md) (SQL Server Connector Wartung & Problembehandlung) unter „Upgrade des SQL Server-Connectors“ ausführen.  
  
## <a name="transparent-data-encryption-by-using-an-asymmetric-key-from-azure-key-vault"></a>Transparente Datenverschlüsselung mithilfe eines asymmetrischen Schlüssels aus Azure Key Vault  
 Verwenden Sie nach dem Abschluss der Teile I bis IV des Themas „Installationsschritte für die Erweiterbare Schlüsselverwaltung mit Azure Key Vault“ den Azure Key Vault-Schlüssel, um den Datenbankverschlüsselungsschlüssel mithilfe von TDE zu verschlüsseln.  
Sie müssen Anmeldeinformationen und eine Anmeldung sowie einen Datenbankverschlüsselungsschlüssel erstellen, der zum Verschlüsseln der Daten und Protokolle in der Datenbank dient. Zum Verschlüsseln einer Datenbank ist die **CONTROL** -Berechtigung für die Datenbank erforderlich. Die folgende Grafik zeigt die Hierarchie des Verschlüsselungsschlüssels bei Verwendung von Azure Key Vault.  
  
 ![ekm&#45;key&#45;hierarchy&#45;with&#45;akv](../../../relational-databases/security/encryption/media/ekm-key-hierarchy-with-akv.png "ekm-key-hierarchy-with-akv")  
  
1.  **Erstellen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Anmeldeinformationen für das Datenbankmodul für die Nutzung von TDE**  
  
     Das Datenbankmodul verwendet die Anmeldeinformationen für den Zugriff auf den Schlüsseltresor während des Ladens der Datenbank. Es wird empfohlen, in Teil I eine weitere Azure Active Directory- **Client-ID** und einen weiteren **geheimen Schlüssel** für das [!INCLUDE[ssDE](../../../includes/ssde-md.md)]zu erstellen, um die erteilten Schlüsseltresorberechtigungen einzuschränken.  
  
     Ändern Sie das [!INCLUDE[tsql](../../../includes/tsql-md.md)] -Skript unten in der folgenden Weise:  
  
    -   Bearbeiten Sie das `IDENTITY` -Argument (`ContosoDevKeyVault`), damit es auf Ihren Azure Key Vault verweist.
        - Wenn Sie eine **öffentliche Azure-Cloud**verwenden, ersetzen Sie das `IDENTITY` -Argument durch den Namen Ihres Azure Key Vault aus Teil II.
        - Wenn Sie eine **private Azure-Cloud** verwenden (z. B. Azure für Behörden, Azure China oder Azure Deutschland), ersetzen Sie das `IDENTITY` -Argument durch den Tresor-URI, der in Teil II, Schritt 3 zurückgegeben wird. Schließen Sie „https://“ nicht in den Tresor-URI ein.   
  
    -   Ersetzen Sie den ersten Teil des `SECRET` -Arguments durch die Azure Active Directory- **Client-ID** aus Teil I. In diesem Beispiel ist die **Client-ID** `EF5C8E094D2A4A769998D93440D8115D`.  
  
        > [!IMPORTANT]  
        >  Bindestriche müssen aus der **Client-ID**entfernt werden.  
  
    -   Setzen Sie in den zweiten Teil des `SECRET` -Arguments den **geheimen Clientschlüssel** aus Teil I ein. In diesem Beispiel ist der **geheime Clientschlüssel** aus Teil I `Replace-With-AAD-Client-Secret`. Die endgültige Zeichenfolge für das `SECRET` -Argument ist eine lange Abfolge von Buchstaben und Ziffern *ohne Bindestriche*.  
  
    ```tsql  
    USE master;  
    CREATE CREDENTIAL Azure_EKM_TDE_cred   
        WITH IDENTITY = 'ContosoDevKeyVault', -- for public Azure
        -- WITH IDENTITY = 'ContosoDevKeyVault.vault.usgovcloudapi.net', -- for Azure Government
        -- WITH IDENTITY = 'ContosoDevKeyVault.vault.azure.cn', -- for Azure China
        -- WITH IDENTITY = 'ContosoDevKeyVault.vault.microsoftazure.de', -- for Azure Germany   
        SECRET = 'EF5C8E094D2A4A769998D93440D8115DReplace-With-AAD-Client-Secret'   
    FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov;  
    ```  
  
2.  **Erstellen einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Anmeldung für das [!INCLUDE[ssDE](../../../includes/ssde-md.md)] für TDE**  
  
     Erstellen Sie eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Anmeldung, und fügen Sie ihr die Anmeldeinformationen aus Schritt 1 hinzu. In diesem [!INCLUDE[tsql](../../../includes/tsql-md.md)] -Beispiel wird der gleiche Schlüssel verwendet, der zuvor importiert wurde.  
  
    ```tsql  
    USE master;  
    -- Create a SQL Server login associated with the asymmetric key   
    -- for the Database engine to use when it loads a database   
    -- encrypted by TDE.  
    CREATE LOGIN TDE_Login   
    FROM ASYMMETRIC KEY CONTOSO_KEY;  
    GO   
  
    -- Alter the TDE Login to add the credential for use by the   
    -- Database Engine to access the key vault  
    ALTER LOGIN TDE_Login   
    ADD CREDENTIAL Azure_EKM_TDE_cred ;  
    GO  
    ```  
  
3.  **Erstellen des Datenbank-Verschlüsselungsschlüssels (DEK)**  
  
     Der DEK verschlüsselt Ihre Daten und Protokolldateien in der Datenbankinstanz und wird seinerseits mithilfe des asymmetrischen Schlüssels aus Azure Key Vault verschlüsselt. Der DEK kann mithilfe eines beliebigen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] unterstützten Algorithmus mit beliebiger Schlüssellänge erstellt werden.  
  
    ```tsql  
    USE ContosoDatabase;  
    GO  
  
    CREATE DATABASE ENCRYPTION KEY   
    WITH ALGORITHM = AES_256   
    ENCRYPTION BY SERVER ASYMMETRIC KEY CONTOSO_KEY;  
    GO  
    ```  
  
4.  **Aktivieren von TDE**  
  
    ```tsql  
    -- Alter the database to enable transparent data encryption.  
    ALTER DATABASE ContosoDatabase   
    SET ENCRYPTION ON;  
    GO  
    ```  
  
     Überprüfen Sie mithilfe von [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)], dass TDE aktiviert wurde, indem Sie eine Verbindung mit Ihrer Datenbank mithilfe des Objekt-Explorers herstellen. Klicken Sie mit der rechten Maustaste auf Ihre Datenbank, zeigen Sie auf **Aufgaben**, und klicken Sie anschließend auf **Datenbankverschlüsselung verwalten**.  
  
     ![ekm&#45;tde&#45;object&#45;explorer](../../../relational-databases/security/encryption/media/ekm-tde-object-explorer.png "ekm-tde-object-explorer")  
  
     Prüfen Sie im Dialogfeld **Datenbankverschlüsselung verwalten** , nach, ob TDE aktiviert ist und welcher Schlüssel für die Verschlüsselung des DEKs verwendet wird.  
  
     ![ekm&#45;tde&#45;dialog&#45;box](../../../relational-databases/security/encryption/media/ekm-tde-dialog-box.png "ekm-tde-dialog-box")  
  
     Alternativ können Sie das folgende [!INCLUDE[tsql](../../../includes/tsql-md.md)] -Skript ausführen. Der Verschlüsselungsstatus 3 gibt eine verschlüsselte Datenbank an.  
  
    ```tsql  
    USE MASTER  
    SELECT * FROM sys.asymmetric_keys  
  
    -- Check which databases are encrypted using TDE  
    SELECT d.name, dek.encryption_state   
    FROM sys.dm_database_encryption_keys AS dek  
    JOIN sys.databases AS d  
         ON dek.database_id = d.database_id;  
    ```  
  
    > [!NOTE]  
    >  Die `tempdb` -Datenbank wird automatisch verschlüsselt, wenn für eine beliebige Datenbank TDE aktiviert wird.  
  
## <a name="encrypting-backups-by-using-an-asymmetric-key-from-the-key-vault"></a>Verschlüsseln von Sicherungen mit einem asymmetrischen Schlüssel aus dem Schlüsseltresor  
 Verschlüsselte Sicherungen werden ab [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]unterstützt. Im folgenden Beispiel wird eine Sicherung erstellt und wiederhergestellt, die mit einem Verschlüsselungsschlüssel verschlüsselt wurde, der durch den asymmetrischen Schlüssel im Schlüsseltresor geschützt wird.  
Das [!INCLUDE[ssDE](../../../includes/ssde-md.md)] benötigt die Anmeldeinformationen zum Zugriff auf den Schlüsseltresor während des Ladens der Datenbank. Es wird empfohlen, in Teil I eine weitere Azure Active Directory-Client-ID und einen weiteren geheimen Schlüssel für das Datenbankmodul zu erstellen, um die erteilten Schlüsseltresorberechtigungen einzuschränken.  
  
1.  **Erstellen von SQL Server-Anmeldeinformationen für das Datenbankmodul für die Sicherungsverschlüsselung**  
  
     Ändern Sie das [!INCLUDE[tsql](../../../includes/tsql-md.md)] -Skript unten in der folgenden Weise:  
  
    -   Bearbeiten Sie das `IDENTITY` -Argument (`ContosoDevKeyVault`), damit es auf Ihren Azure Key Vault verweist.
        - Wenn Sie eine **öffentliche Azure-Cloud**verwenden, ersetzen Sie das `IDENTITY` -Argument durch den Namen Ihres Azure Key Vault aus Teil II.
        - Wenn Sie eine **private Azure-Cloud** verwenden (z. B. Azure für Behörden, Azure China oder Azure Deutschland), ersetzen Sie das `IDENTITY` -Argument durch den Tresor-URI, der in Teil II, Schritt 3 zurückgegeben wird. Schließen Sie „https://“ nicht in den Tresor-URI ein.    
  
    -   Ersetzen Sie den ersten Teil des `SECRET` -Arguments durch die Azure Active Directory- **Client-ID** aus Teil I. In diesem Beispiel ist die **Client-ID** `EF5C8E094D2A4A769998D93440D8115D`.  
  
        > [!IMPORTANT]  
        >  Bindestriche müssen aus der **Client-ID**entfernt werden.  
  
    -   Setzen Sie in den zweiten Teil des `SECRET` -Arguments den **geheimen Clientschlüssel** aus Teil I ein. In diesem Beispiel ist der **geheime Clientschlüssel** aus Teil I `Replace-With-AAD-Client-Secret`. Die endgültige Zeichenfolge für das `SECRET` -Argument ist eine lange Abfolge von Buchstaben und Ziffern *ohne Bindestriche*.   
  
        ```tsql  
        USE master;  
  
        CREATE CREDENTIAL Azure_EKM_Backup_cred   
            WITH IDENTITY = 'ContosoDevKeyVault', -- for public Azure
            -- WITH IDENTITY = 'ContosoDevKeyVault.vault.usgovcloudapi.net', -- for Azure Government
            -- WITH IDENTITY = 'ContosoDevKeyVault.vault.azure.cn', -- for Azure China
            -- WITH IDENTITY = 'ContosoDevKeyVault.vault.microsoftazure.de', -- for Azure Germany   
            SECRET = 'EF5C8E094D2A4A769998D93440D8115DReplace-With-AAD-Client-Secret'   
        FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov;    
        ```  
  
2.  **Erstellen einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Anmeldung für das [!INCLUDE[ssDE](../../../includes/ssde-md.md)] für die Sicherungsverschlüsselung**  
  
     Erstellen Sie eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] --Anmeldung, die vom [!INCLUDE[ssDE](../../../includes/ssde-md.md)]für verschlüsselte Sicherungen verwendet wird, und fügen Sie ihr die Anmeldeinformationen aus Schritt 1 hinzu. In diesem [!INCLUDE[tsql](../../../includes/tsql-md.md)] -Beispiel wird der gleiche Schlüssel verwendet, der zuvor importiert wurde.  
  
    > [!IMPORTANT]  
    >  Sie können zum Verschlüsseln von Sicherungen keinen asymmetrischen Schlüssel verwenden, den Sie bereits für TDE (im Beispiel oben) oder die Verschlüsselung auf Spaltenebene (im Beispiel unten) verwendet haben.  
  
     In diesem Beispiel wird der asymmetrische Schlüssel `CONTOSO_KEY_BACKUP` aus dem Schlüsseltresor verwendet, der zuvor für die Masterdatenbank importiert oder erstellt werden kann, wie weiter oben in Teil IV, Schritt 5 beschrieben.  
  
    ```tsql  
    USE master;  
  
    -- Create a SQL Server login associated with the asymmetric key   
    -- for the Database engine to use when it is encrypting the backup.  
    CREATE LOGIN Backup_Login   
    FROM ASYMMETRIC KEY CONTOSO_KEY_BACKUP;  
    GO   
  
    -- Alter the Encrypted Backup Login to add the credential for use by   
    -- the Database Engine to access the key vault  
    ALTER LOGIN Backup_Login   
    ADD CREDENTIAL Azure_EKM_Backup_cred ;  
    GO  
    ```  
  
3.  **Sichern der Datenbank**  
  
     Sichern Sie die Datenbank, und geben Sie die Verschlüsselung mit dem im Key Vault gespeicherten symmetrischen Schlüssel an.
     
     Im folgenden Beispiel sollten Sie beachten, dass wenn die Datenbank bereits mit TDE verschlüsselt wurde und sich der asymmetrische Schlüssel `CONTOSO_KEY_BACKUP` vom asymmetrischen Schlüssel von TDE unterscheidet, die Sicherung mit dem asymmetrischen Schlüssel von TDE und `CONTOSO_KEY_BACKUP` verschlüsselt wird. Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Zielinstanz benötigt beide Schlüssel, um die Sicherung zu entschlüsseln.
  
    ```tsql  
    USE master;  
  
    BACKUP DATABASE [DATABASE_TO_BACKUP]  
    TO DISK = N'[PATH TO BACKUP FILE]'   
    WITH FORMAT, INIT, SKIP, NOREWIND, NOUNLOAD,   
    ENCRYPTION(ALGORITHM = AES_256,   
    SERVER ASYMMETRIC KEY = [CONTOSO_KEY_BACKUP]);  
    GO  
    ```  
  
4.  **Wiederherstellen der Datenbank**  
    
    Um eine Sicherung, die mithilfe von TDE verschlüsselt wurde, wiederherzustellen, muss die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Zielinstanz zunächst über eine Kopie des asymmetrischen Key Vault-Schlüssels für die Verschlüsselung verfügen. Dies würde folgendermaßen erreicht werden:  
    
    - Ist der ursprüngliche asymmetrische Schlüssel, der für TDE verwendet wird, nicht mehr im Key Vault vorhanden, dann stellen Sie die wichtigste Schlüsselsicherung im Key Vault wieder her oder importieren Sie den Schlüssel aus einem lokalen HSM. **Wichtig:** Damit der Fingerabdruck des Schlüssels dem in der Datenbanksicherung gespeicherten Fingerabdruck entspricht, erhält der Schlüssel **denselben Key Vault-Schlüsselnamen**, den er ursprünglich erhalten hatte.
    
    - Wenden Sie die Schritte 1 und 2 auf die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Zielinstanz an.
    
    - Sobald die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Zielinstanz Zugriff auf den asymmetrischen Schlüssel zum Verschlüsseln der Sicherung hat, stellen Sie die Datenbank auf dem Server wieder her.
    
     Codebeispiel für die Wiederherstellung:  
  
    ```tsql  
    RESTORE DATABASE [DATABASE_TO_BACKUP]  
    FROM DISK = N'[PATH TO BACKUP FILE]'   
        WITH FILE = 1, NOUNLOAD, REPLACE;  
    GO  
    ```  
  
     Weitere Informationen zu Sicherungsoptionen finden Sie unter [BACKUP (Transact-SQL)](../../../t-sql/statements/backup-transact-sql.md).  
  
## <a name="column-level-encryption-by-using-an-asymmetric-key-from-the-key-vault"></a>Verschlüsselung auf Spaltenebene mit einem asymmetrischen Schlüssel aus dem Schlüsseltresor  
 Das folgende Beispiel erstellt einen symmetrischen Schlüssel, der durch den asymmetrischen Schlüssel im Schlüsseltresor geschützt wird. Anschließend wird der symmetrische Schlüssel zum Verschlüsseln von Daten in der Datenbank verwendet.  
  
> [!IMPORTANT]  
>  Sie können für die Sicherungsverschlüsselung nicht den gleichen asymmetrischen Schlüssel verwenden, den Sie bereits für TDE oder die Sicherungsverschlüsslung (siehe vorstehende Beispiele) verwendet haben.  
  
 In diesem Beispiel wird der asymmetrische Schlüssel `CONTOSO_KEY_COLUMNS` aus dem Schlüsseltresor verwendet, der zuvor importiert oder erstellt wurde, wie oben in Schritt 3, Abschnitt 3 von [Installationsschritte für die Erweiterbare Schlüsselverwaltung mit Azure Key Vault](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md)beschrieben. Um diesen asymmetrischen Schlüssel in der `ContosoDatabase` -Datenbank zu verwenden, müssen Sie die `CREATE ASYMMETRIC KEY` -Anweisung erneut ausführen, um der `ContosoDatabase` -Datenbank einen Verweis auf den Schlüssel zur Verfügung zu stellen.  
  
```tsql  
USE [ContosoDatabase];  
GO  
  
-- Create a reference to the key in the key vault  
CREATE ASYMMETRIC KEY CONTOSO_KEY_COLUMNS   
FROM PROVIDER [AzureKeyVault_EKM_Prov]  
WITH PROVIDER_KEY_NAME = 'ContosoDevRSAKey2',  
CREATION_DISPOSITION = OPEN_EXISTING;  
  
-- Create the data encryption key.  
-- The data encryption key can be created using any SQL Server   
-- supported algorithm or key length.  
-- The DEK will be protected by the asymmetric key in the key vault  
  
CREATE SYMMETRIC KEY DATA_ENCRYPTION_KEY  
    WITH ALGORITHM=AES_256  
    ENCRYPTION BY ASYMMETRIC KEY CONTOSO_KEY_COLUMNS;  
  
DECLARE @DATA VARBINARY(MAX);  
  
--Open the symmetric key for use in this session  
OPEN SYMMETRIC KEY DATA_ENCRYPTION_KEY   
DECRYPTION BY ASYMMETRIC KEY CONTOSO_KEY_COLUMNS;  
  
--Encrypt syntax  
SELECT @DATA = ENCRYPTBYKEY  
    (  
    KEY_GUID('DATA_ENCRYPTION_KEY'),   
    CONVERT(VARBINARY,'Plain text data to encrypt')  
    );  
  
-- Decrypt syntax  
SELECT CONVERT(VARCHAR, DECRYPTBYKEY(@DATA));  
  
--Close the symmetric key  
CLOSE SYMMETRIC KEY DATA_ENCRYPTION_KEY;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Installationsschritte für die Erweiterbare Schlüsselverwaltung mit Azure Key Vault](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md)   
 [Erweiterbare Schlüsselverwaltung mit Azure Key Vault](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
 [EKM provider enabled (Serverkonfigurationsoption)](../../../database-engine/configure-windows/ekm-provider-enabled-server-configuration-option.md)   
 [SQL Server-Connector Wartung & Problembehandlung](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md)  
  
  


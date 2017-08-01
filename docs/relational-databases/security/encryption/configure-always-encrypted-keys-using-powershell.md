---
title: "Konfigurieren von Always Encrypted-Schlüsseln mithilfe von PowerShell | Microsoft-Dokumentation"
ms.custom: 
ms.date: 05/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-security
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3bdf8629-738c-489f-959b-2f5afdaf7d61
caps.latest.revision: 27
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: c4cd6d86cdcfe778d6b8ba2501ad4a654470bae7
ms.openlocfilehash: 0d112912b35e05e5e96ec43cf6bc5f7caee21bf4
ms.contentlocale: de-de
ms.lasthandoff: 07/31/2017

---
# <a name="configure-always-encrypted-keys-using-powershell"></a>Konfigurieren von Always Encrypted-Schlüsseln mithilfe von PowerShell
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

    
Dieser Artikel enthält die Schritte zum Bereitstellen von Always Encrypted-Schlüsseln unter Verwendung des [SqlServer PowerShell-Moduls](../../../relational-databases/scripting/sql-server-powershell-provider.md). Sie können PowerShell verwenden, um Always Encrypted-Schlüssel jeweils [mit und ohne Rollentrennung](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md#KeyManagementRoles)zu verwenden, und so Kontrolle über den Zugriff auf die tatsächlichen Verschlüsselungsschlüssel im Schlüsselspeicher zu bieten, und wer über Zugang zur Datenbank verfügt. 

Für einen Überblick über die Always Encrypted-Schlüsselverwaltung, einschließlich einiger allgemeiner bewährter Methoden, gehen Sie unter [Overview of Key Management for Always Encrypted](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)(Übersicht der Schlüsselverwaltung für Always Encrypted).
Informationen darüber, wie Sie die Arbeit mit dem SQL Server-PowerShell-Modul beginnen, finden Sie unter [Konfigurieren von Always Encrypted-Schlüsseln mithilfe von PowerShell](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md).


## <a name="KeyProvisionWithoutRoles"></a> Schlüsselbereitstellung ohne Rollentrennung

Die in diesem Abschnitt beschriebene Schlüsselbereitstellungsmethode unterstützt die Rollentrennung zwischen Sicherheitsadministratoren und Datenbankadministratoren (DBAs) nicht. Einige der unten aufgeführten Schritten kombinieren Vorgänge auf physischen Schlüsseln mit Vorgängen mit Schlüsselmetadaten. Deshalb wird diese Bereitstellungsmethode für Organisationen empfohlen, die das DevOps-Modell verwenden, oder für Fälle, in denen die Datenbank in der Cloud gehostet wird und das primäre Ziel ist, Cloudadministratoren (nicht jedoch lokalen DBAs) den Zugriff auf sensible Daten zu verweigern. Die Methode wird nicht empfohlen, wenn DBAs zu potenziellen Angreifer gehören, oder wenn DBAs einfach nicht über Zugriff auf sensible Daten verfügen sollen.

Stellen Sie vor der Ausführung der Schritte, die Zugriff auf Nur-Text-Schlüssel oder dem Schlüsselspeicher erfordern (in der Spalte **Greift auf Klartextschlüssel/-schlüsselspeicher zu** unten in der Tabelle angegeben), sicher, dass die PowerShell-Umgebung auf einem sicheren Computer ausgeführt wird, der nicht der Computer ist, auf dem Ihre Datenbank gehostet wird. Weitere Informationen finden Sie im Abschnitt ***Security Considerations for Key Management***(Überlegungen zur Sicherheit für die Schlüsselverwaltung).


Task  |Artikel  |Greift auf Klartextschlüssel/-schlüsselspeicher zu  |Greift auf Datenbank zu   
---------|---------|---------|---------
Schritt 1: Erstellen Sie einen Spaltenhauptschlüssel in einem Schlüsselspeicher.<br><br>**Hinweis:** Das SqlServer PowerShell-Modul unterstützt diesen Schritt nicht. Verwenden Sie die Tools, die für Ihren gewählten Schlüsselspeicher spezifisch sind, um diese Aufgabe über eine Befehlszeile durchzuführen. |[Create and Store Column Master Keys (Always Encrypted) (Erstellen und Speichern von Spaltenhauptschlüsseln (Always Encrypted))](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md) | ja | Nein     
Schritt 2:  Starten Sie eine PowerShell-Umgebung, und importieren Sie das SqlServer PowerShell-Modul.  |   [Konfigurieren von Always Encrypted-Schlüsseln mithilfe von PowerShell](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)   |    Nein    | Nein         
Schritt 3:  Stellen Sie eine Verbindung mit Ihrem Server und Ihrer Datenbank her.     |     [Stellt eine Verbindung mit einer Datenbank her.](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#connectingtodatabase)    |    Nein     | ja         
Schritt 4.  Erstellen Sie ein *SqlColumnMasterKeySettings* -Objekt, dass Informationen über den Speicherort Ihres Spaltenhauptschlüssels enthält. SqlColumnMasterKeySettings ist ein Objekt, das im Arbeitsspeicher (in PowerShell) vorhanden ist. Verwenden Sie das Cmdlet, das für Ihren Schlüsselspeicher spezifisch ist.   |     [New-SqlAzureKeyVaultColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlazurekeyvaultcolumnmasterkeysettings)<br><br>[New-SqlCertificateStoreColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcertificatestorecolumnmasterkeysettings)<br><br>[New-SqlCngColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcngcolumnmasterkeysettings)<br><br>[New-SqlCspColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcspcolumnmasterkeysettings)        |   Nein      | Nein         
Schritt 5.  Erstellen Sie die Metadaten über den Spaltenhauptschlüssel in Ihrer Datenbank.      |    [New-SqlColumnMasterKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnmasterkey)<br><br>**Hinweis:** Im Hintergrund gibt das Cmdlet die Anweisung [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md) heraus, um Schlüsselmetadaten zu erstellen.|    Nein     |    ja
Schritt 6.  Authentifizieren Sie sich bei Azure, wenn Ihr Spaltenhauptschlüssel in Azure Key Vault gespeichert ist. | [Add-SqlAzureAuthenticationContext](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/add-sqlazureauthenticationcontext)    |  ja   | Nein         
Schritt 7.  Generieren Sie einen neuen Spaltenverschlüsselungsschlüssel, verschlüsseln Sie ihn mit dem Spaltenhauptschlüssel, und erstellen Sie Spaltenverschlüsselungsschlüssel-Metadaten in der Datenbank.     |    [New-SqlColumnEncryptionKey](https://docs.microsoft.com/en-us/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnencryptionkey)<br><br>**Hinweis:** Verwenden Sie eine Variation des Cmdlets, dass intern einen Spaltenverschlüsselungsschlüssel generiert und verschlüsselt.<br><br>**Hinweis:** Im Hintergrund gibt das Cmdlet die Anweisung [CREATE COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/create-column-encryption-key-transact-sql.md) heraus, um Schlüsselmetadaten zu erstellen.  | ja | ja
  

## <a name="windows-certificate-store-without-role-separation-example"></a>Windows-Zertifikatspeicher ohne Rollentrennung (Beispiel)

Dieses Skript ist ein End-to-End-Beispiel für das Generieren eines Spaltenhauptschlüssels, der ein Zertifikat im Windows-Zertifikatspeicher darstellt, einen Spaltenverschlüsselungsschlüssel generiert und verschlüsselt und Schlüsselmetadaten in einer SQL Server-Datenbank erstellt.


```
# Create a column master key in Windows Certificate Store.
$cert1 = New-SelfSignedCertificate -Subject "AlwaysEncryptedCert" -CertStoreLocation Cert:CurrentUser\My -KeyExportPolicy Exportable -Type DocumentEncryptionCert -KeyUsage DataEncipherment -KeySpec KeyExchange

# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$connection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection
$connection.ConnectionString = $connStr
$connection.Connect()
$server = New-Object Microsoft.SqlServer.Management.Smo.Server($connection)
$database = $server.Databases[$databaseName]

# Create a SqlColumnMasterKeySettings object for your column master key. 
$cmkSettings = New-SqlCertificateStoreColumnMasterKeySettings -CertificateStoreLocation "CurrentUser" -Thumbprint $cert1.Thumbprint

# Create column master key metadata in the database.
$cmkName = "CMK1"
New-SqlColumnMasterKey -Name $cmkName -InputObject $database -ColumnMasterKeySettings $cmkSettings


# Generate a column encryption key, encrypt it with the column master key and create column encryption key metadata in the database. 
$cekName = "CEK1"
New-SqlColumnEncryptionKey -Name $cekName  -InputObject $database -ColumnMasterKey $cmkName
```

## <a name="azure-key-vault-without-role-separation-example"></a>Azure Key Vault ohne Rollentrennung (Beispiel)

Dieses Skript ist ein End-to-End-Beispiel für das Bereitstellen und Konfigurieren von Azure Key Vault, für das Generieren eines Spaltenhauptschlüssels im Tresor, für das Generieren und Verschlüsseln eines Spaltenhauptschlüssels und für das Erstellen von Schlüsselmetadaten in einer Azure SQL-Datenbank.


```
# Create a column master key in Azure Key Vault.
Login-AzureRmAccount
$SubscriptionId = "<Azure SubscriptionId>"
$resourceGroup = "<resource group name>"
$azureLocation = "<datacenter location>"
$akvName = "<key vault name>"
$akvKeyName = "<key name>"
$azureCtx = Set-AzureRMConteXt -SubscriptionId $SubscriptionId # Sets the context for the below cmdlets to the specified subscription.
New-AzureRmResourceGroup –Name $resourceGroup –Location $azureLocation # Creates a new resource group - skip, if you desire group already exists.
New-AzureRmKeyVault -VaultName $akvName -ResourceGroupName $resourceGroup -Location $azureLocation # Creates a new key vault - skip if your vault already exists.
Set-AzureRmKeyVaultAccessPolicy -VaultName $akvName -ResourceGroupName $resourceGroup -PermissionsToKeys get, create, delete, list, update, import, backup, restore, wrapKey,unwrapKey, sign, verify -UserPrincipalName $azureCtx.Account
$akvKey = Add-AzureKeyVaultKey -VaultName $akvName -Name $akvKeyName -Destination "Software"

# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database (Azure SQL database).
$serverName = "<Azure SQL server name>.database.windows.net"
$databaseName = "<database name>"
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Authentication = Active Directory Integrated"
$connection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection
$connection.ConnectionString = $connStr
$connection.Connect()
$server = New-Object Microsoft.SqlServer.Management.Smo.Server($connection)
$database = $server.Databases[$databaseName] 

# Create a SqlColumnMasterKeySettings object for your column master key. 
$cmkSettings = New-SqlAzureKeyVaultColumnMasterKeySettings -KeyURL $akvKey.ID

# Create column master key metadata in the database.
$cmkName = "CMK1"
New-SqlColumnMasterKey -Name $cmkName -InputObject $database -ColumnMasterKeySettings $cmkSettings

# Authenticate to Azure
Add-SqlAzureAuthenticationContext -Interactive

# Generate a column encryption key, encrypt it with the column master key and create column encryption key metadata in the database. 
$cekName = "CEK1"
New-SqlColumnEncryptionKey -Name $cekName -InputObject $database -ColumnMasterKey $cmkName
```

## <a name="cngksp-without-role-separation-example"></a>CNG/KSP ohne Rollentrennung (Beispiel)

Das Skript unten ist ein End-to-End-Beispiel für das Generieren eines Spaltenhauptschlüssels in einem Schlüsselspeicher, der die Cryptography Next Generation API (CNG) implementiert, für das Generieren und Verschlüsseln eines Spaltenhauptschlüssels und für das Erstellen von Schlüsselmetadaten in einer SQL Server-Datenbank.

Dieses Beispiel nutzt den Schlüsselspeicher, der den Softwareschlüsselspeicher-Anbieter von Microsoft verwendet. Sie möchten vielleicht das Beispiel ändern, um einen anderen Speicher zu verwenden, z.B. Ihr Hardwaresicherheitsmodul. Dazu müssen Sie sicherstellen, dass der Schlüsselspeicheranbieter (KSP), der CNG für Ihr Gerät implementiert, ordnungsgemäß auf dem Computer installiert ist. Sie müssen „Microsoft Software Key Storage Provider“ mit dem Namen des KSPs Ihres Geräts ersetzen.


```
# Create a column master key in a key store that has a CNG provider, a.k.a key store provider (KSP).
$cngProviderName = "Microsoft Software Key Storage Provider" # If you have an HSM, you can use a KSP for your HSM instead of a Microsoft KSP
$cngAlgorithmName = "RSA"
$cngKeySize = 2048 # Recommended key size for Always Encrypted column master keys
$cngKeyName = "AlwaysEncryptedKey" # Name identifying your new key in the KSP
$cngProvider = New-Object System.Security.Cryptography.CngProvider($cngProviderName)
$cngKeyParams = New-Object System.Security.Cryptography.CngKeyCreationParameters
$cngKeyParams.provider = $cngProvider
$cngKeyParams.KeyCreationOptions = [System.Security.Cryptography.CngKeyCreationOptions]::OverwriteExistingKey
$keySizeProperty = New-Object System.Security.Cryptography.CngProperty("Length", [System.BitConverter]::GetBytes($cngKeySize), [System.Security.Cryptography.CngPropertyOptions]::None);
$cngKeyParams.Parameters.Add($keySizeProperty)
$cngAlgorithm = New-Object System.Security.Cryptography.CngAlgorithm($cngAlgorithmName)
$cngKey = [System.Security.Cryptography.CngKey]::Create($cngAlgorithm, $cngKeyName, $cngKeyParams)

# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$connection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection
$connection.ConnectionString = $connStr
$connection.Connect()
$server = New-Object Microsoft.SqlServer.Management.Smo.Server($connection)
$database = $server.Databases[$databaseName]

# Create a SqlColumnMasterKeySettings object for your column master key. 
$cmkSettings = New-SqlCngColumnMasterKeySettings -CngProviderName $cngProviderName -KeyName $cngKeyName

# Create column master key metadata in the database.
$cmkName = "CMK1"
New-SqlColumnMasterKey -Name $cmkName -InputObject $database -ColumnMasterKeySettings $cmkSettings

# Generate a column encryption key, encrypt it with the column master key and create column encryption key metadata in the database. 
$cekName = "CEK1"
New-SqlColumnEncryptionKey -Name $cekName -InputObject $database -ColumnMasterKey $cmkName
```

## <a name="KeyProvisionWithRoles"></a> Schlüsselbereitstellung mit Rollentrennung

Dieser Abschnitt enthält die Schritte zum Konfigurieren einer Verschlüsselung, mit der Sicherheitsadministratoren nicht über Zugriff auf die Datenbank verfügen, und Datenbankadministratoren nicht über Zugriff auf den Schlüsselspeicher oder Nur-Text-Schlüssel verfügen.


### <a name="security-administrator"></a>Sicherheitsadministrator

Bevor Sie Schritte ausführen, für die Sie Zugriff auf Nur-Text-Schlüssel oder den Schlüsselspeicher benötigen (in der Spalte **Greift auf Klartextschlüssel/-schlüsselspeicher zu** in der Tabelle unten), stellen Sie sicher, dass:
1.  Die PowerShell-Umgebung wird auf einem sicheren Computer ausgeführt, der nicht der Computer ist, auf dem Ihre Datenbank gehostet wird.
2.  Datenbankadministratoren in Ihrer Organisation nicht über Zugriff auf den Computer verfügen (die den Zweck der Rollentrennung zunichte machen würden).

Weitere Informationen finden Sie im Abschnitt [Security Considerations for Key Management](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md#SecurityForKeyManagement)(Überlegungen zur Sicherheit für die Schlüsselverwaltung).


Task  |Artikel  |Greift auf Klartextschlüssel/-schlüsselspeicher zu  |Greift auf Datenbank zu  
---------|---------|---------|---------
Schritt 1: Erstellen Sie einen Spaltenhauptschlüssel in einem Schlüsselspeicher.<br><br>**Hinweis:** Das SqlServer-Modul unterstützt diesen Schritt nicht. Sie müssen die Tools Verwenden, die für den Typ Ihres Schlüsselspeichers spezifisch sind, um diese Aufgabe mithilfe einer Befehlszeile durchzuführen.     | [Create and Store Column Master Keys (Always Encrypted) (Erstellen und Speichern von Spaltenhauptschlüsseln (Always Encrypted))](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)  |    ja    | Nein 
Schritt 2:  Starten Sie eine PowerShell-Sitzung, und importieren Sie das SqlServer-Modul.      |     [Importieren des SqlServer-Moduls](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#importsqlservermodule)     | Nein | Nein         
Schritt 3:  Erstellen Sie ein *SqlColumnMasterKeySettings* -Objekt, dass Informationen über den Speicherort Ihres Spaltenhauptschlüssels enthält. *SqlColumnMasterKeySettings* ist ein Objekt, das im Arbeitsspeicher (in PowerShell) vorhanden ist. Verwenden Sie das Cmdlet, das für Ihren Schlüsselspeicher spezifisch ist. |      [New-SqlAzureKeyVaultColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlazurekeyvaultcolumnmasterkeysettings)<br><br>[New-SqlCertificateStoreColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcertificatestorecolumnmasterkeysettings)<br><br>[New-SqlCngColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcngcolumnmasterkeysettings)<br><br>[New-SqlCspColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcspcolumnmasterkeysettings)   | Nein         | Nein         
Schritt 4.  Authentifizieren Sie sich bei Azure, wenn Ihr Spaltenhauptschlüssel in Azure Key Vault gespeichert ist. |    [Add-SqlAzureAuthenticationContext](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/add-sqlazureauthenticationcontext)    |ja|Nein         
Schritt 5.  Generieren Sie einen Spaltenverschlüsselungsschlüssel, und verschlüsseln Sie ihn mit dem Spaltenhauptschlüssel, um einen verschlüsselten Wert des Spaltenverschlüsselungsschlüssels zu erstellen.     |   [New-SqlColumnEncryptionKeyEncryptedValue](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnencryptionkeyencryptedvalue)     |    ja    | Nein        
Schritt 6.  Stellen Sie den Speicherort des Spaltenhauptschlüssels (den Anbieternamen und einen Schlüsselpfad des Spaltenhauptschlüssels) und einen verschlüsselten Wert des Spaltenverschlüsselungsschlüssels für den DBA bereit.  | Siehe folgende Beispiele.        |   Nein      | Nein         

### <a name="dba"></a>DBA 

Datenbankadministratoren (DBAs) verwenden die Informationen, die sie vom Sicherheitsadministrator (Schritt 6 oben) empfangen, um die Always Encrypted-Schlüsselmetadaten in der Datenbank zu erstellen und zu verwalten.

Task  |Artikel  |Greift auf Nur-Text-Schlüsse zu  |Greift auf Datenbank zu   
---------|---------|---------|---------
Schritt 1:  Rufen Sie den Speicherort des Spaltenhauptschlüssels und des verschlüsselten Werts des Spaltenverschlüsselungsschlüssels von Ihrem Sicherheitsadministrator ab. |Siehe folgende Beispiele. | Nein | Nein
Schritt 2:  Starten Sie eine PowerShell-Umgebung, und importieren Sie das SqlServer-Modul.  | [Konfigurieren von Always Encrypted-Schlüsseln mithilfe von PowerShell](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)  | Nein | Nein
Schritt 3:  Stellen Sie eine Verbindung mit Ihrem Server und Ihrer Datenbank her. | [Herstellen einer Verbindung mit einer Datenbank](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#connectingtodatabase) | Nein | ja
Schritt 4.  Erstellen Sie ein SqlColumnMasterKeySettings-Objekt, dass Informationen über den Speicherort Ihres Spaltenhauptschlüssels enthält. SqlColumnMasterKeySettings ist ein Objekt, das im Arbeitsspeicher vorhanden ist. | New-SqlColumnMasterKeySettings | Nein | Nein
Schritt 5. Erstellen Sie die Metadaten über den Spaltenhauptschlüssel in Ihrer Datenbank. | [New-SqlColumnMasterKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnmasterkey)<br>**Hinweis:** Im Hintergrund gibt das Cmdlet die Anweisung [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md) heraus, um Spaltenhauptschlüssel-Metadaten zu erstellen. | Nein | ja
Schritt 6. Erstellen Sie die Spaltenverschlüsselungsschlüssel-Metadaten in der Datenbank. | New-SqlColumnEncryptionKey<br>**Hinweis:** DBAs verwenden eine Variation des Cmdlets, das nur Spaltenverschlüsselungsschlüssel-Metadaten erstellt.<br>Im Hintergrund gibt das Cmdlet die Anweisung [CREATE COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/create-column-encryption-key-transact-sql.md) heraus, um Spaltenverschlüsselungsschlüssel-Metadaten zu erstellen. | Nein | ja
  
## <a name="windows-certificate-store-with-role-separation-example"></a>Windows-Zertifikatspeicher mit Rollentrennung (Beispiel)

### <a name="security-administrator"></a>Sicherheitsadministrator


```
# Create a column master key in Windows Certificate Store.
$storeLocation = "CurrentUser"
$certPath = "Cert:" + $storeLocation + "\My"
$cert = New-SelfSignedCertificate -Subject "AlwaysEncryptedCert" -CertStoreLocation $certPath -KeyExportPolicy Exportable -Type DocumentEncryptionCert -KeyUsage DataEncipherment -KeySpec KeyExchange

# Import the SqlServer module
Import-Module "SqlServer"

# Create a SqlColumnMasterKeySettings object for your column master key. 
$cmkSettings = New-SqlCertificateStoreColumnMasterKeySettings -CertificateStoreLocation "CurrentUser" -Thumbprint $cert.Thumbprint

# Generate a column encryption key, encrypt it with the column master key to produce an encrypted value of the column encryption key.
$encryptedValue = New-SqlColumnEncryptionKeyEncryptedValue -TargetColumnMasterKeySettings $cmkSettings

# Share the location of the column master key and an encrypted value of the column encryption key with a DBA, via a CSV file on a share drive
$keyDataFile = "Z:\keydata.txt"
"KeyStoreProviderName, KeyPath, EncryptedValue" > $keyDataFile
$cmkSettings.KeyStoreProviderName + ", " + $cmkSettings.KeyPath + ", " + $encryptedValue >> $keyDataFile

# Read the key data back to verify
$keyData = Import-Csv $keyDataFile
$keyData.KeyStoreProviderName
$keyData.KeyPath
$keyData.EncryptedValue 
```

### <a name="dba"></a>DBA

```
# Obtain the location of the column master key and the encrypted value of the column encryption key from your Security Administrator, via a CSV file on a share drive.
$keyDataFile = "Z:\keydata.txt"
$keyData = Import-Csv $keyDataFile

# Import the SqlServer module
Import-Module "SqlServer"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$connection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection
$connection.ConnectionString = $connStr
$connection.Connect()
$server = New-Object Microsoft.SqlServer.Management.Smo.Server($connection)
$database = $server.Databases[$databaseName]

# Create a SqlColumnMasterKeySettings object for your column master key. 
$cmkSettings = New-SqlColumnMasterKeySettings -KeyStoreProviderName $keyData.KeyStoreProviderName -KeyPath $keyData.KeyPath

# Create column master key metadata in the database.
$cmkName = "CMK1"
New-SqlColumnMasterKey -Name $cmkName -InputObject $database -ColumnMasterKeySettings $cmkSettings

# Generate a  column encryption key, encrypt it with the column master key and create column encryption key metadata in the database. 
$cekName = "CEK1"
New-SqlColumnEncryptionKey -Name $cekName -InputObject $database -ColumnMasterKey $cmkName -EncryptedValue $keyData.EncryptedValue
```  
 
## <a name="next-steps"></a>Nächste Schritte    

- [Konfigurieren der Spaltenverschlüsselung mithilfe von PowerShell](../../../relational-databases/security/encryption/configure-column-encryption-using-powershell.md)    
- [Rotieren von Always Encrypted-Schlüsseln mithilfe von PowerShell](../../../relational-databases/security/encryption/rotate-always-encrypted-keys-using-powershell.md)
    
## <a name="additional-resources"></a>Zusätzliche Ressourcen    
    
- [Übersicht über die Schlüsselverwaltung für Always Encrypted](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)
- [Konfigurieren von Always Encrypted mithilfe von PowerShell](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)
- [„Immer verschlüsselt“ (Datenbankmodul)](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Always Encrypted (Cliententwicklung)](../../../relational-databases/security/encryption/always-encrypted-client-development.md)
- [Always Encrypted-Blog](https://blogs.msdn.microsoft.com/sqlsecurity/tag/always-encrypted/)



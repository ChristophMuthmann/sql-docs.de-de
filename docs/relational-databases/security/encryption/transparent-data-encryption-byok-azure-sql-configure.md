---
title: 'PowerShell und CLI: Aktivieren von SQL TDE mithilfe eines eigenen Azure Key Vault-Schlüssels | Microsoft-Dokumentation'
description: Erfahren Sie, wie Sie eine Azure SQL-Datenbank und Data Warehouse so konfigurieren, dass Sie Transparent Data Encryption (TDE) für die Verschlüsselung ruhender Daten mit PowerShell oder der CLI verwenden können.
keywords: ''
documentationcenter: ''
author: aliceku
manager: craigg
editor: ''
ms.prod: ''
ms.reviewer: ''
ms.suite: sql
ms.prod_service: sql-database, sql-data-warehouse
ms.service: sql-database
ms.component: security
ms.workload: On Demand
ms.tgt_pltfrm: ''
ms.devlang: azurecli, powershell
ms.topic: article
ms.date: 03/15/2018
ms.author: aliceku
ms.openlocfilehash: 9d1fee3a22bfa930f70a8c6e2585f60acaf5f419
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/21/2018
---
# <a name="powershell-and-cli-enable-transparent-data-encryption-using-your-own-key-from-azure-key-vault-preview"></a>PowerShell und CLI: Aktivieren von Transparent Data Encryption mithilfe eines eigenen Azure Key Vault-Schlüssels (Vorschauversion)

[!INCLUDE[appliesto-xx-asdb-asdw-xxx-md](../../../includes/appliesto-xx-asdb-asdw-xxx-md.md)]

In dieser Anleitung wird die Art und Weise erläutert, wie Sie einen Schlüssel aus Azure Key Vault für Transparent Data Encryption (TDE) in der Vorschauversion in SQL-Datenbank oder Data Warehouse verwenden können. Um mehr über die Unterstützung für TDE mit „Bring Your Own Key“ (BYOK) in der Vorschauversion zu erfahren, besuchen Sie die Seite [TDE Bring Your Own Key to Azure SQL (TDE mit Bring Your Own Key für Azure SQL)](transparent-data-encryption-byok-azure-sql.md). 

## <a name="prerequisites-for-powershell"></a>Voraussetzungen für PowerShell

- Sie müssen über ein Azure-Abonnement verfügen und Administrator für dieses Abonnement sein.
- [Empfohlen aber optional] Sie sollten ein Hardwaresicherheitsmodul (HSM) oder einen lokalen Schlüsselspeicher zum Erstellen einer lokalen Kopie des Schlüsselmaterials für den TDE-Schutz besitzen.
- Sie müssen eine Installation von Azure PowerShell Version 4.2.0 oder höher besitzen und diese ausführen. 
- Sie müssen einen Azure Key Vault-Schlüsseltresor und einen Schlüssel für die Verwendung für TDE erstellen.
   - [Erste Schritte mit Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-get-started)
   - [Instructions for using a hardware security module (HSM) and Key Vault (Anweisungen zur Verwendung eines Hardwaresicherheitsmodells (HSM) und Key Vault)](https://docs.microsoft.com/azure/key-vault/key-vault-get-started#a-idhsmaif-you-want-to-use-a-hardware-security-module-hsm)
- Der Schlüssel muss über folgende Attribute verfügen, um für TDE verwendet werden zu können:
   - Kein Ablaufdatum
   - Nicht deaktiviert
   - Muss die Operationen *get*, *wrap key* und *unwrap key* ausführen können

## <a name="step-1-assign-an-azure-ad-identity-to-your-server"></a>Schritt 1: Zuweisen einer Azure AD-Identität zu einem Server 

Wenn bereits ein Server vorhanden ist, können Sie diesem mit dem folgenden Code eine Azure AD-Identität hinzufügen:

   ```powershell
   $server = Set-AzureRmSqlServer `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> `
   -AssignIdentity
   ```

Wenn Sie einen Server erstellen, können Sie das Cmdlet [New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) mit dem Tag „-AssignIdentity“ verwenden, um eine Azure AD-Identität während der Servererstellung hinzuzufügen:

   ```powershell
   $server = New-AzureRmSqlServer `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -Location <RegionName> `
   -ServerName <LogicalServerName> `
   -ServerVersion "12.0" `
   -SqlAdministratorCredentials <PSCredential> `
   -AssignIdentity 
   ```

## <a name="step-2-grant-key-vault-permissions-to-your-server"></a>Schritt 2: Gewähren von Key Vault-Berechtigungen für Ihren Server

Verwenden Sie das Cmdlet [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy), um Ihrem Server Zugriff auf den Schlüsseltresor zu gewähren, bevor Sie von diesem einen Schlüssel für TDE verwenden.

   ```powershell
   Set-AzureRmKeyVaultAccessPolicy  `
   -VaultName <KeyVaultName> `
   -ObjectId $server.Identity.PrincipalId `
   -PermissionsToKeys get, wrapKey, unwrapKey
   ```

## <a name="step-3-add-the-key-vault-key-to-the-server-and-set-the-tde-protector"></a>Schritt 3: Hinzufügen eines Key Vault-Schlüssels zum Server und Festlegen des TDE-Schutzes

- Verwenden Sie das Cmdlet [Add-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/add-azurermsqlserverkeyvaultkey), um dem Server den Schlüssel aus Key Vault hinzuzufügen.
- Verwenden Sie das Cmdlet [Set-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/set-azurermsqlservertransparentdataencryptionprotector), um den Schlüssel als TDE-Schutz für alle Serverressourcen hinzuzufügen.
- Verwenden Sie das Cmdlet [Get-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/get-azurermsqlservertransparentdataencryptionprotector), um zu bestätigen, dass der TDE-Schutz wie geplant konfiguriert wurde.

> [!Note]
> Die kombinierte Länge für den Schlüsseltresornamen und Schlüsselnamen darf nicht über 94 Zeichen hinausgehen.
> 

>[!Tip]
>Beispiel für eine Schlüssel-ID von Key Vault: https://contosokeyvault.vault.azure.net/keys/Key1/1a1a2b2b3c3c4d4d5e5e6f6f7g7g8h8h
>

   ```powershell
   <# Add the key from Key Vault to the server #>
   Add-AzureRmSqlServerKeyVaultKey `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> `
   -KeyId <KeyVaultKeyId>

   <# Set the key as the TDE protector for all resources under the server #>
   Set-AzureRmSqlServerTransparentDataEncryptionProtector `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> `
   -Type AzureKeyVault `
   -KeyId <KeyVaultKeyId> 

   <# To confirm that the TDE protector was configured as intended: #>
   Get-AzureRmSqlServerTransparentDataEncryptionProtector `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> 
   ```

## <a name="step-4-turn-on-tde"></a>Schritt 4. Aktivieren von TDE 

Verwenden Sie das Cmdlet [Set-AzureRMSqlDatabaseTransparentDataEncryption](/powershell/module/azurerm.sql/set-azurermsqldatabasetransparentdataencryption), um TDE zu aktivieren.

   ```powershell
   Set-AzureRMSqlDatabaseTransparentDataEncryption `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> `
   -DatabaseName <DatabaseName> `
   -State "Enabled"
   ```

Nun verfügt die Datenbank oder Data Warehouse über aktivierte TDE-Technologie mit einem Verschlüsselungsschlüssel in Key Vault.

## <a name="step-5-check-the-encryption-state-and-encryption-activity"></a>Schritt 5. Überprüfen des Verschlüsselungsstatus und der Verschlüsselungsaktivität

Verwenden Sie [Get-AzureRMSqlDatabaseTransparentDataEncryption](/powershell/module/azurerm.sql/get-azurermsqldatabasetransparentdataencryption), um den Verschlüsselungsstatus aufzurufen, und [Get-AzureRMSqlDatabaseTransparentDataEncryptionActivity](/powershell/module/azurerm.sql/get-azurermsqldatabasetransparentdataencryptionactivity), um den Verschlüsselungsfortschritt für eine Datenbank oder Data Warehouse zu überprüfen.

   ```powershell
   # Get the encryption state
   Get-AzureRMSqlDatabaseTransparentDataEncryption `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> `
   -DatabaseName <DatabaseName> `

   <# Check the encryption progress for a database or data warehouse #>
   Get-AzureRMSqlDatabaseTransparentDataEncryptionActivity `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> `
   -DatabaseName <DatabaseName>  
   ```

## <a name="other-useful-powershell-cmdlets"></a>Andere nützliche PowerShell-Cmdlets

- Verwenden Sie das Cmdlet [Set-AzureRMSqlDatabaseTransparentDataEncryption](/powershell/module/azurerm.sql/set-azurermsqldatabasetransparentdataencryption), um TDE zu deaktivieren.

   ```powershell
   Set-AzureRMSqlDatabaseTransparentDataEncryption `
   -ServerName <LogicalServerName> `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -DatabaseName <DatabaseName> `
   -State "Disabled”
   ```
 
- Verwenden Sie das Cmdlet [Get-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/get-azurermsqlserverkeyvaultkey), um die Liste der Key Vault-Schlüssel zurückzugeben, die dem Server hinzugefügt wurden.

   ```powershell
   <# KeyId is an optional parameter, to return a specific key version #>
   Get-AzureRmSqlServerKeyVaultKey `
   -ServerName <LogicalServerName> `
   -ResourceGroupName <SQLDatabaseResourceGroupName>
   ```
 
- Verwenden Sie [Remove-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/remove-azurermsqlserverkeyvaultkey), um einen Key Vault-Schlüssel aus dem Server zu entfernen.

   ```powershell
   <# The key set as the TDE Protector cannot be removed. #>
   Remove-AzureRmSqlServerKeyVaultKey `
   -KeyId <KeyVaultKeyId> `
   -ServerName <LogicalServerName> `
   -ResourceGroupName <SQLDatabaseResourceGroupName>   
   ```
 
## <a name="troubleshooting"></a>Problembehandlung

Überprüfen Sie Folgendes, falls ein Problem auftritt:
- Überprüfen Sie, ob der Schlüsseltresor nicht gefunden werden kann, und stellen Sie mithilfe des Cmdlets [Get-AzureRmSubscription](/powershell/module/azurerm.profile/get-azurermsubscription) sicher, dass Sie sich im richtigen Abonnement befinden.

   ```powershell
   Get-AzureRmSubscription `
   -SubscriptionId <SubscriptionId>
   ```

- Wenn der neue Schlüssel dem Server nicht hinzugefügt oder nicht als TDE-Schutz aktualisiert werden kann, überprüfen Sie Folgendes:
   - Der Schlüssel darf kein Ablaufdatum haben.
   - Für den Schlüssel müssen die Operationen *get*, *wrap key* und *unwrap key* aktiviert sein.

## <a name="next-steps"></a>Nächste Schritte

- Erfahren Sie , wie Sie den TDE-Schutz eines Servers rotieren können, damit dieser den Sicherheitsanforderungen entspricht: [Rotate the Transparent Data Encryption protector Using PowerShell (Rotieren des Transparent Data Encryption-Schutzes mithilfe von PowerShell)](transparent-data-encryption-byok-azure-sql-key-rotation.md).
- Im Falle eines Sicherheitsrisikos, erfahren Sie unter [Remove a potentially compromised key (Entfernen eines möglicherweise kompromittierten Schlüssels)](transparent-data-encryption-byok-azure-sql-remove-tde-protector.md), wie Sie einen möglicherweise kompromittierten TDE-Schutz entfernen können. 

## <a name="prerequisites-for-cli"></a>Erforderliche Komponenten für die CLI

- Sie müssen über ein Azure-Abonnement verfügen und Administrator für dieses Abonnement sein.
- [Empfohlen aber optional] Sie sollten ein Hardwaresicherheitsmodul (HSM) oder einen lokalen Schlüsselspeicher zum Erstellen einer lokalen Kopie des Schlüsselmaterials für den TDE-Schutz besitzen.
- CLI 2.0 oder höhere Version. Wie Sie die neueste Version installieren und eine Verbindung mit Ihrem Azure-Abonnement herstellen, können Sie unter [Installieren und Konfigurieren der plattformübergreifenden Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest) nachlesen. 
- Sie müssen einen Azure Key Vault-Schlüsseltresor und einen Schlüssel für die Verwendung für TDE erstellen.
   - [Manage Key Vault using CLI 2.0 (Verwalten von Key Vault mithilfe der CLI 2.0)](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-manage-with-cli2)
   - [Instructions for using a hardware security module (HSM) and Key Vault (Anweisungen zur Verwendung eines Hardwaresicherheitsmodells (HSM) und Key Vault)](https://docs.microsoft.com/azure/key-vault/key-vault-get-started#a-idhsmaif-you-want-to-use-a-hardware-security-module-hsm)
- Der Schlüssel muss über folgende Attribute verfügen, um für TDE verwendet werden zu können:
   - Kein Ablaufdatum
   - Nicht deaktiviert
   - Muss die Operationen *get*, *wrap key* und *unwrap key* ausführen können
   
## <a name="step-1-create-a-server-and-assign-an-azure-ad-identity-to-your-server"></a>Schritt 1: Erstellen eines Servers und Zuweisen einer Azure AD-Identität zum Server
      ```cli
      # create server (with identity) and database
      az sql server create -n "ServerName" -g "ResourceGroupName" -l "westus" -u "cloudsa" -p "YourFavoritePassWord99@34" -I 
      az sql db create -n "DatabaseName" -g "ResourceGroupName" -s "ServerName" 
      ```

 
## <a name="step-2-grant-key-vault-permissions-to-your-server"></a>Schritt 2: Gewähren von Key Vault-Berechtigungen für Ihren Server
      ```cli
      # create key vault, key and grant permission
      az keyvault create -n "VaultName" -g "ResourceGroupName" 
      az keyvault key create -n myKey -p software --vault-name "VaultName" 
      az keyvault set-policy -n "VaultName" --object-id "ServerIdentityObjectId" -g "ResourceGroupName" --key-permissions wrapKey unwrapKey get list 
      ```

 
## <a name="step-3-add-the-key-vault-key-to-the-server-and-set-the-tde-protector"></a>Schritt 3: Hinzufügen eines Key Vault-Schlüssels zum Server und Festlegen des TDE-Schutzes
  
     ```cli
     # add server key and update encryption protector
      az sql server key create -g "ResourceGroupName" -s "ServerName" -t "AzureKeyVault" -u "FullVersionedKeyUri 
      az sql server tde-key update -g "ResourceGroupName" -s "ServerName" -t AzureKeyVault -u "FullVersionedKeyUri" 
      ```
  
  > [!Note]
> Die kombinierte Länge für den Schlüsseltresornamen und Schlüsselnamen darf nicht über 94 Zeichen hinausgehen.
> 

>[!Tip]
>Beispiel für eine Schlüssel-ID von Key Vault: https://contosokeyvault.vault.azure.net/keys/Key1/1a1a2b2b3c3c4d4d5e5e6f6f7g7g8h8h
>
  
## <a name="step-4-turn-on-tde"></a>Schritt 4. Aktivieren von TDE 
      ```cli
      # enable encryption
      az sql db tde create -n "DatabaseName" -g "ResourceGroupName" -s "ServerName" --status Enabled 
      ```

Nun verfügt die Datenbank oder Data Warehouse über aktivierte TDE-Technologie mit einem Verschlüsselungsschlüssel in Key Vault.

## <a name="step-5-check-the-encryption-state-and-encryption-activity"></a>Schritt 5. Überprüfen des Verschlüsselungsstatus und der Verschlüsselungsaktivität

     ```cli
      # get encryption scan progress
      az sql db tde show-activity -n "DatabaseName" -g "ResourceGroupName" -s "ServerName" 

      # get whether encryption is on or off
      az sql db tde show-configuration -n "DatabaseName" -g "ResourceGroupName" -s "ServerName" 

      ```

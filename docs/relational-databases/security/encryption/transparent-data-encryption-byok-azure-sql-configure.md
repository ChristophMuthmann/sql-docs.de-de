---
title: "PowerShell: Aktivieren von TDE mithilfe Ihres eigenen Azure Key Vault-Schlüssels | Microsoft-Dokumentation"
description: "Erfahren Sie, wie Sie eine Azure SQL-Datenbank und Data Warehouse konfigurieren können, um damit zu beginnen,Transparent Data Encryption (TDE) für die Verschlüsselung ruhender Daten mithilfe von PowerShell zu verwenden."
keywords: 
services: sql-database
documentationcenter: 
author: becczhang
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: security
ms.workload: Inactive
ms.tgt_pltfrm: 
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: rebeccaz
ms.translationtype: HT
ms.sourcegitcommit: 46b16dcf147dbd863eec0330e87511b4ced6c4ce
ms.openlocfilehash: cf8f46ab01c08e68fa22f65a4f86f4ff16f16ba3
ms.contentlocale: de-de
ms.lasthandoff: 09/05/2017

---


# <a name="powershell-enable-transparent-data-encryption-using-your-own-key-from-azure-key-vault"></a>PowerShell: Aktivieren von Transparent Data Encryption mithilfe Ihres eigenen Schlüssels aus Azure Key Vault

[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

Dieser Leitfaden zur Vorgehensweise erläutert die Art und Weise, wie Sie einen Schlüssel aus Azure Key Vault für Transparent Data Encryption (TDE) auf der SQL-Datenbank oder Data Warehouse verwenden können. Um mehr über die Unterstützung für TDE mit „Bring Your Own Key“ (BYOK) zu erfahren, besuchen Sie die Seite [TDE Bring Your Own Key to Azure SQL (TDE mit Bring Your Own Key für Azure SQL)](transparent-data-encryption-byok-azure-sql.md). 

## <a name="prerequisites"></a>Erforderliche Komponenten

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

## <a name="step-1-assign-an-aad-identity-to-your-server"></a>Schritt 1: Zuweisen einer AAD-Identität zu Ihrem Server 

Wenn Sie über einen vorhandenen Server verfügen, verwenden Sie folgenden Code, um Ihrem Server eine AAD-Identität hinzuzufügen.

   ```powershell
   $server = Set-AzureRmSqlServer `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> `
   -AssignIdentity
   ```

Wenn Sie einen Server erstellen, verwenden Sie das Cmdlet [New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) mit dem Tag „-Identity“, um eine AAD-Identität während der Servererstellung hinzuzufügen:

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

Verwenden Sie das Cmdlet [Set-AzureRmKeyValutAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy), um Ihrem Server Zugriff auf den Schlüsseltresor zu gewähren, bevor Sie davon einen Schlüssel für TDE verwenden.

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
>Eine Beispiel-Schlüssel-ID von Key Vault: https://contosokeyvault.vault.azure.net/keys/Key1/1a1a2b2b3c3c4d4d5e5e6f6f7g7g8h8h
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

## <a name="step-5-check-the-encryption-state-and-encryption-activity-of-the-database-or-data-warehouse"></a>Schritt 5. Überprüfen des Verschlüsselungsstatus und der Verschlüsselungsaktivität der Datenbank oder Data Warehouse

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




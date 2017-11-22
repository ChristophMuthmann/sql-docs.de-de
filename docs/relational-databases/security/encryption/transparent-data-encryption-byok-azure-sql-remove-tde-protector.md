---
title: Entfernen einer TDE-Schutzvorrichtung (PowerShell, Azure SQL) | Microsoft-Dokumentation
description: "Leitfaden für die Reaktion auf eine möglicherweise kompromittierte TDE-Schutzvorrichtung für Azure SQL-Datenbank oder Data Warehouse, die die BYOK-Unterstützung (Bring Your Own Key) für TDE verwendet."
keywords: 
services: sql-database
documentationcenter: 
author: becczhang
manager: craigg
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
ms.openlocfilehash: be2fd15b1f742d7edb01d39be69456c58d472801
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="remove-a-transparent-data-encryption-tde-protector-using-powershell"></a>Entfernen einer TDE-Schutzvorrichtung (Transparent Data Encryption) mithilfe von PowerShell
[!INCLUDE[appliesto-xx-asdb-xxxx-xxx-md](../../../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]

## <a name="prerequisites"></a>Erforderliche Komponenten
- Sie müssen über ein Azure-Abonnement verfügen und Administrator für dieses Abonnement sein.
- Sie müssen eine Installation von Azure PowerShell Version 4.2.0 oder höher besitzen und diese ausführen. 
- In diesem Leitfaden wird davon ausgegangen, dass Sie bereits einen Schlüssel von Azure Key Vault als TDE-Schutzvorrichtung für Azure SQL-Datenbank oder Data Warehouse verwenden. Weitere Informationen finden Sie unter [Transparent Data Encryption with BYOK Support (Transparente Datenverschlüsselung mit BYOK-Unterstützung)](transparent-data-encryption-byok-azure-sql.md).

## <a name="overview"></a>Übersicht
Dieser Leitfaden beschreibt, wie auf eine möglicherweise kompromittierte TDE-Schutzvorrichtung für Azure SQL-Datenbank oder Data Warehouse reagiert werden kann, die die BYOK-Unterstützung (Bring Your Own Key) für TDE verwendet. Weitere Informationen zur BYOK-Unterstützung für TDE finden Sie auf der [Übersichtsseite](transparent-data-encryption-byok-azure-sql.md). 

Die folgenden Verfahren sollten nur in Ausnahmefällen oder in Testumgebungen durchgeführt werden. Lesen Sie den Leitfaden sorgfältig, da das Löschen von aktiv verwendeten TDE-Schutzvorrichtungen aus Azure Key Vault zu **Datenverlust** führen kann. 

Wenn ein Schlüssel jemals unter Verdacht steht, kompromittiert zu sein, zum Beispiel durch unautorisierten Zugriff auf den Schlüssel durch einen Dienst oder Benutzer, ist es am besten, den Schlüssel zu löschen.

Beachten Sie, dass **alle Verbindungen zu den verschlüsselten Datenbanken auf dem Server blockiert und diese Datenbanken offline geschaltet und innerhalb von 24 Stunden gelöscht werden**, sobald die TDE-Schutzvorrichtung in Key Vault gelöscht wurde. Auf alte Sicherungen, die mit dem kompromittierten Schlüssel verschlüsselt sind, kann nicht mehr zugegriffen werden.

Dieser Leitfaden geht zwei Ansätze durch, je nachdem, welches Ergebnis nach der Reaktion auf Incidents gewünscht ist:
- Der **Zugriff** auf Azure SQL-Datenbanken bzw. Data Warehouses soll weiterhin möglich sein.
- Auf Azure SQL-Datenbanken bzw. Data Warehouses soll **kein Zugriff** mehr möglich sein.

## <a name="to-keep-the-encrypted-resources-accessible"></a>Zugriff auf die verschlüsselten Ressourcen weiterhin ermöglichen
1. Erstellen Sie einen [neuen Schlüssel in Key Vault](https://docs.microsoft.com/powershell/module/azurerm.keyvault/add-azurekeyvaultkey?view=azurermps-4.1.0). Stellen Sie sicher, dass der neue Schlüssel in einem separaten Schlüsseltresor der möglicherweise kompromittierte TDE-Schutzvorrichtung erstellt wird, da die Zugriffskontrolle auf Tresorebene bereitgestellt wird. 
2. Fügen Sie den neuen Schlüssel zum Server hinzu, indem Sie die Cmdlets [Add-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/add-azurermsqlserverkeyvaultkey) und [Set-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/set-azurermsqlservertransparentdataencryptionprotector) verwenden und diesen als neue TDE-Schutzvorrichtung des Servers aktualisieren.

   ```powershell
   # Add the key from Key Vault to the server  
   Add-AzureRmSqlServerKeyVaultKey `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> `
   -KeyId <KeyVaultKeyId>
   
   # Set the key as the TDE protector for all resources under the server
   Set-AzureRmSqlServerTransparentDataEncryptionProtector `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> `
   -Type AzureKeyVault -KeyId <KeyVaultKeyId> 
   ```

3. Stellen Sie sicher, dass der Server und alle Replikate auf die neue TDE-Schutzvorrichtung aktualisiert wurden, indem Sie das Cmdlet [Get-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/get-azurermsqlservertransparentdataencryptionprotector) verwenden. 

   >[!NOTE]
   > Es dauert möglicherweise ein paar Minuten, bis die neue TDE-Schutzvorrichtung sich auf alle Datenbanken und sekundären Datenbanken auf dem Server verteilt.
   >

   ```powershell
   Get-AzureRmSqlServerTransparentDataEncryptionProtector `
   -ServerName <LogicalServerName> `
   -ResourceGroupName <SQLDatabaseResourceGroupName>
   ```

4. Führen Sie eine [Sicherung des neuen Schlüssels](/powershell/module/azurerm.keyvault/backup-azurekeyvaultkey) in Key Vault durch.

   ```powershell
   <# -OutputFile parameter is optional; 
   if removed, a file name is automatically generated. #>
   Backup-AzureKeyVaultKey `
   -VaultName <KeyVaultName> `
   -Name <KeyVaultKeyName> `
   -OutputFile <DesiredBackupFilePath>
   ```
 
5. Löschen Sie den kompromittierten Schlüssel aus Key Vault, indem Sie das Cmdlet [Remove-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/remove-azurekeyvaultkey) verwenden. 

   ```powershell
   Remove-AzureKeyVaultKey `
   -VaultName <KeyVaultName> `
   -Name <KeyVaultKeyName>
   ```
 
6. Verwenden Sie das Cmdlet [Restore-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/restore-azurekeyvaultkey), um einen Schlüssel in Key Vault in Zukunft wiederherzustellen:
   ```powershell
   Restore-AzureKeyVaultKey `
   -VaultName <KeyVaultName> `
   -InputFile <BackupFilePath>
   ```
 
## <a name="to-make-the-encrypted-resources-inaccessible"></a>Zugriff auf die verschlüsselten Ressourcen verweigern
1. Löschen Sie die Datenbanken, die durch den möglicherweise kompromittierten Schlüssel verschlüsselt sind.
Die Datenbank- und Protokolldateien werden automatisch gesichert, sodass eine Zeitpunktwiederherstellung der Datenbank zu einem beliebigen Zeitpunkt durchgeführt werden kann (solange Sie den Schlüssel bereitstellen). Die Datenbanken müssen gelöscht werden, bevor eine aktive TDE-Schutzvorrichtung gelöscht wird, um einen möglichen Datenverlust von bis zu zehn Minuten der aktuellsten Transaktionen zu verhindern. 
2. Sichern Sie das Schlüsselmaterial der TDE-Schutzvorrichtung in Key Vault.
3. Entfernen Sie den möglicherweise kompromittierten Schlüssel aus Key Vault.

## <a name="next-steps"></a>Nächste Schritte

- Erfahren Sie , wie Sie die TDE-Schutzvorrichtung eines Servers rotieren können, damit dieser den Sicherheitsanforderungen entspricht: [Rotate the Transparent Data Encryption protector Using PowerShell (Rotieren des Transparent Data Encryption-Schutzes mithilfe von PowerShell)](transparent-data-encryption-byok-azure-sql-key-rotation.md).

- Erste Schritte mit der Bring Your Own Key-Unterstützung für TDE: [Turn on TDE using your own key from Key Vault using PowerShell (Aktivieren von TDE für das Verwenden Ihres eigenen Schlüssels von Key Vault mithilfe von PowerShell)](transparent-data-encryption-byok-azure-sql-configure.md)

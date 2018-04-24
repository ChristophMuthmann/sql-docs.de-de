---
title: PowerShell – Rotieren der TDE-Schutzvorrichtung – Azure SQL | Microsoft-Dokumentation
description: Erfahren Sie, wie Sie die Transparent Data Encryption-Schutzvorrichtung (TDE) für einen Server von Azure SQL Server rotieren können.
keywords: ''
services: sql-database
documentationcenter: ''
author: becczhang
manager: jhubbard
editor: ''
ms.prod: ''
ms.reviewer: ''
ms.suite: sql
ms.prod_service: sql-database, sql-data-warehouse
ms.service: sql-database
ms.custom: ''
ms.component: security
ms.workload: Inactive
ms.tgt_pltfrm: ''
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: ryzhang26
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 43784cd826223281f922a0165b0e742979ea2c47
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="rotate-the-transparent-data-encryption-tde-protector-using-powershell"></a>Rotieren einer Transparent Data Encryption-Schutzvorrichtung (TDE) mithilfe von PowerShell 
[!INCLUDE[appliesto-xx-asdb-asdw-xxx-md](../../../includes/appliesto-xx-asdb-asdw-xxx-md.md)]

Dieser Leitfaden zur Vorgehensweise beschreibt die Schlüsselrotation für einen Server von Azure SQL Server mithilfe einer TDE-Schutzvorrichtung von Azure Key Vault. Das Rotieren einer TDE-Schutzvorrichtung eines Servers von Azure SQL Server bedeutet, dass zu einem asymmetrischen Schlüssel gewechselt wird, der die Datenbanken auf einem Server schützt. Die Schlüsselrotation ist ein Onlinevorgang und sollte in ein paar Sekunden abgeschlossen sein, da dieser nur den Datenverschlüsselungsschlüssel der Datenbank entschlüsselt und wieder verschlüsselt und nicht die gesamte Datenbank.

Dieser Leitfaden erläutert zwei Optionen zum Rotieren der TDE-Schutzvorrichtung auf dem Server.

> [!NOTE]
> Ein angehaltener SQL Data Warehouse-Dienst muss vor den Schlüsselrotationen fortgesetzt werden.
>

> [!IMPORTANT]
> **Löschen Sie keine** vorherigen Versionen des Schlüssels nach einem Rollover.  Wenn die Schlüssel von neuem beginnen, sind einige Daten noch immer mit den vorherigen Schlüsseln verschlüsselt, z.B. ältere Datenbanksicherungen. 
>

## <a name="prerequisites"></a>Voraussetzungen

- In diesem Leitfaden wird davon ausgegangen, dass Sie bereits einen Schlüssel von Azure Key Vault als TDE-Schutzvorrichtung für Azure SQL-Datenbank oder Data Warehouse verwenden. Weitere Informationen finden Sie unter [Transparent Data Encryption with BYOK Support (Transparente Datenverschlüsselung mit BYOK-Unterstützung)](transparent-data-encryption-byok-azure-sql.md).
- Sie müssen eine Installation von Azure PowerShell Version 3.7.0 oder höher besitzen und diese ausführen. 
- [Empfohlen aber optional] Erstellen Sie das Schlüsselmaterial für die TDE-Schutzvorrichtung zunächst in einem Hardwaresicherheitsmodul (HSM) oder einem lokalen Schlüsselspeicher, und importieren Sie das Schlüsselmaterial in Azure Key Vault. Weiter Informationen erhalten Sie, wenn Sie die Anweisungen unter [Instructions for using a hardware security module (HSM) and Key Vault (Anweisungen zur Verwendung eines Hardwaresicherheitsmodells (HSM) und Key Vault)](https://docs.microsoft.com/azure/key-vault/key-vault-get-started) befolgen.

## <a name="option-1-auto-rotation"></a>Option 1: Automatische Rotation

Generieren Sie eine neue Version des vorhandenen Schlüssels der TDE-Schutzvorrichtung in Key Vault und zwar unter demselben Schlüsselnamen und im selben Schlüsseltresor. Der Azure SQL-Dienst verwendet die neue Version innerhalb von 24 Stunden. 

So erstellen Sie eine neue Version der TDE-Schutzvorrichtung mithilfe des Cmdlets [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey):

   ```powershell
   Add-AzureKeyVaultKey `
   -VaultName <KeyVaultName> `
   -Name <KeyVaultKeyName> `
   -Destination <HardwareOrSoftware>
   ```

## <a name="option-2-manual-rotation"></a>Option 2: Manuelle Rotation

Die Option verwendet die Cmdlets [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey), [Add-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/add-azurermsqlserverkeyvaultkey) und [Set-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/set-azurermsqlservertransparentdataencryptionprotector), um einen komplett neuen Schlüssel hinzuzufügen, der unter einem neuen Schlüsselnamen oder auch in einem anderen Schlüsseltresor gespeichert werden kann. 

>[!NOTE]
>Die kombinierte Länge für den Schlüsseltresornamen und Schlüsselnamen darf nicht über 94 Zeichen hinausgehen.
>

   ```powershell
   # Add a new key to Key Vault
   Add-AzureKeyVaultKey `
   -VaultName <KeyVaultName> `
   -Name <KeyVaultKeyName> `
   -Destination <HardwareOrSoftware>

   # Add the new key from Key Vault to the server
   Add-AzureRmSqlServerKeyVaultKey `
   -KeyId <KeyVaultKeyId> `
   -ServerName <LogicalServerName> `
   -ResourceGroup <SQLDatabaseResourceGroupName>   
  
   <# Set the key as the TDE protector for all resources 
   under the server #>
   Set-AzureRmSqlServerTransparentDataEncryptionProtector `
   -Type AzureKeyVault `
   -KeyId <KeyVaultKeyId> `
   -ServerName <LogicalServerName> `
   -ResourceGroup <SQLDatabaseResourceGroupName>
   ```
  
## <a name="other-useful-powershell-cmdlets"></a>Andere nützliche PowerShell-Cmdlets

- Verwenden Sie das Cmdlet [Set-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/set-azurermsqlservertransparentdataencryptionprotector), um die TDE-Schutzvorrichtung vom durch Microsoft verwalteten Modus in den BYOK-Modus zu ändern.

   ```powershell
   Set-AzureRmSqlServerTransparentDataEncryptionProtector `
   -Type AzureKeyVault `
   -KeyId <KeyVaultKeyId> `
   -ServerName <LogicalServerName> `
   -ResourceGroup <SQLDatabaseResourceGroupName>
   ```

- Verwenden Sie das Cmdlet [Set-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/set-azurermsqlservertransparentdataencryptionprotector), um die TDE-Schutzvorrichtung vom BYOK-Modus in den durch Microsoft verwalteten Modus zu ändern.

   ```powershell
   Set-AzureRmSqlServerTransparentDataEncryptionProtector `
   -Type ServiceManaged `
   -ServerName <LogicalServerName> `
   -ResourceGroup <SQLDatabaseResourceGroupName> 
   ``` 

## <a name="next-steps"></a>Nächste Schritte

- Im Falle eines Sicherheitsrisikos, erfahren Sie unter [Remove a potentially compromised key (Entfernen eines möglicherweise kompromittierten Schlüssels)](transparent-data-encryption-byok-azure-sql-remove-tde-protector.md), wie Sie eine möglicherweise kompromittierten TDE-Schutzvorrichtung entfernen können. 

- Erste Schritte mit der Bring Your Own Key-Unterstützung für TDE: [Turn on TDE using your own key from Key Vault using PowerShell (Aktivieren von TDE für das Verwenden Ihres eigenen Schlüssels von Key Vault mithilfe von PowerShell)](transparent-data-encryption-byok-azure-sql-configure.md).

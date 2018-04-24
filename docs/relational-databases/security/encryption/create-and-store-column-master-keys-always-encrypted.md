---
title: Erstellen und Speichern von Spaltenhauptschlüsseln (Always Encrypted) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/01/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: security
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-security
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 856e8061-c604-4ce4-b89f-a11876dd6c88
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 4a3923ed38a97873eeee88104118d06ce7825776
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="create-and-store-column-master-keys-always-encrypted"></a>Erstellen und Speichern von Spaltenhauptschlüsseln (Always Encrypted)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

*Spaltenhauptschlüssel* sind Schlüsselschutzschlüssel, die in Always Encrypted zur Verschlüsselung von Spaltenverschlüsselungsschlüsseln verwendet werden. Spaltenhauptschlüssel müssen in einem vertrauenswürdigen Schlüsselspeicher gespeichert werden. Die Schlüssel müssen für Anwendungen verfügbar sein, die Daten ver- oder entschlüsseln müssen. Auch Tools, die Always Encrypted konfigurieren und Always Encrypted-Schlüssel verwalten, müssen auf die Spaltenhauptschlüssel zugreifen können.

Dieser Artikel bietet ausführliche Informationen zum Auswählen eines Schlüsselspeichers und Erstellen von Spaltenhauptschlüsseln für Always Encrypted. Einen detaillierten Überblick finden Sie unter [Übersicht über die Schlüsselverwaltung für Always Encrypted](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md).

## <a name="selecting-a-key-store-for-your-column-master-key"></a>Auswählen eines Schlüsselspeichers für Ihren Spaltenhauptschlüssel

Always Encrypted unterstützt mehrere Schlüsselspeicher zum Speichern von Always Encrypted-Spaltenhauptschlüsseln. Die unterstützten Schlüsselspeicher richten sich danach, welchen Treiber und welche Version Sie verwenden.

Es gibt zwei allgemeine Kategorien von Schlüsselspeichern: *Lokale Schlüsselspeicher*und *Zentrale Schlüsselspeicher*.

###  <a name="local-or-centralized-key-store"></a>Lokaler oder zentraler Schlüsselspeicher?

* **Lokale Schlüsselspeicher** können nur von Anwendungen auf Computern verwendet werden, die den lokalen Schlüsselspeicher enthalten. Anders gesagt: Sie müssen den Schlüsselspeicher und den Schlüssel auf jedem Computer replizieren, auf dem Ihre Anwendung ausgeführt wird. Ein Beispiel eines lokalen Schlüsselspeichers ist der Windows-Zertifikatspeicher. Wenn Sie einen lokalen Schlüsselspeicher verwenden, müssen Sie sicherstellen, dass der Schlüsselspeicher auf jedem Computer vorhanden ist, der Ihre Anwendung hostet. Sie müssen auch sicherstellen, dass auf dem Computer die Spaltenhauptschlüssel gespeichert sind, die Ihre Anwendung für den Zugriff auf durch Always Encrypted geschützte Daten benötigt. Wenn Sie zum ersten Mal einen Spaltenhauptschlüssel bereitstellen oder den Schlüssel ändern (rotieren), müssen Sie sicherstellen, dass der Schlüssel auf allen Computern bereitgestellt wird, die Ihre Anwendung(en) hosten.

* **Zentrale Schlüsselspeicher** stellen Schlüssel für Anwendungen auf mehreren Computern bereit. Ein Beispiel eines zentralen Schlüsselspeichers ist [Azure Key Vault](https://azure.microsoft.com/services/key-vault/). Ein zentraler Schlüsselspeicher vereinfacht die Schlüsselverwaltung, weil Sie nicht mehrere Kopien Ihrer Spaltenhauptschlüssel auf mehreren Computern verwalten müssen. Sie müssen sicherstellen, dass Ihre Anwendungen so konfiguriert sind, dass sie eine Verbindung zum zentralen Schlüsselspeicher herstellen können.

### <a name="which-key-stores-are-supported-in-always-encrypted-enabled-client-drivers"></a>Welche Schlüsselspeicher werden in für Always Encrypted aktivierten Clienttreibern unterstützt?

Für Always Encrypted aktivierte Clienttreiber sind SQL Server-Clienttreiber, die über integrierte Unterstützung für die Einbindung von Always Encrypted in Ihre Clientanwendungen verfügen. Für Always Encrypted aktivierte Treiber enthalten einige integrierte Anbieter für beliebte Schlüsselspeicher. Beachten Sie, dass einige Treiber Ihnen die Implementierung und Registrierung eines benutzerdefinierten Speicheranbieters für Spaltenhauptschlüssel ermöglichen, sodass Sie einen beliebigen Schlüsselspeicher verwenden können, auch wenn kein integrierter Anbieter vorhanden ist. Bedenken Sie bei der Entscheidung zwischen einem integrierten und einem benutzerdefinierten Anbieter, dass ein integrierter Anbieter in der Regel weniger Änderungen an Ihren Anwendungen erfordert (in einigen Fällen muss nur eine Verbindungszeichenfolge für die Datenbank geändert werden).

Die verfügbaren integrierten Anbieter richten sich danach, welcher Treiber, welche Treiberversion und welches Betriebssystem ausgewählt werden.  Lesen Sie die Always Encrypted-Dokumentation für Ihren jeweiligen Treiber, um zu ermitteln, welche Schlüsselspeicher standardmäßig unterstützt werden und ob Ihr Treiber benutzerdefinierte Schlüsselspeicheranbieter unterstützt.

- [Entwickeln von Anwendungen unter Verwendung von Always Encrypted mit dem .NET Framework-Datenanbieter für SQL Server](../../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)


### <a name="supported-tools"></a>Unterstützte Tools

Sie können [SQL Server Management Studio](../../../ssms/sql-server-management-studio-ssms.md) und das [SQL Server PowerShell-Modul](https://blogs.technet.microsoft.com/dataplatforminsider/2016/06/30/sql-powershell-july-2016-update) verwenden, um Always Encrypted zu konfigurieren und Always Encrypted-Schlüssel zu verwalten. Eine Liste der von diesen Tools unterstützen Schlüsselspeicher finden Sie hier:

- [Konfigurieren von Always Encrypted mithilfe von SQL Server Management Studio](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md)
- [Konfigurieren von Always Encrypted mithilfe von PowerShell](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)


## <a name="creating-column-master-keys-in-windows-certificate-store"></a>Erstellen von Spaltenhauptschlüsseln im Windows-Zertifikatspeicher    

Ein Spaltenhauptschlüssel kann ein Zertifikat sein, das im Windows-Zertifikatspeicher gespeichert ist. Beachten Sie, dass ein für Always Encrypted aktivierter Treiber kein Ablaufdatum und keine Zertifizierungsstellenkette überprüft. Ein Zertifikat wird einfach als Schlüsselpaar verwendet, das aus einem öffentlichen und einem privaten Schlüssel besteht.

Ein Zertifikat muss folgende Anforderungen erfüllen, um als gültiger Spaltenhauptschlüssel verwendet werden zu können:
* Es muss sich um ein X.509-Zertifikat handeln.
* Es muss in einem der beiden Zertifikatspeicherorte gespeichert werden: *lokaler Computer* oder *aktueller Benutzer*. (Um ein Zertifikat im Zertifikatspeicherort des lokalen Computers zu erstellen, müssen Sie Administrator auf dem Zielcomputer sein.)
* Es muss einen privaten Schlüssel enthalten (die empfohlene Länge der Schlüssel im Zertifikat beträgt 2048 Bits oder mehr).
* Es muss für den Schlüsselaustausch erstellt worden sein.


Es gibt mehrere Möglichkeiten, ein Zertifikat zu erstellen, das als gültiger Spaltenhauptschlüssel fungiert – die einfachste Methode ist jedoch die Erstellung eines selbstsignierten Zertifikats.


### <a name="create-a-self-signed-certificate-using-powershell"></a>Erstellen eines selbstsignierten Zertifikats mithilfe von PowerShell

Verwenden Sie das Cmdlet [New-SelfSignedCertificate](https://technet.microsoft.com/library/hh848633.aspx) , um ein selbstsigniertes Zertifikat zu erstellen. Das folgende Beispiel zeigt, wie Sie ein Zertifikat generieren, das als Spaltenhauptschlüssel für Always Encrypted verwendet werden kann.

```
New-SelfSignedCertificate is a Windows PowerShell cmdlet that creates a self-signed certificate. The below examples show how to generate a certificate that can be used as a column master key for Always Encrypted.
$cert = New-SelfSignedCertificate -Subject "AlwaysEncryptedCert" -CertStoreLocation Cert:CurrentUser\My -KeyExportPolicy Exportable -Type DocumentEncryptionCert -KeyUsage KeyEncipherment -KeySpec KeyExchange -KeyLength 2048 

# To create a certificate in the local machine certificate store location you need to run the cmdlet as an administrator.
$cert = New-SelfSignedCertificate -Subject "AlwaysEncryptedCert" -CertStoreLocation Cert:LocalMachine\My -KeyExportPolicy Exportable -Type DocumentEncryptionCert -KeyUsage KeyEncipherment -KeySpec KeyExchange -KeyLength 2048
```

### <a name="create-a-self-signed-certificate-using-sql-server-management-studio-ssms"></a>Erstellen eines selbstsignierten Zertifikats in SQL Server Management Studio (SSMS)

Weitere Informationen finden Sie unter [Konfigurieren von Always Encrypted mithilfe von SQL Server Management Studio](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md).
Ein Schritt-für-Schritt-Tutorial, das SSMS verwendet und Always Encrypted-Schlüssel im Windows-Zertifikatspeicher speichert, finden Sie unter [Tutorial zum Always Encrypted-Assistenten (Windows-Zertifikatspeicher)](https://azure.microsoft.com/documentation/articles/sql-database-always-encrypted/).


### <a name="making-certificates-available-to-applications-and-users"></a>Verfügbarmachen von Zertifikaten für Anwendungen und Benutzer

Wenn es sich bei Ihrem Spaltenhauptschlüssel um ein Zertifikat handelt, das im Zertifikatspeicherort *lokaler Computer* gespeichert ist, müssen Sie das Zertifikat mit dem privaten Schlüssel exportieren. Anschließend müssen Sie es auf allen Computern importieren, auf denen Anwendungen gehostet werden, die Daten in verschlüsselten Spalten ver- oder entschlüsseln sollen, oder auf denen Tools für die Konfiguration von Always Encrypted und für die Verwaltung der Always Encrypted-Schlüssel verwendet werden. Außerdem muss jedem Benutzer eine Leseberechtigung für das im Zertifikatspeicherort des lokalen Computers gespeicherte Zertifikat gewährt werden, damit der Benutzer das Zertifikat als Spaltenhauptschlüssel verwenden kann.

Wenn es sich bei Ihrem Spaltenhauptschlüssel um ein Zertifikat handelt, das im Zertifikatspeicherort *aktueller Benutzer* gespeichert ist, müssen Sie das Zertifikat mit dem privaten Schlüssel exportieren. Anschließend müssen Sie es in den Zertifikatspeicherort des aktuellen Benutzers für alle Benutzerkonten importieren, mit denen Anwendungen ausgeführt werden, die Daten in verschlüsselten Spalten ver- oder entschlüsseln sollen, oder mit denen Tools für die Konfiguration von Always Encrypted und für die Verwaltung der Always Encrypted-Schlüssel verwendet werden (auf allen Computern, die diese Anwendungen/Tools enthalten). Es muss keine Berechtigung konfiguriert werden – nach dem Anmelden bei einem Computer kann ein Benutzer auf alle Zertifikate im Zertifikatspeicherort des aktuellen Benutzers zugreifen.

#### <a name="using-powershell"></a>PowerShell
Verwenden Sie die Cmdlets [Import-PfxCertificate](https://msdn.microsoft.com/library/hh848625.aspx) und [Export-PfxCertificate](https://msdn.microsoft.com/library/hh848635.aspx) , um ein Zertifikat zu importieren und zu exportieren.

#### <a name="using-microsoft-management-console"></a>Verwenden der Microsoft Management Console 

Um einem Benutzer die Berechtigung *Lesen* für ein im Zertifikatspeicherort des lokalen Computers gespeichertes Zertifikat zu gewähren, führen Sie die folgenden Schritte aus:

1.  Öffnen Sie eine Eingabeaufforderung, und geben Sie **mmc**ein.
2.  Klicken Sie in der MMC-Konsole im Menü **Datei** auf **Snap-In hinzufügen/entfernen**.
3.  Klicken Sie im Dialogfeld **Snap-In hinzufügen/entfernen** auf **Hinzufügen**.
4.  Klicken Sie im Dialogfeld **Eigenständiges Snap-In hinzufügen** auf **Zertifikate**, und klicken Sie dann auf **Hinzufügen**.
5.  Klicken Sie im Dialogfeld **Zertifikat-Snap-In** auf **Computerkonto**, und klicken Sie dann auf **Fertig stellen**.
6.  Klicken Sie im Dialogfeld **Eigenständiges Snap-In** hinzufügen auf **Schließen**.
7.  Klicken Sie im Dialogfeld **Snap-In hinzufügen/entfernen** auf **OK**.
8.  Finden Sie das Zertifikat im **Zertifikat-Snap-In** im Ordner  **Eigene Zertifikate**, klicken Sie mit der rechten Maustaste auf das Zertifikat, zeigen Sie auf **Alle Aufgaben**, und klicken Sie dann auf **Private Schlüssel verwalten**.
9.  Fügen Sie bei Bedarf im Dialogfeld **Sicherheit** die Leseberechtigung für ein Benutzerkonto hinzu.

## <a name="creating-column-master-keys-in-azure-key-vault"></a>Erstellen von Spaltenhauptschlüsseln in Azure Key Vault

Azure Key Vault hilft beim Schutz kryptografischer und geheimer Schlüssel und ist eine praktische Möglichkeit zum Speichern von Spaltenhauptschlüsseln für Always Encrypted, insbesondere, wenn Ihre Anwendungen in Azure gehostet werden. Um einen Schlüssel in [Azure Key Vault](https://azure.microsoft.com/documentation/articles/key-vault-get-started/)zu erstellen, benötigen Sie ein [Azure-Abonnement](https://azure.microsoft.com/free/) und einen Azure-Schlüsseltresor.

#### <a name="using-powershell"></a>PowerShell

Das folgende Beispiel erstellt einen neuen Azure-Schlüsseltresor und Schlüssel und gewährt dann Berechtigungen für den gewünschten Benutzer.

```
# Create a column master key in Azure Key Vault.
Login-AzureRmAccount
$SubscriptionId = "<Azure subscription ID>"
$resourceGroup = "<resource group name>"
$azureLocation = "<key vault location>"
$akvName = "<key vault name>"
$akvKeyName = "<column master key name>"
$azureCtx = Set-AzureRMContext -SubscriptionId $SubscriptionId # Sets the context for the below cmdlets to the specified subscription.
New-AzureRmResourceGroup –Name $resourceGroup –Location $azureLocation # Creates a new resource group - skip, if you desire group already exists.
New-AzureRmKeyVault -VaultName $akvName -ResourceGroupName $resourceGroup -Location $azureLocation -SKU premium # Creates a new key vault - skip if your vault already exists.
Set-AzureRmKeyVaultAccessPolicy -VaultName $akvName -ResourceGroupName $resourceGroup -PermissionsToKeys get, create, delete, list, update, import, backup, restore, wrapKey, unwrapKey, sign, verify -UserPrincipalName $azureCtx.Account
$akvKey = Add-AzureKeyVaultKey -VaultName $akvName -Name $akvKeyName -Destination HSM
```

#### <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)

Ein Schritt-für-Schritt-Tutorial, das SSMS verwendet und Always Encrypted-Schlüssel in einem Azure-Schlüsseltresor speichert, finden Sie unter [Tutorial zum Always Encrypted-Assistenten (Windows Key Vault)](https://azure.microsoft.com/documentation/articles/sql-database-always-encrypted-azure-key-vault).

### <a name="making-azure-key-vault-keys-available-to-applications-and-users"></a>Verfügbarmachen von Azure Key Vault-Schlüsseln für Anwendungen und Benutzer

Wenn Sie einen Azure Key Vault-Schlüssel als Spaltenhauptschlüssel verwenden, muss Ihre Anwendung sich in Azure authentifizieren, und die Identität Ihrer Anwendung muss über die folgenden Berechtigungen im Schlüsseltresor verfügen: *get*, *unwrapKey*und *verify*. 

Um Spaltenverschlüsselungsschlüssel bereitzustellen, die mit einem in Azure Key Vault gespeicherten Spaltenhauptschlüssel geschützt sind, benötigen Sie die Berechtigungen *get*, *unwrapKey*, *wrapKey*, *sign*und *verify* . Außerdem benötigen Sie zum Erstellen eines neuen Schlüssels in einem Azure-Schlüsseltresor die Berechtigung *create* . Zum Auflisten der Schlüsseltresorinhalte benötigen Sie die Berechtigung *list* .

#### <a name="using-powershell"></a>PowerShell

Um Benutzern und Anwendungen den Zugriff auf die tatsächlichen Schlüssel im Azure-Schlüsseltresor zu ermöglichen, müssen Sie die Tresorzugriffsrichtlinie ([Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx)) einrichten:

```
$vaultName = "<vault name>"
$resourceGroupName = "<resource group name>"
$userPrincipalName = "<user to grant access to>"
$clientId = "<client Id>"

# grant users permissions to the keys:
Set-AzureRmKeyVaultAccessPolicy -VaultName $vaultName -ResourceGroupName $resourceGroupName -PermissionsToKeys create,get,wrapKey,unwrapKey,sign,verify,list -UserPrincipalName $userPrincipalName
# grant applications permissions to the keys:
Set-AzureRmKeyVaultAccessPolicy  -VaultName $vaultName  -ResourceGroupName $resourceGroupName -ServicePrincipalName $clientId -PermissionsToKeys get,wrapKey,unwrapKey,sign,verify,list
```

## <a name="creating-column-master-keys-in-hardware-security-modules-using-cng"></a>Erstellen von Spaltenhauptschlüsseln in Hardwaresicherheitsmodulen mithilfe von CNG

Ein Spaltenhauptschlüssel für Always Encrypted kann in einem Schlüsselspeicher gespeichert werden, der die CNG-API (Cryptography Next Generation) implementiert. Bei dieser Art Speicher handelt sich in der Regel um ein Hardwaresicherheitsmodul (HSM). Ein HSM ist ein physisches Gerät, das digitale Schlüssel schützt und verwaltet und die kryptografische Verarbeitung bereitstellt. Hardwaresicherheitsmodule werden üblicherweise als Plug-In-Karte oder externes Gerät bereitgestellt, die bzw. das direkt an einen Computer (lokales HSM) oder einen Netzwerkserver angeschlossen wird.

Um ein HSM für Anwendungen auf einem bestimmten Computer verfügbar zu machen, muss ein Schlüsselspeicheranbieter (Key Storage Provider, KSP), der CNG implementiert, auf dem Computer installiert und konfiguriert werden. Ein Always Encrypted-Clienttreiber (ein Speicheranbieter für einen Spaltenhauptschlüssel innerhalb des Treibers) verwendet den KSP, um Spaltenverschlüsselungsschlüssel zu ver- und entschlüsseln, die mit dem im Schlüsselspeicher gespeicherten Spaltenhauptschlüssel geschützt sind.

Windows enthält den Softwareschlüsselspeicher-Anbieter von Microsoft – einen softwarebasierten KSP, den Sie zu Testzwecken verwenden können. Weitere Informationen finden Sie unter [CNG Key Storage Providers](https://msdn.microsoft.com/library/windows/desktop/bb931355.aspx)(CNG-Schlüsselspeicheranbieter).

### <a name="creating-column-master-keys-in-a-key-store-using-cngksp"></a>Erstellen von Spaltenhauptschlüsseln in einem Schlüsselspeicher mithilfe von CNG/KSP

Ein Spaltenhauptschlüssel sollte ein asymmetrischer Schlüssel sein (ein öffentliches/privates Schlüsselpaar), das den RSA-Algorithmus verwendet. Die empfohlene Schlüssellänge beträgt 2048 Bits oder mehr.

#### <a name="using-hsm-specific-tools"></a>Verwenden von HSM-spezifischen Tools
Lesen Sie die Dokumentation für Ihr HSM.

#### <a name="using-powershell"></a>PowerShell

Sie können .NET-APIs verwenden, um mithilfe von CNG in PowerShell einen Schlüssel in einem Schlüsselspeicher zu erstellen.


```
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
```

#### <a name="using-sql-server-management-studio"></a>Verwendung von SQL Server Management Studio

Weitere Informationen finden Sie unter [Bereitstellung von Spaltenhauptschlüsseln mithilfe von SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt757096.aspx#Anchor_2).


### <a name="making-cng-keys-available-to-applications-and-users"></a>Verfügbarmachen von CNG-Schlüsseln für Anwendungen und Benutzer

Informieren Sie sich in Ihrer HSM- und KSP-Dokumentation, wie Sie den KSP auf einem Computer konfigurieren und Anwendungen und Benutzern Zugriff auf das HSM gewähren.

## <a name="creating-column-master-keys-in-hardware-security-modules-using-capi"></a>Erstellen von Spaltenhauptschlüsseln in Hardwaresicherheitsmodulen mithilfe der CAPI

Ein Spaltenhauptschlüssel für Always Encrypted kann in einem Schlüsselspeicher gespeichert werden, der die Kryptografie-API (Cryptography API, CAPI) implementiert. Üblicherweise handelt es sich bei einem solchen Speicher um ein Hardwaresicherheitsmodul (HSM) – ein physisches Gerät, das digitale Schlüssel schützt und verwaltet und die kryptografische Verarbeitung bereitstellt. Hardwaresicherheitsmodule werden üblicherweise als Plug-In-Karte oder externes Gerät bereitgestellt, die bzw. das direkt an einen Computer (lokales HSM) oder einen Netzwerkserver angeschlossen wird.

Um ein HSM für Anwendungen auf einem bestimmten Computer verfügbar zu machen, muss ein Kryptografiedienstanbieter (Cryptography Service Provider, CSP), der die CAPI implementiert, auf dem Computer installiert und konfiguriert werden. Ein Always Encrypted-Clienttreiber (ein Speicheranbieter für einen Spaltenhauptschlüssel innerhalb des Treibers) verwendet den CSP, um Spaltenverschlüsselungsschlüssel zu ver- und entschlüsseln, die mit dem im Schlüsselspeicher gespeicherten Spaltenhauptschlüssel geschützt sind. Hinweis: die CAPI ist eine veraltete API. Wenn für Ihr HSM ein KSP verfügbar ist, sollten Sie diesen statt des CSP bzw. der CAPI verwenden.

Ein CSP muss den RSA-Algorithmus unterstützen, um mit Always Encrypted verwendet werden zu können.

Windows enthält die folgenden softwarebasierten (nicht durch ein HSM gesicherten) CSPs, die RSA unterstützen und zu Testzwecken verwendet werden können: Microsoft Enhanced RSA und AES Cryptographic Provider.

### <a name="creating-column-master-keys-in-a-key-store-using-capicsp"></a>Erstellen von Spaltenhauptschlüsseln in einem Schlüsselspeicher mithilfe von CAPI/CSP

Ein Spaltenhauptschlüssel sollte ein asymmetrischer Schlüssel sein (ein öffentliches/privates Schlüsselpaar), das den RSA-Algorithmus verwendet. Die empfohlene Schlüssellänge beträgt 2048 Bits oder mehr.

#### <a name="using-hsm-specific-tools"></a>Verwenden von HSM-spezifischen Tools
Lesen Sie die Dokumentation für Ihr HSM.

#### <a name="using-sql-server-management-studio-ssms"></a>Verwenden von SQL Server Management Studio (SSMS)
Informationen hierzu finden Sie im Abschnitt „Bereitstellen von Spaltenhauptschlüsseln“ des Artikels „Konfigurieren von Always Encrypted mithilfe von SQL Server Management Studio“.

 
### <a name="making-cng-keys-available-to-applications-and-users"></a>Verfügbarmachen von CNG-Schlüsseln für Anwendungen und Benutzer
Informieren Sie sich in der Dokumentation zu Ihrem HSM und CSP, wie Sie den CSP auf einem Computer konfigurieren und Anwendungen und Benutzern Zugriff auf das HSM gewähren.
 
 
## <a name="next-steps"></a>Next Steps  
  
- [Konfigurieren von Always Encrypted-Schlüsseln mithilfe von PowerShell](../../../relational-databases/security/encryption/configure-always-encrypted-keys-using-powershell.md)
- [Rotation von Always Encrypted-Schlüsseln mithilfe von PowerShell](../../../relational-databases/security/encryption/rotate-always-encrypted-keys-using-powershell.md)
- [Konfigurieren von Always Encrypted mithilfe von SQL Server Management Studio](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md)

  
## <a name="additional-resources"></a>Zusätzliche Ressourcen  

- [Overview of Key Management for Always Encrypted (Übersicht über die Schlüsselverwaltung für Always Encrypted)](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)
- [Always Encrypted (Datenbankmodul)](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Entwickeln von Anwendungen unter Verwendung von Always Encrypted mit dem .NET Framework-Datenanbieter für SQL Server](../../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)
- [Always Encrypted-Blog](https://blogs.msdn.microsoft.com/sqlsecurity/tag/always-encrypted/)
    


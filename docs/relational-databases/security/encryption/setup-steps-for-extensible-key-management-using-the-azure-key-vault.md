---
title: "Installationsschritte für die Erweiterbare Schlüsselverwaltung mit Azure Key Vault | Microsoft-Dokumentation"
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- EKM, with key vault setup
- SQL Server Connector, setup
- SQL Server Connector
ms.assetid: c1f29c27-5168-48cb-b649-7029e4816906
caps.latest.revision: 34
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 8b6ddedabeb826caf903701327b6b103666b2abb
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="setup-steps-for-extensible-key-management-using-the-azure-key-vault"></a>Installationsschritte für die Erweiterbare Schlüsselverwaltung mit Azure Key Vault.
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  In den folgenden Schritten wird die Installation und Konfiguration des [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Connectors für Azure Key Vault exemplarisch durchlaufen und vorgestellt.  
  
## <a name="before-you-start"></a>Vorbereitungen  
 Damit Sie Azure Key Vault mit Ihrem SQL Server verwenden können, müssen einige Voraussetzungen erfüllt sein:  
  
-   Sie müssen über ein Azure-Abonnement verfügen  
  
-   Installieren Sie die neueste [Azure PowerShell](https://azure.microsoft.com/en-us/documentation/articles/powershell-install-configure/) -Version (1.0.1 oder höher).  

-   Erstellen Sie ein Azure Active Directory  

-   Machen Sie sich mit den Grundlagen der EKM-Speicherung mithilfe von Azure Key Vault vertraut, indem Sie [Erweiterbare Schlüsselverwaltung mit Azure Key Vault &#40;SQL Server&#41;](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md) durcharbeiten.  

-   Überprüfen Sie, ob die für die ausgeführte SQL Server-Version geeignete Version der weitervertreibbaren Visual Studio C++-Komponente installiert ist:
  
SQL Server-Version  |Link zum Installieren der weitervertreibbaren Komponente    
---------|--------- 
2008, 2008 R2, 2012, 2014 | [Visual C++ Redistributable-Pakete für Visual Studio 2013](https://www.microsoft.com/download/details.aspx?id=40784)    
2016 | [Visual C++ Redistributable für Visual Studio 2015](https://www.microsoft.com/download/details.aspx?id=48145)    
 
  
## <a name="part-i-set-up-an-azure-active-directory-service-principal"></a>Teil I: Einrichten eines Azure Active Directory-Dienstprinzipals  
 Um SQL Server-Zugriffsberechtigungen auf Ihrem Azure Key Vault zu erteilen, benötigen Sie ein Dienstprinzipalkonto in Azure Active Directory (AAD).  
  
1.  Navigieren Sie zum [klassischen Azure-Portal](https://manage.windowsazure.com), und melden Sie sich an.  
  
2.  Registrieren Sie eine Anwendung bei Azure Active Directory. Ausführliche Schrittanleitungen zum Registrieren einer Anwendung finden Sie im Abschnitt **Get an identity for the application** (Erhalten einer Identität für die Anwendung) im [Azure Key Vault-Blogbeitrag](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/).  
  
3.  Kopieren Sie die **Client-ID** und den **geheimen Clientschlüssel** für einen späteren Schritt, in dem sie verwendet werden, um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Zugriff auf Ihren Schlüsseltresor zu erteilen.  
  
 ![EKM-Client-Id](../../../relational-databases/security/encryption/media/ekm-client-id.png "Ekm-Client-Id")  
  
 ![EKM-Schlüssel-Id](../../../relational-databases/security/encryption/media/ekm-key-id.png "Ekm-Schlüssel-Id")  
  
## <a name="part-ii-create-a-key-vault-and-key"></a>Teil II: Erstellen eines Schlüsseltresors und eines Schlüssels  
 Der hier erstellte Schlüsseltresor und Schlüssel werden vom SQL Server-Datenbankmodul zum Schutz des Verschlüsselungsschlüssels verwendet.  
  
> [!IMPORTANT]  
>  Das Abonnement, in dem der Schlüsseltresor erstellt wird, muss sich im gleichen standardmäßigen Azure Active Directory befinden, in dem der Azure Active Directory-Dienstprinzipal erstellt wurde. Wenn Sie ein anderes Active Directory als das standardmäßige Active Directory zum Erstellen eines Dienstprinzipals für den SQL Server-Connector verwenden möchten, müssen Sie das standardmäßige Active Directory in Ihrem Azure-Konto ändern, bevor Sie Ihren Schlüsseltresor erstellen. Weitere Informationen zum Ändern des standardmäßigen Active Directory in ein von Ihnen bevorzugtes Active Directory finden Sie in den [Häufig gestellten Fragen (FAQs)](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md#AppendixB)zum SQL Server-Connector.  
  
1.  **Öffnen Sie PowerShell, und melden Sie sich an**  
  
     Installieren und starten Sie die [neueste Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) -Version (1.0.1 oder höher). Melden Sie sich beim Azure-Konto mit dem folgenden Befehl an:  
  
    ```powershell  
    Login-AzureRmAccount  
    ```  
  
     Die Anweisung gibt Folgendes zurück:  
  
    ```  
    Environment           : AzureCloud  
    Account               : <account_name>  
    TenantId              : <tenant_id>  
    SubscriptionId        : <subscription_id>  
    CurrentStorageAccount :  
    ```  
  
    > [!NOTE]  
    >  Wenn Sie über mehrere Abonnements verfügen und ein bestimmtes zur Verwendung durch den Tresor angeben möchten, verwenden Sie `Get-AzureRmSubscription` , um die Abonnements anzuzeigen und `Select-AzureRmSubscription` , um das richtige Abonnement auszuwählen. Andernfalls sucht PowerShell standardmäßig ein Abonnement aus.  
  
2.  **Erstellen Sie eine neue Ressourcengruppe**  
  
     Alle mithilfe des Azure-Ressourcen-Managers erstellten Ressourcen müssen in Ressourcengruppen enthalten sein. Erstellen Sie eine Ressourcengruppe, die Ihren Schlüsseltresor aufnehmen soll. In diesem Beispiel wird `ContosoDevRG`verwendet. Wählen Sie Ihren eigenen **eindeutigen** Ressourcengruppen- und Schlüsseltresornamen, da alle Schlüsseltresornamen global eindeutig sind.  
  
    ```powershell  
    New-AzureRmResourceGroup -Name ContosoDevRG -Location 'East Asia'  
    ```  
  
     Die Anweisung gibt Folgendes zurück:  
  
    ```  
    ResourceGroupName: ContosoDevRG  
    Location         : eastasia  
    ProvisioningState: Succeeded  
    Tags             :   
    ResourceId       : /subscriptions/<subscription_id>/  
                        resourceGroups/ContosoDevRG  
    ```  
  
    > [!NOTE]  
    >  Verwenden Sie für den `-Location parameter`den `Get-AzureLocation` -Befehl, um zu ermitteln, wie Sie einen alternativen Speicherort zu dem in diesem Beispiel verwendeten Speicherort angeben können. Falls Sie weitere Informationen benötigen, geben Sie Folgendes ein: `Get-Help Get-AzureLocation`  
  
3.  **Erstellen Sie einen Schlüsseltresor**  
  
     Das `New-AzureRmKeyVault` -Cmdlet benötigt einen Ressourcengruppennamen, einen Schlüsseltresornamen und einen geografischen Standort. Geben Sie z. B. für einen Schlüsseltresor mit dem Namen `ContosoDevKeyVault`Folgendes ein:  
  
    ```powershell  
    New-AzureRmKeyVault -VaultName 'ContosoDevKeyVault' `  
       -ResourceGroupName 'ContosoDevRG' -Location 'East Asia'  
    ```  
  
     Notieren Sie den Namen Ihres Schlüsseltresors.  
  
     Die Anweisung gibt Folgendes zurück:  
  
    ```  
    Vault Name                       : ContosoDevKeyVault  
    Resource Group Name              : ContosoDevRG  
    Location                         : East Asia  
    ResourceId                       : /subscriptions/<subscription_id>/  
                                        resourceGroups/ContosoDevRG/providers/  
                                        Microsoft/KeyVault/vaults/ContosoDevKeyVault  
    Vault URI: https://ContosoDevKeyVault.vault.azure.net  
    Tenant ID                        : <tenant_id>  
    SKU                              : Standard  
    Enabled For Deployment?          : False  
    Enabled For Template Deployment? : False  
    Enabled For Disk Encryption?     : False  
    Access Policies                  :  
             Tenant ID              : <tenant_id>  
             Object ID              : <object_id>  
             Application ID         :   
             Display Name           : <display_name>  
             Permissions to Keys    : get, create, delete, list, update, import,   
                                      backup, restore  
             Permissions to Secrets : all  
    Tags                             :  
    ```  
  
4.  **Erteilen Sie dem Azure Active Directory-Dienstprinzipal die Berechtigung zum Zugriff auf den Schlüsseltresor**  
  
     Sie können andere Benutzer und andere Anwendungen autorisieren, Ihren Schlüsseltresor zu verwenden.   
    Nutzen wir im Rahmen dieses Beispiels den in Teil I erstellten Azure Active Directory-Dienstprinzipal zum Autorisieren der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Instanz.  
  
    > [!IMPORTANT]  
    >  Der Azure Active Directory-Dienstprinzipal benötigt mindestens die Berechtigungen `get`, `list`, `wrapKey`und `unwrapKey` für den Schlüsseltresor.  
  
     Verwenden Sie die **Client-ID** aus Teil I für den `ServicePrincipalName` -Parameter, wie unten dargestellt. Die `Set-AzureRmKeyVaultAccessPolicy` wird lautlos ausgeführt und gibt bei erfolgreicher Ausführung keinen Wert zurück.  
  
    ```powershell  
    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoDevKeyVault'`  
      -ServicePrincipalName EF5C8E09-4D2A-4A76-9998-D93440D8115D `  
      -PermissionsToKeys get, list, wrapKey, unwrapKey  
    ```  
  
     Rufen Sie das `Get-AzureRmKeyVault` -Cmdlet auf, um die Berechtigungen zu bestätigen. In der Ausgabe der Anweisung sollten Sie unter „Zugriffsrichtlinien“ den Namen Ihrer AAD-Anwendung als weiteren Mandanten finden, der Zugriff auf diesen Schlüsseltresor hat.  
  
       
5.  **Erstellen Sie einen asymmetrischen Schlüssel im Schlüsseltresor**  
  
     Es gibt zwei Möglichkeiten, einen Schlüssel in Azure Key Vault zu erstellen: 1) Importieren eines vorhandenes Schlüssels oder 2) Erstellen eines neuen Schlüssels.  

    ### <a name="best-practice"></a>Bewährte Methode:
    
    Es wird die folgende bewährte Methode empfohlen, um die schnelle Wiederherstellung von Schlüsseln sicherzustellen und den Zugriff auf Ihre Daten außerhalb von Azure zu ermöglichen:
 
    1. Erstellen Sie Ihren Verschlüsselungsschlüssel lokal auf einem lokalen HSM-Gerät. (Stellen Sie sicher, dass dies ein asymmetrischer RSA-2048-Schlüssel ist, damit er in Azure Key Vault gespeichert werden kann.)
    2. Importieren Sie den Verschlüsselungsschlüssel in Azure Key Vault. Informationen zur Vorgehensweise finden Sie unter den folgenden Schritten.
    3. Bevor Sie den Schlüssel zum ersten Mal in Azure Key Vault verwenden, erstellen Sie eine Azure Key Vault-Schlüsselsicherung. Erhalten Sie weitere Informationen zum Befehl [Backup-AzureKeyVaultKey](https://msdn.microsoft.com/library/mt126292.aspx) .
    4. Sobald Änderungen am Schlüssel vorgenommen werden (z. B. durch Hinzufügen von ACLs, Tags oder Schlüsselattributen), müssen Sie sicherstellen, dass Sie eine weitere Azure Key Vault-Schlüsselsicherung erstellen.

        > [!NOTE]  
        >  Die Sicherung eines Schlüssels ist ein Azure Key Vault-Schlüsselvorgang, der eine Datei zurückgibt, die an einer beliebigen Stelle gespeichert werden kann.

    ### <a name="types-of-keys"></a>Schlüsselarten:
    Es gibt zwei Arten von Schlüsseln, die in Azure Key Vault generiert werden können. Bei beiden handelt es sich um asymmetrische 2048-Bit-RSA-Schlüssel.  
  
    -   **Softwaregeschützt:** In Software verarbeitet und in Ruhezeiten verschlüsselt. Vorgänge für softwaregeschützte Schlüssel erfolgen auf virtuellen Azure-Computern. Für Schlüssel empfohlen, die nicht in einer Produktionsumgebung verwendet werden.  
  
    -   **HSM-geschützt** : Von einem Hardwaresicherheitsmodul (HSM) erstellt und geschützt, um zusätzliche Sicherheit zu erzielen. Die Kosten liegen bei ungefähr 1 $ pro Schlüsselversion.  
  
        > [!IMPORTANT]  
        >  Für den SQL Server-Connector ist es erforderlich, dass im Schlüsselnamen nur die Zeichen „a-z“, „A-Z“, „0-9“ und „-“ bei einem Zeichenlimit von 26 Zeichen verwendet werden.   
        > Verschiedene Schlüsselversionen unter dem gleichen Schlüsselnamen in Azure Key Vault funktionieren in Verbindung mit dem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Connector nicht. Informationen zur rotierenden Verwendung eines Azure Key Vault-Schlüssels, der von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]verwendet wird, finden Sie in den Schritten zum Schlüsselrollover unter [SQL Server-Connector – Verwaltung und Problembehandlung](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md)durcharbeiten.  

    ### <a name="import-an-existing-key"></a>Importieren eines vorhandenen Schlüssels   
  
    Wenn Sie über einen vorhandenen softwaregeschützten 2048-Bit-RSA-Schlüssel verfügen, können Sie den Schlüssel in den Azure Key Vault hochladen. Wenn beispielsweise eine PFX-Datei auf Ihrem Laufwerk `C:\\` in einer Datei mit dem Namen `softkey.pfx` gespeichert ist, die Sie in den Azure Key Vault hochladen möchten, geben Sie Folgendes ein, um die Variable `securepfxpwd` für das Kennwort `12987553` für die PFX-Datei festzulegen:  
  
    ``` powershell  
    $securepfxpwd = ConvertTo-SecureString –String '12987553' `  
      –AsPlainText –Force  
    ```  
  
    Anschließend können Sie Folgendes eingeben, um den Schlüssel aus der PFX-Datei, die ihn durch die Hardware schützt (empfohlen), in den Schlüsseltresordienst zu importieren:  
  
    ``` powershell  
        Add-AzureKeyVaultKey -VaultName 'ContosoKeyVault' `  
          -Name 'ContosoFirstKey' -KeyFilePath 'c:\softkey.pfx' `  
          -KeyFilePassword $securepfxpwd $securepfxpwd  -Destination 'HSM'  
    ```  
 
    > [!IMPORTANT]  
    > Das Importieren des asymmetrischen Schlüssels wird für Produktionsszenarien dringend empfohlen, da der Administrator dann den Schlüssel in einem Schlüsselhinterlegungssystem hinterlegen kann. Wenn der asymmetrische Schlüssel im Tresor erstellt wird, kann er nicht hinterlegt werden, da der private Schlüssel nie den Tresor verlassen kann. Schlüssel zum Schützen wichtiger Daten sollten hinterlegt werden. Der Verlust eines asymmetrischen Schlüssels führt dazu, dass Daten dauerhaft nicht wiederhergestellt werden können.  

    ### <a name="create-a-new-key"></a>Erstellen eines neuen Schlüssels

    ##### <a name="example"></a>Beispiel:  
    Sie können bei Bedarf einen neuen Verschlüsselungsschlüssel direkt in Azure Key Vault erstellen und ihn per Software oder HSM schützen lassen. In diesem Beispiel erstellen wir einen softwaregeschützten Schlüssel mithilfe des `Add-AzureKeyVaultKey cmdlet`:  

    ``` powershell  
    Add-AzureKeyVaultKey -VaultName 'ContosoDevKeyVault' `  
      -Name 'ContosoRSAKey0' -Destination 'Software'  
    ```  
  
    Die Anweisung gibt Folgendes zurück:  
  
    ```  
    Attributes : Microsoft.Azure.Commands.KeyVault.Models.KeyAttributes  
    Key        :  {"kid":"https:contosodevKeyVault.azure.net/keys/  
                   ContosoRSAKey0/<guid>","dty":"RSA:,"key_ops": ...  
    VaultName  : contosodevkeyvault  
    Name       : contosoRSAKey0  
    Version    : <guid>  
    Id         : https://contosodevkeyvault.vault.azure.net:443/  
                 keys/ContosoRSAKey0/<guid>  
    ```  

    > [!IMPORTANT]  
    >  Der Schlüsseltresor unterstützt mehrere Versionen eines Schlüssels unter dem gleichen Namen, für vom [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Connector verwendete Schlüssel sollte aber weder Versionierung noch Rollover ausgeführt werden. Wenn der Administrator den Schlüssel für die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Verschlüsselung wieder verwenden möchte, sollte ein neuer Schlüssel mit einem anderen Namen im Tresor erstellt und zum Verschlüsseln des Datenverschlüsselungsschlüssels verwendet werden.  
   
  
## <a name="part-iii-install-the-includessnoversionincludesssnoversion-mdmd-connector"></a>Teil III: Installieren des [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Connectors  
 Laden Sie den SQL Server-Connector aus dem [Microsoft Download Center](http://go.microsoft.com/fwlink/p/?LinkId=521700)herunter. (Dies sollte vom Administrator des [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Computers ausgeführt werden.)  

> [!NOTE]  
>  Die Versionen 1.0.0.440 und älter wurden ersetzt und werden in Produktionsumgebungen nicht mehr unterstützt. Führen Sie ein Upgrade auf Version 1.0.1.0 oder höher durch, indem Sie das [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=45344) besuchen und die Anweisungen auf der Seite [SQL Server-Connector – Verwaltung und Problembehandlung](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md) unter „Upgrade des SQL Server-Connectors“ ausführen.
  
 ![EKM-Connector-Installation](../../../relational-databases/security/encryption/media/ekm-connector-install.png "Ekm-Connector-Installation")  
  
 Standardmäßig wird der Connector hier installiert: C:\Programme\SQL Server Connector for Microsoft Azure Key Vault. Dieser Speicherort kann während des Setups geändert werden. (Wenn Sie ihn ändern, passen Sie die unten angegebenen Skripts entsprechend an.)  
  
 Der Connector hat keine Benutzeroberfläche, doch wenn er erfolgreich installiert wurde, befindet sich die Datei **Microsoft.AzureKeyVaultService.EKM.dll** auf dem Computer. Dies ist die DLL des EKM-Kryptografieanbieters, die bei [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mithilfe der `CREATE CRYPTOGRAPHIC PROVIDER` -Anweisung registriert werden muss.  
  
 Die SQL Server-Connectorinstallation ermöglicht außerdem den Download von Beispieldateien für die SQL Server-Verschlüsselung.  
  
 Fehlercodeerläuterungen, Konfigurationseinstellungen oder Wartungsaufgaben für SQL Server-Connector finden Sie im Anhang unten in diesem Thema:  
  
-   [A. Wartungsanweisungen für SQL Server-Connector](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md#AppendixA)  
  
-   [C. Fehlercodeerläuterungen für SQL Server-Connector](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md#AppendixC)  
  
  
## <a name="part-iv-configure-includessnoversionincludesssnoversion-mdmd"></a>Teil IV: Konfigurieren [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
 Einen Hinweis zu den mindestens erforderlichen Berechtigungsstufen für jede Aktion in diesem Abschnitt finden Sie unter [B. Häufig gestellte Fragen (FAQ)](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md#AppendixB) .  
  
1.  **Starten Sie „sqlcmd.exe“ oder [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Studio**  
  
2.  **Konfigurieren Sie [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] für die Verwendung von EKM**  
  
     Führen Sie das folgende [!INCLUDE[tsql](../../../includes/tsql-md.md)] -Skript aus, um das [!INCLUDE[ssDE](../../../includes/ssde-md.md)] für die Verwendung eines EKM-Anbieters zu konfigurieren.  
  
    ```tsql  
    -- Enable advanced options.  
    USE master;  
    GO  
  
    sp_configure 'show advanced options', 1;  
    GO  
    RECONFIGURE;  
    GO  
  
    -- Enable EKM provider  
    sp_configure 'EKM provider enabled', 1;  
    GO  
    RECONFIGURE;  
    ```  
  
3.  **Registrieren (erstellen) Sie den [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Connector als EKM-Anbieter bei [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]**  
  
     Erstellen Sie einen Kryptografieanbieter mithilfe des [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Connectors, der einen EKM-Anbieter für den Azure Key Vault darstellt.    
    In diesem Beispiel wird der Name `AzureKeyVault_EKM_Prov`verwendet.  
  
    ```tsql  
    CREATE CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov   
    FROM FILE = 'C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\Microsoft.AzureKeyVaultService.EKM.dll';  
    GO  
    ```  
  
    > [!NOTE]  
    >  Der Dateipfad darf höchstens 256 Zeichen umfassen.  
  
  
4.  **Richten Sie eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Anmeldeinformation für eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Anmeldung zur Verwendung des Schlüsseltresors ein**  
  
     Für jede Anmeldung, die Verschlüsselung mithilfe eines Schlüssels aus dem Schlüsseltresor ausführen soll, müssen Anmeldeinformationen erstellt werden. Dazu können beispielsweise gehören:  
  
    -   Eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Administratoranmeldung, die den Schlüsseltresor verwenden soll, um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Verschlüsselungsszenarien einzurichten und zu verwalten.  
  
    -   Andere [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Anmeldungen, die möglicherweise die transparente Datenverschlüsselung (Transparent Data Encryption, TDE) oder andere [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Verschlüsselungsfunktionen aktivieren.  
  
     Es besteht eine Eins-zu-Eins-Zuordnung zwischen Anmeldeinformationen und Anmeldungen. Da heißt, für jede Anmeldung müssen eindeutige Anmeldeinformationen vorhanden sein.  
  
     Ändern Sie das [!INCLUDE[tsql](../../../includes/tsql-md.md)] -Skript unten in der folgenden Weise:  
  
    -   Bearbeiten Sie das `IDENTITY` -Argument (`ContosoDevKeyVault`), damit es auf Ihren Azure Key Vault verweist.
        - Wenn Sie eine **öffentliche Azure-Cloud**verwenden, ersetzen Sie das `IDENTITY` -Argument durch den Namen Ihres Azure Key Vault aus Teil II.
        - Wenn Sie eine **private Azure-Cloud** verwenden (z. B. Azure für Behörden, Azure China oder Azure Deutschland), ersetzen Sie das `IDENTITY` -Argument durch den Tresor-URI, der in Teil II, Schritt 3 zurückgegeben wird. Schließen Sie „https://“ nicht in den Tresor-URI ein.   
    -   Ersetzen Sie den ersten Teil des `SECRET` -Arguments durch die Azure Active Directory- **Client-ID** aus Teil I. In diesem Beispiel ist die **Client-ID** `EF5C8E094D2A4A769998D93440D8115D`.  
  
        > [!IMPORTANT]  
        >  Bindestriche müssen aus der **Client-ID**entfernt werden.  
  
    -   Setzen Sie in den zweiten Teil des `SECRET` -Arguments den **geheimen Clientschlüssel** aus Teil I ein. In diesem Beispiel ist der **geheime Clientschlüssel** aus Teil I `Replace-With-AAD-Client-Secret`. Die endgültige Zeichenfolge für das `SECRET`-Argument ist eine lange Abfolge von Buchstaben und Ziffern *ohne Bindestriche*.  
  
    ```tsql  
    USE master;  
    CREATE CREDENTIAL sysadmin_ekm_cred   
        WITH IDENTITY = 'ContosoDevKeyVault', -- for public Azure
        -- WITH IDENTITY = 'ContosoDevKeyVault.vault.usgovcloudapi.net', -- for Azure Government
        -- WITH IDENTITY = 'ContosoDevKeyVault.vault.azure.cn', -- for Azure China
        -- WITH IDENTITY = 'ContosoDevKeyVault.vault.microsoftazure.de', -- for Azure Germany   
        SECRET = 'EF5C8E094D2A4A769998D93440D8115DReplace-With-AAD-Client-Secret'   
    FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov;  
  
    -- Add the credential to the SQL Server administrator's domain login   
    ALTER LOGIN [<domain>\<login>]  
    ADD CREDENTIAL sysadmin_ekm_cred;  
    ```  
  
     Ein Beispiel für die Verwendung von Variablen für die **CREATE CREDENTIAL**-Argumente und die programmgesteuerte Entfernung der Bindestriche aus der Client-ID finden Sie unter [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md).  
  
5.  **Öffnen Sie in Ihren Azure Key Vault-Schlüssel in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]**  
  
     Wenn Sie einen asymmetrischen Schlüssel importiert haben, wie in Teil II beschrieben, öffnen Sie den Schlüssel, indem Sie Ihren Schlüsselnamen im folgenden [!INCLUDE[tsql](../../../includes/tsql-md.md)] -Skript angeben.  
  
    -   Ersetzen Sie `CONTOSO_KEY` durch den Namen, den der Schlüssel in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]haben soll.  
  
    -   Ersetzen Sie `ContosoRSAKey0` durch den Namen Ihres Schlüssels im Azure Key Vault.  
  
    ```tsql  
    CREATE ASYMMETRIC KEY CONTOSO_KEY   
    FROM PROVIDER [AzureKeyVault_EKM_Prov]  
    WITH PROVIDER_KEY_NAME = 'ContosoRSAKey0',  
    CREATION_DISPOSITION = OPEN_EXISTING;  
    ```  
## <a name="next-step"></a>Nächster Schritt  
  
Jetzt, da Sie die Grundkonfiguration abgeschlossen haben, erfahren Sie mehr zum [Verwenden von SQL Server-Connector mit SQL-Verschlüsselungsfunktionen](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md)   
  
## <a name="see-also"></a>Siehe auch  
 [Erweiterbare Schlüsselverwaltung mit Azure Key Vault](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)   
[SQL Server-Connector – Verwaltung und Problembehandlung](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md)  
  
  


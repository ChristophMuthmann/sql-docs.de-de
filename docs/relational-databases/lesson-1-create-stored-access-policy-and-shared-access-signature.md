---
title: 'Lektion 1: Erstellen einer gespeicherten Zugriffsrichtlinie und SAS | Microsoft-Dokumentation'
ms.custom:
- SQL2016_New_Updated
ms.date: 06/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: 41674d9d-8132-4bff-be4d-85a861419f3d
caps.latest.revision: 22
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: On Demand
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f2c8af4701b9a01ee21613fe7e093a89f1d8f990
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="lesson-1-create-stored-access-policy-and-shared-access-signature"></a>Lektion 1: Erstellen einer gespeicherten Zugriffsrichtlinie und SAS
In dieser Lektion verwenden Sie ein [Azure PowerShell](https://azure.microsoft.com/en-us/documentation/articles/powershell-install-configure/) -Skript zum Erstellen einer SAS für einen Azure-Blobcontainer mithilfe einer gespeicherten Zugriffsrichtlinie.  
  
> [!NOTE]  
> Dieses Skript wurde mit Azure PowerShell 5.0.10586 geschrieben.  
  
Eine SAS ist ein URI, der eingeschränkte Zugriffsrechte für Container, Blobs, Warteschlangen oder Tabellen gewährt. Eine gespeicherte Zugriffsrichtlinie stellt eine zusätzliche Steuerungsebene für Shared Access Signatures auf Serverseite bereit, einschließlich das Aufheben, Ablaufen oder Erweitern des Zugriffs. Wenn Sie diese neue Erweiterung verwenden, müssen Sie eine Richtlinie für einen Container mit mindestens Lese-, Schreib- und Auflistungsrechten erstellen.  
  
Sie können eine gespeicherte Zugriffsrichtlinie und eine SAS mithilfe von Azure PowerShell, mithilfe des Azure Storage SDKs, der Azure-REST-API oder einem Hilfsprogramm von Drittanbietern erstellen. Dieses Tutorial veranschaulicht, wie ein Azure PowerShell-Skript verwendet wird, um diesen Vorgang abzuschließen. Das Skript verwendet das Bereitstellungsmodell des Ressourcen-Managers und erstellt die nachstehenden neuen Ressourcen.  
  
-   Ressourcengruppe  
  
-   Speicherkonto  
  
-   Azure-Blobcontainer  
  
-   SAS-Richtlinie  
  
Dieses Skript beginnt mit der Deklarierung einer Reihe von Variablen, um die Namen für die oben genannten Ressourcen und die Namen der folgenden erforderlichen Eingabewerte anzugeben:  
  
-   Ein Präfixname, der zur Benennung von anderen Ressourcenobjekten verwendet wird  
  
-   Abonnementname  
  
-   Standort des Rechenzentrums  
  
> [!NOTE]  
> Dieses Skript wird so geschrieben, dass Sie entweder die vorhandenen Ressourcen des Azure Ressourcen-Managers oder eines klassischen Bereitstellungsmodells verwenden können.  
  
Das Skript wird durch die Generierung der erforderlichen CREATE CREDENTIAL-Anweisung abgeschlossen, die Sie in [Lektion 2: Erstellen von SQL Server-Anmeldeinformationen mit einer Shared Access Signature (SAS)](../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)verwenden werden. Diese Anweisung wird für Sie in die Zwischenablage kopiert und wird an der Konsole ausgegeben, damit Sie sie anzeigen können.  
  
Befolgen Sie folgende Schritte, um eine Richtlinie für einen Container zu erstellen und einen SAS-Schlüssel zu erstellen:  
  
1.  Öffnen Sie Windows PowerShell oder Windows PowerShell ISE (siehe oben genannte Versionsanforderungen).  
  
2.  Bearbeiten Sie das nachstehende Skript und führen Sie es anschließend aus.  
  
    ```  
    \<#   
    This script uses the Azure Resource model and creates a new ARM storage account.  
    Modify this script to use an existing ARM or classic storage account   
    using the instructions in comments within this script  
    #>  
    # Define global variables for the script  
    $prefixName = '<a prefix name>'  # used as the prefix for the name for various objects  
    $subscriptionName='<your subscription name>'   # the name  of subscription name you will use  
    $locationName = '<a data center location>'  # the data center region you will use  
    $storageAccountName= $prefixName + 'storage' # the storage account name you will create or use  
    $containerName= $prefixName + 'container'  # the storage container name to which you will attach the SAS policy with its SAS token  
    $policyName = $prefixName + 'policy' # the name of the SAS policy  
  
    \<#   
    Using Azure Resource Manager deployment model  
    Comment out this entire section and use the classic storage account name to use an existing classic storage account  
    #>  
  
    # Set a variable for the name of the resource group you will create or use  
    $resourceGroupName=$prefixName + 'rg'   
  
    # adds an authenticated Azure account for use in the session   
    Login-AzureRmAccount    
  
    # set the tenant, subscription and environment for use in the rest of   
    Set-AzureRmContext -SubscriptionName $subscriptionName   
  
    # create a new resource group - comment out this line to use an existing resource group  
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $locationName   
  
    # Create a new ARM storage account - comment out this line to use an existing ARM storage account  
    New-AzureRmStorageAccount -Name $storageAccountName -ResourceGroupName $resourceGroupName -Type Standard_RAGRS -Location $locationName   
  
    # Get the access keys for the ARM storage account  
    $accountKeys = Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName  
  
    # Create a new storage account context using an ARM storage account  
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $accountKeys[0].Value 
  
    \<#  
    Using the Classic deployment model  
    Use the following four lines to use an existing classic storage account  
    #>  
    #Classic storage account name  
    #Add-AzureAccount  
    #Select-AzureSubscription -SubscriptionName $subscriptionName #provide an existing classic storage account  
    #$accountKeys = Get-AzureStorageKey -StorageAccountName $storageAccountName  
    #$storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $accountKeys.Primary  
  
    # The remainder of this script works with either the ARM or classic sections of code above  
  
    # Creates a new container in blob storage  
    $container = New-AzureStorageContainer -Context $storageContext -Name $containerName  
    $cbc = $container.CloudBlobContainer  
  
    # Sets up a Stored Access Policy and a Shared Access Signature for the new container  
    $permissions = $cbc.GetPermissions();  
    $policyName = $policyName  
    $policy = new-object 'Microsoft.WindowsAzure.Storage.Blob.SharedAccessBlobPolicy'  
    $policy.SharedAccessStartTime = $(Get-Date).ToUniversalTime().AddMinutes(-5)  
    $policy.SharedAccessExpiryTime = $(Get-Date).ToUniversalTime().AddYears(10)  
    $policy.Permissions = "Read,Write,List,Delete"  
    $permissions.SharedAccessPolicies.Add($policyName, $policy)  
    $cbc.SetPermissions($permissions);  
  
    # Gets the Shared Access Signature for the policy  
    $policy = new-object 'Microsoft.WindowsAzure.Storage.Blob.SharedAccessBlobPolicy'  
    $sas = $cbc.GetSharedAccessSignature($policy, $policyName)  
    Write-Host 'Shared Access Signature= '$($sas.Substring(1))''  
  
    # Outputs the Transact SQL to the clipboard and to the screen to create the credential using the Shared Access Signature  
    Write-Host 'Credential T-SQL'  
    $tSql = "CREATE CREDENTIAL [{0}] WITH IDENTITY='Shared Access Signature', SECRET='{1}'" -f $cbc.Uri,$sas.Substring(1)   
    $tSql | clip  
    Write-Host $tSql  
  
    ```  
  
3.  Nach Abschluss des Skripts wir die CREATE CREDENTIAL-Anweisung in Ihrer Zwischenablage zur Verwendung in der nächsten Lektion abgelegt.  
  
**Nächste Lektion:**  
  
[Lektion 2: Erstellen von SQL Server-Anmeldeinformationen mit einer Shared Access Signature (SAS)](../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)  
  
## <a name="see-also"></a>Siehe auch  
[Shared Access Signatures, Teil 1: Grundlagen zum SAS-Modell](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)  
[Erstellen von Containern](https://msdn.microsoft.com/library/azure/dd179468.aspx)  
[Set Container ACL](https://msdn.microsoft.com/library/azure/dd179391.aspx)  
[Get Container ACL](https://msdn.microsoft.com/library/azure/dd179469.aspx)  
  
  
  



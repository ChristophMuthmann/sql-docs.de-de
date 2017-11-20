---
title: Bereitstellen ein SSIS-Projekts mit PowerShell | Microsoft Docs
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.suite: sql
ms.custom: 
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 656e62f36446db4ef5b232129130a0253d2aebdf
ms.openlocfilehash: 37fe358eb7e11cb878ebd9b0c8356ac2295ca7e9
ms.contentlocale: de-de
ms.lasthandoff: 09/22/2017

---
# <a name="deploy-an-ssis-project-with-powershell"></a>Bereitstellen eines SSIS-Projekts mit PowerShell
Dieser Schnellstart-Lernprogramm veranschaulicht, wie ein PowerShell-Skript verwenden, um eine Verbindung mit einem Datenbankserver und einem SSIS-Projekt im SSIS-Katalog bereitstellen.

## <a name="powershell-script"></a>PowerShell-Skript
Geben Sie geeignete Werte für die Variablen am Anfang das folgende Skript aus, und führen Sie das Skript zum Bereitstellen des SSIS-Projekts.

> [!NOTE]
> Im folgenden Beispiel wird die Windows-Authentifizierung. Um SQL Server-Authentifizierung verwenden, ersetzen die `Integrated Security=SSPI;` Argument mit `User ID=<user name>;Password=<password>;`.

```powershell
# Variables
$SSISNamespace = "Microsoft.SqlServer.Management.IntegrationServices"
$TargetServerName = "localhost"
$TargetFolderName = "Project1Folder"
$ProjectFilePath = "C:\Projects\Integration Services Project1\Integration Services Project1\bin\Development\Integration Services Project1.ispac"
$ProjectName = "Integration Services Project1"

# Load the IntegrationServices assembly
$loadStatus = [System.Reflection.Assembly]::Load("Microsoft.SQLServer.Management.IntegrationServices, "+
    "Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91, processorArchitecture=MSIL")

# Create a connection to the server
$sqlConnectionString = `
    "Data Source=" + $TargetServerName + ";Initial Catalog=master;Integrated Security=SSPI;"
$sqlConnection = New-Object System.Data.SqlClient.SqlConnection $sqlConnectionString

# Create the Integration Services object
$integrationServices = New-Object $SSISNamespace".IntegrationServices" $sqlConnection

# Get the Integration Services catalog
$catalog = $integrationServices.Catalogs["SSISDB"]

# Create the target folder
$folder = New-Object $SSISNamespace".CatalogFolder" ($catalog, $TargetFolderName,
    "Folder description")
$folder.Create()

Write-Host "Deploying " $ProjectName " project ..."

# Read the project file and deploy it
[byte[]] $projectFile = [System.IO.File]::ReadAllBytes($ProjectFilePath)
$folder.DeployProject($ProjectName, $projectFile)

Write-Host "Done."
```

## <a name="next-steps"></a>Nächste Schritte
- Erwägen Sie andere Verfahren zum Bereitstellen eines Pakets aus.
    - [Bereitstellen eines SSIS-Pakets mit SSMS](./ssis-quickstart-deploy-ssms.md)
    - [Bereitstellen eines SSIS-Pakets mit Transact-SQL (SSMS)](./ssis-quickstart-deploy-tsql-ssms.md)
    - [Bereitstellen eines SSIS-Pakets mit Transact-SQL (Visual Studio-Code)](ssis-quickstart-deploy-tsql-vscode.md)
    - [Bereitstellen eines SSIS-Pakets von der Befehlszeile aus](./ssis-quickstart-deploy-cmdline.md)
    - [Bereitstellen eines SSIS-Pakets mit c#](./ssis-quickstart-deploy-dotnet.md) 
- Führen Sie ein bereitgestelltes Paket. Um ein Paket auszuführen, können Sie über mehrere Tools und Sprachen auswählen. Weitere Informationen finden Sie unter den folgenden Artikeln:
    - [Führen Sie ein SSIS-Paket mit SSMS](./ssis-quickstart-run-ssms.md)
    - [Führen Sie ein SSIS-Paket mit Transact-SQL (SSMS)](./ssis-quickstart-run-tsql-ssms.md)
    - [Führen Sie ein SSIS-Paket mit Transact-SQL (Visual Studio-Code)](ssis-quickstart-run-tsql-vscode.md)
    - [Führen Sie ein SSIS-Paket von der Befehlszeile aus](./ssis-quickstart-run-cmdline.md)
    - [Führen Sie ein SSIS-Paket mit PowerShell](ssis-quickstart-run-powershell.md)
    - [Führen Sie ein SSIS-Paket mit c#](./ssis-quickstart-run-dotnet.md) 


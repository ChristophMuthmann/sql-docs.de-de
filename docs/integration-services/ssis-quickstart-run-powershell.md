---
title: "Ein SSIS-Paket mit PowerShell ausführen | Microsoft Docs"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-server-2017
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: 656e62f36446db4ef5b232129130a0253d2aebdf
ms.openlocfilehash: d392ac49442ef0f04961908fff7acf553fa1aa57
ms.contentlocale: de-de
ms.lasthandoff: 09/22/2017

---
# <a name="run-an-ssis-package-with-powershell"></a>Führen Sie ein SSIS-Paket mit PowerShell
Dieser Schnellstart-Lernprogramm veranschaulicht, wie ein PowerShell-Skript verwenden, um eine Verbindung mit einem Datenbankserver und einem SSIS-Paket ausführen.

## <a name="powershell-script"></a>PowerShell-Skript
Geben Sie geeignete Werte für die Variablen am Anfang das folgende Skript aus, und führen Sie das Skript zum Ausführen des SSIS-Pakets.

> [!NOTE]
> Im folgenden Beispiel wird die Windows-Authentifizierung. Um SQL Server-Authentifizierung verwenden, ersetzen die `Integrated Security=SSPI;` Argument mit `User ID=<user name>;Password=<password>;`.

```powershell
# Variables
$SSISNamespace = "Microsoft.SqlServer.Management.IntegrationServices"
$TargetServerName = "localhost"
$TargetFolderName = "Project1Folder"
$ProjectName = "Integration Services Project1"
$PackageName = "Package.dtsx"

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

# Get the folder
$folder = $catalog.Folders[$TargetFolderName]

# Get the project
$project = $folder.Projects[$ProjectName]

# Get the package
$package = $project.Packages[$PackageName]

Write-Host "Running " $PackageName "..."

$result = $package.Execute("false", $null)

Write-Host "Done."
```

## <a name="next-steps"></a>Nächste Schritte
- Erwägen Sie andere Verfahren zum Ausführen eines Pakets aus.
    - [Führen Sie ein SSIS-Paket mit SSMS](./ssis-quickstart-run-ssms.md)
    - [Führen Sie ein SSIS-Paket mit Transact-SQL (SSMS)](./ssis-quickstart-run-tsql-ssms.md)
    - [Führen Sie ein SSIS-Paket mit Transact-SQL (Visual Studio-Code)](ssis-quickstart-run-tsql-vscode.md)
    - [Führen Sie ein SSIS-Paket von der Befehlszeile aus](./ssis-quickstart-run-cmdline.md)
    - [Führen Sie ein SSIS-Paket mit c#](./ssis-quickstart-run-dotnet.md) 


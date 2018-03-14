---
title: "Bereitstellen, Ausführen und Überwachen von SSIS-Paketen in Azure | Microsoft-Dokumentation"
ms.date: 02/05/2018
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: lift-shift
ms.suite: sql
ms.custom: 
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7b17cdd39e1eb155581d070ef659d6c34c044b4d
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/08/2018
---
# <a name="deploy-run-and-monitor-an-ssis-package-on-azure"></a>Bereitstellen, Ausführen und Überwachen eines SSIS-Pakets in Azure
Dieses Tutorial zeigt, wie ein SQL Server Integration Services-Projekt in der SSISDB-Katalogdatenbank auf einer Azure SQL-Datenbank bereitgestellt wird, ein Paket in Azure SSIS Integration Runtime ausgeführt wird und das ausgeführte Paket überwacht wird.

## <a name="prerequisites"></a>Voraussetzungen

Prüfen Sie, ob Sie über die Version 17.2 oder höher von SQL Server Management Studio verfügen, bevor Sie beginnen. Die neueste Version von SSMS können Sie unter [Herunterladen von SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) herunterladen.

Vergewissern Sie sich auch, dass Sie die SSIS-Datenbank eingerichtet und eine Azure SSIS Integration Runtime bereitgestellt haben. Informationen zur Bereitstellung von SSIS unter Azure finden Sie unter [Bereitstellen von SQL Server Integration Services-Paketen in Azure](https://docs.microsoft.com/azure/data-factory/tutorial-create-azure-ssis-runtime-portal).

> [!NOTE]
> Für die Bereitstellung in Azure wird nur das Projektbereitstellungsmodell unterstützt.

## <a name="connect-to-the-ssisdb-database"></a>Herstellen einer Verbindung mit SSISDB

Verwenden Sie SQL Server Management Studio, um eine Verbindung mit dem SSIS-Katalog auf Ihrem Azure SQL-Datenbankserver herzustellen. Weitere Informationen und Screenshots finden Sie unter [Herstellen einer Verbindung mit der SSISDB-Katalogdatenbank in Azure](ssis-azure-connect-to-catalog-database.md).

Beachten Sie diese beiden wichtigen Punkte. Diese Schritte werden in der folgenden Prozedur beschrieben.
-   Geben Sie den vollqualifizierten Namen des Azure SQL-Datenbankservers im Format **mysqldbserver.database.windows.net** ein.
-   Wählen Sie `SSISDB` als Datenbank für die Verbindung.

> [!IMPORTANT]
> Ein Azure SQL-Datenbankserver überwacht Port 1433. Wenn Sie versuchen, eine Verbindung zu einem Azure SQL-Datenbankserver innerhalb einer Unternehmensfirewall herzustellen, muss dieser Port in der Unternehmensfirewall geöffnet sein, damit Sie eine Verbindung herstellen können.

1. Öffnen Sie SQL Server Management Studio.

2. **Stellen Sie eine Verbindung mit dem Server her**. Geben Sie im Dialogfeld **Verbindung mit dem Server herstellen** die folgenden Informationen ein:

   | Einstellung       | Vorgeschlagener Wert | Description | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Servertyp** | Datenbankmodul | Dieser Wert ist erforderlich. |
   | **Servername** | Der vollqualifizierte Servername | Der Name muss das folgende Format aufweisen: **mysqldbserver.database.windows.net**. Falls Sie den Servernamen benötigen, finden Sie ihn mithilfe der Anweisungen unter [Connect to the SSISDB Catalog database on Azure (Herstellen einer Verbindung mit der SSIS-Katalogdatenbank in Azure)](ssis-azure-connect-to-catalog-database.md). |
   | **Authentifizierung** | SQL Server-Authentifizierung | In diesem Schnellstart wird die SQL-Authentifizierung verwendet. |
   | **Anmeldename** | Das Konto des Serveradministrators | Das Konto, das Sie beim Erstellen des Servers angegeben haben. |
   | **Kennwort** | Das Kennwort für das Konto des Serveradministrators | Das Kennwort, das Sie beim Erstellen des Servers angegeben haben. |

3. **Stellen Sie eine Verbindung mit der SSIS-Datenbank her**. Wählen Sie **Optionen**  aus, um das Dialogfeld **Mit Server verbinden** zu erweitern. Wählen Sie im erweiterten Dialogfeld **Mit Server verbinden** die Registerkarte **Verbindungseigenschaften** aus. Wählen Sie `SSISDB` im Feld **Mit Datenbank verbinden** aus, oder geben Sie es ein.

4. Klicken Sie auf **Verbinden**. Das Fenster „Objekt-Explorer“ wird in SSMS geöffnet. 

5. Erweitern Sie im Objekt-Explorer **Integration Services-Kataloge** und dann **SSISDB**, um die Objekte in der SSIS-Katalogdatenbank anzuzeigen.

## <a name="deploy-a-project-with-the-deployment-wizard"></a>Bereitstellen eines Projekts mit dem Bereitstellungs-Assistenten

Weitere Informationen zum Bereitstellen von Paketen und zum Bereitstellungs-Assistenten finden Sie unter [Bereitstellen von SQL Server Integration Services-Projekten und Paketen (SSIS)](../packages/deploy-integration-services-ssis-projects-and-packages.md) und [Bereitstellungs-Assistent für Integration Services](../packages/deploy-integration-services-ssis-projects-and-packages.md#integration-services-deployment-wizard).

### <a name="start-the-integration-services-deployment-wizard"></a>Starten des Bereitstellungs-Assistenten für Integration Services
1. Erweitern Sie im Objekt-Explorer in SSMS einen Projektorder mit den Knoten **Integration Services-Kataloge** und dem erweiterten **SSISDB**-Knoten.

2.  Wählen Sie den Knoten **Projekte** aus.

3.  Klicken Sie mit der rechten Maustaste auf den Knoten **Projekte**, und wählen Sie **Projekt bereitstellen** aus. Der Bereitstellungs-Assistent für Integration Services wird geöffnet. Sie können ein Projekt aus der SSIS-Katalogdatenbank oder dem Dateisystem bereitstellen.

    ![Bereitstellen eines Projekts aus SSMS](media/ssis-azure-deploy-run-monitor-tutorial/ssisdb-deploy-project1.png)

    ![Das Dialogfeld des SSIS-Bereitstellungs-Assistenten wird geöffnet](media/ssis-azure-deploy-run-monitor-tutorial/ssisdb-deploy-project2.png)

### <a name="deploy-a-project-with-the-deployment-wizard"></a>Bereitstellen eines Projekts mit dem Bereitstellungs-Assistenten
1. Lesen Sie auf der Seite **Einführung** des Bereitstellungs-Assistenten die Einführung. Klicken Sie auf **Weiter**, um zur Seite **Quelle auswählen** zu wechseln.

2. Wählen Sie auf der Seite **Quelle auswählen** das vorhandene SSIS-Projekt aus, das bereitgestellt werden soll.
    -   Um eine von Ihnen erstellte Projektbereitstellungsdatei bereitzustellen, wählen Sie **Projektbereitstellungsdatei** aus, und geben Sie den Pfad für die ISPAC-Datei ein.
    -   Um ein Projekt bereitzustellen, das sich in einem SSIS-Katalog befindet, wählen Sie **Integration Services-Katalog** aus und geben dann den Servernamen und den Pfad zum Projekt im Katalog ein.
    -   Klicken Sie auf **Weiter**, um die Seite **Ziel auswählen** zu sehen.
  
3.  Wählen Sie auf der Seite **Ziel auswählen** das Ziel für das Projekt aus.
    -   Geben Sie den vollqualifizierten Servernamen im Format `<server_name>.database.windows.net` ein.
    -   Klicken Sie dann auf **Durchsuchen**, um den Zielordner in SSISDB auszuwählen.
    -   Klicken Sie auf **Weiter**, um die Seite **Überprüfen** zu öffnen.  
  
4.  Überprüfen Sie auf der Seite **Überprüfen** die Einstellungen, die Sie ausgewählt haben.
    -   Sie können Ihre Auswahl ändern, indem Sie auf **Vorherige** klicken, oder indem Sie auf einen der Schritte im linken Bereich klicken.
    -   Klicken Sie auf **Bereitstellen**, um den Bereitstellungsprozess zu starten.

    > ![HINWEIS] Wenn Sie die Fehlermeldung **Es liegt kein aktiver Worker-Agent vor (.Net SqlClient-Datenanbieter)** erhalten, stellen Sie sicher, dass die Azure-SSIS Integration Runtime (Azure-SSIS IR) ausgeführt wird. Dieser Fehler tritt auf, wenn Sie versuchen, eine Bereitstellung durchzuführen, während die Azure-SSIS IR beendet ist.

5.  Nachdem der Bereitstellungsvorgang abgeschlossen ist, wird die Seite **Ergebnisse** geöffnet. Diese Seite zeigt an, ob die einzelnen Aktionen erfolgreich ausgeführt wurden oder ob Fehler aufgetreten sind.
    -   Ist die Aktion fehlerhaft, klicken Sie in der Spalte **Ergebnis** auf **Fehlgeschlagen**, um eine Erklärung über den Fehler anzuzeigen.
    -   Sie können auf **Bericht speichern** klicken, um die Ergebnisse in einer XML-Datei zu speichern.
    -   Klicken Sie auf **Schließen**, um den Assistenten zu beenden.

## <a name="deploy-a-project-with-powershell"></a>Bereitstellen eines Projekts mit PowerShell

Um ein Projekt mit PowerShell für SSISDB in Azure SQL-Datenbank bereitzustellen, passen Sie das folgende Skript an Ihre Anforderungen an. Das Skript zählt die untergeordneten Ordner unter `$ProjectFilePath` sowie die Projekte in jedem untergeordneten Ordner auf, erstellt daraufhin die gleichen Ordner in SSISDB und stellt die Projekte in diesen Ordnern bereit.

Dieses Skript erfordert, dass SQL Server Data Tools Version 17.x oder SQL Server Management Studio auf dem Computer installiert ist, auf dem das Skript ausgeführt wird.

```powershell
# Variables
$ProjectFilePath = "C:\<folder>"
$SSISDBServerEndpoint = "<servername>.database.windows.net"
$SSISDBServerAdminUserName = "<username>"
$SSISDBServerAdminPassword = "<password>"

# Load the IntegrationServices Assembly
[System.Reflection.Assembly]::LoadWithPartialName("Microsoft.SqlServer.Management.IntegrationServices") | Out-Null;

# Store the IntegrationServices Assembly namespace to avoid typing it every time
$ISNamespace = "Microsoft.SqlServer.Management.IntegrationServices"

Write-Host "Connecting to server ..."

# Create a connection to the server
$sqlConnectionString = "Data Source=" + $SSISDBServerEndpoint + ";User ID="+ $SSISDBServerAdminUserName +";Password="+ $SSISDBServerAdminPassword + ";Initial Catalog=SSISDB"
$sqlConnection = New-Object System.Data.SqlClient.SqlConnection $sqlConnectionString

# Create the Integration Services object
$integrationServices = New-Object $ISNamespace".IntegrationServices" $sqlConnection

# Get the catalog
$catalog = $integrationServices.Catalogs['SSISDB']

write-host "Enumerating all folders..."

$folders = ls -Path $ProjectFilePath -Directory

if ($folders.Count -gt 0)
{
    foreach ($filefolder in $folders)
    {
        Write-Host "Creating Folder " $filefolder.Name " ..."

        # Create a new folder
        $folder = New-Object $ISNamespace".CatalogFolder" ($catalog, $filefolder.Name, "Folder description")
        $folder.Create()

        $projects = ls -Path $filefolder.FullName -File -Filter *.ispac
        if ($projects.Count -gt 0)
        {
            foreach($projectfile in $projects)
            {
                $projectfilename = $projectfile.Name.Replace(".ispac", "")
                Write-Host "Deploying " $projectfilename " project ..."

                # Read the project file, and deploy it to the folder
                [byte[]] $projectFileContent = [System.IO.File]::ReadAllBytes($projectfile.FullName)
                $folder.DeployProject($projectfilename, $projectFileContent)
            }
        }
    }
}

Write-Host "All done." 
```

## <a name="run-a-package"></a>Ausführen eines Pakets

1. Wählen Sie im Objekt-Explorer von SSMS das Paket aus, das Sie ausführen möchten.

2. Klicken Sie mit der rechten Maustaste auf das ausgewählte Paket, und klicken Sie auf **Ausführen**, um das Dialogfeld **Paket ausführen** zu öffnen.

3.  Konfigurieren Sie im Dialogfeld **Paket ausführen** die Paketausführung, indem Sie die Einstellungen auf den Registerkarten **Parameter**, **Verbindungs-Manager** und **Erweitert** nutzen.

4.  Klicken Sie auf **OK**, um das Paket auszuführen.

## <a name="monitor-the-running-package-in-ssms"></a>Überwachen des ausgeführten Pakets in SSMS

Um die Status der ausgeführten Integration Services-Vorgänge, wie Bereitstellung, Überprüfung und Paketausführung, auf dem Integration Services-Server anzuzeigen, verwenden Sie das Dialogfeld **Aktive Vorgänge** in SSMS. Klicken Sie mit der rechten Maustaste auf **SSISDB**, und klicken Sie dann auf **Aktive Vorgänge**, um das Dialogfeld **Aktive Vorgänge** zu öffnen.

Sie können auch im Objekt-Explorer ein Paket auswählen, mit der rechten Maustaste darauf klicken, und dann auf **Berichte** > **Standardberichte** > **Alle Ausführungen** klicken.

Weitere Informationen zum Überwachen von ausgeführten Paketen in SSMS finden Sie unter [Monitor Running Packages and Other Operations (Überwachen ausgeführter Pakete und anderer Vorgänge)](https://docs.microsoft.com/sql/integration-services/performance/monitor-running-packages-and-other-operations).

## <a name="monitor-the-azure-ssis-integration-runtime"></a>Überwachen der Azure SSIS Integration Runtime

Um Statusinformationen über ausgeführte Pakete in Azure SSIS Integration Runtime zu erhalten, verwenden Sie folgende PowerShell-Befehle: Geben Sie für jeden Befehl die Namen der Data Factory, Azure SSIS IR und der Ressourcengruppe an.

### <a name="get-metadata-about-the-azure-ssis-integration-runtime"></a>Abrufen von Metadaten über Azure SSIS Integration Runtime

```powershell
Get-AzureRmDataFactoryV2IntegrationRuntime -DataFactoryName $DataFactoryName -Name $AzureSsisIRName -ResourceGroupName $ResourceGroupName
```

### <a name="get-the-status-of-the-azure-ssis-integration-runtime"></a>Abrufen des Status von Azure SSIS Integration Runtime

```powershell
Get-AzureRmDataFactoryV2IntegrationRuntime -Status -DataFactoryName $DataFactoryName -Name $AzureSsisIRName -ResourceGroupName $ResourceGroupName
```

## <a name="next-steps"></a>Nächste Schritte
- Lernen Sie, wie Sie die Paketausführung zeitlich planen. Weitere Informationen finden Sie unter [Schedule SSIS package execution on Azure (Planen der Ausführung von SSIS-Paketen in Azure)](ssis-azure-schedule-packages.md)

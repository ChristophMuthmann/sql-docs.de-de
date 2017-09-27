---
title: Bereitstellen ein SSIS-Projekts durch .NET Code (c#) | Microsoft Docs
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
ms.openlocfilehash: c83ad5be88951b92c59a7517ed2676ff30692d02
ms.contentlocale: de-de
ms.lasthandoff: 09/22/2017

---
# <a name="deploy-an-ssis-project-with-c-code-in-a-net-app"></a>Bereitstellen eines SSIS-Projekts mit C#-Code in einer .NET-App
Dieser Schnellstart-Lernprogramm veranschaulicht, wie zum Schreiben von C#-Code zum Herstellen einer Verbindung mit einem Datenbankserver und einem SSIS-Projekt bereitstellen.

Zum Erstellen einer c#-app können Sie Visual Studio, Visual Studio-Code oder ein anderes Tool Ihrer Wahl verwenden.

## <a name="prerequisites"></a>Erforderliche Komponenten

Bevor Sie beginnen, stellen Sie sicher, dass Sie Visual Studio oder Visual Studio Code installiert sein. Herunterladen die kostenlose Community Edition von Visual Studio oder das kostenlose Visual Studio-Code aus [Visual Studio-Downloads](https://www.visualstudio.com/downloads/).

> [!NOTE]
> Ein Azure SQL-Datenbankserver wird Port 1433 überwacht. Wenn Sie, zur Verbindung mit eines Azure SQL-Datenbank-Servers innerhalb einer Unternehmens-Firewall versuchen muss diesen Port in der Unternehmensfirewall für Sie erfolgreich eine Verbindung herstellen geöffnet sein.

## <a name="get-the-connection-info-if-deployed-to-sql-database"></a>Erhalten Sie die Verbindungsinformationen aus, wenn SQL-Datenbank bereitgestellt. 

Wenn Ihre Pakete mit einer Azure SQL-Datenbank bereitgestellt werden, erhalten Sie die Verbindung mit dem SSIS-Katalogdatenbank (SSISDB) benötigten Verbindungsinformationen. Sie benötigen die vollqualifizierten Namen und Anmeldenamen Serverinformationen in die folgenden Schritte.

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com/)an.
2. Wählen Sie **SQL-Datenbanken** aus der linken Menü, und klicken Sie auf die SSISDB-Datenbank auf dem **SQL-Datenbanken** Seite. 
3. Auf der **Übersicht** Seite für Ihre Datenbank, überprüfen Sie den vollqualifizierten Servernamen. Um die **klicken** Option, zeigen Sie auf den Namen des Servers. 
4. Wenn Sie Ihre Anmeldeinformationen für Azure SQL-Datenbank-Server vergessen haben, navigieren Sie zu SQL-Datenbank-Server auf den Admin-Servernamen anzeigen. Sie können das Kennwort zurücksetzen, falls erforderlich.
5. Klicken Sie auf **Anzeigen von Datenbank-Verbindungszeichenfolgen**.
6. Überprüfen Sie die vollständige **ADO.NET** Verbindungszeichenfolge. Im Beispielcode wird ein `SqlConnectionStringBuilder` diese Verbindungszeichenfolge mit den einzelnen Parameterwerten erneut erstellen, die Sie bereitstellen.

## <a name="create-a-new-visual-studio-project"></a>Erstellen eines neuen Visual Studio-Projekts

1. Wählen Sie in Visual Studio **Datei**, **neu**, **Projekt**. 
2. In der **neues Projekt** Dialogfeld, und erweitern Sie **Visual C#-**.
3. Wählen Sie **Konsolen-App** , und geben Sie *Deploy_ssis_project* für den Namen des Projekts.
4. Klicken Sie auf **OK** erstellen und öffnen das neue Projekt in Visual Studio.

## <a name="add-references"></a>Fügen Sie Verweise hinzu
1. Klicken Sie im Projektmappen-Explorer mit der Maustaste die **Verweise** Ordner, und wählen **Verweis hinzufügen**. Die **Verweis-Manager** Dialogfeld wird geöffnet.
2. In der **Verweis-Manager** Dialogfeld erweitern Sie **Assemblys** , und wählen Sie **Erweiterungen**.
3. Wählen Sie die folgenden zwei Verweise hinzufügen:
    -   Microsoft.SqlServer.Management.Sdk.Sfc
    -   Microsoft.SqlServer.Smo
4. Klicken Sie auf die **Durchsuchen** Schaltfläche, um einen Verweis hinzufügen **Microsoft.SqlServer.Management.IntegrationServices**. (Diese Assembly ist nur im globalen Assemblycache (GAC) installiert.) Die **wählen Sie die Dateien zu verweisen** Dialogfeld wird geöffnet.
5. In der **wählen Sie die Dateien zu verweisen** Dialogfeld navigieren Sie zum GAC-Ordner, der die Assembly enthält. Dieser Ordner ist in der Regel `C:\Windows\assembly\GAC_MSIL\Microsoft.SqlServer.Management.IntegrationServices\14.0.0.0__89845dcd8080cc91`.
6. Wählen Sie die Assembly (d. h. die DLL-Datei) in den Ordner und klicken Sie auf **hinzufügen**.
7. Klicken Sie auf **OK** schließen die **Verweis-Manager** Dialogfeld Feld und die drei Verweise hinzuzufügen. Um sicherzustellen, dass die Verweise vorhanden sind, überprüfen Sie die **Verweise** Liste im Projektmappen-Explorer.

## <a name="add-the-c-code"></a>Fügen Sie den C#-code 
1. Open **"Program.cs"**.

2. Ersetzen Sie den Inhalt des **"Program.cs"** durch den folgenden Code. Fügen Sie die entsprechenden Werte für Server, Datenbank, Benutzername und Kennwort.

> [!NOTE]
> Im folgenden Beispiel wird die Windows-Authentifizierung. Um SQL Server-Authentifizierung verwenden, ersetzen die `Integrated Security=SSPI;` Argument mit `User ID=<user name>;Password=<password>;`.

```csharp
using Microsoft.SqlServer.Management.IntegrationServices;
using System;
using System.Data.SqlClient;
using System.IO;

namespace deploy_ssis_project
{
    class Program
    {
        static void Main(string[] args)
        {
            // Variables
            string targetServerName = "localhost";
            string targetFolderName = "Project1Folder";
            string projectName = "Integration Services Project1";
            string projectFilePath = @"C:\Projects\Integration Services Project1\Integration Services Project1\bin\Development\Integration Services Project1.ispac";

            // Create a connection to the server
            string sqlConnectionString = "Data Source=" + targetServerName +
                ";Initial Catalog=master;Integrated Security=SSPI;";
            SqlConnection sqlConnection = new SqlConnection(sqlConnectionString);

            // Create the Integration Services object
            IntegrationServices integrationServices = new IntegrationServices(sqlConnection);

            // Get the Integration Services catalog
            Catalog catalog = integrationServices.Catalogs["SSISDB"];

            // Create the target folder
            CatalogFolder folder = new CatalogFolder(catalog,
                targetFolderName, "Folder description");
            folder.Create();

            Console.WriteLine("Deploying " + projectName + " project.");

            byte[] projectFile = File.ReadAllBytes(projectFilePath);
            folder.DeployProject(projectName, projectFile);

            Console.WriteLine("Done.");
        }
    }
}
```

## <a name="run-the-code"></a>Führen Sie den code

1. Um die Anwendung auszuführen, drücken Sie die **F5**.
2. Stellen Sie sicher, dass das Projekt bereitgestellt wurde, in SSMS.

## <a name="next-steps"></a>Nächste Schritte
- Erwägen Sie andere Verfahren zum Bereitstellen eines Pakets aus.
    - [Bereitstellen eines SSIS-Pakets mit SSMS](./ssis-quickstart-deploy-ssms.md)
    - [Bereitstellen eines SSIS-Pakets mit Transact-SQL (SSMS)](./ssis-quickstart-deploy-tsql-ssms.md)
    - [Bereitstellen eines SSIS-Pakets mit Transact-SQL (Visual Studio-Code)](ssis-quickstart-deploy-tsql-vscode.md)
    - [Bereitstellen eines SSIS-Pakets von der Befehlszeile aus](./ssis-quickstart-deploy-cmdline.md)
    - [Bereitstellen eines SSIS-Pakets mit PowerShell](ssis-quickstart-deploy-powershell.md)
- Führen Sie ein bereitgestelltes Paket. Um ein Paket auszuführen, können Sie über mehrere Tools und Sprachen auswählen. Weitere Informationen finden Sie unter den folgenden Artikeln:
    - [Führen Sie ein SSIS-Paket mit SSMS](./ssis-quickstart-run-ssms.md)
    - [Führen Sie ein SSIS-Paket mit Transact-SQL (SSMS)](./ssis-quickstart-run-tsql-ssms.md)
    - [Führen Sie ein SSIS-Paket mit Transact-SQL (Visual Studio-Code)](ssis-quickstart-run-tsql-vscode.md)
    - [Führen Sie ein SSIS-Paket von der Befehlszeile aus](./ssis-quickstart-run-cmdline.md)
    - [Führen Sie ein SSIS-Paket mit PowerShell](ssis-quickstart-run-powershell.md)
    - [Führen Sie ein SSIS-Paket mit c#](./ssis-quickstart-run-dotnet.md) 


---
title: "Ausführen eines SSIS-Pakets mit Transact-SQL (Visual Studio Code) | Microsoft-Dokumentation"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: quick-start
ms.suite: sql
ms.custom: 
ms.technology: integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c962285d10ca05434deafc9cf1d071a09f8cca65
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="run-an-ssis-package-from-visual-studio-code-with-transact-sql"></a>Ausführen eines SSIS-Pakets aus Visual Studio Code mit Transact-SQL
In diesem Schnellstart wird erläutert, wie Sie Visual Studio Code verwenden müssen, um eine Verbindung mit der SSIS-Katalogdatenbank herzustellen, und wie Sie anschließend Transact-SQL-Anweisungen verwenden müssen, um ein im SSIS-Katalog gespeichertes SSIS-Paket auszuführen.

Visual Studio Code ist ein Code-Editor für Windows, macOS und Linux, der Erweiterung unterstützt. Dazu gehört auch die `mssql`-Erweiterung zum Herstellen einer Verbindung mit Microsoft SQL Server, Azure SQL-Datenbank und Azure SQL Data Warehouse. Weitere Informationen zu Visual Studio Code finden Sie unter [Visual Studio Code](https://code.visualstudio.com/).

## <a name="prerequisites"></a>Voraussetzungen

Prüfen Sie, bevor Sie beginnen, ob Sie die neueste Version von Visual Studio Code installiert haben und die `mssql`-Erweiterung geladen ist. Informationen zum Herunterladen dieser Tools finden Sie auf den folgenden Seiten:
-   [Herunterladen von Visual Studio Code](https://code.visualstudio.com/Download)
-   [mssql extension (mssql-Erweiterung)](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)

## <a name="set-language-mode-to-sql-in-vs-code"></a>Festlegen des Sprachmodus auf SQL in Visual Studio Code

Legen Sie den Sprachmodus auf `mssql`SQL **in Visual Studio Code fest, um** -Befehle und T-SQL-IntelliSense zu aktivieren.

1. Öffnen Sie zuerst Visual Studio Code und dann ein neues Fenster. 

2. Klicken Sie auf **Nur-Text** in der unteren rechten Ecke der Statusleiste.

3. Klicken Sie im sich öffnenden Dropdownmenü **Sprachmodus auswählen** auf **SQL**, oder geben Sie es ein, und drücken Sie dann die **EINGABETASTE**, um den Sprachmodus auf „SQL“ festzulegen. 

## <a name="connect-to-the-ssis-catalog-database"></a>Herstellen einer Verbindung mit der SSIS-Katalogdatenbank

Verwenden Sie Visual Studio Code, um eine Verbindung mit dem SSIS-Katalog herzustellen.

> [!IMPORTANT]
> Bevor Sie fortfahren, stellen Sie sicher, dass Sie die erforderlichen Server-, Datenbank- und Anmeldeinformationen zur Hand haben. Wenn Sie den Fokus von Visual Studio Code ändern, nachdem Sie mit der Eingabe der Verbindungsprofilinformationen begonnen haben, müssen Sie erneut mit dem Erstellen des Verbindungsprofils beginnen.

1. Drücken Sie in VS Code **STRG+UMSCHALT+P** (oder **F1**), um die Befehlspalette zu öffnen.

2. Geben Sie **sqlcon** ein, und drücken Sie die **EINGABETASTE**.

3. Drücken Sie die **EINGABETASTE**, um **Create Connection Profile** (Verbindungsprofil erstellen) auszuwählen. Mithilfe dieses Schritts wird ein Verbindungsprofil für Ihre SQL Server-Instanz erstellt.

4. Befolgen Sie die Anweisungen, um die Verbindungseigenschaften für das neue Verbindungsprofil anzugeben. Nachdem Sie sämtliche Werte angegeben haben, drücken Sie die **EINGABETASTE**, um fortzufahren. 

   | Einstellung       | Vorgeschlagener Wert | Weitere Informationen |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Servername** | Der vollqualifizierte Servername | Wenn Sie eine Verbindung mit einem Azure SQL-Datenbankserver herstellen, ist der Name im Format `<server_name>.database.windows.net`. |
   | **Datenbankname** | **SSISDB** | Dies ist der Name der Datenbank, mit der eine Verbindung hergestellt werden soll. |
   | **Authentifizierung** | SQL-Anmeldung| In diesem Schnellstart wird die SQL-Authentifizierung verwendet. |
   | **User name** | Das Konto des Serveradministrators | Dabei handelt es sich um das Konto, das Sie beim Erstellen des Servers angegeben haben. |
   | **Kennwort (SQL-Anmeldung)** | Das Kennwort für das Konto des Serveradministrators | Dabei handelt es sich um das Kennwort, das Sie beim Erstellen des Servers angegeben haben. |
   | **Kennwort speichern** | Ja oder Nein | Wenn Sie nicht bei jedem Neustart Ihr Kennwort eingeben möchten, wählen Sie „Ja“ aus. |
   | **Namen für dieses Profil eingeben** | Ein Profilname wie **mySSISServer** | Wenn Sie den Profilnamen speichern, wird bei späteren Anmeldungen schneller eine Verbindung hergestellt. | 

5. Drücken Sie die **ESC**-Taste, um die Meldung zu schließen, in der Sie darüber informiert werden, dass das Profil erstellt und eine Verbindung hergestellt wurde.

6. Überprüfen Sie Ihre Verbindung in der Statusleiste.

## <a name="run-the-t-sql-code"></a>Ausführen des T-SQL-Codes
Führen Sie den folgenden Transact-SQL-Code aus, um ein SSIS-Paket auszuführen.

1. Geben Sie im Fenster **Editor** die folgende Abfrage in ein leeres Abfragefenster ein. (Dabei handelt es sich um den Code, der durch die Option **Skript** im Dialogfeld **Paket ausführen** in SSMS generiert wurde.)

2. Aktualisieren Sie die Parameterwerte in der für das System gespeicherten `catalog.create_execution`-Prozedur.

3. Drücken Sie **STRG+UMSCHALT+E**, um den Code und das Paket auszuführen.

```sql
Declare @execution_id bigint
EXEC [SSISDB].[catalog].[create_execution] @package_name=N'Package.dtsx',
    @execution_id=@execution_id OUTPUT,
    @folder_name=N'Deployed Projects',
      @project_name=N'Integration Services Project1',
    @use32bitruntime=False,
      @reference_id=Null
Select @execution_id
DECLARE @var0 smallint = 1
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,
    @object_type=50,
      @parameter_name=N'LOGGING_LEVEL',
      @parameter_value=@var0
EXEC [SSISDB].[catalog].[start_execution] @execution_id
GO
```

## <a name="next-steps"></a>Nächste Schritte
- Erfahren Sie mehr über weitere Möglichkeiten, ein Paket auszuführen.
    - [Run an SSIS package with SSMS](./ssis-quickstart-run-ssms.md) (Ausführen eines SSIS-Pakets mit SSMS)
    - [Ausführen eines SSIS-Pakets mit Transact-SQL (SSMS)](./ssis-quickstart-run-tsql-ssms.md)
    - [Run an SSIS package from the command prompt (Ausführen eines SSIS-Pakets über die Eingabeaufforderung)](./ssis-quickstart-run-cmdline.md)
    - [Run an SSIS package with PowerShell](ssis-quickstart-run-powershell.md) (Ausführen eines SSIS-Pakets mit PowerShell)
    - [Run an SSIS package with C#](./ssis-quickstart-run-dotnet.md) (Ausführen eines SSIS-Pakets mit C#) 

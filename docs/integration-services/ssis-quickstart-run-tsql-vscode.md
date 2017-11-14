---
title: "Führen Sie ein SSIS-Paket mit Transact-SQL (Visual Studio-Code) | Microsoft Docs"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-server-2017
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 656e62f36446db4ef5b232129130a0253d2aebdf
ms.openlocfilehash: a912bf7f7944d4af3d41c5596e67aa77f3214112
ms.contentlocale: de-de
ms.lasthandoff: 09/22/2017

---
# <a name="run-an-ssis-package-from-visual-studio-code-with-transact-sql"></a>Führen Sie ein SSIS-Paket von Visual Studio-Code mit Transact-SQL
Dieser Schnellstart veranschaulicht, wie Visual Studio-Code zum Herstellen einer Verbindung mit dem SSIS-Katalogdatenbank und verwenden Sie Transact-SQL-Anweisungen zum Ausführen eines SSIS-Pakets im SSIS-Katalog gespeichert.

Visual Studio-Code ist ein Codeeditor für Windows, Mac OS und Linux, der Erweiterungen, einschließlich unterstützt die `mssql` -Erweiterung für das Herstellen einer Verbindung mit Microsoft SQL Server, Azure SQL-Datenbank oder Azure SQL Data Warehouse. Weitere Informationen zu Visual Studio Code, finden Sie unter [Visual Studio Cod](https://code.visualstudio.com/).

## <a name="prerequisites"></a>Erforderliche Komponenten

Bevor Sie beginnen, stellen Sie sicher, dass Sie die neueste Version von Visual Studio Code installiert und geladen haben die `mssql` Erweiterung. Zum Herunterladen dieser Tools finden Sie unter den folgenden Seiten:
-   [Herunterladen von Visual Studio Code](https://code.visualstudio.com/Download)
-   [MSSQL-Erweiterung](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)

## <a name="set-language-mode-to-sql-in-vs-code"></a>Modus "Sprache" in SQL in Visual Studio Code festlegen

So aktivieren Sie `mssql` Befehle und T-SQL-IntelliSense wird der Modus "Sprache" wird festgelegt **SQL** in Visual Studio-Code.

1. Öffnen Sie Visual Studio-Code, und klicken Sie dann öffnen Sie ein neues Fenster. 

2. Klicken Sie auf **Klartext** in der unteren rechten Ecke der Statusleiste.

3. In der **Sprachauswahl Modus** Dropdown-Menü, das geöffnet wird, eingeben oder auswählen **SQL**, und drücken Sie dann die **EINGABETASTE** Modus "Sprache" auf SQL festgelegt. 

## <a name="connect-to-the-ssis-catalog-database"></a>Herstellen einer Verbindung mit dem SSIS-Katalogdatenbank

Verwenden Sie Visual Studio-Code zum Herstellen einer Verbindung im SSIS-Katalog.

> [!IMPORTANT]
> Stellen Sie bevor Sie fortfahren sicher, dass Sie Ihre Server, Datenbank und Anmeldeinformationen bereit. Wenn Sie sich der Fokus aus Visual Studio-Code ändern, nachdem Sie mit der Eingabe der Verbindungsinformationen für das Profil beginnen, müssen Sie neu starten, erstellen das Verbindungsprofil.

1. Drücken Sie in Visual Studio-Code **STRG + UMSCHALT + P** (oder **F1**) öffnen Sie die Palette-Befehl.

2. Typ **Sqlcon** , und drücken Sie **EINGABETASTE**.

3. Drücken Sie **EINGABETASTE** auswählen **Verbindungsprofils erstellen**. Dieser Schritt erstellt ein Profil für die SQL Server-Instanz.

4. Befolgen Sie die Verbindungseigenschaften für das neue Verbindungsprofil angeben. Drücken Sie nach jeder Wert angeben, **EINGABETASTE** um den Vorgang fortzusetzen. 

   | Einstellung       | Empfohlener Wert | Weitere Informationen |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Servername** | Die vollqualifizierten Servernamen | Wenn Sie die Verbindung mit einem Azure SQL-Datenbankserver herstellen, wird der Name im folgenden Format: `<server_name>.database.windows.net`. |
   | **Datenbankname** | **SSISDB** | Der Name der Datenbank für die Verbindung. |
   | **Authentifizierung** | SQL-Anmeldung| Dieser Schnellstart verwendet SQL-Authentifizierung. |
   | **Benutzername** | Serveradmin-Kontos | Dies ist das Konto, das Sie angegeben werden, wenn Sie auf den Server erstellt haben. |
   | **Kennwort (SQL-Anmeldung)** | Das Kennwort für Ihr serveradmin-Kontos | Dies ist das Kennwort, das Sie angegeben werden, wenn Sie auf den Server erstellt haben. |
   | **Speichern Kennwort?** | Ja oder Nein | Wählen Sie Ja, wenn Sie nicht, das Kennwort jedes Mal eingeben möchten. |
   | **Geben Sie einen Namen für dieses Profil** | Benennen Sie ein Profil, z. B. **MySSISServer** | Eine gespeicherte Profilname beschleunigt die Verbindung bei nachfolgenden Anmeldungen. | 

5. Drücken Sie die **ESC** Taste, um die Info-Meldung zu schließen, die Sie informiert, dass das Profil erstellt und verbunden ist.

6. Überprüfen Sie die Verbindung in der Statusleiste aus.

## <a name="run-the-t-sql-code"></a>Führen Sie den T-SQL-code
Führen Sie den folgenden Transact-SQL-Code, um ein SSIS-Paket ausführen.

1. In der **Editor** Fenster, geben Sie die folgende Abfrage in das leere Abfragefenster. (Dieser Code ist die vom generierten Code der **Skript** option in der **Paketausführungs** Dialogfeld in SSMS.)

2. Aktualisieren Sie die Parameterwerte in der `catalog.create_execution` für Ihr System die gespeicherte Prozedur.

3. Drücken Sie **STRG + UMSCHALT + E** führen Sie den Code, und führen Sie das Paket.

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
- Erwägen Sie andere Verfahren zum Ausführen eines Pakets aus.
    - [Führen Sie ein SSIS-Paket mit SSMS](./ssis-quickstart-run-ssms.md)
    - [Führen Sie ein SSIS-Paket mit Transact-SQL (SSMS)](./ssis-quickstart-run-tsql-ssms.md)
    - [Führen Sie ein SSIS-Paket von der Befehlszeile aus](./ssis-quickstart-run-cmdline.md)
    - [Führen Sie ein SSIS-Paket mit PowerShell](ssis-quickstart-run-powershell.md)
    - [Führen Sie ein SSIS-Paket mit c#](./ssis-quickstart-run-dotnet.md) 


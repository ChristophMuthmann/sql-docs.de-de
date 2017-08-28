---
title: "Verwenden Sie die Visual Studio Code-Mssql-Erweiterung für SQL Server | Microsoft Docs"
description: "In diesem Lernprogramm wird gezeigt, wie die Mssql-Erweiterung für Visual Studio Code verwendet wird. Diese Erweiterung ermöglicht das Bearbeiten und Ausführen von Transact-SQL-Skripts in Visual Studio Code."
author: erickangMSFT
ms.author: erickang
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 9766ee75-32d3-4045-82a6-4c7968bdbaa6
ms.custom: H1Hack27Feb2017
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: a4b2f82ac904d58604b0c27d46624995878e8a35
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="use-visual-studio-code-to-create-and-run-transact-sql-scripts-for-sql-server"></a>Verwenden von Visual Studio-Code zum Erstellen und Ausführen von Transact-SQL-Skripts für SQL Server

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

In diesem Thema zeigt, wie die **Mssql** -Erweiterung für Visual Studio-Code (Visual Studio-Code), SQL Server-Datenbanken zu entwickeln.

Visual Studio-Code ist eine grafische Code-Editor für Linux, Mac OS und Windows, der Erweiterungen unterstützt. Die [**Mssql** -Erweiterung für Visual Studio Code]  ermöglicht es Ihnen, eine Verbindung mit SQL Server, Abfrage mit Transact-SQL (T-SQL) und die Ergebnisse anzuzeigen.

## <a name="install-vs-code"></a>Installieren von VS-Code
1. Wenn Sie Visual Studio-Code nicht bereits installiert haben [herunterladen und installieren Sie Visual Studio Code] auf Ihrem Computer.

2. Starten Sie Visual Studio Code.

## <a name="install-the-mssql-extension"></a>Installieren Sie die Mssql-Erweiterung
Die folgenden Schritte erläutern, wie zum Installieren der Mssql-Erweiterung. 

1. Drücken Sie **STRG + UMSCHALT + P** (oder **F1**) um den Befehl Palette in Visual Studio Code zu öffnen. 

2. Wählen Sie **Erweiterung installieren** und Typ **Mssql**.
   > [!TIP] 
   > Für MacOS die **CMD** Schlüssel entspricht dem **STRG** auf Linux- und Windows-Taste.

2. Klicken Sie auf Installieren **Mssql**. 
   
   <img src="./media/sql-server-linux-develop-use-vscode/vscode-extension.png" alt="Install the extension" style="width: 600px;"/>

3. Die **Mssql** Erweiterung akzeptiert bis zu einer Minute zu installieren. Warten Sie, bis die Meldung, die Sie informiert, dass es erfolgreich installiert.

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-install-success-notification.png" alt="Installation success notification" style="width: 600px;"/>

   > [!NOTE]
   > Für MacOS müssen Sie OpenSSL installieren. Dies ist eine Voraussetzung für .net Core, die von der Mssql-Erweiterung verwendet. Führen Sie die **Voraussetzung installieren** Schritte in der [.Net Core Anweisungen]. Oder Sie können die folgenden Befehle ausführen, in Ihrem MacOS Terminaldienste.
   >
   >   ```bash
   >   brew update
   >   brew install openssl
   >   ln -s /usr/local/opt/openssl/lib/libcrypto.1.0.0.dylib /usr/local/lib/
   >   ln -s /usr/local/opt/openssl/lib/libssl.1.0.0.dylib /usr/local/lib/
   >   ```
   
   > [!NOTE]
   > Bei Windows 8.1, Windows Server 2012 oder niedrigere Versionen müssen Sie herunterladen und Installieren der [Windows 10 universelle C-Laufzeit]. Herunter, und öffnen Sie die Zip-Datei. Führen Sie das Installationsprogramm (MSU-Datei) die aktuelle Konfiguration Ihrer OS abzielt.

## <a name="create-or-open-a-sql-file"></a>Erstellen Sie oder öffnen Sie eine SQL-Datei

Die **Mssql** Erweiterung Mssql-Befehle und T-SQL-IntelliSense, wenn der Modus "Sprache", um festgelegt ist im Editor ermöglicht **SQL**.

1. Drücken Sie **STRG + N**. Visual Studio-Code wird eine neue Datei mit "Nur-Text" standardmäßig geöffnet. 

2. Drücken Sie **STRG + K, M** , und ändern Sie den Modus "Sprache" zu **SQL**. 

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-language-mode.png" alt="SQL language mode" style="width: 500px;" />

3. Alternativ öffnen Sie eine vorhandene Datei mit der Dateierweiterung SQL aufweisen. Der Modus "Sprache" wird automatisch **SQL** für Dateien, die die SQL-Erweiterung aufweisen.  

## <a name="connect-to-sql-server"></a>Verbindung mit SQL Server herstellen

Die folgenden Schritte zeigen, Herstellen einer Verbindung mit SQL Server mit Visual Studio Code.

1. Drücken Sie in Visual Studio-Code **STRG + UMSCHALT + P** (oder **F1**) öffnen Sie die Palette-Befehl.

2. Typ **Sql** Mssql-Befehle anzeigen.

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-commands.png" alt="mssql commands" style="width: 500px;" />
   

3. Wählen Sie die **MS SQL: Verbinden** Befehl. Geben Sie einfach **Sqlcon** , und drücken Sie **EINGABETASTE**.

4. Wählen Sie **erstellen Verbindungsprofils**. Dadurch wird ein Profil für die SQL Server-Instanz erstellt.

5. Befolgen Sie die Verbindungseigenschaften für das neue Verbindungsprofil angeben. Drücken Sie nach jeder Wert angeben, **EINGABETASTE** um den Vorgang fortzusetzen. 

   Die folgende Tabelle beschreibt die Verbindungsprofils-Eigenschaften.

   | Einstellung | Description |
   |-----|-----|
   | **Servername** | Der Name des SQL Server-Instanz. Verwenden Sie für dieses Lernprogramm **"localhost"** für die Verbindung mit der lokalen SQL Server-Instanz auf dem Computer. Wenn eine Verbindung mit einem SQL-Remoteserver herstellen, geben Sie den Namen des Ziel-SQL Server-Computer oder die IP-Adresse ein. |
   | **[Optional] Datenbankname** | Die Datenbank, die Sie verwenden möchten. Für die Zwecke dieses Lernprogramms, geben Sie eine Datenbank, und drücken Sie **EINGABETASTE** um den Vorgang fortzusetzen. |
   | **Benutzername** | Geben Sie den Namen eines Benutzers mit Zugriff auf eine Datenbank auf dem Server. Für dieses Lernprogramm verwenden Sie den Standardnamen **SA** Konto während der SQL Server-Setup erstellt. |
   | **Kennwort (SQL-Anmeldung)** | Geben Sie das Kennwort für den angegebenen Benutzer ein. | 
   | **Speichern Kennwort?** | Typ **Ja** zum Speichern des Kennworts. Geben Sie andernfalls **keine** für das Kennwort jedes Mal aufgefordert werden das Verbindungsprofil verwendet wird. |
   | **[Optional] Geben Sie einen Namen für dieses Profil** | Der Name des Verbindungsprofils. Angenommen, nennen Sie das Profil **"localhost" Profil**. 

   > [!Tip] 
   > Sie können erstellen und Bearbeiten von remoteverbindungsprofilen in Benutzereinstellungen-Datei (settings.json). Öffnen Sie dazu die Einstellungsdatei **Voreinstellung** und dann **Benutzereinstellungen** im VS-Code. Weitere Informationen finden Sie unter [Verwalten von remoteverbindungsprofilen].

6. Drücken Sie die **ESC** Taste, um die Info-Meldung zu schließen, die Sie informiert, dass das Profil erstellt und verbunden ist.

   > [!TIP]
   > Wenn Sie einen Verbindungsfehler erhalten, versuchen zunächst, die diagnose des Problems aus der Fehlermeldung, in der **Ausgabe** Bereich in Visual Studio Code (Wählen Sie **Ausgabe** auf die **Ansicht** im Menü). Überprüfen Sie anschließend die [Empfehlungen zur Verbindungsproblembehandlung].

7. Überprüfen Sie die Verbindung in der Statusleiste aus.

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-connection-status.png" alt="Connection status" style="width: 500px;" />

## <a name="create-a-database"></a>Erstellen Sie eine Datenbank

1. Geben Sie im Editor **Sql** , um eine Liste der bearbeitbaren Codeausschnitte anzuzeigen. 

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-sql-snippets.png" alt="SQL snippets" style="width: 500px;" />

2. Wählen Sie **SqlCreateDatabase**.

3. Geben Sie in den Ausschnitt, **TutorialDB** für den Datenbanknamen.

   ```sql
   USE master
   GO
   IF NOT EXISTS (
      SELECT name
      FROM sys.databases
      WHERE name = N'TutorialDB'
   )
   CREATE DATABASE [TutorialDB]
   GO
   ```
   
4. Drücken Sie **STRG + UMSCHALT + E** zur Ausführung der Transact-SQL-Befehle. Anzeigen der Ergebnisse in das Abfragefenster ein.

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-create-database-messages.png" alt="create database messages" style="width: 500px;" />

   > [!TIP]
   > Sie können die Verknüpfung von schlüsselbindungen für die Befehle der Mssql-Erweiterung anpassen. Finden Sie unter [Tastenkombinationen anpassen].

## <a name="create-a-table"></a>Erstellen Sie eine Tabelle

1. Entfernen Sie den Inhalt im Editor-Fenster.

2. Drücken Sie **F1** um die Befehls-Palette anzuzeigen.

3. Typ **Sql** in der Palette der Befehl zum Anzeigen der SQL-Befehle oder Typ **Sqluse** für **MS SQL: Use Database** Befehl.

4. Klicken Sie auf **MS SQL: Use Database**, und wählen Sie die **TutorialDB** Datenbank. Dies ändert den Kontext, in die neue Datenbank, die im vorherigen Abschnitt erstellt haben.

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-use-database.png" alt="use database" style="width: 500px;" />

3. Geben Sie im Editor **Sql** Ausschnitte angezeigt, und wählen Sie dann **SqlCreateTable** , und drücken Sie **geben**.

4. Geben Sie in den Ausschnitt, **Mitarbeiter** für den Tabellennamen.

5. Drücken Sie **Registerkarte**, und geben Sie dann **Dbo** für den Schemanamen an.

   > [!NOTE]
   > Nach dem Hinzufügen des Ausschnitts, müssen Sie die Namen der Tabelle und Schema eingeben, ohne den Fokus von der Visual Studio Code-Editor ändern.

6. Ändern Sie den Spaltennamen für **Column1** auf **Namen** und **Column2** auf **Speicherort**.

   ```sql
   -- Create a new table called 'Employees' in schema 'dbo'
   -- Drop the table if it already exists
   IF OBJECT_ID('dbo.Employees', 'U') IS NOT NULL
   DROP TABLE dbo.Employees
   GO
   -- Create the table in the specified schema
   CREATE TABLE dbo.Employees
   (
      EmployeesId        INT    NOT NULL   PRIMARY KEY, -- primary key column
      Name      [NVARCHAR](50)  NOT NULL,
      Location   [NVARCHAR](50)  NOT NULL
   );
   GO
   ```

7. Drücken Sie **STRG + UMSCHALT + E** zum Erstellen der Tabelle.

## <a name="insert-and-query"></a>Einfüge- und abfrageleistung

1. Fügen Sie die folgenden Anweisungen zum Einfügen von vier Zeilen in der **Mitarbeiter** Tabelle. Wählen Sie dann alle Zeilen aus.

   ```sql
   -- Insert rows into table 'Employees'
   INSERT INTO Employees
      ([EmployeesId],[Name],[Location])
   VALUES
      ( 1, N'Jared', N'Australia'),
      ( 2, N'Nikita', N'India'),
      ( 3, N'Tom', N'Germany'),
      ( 4, N'Jake', N'United States')   
   GO   
   -- Query the total count of employees
   SELECT COUNT(*) as EmployeeCount FROM dbo.Employees;
   -- Query all employee information
   SELECT e.EmployeesId, e.Name, e.Location 
   FROM dbo.Employees as e
   GO
   ```

   > [!TIP]
   > Verwenden Sie beim eingeben, der Unterstützung des T-SQL IntelliSense.
   >   <img src="./media/sql-server-linux-develop-use-vscode/vscode-intellisense.png" alt="TSQL IntelliSense" style="width: 500px;" />

2. Drücken Sie **STRG + UMSCHALT + E** zur Ausführung der Befehle. Die beiden führen legt Anzeige in der **Ergebnisse** Fenster. 

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-result-grid.png" alt="Results" style="width: 300px;" />

## <a name="view-and-save-the-result"></a>Anzeigen und Speichern des Ergebnisses

1. Auf der **Ansicht** klicken Sie im Menü **zum ein-/ausschalten Editor Gruppe Layout** vertikale oder horizontale Teilung Layouts wechseln.

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-toggle-split.png" alt="Vertical split" style="width: 500px;" />

2. Klicken Sie auf die **Ergebnisse** und **Nachrichten** Bereich Header reduzieren und erweitern im Bereich.

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-toggle-messages-pannel.png" alt="Toggle Messages" style="width: 500px;" />

   > [!TIP]
   > Sie können das Standardverhalten der Mssql-Erweiterung anpassen. Finden Sie unter [Erweiterung Optionen anpassen].

2. Klicken Sie auf das Symbol "Raster maximieren" auf der zweiten Ergebnisrasters zu vergrößern.

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-maximize-grid.png" alt="Maximize grid" style="width: 500px;" />

   > [!NOTE]
   > Das Symbol "Maximieren" zeigt an, wenn die T-SQL-Skript mindestens zwei Ergebnisraster aufweist.

3. Öffnen Sie im Kontextmenü Raster mit der rechten Maustaste in einem Raster an. 

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-grid-context-menu.png" alt="Context menu" style="width: 500px;" />

4. Wählen Sie **wählen Sie alle**.

5. Öffnen Sie das Raster-Kontextmenü, und wählen **speichern als JSON** um das Ergebnis in eine JSON-Datei zu speichern.

6. Geben Sie einen Dateinamen für die JSON-Datei. Geben Sie für dieses Lernprogramm **employees.json**.

7. Stellen Sie sicher, dass die JSON-Datei gespeichert und in Visual Studio Code geöffnet ist.

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-save-as-json.png" alt="Save as Json" style="width: 500px;" />

## <a name="next-steps"></a>Nächste Schritte

In einem realen Szenario könnten Sie ein Skript, die Sie benötigen, speichern und Ausführen erstellen höher (für die Verwaltung oder als Teil einer größeren Entwicklungsprojekt). In diesem Fall können Sie speichern Sie das Skript mit einem **.sql** Erweiterung.

Wenn Sie noch nicht in T-SQL vertraut sind, finden Sie unter [Lernprogramm: Schreiben von Transact-SQL-Anweisungen] und [Transact-SQL-Referenz (Datenbankmodul)].

Weitere Informationen zu verwenden, oder der Mssql-Erweiterung verwendet werden sollen, finden Sie unter [Mssql Erweiterung Projekt Wiki].

Weitere Informationen zur Verwendung von Visual Studio Code finden Sie unter der [Dokumentation zu Visual Studio Code](https://code.visualstudio.com/docs).

[**Mssql** Erweiterung für Visual Studio-Code]:https://aka.ms/mssql-marketplace
[herunterladen und installieren Sie Visual Studio Code]:https://code.visualstudio.com/Download
[.Net Core Anweisungen]:https://www.microsoft.com/net/core
[Verwalten von remoteverbindungsprofilen]:https://github.com/Microsoft/vscode-mssql/wiki/manage-connection-profiles
[Empfehlungen zur Verbindungsproblembehandlung]:./sql-server-linux-troubleshooting-guide.md#connection
[Tastenkombinationen anpassen]:https://github.com/Microsoft/vscode-mssql/wiki/customize-shortcuts
[Lernprogramm: Schreiben von Transact-SQL-Anweisungen]:https://msdn.microsoft.com/library/ms365303.aspx
[Transact-SQL-Referenz (Datenbankmodul)]:https://msdn.microsoft.com/library/bb510741.aspx
[Visual Studio Code documentation]:https://code.visualstudio.com/docs
[Windows 10 universelle C-Laufzeit]:https://github.com/Microsoft/vscode-mssql/wiki/windows10-universal-c-runtime-requirement
[Erweiterung Optionen anpassen]: https://github.com/Microsoft/vscode-mssql/wiki/customize-options
[Mssql Erweiterung Projekt Wiki]: https://github.com/Microsoft/vscode-mssql/wiki


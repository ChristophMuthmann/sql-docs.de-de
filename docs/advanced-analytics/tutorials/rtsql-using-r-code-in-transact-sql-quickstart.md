---
title: Verwenden von R-Code in Transact-SQL (R in SQL-Schnellstart) | Microsoft Docs
ms.custom: SQL2016_New_Updated
ms.date: 08/20/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: 4e6fe30d-a105-4d5b-bc05-5e5204753847
caps.latest.revision: "36"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Active
ms.openlocfilehash: 812a37c9400d67f2aa5bb08796877e0d06b815b9
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="using-r-code-in-transact-sql-r-in-sql-quickstart"></a>Verwenden von R-Code in Transact-SQL (R in SQL-Schnellstart)

Dieses Tutorial erklärt Ihnen, wie Sie grundsätzlich ein R-Skript aus einer gespeicherten T-SQL-Prozedur aufrufen.

**Lernen Sie**

+ Einbetten von R in eine T-SQL-Funktion
+ Einige Tipps zum Arbeiten mit R und SQL-Typen und Daten Datenobjekte
+ Wie Sie ein einfaches Modell erstellen, und speichern sie mit SQL Server
+ Vorgehensweise: Erstellen von Vorhersagen und ein R-Plots mithilfe des Modells

**Geschätzte Dauer**

30 Minuten ohne Setup

## <a name="prerequisites"></a>Erforderliche Komponenten

Sie benötigen Zugriff auf eine Instanz von SQL Server mit einem der folgenden bereits installiert:

+ SQL Server 2017 Machine Learning Services mit installierte R-Sprache
+ SQL Server 2016 R Services

Die SQL Server-Instanz kann im virtuellen Computer in Azure oder lokal sein. Beachten Sie, dass die externe Skriptingfunktion standardmäßig deaktiviert ist, müssen Sie möglicherweise einige zusätzliche Schritte erforderlich, um Bezugsquelle arbeiten nur sein.

Zum Ausführen von SQL-Abfragen, die R-Skripts enthalten, können Sie eine andere Anwendung, die eine Verbindung mit einer Datenbank herstellen und T-SQL-Code ausführen können. SQL-Experten können SQL Server Management Studio (SSMS) oder Visual Studio verwenden.

Für dieses Lernprogramm soll zeigen, wie einfach es ist zum Ausführen von R in SQL Server, wir haben verwendet die neue **Mssql-Erweiterung für Visual Studio Code**. Visual Studio Code ist einer kostenlosen Entwicklungsumgebung, die unter Linux, Mac OS oder Windows ausgeführt werden kann. Die **Mssql** Erweiterung ist eine einfache Erweiterung für die Ausführung von T-SQL-Abfragen. Informationen zur Installation finden Sie im Artikel [Use the mssql extension for Visual Studio Code (Verwenden der MSSQL-Erweiterung für Visual Studio Code)](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode).

## <a name="connect-to-a-database-and-run-a-hello-world-test-script"></a>Verbinden mit Datenbank und Ausführen eines Hello World-Testskripts

1. Erstellen Sie in Visual Studio Code eine neue Textdatei, und nennen Sie sie „BasicRSQL.sql“.
2. Drücken Sie, während diese Datei geöffnet ist, STRG+UMSCHALT+P (COMMAND+P auf einem Mac OS), geben Sie **sql** ein, um die SQL-Befehle aufzulisten, und klicken Sie auf **Verbinden**. Visual Studio-Code fordert Sie zum Erstellen eines Profils zu verwendende Verbindung mit einer bestimmten Datenbank. Dies ist optional, jedoch erleichtert das Wechseln zwischen Datenbanken und Anmeldungen.
    + Wählen Sie einen Server oder eine Instanz, auf dem R in SQL Server installiert wurde.
    + Verwenden Sie ein Konto mit Berechtigungen zum Erstellen einer neuen Datenbank, führen Sie SELECT-Anweisungen aus, und zeigen Sie Tabellendefinitionen an.
2. Wenn die Verbindung hergestellt wurde, sollten Server- und Datenbankname zusammen mit Ihren aktuellen Anmeldeinformationen in der Statusleiste angezeigt werden. Wenn keine Verbindung hergestellt werden konnte, sollten Sie überprüfen, ob der Computername und der Servername richtig sind.
3. Fügen Sie diese Anweisung ein, und führen Sie sie aus.

    ```sql
    EXEC sp_execute_external_script
      @language =N'R',
      @script=N'OutputDataSet<-InputDataSet',
      @input_data_1 =N'SELECT 1 AS hello'
      WITH RESULT SETS (([hello] int not null));
    GO
    ```

    In Visual Studio Code können Sie den Code markieren, den Sie ausführen möchten, und STRG+UMSCHALT+E drücken. Wenn dies für Sie schwer zu merken ist, können Sie es ändern. Siehe [Customize the shortcut key bindings (Anpassen der Tastenkombinationen)](https://github.com/Microsoft/vscode-mssql/wiki/customize-shortcuts).

    ![rsql-basictut_hello1code](media/rsql-basictut-hello1code.PNG)

**Ergebnisse**

![rsql_basictut_hello1](media/rsql-basictut-hello1.PNG)

## <a name="troubleshooting"></a>Problembehandlung

+ Wenn Sie alle Fehler aus dieser Abfrage erhalten haben, kann Installation unvollständig sein. Nach dem Hinzufügen der Funktion mit dem SQL Server-Setup-Assistenten müssen Sie einige zusätzliche Schritte unternehmen, um die Verwendung externer Codebibliotheken zu aktivieren.  Siehe [Set up SQL Server R Services (Einrichten von SQL Server R Services)](../r/set-up-sql-server-r-services-in-database.md).

+ Stellen Sie sicher, dass der Launchpad-Dienst ausgeführt wird. Je nach Umgebung kann es erforderlich sein, dass Sie die R-Workerkonten für die Verbindung mit SQL Server aktivieren, zusätzliche Netzwerkbibliotheken installieren, Remotecodeausführung zulassen oder die Instanz neu starten, nachdem alles konfiguriert wurde. Siehe [R Services Installation and Upgrade FAQ (FAQ zu Installation und Upgrade von R Services)](../r/upgrade-and-installation-faq-sql-server-r-services.md).

+ Visual Studio Code erhalten Sie unter [Download and install Visual Studio Code (Herunterladen und Installieren von Visual Studio Code)](https://code.visualstudio.com/Download).

## <a name="next-lesson"></a>Nächste Lektion

Jetzt, dass die Instanz mit R arbeiten kann, los geht.

Lektion 1: [arbeiten mit Eingaben und Ausgaben](rtsql-working-with-inputs-and-outputs.md)

Lektion 2: [R und SQL-Typen und Daten Datenobjekte](rtsql-r-and-sql-data-types-and-data-objects.md)

Lektion 3: [mit R-Funktionen mit SQL Server-Daten](rtsql-using-r-functions-with-sql-server-data.md)

Lektion 4: [aus einem Vorhersagemodell erstellen](rtsql-create-a-predictive-model-r.md)

Lektion 5: [Vorhersagen und der Zeichnungsfläche aus Modell](rtsql-predict-and-plot-from-model.md)

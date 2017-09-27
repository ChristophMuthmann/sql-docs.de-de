---
title: "Führen Sie ein SSIS-Paket von der Befehlszeile aus | Microsoft Docs"
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
ms.openlocfilehash: a33b8518ec3284f5de73d38c87209057dc1c7487
ms.contentlocale: de-de
ms.lasthandoff: 09/22/2017

---
# <a name="run-an-ssis-package-from-the-command-prompt-with-dtexecexe"></a>Führen Sie ein SSIS-Paket von der Befehlszeile aus mit DTExec.exe
Dieser Schnellstart-Lernprogramm veranschaulicht, wie ein SSIS-Paket von der Befehlszeile aus ausführen, durch Ausführen `DTExec.exe` mit den entsprechenden Parametern.

> [!NOTE]
> In diesem Artikel beschriebene Methode wurde nicht mit einer Azure SQL-Datenbankserver bereitgestellten Pakete getestet.

Weitere Informationen zu `DTExec.exe`, finden Sie unter [Dtexec-Hilfsprogramm](https://docs.microsoft.com/en-us/sql/integration-services/packages/dtexec-utility).

## <a name="run-a-package-with-dtexec"></a>Ausführen eines Pakets mit dtexec

Falls der Ordner, die enthält `DTExec.exe` befindet sich nicht in Ihrer `path` Umgebungsvariablen müssen unter Umständen verwendet die `cd` Befehl aus, um in das Verzeichnis zu ändern. Für SQL Server 2017 dieser Ordner ist in der Regel `C:\Program Files (x86)\Microsoft SQL Server\140\DTS\Binn`.

Mit den Parameterwerten, die im folgenden Beispiel verwendet wird führt das Programm das Paket in der angegebene Ordnerpfad auf dem SSIS-Server – d. h. der Server, SSIS-Katalogdatenbank (SSISDB) gehostet. Die `/Server` Parameter enthält den Namen des Servers. Das Programm stellt eine Verbindung als der aktuelle Benutzer mit integrierter Windows-Authentifizierung her. SQL-Authentifizierung verwenden, geben Sie die `/User` und `Password` Parameter durch die entsprechenden Werte.

1. Öffnen Sie ein Eingabeaufforderungsfenster.

2. Führen Sie `DTExec.exe` und geben Sie mindestens Werte für die `ISServer` und die `Server` Parameter, wie im folgenden Beispiel gezeigt:

    ```cmd
    dtexec /ISServer "\SSISDB\Project1Folder\Integration Services Project1\Package.dtsx" /Server "localhost"
    ```

## <a name="next-steps"></a>Nächste Schritte
- Erwägen Sie andere Verfahren zum Ausführen eines Pakets aus.
    - [Führen Sie ein SSIS-Paket mit SSMS](./ssis-quickstart-run-ssms.md)
    - [Führen Sie ein SSIS-Paket mit Transact-SQL (SSMS)](./ssis-quickstart-run-tsql-ssms.md)
    - [Führen Sie ein SSIS-Paket mit Transact-SQL (Visual Studio-Code)](ssis-quickstart-run-tsql-vscode.md)
    - [Führen Sie ein SSIS-Paket mit PowerShell](ssis-quickstart-run-powershell.md)
    - [Führen Sie ein SSIS-Paket mit c#](./ssis-quickstart-run-dotnet.md) 


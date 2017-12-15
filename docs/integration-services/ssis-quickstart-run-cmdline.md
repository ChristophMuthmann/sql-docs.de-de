---
title: "Ausführen eines SSIS-Pakets über die Eingabeaufforderung | Microsoft-Dokumentation"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.suite: sql
ms.custom: 
ms.technology: integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 33293b17caff5d5c71b58bff3f34ed130ab19ba3
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/01/2017
---
# <a name="run-an-ssis-package-from-the-command-prompt-with-dtexecexe"></a>Ausführen eines SSIS-Pakets über die Eingabeaufforderung mit „DTExec.exe“
Dieses Schnellstarttutorial zeigt das Ausführen eines SSIS-Pakets über die Eingabeaufforderung mittels Ausführung von `DTExec.exe` mit den entsprechenden Parametern.

> [!NOTE]
> Die in diesem Artikel beschriebene Methode wurde nicht Paketen getestet, die für einen Azure SQL-Datenbank-Server bereitgestellt werden.

Weitere Informationen zu `DTExec.exe` finden Sie unter [dtexec Utility](https://docs.microsoft.com/sql/integration-services/packages/dtexec-utility) (Hilfprogramm dtexec).

## <a name="run-a-package-with-dtexec"></a>Ausführen eines Pakets mit dtexec

Wenn sich der Ordner, der `DTExec.exe` enthält, nicht in Ihrer Umgebungsvariable `path` befindet, müssen Sie möglicherweise mit dem Befehl `cd` in das Verzeichnis wechseln. Bei SQL Server 2017 lautet dieser Ordner in der Regel `C:\Program Files (x86)\Microsoft SQL Server\140\DTS\Binn`.

Mit den im folgenden Beispiel verwendeten Parameterwerten führt das Programm das Paket im angegebenen Ordnerpfad auf dem SSIS-Server aus – d.h. dem Server, der die SSIS-Katalogdatenbank (SSISDB) hostet. Der `/Server`-Parameter stellt den Namen des Servers bereit. Das Programm stellt als aktueller Benutzer eine Verbindung mit der integrierten Windows-Authentifizierung her. Um die SQL-Authentifizierung zu verwenden, geben Sie die entsprechenden Werte für die Parameter `/User` und `Password` an.

1. Öffnen Sie ein Eingabeaufforderungsfenster.

2. Führen Sie `DTExec.exe` aus, und geben Sie mindestens für die Parameter `ISServer` und `Server` Werte an, wie im folgenden Beispiel gezeigt:

    ```cmd
    dtexec /ISServer "\SSISDB\Project1Folder\Integration Services Project1\Package.dtsx" /Server "localhost"
    ```

## <a name="next-steps"></a>Nächste Schritte
- Erfahren Sie mehr über weitere Möglichkeiten, ein Paket auszuführen.
    - [Run an SSIS package with SSMS](./ssis-quickstart-run-ssms.md) (Ausführen eines SSIS-Pakets mit SSMS)
    - [Run an SSIS package with Transact-SQL (SSMS) (Ausführen eines SSIS-Pakets mit Transact-SQL [SSMS])](./ssis-quickstart-run-tsql-ssms.md)
    - [Run an SSIS package with Transact-SQL (VS Code)](ssis-quickstart-run-tsql-vscode.md) (Ausführen eines SSIS-Pakets mit Transact-SQL [VS Code])
    - [Ausführen eines SSIS-Pakets mit PowerShell](ssis-quickstart-run-powershell.md)
    - [Run an SSIS package with C#](./ssis-quickstart-run-dotnet.md) (Ausführen eines SSIS-Pakets mit C#) 

---
title: "Ausführen eines SSIS-Pakets mit SSMS | Microsoft-Dokumentation"
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
ms.openlocfilehash: 7b35bade8769e3de11f60046375f082146da579d
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="run-an-ssis-package-with-sql-server-management-studio-ssms"></a>Ausführen eines SSIS-Pakets mit SQL Server Management Studio (SSMS)
In diesem Schnellstart wird erläutert, wie Sie SQL Server Management Studio (SSMS) verwenden müssen, um eine Verbindung mit der SSIS-Katalogdatenbank herzustellen, und wie Sie anschließend ein im SSIS-Katalog gespeichertes SSIS-Paket im Objekt-Explorer in SSMS ausführen.

SQL Server Management Studio ist eine integrierte Umgebung zum Verwalten jeder beliebigen SQL-Infrastruktur, von SQL Server bis hin zur SQL-Datenbank. Weitere Informationen zu SSMS finden Sie unter [SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md).

## <a name="prerequisites"></a>Erforderliche Komponenten

Prüfen Sie, ob Sie über die neueste Version von SQL Server Management Studio (SSMS) verfügen, bevor Sie beginnen. Wie Sie SSMS herunterladen, erfahren Sie unter [Herunterladen von SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

## <a name="connect-to-the-ssisdb-database"></a>Herstellen einer Verbindung mit der SSISDB-Datenbank

Verwenden Sie SQL Server Management Studio, um eine Verbindung mit dem SSIS-Katalog einzurichten. 

> [!NOTE]
> Ein Azure SQL-Datenbankserver überwacht Port 1433. Wenn Sie versuchen, eine Verbindung mit einem Azure SQL-Datenbankserver innerhalb einer Unternehmensfirewall herzustellen, muss dieser Port in der Unternehmensfirewall geöffnet sein, damit Sie eine Verbindung herstellen können.

1. Öffnen Sie SQL Server Management Studio.

2. Geben Sie im Dialogfeld **Mit Server verbinden** die folgenden Informationen ein:

   | Einstellung       | Vorgeschlagener Wert | Weitere Informationen | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Servertyp** | Datenbank-Engine | Dieser Wert ist erforderlich. |
   | **Servername** | Der vollqualifizierte Servername | Wenn Sie eine Verbindung mit einem Azure SQL-Datenbankserver herstellen, ist der Name im Format `<server_name>.database.windows.net`. |
   | **Authentifizierung** | SQL Server-Authentifizierung | In diesem Schnellstart wird die SQL-Authentifizierung verwendet. |
   | **Anmeldename** | Das Konto des Serveradministrators | Dabei handelt es sich um das Konto, das Sie beim Erstellen des Servers angegeben haben. |
   | **Kennwort** | Das Kennwort für das Konto des Serveradministrators | Dabei handelt es sich um das Kennwort, das Sie beim Erstellen des Servers angegeben haben. |

3. Klicken Sie auf **Verbinden**. Das Fenster „Objekt-Explorer“ wird in SSMS geöffnet. 

4. Erweitern Sie im Objekt-Explorer **Integration Services-Kataloge** und dann **SSISDB**, um die Objekte in der SSIS-Katalogdatenbank anzuzeigen.

## <a name="run-a-package"></a>Ausführen eines Pakets

1. Wählen Sie im Objekt-Explorer das Paket aus, das Sie ausführen möchten.

2. Klicken Sie mit der rechten Maustaste, und wählen Sie **Ausführen** aus. Das Dialogfeld **Paket ausführen** wird geöffnet.

3.  Konfigurieren Sie die Paketausführung im Dialogfeld „Paket ausführen“ mit den Einstellungen auf den Registerkarten **Parameter**, **Verbindungs-Manager** und **Erweitert**.

4.  Klicken Sie auf „OK“, um das Paket auszuführen.

## <a name="next-steps"></a>Nächste Schritte
- Erfahren Sie mehr über weitere Möglichkeiten, ein Paket auszuführen.
    - [Run an SSIS package with Transact-SQL (SSMS)](./ssis-quickstart-run-tsql-ssms.md) (Ausführen eines SSIS-Pakets mit Transact-SQL [SSMS])
    - [Run an SSIS package with Transact-SQL (VS Code)](ssis-quickstart-run-tsql-vscode.md) (Ausführen eines SSIS-Pakets mit Transact-SQL [VS Code])
    - [Run an SSIS package from the command prompt](./ssis-quickstart-run-cmdline.md) (Ausführen eines SSIS-Pakets über die Eingabeaufforderung)
    - [Run an SSIS package with PowerShell](ssis-quickstart-run-powershell.md) (Ausführen eines SSIS-Pakets mit PowerShell)
    - [Run an SSIS package with C#](./ssis-quickstart-run-dotnet.md) (Ausführen eines SSIS-Pakets mit C#) 

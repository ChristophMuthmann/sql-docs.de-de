---
title: Ausführen eines SSIS-Pakets mit Transact-SQL (SSMS) | Microsoft-Dokumentation
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: quick-start
ms.suite: sql
ms.custom: ''
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b72473635da4818ace7b888ee73e186f7d8ad7ed
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="run-an-ssis-package-from-ssms-with-transact-sql"></a>Ausführen eines SSIS-Pakets aus SSMS mit Transact-SQL (SSMS)
In diesem Schnellstart wird erläutert, wie Sie SQL Server Management Studio (SSMS) verwenden müssen, um eine Verbindung mit der SSIS-Katalogdatenbank herzustellen, und wie Sie anschließend Transact-SQL-Anweisungen verwenden müssen, um ein im SSIS-Katalog gespeichertes SSIS-Paket auszuführen.

SQL Server Management Studio ist eine integrierte Umgebung zum Verwalten jeder beliebigen SQL-Infrastruktur, von SQL Server bis hin zur SQL-Datenbank. Weitere Informationen zu SSMS finden Sie unter [SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md).

## <a name="prerequisites"></a>Voraussetzungen

Prüfen Sie, ob Sie über die neueste Version von SQL Server Management Studio (SSMS) verfügen, bevor Sie beginnen. Wie Sie SSMS herunterladen, erfahren Sie unter [Herunterladen von SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

## <a name="connect-to-the-ssisdb-database"></a>Herstellen einer Verbindung mit SSISDB

Verwenden Sie SQL Server Management Studio, um eine Verbindung mit dem SSIS-Katalog auf Ihrem Azure SQL-Datenbankserver einzurichten. 

> [!NOTE]
> Ein Azure SQL-Datenbankserver überwacht Port 1433. Wenn Sie versuchen, eine Verbindung mit einem Azure SQL-Datenbankserver innerhalb einer Unternehmensfirewall herzustellen, muss dieser Port in der Unternehmensfirewall geöffnet sein, damit Sie eine Verbindung herstellen können.

1. Öffnen Sie SQL Server Management Studio.

2. Geben Sie im Dialogfeld **Verbindung mit dem Server herstellen** die folgenden Informationen ein:

   | Einstellung       | Vorgeschlagener Wert | Weitere Informationen | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Servertyp** | Datenbank-Engine | Dieser Wert ist erforderlich. |
   | **Servername** | Der vollqualifizierte Servername | Wenn Sie eine Verbindung mit einem Azure SQL-Datenbankserver herstellen, ist der Name im Format `<server_name>.database.windows.net`. |
   | **Authentifizierung** | SQL Server-Authentifizierung | In diesem Schnellstart wird die SQL-Authentifizierung verwendet. |
   | **Anmeldename** | Das Konto des Serveradministrators | Dabei handelt es sich um das Konto, das Sie beim Erstellen des Servers angegeben haben. |
   | **Kennwort** | Das Kennwort für das Konto des Serveradministrators | Dabei handelt es sich um das Kennwort, das Sie beim Erstellen des Servers angegeben haben. |

3.  Klicken Sie auf **Verbinden**. Das Fenster „Objekt-Explorer“ wird in SSMS geöffnet.

4. Erweitern Sie im Objekt-Explorer **Integration Services-Kataloge** und dann **SSISDB**, um die Objekte in der SSIS-Katalogdatenbank anzuzeigen.

## <a name="run-a-package"></a>Ausführen eines Pakets
Führen Sie den folgenden Transact-SQL-Code aus, um ein SSIS-Paket auszuführen.

1.  Öffnen Sie in SSMS ein neues Abfragefenster, und fügen Sie den folgenden Code ein. (Dabei handelt es sich um den Code, der durch die Option **Skript** im Dialogfeld **Paket ausführen** in SSMS generiert wurde.)

2.  Aktualisieren Sie die Parameterwerte in der für das System gespeicherten `catalog.create_execution`-Prozedur.

3.  Prüfen Sie, ob es sich bei SSISDB um die aktuelle Datenbank handelt.

4.  Führen Sie das Skript aus.

5. Aktualisieren Sie im Objekt-Explorer ggf. die Inhalte von **SSISDB**, und überprüfen Sie das Projekt, das Sie bereitgestellt haben.

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
    - [Run an SSIS package with SSMS (Ausführen eines SSIS-Pakets mit SSMS)](./ssis-quickstart-run-ssms.md)
    - [Ausführen eines SSIS-Pakets mit Transact-SQL (Visual Studio Code)](ssis-quickstart-run-tsql-vscode.md)
    - [Run an SSIS package from the command prompt](./ssis-quickstart-run-cmdline.md) (Ausführen eines SSIS-Pakets über die Eingabeaufforderung)
    - [Run an SSIS package with PowerShell](ssis-quickstart-run-powershell.md) (Ausführen eines SSIS-Pakets mit PowerShell)
    - [Run an SSIS package with C#](./ssis-quickstart-run-dotnet.md) (Ausführen eines SSIS-Pakets mit C#) 

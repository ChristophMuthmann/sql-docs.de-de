---
title: Bereitstellen eines SSIS-Projekts mit Transact-SQL (SSMS) | Microsoft-Dokumentation
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
ms.openlocfilehash: 65991b38dfecff6a57b9fba0343b43307ec9c2fc
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="deploy-an-ssis-project-from-ssms-with-transact-sql"></a>Bereitstellen eines SSIS-Projekts aus SSMS mit Transact-SQL

In diesem Schnellstart wird erläutert, wie Sie SQL Server Management Studio (SSMS) verwenden müssen, um eine Verbindung mit der SSIS-Katalogdatenbank herzustellen, und wie Sie anschließend Transact-SQL-Anweisungen verwenden müssen, um ein im SSIS-Katalog gespeichertes SSIS-Projekt bereitzustellen. 

> [!NOTE]
> Die in diesem Artikel beschriebene Methode ist nicht verfügbar, wenn Sie mit SSMS eine Verbindung mit einem Azure SQL-Datenbankserver herstellen. Die gespeicherte Prozedur `catalog.deploy_project` erwartet den Pfad zur Datei `.ispac` im lokalen Dateisystem.

SQL Server Management Studio ist eine integrierte Umgebung zum Verwalten jeder beliebigen SQL-Infrastruktur, von SQL Server bis hin zur SQL-Datenbank. Weitere Informationen zu SSMS finden Sie unter [SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md).

## <a name="prerequisites"></a>Voraussetzungen

Prüfen Sie, ob Sie über die neueste Version von SQL Server Management Studio verfügen, bevor Sie beginnen. Wie Sie SSMS herunterladen, erfahren Sie unter [Herunterladen von SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

## <a name="connect-to-the-ssis-catalog-database"></a>Herstellen einer Verbindung mit der SSIS-Katalogdatenbank

Verwenden Sie SQL Server Management Studio, um eine Verbindung mit dem SSIS-Katalog einzurichten. 

> [!NOTE]
> Ein Azure SQL-Datenbankserver überwacht Port 1433. Wenn Sie versuchen, eine Verbindung mit einem Azure SQL-Datenbankserver innerhalb einer Unternehmensfirewall herzustellen, muss dieser Port in der Unternehmensfirewall geöffnet sein, damit Sie eine Verbindung herstellen können.

1. Öffnen Sie SQL Server Management Studio.

2. Geben Sie im Dialogfeld **Verbindung mit dem Server herstellen** die folgenden Informationen ein:

   | Einstellung       | Vorgeschlagener Wert | Weitere Informationen | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Servertyp** | Datenbank-Engine | Dieser Wert ist erforderlich. |
   | **Servername** | Der vollqualifizierte Servername |  |
   | **Authentifizierung** | SQL Server-Authentifizierung | In diesem Schnellstart wird die SQL-Authentifizierung verwendet. |
   | **Anmeldename** | Das Konto des Serveradministrators | Dabei handelt es sich um das Konto, das Sie beim Erstellen des Servers angegeben haben. |
   | **Kennwort** | Das Kennwort für das Konto des Serveradministrators | Dabei handelt es sich um das Kennwort, das Sie beim Erstellen des Servers angegeben haben. |

3. Klicken Sie auf **Verbinden**. Das Fenster „Objekt-Explorer“ wird in SSMS geöffnet. 

4. Erweitern Sie im Objekt-Explorer **Integration Services-Kataloge** und dann **SSISDB**, um die Objekte in der SSIS-Katalogdatenbank anzuzeigen.

## <a name="run-the-t-sql-code"></a>Ausführen des T-SQL-Codes
Führen Sie den folgenden Transact-SQL-Code aus, um ein SSIS-Projekt bereitzustellen.

1.  Öffnen Sie in SSMS ein neues Abfragefenster, und fügen Sie den folgenden Code ein.

2.  Aktualisieren Sie die Parameterwerte in der für das System gespeicherten `catalog.deploy_project`-Prozedur.

3.  Prüfen Sie, ob es sich bei SSISDB um die aktuelle Datenbank handelt.

4.  Führen Sie das Skript aus.

5. Aktualisieren Sie im Objekt-Explorer ggf. die Inhalte von **SSISDB**, und überprüfen Sie das Projekt, das Sie bereitgestellt haben.

```sql
DECLARE @ProjectBinary AS varbinary(max)
DECLARE @operation_id AS bigint
SET @ProjectBinary =
    (SELECT * FROM OPENROWSET(BULK '<project_file_path>.ispac', SINGLE_BLOB) AS BinaryData)

EXEC catalog.deploy_project @folder_name = '<target_folder>',
    @project_name = '<project_name',
    @Project_Stream = @ProjectBinary,
    @operation_id = @operation_id out
```

## <a name="next-steps"></a>Nächste Schritte
- Erfahren Sie mehr über weitere Möglichkeiten, ein Paket bereitzustellen.
    - [Deploy an SSIS package with SSMS (Bereitstellen eines SSIS-Pakets mit SSMS)](./ssis-quickstart-deploy-ssms.md)
    - [Deploy an SSIS package with Transact-SQL (VS Code) (Bereitstellen eines SSIS-Pakets mit Transact-SQL [VS Code])](ssis-quickstart-deploy-tsql-vscode.md)
    - [Deploy an SSIS package from the command prompt (Bereitstellen eines SSIS-Pakets von der Befehlszeile aus)](./ssis-quickstart-deploy-cmdline.md)
    - [Deploy an SSIS package with PowerShell (Bereitstellen eines SSIS-Pakets mit PowerShell)](ssis-quickstart-deploy-powershell.md)
    - [Deploy an SSIS package with C# (Bereitstellen eines SSIS-Pakets mit C#)](./ssis-quickstart-deploy-dotnet.md) 
- Führen Sie ein bereitgestelltes Paket aus. Für die Ausführung eines Pakets können Sie aus mehreren Tools und Sprachen auswählen. Weitere Informationen finden Sie in den folgenden Artikeln:
    - [Run an SSIS package with SSMS](./ssis-quickstart-run-ssms.md) (Ausführen eines SSIS-Pakets mit SSMS)
    - [Run an SSIS package with Transact-SQL (SSMS) (Ausführen eines SSIS-Pakets mit Transact-SQL [SSMS])](./ssis-quickstart-run-tsql-ssms.md)
    - [Run an SSIS package with Transact-SQL (VS Code)](ssis-quickstart-run-tsql-vscode.md) (Ausführen eines SSIS-Pakets mit Transact-SQL [VS Code])
    - [Run an SSIS package from the command prompt](./ssis-quickstart-run-cmdline.md) (Ausführen eines SSIS-Pakets über die Eingabeaufforderung)
    - [Run an SSIS package with PowerShell](ssis-quickstart-run-powershell.md) (Ausführen eines SSIS-Pakets mit PowerShell)
    - [Run an SSIS package with C#](./ssis-quickstart-run-dotnet.md) (Ausführen eines SSIS-Pakets mit C#) 

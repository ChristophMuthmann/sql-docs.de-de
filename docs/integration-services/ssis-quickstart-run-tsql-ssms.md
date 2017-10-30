---
title: "Führen Sie ein SSIS-Paket mit Transact-SQL (SSMS) | Microsoft Docs"
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
ms.openlocfilehash: 1c656661f645ac9f5d1659800893290819525f39
ms.contentlocale: de-de
ms.lasthandoff: 09/22/2017

---
# <a name="run-an-ssis-package-from-ssms-with-transact-sql"></a>Ausführen eines SSIS-Pakets von SSMS mit Transact-SQL
Dieser Schnellstart veranschaulicht, wie SQL Server Management Studio (SSMS) zum Herstellen einer Verbindung mit dem SSIS-Katalogdatenbank und verwenden Sie Transact-SQL-Anweisungen zum Ausführen eines SSIS-Pakets im SSIS-Katalog gespeichert.

SQL Server Management Studio ist eine integrierte Umgebung für alle SQL-Infrastruktur von SQL Server mit SQL-Datenbank verwalten. Weitere Informationen über SSMS finden Sie unter [SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md).

## <a name="prerequisites"></a>Erforderliche Komponenten

Bevor Sie beginnen, stellen Sie sicher, dass Sie die neueste Version von SQL Server Management Studio (SSMS) verfügen. Informationen zum Herunterladen von SSMS finden Sie unter [Download SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

## <a name="connect-to-the-ssisdb-database"></a>Herstellen einer Verbindung mit dem SSISDB-Datenbank

Verwenden Sie SQL Server Management Studio zum Herstellen einer Verbindung im SSIS-Katalog auf dem Azure SQL-Datenbankserver. 

> [!NOTE]
> Ein Azure SQL-Datenbankserver wird Port 1433 überwacht. Wenn Sie, zur Verbindung mit eines Azure SQL-Datenbank-Servers innerhalb einer Unternehmens-Firewall versuchen muss diesen Port in der Unternehmensfirewall für Sie erfolgreich eine Verbindung herstellen geöffnet sein.

1. Öffnen Sie SQL Server Management Studio.

2. In der **Verbindung mit Server herstellen** Dialogfeld Geben Sie die folgende Informationen:

   | Einstellung       | Empfohlener Wert | Weitere Informationen | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Servertyp** | Datenbankmodul | Dieser Wert ist erforderlich. |
   | **Servername** | Die vollqualifizierten Servernamen | Wenn Sie die Verbindung mit einem Azure SQL-Datenbankserver herstellen, wird der Name im folgenden Format: `<server_name>.database.windows.net`. |
   | **Authentifizierung** | SQL Server-Authentifizierung | Dieser Schnellstart verwendet SQL-Authentifizierung. |
   | **Anmeldename** | Serveradmin-Kontos | Dies ist das Konto, das Sie angegeben werden, wenn Sie auf den Server erstellt haben. |
   | **Kennwort** | Das Kennwort für Ihr serveradmin-Kontos | Dies ist das Kennwort, das Sie angegeben werden, wenn Sie auf den Server erstellt haben. |

3.  Klicken Sie auf **Verbinden**. Die Objekt-Explorer-Fenster wird geöffnet, in SSMS.

4. Erweitern Sie im Objekt-Explorer **Integration Services-Kataloge** und schließlich **SSISDB** zum Anzeigen der Objekte in der SSIS-Katalogdatenbank.

## <a name="run-a-package"></a>Ausführen eines Pakets
Führen Sie den folgenden Transact-SQL-Code, um ein SSIS-Paket ausführen.

1.  Öffnen Sie ein neues Abfragefenster, und fügen Sie den folgenden Code, in SSMS. (Dieser Code ist die vom generierten Code der **Skript** option in der **Paketausführungs** Dialogfeld in SSMS.)

2.  Aktualisieren Sie die Parameterwerte in der `catalog.create_execution` für Ihr System die gespeicherte Prozedur.

3.  Stellen Sie sicher, dass die SSISDB der aktuellen Datenbank befindet.

4.  Führen Sie das Skript aus.

5. Aktualisieren Sie im Objekt-Explorer den Inhalt des **SSISDB** bei Bedarf und prüfen Sie das Projekt, das Sie bereitgestellt haben.

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
    - [Führen Sie ein SSIS-Paket mit Transact-SQL (Visual Studio-Code)](ssis-quickstart-run-tsql-vscode.md)
    - [Führen Sie ein SSIS-Paket von der Befehlszeile aus](./ssis-quickstart-run-cmdline.md)
    - [Führen Sie ein SSIS-Paket mit PowerShell](ssis-quickstart-run-powershell.md)
    - [Führen Sie ein SSIS-Paket mit c#](./ssis-quickstart-run-dotnet.md) 


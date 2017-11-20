---
title: Bereitstellen ein SSIS-Projekts mit Transact-SQL (SSMS) | Microsoft Docs
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.suite: sql
ms.custom: 
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 656e62f36446db4ef5b232129130a0253d2aebdf
ms.openlocfilehash: e97fb20f5b0ee10aa3e5de690676b7e0bb797b4c
ms.contentlocale: de-de
ms.lasthandoff: 09/22/2017

---
# <a name="deploy-an-ssis-project-from-ssms-with-transact-sql"></a>Bereitstellen eines SSIS-Projekts aus SSMS mit Transact-SQL

Dieser Schnellstart veranschaulicht, wie SQL Server Management Studio (SSMS) zum Herstellen einer Verbindung mit dem SSIS-Katalogdatenbank und verwenden dann Transact-SQL-Anweisungen, um ein SSIS-Projekt im SSIS-Katalog bereitstellen. 

> [!NOTE]
> In diesem Artikel beschriebene Methode ist nicht verfügbar, bei der Herstellung einer Verbindung mit eines Azure SQL-Datenbankserver mit SSMS. Die `catalog.deploy_project` gespeicherte Prozedur erwartet den Pfad zu der `.ispac` Datei im Dateisystem lokalen (lokal).

SQL Server Management Studio ist eine integrierte Umgebung für alle SQL-Infrastruktur von SQL Server mit SQL-Datenbank verwalten. Weitere Informationen über SSMS finden Sie unter [SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md).

## <a name="prerequisites"></a>Erforderliche Komponenten

Bevor Sie beginnen, stellen Sie sicher, dass Sie die neueste Version von SQL Server Management Studio haben. Informationen zum Herunterladen von SSMS finden Sie unter [Download SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

## <a name="connect-to-the-ssis-catalog-database"></a>Herstellen einer Verbindung mit dem SSIS-Katalogdatenbank

Verwenden Sie SQL Server Management Studio zum Herstellen einer Verbindung im SSIS-Katalog. 

> [!NOTE]
> Ein Azure SQL-Datenbankserver wird Port 1433 überwacht. Wenn Sie, zur Verbindung mit eines Azure SQL-Datenbank-Servers innerhalb einer Unternehmens-Firewall versuchen muss diesen Port in der Unternehmensfirewall für Sie erfolgreich eine Verbindung herstellen geöffnet sein.

1. Öffnen Sie SQL Server Management Studio.

2. In der **Verbindung mit Server herstellen** Dialogfeld Geben Sie die folgende Informationen:

   | Einstellung       | Empfohlener Wert | Weitere Informationen | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Servertyp** | Datenbankmodul | Dieser Wert ist erforderlich. |
   | **Servername** | Die vollqualifizierten Servernamen |  |
   | **Authentifizierung** | SQL Server-Authentifizierung | Dieser Schnellstart verwendet SQL-Authentifizierung. |
   | **Anmeldename** | Serveradmin-Kontos | Dies ist das Konto, das Sie angegeben werden, wenn Sie auf den Server erstellt haben. |
   | **Kennwort** | Das Kennwort für Ihr serveradmin-Kontos | Dies ist das Kennwort, das Sie angegeben werden, wenn Sie auf den Server erstellt haben. |

3. Klicken Sie auf **Verbinden**. Die Objekt-Explorer-Fenster wird geöffnet, in SSMS. 

4. Erweitern Sie im Objekt-Explorer **Integration Services-Kataloge** und schließlich **SSISDB** zum Anzeigen der Objekte in der SSIS-Katalogdatenbank.

## <a name="run-the-t-sql-code"></a>Führen Sie den T-SQL-code
Führen Sie den folgenden Transact-SQL-Code, um ein SSIS-Projekt bereitstellen.

1.  Öffnen Sie ein neues Abfragefenster, und fügen Sie den folgenden Code, in SSMS.

2.  Aktualisieren Sie die Parameterwerte in der `catalog.deploy_project` für Ihr System die gespeicherte Prozedur.

3.  Stellen Sie sicher, dass die SSISDB der aktuellen Datenbank befindet.

4.  Führen Sie das Skript aus.

5. Aktualisieren Sie im Objekt-Explorer den Inhalt des **SSISDB** bei Bedarf und prüfen Sie das Projekt, das Sie bereitgestellt haben.

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
- Erwägen Sie andere Verfahren zum Bereitstellen eines Pakets aus.
    - [Bereitstellen eines SSIS-Pakets mit SSMS](./ssis-quickstart-deploy-ssms.md)
    - [Bereitstellen eines SSIS-Pakets mit Transact-SQL (Visual Studio-Code)](ssis-quickstart-deploy-tsql-vscode.md)
    - [Bereitstellen eines SSIS-Pakets von der Befehlszeile aus](./ssis-quickstart-deploy-cmdline.md)
    - [Bereitstellen eines SSIS-Pakets mit PowerShell](ssis-quickstart-deploy-powershell.md)
    - [Bereitstellen eines SSIS-Pakets mit c#](./ssis-quickstart-deploy-dotnet.md) 
- Führen Sie ein bereitgestelltes Paket. Um ein Paket auszuführen, können Sie über mehrere Tools und Sprachen auswählen. Weitere Informationen finden Sie unter den folgenden Artikeln:
    - [Führen Sie ein SSIS-Paket mit SSMS](./ssis-quickstart-run-ssms.md)
    - [Führen Sie ein SSIS-Paket mit Transact-SQL (SSMS)](./ssis-quickstart-run-tsql-ssms.md)
    - [Führen Sie ein SSIS-Paket mit Transact-SQL (Visual Studio-Code)](ssis-quickstart-run-tsql-vscode.md)
    - [Führen Sie ein SSIS-Paket von der Befehlszeile aus](./ssis-quickstart-run-cmdline.md)
    - [Führen Sie ein SSIS-Paket mit PowerShell](ssis-quickstart-run-powershell.md)
    - [Führen Sie ein SSIS-Paket mit c#](./ssis-quickstart-run-dotnet.md) 


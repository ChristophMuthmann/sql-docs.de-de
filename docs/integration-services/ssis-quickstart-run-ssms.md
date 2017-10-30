---
title: "Führen Sie ein SSIS-Paket mit SSMS | Microsoft Docs"
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
ms.openlocfilehash: bbc17907311785ef98560493cb453b7b9b6d1556
ms.contentlocale: de-de
ms.lasthandoff: 09/22/2017

---
# <a name="run-an-ssis-package-with-sql-server-management-studio-ssms"></a>Führen Sie ein SSIS-Paket mit SQL Server Management Studio (SSMS)
Dieser Schnellstart veranschaulicht, wie SQL Server Management Studio (SSMS) zum Herstellen einer Verbindung mit dem SSIS-Katalogdatenbank, und führen Sie ein SSIS-Paket im SSIS-Katalog im Objekt-Explorer in SSMS gespeichert.

SQL Server Management Studio ist eine integrierte Umgebung für alle SQL-Infrastruktur von SQL Server mit SQL-Datenbank verwalten. Weitere Informationen über SSMS finden Sie unter [SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md).

## <a name="prerequisites"></a>Erforderliche Komponenten

Bevor Sie beginnen, stellen Sie sicher, dass Sie die neueste Version von SQL Server Management Studio (SSMS) verfügen. Informationen zum Herunterladen von SSMS finden Sie unter [Download SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

## <a name="connect-to-the-ssisdb-database"></a>Herstellen einer Verbindung mit dem SSISDB-Datenbank

Verwenden Sie SQL Server Management Studio zum Herstellen einer Verbindung im SSIS-Katalog. 

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

3. Klicken Sie auf **Verbinden**. Die Objekt-Explorer-Fenster wird geöffnet, in SSMS. 

4. Erweitern Sie im Objekt-Explorer **Integration Services-Kataloge** und schließlich **SSISDB** zum Anzeigen der Objekte in der SSIS-Katalogdatenbank.

## <a name="run-a-package"></a>Ausführen eines Pakets

1. Wählen Sie im Objekt-Explorer das Paket, das Sie ausführen möchten.

2. Mit der rechten Maustaste, und wählen Sie **Execute**. Die **Paketausführungs** Dialogfeld wird geöffnet.

3.  Konfigurieren Sie die Ausführung des Pakets mit den Einstellungen auf der **Parameter**, **Verbindungs-Manager**, und **erweitert** Registerkarten im Dialogfeld Paket ausführen.

4.  Klicken Sie auf OK, um das Paket ausgeführt werden.

## <a name="next-steps"></a>Nächste Schritte
- Erwägen Sie andere Verfahren zum Ausführen eines Pakets aus.
    - [Führen Sie ein SSIS-Paket mit Transact-SQL (SSMS)](./ssis-quickstart-run-tsql-ssms.md)
    - [Führen Sie ein SSIS-Paket mit Transact-SQL (Visual Studio-Code)](ssis-quickstart-run-tsql-vscode.md)
    - [Führen Sie ein SSIS-Paket von der Befehlszeile aus](./ssis-quickstart-run-cmdline.md)
    - [Führen Sie ein SSIS-Paket mit PowerShell](ssis-quickstart-run-powershell.md)
    - [Führen Sie ein SSIS-Paket mit c#](./ssis-quickstart-run-dotnet.md) 


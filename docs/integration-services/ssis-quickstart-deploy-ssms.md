---
title: Bereitstellen ein SSIS-Projekts mit SSMS | Microsoft Docs
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
ms.openlocfilehash: b9729343ab14563ee6264795d6f098f3c22e91bf
ms.contentlocale: de-de
ms.lasthandoff: 09/22/2017

---
# <a name="deploy-an-ssis-project-with-sql-server-management-studio-ssms"></a>Bereitstellen eines SSIS-Projekts mit SQL Server Management Studio (SSMS)
Dieser Schnellstart veranschaulicht, wie SQL Server Management Studio (SSMS) zum Herstellen einer Verbindung mit dem SSIS-Katalogdatenbank, und führen Sie die Integration Services Deployment Wizard zum Bereitstellen eines SSIS-Projekts im SSIS-Katalog. 

SQL Server Management Studio ist eine integrierte Umgebung für alle SQL-Infrastruktur von SQL Server mit SQL-Datenbank verwalten. Weitere Informationen über SSMS finden Sie unter [SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md).

## <a name="prerequisites"></a>Erforderliche Komponenten

Bevor Sie beginnen, stellen Sie sicher, dass Sie die neueste Version von SQL Server Management Studio haben. Informationen zum Herunterladen von SSMS finden Sie unter [Download SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

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

## <a name="start-the-integration-services-deployment-wizard"></a>Starten Sie den Bereitstellungs-Assistenten von Integration Services
1. Im Objekt-Explorer mit der **Integration Services-Kataloge** Knoten und die **SSISDB** Kategorie erweitert ist, erweitern Sie in einem Projektordner.

2.  Wählen Sie die **Projekte** Knoten.

3.  Mit der rechten Maustaste auf die **Projekte** Knoten, und wählen **Projekt bereitstellen**. Integration Services-Bereitstellungs-Assistent wird geöffnet. Sie können ein Projekt aus dem aktuellen Katalog oder aus dem Dateisystem bereitstellen.

## <a name="deploy-a-project-with-the-wizard"></a>Bereitstellen eines Projekts mit dem Assistenten
1. Auf der **Einführung** Seite des Assistenten, überprüfen Sie in der Einführung. Klicken Sie auf **Weiter** So öffnen die **Quelle auswählen** Seite.

2. Auf der **Quelle auswählen** Seite, wählen Sie die vorhandene SSIS-Projekt bereitstellen.
    -   Um eine von Ihnen erstellte Projektbereitstellungsdatei bereitzustellen, wählen Sie **Projektbereitstellungsdatei** aus, und geben Sie den Pfad für die ISPAC-Datei ein.
    -   Wählen Sie zum Bereitstellen eines Projekts, die sich in einem SSIS-Katalog befindet, **Integration Services-Katalog**, und geben Sie dann den Servernamen und den Pfad zum Projekt im Katalog.
    Klicken Sie auf **Weiter** , um die Seite **Ziel auswählen** zu sehen.
  
3.  Auf der **Ziel auswählen** Seite, wählen Sie das Ziel für das Projekt.
    -   Geben Sie den vollqualifizierten Servernamen ein. Wenn der Zielserver eine Azure SQL-Datenbankserver ist, wird der Name im folgenden Format: `<server_name>.database.windows.net`.
    -   Klicken Sie dann auf **Durchsuchen** um den Zielordner im SSISDB auszuwählen.
    Klicken Sie auf **Weiter** So öffnen die **Überprüfung** Seite.  
  
4.  Auf der **überprüfen** überprüfen Sie die Einstellungen, die Sie ausgewählt haben.
    -   Sie können Ihre Auswahl ändern, indem Sie auf **Zurück**klicken oder indem Sie auf einen der Schritte im linken Bereich klicken.
    -   Klicken Sie auf **Bereitstellen** , um den Bereitstellungsprozess zu starten.
  
5.  Nachdem der Bereitstellungsvorgang abgeschlossen ist, ist die **Ergebnisse** -Seite wird geöffnet. Diese Seite zeigt an, ob die einzelnen Aktionen erfolgreich ausgeführt wurden oder ob Fehler aufgetreten sind.
    -   Wenn der Vorgang fehlgeschlagen ist, klicken Sie auf **Fehler** in der **Ergebnis** Spalte um eine Erklärung des Fehlers anzuzeigen.
    -   Klicken Sie optional auf **Bericht speichern...**  um die Ergebnisse als XML-Datei zu speichern.
    -   Klicken Sie auf **schließen** um den Assistenten zu beenden.

## <a name="next-steps"></a>Nächste Schritte
- Erwägen Sie andere Verfahren zum Bereitstellen eines Pakets aus.
    - [Bereitstellen eines SSIS-Pakets mit Transact-SQL (SSMS)](./ssis-quickstart-deploy-tsql-ssms.md)
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


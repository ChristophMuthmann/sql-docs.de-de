---
title: Bereitstellen eines SSIS-Projekts mit SSMS | Microsoft-Dokumentation
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: quick-start
ms.suite: sql
ms.custom: 
ms.technology: integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 151089d319a1106f81426beee4aa2989bc72b978
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="deploy-an-ssis-project-with-sql-server-management-studio-ssms"></a>Bereitstellen eines SSIS-Projekts mit SQL Server Management Studio (SSMS)
In diesem Schnellstart wird erläutert, wie Sie SQL Server Management Studio (SSMS) verwenden müssen, um eine Verbindung mit der SSIS-Katalogdatenbank herzustellen, und wie Sie anschließend Bereitstellungs-Assistent für Integration Services verwenden müssen, um ein im SSIS-Katalog gespeichertes SSIS-Projekt bereitzustellen. 

SQL Server Management Studio ist eine integrierte Umgebung zum Verwalten jeder beliebigen SQL-Infrastruktur, von SQL Server bis hin zur SQL-Datenbank. Weitere Informationen zu SSMS finden Sie unter [SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md).

## <a name="prerequisites"></a>Voraussetzungen

Prüfen Sie, ob Sie über die neueste Version von SQL Server Management Studio verfügen, bevor Sie beginnen. Wie Sie SSMS herunterladen, erfahren Sie unter [Herunterladen von SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

## <a name="connect-to-the-ssisdb-database"></a>Herstellen einer Verbindung mit der SSISDB-Datenbank

Verwenden Sie SQL Server Management Studio, um eine Verbindung mit dem SSIS-Katalog einzurichten. 

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

3. Klicken Sie auf **Verbinden**. Das Fenster „Objekt-Explorer“ wird in SSMS geöffnet. 

4. Erweitern Sie im Objekt-Explorer **Integration Services-Kataloge** und dann **SSISDB**, um die Objekte in der SSIS-Katalogdatenbank anzuzeigen.

## <a name="start-the-integration-services-deployment-wizard"></a>Starten des Bereitstellungs-Assistenten für Integration Services
1. Erweitern Sie im Objekt-Explorer den Knoten **Integration Services-Kataloge**, **SSISDB** und dann einen Projektorder.

2.  Wählen Sie den Knoten **Projekte** aus.

3.  Klicken Sie mit der rechten Maustaste auf den Knoten **Projekte**, und wählen Sie **Projekt bereitstellen** aus. Der Bereitstellungs-Assistent für Integration Services wird geöffnet. Sie können ein Projekt aus dem aktuellen Katalog oder dem Dateisystem bereitstellen.

## <a name="deploy-a-project-with-the-wizard"></a>Bereitstellen eines Projekts mit dem Assistenten
1. Lesen Sie auf der Seite **Einführung** des Assistenten die Einführung. Klicken Sie auf **Weiter**, um die Seite **Quelle auswählen** zu öffnen.

2. Wählen Sie auf der Seite **Quelle auswählen** das vorhandene SSIS-Projekt aus, das bereitgestellt werden soll.
    -   Um eine von Ihnen erstellte Projektbereitstellungsdatei bereitzustellen, wählen Sie **Projektbereitstellungsdatei** aus, und geben Sie den Pfad für die ISPAC-Datei ein.
    -   Um ein Projekt bereitzustellen, das sich in einem SSIS-Katalog befindet, wählen Sie **Integration Services-Katalog** aus und geben dann den Servernamen und den Pfad zum Projekt im Katalog ein.
    Klicken Sie auf **Weiter** , um die Seite **Ziel auswählen** zu sehen.
  
3.  Wählen Sie auf der Seite **Ziel auswählen** das Ziel für das Projekt aus.
    -   Geben Sie den vollqualifizierten Servernamen ein. Wenn es sich dem Zielserver um einen Azure SQL-Datenbankserver handelt, ist der Name im Format `<server_name>.database.windows.net`.
    -   Klicken Sie dann auf **Durchsuchen**, um den Zielordner in SSISDB auszuwählen.
    Klicken Sie auf **Weiter**, um die Seite **Überprüfen** zu öffnen.  
  
4.  Überprüfen Sie auf der Seite **Überprüfen** die Einstellungen, die Sie ausgewählt haben.
    -   Sie können Ihre Auswahl ändern, indem Sie auf **Zurück**klicken oder indem Sie auf einen der Schritte im linken Bereich klicken.
    -   Klicken Sie auf **Bereitstellen** , um den Bereitstellungsprozess zu starten.
  
5.  Nachdem der Bereitstellungsvorgang abgeschlossen ist, wird die Seite **Ergebnisse** geöffnet. Diese Seite zeigt an, ob die einzelnen Aktionen erfolgreich ausgeführt wurden oder ob Fehler aufgetreten sind.
    -   Ist die Aktion fehlerhaft, klicken Sie in der Spalte **Ergebnis** auf **Fehler**, um eine Erläuterung zum Fehler anzuzeigen.
    -   Klicken Sie auf **Bericht speichern...**, um die Ergebnisse in einer XML-Datei zu speichern.
    -   Klicken Sie auf **Schließen**, um den Assistenten zu beenden.

## <a name="next-steps"></a>Nächste Schritte
- Erfahren Sie mehr über weitere Möglichkeiten, ein Paket bereitzustellen.
    - [Deploy an SSIS package with Transact-SQL (SSMS) (Bereitstellen eines SSIS-Pakets mit Transact-SQL [SSMS])](./ssis-quickstart-deploy-tsql-ssms.md)
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

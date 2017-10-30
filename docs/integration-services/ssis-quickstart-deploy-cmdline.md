---
title: Bereitstellen ein SSIS-Projekts von der Befehlszeile aus | Microsoft Docs
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
ms.sourcegitcommit: bc1321dd91a0fcb7ab76b207301c6302bb3a5e64
ms.openlocfilehash: 0f1c7733f0ce6b132c209961a1fd12da80cbd282
ms.contentlocale: de-de
ms.lasthandoff: 10/06/2017

---
# <a name="deploy-an-ssis-project-from-the-command-prompt-with-isdeploymentwizardexe"></a>Bereitstellen eines SSIS-Projekts von der Befehlszeile aus mit ISDeploymentWizard.exe
Dieser Schnellstart-Lernprogramm veranschaulicht, wie ein SSIS-Projekt, von der Befehlszeile aus bereitstellen, indem Sie mit dem Integration Services-Bereitstellungs-Assistenten `ISDeploymentWizard.exe`.

Weitere Informationen zu den Bereitstellungs-Assistenten von Integration Services, finden Sie unter [Integration Services Deployment Wizard](packages/deploy-integration-services-ssis-projects-and-packages.md#integration-services-deployment-wizard).

## <a name="start-the-integration-services-deployment-wizard"></a>Starten Sie den Bereitstellungs-Assistenten von Integration Services
1. Öffnen Sie ein Eingabeaufforderungsfenster.

2. Führen Sie `ISDeploymentWizard.exe` aus. Integration Services-Bereitstellungs-Assistent wird geöffnet.

    Falls der Ordner, die enthält `ISDeploymentWizard.exe` befindet sich nicht in Ihrer `path` Umgebungsvariablen müssen unter Umständen verwendet die `cd` Befehl aus, um in das Verzeichnis zu ändern. Für SQL Server 2017 dieser Ordner ist in der Regel `C:\Program Files (x86)\Microsoft SQL Server\140\DTS\Binn`.

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
    - [Bereitstellen eines SSIS-Pakets mit SSMS](./ssis-quickstart-deploy-ssms.md)
    - [Bereitstellen eines SSIS-Pakets mit Transact-SQL (SSMS)](./ssis-quickstart-deploy-tsql-ssms.md)
    - [Bereitstellen eines SSIS-Pakets mit Transact-SQL (Visual Studio-Code)](ssis-quickstart-deploy-tsql-vscode.md)
    - [Bereitstellen eines SSIS-Pakets mit PowerShell](ssis-quickstart-deploy-powershell.md)
    - [Bereitstellen eines SSIS-Pakets mit c#](./ssis-quickstart-deploy-dotnet.md) 
- Führen Sie ein bereitgestelltes Paket. Um ein Paket auszuführen, können Sie über mehrere Tools und Sprachen auswählen. Weitere Informationen finden Sie unter den folgenden Artikeln:
    - [Führen Sie ein SSIS-Paket mit SSMS](./ssis-quickstart-run-ssms.md)
    - [Führen Sie ein SSIS-Paket mit Transact-SQL (SSMS)](./ssis-quickstart-run-tsql-ssms.md)
    - [Führen Sie ein SSIS-Paket mit Transact-SQL (Visual Studio-Code)](ssis-quickstart-run-tsql-vscode.md)
    - [Führen Sie ein SSIS-Paket von der Befehlszeile aus](./ssis-quickstart-run-cmdline.md)
    - [Führen Sie ein SSIS-Paket mit PowerShell](ssis-quickstart-run-powershell.md)
    - [Führen Sie ein SSIS-Paket mit c#](./ssis-quickstart-run-dotnet.md) 


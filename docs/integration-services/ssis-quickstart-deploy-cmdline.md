---
title: Bereitstellen eines SSIS-Projekts über die Eingabeaufforderung | Microsoft-Dokumentation
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: non-specific
ms.suite: sql
ms.custom: ''
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 65a94a74659cefdb1fbed508836d45cacff1cf65
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="deploy-an-ssis-project-from-the-command-prompt-with-isdeploymentwizardexe"></a>Bereitstellen eines SSIS-Projekts über die Eingabeaufforderung mit ISDeploymentWizard.exe
Dieses Schnellstarttutorial zeigt, wie Sie ein SSIS-Projekt über die Eingabeaufforderung bereitstellen, indem Sie den Bereitstellungs-Assistenten für Integration Services, `ISDeploymentWizard.exe`, ausführen.

Weitere Informationen zum Bereitstellungs-Assistenten für Integration Services finden Sie unter [Bereitstellungs-Assistent für Integration Services](packages/deploy-integration-services-ssis-projects-and-packages.md#integration-services-deployment-wizard).

## <a name="start-the-integration-services-deployment-wizard"></a>Starten des Bereitstellungs-Assistenten für Integration Services
1. Öffnen Sie ein Eingabeaufforderungsfenster.

2. Führen Sie `ISDeploymentWizard.exe` aus. Der Bereitstellungs-Assistent für Integration Services wird geöffnet.

    Wenn sich der Ordner, der `ISDeploymentWizard.exe` enthält, nicht in Ihrer Umgebungsvariable `path` befindet, müssen Sie möglicherweise mit dem Befehl `cd` in das Verzeichnis wechseln. Bei SQL Server 2017 lautet dieser Ordner in der Regel `C:\Program Files (x86)\Microsoft SQL Server\140\DTS\Binn`.

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
    - [Deploy an SSIS package with SSMS (Bereitstellen eines SSIS-Pakets mit SSMS)](./ssis-quickstart-deploy-ssms.md)
    - [Deploy an SSIS package with Transact-SQL (SSMS) (Bereitstellen eines SSIS-Pakets mit Transact-SQL [SSMS])](./ssis-quickstart-deploy-tsql-ssms.md)
    - [Deploy an SSIS package with Transact-SQL (VS Code) (Bereitstellen eines SSIS-Pakets mit Transact-SQL [VS Code])](ssis-quickstart-deploy-tsql-vscode.md)
    - [Deploy an SSIS package with PowerShell (Bereitstellen eines SSIS-Pakets mit PowerShell)](ssis-quickstart-deploy-powershell.md)
    - [Deploy an SSIS package with C# (Bereitstellen eines SSIS-Pakets mit C#)](./ssis-quickstart-deploy-dotnet.md) 
- Führen Sie ein bereitgestelltes Paket aus. Für die Ausführung eines Pakets können Sie aus mehreren Tools und Sprachen auswählen. Weitere Informationen finden Sie in den folgenden Artikeln:
    - [Run an SSIS package with SSMS](./ssis-quickstart-run-ssms.md) (Ausführen eines SSIS-Pakets mit SSMS)
    - [Run an SSIS package with Transact-SQL (SSMS) (Ausführen eines SSIS-Pakets mit Transact-SQL [SSMS])](./ssis-quickstart-run-tsql-ssms.md)
    - [Run an SSIS package with Transact-SQL (VS Code)](ssis-quickstart-run-tsql-vscode.md) (Ausführen eines SSIS-Pakets mit Transact-SQL [VS Code])
    - [Run an SSIS package from the command prompt](./ssis-quickstart-run-cmdline.md) (Ausführen eines SSIS-Pakets über die Eingabeaufforderung)
    - [Run an SSIS package with PowerShell](ssis-quickstart-run-powershell.md) (Ausführen eines SSIS-Pakets mit PowerShell)
    - [Run an SSIS package with C#](./ssis-quickstart-run-dotnet.md) (Ausführen eines SSIS-Pakets mit C#) 

---
title: "Bereitstellen, ausführen und überwachen Sie ein SSIS-Paket in Azure | Microsoft Docs"
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
ms.sourcegitcommit: 560965a241b24a09f50a23faf63ce74d0049d5a7
ms.openlocfilehash: 2e16666c412870cc55024e7156752f43ddbc1800
ms.contentlocale: de-de
ms.lasthandoff: 10/13/2017

---
# <a name="deploy-run-and-monitor-an-ssis-package-on-azure"></a>Bereitstellen Sie, führen Sie aus und überwachen Sie ein SSIS-Paket in Azure
In diesem Lernprogramm wird gezeigt, wie ein SQL Server Integration Services-Projekt mit der Datenbank SSISDB-Katalog für Azure SQL-Datenbank bereitstellen, Ausführen eines Pakets in der Azure-SSIS-Integrationslaufzeit, und überwachen die Ausführung des Pakets.

## <a name="prerequisites"></a>Erforderliche Komponenten

Bevor Sie beginnen, stellen Sie sicher, dass Sie Version 17.2 oder höher von SQL Server Management Studio verwenden. Informationen zum Herunterladen der neuesten Version von SSMS finden Sie unter [Download SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

Stellen Sie außerdem sicher, dass Sie die SSISDB-Datenbank einrichten und der Azure-SSIS-Integrationslaufzeit bereitgestellt haben. Informationen zum Bereitstellen von SSIS in Azure finden Sie unter [Lift- and -Shift SQL Server Integration Services (SSIS)-Pakete Azure](https://docs.microsoft.com/en-us/azure/data-factory/tutorial-deploy-ssis-packages-azure).

## <a name="connect-to-the-ssisdb-database"></a>Herstellen einer Verbindung mit dem SSISDB-Datenbank

Verwenden Sie SQL Server Management Studio, um im SSIS-Katalog auf dem Azure SQL-Datenbankserver herstellen. Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit der Datenbank SSISDB-Katalog in Azure](ssis-azure-connect-to-catalog-database.md).

> [!IMPORTANT]
> Ein Azure SQL-Datenbankserver wird Port 1433 überwacht. Wenn Sie versuchen, die Verbindung mit eines Azure SQL-Datenbank-Servers innerhalb einer Unternehmens-Firewall, muss diesen Port in der Unternehmens-Firewall für Sie erfolgreich eine Verbindung herstellen geöffnet sein.

1. Öffnen Sie SQL Server Management Studio.

2. **Herstellen einer Verbindung mit dem Server**. In der **Verbindung mit Server herstellen** Dialogfeld Geben Sie die folgende Informationen:

   | Einstellung       | Empfohlener Wert | Description | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Servertyp** | Datenbankmodul | Dieser Wert ist erforderlich. |
   | **Servername** | Die vollqualifizierten Servernamen | Der Name muss im folgenden Format: **mysqldbserver.database.windows.net**. Wenn Sie den Namen des Servers benötigen, finden Sie unter [Herstellen einer Verbindung mit der Datenbank SSISDB-Katalog in Azure](ssis-azure-connect-to-catalog-database.md). |
   | **Authentifizierung** | SQL Server-Authentifizierung | Dieser Schnellstart verwendet SQL-Authentifizierung. |
   | **Anmeldename** | Serveradmin-Kontos | Dies ist das Konto, das Sie angegeben werden, wenn Sie auf den Server erstellt haben. |
   | **Kennwort** | Das Kennwort für Ihr serveradmin-Kontos | Dies ist das Kennwort, das Sie angegeben werden, wenn Sie auf den Server erstellt haben. |

3. **Herstellen einer Verbindung mit dem SSISDB-Datenbank**. Wählen Sie **Optionen** , erweitern die **Verbindung mit Server herstellen** (Dialogfeld). In den erweiterten **Verbindung mit Server herstellen** wählen Sie im Dialogfeld die **Verbindungseigenschaften** Registerkarte. In der **mit Datenbank verbinden** aktivieren, oder geben Sie `SSISDB`.

4. Wählen Sie dann **verbinden**. Die Objekt-Explorer-Fenster wird geöffnet, in SSMS. 

5. Erweitern Sie im Objekt-Explorer **Integration Services-Kataloge** und schließlich **SSISDB** zum Anzeigen der Objekte in der SSIS-Katalogdatenbank.

## <a name="deploy-a-project"></a>Bereitstellen eines Projekts

### <a name="start-the-integration-services-deployment-wizard"></a>Starten Sie den Bereitstellungs-Assistenten von Integration Services
1. Im Objekt-Explorer in SSMS mit der **Integration Services-Kataloge** Knoten und die **SSISDB** Knoten erweitert, erweitern Sie einen Projektordner.

2.  Wählen Sie die **Projekte** Knoten.

3.  Mit der rechten Maustaste auf die **Projekte** Knoten, und wählen **Projekt bereitstellen**. Integration Services-Bereitstellungs-Assistent wird geöffnet. Sie können ein Projekt aus einer Datenbank SSIS-Katalog oder aus dem Dateisystem bereitstellen.

### <a name="deploy-a-project-with-the-deployment-wizard"></a>Bereitstellen eines Projekts mit dem Bereitstellungs-Assistenten
1. Auf der **Einführung** Seite des Bereitstellungs-Assistenten, überprüfen Sie in der Einführung. Wählen Sie **Weiter** So öffnen die **Quelle auswählen** Seite.

2. Auf der **Quelle auswählen** Seite, wählen Sie die vorhandene SSIS-Projekt bereitstellen.
    -   Um eine von Ihnen erstellte Projektbereitstellungsdatei bereitzustellen, wählen Sie **Projektbereitstellungsdatei** aus, und geben Sie den Pfad für die ISPAC-Datei ein.
    -   Wählen Sie zum Bereitstellen eines Projekts, die sich in einem SSIS-Katalog befindet, **Integration Services-Katalog**, und geben Sie dann den Servernamen und den Pfad zum Projekt im Katalog.
    -   Wählen Sie **Weiter** , finden Sie unter der **Ziel auswählen** Seite.
  
3.  Auf der **Ziel auswählen** Seite, wählen Sie das Ziel für das Projekt.
    -   Geben Sie den vollqualifizierten Servernamen im Format `<server_name>.database.windows.net`.
    -   Wählen Sie dann **Durchsuchen** um den Zielordner im SSISDB auszuwählen.
    -   Wählen Sie **Weiter** So öffnen die **Überprüfung** Seite.  
  
4.  Auf der **überprüfen** überprüfen Sie die Einstellungen, die Sie ausgewählt haben.
    -   Sie können Ihre Auswahl ändern, indem Sie auswählen **vorherige**, oder durch Auswahl einer der Schritte im linken Bereich.
    -   Wählen Sie **bereitstellen** um den Bereitstellungsprozess zu starten.
  
5.  Nachdem der Bereitstellungsvorgang abgeschlossen ist, ist die **Ergebnisse** -Seite wird geöffnet. Diese Seite zeigt an, ob die einzelnen Aktionen erfolgreich ausgeführt wurden oder ob Fehler aufgetreten sind.
    -   Wenn Fehler bei der Aktion auswählen **Fehler** in der **Ergebnis** Spalte um eine Erklärung des Fehlers anzuzeigen.
    -   Wählen Sie optional **Bericht speichern...**  um die Ergebnisse als XML-Datei zu speichern.
    -   Wählen Sie **schließen** um den Assistenten zu beenden.

## <a name="run-a-package"></a>Ausführen eines Pakets

1. Wählen Sie im Objekt-Explorer in SSMS das Paket, das Sie ausführen möchten.

2. Mit der rechten Maustaste, und wählen Sie **Execute** So öffnen die **Paketausführungs** (Dialogfeld).

3.  In der **Paketausführungs** Dialogfeld Feld, konfigurieren Sie die Ausführung des Pakets mit den Einstellungen auf der **Parameter**, **Verbindungs-Manager**, und **erweitert**  Registerkarten.

4.  Wählen Sie **OK** zum Ausführen des Pakets.

## <a name="monitor-the-running-package-in-ssms"></a>Überwachen des ausgeführten Pakets in SSMS

Verwenden Sie zum Anzeigen des Status der derzeit ausgeführten Integration Services-Vorgänge auf dem Integration Services-Server, z. B. Bereitstellung, Überprüfung und Ausführung des Pakets, das **aktive Vorgänge** Dialogfeld in SSMS. So öffnen die **aktive Vorgänge** (Dialogfeld), mit der rechten Maustaste **SSISDB**, und wählen Sie dann **aktive Vorgänge**.

Sie können auch ein Paket auswählen, in Objekt-Explorer mit der rechten Maustaste, und wählen **Berichte**, klicken Sie dann **Standardberichte**, klicken Sie dann **alle Ausführungen**.

Weitere Informationen zum Überwachen von ausgeführter Paketen in SSMS finden Sie unter [Monitor ausgeführte Pakete und andere Vorgänge](https://docs.microsoft.com/en-us/sql/integration-services/performance/monitor-running-packages-and-other-operations).

## <a name="monitor-the-azure-ssis-integration-runtime"></a>Überwachen der Azure-SSIS-Integrationslaufzeit

Um Statusinformationen zu den Azure-SSIS-Integrationslaufzeit erhalten, in denen Pakete ausgeführt werden, verwenden Sie die folgenden PowerShell-Befehle: Geben Sie für jeden der Befehle, die Namen der Data Factory, die Azure-SSIS-IR und die Ressourcengruppe.

### <a name="get-metadata-about-the-azure-ssis-integration-runtime"></a>Abrufen von Metadaten zur Laufzeit Azure-SSIS-Integration

```powershell
Get-AzureRmDataFactoryV2IntegrationRuntime -DataFactoryName $DataFactoryName -Name $AzureSsisIRName -ResourceGroupName $ResourceGroupName
```

### <a name="get-the-status-of-the-azure-ssis-integration-runtime"></a>Rufen Sie den Status der Azure-SSIS-Integrationslaufzeit

```powershell
Get-AzureRmDataFactoryV2IntegrationRuntime -Status -DataFactoryName $DataFactoryName -Name $AzureSsisIRName -ResourceGroupName $ResourceGroupName
```

## <a name="next-steps"></a>Nächste Schritte
- Informationen Sie zum Planen der Ausführung des Pakets. Weitere Informationen finden Sie unter [Zeitplan SSIS-paketausführung in Azure](ssis-azure-schedule-packages.md)


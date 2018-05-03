---
title: Migration von SQL Server Integration Services-Workloads in die Cloud per Lift & Shift | Microsoft-Dokumentation
ms.date: 04/13/2018
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: ''
ms.component: lift-shift
ms.suite: sql
ms.custom: ''
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8fb064a5efe77b9b273234f8ccd4f9760a128d92
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="lift-and-shift-sql-server-integration-services-workloads-to-the-cloud"></a>Migration von SQL Server Integration Services-Workloads in die Cloud per Lift & Shift
Sie können Ihre SQL Server Integration Services-Pakete und -Workloads (SSIS) nun in die Azure-Cloud verschieben.
-   Speichern und verwalten Sie SSIS-Projekte und -Pakete in der SSIS-Katalogdatenbank (SSISDB) in Azure SQL-Datenbank oder verwaltete SQL-Datenbank-Instanz (Vorschauversion).
-   Führen Sie Pakete in einer Instanz von Azure SSIS Integration Runtime aus, die mit Version 2 von Azure Data Factory eingeführt wurde.
-   Verwenden Sie vertraute Tools für diese allgemeinen Aufgaben, z.B. SQL Server Management Studio (SSMS).

## <a name="benefits"></a>Vorteile
Das Verschieben Ihrer SSIS-Workload in Azure hat folgende potenzielle Vorteile:
-   **Verringern Sie Betriebskosten** und den Aufwand der Verwaltung der Infrastruktur, der anfällt, wenn Sie SSIS lokal oder auf virtuellen Azure-Computern ausführen.
-   **Erhöhen Sie die Hochverfügbarkeit** und die Hochverfügbarkeitsfeatures von Azure und Azure SQL-Datenbank durch die Möglichkeit, mehrere Knoten pro Cluster anzugeben.
-   **Erhöhen Sie die Skalierbarkeit** durch die Möglichkeit, mehrere Kerne pro Knoten (zentrales Hochskalieren) und mehrere Knoten pro Cluster (horizontales Hochskalieren) anzugeben.

## <a name="architecture-overview"></a>Übersicht über die Architektur
In der folgenden Tabelle werden die Unterschiede zwischen der lokalen Ausführung von SSIS und SSIS in Azure hervorgehoben. Der wichtigste Unterschied ist die Trennung des Speichers von Computevorgängen.

| Speicherung | Typ | Skalierbarkeit |
|---|---|---|
| Lokal (SQL Server) | Von SQL Server gehostete SSIS-Runtime | SSIS Scale Out (in SQL Server 2017 und höher)<br/><br/>Benutzerdefinierte Projektmappen (in früheren Versionen von SQL Server) |
| In Azure (SQL-Datenbank oder verwaltete SQL-Datenbank-Instanz (Vorschauversion)) | Azure SSIS Integration Runtime, eine Komponente von Azure Data Factory (Version 2) | Skalierungsoptionen für SSIS Integration Runtime (SSIS IR) |
| | | |

Azure Data Factory hostet das Runtimemodul für SSIS-Pakete in Azure. Das Runtimemodul wird als Azure SSIS Integration Runtime (SSIS IR) bezeichnet.

Wenn Sie SSIS IR bereitstellen, können Sie zentral und horizontal hochskalieren, indem Sie Werte für folgende Optionen angeben:
-   Die Knotengröße (einschließlich der Anzahl von Kernen) und die Anzahl von Knoten im Cluster.
-   Die vorhandene Instanz von Azure SQL-Datenbank, auf der die SSIS-Katalogdatenbank (SSISDB) gehostet werden soll, und die Dienstebene der Datenbank.
-   Die maximalen parallelen Ausführungen pro Knoten.

Sie müssen SSIS IR nur einmal bereitstellen. Danach können Sie vertraute Tools wie SQL Server Data Tools (SSDT) und SQL Server Management Studio (SSMS) für das Bereitstellen, Konfigurieren, Ausführen, Überwachen, Planen und Verwalten von Paketen verwenden.

> [!NOTE]
> Während dieser öffentlichen Vorschauversion ist die Azure SSIS Integration Runtime noch nicht in allen Regionen verfügbar. Weitere Informationen zu den unterstützten Regionen finden Sie unter [Verfügbare Produkte nach Region – Microsoft Azure](https://azure.microsoft.com/regions/services/).

Data Factory unterstützt auch andere Arten von Integration Runtimes. Weitere Informationen zu SSIS IR und anderen Typen von Integration Runtime finden Sie unter [Integration Runtime in Azure Data Factory](https://docs.microsoft.com/azure/data-factory/concepts-integration-runtime).

## <a name="version-info"></a>Versionsinformationen

Sie können ein Paket in Azure bereitstellen, das mit einer beliebigen Version von SSIS erstellt wurde. Wenn Sie ein Paket in Azure bereitstellen, wird das Paket automatisch in das aktuelle Paketformat geändert, sofern es zu keinen Überprüfungsfehlern kam. Das heißt, es wird immer auf die aktuelle Version von SSIS aktualisiert.

Der Bereitstellungsprozess überprüft Pakete, um sicherzustellen, dass sie auf der Integration Runtime von Azure SSIS ausgeführt werden können. Weitere Informationen finden Sie unter [Überprüfen von in Azure bereitgestellten SSIS-Paketen](ssis-azure-validate-packages.md).

## <a name="prerequisites"></a>Voraussetzungen

Die in diesem Artikel beschriebenen Funktionen erfordern die folgenden Versionen von SQL Server Data Tools (SSDT):
-   Version 15.3 (Vorschau) oder höher für Visual Studio 2017.
-   Version 17.2 oder höher für Visual Studio 2015.

Weitere Informationen zu Voraussetzungen für Azure finden Sie unter [Bereitstellen von SQL Server Integration Services-Paketen in Azure](https://docs.microsoft.com/azure/data-factory/tutorial-create-azure-ssis-runtime-portal).

## <a name="provision-ssis-on-azure"></a>Bereitstellen von SSIS in Azure
Bevor Sie SSIS-Pakete in Azure bereitstellen und ausführen können, müssen Sie die SSIS-Katalogdatenbank (SSISDB) und Azure SSIS Integration Runtime bereitstellen. Befolgen Sie die Schritte zur Bereitstellung im folgenden Artikel: [Bereitstellen von SQL Server Integration Services-Paketen in Azure](https://docs.microsoft.com/azure/data-factory/tutorial-create-azure-ssis-runtime-portal).

Der **Name der SQL-Datenbank**, die SSISDB hostet, stellt den ersten Teil des vierteiligen Namens dar, den Sie beim Bereitstellen und Verwalten von Paketen von SSDT und SSMS verwenden müssen: `<sql_database_name>.database.windows.net`.

Informationen darüber, wie Sie eine Verbindung zur SSIS-Katalogdatenbank herstellen, finden Sie unter [Herstellen einer Verbindung mit der SSISDB-Katalogdatenbank in Azure](ssis-azure-connect-to-catalog-database.md).

## <a name="design-packages"></a>Entwerfen von Paketen
Sie können Pakete weiterhin lokal in SSDT oder in Visual Studio (wenn SSDT installiert ist) **entwerfen und erstellen**.

Weitere Informationen zur Verbindung mit lokalen Datenquellen aus der Cloud mithilfe der **Windows-Authentifizierung** finden Sie unter [Herstellen einer Verbindung mit lokalen Datenquellen und Azure-Dateifreigaben mit der Windows-Authentifizierung](ssis-azure-connect-with-windows-auth.md).

Informationen dazu, wie Sie eine Verbindung zu Dateien und Dateifreigaben herstellen, finden Sie unter [Speichern und Abrufen von Dateien auf lokalen Dateifreigaben und Dateifreigaben in Azure mit SSIS](ssis-azure-files-file-shares.md).

Wenn Sie eine Instanz von SQL-Datenbank bereitstellen, um SSISDB zu hosten, werden auch das Azure Feature Pack für SSIS und die weitervertreibbare Komponente von Access installiert. Diese Komponenten stellen zusätzlich zu den Datenquellen, die von den integrierten Komponenten unterstützt werden, die Konnektivität zu **Excel- und Access-Dateien** und zu verschiedenen **Azure**-Datenquellen bereit.

Sie können ebenfalls zusätzliche Komponenten installieren. Weitere Informationen finden Sie unter [Custom setup for the Azure-SSIS integration runtime (Benutzerdefiniertes Setup von Azure SSIS Integration Runtime)](/azure/articles/data-factory/how-to-configure-azure-ssis-ir-custom-setup.md).

## <a name="deploy-and-run-packages"></a>Bereitstellen und Ausführen von Paketen
Sie müssen das **Projektbereitstellungsmodell** verwenden und nicht das Paketbereitstellungsmodell, wenn Sie Projekte für SSISDB in Azure bereitstellen.

Zum Bereitstellen von Projekten und Ausführen von Paketen in Azure, können Sie diese vertrauten Tools und Skriptoptionen verwenden:
-   SQL Server Management Studio (SSMS)
-   Transact-SQL (von SSMS, Visual Studio Code oder einem anderen Tool)
-   Ein Befehlszeilentool
-   PowerShell
-   C# und das Objektmodell der SSIS-Verwaltung

Erste Schritte finden Sie unter [Bereitstellen, Ausführen und Überwachen eines SSIS-Pakets in Azure](ssis-azure-deploy-run-monitor-tutorial.md).

## <a name="monitor-packages"></a>Überwachen von Paketen
Sie können eines der folgenden Berichtstools in SSMS verwenden, um ausgeführte Pakete in SSMS zu überwachen.
-   Klicken Sie mit der rechten Maustaste auf **SSISDB**, und klicken Sie dann auf **Aktive Vorgänge**, um das Dialogfeld **Aktive Vorgänge** zu öffnen.
-   Wählen Sie im Objekt-Explorer ein Paket aus, klicken Sie mit der rechten Maustaste, und klicken Sie dann auf **Berichte** > **Standardberichte** > **Alle Ausführungen**.

## <a name="schedule-packages"></a>Planen von Paketen
Sie können folgende Tools verwenden, um die Ausführung von in SQL-Datenbank gespeicherten Paketen zu planen:
-   SQL Server-Agent (lokal)
-   Die Data Factory-Aktivität für gespeicherte SQL Server-Prozeduren

Weitere Informationen finden Sie unter [Schedule SSIS package execution on Azure (Planen der Ausführung von SSIS-Paketen in Azure)](ssis-azure-schedule-packages.md).

## <a name="next-steps"></a>Nächste Schritte
Weitere Informationen zu den ersten Schritten mit SSIS-Workloads in Azure finden Sie in folgenden Artikeln:
-   [Bereitstellen von SQL Server Integration Services-Paketen in Azure](https://docs.microsoft.com/azure/data-factory/tutorial-create-azure-ssis-runtime-portal)
-   [Bereitstellen, Ausführen und Überwachen eines SSIS-Pakets in Azure](ssis-azure-deploy-run-monitor-tutorial.md)

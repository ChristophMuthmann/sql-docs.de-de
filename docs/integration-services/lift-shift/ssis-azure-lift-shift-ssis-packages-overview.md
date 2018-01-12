---
title: Migration von SQL Server Integration Services-Workloads in die Cloud per Lift & Shift | Microsoft-Dokumentation
ms.date: 10/31/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: lift-shift
ms.suite: sql
ms.custom: 
ms.technology: integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d534f3118cbc8d9516d7db6033c490a9ab59dd1c
ms.sourcegitcommit: 4aeedbb88c60a4b035a49754eff48128714ad290
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/05/2018
---
# <a name="lift-and-shift-sql-server-integration-services-workloads-to-the-cloud"></a>Migration von SQL Server Integration Services-Workloads in die Cloud per Lift & Shift
Sie können Ihre SQL Server Integration Services-Pakete und -Workloads (SSIS) nun in die Azure-Cloud verschieben.
-   Speichern und verwalten Sie SSIS-Projekte und -Pakete in der SSIS-Katalogdatenbank (SSISDB) in Azure SQL-Datenbank.
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
| In Azure (SQL-Datenbank) | Azure SSIS Integration Runtime, eine Komponente von Azure Data Factory (Version 2) | Skalierungsoptionen für SSIS Integration Runtime (SSIS IR) |
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

## <a name="prerequisites"></a>Voraussetzungen
Die in diesem Artikel beschriebenen Funktionen erfordern nicht SQL Server 2017 oder SQL Server 2016.

Diese Funktionen erfordern die folgenden Versionen von SQL Server Data Tools (SSDT):
-   Version 15.3 (Vorschau) oder höher für Visual Studio 2017.
-   Version 17.2 oder höher für Visual Studio 2015.

> [!NOTE]
> Wenn Sie Pakete in Azure bereitstellen, aktualisiert der Assistent für die Paketbereitstellung die Pakete immer auf das aktuelle Paketformat.

Weitere Informationen zu den Voraussetzungen in Azure finden Sie unter [Bereitstellen von SQL Server Integration Services-Paketen in Azure](https://docs.microsoft.com/azure/data-factory/tutorial-deploy-ssis-packages-azure).

## <a name="ssis-features-on-azure"></a>SSIS-Features in Azure

Wenn Sie eine Instanz von SQL-Datenbank bereitstellen, um SSISDB zu hosten, werden auch das Azure Feature Pack für SSIS und die weitervertreibbare Komponente von Access installiert. Diese Komponenten stellen zusätzlich zu den Datenquellen, die von den integrierten Komponenten unterstützt werden, die Konnektivität zu **Excel- und Access-Dateien** und zu verschiedenen **Azure**-Datenquellen bereit. Sie können derzeit keine **Drittanbieterkomponenten** für SSIS (einschließlich der Drittanbieterkomponenten von Microsoft, z.B. Oracle- und Teradata-Komponenten von Attunity- und SAP BI-Komponenten) installieren.

Der **Name der SQL-Datenbank**, die SSISDB hostet, stellt den ersten Teil des vierteiligen Namens dar, den Sie beim Bereitstellen und Verwalten von Paketen von SSDT und SSMS verwenden müssen: `<sql_database_name>.database.windows.net`.

Sie müssen das **Projektbereitstellungsmodell** und nicht das Paketbereitstellungsmodell für Projekte verwenden, die Sie für SSISDB in Azure SQL-Datenbank bereitstellen.

Sie können Pakete weiterhin lokal in SSDT oder in Visual Studio (wenn SSDT installiert ist) **entwerfen und erstellen**.

Weitere Informationen zur Verbindung mit **lokalen Datenquellen** aus der Cloud mithilfe der Windows-Authentifizierung finden Sie unter [Connect to on-premises data sources with Windows Authentication (Herstellen einer Verbindung mit lokalen Datenquellen mit der Windows-Authentifizierung)](ssis-azure-connect-with-windows-auth.md).

## <a name="common-tasks"></a>Allgemeine Aufgaben

### <a name="provision"></a>Bereitstellen
Bevor Sie SSIS-Pakete in Azure bereitstellen und ausführen können, müssen Sie die SSIS-Katalogdatenbank und Azure SSIS Integration Runtime bereitstellen. Führen Sie die Bereitstellungsschritte in diesem Artikel aus: [Bereitstellen von SQL Server Integration Services-Paketen in Azure](https://docs.microsoft.com/azure/data-factory/tutorial-deploy-ssis-packages-azure).

### <a name="deploy-and-run-packages"></a>Bereitstellen und Ausführen von Paketen
Sie können diese vertrauten Tools und Skriptoptionen verwenden, um Projekte bereitzustellen und Pakete in SQL-Datenbank auszuführen:
-   SQL Server Management Studio (SSMS)
-   Transact-SQL (von SSMS, Visual Studio Code oder einem anderen Tool)
-   Ein Befehlszeilentool
-   PowerShell
-   C# und das Objektmodell der SSIS-Verwaltung

### <a name="monitor-packages"></a>Überwachen von Paketen
Sie können eines der folgenden Berichtstools in SSMS verwenden, um ausgeführte Pakete in SSMS zu überwachen.
-   Klicken Sie mit der rechten Maustaste auf **SSISDB**, und klicken Sie dann auf **Aktive Vorgänge**, um das Dialogfeld **Aktive Vorgänge** zu öffnen.
-   Wählen Sie im Objekt-Explorer ein Paket aus, klicken Sie mit der rechten Maustaste, und klicken Sie dann auf **Berichte** > **Standardberichte** > **Alle Ausführungen**.

### <a name="schedule-packages"></a>Planen von Paketen
Sie können folgende Tools verwenden, um die Ausführung von in SQL-Datenbank gespeicherten Paketen zu planen:
-   SQL Server-Agent (lokal)
-   Die Data Factory-Aktivität für gespeicherte SQL Server-Prozeduren

Weitere Informationen finden Sie unter [Schedule SSIS package execution on Azure (Planen der Ausführung von SSIS-Paketen in Azure)](ssis-azure-schedule-packages.md).

## <a name="next-steps"></a>Nächste Schritte
Weitere Informationen zu den ersten Schritten mit SSIS-Workloads in Azure finden Sie in folgenden Artikeln:
-   [Bereitstellen von SQL Server Integration Services-Paketen in Azure](https://docs.microsoft.com/azure/data-factory/tutorial-deploy-ssis-packages-azure)
-   [Deploy, run, and monitor an SSIS package on Azure (Bereitstellen, Ausführen und Überwachen von SSIS-Paketen in Azure)](ssis-azure-deploy-run-monitor-tutorial.md)

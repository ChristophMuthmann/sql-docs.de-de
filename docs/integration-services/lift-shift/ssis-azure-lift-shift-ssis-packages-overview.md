---
title: Heben und Verschieben von SQL Server Integration Services-arbeitsauslastungen in die Cloud | Microsoft Docs
ms.date: 10/09/2017
ms.topic: article
ms.prod: sql-server-2017
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: 29122bdf543e82c1f429cf401b5fe1d8383515fc
ms.openlocfilehash: 85ab11747276f0c6c58b13cd409df3e5774915ae
ms.contentlocale: de-de
ms.lasthandoff: 10/10/2017

---
# <a name="lift-and-shift-sql-server-integration-services-workloads-to-the-cloud"></a>Heben und Verschieben von SQL Server Integration Services-arbeitsauslastungen in der cloud
Sie können jetzt Ihre SQL Server Integration Services (SSIS)-Pakete und arbeitsauslastungen in Azure-Cloud verschieben.
-   Speichern und Verwalten von SSIS-Projekte und Pakete im SSIS-Katalogdatenbank (SSISDB) für Azure SQL-Datenbank.
-   Ausführen von Paketen in einer Instanz von der Azure-SSIS-Integrationslaufzeit als Teil des Azure Data Factory, Version 2 eingeführt.
-   Verwenden von vertrauten Tools z. B. SQL Server Management Studio (SSMS) für diesen gemeinsamen Aufgaben.

## <a name="benefits"></a>Vorteile
Verschieben Ihre lokalen SSIS-arbeitsauslastungen in Azure hat die folgenden potenziellen Vorteile:
-   **Betriebskosten senken** durch das Reduzieren von lokaler Infrastruktur.
-   **Hohen Verfügbarkeit zu erhöhen** mit mehreren Knoten pro Cluster als auch die Funktionen für hohe Verfügbarkeit von Azure und Azure SQL-Datenbank.
-   **Erhöhen der Skalierbarkeit** die Möglichkeit, mehrere Kerne pro Knoten (Zentrales Skalieren) und mehrere Knoten pro Cluster (horizontales Skalieren) anzugeben.
-   **Vermeiden Sie die Einschränkungen** SSIS auf virtuellen Azure-Computern ausgeführt.

## <a name="architecture-overview"></a>Architekturübersicht
In der folgenden Tabelle werden die Unterschiede zwischen SSIS lokal und SSIS in Azure. Der wichtigste Unterschied ist die Trennung der Speicherung von Compute.

| Speicherung | Typ | Skalierbarkeit |
|---|---|---|
| Lokal (SQL Server) | SSIS-Laufzeit, die von SQL Server gehostet wird | SSIS-Horizontales Skalieren (SQL Server-2017 und höher)<br/><br/>Benutzerdefinierte Lösungen (in früheren Versionen von SQL Server) |
| In Azure (SQL-Datenbank) | Azure SSIS-Integrationslaufzeit, eine Komponente von Azure Data Factory, Version 2 | Skalierungsoptionen für den SSIS-IR |
| | | |

Azure Data Factory hostet das Laufzeitmodul für SSIS-Pakete in Azure. Das Laufzeitmodul wird der Azure-SSIS-Integrationslaufzeit (SSIS-IR) aufgerufen.

Wenn Sie den SSIS-IR bereitstellen, können Sie skalieren und skalieren, indem Sie Werte für die folgenden Optionen angeben:
-   Die Knotengröße (einschließlich der Anzahl von Kernen) und die Anzahl der Knoten im Cluster.
-   Die vorhandene Instanz von Azure SQL-Datenbank zum Hosten von SSIS-Katalog-Datenbank (SSISDB) und die Dienstebene für die Datenbank.
-   Die maximale parallelen Ausführungen pro Knoten.

Sie müssen nur den SSIS-IR einmal bereitstellen. Danach können Sie die vertrauten Tools verwenden, z. B. SQL Server Data Tools (SSDT) und SQL Server Management Studio (SSMS) bereitstellen, konfigurieren, führen Sie überwachen, Planen und Verwalten von Paketen.

> [!NOTE]
> Während dieser öffentlichen Vorschau ist der Azure-SSIS-Integrationslaufzeit nur in den USA, Osten und Nordeuropa Regionen verfügbar.

Data Factory unterstützt auch andere Arten von Integration Laufzeiten. Weitere Informationen zu den SSIS-IR und anderen Typen von Integration Laufzeiten finden Sie unter [integrationslaufzeit in Azure Data Factory](https://docs.microsoft.com/en-us/azure/data-factory/concepts-integration-runtime).

## <a name="prerequisites"></a>Erforderliche Komponenten
Die Funktionen, die in diesem Thema beschriebenen SQL Server Data Tools (SSDT) Version 17.2 oder höher erforderlich, aber Sie erfordern keine 2017 von SQL Server oder SQL Server 2016. Wenn Sie Pakete in Azure bereitstellen, aktualisiert der Paket-Bereitstellungs-Assistent die Pakete immer auf das aktuelle Paketformat.

Weitere Informationen zu den Voraussetzungen in Azure finden Sie unter [Lift- and -Shift SQL Server Integration Services (SSIS)-Pakete Azure](https://docs.microsoft.com/en-us/azure/data-factory/tutorial-deploy-ssis-packages-azure).

## <a name="ssis-features-on-azure"></a>SSIS-Funktionen in Azure

Wenn Sie eine Instanz von SQL-Datenbank zum Hosten von SSISDB bereitstellen, das Azure Feature Pack für SSIS und Zugriff verteilbaren installiert. Diese Komponenten stellen Verbindungen mit Excel- und Access-Dateien und mit verschiedenen Azure-Datenquellen bereit. Sie können nicht zu diesem Zeitpunkt Drittanbieter-Komponenten für SSIS installieren.

Der Name der SQL-Datenbank, die SSISDB hostet, wird der erste Teil des vierteiligen Namens zu verwendende bereitstellen und Verwalten von Paketen aus SSDT und SSMS - `<sql_database_name>.database.windows.net`.

Sie haben das projektbereitstellungsmodell nicht das paketbereitstellungsmodell für Projekte verwenden, die Sie SSISDB für Azure SQL-Datenbank bereitstellen.

Sie weiterhin entwerfen und Erstellen von Paketen lokal in SSDT oder in Visual Studio mit SSDT installiert.

Informationen zum Herstellen einer Verbindung mit lokalen Datenquellen über die Cloud mit Windows-Authentifizierung finden Sie unter [Herstellen einer Verbindung mit lokalen Datenquellen mit Windows-Authentifizierung](ssis-azure-connect-with-windows-auth.md).

## <a name="common-tasks"></a>Allgemeine Aufgaben

### <a name="provision"></a>Bereitstellen
Vor der Bereitstellung und SSIS-Pakete in Azure ausführen können, müssen Sie die SSISDB-Katalog-Datenbank und der Azure-SSIS-Integrationslaufzeit bereitstellen. Führen Sie die Bereitstellung die Schritte in diesem Artikel: [Lift- and -Shift SQL Server Integration Services (SSIS)-Pakete Azure](https://docs.microsoft.com/en-us/azure/data-factory/tutorial-deploy-ssis-packages-azure).

### <a name="deploy-and-run-packages"></a>Bereitstellen und Ausführen von Paketen
Zum Bereitstellen von Projekten und Paketen auf SQL-Datenbank ausgeführt, können Sie eine der zahlreichen vertrauter Tools und Optionen für Skripts verwenden:
-   SQL Server Management Studio (SSMS)
-   Transact-SQL (von SSMS, Visual Studio-Code oder ein anderes Tool)
-   Ein Befehlszeilenprogramm
-   PowerShell
-   C#- und des SSIS-Management-Objektmodells

### <a name="monitor-packages"></a>Monitor-Pakete
Zum Überwachen von ausgeführter Paketen in SSMS können Sie eine der folgenden Berichtstools in SSMS verwenden.
-   Mit der rechten Maustaste **SSISDB**, und wählen Sie dann **aktive Vorgänge** So öffnen die **aktive Vorgänge** (Dialogfeld).
-   Wählen Sie im Objekt-Explorer, mit der rechten Maustaste und wählen ein Paket **Berichte**, klicken Sie dann **Standardberichte**, klicken Sie dann **alle Ausführungen**.

### <a name="schedule-packages"></a>Zeitplan-Pakete
So planen Sie die Ausführung von Paketen in SQL-Datenbank gespeichert, können Sie die folgenden Tools verwenden:
-   SQL Server-Agent lokal
-   Der Data Factory SQL Server Stored Procedure-Aktivität

Weitere Informationen finden Sie unter [Zeitplan SSIS-Paket die Ausführung auf Azure](ssis-azure-schedule-packages.md).

## <a name="next-steps"></a>Nächste Schritte
Zum Einstieg in SSIS-Workloads in Azure finden Sie in den folgenden Artikeln:
-   [Heben und Verschieben von SQL Server Integration Services (SSIS)-Pakete in Azure](https://docs.microsoft.com/en-us/azure/data-factory/tutorial-deploy-ssis-packages-azure)
-   [Bereitstellen Sie, führen Sie aus und überwachen Sie ein SSIS-Paket in Azure](ssis-azure-deploy-run-monitor-tutorial.md)


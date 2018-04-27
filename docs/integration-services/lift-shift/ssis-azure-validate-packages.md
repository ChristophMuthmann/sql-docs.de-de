---
title: Überprüfen von in Azure bereitgestellten SSIS-Paketen | Microsoft-Dokumentation
ms.date: 11/27/2017
ms.topic: article
ms.prod: sql
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
ms.openlocfilehash: 6e2bf8f48751d819293edbaa0e40a85e74b0c513
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="validate-ssis-packages-deployed-to-azure"></a>Überprüfen von in Azure bereitgestellten SSIS-Paketen
Wenn Sie auf einem Azure-Server ein SSIS-Projekt (SQL Server Integration Services) in der SSIS-Katalogdatenbank (SSISDB) bereitstellen, fügt der Assistent für die Paketbereitstellung hinter der Seite **Überprüfen** einen zusätzlichen Überprüfungsschritt hinzu. In diesem Überprüfungsschritt werden die im Projekt enthaltenen Pakete auf bekannte Probleme hin überprüft, die möglicherweise eine erwartungsgemäße Ausführung in der Azure SSIS Integration Runtime verhindern. Anschließend zeigt der Assistent alle zutreffenden Warnungen auf der Seite **Überprüfen** an.

> [!IMPORTANT]
> Die in diesem Artikel beschriebene Überprüfung tritt ein, wenn Sie ein Projekt mit SQL Server Data Tools (SSDT), Version 17.4 oder höher, bereitstellen. Informationen zum Abrufen der neuesten Version von SSDT finden Sie unter [Herunterladen von SQL Server Data Tools (SSDT)](../../ssdt/download-sql-server-data-tools-ssdt.md).

Weitere Informationen zum Assistenten für die Paketbereitstellung finden sie unter [Bereitstellen von SQL Server Integration Services-Projekten und Paketen (SSIS)](../packages/deploy-integration-services-ssis-projects-and-packages.md).

## <a name="validate-connection-managers"></a>Überprüfen von Verbindungs-Managern

Der Assistent überprüft bestimmte Verbindungs-Manager auf die folgenden Probleme, die zu einem Verbindungsfehler führen können:
- **Windows-Authentifizierung**. Wenn eine Verbindung Windows-Authentifizierung verwendet, löst die Überprüfung eine Warnung aus. Für Windows-Authentifizierung sind zusätzliche Konfigurationsschritte erforderlich. Weitere Informationen finden Sie unter [Herstellen von Verbindungen mit lokalen Datenquellen mit Windows-Authentifizierung](ssis-azure-connect-with-windows-auth.md).
- **Dateipfad**. Wenn eine Verbindungszeichenfolge einen hartcodierten lokalen Dateipfad wie `C:\\...` enthält, löst die Überprüfung eine Warnung aus. Bei Paketen, die einen absoluten Pfad enthalten, tritt möglicherweise ein Fehler auf.
- **UNC-Pfad**. Wenn eine Verbindungszeichenfolge einen UNC-Pfad enthält, löst die Überprüfung eine Warnung aus. Bei Paketen, die einen UNC-Pfad enthalten, tritt möglicherweise ein Fehler auf, normalerweise, weil für den Zugriff auf einen UNC-Pfad Windows-Authentifizierung erforderlich ist.
- **HostName**. Wenn eine Servereigenschaft den Hostnamen anstelle der IP-Adresse enthält, löst die Überprüfung eine Warnung aus. Bei Paketen, die einen Hostnamen enthalten, tritt möglicherweise ein Fehler auf, normalerweise, weil für das virtuelle Azure-Netzwerk die richtige DNS-Konfiguration erforderlich ist, damit die DNS-Namensauflösung unterstützt werden kann.
- **Anbieter oder Treiber**. Wenn ein Anbieter oder Treiber nicht unterstützt wird, löst die Überprüfung eine Warnung aus. Aktuell wird nur eine kleine Anzahl integrierter Anbieter und Treiber unterstützt.

Der Assistent führt die folgenden Überprüfungen für die in der Liste aufgeführten Verbindungs-Manager aus.

| Verbindungs-Manager | Windows-Authentifizierung | Dateipfad | UNC-Pfad | Hostname | Anbieter oder Treiber |
|--------------------|----------|-----------|-----|-----------|-------------------|
| ADO                | ✓        |           |     | ✓         | ✓                 |
| AdoNet             | ✓        |           |     | ✓         | ✓                 |
| Cache              |          | ✓         | ✓   |           |                   |
| Excel              |          | ✓         | ✓   |           |                   |
| File               |          | ✓         | ✓   |           |                   |
| FlatFile           |          | ✓         | ✓   |           |                   |
| FTP                |          |           |     | ✓         |                   |
| MSOLAP100          |          |           |     | ✓         | ✓                 |
| MultiFile          |          | ✓         | ✓   |           |                   |
| MultiFlatFile      |          | ✓         | ✓   |           |                   |
| OData              | ✓        |           |     | ✓         |                   |
| ODBC               | ✓        |           |     | ✓         | ✓                 |
| OLEDB              | ✓        |           |     | ✓         | ✓                 |
| SMOServer          | ✓        |           |     | ✓         |                   |
| SMTP               | ✓        |           |     | ✓         |                   |
| SQLMOBILE          |          | ✓         | ✓   |           |                   |
| WMI                | ✓        |           |     |           |                   |
|||||||

## <a name="validate-sources-and-destinations"></a>Überprüfen von Quellen und Zielen
Die folgenden Quellen und Ziele von Drittanbietern werden nicht unterstützt:

-   Oracle-Quelle und Ziel von Attunity
-   Teradata-Quelle und Ziel von Attunity
-   SAP BI-Quelle und -Ziel

## <a name="validate-tasks-and-components"></a>Überprüfen von Aufgaben und Komponenten

### <a name="execute-process-task"></a>Prozess ausführen (Task)

Die Überprüfung löst eine Warnung aus, wenn ein Befehl mit absolutem Pfad auf eine lokale Datei oder mit einem UNC-Pfad auf eine Datei verweist. Diese Pfade können bei der Ausführung in Azure zu Fehlern führen.

### <a name="script-task-and-script-component"></a>Skriptaufgabe und Skriptkomponente

Die Überprüfung löst eine Warnung aus, wenn ein Paket eine Skriptaufgabe oder eine Skriptkomponente enthält, die auf nicht unterstützte Assemblys verweist oder diese aufruft. Diese Verweise oder Aufrufe können zu Ausführungsfehlern führen.

### <a name="other-components"></a>Andere Komponenten

Das ORC-Format wird für das HDFS-Ziel und das Azure Data Lake Store-Ziel nicht unterstützt.

## <a name="next-steps"></a>Nächste Schritte
Informationen zum Erlernen des Planens der Paketausführung unter Azure finden Sie unter [Planen der Ausführung eines SSIS-Pakets unter Azure](ssis-azure-schedule-packages.md).
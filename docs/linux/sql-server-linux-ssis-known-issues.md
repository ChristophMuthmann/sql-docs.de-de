---
title: Einschränkungen und bekannten Probleme für SSIS unter Linux | Microsoft Docs
description: Dieser Artikel beschreibt Einschränkungen und bekannten Probleme für Microsoft SQL Server Integration Services (SSIS) auf Linux-Computern
author: leolimsft
ms.author: lle
ms.reviewer: douglasl
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.openlocfilehash: 405968dcf44c01e48935a0afe837270b4c140c93
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="limitations-and-known-issues-for-ssis-on-linux"></a>Einschränkungen und bekannten Probleme für SSIS unter Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Dieser Artikel beschreibt aktuelle Einschränkungen und bekannten Probleme für Microsoft SQL Server Integration Services (SSIS) unter Linux.

## <a name="general-limitations-and-known-issues"></a>Allgemeine Einschränkungen und bekannte Probleme

Die folgenden Funktionen werden nicht in dieser Version von SSIS unter Linux unterstützt:
  - SSIS-Katalogdatenbank
  - Geplante paketausführung vom SQL-Agent
  - Windows-Authentifizierung
  - Drittanbieter-Komponenten
  - Change Data Capture (CDC)
  - SSIS für horizontales Skalieren
  - Azure FeaturePack für SSIS
  - Unterstützung für Hadoop und HDFS
  - Microsoft Connector for SAP BW

Andere Einschränkungen und bekannte Probleme mit SSIS unter Linux finden Sie in der [Anmerkungen zu dieser Version](sql-server-linux-release-notes.md#ssis).

## <a name="components"></a> Unterstützte und nicht unterstützte Komponenten

Die folgenden integrierten Integration Services-Komponenten werden unter Linux unterstützt. Einige von ihnen haben Einschränkungen für die Linux-Plattform, wie in den folgenden Tabellen beschrieben.

Integrierte Komponenten, die hier nicht aufgeführt sind, werden nicht unter Linux unterstützt.

### <a name="supported-control-flow-tasks"></a>Ablaufsteuerungstasks unterstützt
- Masseneinfügungstask
- Datenflusstask
- Datenprofilerstellungs-Task
- SQL ausführen (Task)
- T-SQL-Anweisung ausführen (Task)
- Task 'Ausdruck'
- FTP-Task
- Webdienst (Task)
- XML Task

### <a name="control-flow-tasks-supported-with-limitations"></a>Ablaufsteuerungstasks unterstützt mit Einschränkungen

| Task | Einschränkungen |
|------------|---|
| Task Prozess ausführen | Nur unterstützt in-Process-Modus. |
| Datei für den Task ' Dateisystem ' | Die *Move Verzeichnis* und *Festlegen von Dateiattributen* Aktionen werden nicht unterstützt. |
| Skripttask | Unterstützt nur die standardmäßigen .NET Framework-APIs. |
| Mail senden (Task) | Unterstützt nur anonyme Benutzermodus. |
| Tasks "Datenbank übertragen" | UNC-Pfade werden nicht unterstützt. |
| | |

### <a name="supported-control-flow-containers"></a>Unterstützt ablaufsteuerungscontainer
- Sequenzcontainer
- For-Schleifencontainer
- Foreach-Schleifencontainer

### <a name="supported-data-flow-sources-and-destinations"></a>Unterstützte datenflussquellen und Ziele
- Rohdatendatei-Quelle und Ziel
- XML-Quelle

### <a name="data-flow-sources-and-destinations-supported-with-limitations"></a>Datenflussquellen und Ziele, die mit Einschränkungen unterstützt

| Komponente | Einschränkungen |
|------------|---|
| ADO NET-Quelle und Ziel | Unterstützt nur die SQLClient-Datenanbieter. |
| Flatfilequelle und Ziel | Unterstützt nur Windows-Stil Dateipfade, auf die standardmäßige Zuordnung Pfadregel angewendet wird. Z. B. `D:\home\ssis\travel.csv` wird `/home/ssis/travel.csv`. |
| OData-Quelle | Unterstützt nur die Standardauthentifizierung. |
| ODBC-Quelle und -Ziel | Unterstützt 64-Bit-Unicode-ODBC-Treiber unter Linux. Hängt von der UnixODBC-Treiber-Manager unter Linux. |
| OLE DB-Quelle und Ziel | Nur SQL Server Native Client 11.0 und Microsoft OLE DB-Anbieter für SQL Server unterstützt werden. |
| | |

### <a name="supported-data-flow-transformations"></a>Datenflusstransformationen unterstützt
- Aggregat
- Überwachen von
- Balanced Data Distributor
- Zeichenzuordnung
- Bedingtes Teilen
- Kopieren von Spalten
- Datenkonvertierung
- Abgeleitete Spalte
- Exportieren von Spalten
- Fuzzygruppierung
- Fuzzysuche
- Importieren von Spalten
- Suche
- Merge
- Merge Join
- Multicast
- Pivotieren
- Zeilenanzahl
- Langsam veränderliche Dimensionen
- Sort
- Ausdruckssuche
- Union All
- Entpivotieren

### <a name="data-flow-transformations-supported-with-limitations"></a>Datenflusstransformationen unterstützt mit Einschränkungen

| Komponente | Einschränkungen |
|------------|---|
| Transformation für OLE DB-Befehl | Dieselben Einschränkungen wie OLE DB-Quelle und Ziel. |
| Skriptkomponente | Unterstützt nur die standardmäßigen .NET Framework-APIs. |
| | |

### <a name="supported-and-unsupported-log-providers"></a>Unterstützte und nicht unterstützte Protokollanbieter
Alle integrierten SSIS-Protokollanbieter unter Linux unterstützt werden mit Ausnahme der Windows-Ereignisprotokollprovider.

Der Protokollanbieter für SQL Server unterstützt nur die SQL-Authentifizierung; Er unterstützt keine Windows-Authentifizierung.

Die SSIS-Protokollanbieter für Textdateien, XML-Dateien und SQL Server Profiler schreiben ihre Ausgabe, um eine Datei, die Sie angeben. Die folgenden Überlegungen gelten für den Dateipfad:
-   Wenn Sie der Protokollanbieter schreibt in das aktuelle Verzeichnis des Hosts keinen Pfad bereitstellen. Wenn der aktuelle Benutzer über die Berechtigung zum Schreiben in das aktuelle Verzeichnis des Hosts verfügt, löst der Protokollanbieter einen Fehler aus.
-   Sie können keine Umgebungsvariable in einem Dateipfad. Wenn Sie eine Umgebungsvariable angeben, wird der Literaltext an dem von Ihnen im Dateipfad angezeigt. Wenn Sie angeben, z. B. `%TMP%/log.txt`, Protokollanbieters fügt die wörtlichen Text `/%TMP%/log.txt` auf das aktuelle Hostverzeichnis.

## <a name="related-content-about-ssis-on-linux"></a>Verwandte Inhalte über SSIS unter Linux
-   [Extrahieren, Transformieren und Laden von Daten unter Linux mit SSIS](sql-server-linux-migrate-ssis.md)
-   [Installieren von SQL Server Integration Services (SSIS) unter Linux](sql-server-linux-setup-ssis.md)
-   [Konfigurieren von SQL Server Integration Services unter Linux mit Ssis-conf](sql-server-linux-configure-ssis.md)
-   [Zeitplan SQL Server Integration Services-paketausführung unter Linux mit cron](sql-server-linux-schedule-ssis-packages.md)

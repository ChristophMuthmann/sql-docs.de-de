---
title: "Einschränkungen und bekannten Probleme für SSIS unter Linux | Microsoft Docs"
description: "Dieser Artikel beschreibt Einschränkungen und bekannten Probleme für Microsoft SQL Server Integration Services (SSIS) auf Linux-Computern"
author: leolimsft
ms.author: lle
ms.reviewer: douglasl
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 29122bdf543e82c1f429cf401b5fe1d8383515fc
ms.openlocfilehash: eec45efe8fb49afefab418130d05d7a2b82bddd3
ms.contentlocale: de-de
ms.lasthandoff: 10/10/2017

---
# <a name="limitations-and-known-issues-for-ssis-on-linux"></a>Einschränkungen und bekannten Probleme für SSIS unter Linux

In diesem Thema wird beschrieben, aktuelle Einschränkungen und bekannten Probleme für SQL Server Integration Services (SSIS) unter Linux.

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

## <a name="components"></a>Unterstützte und nicht unterstützte Komponenten

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
- XML-Task

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
| ODBC-Quelle und Ziel | Unterstützt 64-Bit-Unicode-ODBC-Treiber unter Linux. Hängt von der UnixODBC-Treiber-Manager unter Linux. |
| OLE DB-Quelle und Ziel | Nur SQL Server Native Client 11.0 und Microsoft OLE DB-Anbieter für SQL Server unterstützt werden. |
| | |

### <a name="supported-data-flow-transformations"></a>Datenflusstransformationen unterstützt
- Aggregat
- Überwachung
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



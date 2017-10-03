---
title: Extrahieren, Transformieren und Laden von Daten unter Linux mit SSIS | Microsoft Docs
description: 
author: leolimsft
ms.author: lle
ms.reviewer: douglasl
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 9dab69c7-73af-4340-aef0-de057356b791
ms.translationtype: MT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: aa4ac0cca739ea57a28beb399325d55b38502217
ms.contentlocale: de-de
ms.lasthandoff: 10/02/2017

---
# <a name="extract-transform-and-load-data-on-linux-with-ssis"></a>Extrahieren, Transformieren und Laden von Daten unter Linux mit SSIS

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

In diesem Thema wird beschrieben, wie SQL Server Integration Services (SSIS)-Pakete auf Linux ausgeführt wird. SSIS löst Probleme bei der Integration von komplexen Daten extrahieren von Daten aus mehreren Quellen und Formaten, Transformieren und Bereinigen der Daten und die Daten in mehrere Ziele laden. 

SSIS-Pakete auf Linux laufende können mit Microsoft SQL Server, die auf Windows lokal oder in der Cloud, die unter Linux oder in Docker verbinden. Sie können auch mit Azure SQL-Datenbank, Azure SQL Data Warehouse, ODBC-Datenquellen, Flatfiles und anderen Datenquellen, einschließlich ADO.NET Quellen, XML-Dateien und OData-Diensten verbinden.

Weitere Informationen zu den Funktionen von SSIS finden Sie unter [SQL Server Integration Services](../integration-services/sql-server-integration-services.md).

## <a name="prerequisites"></a>Erforderliche Komponenten

Um SSIS-Pakete auf einem Linux-Computer auszuführen, müssen Sie zuerst SQL Server Integration Services installieren. SSIS wird während der Installation von SQL Server für Linux-Computern nicht enthalten. Installationsanweisungen finden Sie unter [Installieren von SQL Server Integration Services](sql-server-linux-setup-ssis.md).

Sie haben auch zum Erstellen und verwalten Sie Pakete auf einen Windows-Computer verfügen. Die SSIS-Entwurf und die Verwaltungstools sind Windows-Anwendungen, die nicht für Linux-Computer verfügbar sind. 

## <a name="run-an-ssis-package"></a>Führen Sie ein SSIS-Paket

Um ein SSIS-Paket auf einem Linux-Computer auszuführen, führen Sie folgende Schritte aus:

1.  Kopieren Sie das SSIS-Paket auf dem Linux-Computer.
2.  Führen Sie den folgenden Befehl aus:
    ```
    $ dtexec /F \<package name \> /DE <protection password>
    ```

## <a name="other-common-ssis-tasks"></a>Andere allgemeine SSIS-tasks

-   **Entwerfen Sie Pakete**.

    -   **Herstellen einer Verbindung mit der ODBC-Datenquellen**. Mit SSIS unter Linux CTP-Version 2.1 aktualisiert und höher können SSIS-Pakete auf Linux ODBC-Verbindungen. Diese Funktion wurde mit SQL Server und die MySQL-ODBC-Treiber getestet, aber auch mit jeder Unicode-ODBC-Treiber arbeiten, die die ODBC-Spezifikation berücksichtigt werden sollen. Zur Entwurfszeit können Sie entweder einen DSN oder eine Verbindungszeichenfolge in die ODBC-Verbindung angeben; Sie können auch Windows-Authentifizierung verwenden. Weitere Informationen finden Sie unter der [Blogbeitrag Ankündigung ODBC-Unterstützung unter Linux](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/).

    -   **Pfade**. Geben Sie im Windows-Format Pfade im SSIS-Pakete. SSIS unter Linux unterstützt keine Pfade für Linux-Format, aber Windows-Stil Pfade Linux-Stil Pfade zur Laufzeit zugeordnet. Klicken Sie dann, z. B. SSIS unter Linux ordnet den Windows-Stil Pfad `C:\test` auf den Linux-Stil Pfad `/test`.

-   **Bereitstellen von Paketen**. Sie können nur Pakete im Dateisystem unter Linux in dieser Version speichern. Die SSIS-Katalogdatenbank und die legacy-SSIS-Dienst sind nicht verfügbar unter Linux für die Bereitstellung von Paketen und Speicher.

-   **Planen von Paketen**. Sie können Linux-System Planen von Tools wie z. B. `cron` um Pakete zu planen. SQL-Agent können für Linux keine um Ausführung in dieser Version des Pakets zu planen. Weitere Informationen finden Sie unter [Zeitplan SSIS-Pakete auf Linux mit Cron](sql-server-linux-schedule-ssis-packages.md).

## <a name="limitations-and-known-issues"></a>Einschränkungen und bekannte Probleme

### <a name="general-limitations-and-known-issues"></a>Allgemeine Einschränkungen und bekannte Probleme

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

### <a name="components"></a>Unterstützte und nicht unterstützte Komponenten

Die folgenden integrierten Integration Services-Komponenten werden unter Linux unterstützt. Einige von ihnen haben Einschränkungen für die Linux-Plattform, wie in den folgenden Tabellen beschrieben.

Integrierte Komponenten, die hier nicht aufgeführt sind, werden nicht unter Linux unterstützt.

#### <a name="supported-control-flow-tasks"></a>Ablaufsteuerungstasks unterstützt
- Masseneinfügungstask
- Datenflusstask
- Datenprofilerstellungs-Task
- SQL ausführen (Task)
- T-SQL-Anweisung ausführen (Task)
- Task 'Ausdruck'
- FTP-Task
- Webdienst (Task)
- XML-Task

#### <a name="control-flow-tasks-supported-with-limitations"></a>Ablaufsteuerungstasks unterstützt mit Einschränkungen

| Task | Einschränkungen |
|------------|---|
| Task Prozess ausführen | Nur unterstützt in-Process-Modus. |
| Datei für den Task ' Dateisystem ' | Die *Move Verzeichnis* und *Festlegen von Dateiattributen* Aktionen werden nicht unterstützt. |
| Skripttask | Unterstützt nur die standardmäßigen .NET Framework-APIs. |
| Mail senden (Task) | Unterstützt nur anonyme Benutzermodus. |
| Tasks "Datenbank übertragen" | UNC-Pfade werden nicht unterstützt. |
| | |

#### <a name="supported-control-flow-containers"></a>Unterstützt ablaufsteuerungscontainer
- Sequenzcontainer
- For-Schleifencontainer
- Foreach-Schleifencontainer

#### <a name="supported-data-flow-sources-and-destinations"></a>Unterstützte datenflussquellen und Ziele
- Rohdatendatei-Quelle und Ziel
- XML-Quelle

#### <a name="data-flow-sources-and-destinations-supported-with-limitations"></a>Datenflussquellen und Ziele, die mit Einschränkungen unterstützt

| Komponente | Einschränkungen |
|------------|---|
| ADO NET-Quelle und Ziel | Unterstützt nur die SQLClient-Datenanbieter. |
| Flatfilequelle und Ziel | Unterstützt nur Windows-Stil Dateipfade, auf die standardmäßige Zuordnung Pfadregel angewendet wird. Z. B. `D:\home\ssis\travel.csv` wird `/home/ssis/travel.csv`. |
| OData-Quelle | Unterstützt nur die Standardauthentifizierung. |
| ODBC-Quelle und Ziel | Unterstützt 64-Bit-Unicode-ODBC-Treiber unter Linux. Hängt von der UnixODBC-Treiber-Manager unter Linux. |
| OLE DB-Quelle und Ziel | Nur SQL Server Native Client 11.0 und Microsoft OLE DB-Anbieter für SQL Server unterstützt werden. |
| | |

#### <a name="supported-data-flow-transformations"></a>Datenflusstransformationen unterstützt
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

#### <a name="data-flow-transformations-supported-with-limitations"></a>Datenflusstransformationen unterstützt mit Einschränkungen

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

## <a name="more-info-about-ssis-on-linux"></a>Weitere Informationen zu SSIS unter Linux

Weitere Informationen zu SSIS unter Linux finden Sie unter den folgenden Blogbeiträgen:

-   [SSIS unter Linux finden Sie in SQL Server 2017 CTP2. 1](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/)
-   [ODBC ist in SSIS unter Linux (SQL Server 2017 CTP-Version 2.1 aktualisiert) unterstützt.](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/)

## <a name="more-info-about-ssis"></a>Weitere Informationen über SSIS

Microsoft SQL Server Integration Services (SSIS) ist eine Plattform zum Erstellen von Hochleistungs-datenintegrationslösungen, z. B. extrahieren, Transformieren und laden (ETL) von Paketen für Datawarehousing. Weitere Informationen zu SSIS finden Sie unter [SQL Server Integration Services](/sql/integration-services/sql-server-integration-services.md).

SSIS umfasst die folgenden Funktionen:
- grafische Tools und Assistenten zum Erstellen und Debuggen von Paketen für Windows
- eine Vielzahl von Aufgaben zum Ausführen von Workflowfunktionen wie z. B. FTP-Vorgänge, Ausführen von SQL-Anweisungen und Senden von e-Mail-Nachrichten
- eine Vielzahl von Datenquellen und Zielen zum Extrahieren und Laden von Daten
- eine Reihe von Transformationen zum Bereinigen, aggregieren, Zusammenführen und Kopieren von Daten
- Anwendungsprogrammierschnittstellen (APIs) für die Erweiterung von SSIS mit Ihren eigenen benutzerdefinierten Skripts und Komponenten

Laden Sie zum Einstieg in SSIS die neueste Version des [SQL Server Data Tools (SSDT)](../integration-services/ssis-how-to-create-an-etl-package.md).

## <a name="see-also"></a>Siehe auch
- [Erfahren Sie mehr über SQL Server Integration Services](../integration-services/sql-server-integration-services.md)
- [SQL Server Integration Services (SSIS) Entwicklungs- und Verwaltungstools](../integration-services/integration-services-ssis-development-and-management-tools.md)
- [SQL Serverintegration Services-Lernprogramme](../integration-services/integration-services-tutorials.md)


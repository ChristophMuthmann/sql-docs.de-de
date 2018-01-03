---
title: "Neuheiten bei SSMA für Oracle (OracleToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-oracle
ms.custom: 
ms.date: 09/22/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f305ebb6-7393-4a43-abb3-6332b739d690
caps.latest.revision: "24"
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 908bd781fcbb32e2991976ad197401da0c5c0776
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="whats-new-in-ssma-for-oracle-oracletosql"></a>Was ist neu in SSMA für Oracle (OracleToSQL)
In diesem Thema werden die SSMA für Oracle-Änderungen in jeder Version aufgelistet.  

## <a name="ssma-v76"></a>SSMA v7.6
Die v7.6-Version von SSMA für Oracle wurde verbessert, mit der targeted Korrekturen, die Qualität und Konvertierung Metriken zu verbessern und Unterstützung für SQL Server-2017 (öffentliche Vorschau). Unterstützung für SQL Server-2017 auf Windows- und Linux ist als öffentliche Vorschau verfügbar und sollte nicht für die Produktionsmigrationen verwendet werden.

> [!IMPORTANT]
> SSMA v7.4 und höhere Versionen .net 4.5.2 ist eine Voraussetzung für Installation, und die 32-Bit-Version des Tools wurde eingestellt.

## <a name="ssma-v75"></a>SSMA 7.5
Die Version 7.5 von SSMA für Oracle enthält die folgenden Änderungen:
- Durch mehrere Verbesserungen an größere Barrierefreiheit für Personen mit behinderungen stellen Sie sicher, verbessert.
- Zur Verbesserung der Qualität und Konvertierung Metrik mit dem Ziel Updates aktualisiert, z. B. verbesserte Behandlung von Datums-und "float" während der Datenmigration, basierend auf Kundenfeedback.

> [!IMPORTANT]
> .NET 4.5.2 ist eine Voraussetzung für die Installation von SSMA 7.5. Darüber hinaus wird v7.4 ab, die 32-Bit-Version von SSMA nicht mehr unterstützt wird.

## <a name="ssma-v74"></a>SSMA v7.4
Die v7.4-Version von SSMA für Oracle enthält die folgenden Änderungen:

- SSMA für Oracle unterstützt jetzt die Azure SQL Data Warehouse als Zielplattform für die Migration.

    ![Neue Projektfenster](../media/new-project.png)
  - Unterstützt die Data Warehouse-Speicheroptionen, wie in der folgenden Abbildung gezeigt:

    ![Speicheroptionen für Datawarehouse](../media/storage-options_red.png)
  - Unterstützt die Optionen für die Verteilung der Daten an, wie in der folgenden Abbildung gezeigt:

    ![datenverteilung für das Datawarehouse](../media/data-distribution_red.png)

- Die **Abfragetimeout** Option ist während der Ermittlung an Quelle und Ziel Schema verfügbar.

    ![Option Timeout für Remoteabfragen](../media/query-timeout_red.png)

- Die Qualität und Konvertierung Metrik wurde mit targeted Fehlerbehebungen, aufgrund von Kundenfeedback verbessert.

> [!IMPORTANT]
> .NET 4.5.2 ist eine Voraussetzung für die Installation von SSMA v7.4. Darüber hinaus wird v7.4 ab, die 32-Bit-Version von SSMA nicht mehr unterstützt wird.

## <a name="ssma-v73"></a>SSMA V7. 3
Die V7. 3-Version von SSMA für Oracle enthält die folgenden Änderungen:
- Verbesserte Qualität und Konvertierung Metrik mit dem Ziel Korrekturen, die basierend auf Kundenfeedback.
- SSMA Extensibility Framework verfügbar gemacht werden, über die folgenden Elemente:
  - Exportieren Sie zu einem SQL Server Data Tools (SSDT)-Projekt bereit.
    -   Sie können jetzt Schemaskripts von SSMA in ein SSDT-Projekt exportieren. Die Schemaskripts können Sie zusätzliche Schemas ändern und Bereitstellen der Datenbank.
![Speichern Sie als SSDT-Befehl "Projekt"](../media/export-schema-scripts_red.png)
  - Bibliotheken, die zum Ausführen von benutzerdefinierter Konvertierungen von SSMA genutzt werden können.
    - Jetzt können Sie Code erstellen, die benutzerdefinierte Syntax Konvertierungen und Konvertierungen, die zuvor vom SSMA verarbeitet wurden nicht verarbeiten kann.
      - Anweisungen zum Erstellen eines benutzerdefinierten Konverters stehen in diesem Blogbeitrag [Erweitern von SQL Server Migration Assistant Funktionen](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/).
      - Beispielprojekt für die Konvertierung herunterladen dies [Blogbeitrag](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/).


## <a name="ssma-v72"></a>SSMA V7. 2
Die V7. 2-Version von SSMA für Oracle enthält die folgenden Änderungen:
- Verbesserte Qualität und Konvertierung Metrik mit dem Ziel Korrekturen, die basierend auf Kundenfeedback.
- Telemetrie-Erweiterungen bieten eine bessere Datenpunkte, um Kundenprobleme zu beheben und zu verbessern SSMAs-Wechselkurse.

## <a name="ssma-v71"></a>SSMA v7.1
Die v7.1-Version von SSMA für Oracle enthält die folgenden Änderungen:
- SQL Server-2017 auf Windows- und Linux CTP1 ist jetzt eine unterstützte Zielplattform für die Migration. Dieses Feature ist in der technischen Vorschau und ermöglicht das Verschieben von Schema und Daten an SQL-Zielserver.
- SSMA unterstützt jetzt die automatische Updates, um die neueste Version von SSMA herunterladen, sobald es verfügbar ist.
- Installierbare SSMA-Binärdateien werden jetzt über Windows Installer-Paket-Dateien (.msi) übermittelt.

**Ressourcen**

[Erweitern von SQL Server Migration Assistant Funktionen](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)

[Bewerten und Migrieren von Daten aus datenplattformen nicht von Microsoft SQL Server *(mit der Oracle-Beispiel)*](https://blogs.msdn.microsoft.com/datamigration/2016/11/16/sql-server-migration-assistant-how-to-assess-and-migrate-databases-from-non-microsoft-data-platforms-to-sql-server/) 

## <a name="may-2016"></a>Mai 2016  
Die Mai 2016-Version von SSMA für Oracle enthält die folgenden Änderungen:  

-   Unterstützung für SQL Server 2016.
-   Hinzugefügte Konvertierung von Oracle Flashback Archivtabellen in temporalen Tabellen mit SQL Server.
-   Zusätzliche Konvertierung von Oracle VPD-Richtlinie, die beim Konvertieren in SQL Server-Richtlinienobjekten (Sicherheit auf Zeilenebene für Oracle).
-   Eine verringerte Zeit des anfänglichen Ladevorgangs für Oracle.
-   Verbesserte Parser und den resolvereinstellungen.
-   Überprüfen Sie Installationsprogramm für .net 2.0 wird entfernt.
-   Aktualisierte Erweiterung Pack Abhängigkeit von .net 3.5, .net 4.0.
-   Feste "Speichern" Projekt"und"Projekt öffnen"-Befehle für SSMA-Konsole.
-   Feste "Securepassword"-Befehl für SSMA-Konsole.
-   Korrektur von Objekten für das erstmalige laden zählen.
-   Korrektur der Zeichendatentypen beim Konvertieren eines für Oracle.
-   Korrektur von Bug in den globalen Einstellungen.
  
## <a name="march-2016"></a>März 2016  
März 2016 Preview-Version von SSMA für Oracle enthält die folgenden Änderungen:  
  
-   Unterstützung für die Migration zu SQL Server 2016.  
-   Unterstützung für die Migration von Oracle Sicherheit auf Zeilenebene (mit gewissen Einschränkungen) hinzugefügt.  
-   Zusätzliche Unterstützung für die Migration von Oracle im Arbeitsspeicher zu SQL Server-Spaltenspeicher Tabellen.  
  
## <a name="january-2016"></a>Januar 2016  
Im Januar 2014 Maintenance Release von SSMA für Oracle enthält die folgenden Änderungen:  
  
-   Unterstützung für gruppierte Indizes hinzugefügt.  
-   Korrektur langsame Abfragen für Oracle-Schema (RFC 5076207).  
-   Feste Azure aus der Konsole eine Verbindung hergestellt.  
-   Hinzugefügte Ansicht der Protokoll-Menüelement zu SSMA (RFC 5706203). 
-   Hinzugefügte Telemetrie.  
  
## <a name="july-2014"></a>Juli 2014  
Die Juli 2014-Version von SSMA für Oracle enthält die folgenden Änderungen:  
  
-   Unterstützung für Azure SQL-Datenbank hinzugefügt.  
-   Extension-Pack-Funktionen, die zur Unterstützung von Azure SQL-Datenbank in Schema verschoben werden.  
-   Unterstützung für Oracle materialisierte Sichten hinzugefügt.  
-   Unterstützung für Arbeitsspeicher von SQL Server 2014 Speicheroptimierte Tabellen.  
-   Leistungsverbesserungen enthalten, die für Datenbanken mit mehr als 10 KB Objekte getestet.  
-   UI-Verbesserungen für den Umgang mit einer großen Anzahl von Objekten hinzugefügt.  
-   Hinzugefügt, Hervorhebung von "bekannte" LOB-Schemas.  
-   Geschwindigkeitsverbesserungen Konvertierung enthalten.  
-   Unterstützung für das Objekt anzeigen zählt in der Benutzeroberfläche.  
-   Reduzierte Berichtsgröße von mehr als 25 %.
-   Verbesserte Fehlermeldungen für nicht verarbeitete Konstrukte.  
  
## <a name="april-2014"></a>April 2014  
Die Version April 2014 von SSMA für Oracle enthält die folgenden Änderungen:  
  
-   Unterstützung von MS SQL Server 2014 hinzugefügt.  
-   Unterstützung der Oracle-12 und Abfrage-Optimierung.  
-   Korrigierte Fehler hinsichtlich Konvertierung in Azure.  
-   Korrigierte Fehler bezüglich unsichtbar Berichtsseiten in Internet Explorer 10.  
  
## <a name="january-2012"></a>Januar 2012  
Die Januar 2012-Version von SSMA für Oracle enthält die folgenden Änderungen:  
  
-   Unterstützung für das RowType und RecordType Eingabeparameter standardmäßig auf NULL.  
  
## <a name="july-2011"></a>Vom Juli 2011  
Die vom Juli 2011-Version von SSMA für Oracle enthält die folgenden Änderungen:  
  
-   Zusätzliche Unterstützung für die Konvertierung von Oracle-Sequenz [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali" Sequenz-Generator.  
-   Verbesserte fehlerberichterstellung während der Datenmigration.  
-   Verbesserte Konvertierung der Anweisung, die Verwendung reservierter Wörter.  
-   Verbesserte implizite Konvertierung eines Date-Wert in einer Funktion.  
  
## <a name="april-2011"></a>April 2011  
Die April 2011 von SSMA für Oracle enthält die folgenden Änderungen:  
  
-   Konsolidierte "SSMA für Oracle"-Produkt, unterstützt [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008 und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali"  
-   Zusätzliche Unterstützung für die Verbindung, und Migrieren zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali"  
-   Erweiterte clientseitige Migration Datenmodul, parallele Migration von Daten unterstützen.  
-   Verbesserte Daten migrationsleistung mit einfachen und Bulk protokolliert Wiederherstellungsmodelle.  
-   Unterstützung für die Abwärtskompatibilität von Projekten von früheren Versionen von SSMA (v4. 0 und v4. 2) erstellt.  
-   Wurde die Möglichkeit zum Installieren von SSMA für Oracle V5. 0-Produkt parallel (SxS) mit älteren Versionen von SSMA (v4. 0 und v4. 2) hinzugefügt.  
-   Unterstützung für benutzerdefinierte Typen (einschließlich Untertyp, SAMMLUNGSDATENTYPEN, GESCHACHTELTE Tabelle, Objekttabelle und Objektansicht) und ihre Verwendung in PL/SQL-Blöcken mit speziellen Fehlermeldungen reporting hinzugefügt.  

## <a name="july-2010"></a>Juli 2010  
Die Version vom Juli 2010 von SSMA für Oracle enthält die folgenden Änderungen:  
  
-   Unterstützung für die Migration zu SQL Server 2008 R2 hinzugefügt.  
-   Eine neue Konsolenanwendung von SSMA, für die Ausführung über die Befehlszeile wird hinzugefügt.  
-   Unterstützung für die Datenmigration mithilfe von serverseitigen und clientseitigen Daten Migration Module hinzugefügt.  
-   Unterstützung für die "Benutzerdefinierter SELECT"-Anweisung in die Datenmigration hinzugefügt.  
-   Unterstützung für die Migration von Oracle 11g R2 hinzugefügt.  
  
## <a name="june-2008"></a>Juni 2008  
Die Juni 2008-Version von SSMA für Oracle enthält die folgenden Änderungen:  
  
-   Verbesserungen für den Assessment-Bericht, einschließlich zusätzliche Informationen, um nach Synonymen, unformatierte Quelle analysierbar Objekte, Bereiche und SQL Server-Logo-Deinstallation und layoutspeicherung hinzugefügt.  
-   Verbesserungen im Objekt-Konvertierung hinzugefügt:  
    -   Pakete DBMS_LOB, DBMS_SQL Konvertierung hinzugefügt.  
    -   Verknüpft die Konvertierung wurde überarbeitet.  
    -   Änderung von Sammlungen und Datensätze Konvertierung, jetzt der Datensätze in einfachen Fällen über separate Variablen für die einzelnen Felder veröffentlicht.  
    -   Verbesserungen der Datensätze und Sammlungen-Implementierung.  
    -   Aggregation Fensterfunktionen hinzugefügt.  
    -   ROLLUP-CUBE-Klausel hinzugefügt.  
    -   Verbesserung für NEXTVAL/CURVAL.  
    -   Gruppieren von in SET-Klausel Spalten wurden Grouping Sets, und Gruppieren von ID hinzugefügt.  
    -   MERGE-Anweisung hinzugefügt.  
    -   Unterstützung des neuen Datetime-Typen und der Konvertierung von Datensätzen und Auflistungen als CLR-Datentypen hinzugefügt.  
-   Neue Funktionen für Tester. Tabellen jetzt können getestet werden als Objekte mit Tester, eine Aufrufreihenfolge mehrerer getestet werden Objekte im Testfall kann geändert werden, Benutzer kann testen, Prozeduren und Funktionen mit Datensätzen und Sammlungen, die als Parameter und Rückgabewerte Werte und eine Abhängigkeiten, die Analyzer hinzugefügt wurde, um zu überprüfen, nur Tabellen verwendet.  
  
## <a name="august-2007"></a>August 2007  
Die August 2007-Version von SSMA für Oracle enthält die folgenden Änderungen:  
  
-   Hinzugefügte neue TESTER-Komponente können Sie die erstellen, verwalten und Ausführen von Testfällen mit konvertierten SQL-Code zu überprüfen.  
-   Unterstützung für die Konvertierung von Oracle-Untertypen, Auflistungen und lokale Module an SQL-Konverter hinzugefügt wurde.  
-   Hinzugefügt, dass eine neue Synchronisierungsfunktion können Sie bestimmte Objekte mit SQL Server-Datenbank zu synchronisieren.  
-   Neue Konvertierungsoptionen hinzugefügt.  
  
## <a name="april-2007"></a>April 2007  
Die Version April 2007 von SSMA für die Oracle war die erste Version.

---
title: "Was &#39; s in SSMA für Oracle (OracleToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f305ebb6-7393-4a43-abb3-6332b739d690
caps.latest.revision: 24
author: sabotta
ms.author: carlasab
manager: v-thobro
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 191fe2e11c43f4c190a87ee52df9ff87c259ea7d
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="what39s-new-in-ssma--for-oracle-oracletosql"></a>Was &#39; s in SSMA für Oracle (OracleToSQL)
In diesem Thema werden die SSMA für Oracle-Änderungen in jeder Version aufgelistet.  

## <a name="may-2016"></a>Mai 2016  
Die Mai 2016-Version von SSMA für Oracle enthält die folgenden Änderungen:  

1.  Unterstützung für SQL Server 2016
2.  Zusätzliche Konvertierung von Oracle Flashback Archivtabellen in temporalen Tabellen mit SQL Server
3.  Zusätzliche Konvertierung von Oracle VPD-Richtlinie, die beim Konvertieren in SQL Server-Richtlinienobjekten (Sicherheit auf Zeilenebene für Oracle)
4.  Eine verringerte Zeit des anfänglichen Ladevorgangs für Oracle
5.  Verbesserte Parser und Konfliktlöser
6.  Überprüfen Sie Installationsprogramm für .net 2.0 entfernt
7.  Aktualisierte Erweiterung Pack-Abhängigkeit von .net 3.5, .net 4.0
8.  Feste "Speichern" Projekt"und"Projekt öffnen"-Befehle für SSMA-Konsole
9.  Feste "Securepassword"-Befehl für SSMA-Konsole
10. Zählen von Objekten für das erstmalige laden behoben
11. Konvertieren von Unicodezeichen-Datentypen für Oracle behoben
12. Korrektur von Bug in den globalen Einstellungen
  
## <a name="march-2016"></a>März 2016  
März 2016 Preview-Version von SSMA für Oracle enthält die folgenden Änderungen:  
  
1.  Unterstützt die Migration zu SQL Server 2016  
  
2.  Unterstützung für die Migration von Oracle Sicherheit auf Zeilenebene (mit gewissen Einschränkungen)  
  
3.  Unterstützung für die Migration von Oracle im Arbeitsspeicher zu SQL Server-Spaltenspeicher Tabellen  
  
## <a name="january-2016"></a>Januar 2016  
Im Januar 2014 Maintenance Release von SSMA für Oracle enthält die folgenden Änderungen:  
  
1.  Unterstützung für gruppierte Indizes  
  
2.  Langsame Abfragen für Oracle-Schema (RFC 5076207) behoben  
  
3.  Feste Verbinden mit Azure über die Konsole  
  
4.  Hinzugefügte Ansicht Protokoll Menüelements SSMA (RFC 5706203)  
  
5.  Hinzugefügte Telemetrie  
  
## <a name="july-2014"></a>Juli 2014  
Die Juli 2014-Version von SSMA für Oracle enthält die folgenden Änderungen:  
  
1.  Unterstützung für Azure SQL-Datenbank  
  
2.  Extension-Pack-Funktionalität in Schema zur Unterstützung von Azure SQL-Datenbank verschoben  
  
3.  Unterstützung für Oracle materialisierte Sichten  
  
4.  Unterstützung für Arbeitsspeicher von SQL Server 2014 Speicheroptimierte Tabellen  
  
5.  Leistungsverbesserungen für Datenbanken mit mehr als 10 KB Objekte getestet  
  
6.  Verbesserungen der Benutzeroberfläche für den Umgang mit einer großen Anzahl von Objekten  
  
7.  Hervorheben von "bekannte" LOB-schemas  
  
8.  Konvertierung geschwindigkeitsverbesserungen  
  
9. Objektanzahl Benutzeroberfläche anzeigen  
  
10. Bericht Reduzierung der Größe von mehr als 25 %  
  
11. Verbesserte Fehlermeldungen für nicht verarbeitete Konstrukte.  
  
## <a name="april-2014"></a>April 2014  
Die Version April 2014 von SSMA für Oracle enthält die folgenden Änderungen:  
  
1.  Unterstützung von MS SQL Server 2014 hinzugefügt.  
  
2.  Unterstützung der Oracle-12 und Abfrage-Optimierung.  
  
3.  Korrigierte Fehler hinsichtlich Konvertierung in Azure.  
  
4.  Korrigierte Fehler bezüglich unsichtbar Berichtsseiten in Internet Explorer 10.  
  
## <a name="january-2012"></a>Januar 2012  
Die Januar 2012-Version von SSMA für Oracle enthält die folgenden Änderungen:  
  
-   Unterstützung RowType und RecordType Eingabeparameter standardmäßig auf NULL.  
  
## <a name="july-2011"></a>Vom Juli 2011  
Die vom Juli 2011-Version von SSMA für Oracle enthält die folgenden Änderungen:  
  
-   Unterstützung für die Konvertierung von Oracle-Sequenz [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali" Sequenz-Generator.  
  
-   Verbesserte fehlerberichterstellung während der Datenmigration.  
  
-   Verbesserte Konvertierung der Anweisung, die Verwendung reservierter Wörter.  
  
-   Verbesserte implizite Konvertierung eines Date-Wert in einer Funktion.  
  
## <a name="april-2011"></a>April 2011  
Die April 2011 von SSMA für Oracle enthält die folgenden Änderungen:  
  
-   Konsolidierte "SSMA für Oracle"-Produkt, unterstützt [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008 und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali".  
  
-   Unterstützung für die Verbindung, und Migrieren zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali".  
  
-   Erweiterte Client Side Migration Datenmodul, parallele Migration von Daten unterstützen.  
  
-   Verbesserte Daten migrationsleistung mit einfachen und Bulk protokolliert Wiederherstellungsmodelle.  
  
-   Abwärtskompatibilität von Projekten von früheren Versionen von SSMA (v4. 0 und v4. 2) erstellt.  
  
-   SSMA für die Oracle V5. 0-Produkt möglich installiert nebeneinander angezeigt werden (SxS) mit älteren Versionen von SSMA (v4. 0 und v4. 2).  
  
-   Unterstützung für die Berichterstattung, benutzerdefinierte Typen (einschließlich Untertyp, SAMMLUNGSDATENTYPEN, GESCHACHTELTE Tabelle, Objekttabelle und Objektansicht) und ihre Verwendung in PL/SQL-Blöcken mit speziellen Fehlermeldungen.  
  
## <a name="july-2010"></a>Juli 2010  
Die Version vom Juli 2010 von SSMA für Oracle enthält die folgenden Änderungen:  
  
-   Unterstützung für die Migration zu SQL Server 2008 R2  
  
-   Neue Konsolenanwendung mit SSMA für die Ausführung über die Befehlszeile  
  
-   Unterstützung für die Datenmigration mit sowohl serverseitige als auch Client Side Data Migration Module  
  
-   Unterstützung für die "Benutzerdefinierter SELECT"-Anweisung in der Datenmigration  
  
-   Unterstützung für die Migration von Oracle 11g R2  
  
## <a name="june-2008"></a>Juni 2008  
Die Juni 2008-Version von SSMA für Oracle enthält die folgenden Änderungen:  
  
-   Verbesserungen bei der Bewertungsbericht wurden abgeschlossen. Es enthält zusätzliche Informationen, um nach Synonymen, unformatierte Quelle analysierbar Objekte, Bereiche und SQL Server-Logo-Deinstallation und layoutspeicherung.  
  
-   Verbesserungen bei der Konvertierung des Objekts:  
  
    -   Pakete DBMS_LOB, DBMS_SQL Konvertierung hinzugefügt.  
  
    -   Verknüpft die Konvertierung wurde überarbeitet.  
  
    -   Änderung von Sammlungen und Datensätze Konvertierung, jetzt der Datensätze in einfachen Fällen über separate Variablen für die einzelnen Felder veröffentlicht.  
  
    -   Verbesserungen der Datensätze und Sammlungen-Implementierung.  
  
    -   Aggregation Fensterfunktionen hinzugefügt.  
  
    -   ROLLUP-CUBE-Klausel hinzugefügt.  
  
    -   Verbesserung für NEXTVAL/CURVAL.  
  
    -   Spalten, die in der SET-Klausel zu gruppieren, wurden Grouping Sets, und gruppieren die ID hinzugefügt.  
  
    -   MERGE-Anweisung hinzugefügt.  
  
    -   Unterstützung des neuen Datetime-Typen und der Konvertierung von Datensätzen und Auflistungen als CLR-Datentypen hinzugefügt.  
  
-   Es wurden neue Funktionen für Tester hinzugefügt. Tabellen jetzt können getestet werden als Objekte mit Tester, eine Aufrufreihenfolge mehrerer getestet werden Objekte im Testfall kann geändert werden, Benutzer kann testen, Prozeduren und Funktionen mit Datensätzen und Sammlungen, die als Parameter und Rückgabewerte Werte und eine Abhängigkeiten, die Analyzer hinzugefügt wurde, um zu überprüfen, nur Tabellen verwendet.  
  
## <a name="august-2007"></a>August 2007  
Die August 2007-Version von SSMA für Oracle enthält die folgenden Änderungen:  
  
-   Eine neue TESTER-Komponente können Sie erstellen, verwalten und Ausführen von Testfällen mit konvertierten SQL-Code zu überprüfen.  
  
-   Konvertierung von Oracle-Untertypen, Auflistungen und lokale Module an SQL-Konverter hinzugefügt wurde.  
  
-   Eine neue Synchronisierungsfunktion können Sie bestimmte Objekte mit SQL Server-Datenbank zu synchronisieren.  
  
-   Neue Optionen hinzugefügt.  
  
## <a name="april-2007"></a>April 2007  
Die Version April 2007 von SSMA für die Oracle war die erste Version.  
  


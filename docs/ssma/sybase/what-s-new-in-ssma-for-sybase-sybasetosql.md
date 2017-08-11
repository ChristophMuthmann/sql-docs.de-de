---
title: "Was &#39; s in SSMA für Sybase (SybaseToSQL) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 2be0cf8d-6dbe-443a-abbd-036249922205
caps.latest.revision: 21
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 9d97e03212e6985ce9d506774bfff0aa2f4ec8d1
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="what39s-new-in-ssma--for-sybase-sybasetosql"></a>Was &#39; s in SSMA für Sybase (SybaseToSQL)
In diesem Thema werden die SSMA für Sybase-Änderungen in jeder Version aufgelistet.  

## <a name="may-2016"></a>Mai 2016  
Die Mai 2016-Version von SSMA für Sybase enthält die folgenden Änderungen:  

1.  Unterstützung für SQL Server 2016
2.  Überprüfen Sie Installationsprogramm für .net 2.0 entfernt
3.  Aktualisierte Erweiterung Pack-Abhängigkeit von .net 3.5, .net 4.0
4.  Feste "Speichern" Projekt"und"Projekt öffnen"-Befehle für SSMA-Konsole
5.  Feste "Securepassword"-Befehl für SSMA-Konsole
6.  Zählen von Objekten für das erstmalige laden behoben
7.  Korrektur von Bug in den globalen Einstellungen

## <a name="march-2016"></a>März 2016  
Die März 2016 Preview-Version von SSMA für Sybase enthält die folgenden Änderungen:  
  
1.  Unterstützt die Migration zu SQL Server 2016  
  
## <a name="january-2016"></a>Januar 2016  
Die Januar 2016 Wartung-Version von SSMA für Sybase enthält die folgenden Änderungen:  
  
1.  Hinzugefügte Ansicht Protokoll Menüelements SSMA (RFC 5706203)  
  
2.  Hinzugefügte Telemetrie  
  
## <a name="july-2014"></a>Juli 2014  
Die Version Juli 2014 von SSMA für Sybase enthält die folgenden Änderungen:  
  
1.  Verbesserte codekonvertierung für Azure SQL-Datenbank  
  
2.  Extension-Pack-Funktionalität in Schema zur Unterstützung von Azure SQL-Datenbank verschoben  
  
3.  Leistungsverbesserungen für Datenbanken mit mehr als 10 KB Objekte getestet  
  
4.  Verbesserungen der Benutzeroberfläche für den Umgang mit einer großen Anzahl von Objekten  
  
5.  Hervorheben von "bekannte" LOB-Schemas (damit sie bei der Konvertierung ignoriert werden können)  
  
6.  Konvertierung geschwindigkeitsverbesserungen  
  
7.  Objektanzahl Benutzeroberfläche anzeigen  
  
8.  Bericht Reduzierung der Größe von mehr als 25 %  
  
9. Verbesserte Fehlermeldungen für nicht verarbeitete Konstrukte.  
  
## <a name="april-2014"></a>April 2014  
Die Version April 2014 von SSMA für Sybase enthält die folgenden Änderungen:  
  
-   Unterstützung von MS SQL Server 2014 hinzugefügt.  
  
-   Korrigierte Fehler hinsichtlich Konvertierung in Azure  
  
-   Korrigierte Fehler bezüglich unsichtbar Berichtsseiten in Internet Explorer 10.  
  
## <a name="january-2012"></a>Januar 2012  
Das Januar 2012-Version von SSMA für Sybase enthält die folgenden Änderungen:  
  
-   Unterstützung für die Konvertierung der Rollback-Trigger.  
  
-   Fix für die Konvertierung bereitgestellten@ROWCOUNT und @@ERROR in der gleichen SET-Anweisung.  
  
## <a name="july-2011"></a>Vom Juli 2011  
Die vom Juli 2011-Version von SSMA für Sybase enthält die folgenden Änderungen:  
  
-   Verbesserte fehlerberichterstellung während der Datenmigration.  
  
## <a name="april-2011"></a>April 2011  
Die April 2011 von SSMA für Sybase enthält die folgenden Änderungen:  
  
-   Konsolidierte "SSMA für Sybase"-Produkt, unterstützt [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali" und SQL Azure.  
  
-   Unterstützung für die Verbindung, und Migrieren zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali".  
  
-   Neuen Feature konvertieren und Migrieren von Sybase-Datenbanken zu SQL Azure.  
  
-   Erweiterte Client Side Migration Datenmodul, parallele Migration von Daten unterstützen.  
  
-   Verbesserte Daten migrationsleistung mit einfachen und Bulk protokolliert Wiederherstellungsmodelle.  
  
-   Groß-/Kleinschreibung beachtet Sybase-Datenbanken können ordnungsgemäß konvertiert und zu Groß-/Kleinschreibung beachtet SQL Server migriert werden.  
  
-   Unterstützung für die Konvertierung von Sybase ASE nicht ANSI-Joinanweisungen für SQL Server-ANSI-Join-Anweisungen wurde erweitert, um zu löschen und UPDATE-Anweisungen.  
  
-   Zusätzliche Verbindungsoptionen für die Verbindung mit der Sybase ASE-Server mithilfe von Sybase ASE ODBC-Anbieter und Anbieter für Sybase ASE ADO.Net.  
  
-   Entfernen der Abhängigkeit, die in einer separaten Datenbank bezeichnet **SysDB** enthält die Sybase-Emulation-Funktionen (als Teil der Erweiterung Pack installiert).  
  
-   SSMA für Sybase Erweiterung Pack kann jetzt installiert werden, auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Clustern.  
  
-   Abwärtskompatibilität von Projekten von früheren Versionen von SSMA (v4. 0 und v4. 2) erstellt.  
  
-   SSMA für Sybase V5. 0-Produkt möglich installiert nebeneinander angezeigt werden (SxS) mit älteren Versionen von SSMA (v4. 0 und v4. 2).  
  
## <a name="july-2010"></a>Juli 2010  
Die Version vom Juli 2010 von SSMA für Sybase enthält die folgenden Änderungen:  
  
-   Unterstützung für die Migration zu SQL Server 2008 R2  
  
-   Neue Konsolenanwendung mit SSMA für die Ausführung über die Befehlszeile  
  
-   Unterstützung für die Datenmigration mit sowohl serverseitige als auch Client Side Data Migration Module  
  
-   Unterstützung für die "Benutzerdefinierter SELECT"-Anweisung in der Datenmigration  
  
-   Unterstützung für die Migration von Sybase ASE 15.0.3 und 15.5  
  
## <a name="june-2008"></a>Juni 2008  
Die Juni 2008-Version von SSMA für Sybase enthält die folgenden Änderungen:  
  
-   SSMA-Tester hinzugefügt, wird überprüft automatisch die Konvertierung der Datenbank-Objekt und die Datenmigration von SSMA vorgenommen werden. Nachdem Sie alle Schritte der SSMA-Migration abgeschlossen wurden, verwenden Sie SSMA Tester, stellen Sie sicher, dass die konvertierte Objekte die gleiche Weise funktioniert und alle Daten ordnungsgemäß übertragen wurde.  
  
-   Versionen vor SQL-Konvertierung hinzugefügt. Benutzer kann jetzt temporäre Tabellen (und andere Objekte) angeben Deklarationen für jede Quelle-Prozedur, die in der Konvertierung verwendet werden.  
  
-   Verbesserungen bei der Konvertierung des Objekts:  
  
    -   Verknüpft die Konvertierung wurde überarbeitet.  
  
    -   Aggregate und nicht-Aggregate ohne-müssen/Group by-Klauseln.  
  
    -   Die IDENTITY-Funktion mit einer SELECT INTO-Anweisung.  
  
    -   Gruppierten Einschränkungen und Indizes auf Daten nur gesperrt.  
  
    -   Temporäre Tabellen, die von SELECT INTO erstellt werden.  
  
    -   Einschränkungen / indiziert für temporäre Tabellen.  
  
    -   Neue [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008 "DateTime"-Typen werden unterstützt.  
  
    -   Unterstützung von Sybase-15.0-Konnektivität und Datentypen.  
  
## <a name="may-2007"></a>Mai 2007  
Die Mai 2007-Version von SSMA für Sybase enthält die folgenden Änderungen:  
  
-   Wenn Sie ein Projekt zu speichern, ist das Laden des Inhalts der Datenbank schneller.  
  
-   Unterstützung für die eingegebenen Kommentare, dass der SQL Server SQL Modus formatiert.  
  
-   Verbesserungen bei der Konvertierung des Objekts.  
  
Beachten Sie, dass die Hilfedatei wurde nicht für diese Version aktualisiert. Weitere Informationen finden Sie im Abschnitt "Hinweise zur Dokumentation" weiter unten in diesem Thema.  
  
## <a name="november-2006"></a>November 2006  
Die Version für November 2006 von SSMA für Sybase enthält die folgenden Änderungen:  
  
-   Neue globale Einstellungen:  
  
    -   Wahlweise können Sie zum Anzeigen von Zeilennummern im Editor-Fenstern.  
  
    -   Sie können konfigurieren SSMA aufgefordert werden, um doppelt vorhandene Objekte zu ersetzen, oder Sie können immer oder niemals ersetzen doppelte Objekte während der schemakonvertierung.  
  
-   Neue Konvertierungsoptionen können Sie konfigurieren, wie die folgenden Situationen von SSMA behandelt:  
  
    -   Eine CAST oder CONVERT-Anweisung, die eine binäre Zeichenfolge enthält.  
  
    -   Null-Werte in Gleichheitsausdrücken auf überprüft  
  
    -   Proxy-Tabellen  
  
    -   Benutzer Fehler Meldungsnummern für RAISERROR  
  
    -   UPDATE-Anweisungen, die nicht aufgelösten Bezeichner enthalten.  
  
-   Eine neue Migrationsoption können Sie angeben, wie SSMA Datumsangaben behandeln soll, die sich außerhalb der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datumsbereich.  
  
-   Ein **formatiert SQL** festlegen, auf die **SQL** Registerkarte, die den Code, zur besseren Lesbarkeit formatiert.  
  
-   Fehlerbehebungen, die Folgendes enthalten:  
  
    -   SSMA konvertiert nun SPERRTABELLE *Tabelle* IN {SHARED | EXKLUSIVE} Modus Anweisungen von der nachfolgenden SELECT-Abfrage für die Tabelle hinzugefügt TABLOCK oder TABLOCKX-Hinweis.  
  
    -   Die erforderlichen Umwandlungen werden nun hinzugefügt werden, wenn Binärtypen in Zeichenausdrücke verwendet werden.  
  
    -   Verbesserungen der Arbeitsspeicher- und Leistungsproblemen.  
  
## <a name="july-2006"></a>Juli 2006  
Die Version von Juli 2006 von SSMA für Sybase war die erste Version.  
  
## <a name="see-also"></a>Siehe auch  
[Erste Schritte mit SSMA für Sybase &#40; SybaseToSQL &#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)  
  


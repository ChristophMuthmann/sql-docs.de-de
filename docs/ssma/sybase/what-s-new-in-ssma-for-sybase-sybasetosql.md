---
title: "Was &#39; s in SSMA für die SAP ASE (SybaseToSQL) | Microsoft Docs"
ms.custom: 
ms.date: 09/30/2017
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
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: e3c781449a8f7a1b236508cd21b8c00ff175774f
ms.openlocfilehash: 91c748f24b360934e160cea8b03c2c2259766a5c
ms.contentlocale: de-de
ms.lasthandoff: 09/30/2017

---
# <a name="what39s-new-in-ssma-for-sap-ase-sybasetosql"></a>Was &#39; s in SSMA für die SAP ASE (SybaseToSQL)
In diesem Thema werden die SSMA für SAP ASE (früher SSMA für Sybase) Änderungen in jeder Version aufgelistet. 

## <a name="ssma-v76"></a>SSMA v7.6
Die v7.6-Version von SSMA für SAP ASE enthält die folgenden Änderungen:
- SSMA für die SAP ASE wurde verbessert, wobei targeted Fehlerbehebungen, die Qualität und Konvertierung Metriken zu verbessern und mit Unterstützung für SQL Server-2017 (öffentliche Vorschau). Unterstützung für SQL Server-2017 auf Windows- und Linux ist als öffentliche Vorschau verfügbar und sollte nicht für die Produktionsmigrationen verwendet werden.
- SSMA für die SAP ASE wurde aktualisiert, um Unterstützung für die Konvertierung von Sybase-Funktionen bereitstellen.

> [!IMPORTANT]
> SSMA v7.4 und höhere Versionen .net 4.5.2 ist eine Voraussetzung für Installation, und die 32-Bit-Version des Tools wurde eingestellt.

## <a name="ssma-v75"></a>SSMA 7.5
Die Version 7.5 von SSMA für SAP ASE enthält die folgenden Änderungen:
-   Durch mehrere Verbesserungen an größere Barrierefreiheit für Personen mit behinderungen stellen Sie sicher, verbessert.
-   Aktualisiert, um Unterstützung für Syntax zu erstellen oder zu ersetzen.

> [!IMPORTANT]
> .NET 4.5.2 ist eine Voraussetzung für die Installation von SSMA 7.5. Darüber hinaus wird v7.4 ab, die 32-Bit-Version von SSMA nicht mehr unterstützt wird.  

## <a name="ssma-v74"></a>SSMA v7.4
Die v7.4-Version von SSMA für Sybase enthält die folgenden Änderungen:
- Die **Abfragetimeout** Option ist während der Ermittlung an Quelle und Ziel Schema verfügbar.
![Option Timeout für Remoteabfragen](../media/query-timeout_red.png)
- Die Qualität und Konvertierung Metrik wurde mit targeted Fehlerbehebungen, aufgrund von Kundenfeedback verbessert.

> [!IMPORTANT]
> .NET 4.5.2 ist eine Voraussetzung für die Installation von SSMA v7.4. Darüber hinaus wird v7.4 ab, die 32-Bit-Version von SSMA nicht mehr unterstützt wird.  

## <a name="ssma-v73"></a>SSMA V7. 3
Die V7. 3-Version von SSMA für Sybase enthält die folgenden Änderungen:
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
Die V7. 2-Version von SSMA für Sybase enthält die folgenden Änderungen:
- Verbesserte Qualität und Konvertierung Metrik mit dem Ziel Korrekturen, die basierend auf Kundenfeedback.
- Telemetrie-Erweiterungen bieten eine bessere Datenpunkte, um Kundenprobleme zu beheben und zu verbessern SSMAs-Wechselkurse.

## <a name="ssma-v71"></a>SSMA v7.1
Die v7.1-Version von SSMA für Access umfasst die folgenden Änderungen:
- SQL Server-2017 auf Windows- und Linux CTP1 ist jetzt eine unterstützte Zielplattform für die Migration. Dieses Feature ist in der technischen Vorschau und Verschieben von Schema und Daten an SQL-Zielserver unterstützt.
- SSMA unterstützt jetzt die automatische Updates, um die neueste Version von SSMA herunterladen, sobald es verfügbar ist.
- Installierbare SSMA-Binärdateien werden jetzt über Windows Installer-Paket-Dateien (.msi) übermittelt.

**Ressourcen**

[Erweitern von SQL Server Migration Assistant Funktionen](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)

[Bewerten und Migrieren von Daten aus datenplattformen nicht von Microsoft SQL Server *(mit der Oracle-Beispiel)*](https://blogs.msdn.microsoft.com/datamigration/2016/11/16/sql-server-migration-assistant-how-to-assess-and-migrate-databases-from-non-microsoft-data-platforms-to-sql-server/) 

## <a name="may-2016"></a>Mai 2016  
Die Mai 2016-Version von SSMA für Sybase enthält die folgenden Änderungen:  

-  Unterstützung für SQL Server 2016.
-  Überprüfen Sie Installationsprogramm für .net 2.0 wird entfernt.
-  Aktualisierte Erweiterung Pack Abhängigkeit von .net 3.5, .net 4.0.
-  Feste "Speichern" Projekt"und"Projekt öffnen"-Befehle für SSMA-Konsole.
-  Feste "Securepassword"-Befehl für SSMA-Konsole.
-  Korrektur von Objekten für das erstmalige laden zählen.
-  Korrektur von Bug in den globalen Einstellungen.

## <a name="march-2016"></a>März 2016  
Die März 2016 Preview-Version von SSMA für Sybase enthält die folgenden Änderungen:  
  
-  Unterstützung für die Migration zu SQL Server 2016.  
  
## <a name="january-2016"></a>Januar 2016  
Die Januar 2016 Wartung-Version von SSMA für Sybase enthält die folgenden Änderungen:  
  
-  Hinzugefügte Ansicht der Protokoll-Menüelement zu SSMA (RFC 5706203).  
-  Hinzugefügte Telemetrie. 
  
## <a name="july-2014"></a>Juli 2014  
Die Version Juli 2014 von SSMA für Sybase enthält die folgenden Änderungen:  
  
-  Verbesserte codekonvertierung für Azure SQL-Datenbank.  
-  Erweiterung Pack-Funktion zum Schema zur Unterstützung von Azure SQL-Datenbank verschoben.  
-  Zusätzliche leistungsverbesserungen getestet Objekte für Datenbanken mit mehr als 10 KB.  
-  UI-Verbesserungen für den Umgang mit einer großen Anzahl von Objekten hinzugefügt.  
-  Wurde die Möglichkeit zum Hervorheben von "bekannte" LOB-Schemas (damit sie bei der Konvertierung ignoriert werden können) hinzugefügt.  
-  Geschwindigkeitsverbesserungen Konvertierung wird hinzugefügt.  
-  Hinzugefügt, die Fähigkeit, Objektanzahl Benutzeroberfläche anzuzeigen. 
-  Reduzierte Berichtsgröße von mehr als 25 %.  
-  Verbesserte Fehlermeldungen für nicht verarbeitete Konstrukte.  
  
## <a name="april-2014"></a>April 2014  
Die Version April 2014 von SSMA für Sybase enthält die folgenden Änderungen:  
  
-   Unterstützung von MS SQL Server 2014 hinzugefügt.  
-   Korrigierte Fehler hinsichtlich Konvertierung in Azure.  
-   Korrigierte Fehler bezüglich unsichtbar Berichtsseiten in Internet Explorer 10.  
  
## <a name="january-2012"></a>Januar 2012  
Das Januar 2012-Version von SSMA für Sybase enthält die folgenden Änderungen:  
  
-   Unterstützung für die Konvertierung der Rollback-Trigger hinzugefügt.  
-   Fix für die Konvertierung bereitgestellten@ROWCOUNT und @@ERROR in der gleichen SET-Anweisung.  
  
## <a name="july-2011"></a>Vom Juli 2011  
Die vom Juli 2011-Version von SSMA für Sybase enthält die folgenden Änderungen:  
  
-   Verbesserte fehlerberichterstellung während der Datenmigration.  
  
## <a name="april-2011"></a>April 2011  
Die April 2011 von SSMA für Sybase enthält die folgenden Änderungen:  
  
-   Konsolidierte "SSMA für Sybase"-Produkt, unterstützt [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali" und SQL Azure.  
-   Zusätzliche Unterstützung für die Verbindung, und Migrieren zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali"  
-   Eine neue Funktion zum Konvertieren und Migrieren von Sybase-Datenbanken zu SQL Azure hinzugefügt.  
-   Erweiterte clientseitige Migration Datenmodul, parallele Migration von Daten unterstützen.  
-   Verbesserte Daten migrationsleistung mit einfachen und Bulk protokolliert Wiederherstellungsmodelle.  
-   Wurde die Möglichkeit ordnungsgemäß konvertieren und Migrieren von Sybase-Datenbanken, die Groß-/Kleinschreibung beachtet, Groß-/Kleinschreibung SQL-Server hinzugefügt.  
-   Unterstützung für die Konvertierung von Sybase ASE nicht ANSI-Joinanweisungen für SQL Server-ANSI-Join-Anweisungen hinzugefügt wurde erweitert, damit löschen und UPDATE-Anweisungen.  
-   Zusätzliche Verbindungsoptionen für Verbindungen mit Verwendung Sybase ASE ODBC-Anbieter und Sybase ASE ADO.NET-Anbietern Sybase ASE-Servern wird bereitgestellt.  
-   Entfernt die Abhängigkeit auf einer separaten Datenbank mit dem Namen **SysDB**, enthält die Sybase-Emulation-Funktionen (als Teil der Erweiterung Pack installiert).  
-   Die Möglichkeit zum Installieren von SSMA für Sybase Erweiterung Pack auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Clustern.  
-   Hinzugefügte Abwärtskompatibilität von Projekten von früheren Versionen von SSMA (v4. 0 und v4. 2) erstellt.  
-   Wurde die Möglichkeit zum Installieren von SSMA für Sybase V5. 0 Produkt Seite-an-Seite (SxS) mit älteren Versionen von SSMA (v4. 0 und v4. 2) hinzugefügt.  
  
## <a name="july-2010"></a>Juli 2010  
Die Version vom Juli 2010 von SSMA für Sybase enthält die folgenden Änderungen:  
  
-   Unterstützung für die Migration zu SQL Server 2008 R2 hinzugefügt.  
-   Eine neue Konsolenanwendung von SSMA, für die Ausführung über die Befehlszeile wird hinzugefügt.  
-   Unterstützung für die Datenmigration mithilfe von serverseitigen und clientseitigen Daten Migration Module hinzugefügt.  
-   Unterstützung für die "Benutzerdefinierter SELECT"-Anweisung in die Datenmigration hinzugefügt.  
-   Unterstützung für das Migrieren von Sybase ASE 15.0.3 und 15.5 hinzugefügt.  
  
## <a name="june-2008"></a>Juni 2008  
Die Juni 2008-Version von SSMA für Sybase enthält die folgenden Änderungen:  
  
-   Hinzugefügte SSMA-Tester, der getestet wird automatisch die Konvertierung der Datenbank-Objekt und die Datenmigration von SSMA vorgenommen werden. Nachdem Sie alle Schritte der SSMA-Migration abgeschlossen wurden, verwenden Sie SSMA Tester, stellen Sie sicher, dass die konvertierte Objekte die gleiche Weise funktioniert und alle Daten ordnungsgemäß übertragen wurde.  
-   Versionen vor SQL-Konvertierung hinzugefügt. Benutzer kann jetzt temporäre Tabelle (und ein anderes Objekt) angeben Deklarationen für jede Quelle-Prozedur, die in der Konvertierung verwendet werden.  
-   Verbesserungen im Objekt-Konvertierung hinzugefügt:  
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
  
-   Hinzugefügt, die Möglichkeit, den Datenbankinhalt schneller geladen, wenn Sie ein Projekt zu speichern.  
-   Unterstützung für die eingegebenen Kommentare in der SQL Server formatiert SQL-Modus.  
-   Verbesserungen im Objekt-Konvertierung hinzugefügt.  
  
Die Hilfedatei wurde nicht für diese Version aktualisiert. Weitere Informationen finden Sie im Abschnitt "Hinweise zur Dokumentation" weiter unten in diesem Thema.  
  
## <a name="november-2006"></a>November 2006  
Die Version für November 2006 von SSMA für Sybase enthält die folgenden Änderungen:  
  
-   Hinzugefügte neue globale Einstellungen:  
    -   Wahlweise können Sie zum Anzeigen von Zeilennummern im Editor-Fenstern.  
    -   Sie können konfigurieren SSMA aufgefordert werden, um doppelt vorhandene Objekte zu ersetzen, oder Sie können immer oder niemals ersetzen doppelte Objekte während der schemakonvertierung.  
-   Eine neue Konvertierungsoption, mit dem Sie konfigurieren, wie die folgenden Situationen von SSMA verarbeitet hinzugefügt:  
    -   Eine CAST oder CONVERT-Anweisung, die eine binäre Zeichenfolge enthält.  
    -   Überprüft, ob null-Werte in Gleichheitsausdrücke.  
    -   Proxy-Tabellen.  
    -   Benutzer Nachricht Fehlernummern für RAISERROR.  
    -   UPDATE-Anweisungen, die nicht aufgelösten Bezeichner enthalten.  
-   Fügt eine neue Migrationsoption, mit dem Sie angeben, wie SSMA Datumsangaben behandeln soll, die sich außerhalb der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datumsbereich.  
-   Hinzugefügt eine **formatiert SQL** festlegen, auf die **SQL** Registerkarte, die den Code, zur besseren Lesbarkeit formatiert.  
-   Fehlerbehebungen, die Folgendes enthalten:  
    -   SSMA konvertiert nun SPERRTABELLE *Tabelle* IN {SHARED | EXKLUSIVE} Modus Anweisungen von der nachfolgenden SELECT-Abfrage für die Tabelle hinzugefügt TABLOCK oder TABLOCKX-Hinweis.  
    -   Die erforderlichen Umwandlungen werden nun hinzugefügt werden, wenn Binärtypen in Zeichenausdrücke verwendet werden.  
    -   Verbesserungen der Arbeitsspeicher- und Leistungsproblemen.  
  
## <a name="july-2006"></a>Juli 2006  
Die Version von Juli 2006 von SSMA für Sybase war die erste Version.  
  
## <a name="see-also"></a>Siehe auch  
[Erste Schritte mit SSMA für Sybase &#40; SybaseToSQL &#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)


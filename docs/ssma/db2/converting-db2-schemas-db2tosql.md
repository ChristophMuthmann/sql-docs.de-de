---
title: Konvertieren von DB2-Schemas (DB2ToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 7947efc3-ca86-4ec5-87ce-7603059c75a0
caps.latest.revision: 9
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: a1463d2f715bb957c28064840dcf0ce33e3a0f1e
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="converting-db2-schemas-db2tosql"></a>Konvertieren von DB2-Schemas (DB2ToSQL)
Nachdem Sie eine Verbindung mit DB2 hergestellt haben, verbunden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], und Set-Projekt und Datenoptionen für die Zuordnung, können Sie DB2-Datenbankobjekte zu konvertieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Datenbankobjekten.  
  
## <a name="the-conversion-process"></a>Konvertierungsprozess  
Konvertieren von Datenbankobjekten die Objektdefinitionen aus DB2 dauert, konvertiert diese in ähnliche [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Objekte und lädt dann diese Informationen in die SSMA-Metadaten. Es lädt nicht die Informationen in der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Sie können dann die Objekte und deren Eigenschaften anzeigen, mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Metadaten-Explorer.  
  
Bei der Konvertierung druckt SSMA Ausgabenachrichten in den Ausgabebereich und Fehlermeldungen in den Bereich Fehlerliste. Verwenden Sie die Ausgabe und Fehler Informationen, um festzustellen, ob Sie so ändern Sie die DB2-Datenbanken oder die Konvertierung in die gewünschte Konvertierungsergebnisse zu erhalten haben.  
  
## <a name="setting-conversion-options"></a>Festlegen von Optionen  
Lesen Sie vor dem Konvertieren von Objekten, das Projekt Konvertierungsoptionen in der **Projekteinstellungen** (Dialogfeld). Mithilfe dieses Dialogfelds können Sie festlegen, wie SSMA Funktionen und globalen Variablen konvertiert. Weitere Informationen finden Sie unter [Projekteinstellungen &#40; Konvertierung &#41; &#40; DB2ToSQL &#41; ](../../ssma/db2/project-settings-conversion-db2tosql.md).  
  
## <a name="conversion-results"></a>Konvertierungsergebnisse  
Die folgende Tabelle zeigt, welche DB2 Objekte konvertiert werden, und die resultierende [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Objekte:  
  
|DB2-Objekte|Resultierende SQL Server-Objekte|  
|-----------|----------------------------|  
|Datentypen|**SSMA ist jeder Typ außer den nachfolgend aufgeführten folgenden zugeordnet:**<br /><br />CLOB: Einige systemeigenen Funktionen für die Arbeit mit diesem Typ werden nicht unterstützt (z. B. CLOB_EMPTY())<br /><br />BLOB: Einige systemeigenen Funktionen für die Arbeit mit diesem Typ werden nicht unterstützt (z. B. BLOB_EMPTY())<br /><br />DBLOB: Einige systemeigenen Funktionen für die Arbeit mit diesem Typ werden nicht unterstützt (z. B. DBLOB_EMPTY())|  
|Benutzerdefinierte Typen|**SSMA ordnet die folgenden benutzerdefinierten:**<br /><br />DISTINCT-Typ<br /><br />Strukturierter Typ<br /><br />SQL-PL-Datentypen – Hinweis: unsichere Cursortyp werden nicht unterstützt.|  
|Spezielle Register|**SSMA ordnet nur die unten aufgeführten Register:**<br /><br />AKTUELLER ZEITSTEMPEL<br /><br />AKTUELLES DATUM<br /><br />AKTUELLE UHRZEIT<br /><br />AKTUELLE ZEITZONE<br /><br />AKTUELLER BENUTZER<br /><br />SESSION_USER und Benutzer<br /><br />SYSTEM_USER<br /><br />AKTUELLE CLIENT_APPLNAME<br /><br />AKTUELLE CLIENT_WRKSTNNAME<br /><br />AKTUELLE SPERRTIMEOUT<br /><br />AKTUELLES SCHEMA<br /><br />AKTUELLEN SERVER<br /><br />AKTUELLE ISOLATIONSSTUFE<br /><br />Andere spezielle Register werden nicht mit SQLServer semantische zugeordnet.|  
|CREATE TABLE|**SSMA ist CREATE TABLE zugeordnet, mit folgenden Ausnahmen:**<br /><br />Mehrdimensionale clustering (MDC) Tabellen<br /><br />Bereich gruppierte Tabellen (RCT)<br /><br />Partitionierte Tabellen<br /><br />Getrennte Tabelle<br /><br />DATA CAPTURE-Klausel<br /><br />Option IMPLICITLY AUSGEBLENDET<br /><br />VOLATILE-option|  
|CREATE VIEW|SSMA ordnet CREATE VIEW mit "Mit lokalen CHECK OPTION", aber andere Optionen sind auf SQL Server-Semantik nicht zugeordnet|  
|CREATE INDEX|**SSMA ordnet CREATE INDEX mit den folgenden Ausnahmen:**<br /><br />XML-Index<br /><br />Option BUSINESS_TIME ohne ÜBERLAPPT<br /><br />PARTITIONIERTE-Klausel<br /><br />Option "nur-Spezifikation"<br /><br />Mithilfe von erweitern-option<br /><br />MINPCTUSED-option<br /><br />SEITENTEILUNG-option|  
|Trigger|**SSMA ist der folgende Trigger Semantik zugeordnet:**<br /><br />Nach dem / für EACH ROW-Trigger<br /><br />Nach dem /FOR löst jeder Anweisung<br /><br />Bevor Sie / für EACH Zeile und INSTEAD OF / für MEHRZEILIGE EACH Trigger|  
|Sequenzen|Zugeordnet sind.|  
|SELECT-Anweisung|**Wählen Sie SSMA-Karten mit folgenden Ausnahmen:**<br /><br />Daten-Change-Tabellenverweis-Klausel – teilweise zugeordnet, aber endgültigen Tabellen wird nicht unterstützt<br /><br />Tabellenverweis Klausel – teilweise zugeordnet, aber nur--Tabellenverweis, äußere Tabellenverweis, Analyze_table-Ausdruck, Auflistung abgeleitete Tabelle Xmltable-Ausdruck sind, nicht zugeordnet, SQL Server-Semantik<br /><br />Punkt-zu-Spezifikation-Klausel – nicht zugeordnet.<br /><br />Weiterhin Handler-Klausel – nicht zugeordnet.<br /><br />Typisierte-Abhängigkeitsklausel – nicht zugeordnet.<br /><br />Gleichzeitiger Zugriff Auflösung-Klausel – nicht zugeordnet.|  
|VALUES-Anweisung|Wird zugeordnet.|  
|INSERT-Anweisung|Wird zugeordnet.|  
|UPDATE-Anweisung|S**SMA ordnet UPDATE mit den folgenden Ausnahmen:**<br /><br />Tabellenverweis Klausel – nur--Tabellenverweis wird SQL Server-Semantik nicht zugeordnet.<br /><br />Period-Klausel – ist nicht zugeordnet.|  
|MERGE-Anweisung|**SSMA ordnet MERGE mit folgenden Ausnahmen:**<br /><br />Einzelne oder mehrere Vorkommen of Each-Klausel: SQL Server-Semantik für jede Klausel beschränkt Vorkommen zugeordnet ist<br /><br />SIGNAL-Klausel – entspricht keinem SQL Server-Semantik<br /><br />Gemischte UPDATE und Klauseln löschen – entspricht keinem SQL Server-Semantik<br /><br />Punkt-Klausel – entspricht keinem SQL Server-Semantik|  
|DELETE-Anweisung|**SSMA-Zuordnungen löschen mit folgenden Ausnahmen:**<br /><br />Tabellenverweis Klausel – nur--Tabellenverweis wird SQL Server-Semantik nicht zugeordnet.<br /><br />Period-Klausel – entspricht keinem SQL Server-Semantik|  
|Isolationsstufe und Sperrentyp|Wird zugeordnet.|  
|Prozeduren (SQL)|Zugeordnet sind.|  
|Prozeduren (extern)|Manuelles Update erforderlich.|  
|Prozeduren (Quelle)|SQL Server-Semantik nicht zuordnen.|  
|Zuweisungsanweisung|Wird zugeordnet.|  
|CALL-Anweisung für eine Prozedur|Wird zugeordnet.|  
|CASE-Anweisung|Wird zugeordnet.|  
|FÜR die Anweisung|Wird zugeordnet.|  
|GOTO-Anweisung|Wird zugeordnet.|  
|IF-Anweisung|Wird zugeordnet.|  
|ITERATE-Anweisung|Wird zugeordnet.|  
|Lassen Sie die Anweisung|Wird zugeordnet.|  
|LOOP-Anweisung|Wird zugeordnet.|  
|Wiederholen SIE die Anweisung|Wird zugeordnet.|  
|Zeigen Sie die Anweisung|Bedingungen werden nicht unterstützt. Nachrichten können optional sein.|  
|RETURN-Anweisung|Wird zugeordnet.|  
|SIGNAL-Anweisung|Bedingungen werden nicht unterstützt. Nachrichten können optional sein.|  
|WHILE-Anweisung|Wird zugeordnet.|  
|GET-Diagnose-Anweisung|**SSMA ist abrufen Diagnose zugeordnet, mit folgenden Ausnahmen:**<br /><br />ROW_COUNT – zugeordnet ist.<br /><br />DB2_RETURN_STATUS – zugeordnet ist.<br /><br />MESSAGE_TEXT – zugeordnet ist.<br /><br />DB2_SQL_NESTING_LEVEL - entspricht keinem SQL Server-Semantik<br /><br />DB2_TOKEN_STRING - entspricht keinem SQL Server-Semantik|  
|Cursor|**SSMA ist ein Cursor zugeordnet, mit folgenden Ausnahmen:**<br /><br />ALLOCATE-CURSOR-Anweisung - entspricht keinem SQL Server-Semantik<br /><br />Ordnen Sie LOCATOR Statement - entspricht keinem SQL Server-Semantik<br /><br />DECLARE CURSOR-Anweisung - Returnability-Klausel ist nicht SQL Server-Semantik zugeordnet.<br /><br />FETCH-Anweisung – teilzuordnung. Variablen, die als Ziel werden nur unterstützt. SQLDA-Deskriptor wird SQL Server-Semantik nicht zugeordnet.|  
|Variablen|Zugeordnet sind.|  
|Ausnahmen, Handler und Bedingungen|**SSMA ist "Behandlung von Ausnahmen" zugeordnet, mit folgenden Ausnahmen:**<br /><br />Beenden Sie Handler – zugeordnet sind.<br /><br />Rückgängig machen Handler – zugeordnet sind.<br /><br />Handler – zu fortfahren, werden nicht zugeordnet.<br /><br />Bedingungen - ist es nicht auf SQL Server-Semantik zugeordnet.|  
|Dynamische SQL-Anweisungen|Nicht zugeordnet.|  
|Aliase|Zugeordnet sind.|  
|Spitznamen|Teilzuordnung. Manuelle Verarbeitung ist erforderlich für die zugrunde liegende Objekt|  
|Synonyme|Zugeordnet sind.|  
|Standard-Funktionen in DB2|SSMA ist standardmäßige DB2-Funktionen zugeordnet, wenn eine entsprechende Funktion in SQL Server verfügbar ist:|  
|Autorisierung|Nicht zugeordnet.|  
|Prädikate|Zugeordnet sind.|  
|SELECT INTO-Anweisung|Nicht zugeordnet.|  
|Werte INTO-Anweisung|Nicht zugeordnet.|  
|Steuerung von Transaktionen|Nicht zugeordnet.|  
  
## <a name="converting-db2-database-objects"></a>Konvertieren von DB2-Datenbankobjekte  
Für das Konvertieren von DB2-Datenbankobjekte, stellen Sie zunächst wählen Sie die Objekte, die Sie konvertieren möchten, und lassen dann SSMA die Konvertierung auszuführen. Anzeige von Ausgabenachrichten bei der Konvertierung auf der **Ansicht** klicken Sie im Menü **Ausgabe**.  
  
**Konvertieren von DB2-Objekten in SQL Server-syntax**  
  
1.  In DB2-Metadaten-Explorer, erweitern Sie den DB2-Server, und erweitern Sie dann **Schemas**.  
  
2.  Wählen Sie Objekte zu konvertieren:  
  
    -   Um alle Schemas konvertieren möchten, aktivieren Sie das Kontrollkästchen neben **Schemas**.  
  
    -   Zum konvertieren, oder lassen Sie eine Datenbank, wählen Sie das Kontrollkästchen neben den Schemanamen an.  
  
    -   Zum konvertieren, oder lassen Sie eine Kategorie von Objekten, erweitern Sie ein Schema wählen Sie aus, oder deaktivieren Sie das Kontrollkästchen neben der Kategorie.  
  
    -   Zum konvertieren, oder lassen Sie einzelne Objekte, erweitern Sie den Kategorieordner wählen Sie aus, oder deaktivieren Sie das Kontrollkästchen neben dem Objekt.  
  
3.  Um alle ausgewählten Objekte zu konvertieren, Maustaste **Schemas** , und wählen Sie **Schema konvertieren**.  
  
    Sie können auch einzelne Objekte oder Kategorien von Objekten durch das Objekt oder der übergeordnete Ordner mit der rechten Maustaste, und wählen Sie dann konvertieren **Schema konvertieren**.  
  
## <a name="viewing-conversion-problems"></a>Probleme bei der Konvertierung anzeigen  
Einige Objekte DB2 können nicht konvertiert werden. Sie können die Erfolgsquoten Konvertierung durch Anzeigen der Zusammenfassung Konvertierungsbericht bestimmen.  
  
**So zeigen Sie einen Zusammenfassungsbericht an**  
  
1.  Wählen Sie in der DB2-Metadaten-Explorer **Schemas**.  
  
2.  Wählen Sie im rechten Bereich die **Bericht** Registerkarte.  
  
    Dieser Bericht zeigt die Zusammenfassung Bewertungsbericht für alle Datenbankobjekte, die bewertet oder konvertiert wurden. Sie können auch einen Zusammenfassungsbericht für einzelne Objekte anzeigen:  
  
    -   Um den Bericht für ein einzelnes Schema anzuzeigen, wählen Sie das Schema in DB2-Metadaten-Explorer aus.  
  
    -   Um den Bericht für ein einzelnes Objekt anzuzeigen, wählen Sie das Objekt in DB2-Metadaten-Explorer aus. Objekte sind, die haben Probleme bei der Konvertierung, ein rotes Fehlersymbol.  
  
Für Objekte, die Fehler bei der Konvertierung, können Sie die Syntax anzeigen, die in der Konvertierungsfehler bewirkt, dass geführt haben.  
  
**Einzelne Konvertierungsprobleme anzeigen**  
  
1.  Erweitern Sie im DB2-Metadaten-Explorer **Schemas**.  
  
2.  Erweitern Sie das Schema, das ein rotes Fehlersymbol zeigt.  
  
3.  Erweitern Sie einen Ordner mit einem roten Fehlersymbol, unter dem Schema.  
  
4.  Wählen Sie das Objekt, das ein rotes Fehlersymbol verfügt.  
  
5.  Klicken Sie im rechten Bereich auf die **Bericht** Registerkarte.  
  
6.  Am oberen Rand der **Bericht** Registerkarte ist eine Dropdown-Liste. Wenn die Liste zeigt **Statistiken**, ändern Sie die Auswahl auf **Quelle**.  
  
    SSMA wird der Quellcode und mehrere Schaltflächen direkt über dem Code angezeigt.  
  
7.  Klicken Sie auf die **weiter Problem** Schaltfläche. Dies ist ein rotes Fehlersymbol mit einem Pfeil nach rechts.  
  
    SSMA wird die erste problematisch Quellcode zu markieren, die in das aktuelle Objekt gefunden.  
  
Für jedes Element, das nicht konvertiert werden konnte, müssen Sie ermitteln, was Sie mit diesem Objekt ausführen möchten:  
  
-   Sie können den Quellcode für Prozeduren ändern, auf die **SQL** Registerkarte.  
  
-   Sie können das Objekt in der DB2-Datenbank zu entfernen oder zu überarbeiten problematischen Code ändern. Um den aktualisierten Code in SSMA zu laden, müssen Sie die Metadaten zu aktualisieren. Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit DB2-Datenbank &#40; DB2ToSQL &#41;](../../ssma/db2/connecting-to-db2-database-db2tosql.md).  
  
-   Sie können das Objekt von der Migration ausschließen. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Metadaten-Explorer und DB2-Metadaten-Explorer, deaktivieren Sie das Kontrollkästchen neben dem Element vor dem Laden der Objekte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] und Migrieren von Daten von DB2.  
  
## <a name="next-step"></a>Nächster Schritt  
Der nächste Schritt des Migrationsvorgangs besteht darin [Laden Sie konvertierte Objekte in SQL Server](http://msdn.microsoft.com/en-us/f4ea1ced-9f9f-4a9d-88ab-81dbab64adc3).  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von DB2-Daten in SQLServer &#40; DB2ToSQL &#41;](../../ssma/db2/migrating-db2-data-into-sql-server-db2tosql.md)  
  


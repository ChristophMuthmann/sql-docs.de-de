---
title: Projekteinstellungen (Konvertierung) (DB2ToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-db2
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 538c93cf-c5bb-43d5-b758-186d9fb00c19
caps.latest.revision: "8"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e40e6f4d56f3c246516de617dbdc4a7c9516db9c
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="project-settings-conversion-db2tosql"></a>Projekteinstellungen (Konvertierung) (DB2ToSQL)
Die Seite "Konvertierung", der die **Projekteinstellungen** Dialogfeld enthält Einstellungen, anpassen, wie SSMA zu DB2-Syntax konvertiert [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Syntax.  
  
Bereich Konvertierung finden Sie in der **Projekteinstellungen** und **Projekt Standardeinstellungen** Dialogfelder:  
  
-   Zum Angeben von Einstellungen für alle SSMA-Projekte, auf die **Tools** klicken Sie im Menü **Projekt Standardeinstellungen**, wählen Sie die Migration-Projekttyp, die für die Einstellungen sind erforderlich, angezeigt oder geändert werden **Migration Zielversion** Dropdown-Liste, und klicken Sie auf **allgemeine** am unteren Rand der linken Bereich, und klicken Sie dann auf **Konvertierung**.  
  
-   Zum Angeben von Einstellungen für das aktuelle Projekt auf die **Tools** klicken Sie im Menü **Projekteinstellungen**, klicken Sie dann auf **allgemeine** am unteren Rand der linken Bereich, und klicken Sie dann auf **Konvertierung**.  
  
## <a name="conversion-messages"></a>Konvertierung von Nachrichten  
  
### <a name="generate-messages-about-issues-applied"></a>Generieren von Meldungen zu Problemen, die angewendet  
Gibt an, ob SSMA informationsmeldungen während der Konvertierung generiert, sie in den Ausgabebereich zeigt und konvertierten Code hinzugefügt.  
  
Bei Auswahl einer Konvertierungsmodus in der **Modus** Feld SSMA gilt die folgende Einstellung:  
  
**Standard/Optimistic-Modus:** Nein  
  
**Vollmodus:** Nein  
  
## <a name="miscellaneous-options"></a>Sonstige Optionen  
  
### <a name="cast-rownum-expressions-as-integers"></a>ROWNUM Umwandlungsausdrücke als ganze Zahlen  
SSMA ROWNUM Ausdrücke konvertiert, konvertiert sie den Ausdruck in eine TOP-Klausel, gefolgt von dem Ausdruck. Das folgende Beispiel zeigt ROWNUM in eine DB2-DELETE-Anweisung:  
  
`DELETE FROM Table1`  
  
`WHERE ROWNUM < expression and Field1 >= 2`  
  
Das folgende Beispiel zeigt das resultierende [!INCLUDE[tsql](../../includes/tsql_md.md)]:  
  
`DELETE TOP (expression-1)`  
  
`FROM Table1`  
  
`WHERE Field1>=2`  
  
Im oberen Bereich erfordert, dass der TOP-Klauseln-Ausdruck in eine ganze Zahl ausgewertet wird. Wenn die ganze Zahl negativ ist, wird die Anweisung einen Fehler erzeugen.  
  
-   Bei Auswahl des **Ja**, SSMA wird den Ausdruck als ganze Zahl umgewandelt.  
  
-   Bei Auswahl des **keine**, SSMA kennzeichnet alle noninteger-Ausdrücke als Fehler im Code konvertiert.  
  
Bei Auswahl einer Konvertierungsmodus in der **Modus** Feld SSMA gilt die folgende Einstellung:  
  
**Standard/Full-Modus:** Nein  
  
**Optimistische Modus:** Ja  
  
### <a name="default-schema-mapping"></a>Standardmäßige Schemazuordnung  
Diese Einstellung gibt an, wie DB2-Schemas in SQL Server-Schemas zugeordnet werden. In dieser Einstellung stehen zwei Optionen zur Auswahl:  
  
1.  **Schema für Datenbank:** In diesem Modus DB2-Schema "sch1" wird standardmäßig auf 'Dbo' SQL Server-Datenbankschemas in SQL Server-Datenbank "sch1" zugeordnet werden.  
  
2.  **Schema zum Schema:**In diesem Modus DB2 wird standardmäßig auf "sch1" SQL Server-Datenbankschemas in SQL Server-Standarddatenbank angegeben wird, klicken Sie im Dialogfeld "Verbindung" Schema "sch1" zugeordnet werden.  
  
Bei Auswahl einer Konvertierungsmodus in der **Modus** Feld SSMA gilt die folgende Einstellung:  
  
**Standard/Optimistic/Full-Modus:** Schema, um die Datenbank  
  
### <a name="conversion-ways-of-merge-statement"></a>Konvertierung Möglichkeiten der MERGE-Anweisung  
  
-   Bei Auswahl des **Verwenden von INSERT, UPDATE, DELETE-Anweisung**, SSMA konvertiert Fusion-Anweisung in INSERT-, Update- und Löschen von Anweisungen.  
  
-   Bei Auswahl des **Verwenden von MERGE-Anweisung**, SSMA konvertiert Fusion-Anweisung in der MERGE-Anweisung in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
> [!WARNING]  
> Diese Einstellung Projektoption steht nur in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014.  
  
Bei Auswahl einer Konvertierungsmodus in der **Modus** Feld SSMA gilt die folgende Einstellung:  
  
**Standard/Optimistic/Full-Modus:** mit MERGE Anweisung  
  
### <a name="convert-calls-to-subprograms-that-use-default-arguments"></a>Konvertieren Sie Aufrufe an, mit denen Standardargumente Unterprogramme  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Funktionen unterstützen nicht die Auslassung der Parameter im Funktionsaufruf. Darüber hinaus [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Funktionen und Prozeduren unterstützen keine Ausdrücke als Parameter Standardwerte.  
  
-   Bei Auswahl des **Ja** und ein Funktionsaufruf wird ausgelassen, Parameter, SSMA fügt das Schlüsselwort **Standard** in der Funktion und den Aufruf in der richtigen Position. Es werden dann in den Aufruf mit einer Warnung gekennzeichnet.  
  
-   Bei Auswahl des **keine**, SSMA werden in die Funktionsaufrufe als Fehler gekennzeichnet.  
  
Bei Auswahl einer Konvertierungsmodus in der **Modus** Feld SSMA gilt die folgende Einstellung:  
  
**Standard/optimistische/Full-Modus:** Ja  
  
### <a name="convert-count-function-to-countbig"></a>COUNT-Funktion in COUNT_BIG konvertieren  
Wenn die COUNT-Funktion zum Zurückgeben von Werten größer als 2.147.483.647 wahrscheinlich sind also 2<sup>31</sup>-1 ist, sollten Sie die Funktionen in COUNT_BIG konvertieren.  
  
-   Bei Auswahl des **Ja**, SSMA konvertiert alle Vorkommen von COUNT, COUNT_BIG.  
  
-   Bei Auswahl des **keine**, die Funktionen als Anzahl bleiben. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Gibt einen Fehler zurück, wenn die Funktion einen Wert größer als 2 zurückgibt<sup>31</sup>-1 zurück.  
  
Bei Auswahl einer Konvertierungsmodus in der **Modus** Feld SSMA gilt die folgende Einstellung:  
  
**Standard/Full-Modus:** Ja  
  
**Optimistische Modus:** Nein  
  
### <a name="convert-forall-statement-to-while-statement"></a>FORALL-Anweisung in WHILE konvertieren Anweisung  
Definiert, wie SSMA FORALL-Schleifen auf PL/SQL-Auflistungselemente behandeln.  
  
-   Bei Auswahl des **Ja**, SSMA erstellt eine WHILE-Schleife, in denen Elemente der Auflistung abgerufenen nacheinander werden.  
  
-   Bei Auswahl des **keine**, SSMA ein Rowset mithilfe von Knoten ()-Methode aus der Auflistung generiert und als eine einzelne Tabelle verwendet. Dies ist effizienter, jedoch wird die Ausgabecode weniger lesbar.  
  
Bei Auswahl einer Konvertierungsmodus in der **Modus** Feld SSMA gilt die folgende Einstellung:  
  
**Standard/Optimistic-Modus:** Nein  
  
**Vollmodus:** Ja  
  
### <a name="convert-foreign-keys-with-set-null-referential-action-on-column-that-is-not-null"></a>Konvertieren von Fremdschlüsseln mit referenziellen SET NULL-Aktion auf die Spalte, die NULL nicht  
DB2 ermöglicht foreign Key-Einschränkungen erstellen, in denen konnte eine SET NULL-Aktion nicht möglicherweise ausgeführt werden, da NULL-Werte nicht in der referenzierten Spalte zulässig sind. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]die Konfiguration dieser Art foreign Key ist nicht zulässig.  
  
-   Bei Auswahl des **Ja**, SSMA referenzielle Aktionen wie DB2 generiert, aber Sie müssen manuelle Änderungen vor dem Laden der Einschränkung [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Sie können z. B. NO ACTION anstelle von NULL festgelegt.  
  
-   Bei Auswahl des **keine**, die Einschränkung wird als Fehler markiert sein.  
  
Bei Auswahl einer Konvertierungsmodus in der **Modus** Feld SSMA gilt die folgende Einstellung:  
  
**Standard/optimistische/Full-Modus:** Nein  
  
### <a name="convert-function-calls-to-procedure-calls"></a>Konvertieren von Funktionsaufrufen Prozeduraufrufe  
Einige Funktionen DB2 als autonome Transaktionen definiert sind oder enthalten Anweisungen, die nicht in gültig wäre [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. In diesen Fällen erstellt SSMA an eine Prozedur und eine Funktion, die als Wrapper für die Prozedur verwendet wird. Die konvertierte Funktion ruft die implementierende Prozedur.  
  
SSMA kann Aufrufe an die Wrapperfunktion in Aufrufe an die Prozedur konvertieren. Dies erstellt der Code besser lesbar und kann die Leistung verbessern. Allerdings lässt Kontext nicht immer; Sie können keine z. B. einen Funktionsaufruf in SELECT-Liste mit einem Prozeduraufruf ersetzen. SSMA verfügt über einige Optionen für die gängigen Fälle abdecken:  
  
-   Bei Auswahl des **immer**, SSMA versucht, Wrapper Funktionsaufrufe in Prozeduraufrufen zu konvertieren. Wenn diese Konvertierung durch der aktuelle Kontext nicht möglich ist, wird eine Fehlermeldung erstellt. Auf diese Weise bleiben keine Funktionsaufrufe in den generierten Code.  
  
-   Bei Auswahl des **möglichst**, SSMA stellt einen Verschiebevorgang Prozeduraufrufe nur, wenn die Funktion Ausgabeparameter besitzt. Wenn das Verschieben nicht möglich ist, wird des Parameters Ausgabeattribut entfernt. In allen anderen Fällen bleibt SSMA Funktionsaufrufe.  
  
-   Bei Auswahl des **nie**, SSMA verlassen alle Funktionsaufrufe als Funktionsaufrufe. Diese Option kann in einigen Fällen aus Gründen der Leistung nicht akzeptabel sein.  
  
Bei Auswahl einer Konvertierungsmodus in der **Modus** Feld SSMA gilt die folgende Einstellung:  
  
**Standard/Optimistic/Full-Modus:** möglichst  
  
### <a name="convert-lock-table-statements"></a>LOCK-TABLE-Anweisungen konvertieren  
SSMA kann viele SPERREN TABLE-Anweisungen in Tabellenhinweise konvertieren. SSMA kann nicht konvertiert werden alle SPERREN TABLE-Anweisungen, die PARTITION, SUBPARTITION, enthalten @dblink, und NOWAIT-Klauseln und kennzeichnet diese Anweisungen mit Fehlermeldungen für die Konvertierung.  
  
-   Bei Auswahl des **Ja**, SSMA konvertiert unterstützten SPERRE TABLE-Anweisungen in Tabellenhinweise.  
  
-   Bei Auswahl des **keine**, SSMA werden alle SPERREN TABLE-Anweisungen mit Fehlermeldungen für die Konvertierung zu markieren.  
  
Die folgende Tabelle zeigt, wie SSMA DB2 Sperrmodi konvertiert:  
  
|||  
|-|-|  
|DB2-Sperrmodus|SQL Server-Tabellenhinweis|  
|FREIGABE DER ZEILE|ROWLOCK, HOLDLOCK|  
|EXKLUSIVE ZEILE|ROWLOCK, XLOCK, HOLDLOCK|  
|FREIGABE UPDATE = ZEILE FREIGABE|ROWLOCK, HOLDLOCK|  
|FREIGEBEN|TABLOCK HOLDLOCK|  
|FREIGABE ZEILE EXKLUSIVE|TABLOCK, XLOCK, HOLDLOCK|  
|EXKLUSIVE|TABLOCKX HOLDLOCK|  
  
Bei Auswahl einer Konvertierungsmodus in der **Modus** Feld SSMA gilt die folgende Einstellung:  
  
**Standard/optimistische/Full-Modus:** Ja  
  
### <a name="convert-open-for-statements-for-ref-cursor-out-parameters"></a>Konvertieren von OPEN-FOR-Anweisungen für den REF CURSOR-OUT-Parameter  
In DB2 kann die OPEN-FOR-Anweisung verwendet werden, um ein Resultset an den OUT-Parameter vom Typ REF CURSOR einen Unterprogramm zurückzugeben. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], gespeicherten Prozeduren geben die Ergebnisse der SELECT-Anweisungen direkt zurück.  
  
SSMA kann viele OPEN-FOR-Anweisungen in SELECT-Anweisungen konvertieren.  
  
-   Bei Auswahl des **Ja**, SSMA konvertiert die OPEN-FOR-Anweisung in einer SELECT-Anweisung, die das Resultset an den Client zurückgibt.  
  
-   Bei Auswahl des **keine**, SSMA wird eine Fehlermeldung generiert, in der konvertierten Code und dem Ausgabebereich angezeigt.  
  
Bei Auswahl einer Konvertierungsmodus in der **Modus** Feld SSMA gilt die folgende Einstellung:  
  
**Standard/optimistische/Full-Modus:** Ja  
  
### <a name="convert-record-as-a-list-of-separates-variables"></a>Konvertieren von Datensatz als eine Liste mit Variablen trennt  
SSMA kann DB2-Datensätze in trennt Variablen und XML-Variablen mit speziellen Struktur konvertiert werden.  
  
-   Bei Auswahl des **Ja**, SSMA konvertiert den Datensatz in eine Liste von Variablen trennt, wenn möglich.  
  
-   Bei Auswahl des **keine**, SSMA konvertiert den Datensatz in XML-Variablen mit speziellen Struktur.  
  
Bei Auswahl einer Konvertierungsmodus in der **Modus** Feld SSMA gilt die folgende Einstellung:  
  
**Standard/optimistische/Full-Modus:** Ja  
  
### <a name="convert-substr-function-calls-to-substring-function-calls"></a>SUBSTR-Funktionsaufrufe zur TEILZEICHENFOLGE Funktionsaufrufe konvertieren  
SSMA kann Funktionsaufrufe in DB2 SUBSTR konvertieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **Teilzeichenfolge** Funktionsaufrufe, abhängig von der Anzahl von Parametern. Wenn SSMA einen SUBSTR-Funktionsaufruf kann nicht konvertiert werden, oder die Anzahl der Parameter wird nicht unterstützt, werden SSMA SUBSTR-Funktionsaufruf in einem benutzerdefinierten SSMA-Funktionsaufruf konvertiert.  
  
-   Bei Auswahl des **Ja**, SSMA wandelt SUBSTR-Funktionsaufrufe, die in drei Parameter verwenden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **Teilzeichenfolge**. Andere Funktionen SUBSTR werden zum Aufrufen der benutzerdefinierten SSMA-Funktion konvertiert werden.  
  
-   Bei Auswahl des **keine**, SSMA konvertiert SUBSTR-Funktionsaufruf in einem benutzerdefinierten SSMA-Funktionsaufruf.  
  
Bei Auswahl einer Konvertierungsmodus in der **Modus** Feld SSMA gilt die folgende Einstellung:  
  
**Standard/Optimistic-Modus:** Ja  
  
**Vollmodus:** Nein  
  
### <a name="convert-subtypes"></a>Konvertieren von Untertypen  
SSMA kann PL/SQL-Untertypen auf zwei Arten konvertieren:  
  
-   Bei Auswahl des **Ja**, SSMA erstellt [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] benutzerdefinierte Geben Sie einen Untertyp und verwenden sie für jede Variable dieses Untertyps.  
  
-   Bei Auswahl des **keine**, SSMA wird allen Deklarationen in der Quelle des Untertyps mit dem zugrunde liegenden Typ ersetzen und das Ergebnis wie gewohnt konvertieren. In diesem Fall keine zusätzlichen Typen in erstellt werden.[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]  
  
Bei Auswahl einer Konvertierungsmodus in der **Modus** Feld SSMA gilt die folgende Einstellung:  
  
**Standard/optimistische/Full-Modus:** Nein  
  
### <a name="convert-synonyms"></a>Konvertieren von Synonymen  
Synonyme für die folgenden DB2-Objekte können migriert werden, um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]:  
  
-   Tabellen und Objekttabellen  
  
-   Ansichten und Objekt  
  
-   Gespeicherte Prozeduren und Funktionen  
  
-   Materialisierte Sichten  
  
Synonyme für die folgenden DB2-Objekte können durch direkte Verweise auf die Objekte ersetzt werden:  
  
-   Sequenzen  
  
-   Pakete  
  
-   Schemaobjekte für Java-Klasse  
  
-   Benutzerdefinierte Objekttypen  
  
Synonyme können nicht migriert werden. SSMA generiert Fehlermeldungen für das Synonym, alle Verweise, die das Synonym.  
  
-   Bei Auswahl des **Ja**, SSMA erstellt [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Synonyme und Direct Objektverweise entsprechend die vorherige Liste.  
  
-   Bei Auswahl des **keine**, SSMA wird Direct Objektverweise für alle hier aufgeführten Synonyme erstellt.  
  
Bei Auswahl einer Konvertierungsmodus in der **Modus** Feld SSMA gilt die folgende Einstellung:  
  
**Standard/optimistische/Full-Modus:** Ja  
  
### <a name="convert-tochardate-format"></a>TO_CHAR (Date, Format) konvertieren  
SSMA kann DB2 TO_CHAR(date, format) in Prozeduren aus der Datenbank Sysdb konvertieren.  
  
-   Bei Auswahl des **TO_CHAR_DATE mithilfe Funktion**, SSMA konvertiert die TO_CHAR (Date, Format) in TO_CHAR_DATE-Funktion der englischen Sprache verwendet, für die Konvertierung.  
  
-   Bei Auswahl des **mithilfe TO_CHAR_DATE_LS-Funktion (NLS Care)**, SSMA konvertiert die TO_CHAR (Date, Format) in TO_CHAR_DATE_LS-Funktion der sitzungssprache verwendet, für die Konvertierung  
  
Bei Auswahl einer Konvertierungsmodus in der **Modus** Feld SSMA gilt die folgende Einstellung:  
  
**Standard/Optimistic-Modus:** Using TO_CHAR_DATE Funktion  
  
**Vollmodus:** Using TO_CHAR_DATE_LS Funktion (NLS Care)  
  
### <a name="convert-transaction-processing-statements"></a>Verarbeitung transaktionsanweisungen konvertieren  
SSMA kann DB2-transaktionsanweisungen Verarbeitung konvertiert werden:  
  
-   Bei Auswahl des **Ja**, SSMA konvertiert DB2 Transaction-Anweisungen auf, die sich in Verarbeitung [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Anweisungen.  
  
-   Bei Auswahl des **keine**, SSMA kennzeichnet die Transaktion, die Verarbeitung von Anweisungen, die als Fehler bei der Konvertierung.  
  
> [!NOTE]  
> DB2 wird implizit Transaktionen geöffnet. Um dieses Verhalten zu emulieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], müssen Sie BEGIN TRANSACTION-Anweisungen manuell hinzufügen, in denen Ihre Transaktionen gestartet werden soll. Alternativ können Sie den Befehl SET IMPLICIT_TRANSACTIONS ON am Anfang der Sitzungs ausführen. SSMA fügt SET IMPLICIT_TRANSACTIONS ON beim Konvertieren von Unterroutinen mit autonomen Transaktionen automatisch hinzu.  
  
Bei Auswahl einer Konvertierungsmodus in der **Modus** Feld SSMA gilt die folgende Einstellung:  
  
**Standard/optimistische/Full-Modus:** Ja  
  
### <a name="emulate-db2-null-behavior-in-order-by-clauses"></a>Emulieren von DB2 null Verhalten in ORDER BY-Klauseln  
NULL-Werte werden anders als in sortiert [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] und DB2:  
  
-   In [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]NULL Werte sind die niedrigsten Werte in einer geordneten Liste. In einer aufsteigenden Liste werden NULL-Werte als erstes angezeigt.  
  
-   In DB2 sind NULL-Werte den höchsten Werten in einer geordneten Liste. Standardmäßig werden NULL-Werte in einer Liste mit aufsteigender Reihenfolge zuletzt angezeigt.  
  
-   DB2 wurde zum ersten NULL-Werte und NULL-Werte letzten-Klauseln können Sie ändern, wie DB2 NULL-Werten sortiert.  
  
SSMA kann DB2 ORDER BY-Verhalten emulieren, indem Sie für NULL-Werte überprüfen. Sie ordnet dann zuerst nach NULL-Werte in der angegebenen Reihenfolge und Orders durch andere Werte.  
  
-   Bei Auswahl des **Ja**, SSMA wandelt die DB2-Anweisung, mit denen DB2 ORDER BY Verhalten emuliert.  
  
-   Bei Auswahl des **keine**, SSMA DB2 Regeln ignoriert und beim Erreichen der ersten NULL-Werte und Nullen letzten Klauseln wird eine Fehlermeldung generiert.  
  
Bei Auswahl einer Konvertierungsmodus in der **Modus** Feld SSMA gilt die folgende Einstellung:  
  
**Standard/Optimistic-Modus:** Nein  
  
**Vollmodus:** Ja  
  
### <a name="emulate-row-count-exceptions-in-select"></a>Emulieren Sie Zeile Anzahl Ausnahmen in SELECT  
Wenn die SELECT-Anweisung eine INTO-Klausel keine Zeilen zurückgibt, löst DB2 eine NO_DATA_FOUND-Ausnahme aus. Wenn die Anweisung zwei oder mehr Zeilen zurückgibt, wird die TOO_MANY_ROWS-Ausnahme ausgelöst. Die konvertierte Anweisung im [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] löst keine Ausnahmen aus, wenn sich die Anzahl der Zeilen aus einer unterscheidet.  
  
-   Bei Auswahl des **Ja**, SSMA Aufruf Sysdb Prozedur Db_error_exact_one_row_check nach jeder SELECT-Anweisung hinzugefügt. Diese Prozedur emuliert die NO_DATA_FOUND und TOO_MANY_ROWS Ausnahmen. Dies ist die Standardeinstellung, und ermöglicht DB2 Verhalten so nah wie möglich zu reproduzieren. Sie sollten immer auswählen **Ja** Wenn Quellcode Ausnahmehandler verfügt, die diese Fehler zu verarbeiten. Beachten Sie, dass die SELECT-Anweisung innerhalb einer benutzerdefinierten Funktion tritt auf, dieses Modul an eine gespeicherte Prozedur konvertiert werden, wird da das Ausführen von gespeicherter Prozeduren und Auslösen von Ausnahmen ist nicht kompatibel mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Funktionskontext.  
  
-   Bei Auswahl des **keine**, keine Ausnahmen generiert werden. Der nützlich sein, wenn SSMA eine User-defined Function konvertiert, und Sie eine Funktion in bleiben möchten[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]  
  
Bei Auswahl einer Konvertierungsmodus in der **Modus** Feld SSMA gilt die folgende Einstellung:  
  
**Standard/optimistische/Full-Modus:** Ja  
  
### <a name="generate-error-for-dbmssqlparse"></a>Fehler für DBMS_SQL generiert. ANALYSIEREN  
  
-   Bei Auswahl des **Fehler**, Fehler bei der Konvertierung DBMS_SQL SSMA zu generieren. ANALYSIERT WERDEN.  
  
-   Bei Auswahl des **Warnung**, SSMA Warnung bei der Konvertierung DBMS_SQL generieren. ANALYSIERT WERDEN.  
  
Bei Auswahl einer Konvertierungsmodus in der **Modus** Feld SSMA gilt die folgende Einstellung:  
  
**Standard/optimistische/Full-Modus:** Fehler  
  
### <a name="generate-rowid-column"></a>ROWID Spalte generieren  
Wenn SSMA erstellt Tabellen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], können sie eine ROWID-Spalte erstellen. Wenn Daten migriert werden, erhält jede Zeile von der NEWID()-Funktion generierten einen neuen UNIQUEIDENTIFIER-Wert.  
  
-   Bei Auswahl des **Ja**, die ROWID-Spalte wird für alle Tabellen erstellt und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] GUIDs generiert, wie Sie Werte einfügen. Wählen Sie stets **Ja** , wenn Sie beabsichtigen, die der Tester SSMA verwenden.  
  
-   Bei Auswahl des **keine**, ROWID-Spalten werden nicht in Tabellen eingefügt.  
  
-   **Fügen Sie die ROWID für Tabellen mit Triggern** ROWID für die Tabellen mit Triggern hinzufügen.  
  
> [!WARNING]  
> Die Standardeinstellung bei SQL Server 2005, SQL Server 2008 und SQL Server 2012 und 2014 ist **hinzufügen ROWID für Tabellen mit Triggern**.  
  
Bei Auswahl einer Konvertierungsmodus in der **Modus** Feld SSMA gilt die folgende Einstellung:  
  
**Standard/Optimistic-Modus:** ROWID für Tabellen mit Triggern hinzufügen  
  
**Vollmodus:** Ja  
  
### <a name="generate-unique-index-on-rowid-column"></a>Eindeutigen Index für Spalte ROWID generieren  
Gibt an, ob es sich bei SSMA unique Indexspalte für die Spalte generiert ROWID oder nicht generiert. Eindeutiger Index wird generiert, wenn die Option auf "Ja" festgelegt ist, und wenn sie auf "Nein" festgelegt ist, ist eindeutiger Index nicht für die Spalte ROWID generiert.  
  
Bei Auswahl einer Konvertierungsmodus in der **Modus** Feld SSMA gilt die folgende Einstellung:  
  
**Standard/optimistische/Full-Modus:** Ja  
  
### <a name="local-modules-conversion"></a>Lokale Module-Konvertierung  
Definiert den Typ der Konvertierung von DB2 geschachtelt Unterprogramm (deklariert in eigenständige gespeicherte Prozedur oder Funktion).  
  
-   Bei Auswahl des **Inline**, ruft die geschachtelten Unterprogramm durch Text ersetzt werden.  
  
-   Bei Auswahl des **gespeicherten Prozeduren**, geschachtelte Unterprogramm wird an eine gespeicherte SQL Server-Prozedur konvertiert werden, und seine Aufrufe auf diesen Aufruf einer Prozedur ersetzt werden.  
  
Bei Auswahl einer Konvertierungsmodus in der **Modus** Feld SSMA gilt die folgende Einstellung:  
  
**Standard/optimistische/Full-Modus:** Inline  
  
### <a name="use-isnull-in-string-concatenation"></a>Verwenden von ISNULL in Verketten von Zeichenfolgen  
DB2 und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] unterschiedliche Ergebnisse zurückgeben, wenn die Zeichenfolge Verkettungen NULL-Werte enthalten. DB2 wird der NULL-Wert, wie ein leerer Zeichensatz behandelt. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Gibt NULL zurück.  
  
-   Bei Auswahl des **Ja**, SSMA ersetzt den DB2 Verkettung Strich (|) mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Verkettung Zeichen (+). SSMA überprüft auch die Ausdrücke auf beiden Seiten der Verkettung für NULL-Werte.  
  
-   Bei Auswahl des **keine**, SSMA ersetzt die Verkettung Zeichen, aber nicht für NULL-Werte.  
  
Bei Auswahl einer Konvertierungsmodus in der **Modus** Feld SSMA gilt die folgende Einstellung:  
  
### <a name="use-isnull-in-replace-function-calls"></a>Verwenden von ISNULL in Funktionsaufrufen ersetzen  
ISNULL-Anweisung wird im ersetzen-Funktionsaufrufe zur Emulierung des DB2-Verhaltens verwendet. Die folgenden Optionen sind für diese Einstellung vorhanden:  
  
-   YES  
  
-   Nein  
  
Bei Auswahl einer Konvertierungsmodus in der **Modus** Feld SSMA gilt die folgende Einstellung:  
  
**Standard/Optimistic-Modus:** Nein  
  
**Vollmodus:** Ja  
  
### <a name="use-isnull-in-concat-function-calls"></a>Verwenden von ISNULL in CONCAT-Funktionsaufrufen  
ISNULL-Anweisung wird in CONCAT-Funktionsaufrufe verwendet, um DB2-Verhalten zu emulieren. Die folgenden Optionen sind für diese Einstellung vorhanden:  
  
-   YES  
  
-   Nein  
  
Bei Auswahl einer Konvertierungsmodus in der **Modus** Feld SSMA gilt die folgende Einstellung:  
  
**Standard/Optimistic-Modus:** Nein  
  
**Vollmodus:** Ja  
  
### <a name="use-native-convert-function-when-possible"></a>Verwenden von systemeigenen Convert-Funktion nach Möglichkeit  
  
-   Bei Auswahl des **Ja**, SSMA konvertiert die TO_CHAR (Date, Format) in systemeigenen Convert-Funktion, wenn möglich.  
  
-   Bei Auswahl des **keine**, SSMA konvertiert die TO_CHAR (Date, Format) in TO_CHAR_DATE oder TO_CHAR_DATE_LS (es ist von Optionen für "TO_CHAR(date, format) konvertieren" definiert).  
  
Bei Auswahl einer Konvertierungsmodus in der **Modus** Feld SSMA gilt die folgende Einstellung:  
  
**Standard/Optimistic-Modus:** Ja  
  
**Vollmodus:** Nein  
  
### <a name="use-selectfor-xml-when-converting-selectinto-for-record-variable"></a>Verwenden Sie SELECT... Wählen Sie für XML beim Konvertieren... INTO für Datensatz-variable  
Gibt an, ob ein XML-Resultset bei der Auswahl in eine Datensatzvariable generiert.  
  
-   Bei Auswahl des **Ja**, die SELECT-Anweisung wird die XML-Code.  
  
-   Bei Auswahl des **keine**, die SELECT-Anweisung gibt ein Resultset zurück.  
  
Bei Auswahl einer Konvertierungsmodus in der **Modus** Feld SSMA gilt die folgende Einstellung:  
  
**Standard/optimistische/Full-Modus:** Nein  
  
## <a name="returning-clause-conversion"></a>Zurückgeben der Klausel-Konvertierung  
  
### <a name="convert-returning-clause-in-delete-statement-to-output"></a>RETURNING-Klausel in der DELETE-Anweisung in die Ausgabe zu konvertieren.  
DB2 bietet eine RETURNING-Klausel als eine Möglichkeit, sofort gelöschten Werte zu erhalten. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]stellt diese Funktionalität bereit, mit der OUTPUT-Klausel.  
  
-   Bei Auswahl des **Ja**, SSMA RETURNING-Klauseln in DELETE-Anweisungen in der OUTPUT-Klauseln konvertiert. Da Trigger für eine Tabelle mit Werten ändern können, der zurückgegebene Wert möglicherweise in anderen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] als DB2 vorlag.  
  
-   Bei Auswahl des **keine**, SSMA generiert eine SELECT-Anweisung vor der DELETE-Anweisungen, um zurückgegebene Werte abzurufen.  
  
Bei Auswahl einer Konvertierungsmodus in der **Modus** Feld SSMA gilt die folgende Einstellung:  
  
**Standard/optimistische/Full-Modus:** Ja  
  
### <a name="convert-returning-clause-in-insert-statement-to-output"></a>RETURNING-Klausel in der INSERT-Anweisung in die Ausgabe zu konvertieren.  
DB2 bietet eine RETURNING-Klausel als eine Möglichkeit, sofort eingefügten Werte zu erhalten. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]stellt diese Funktionalität bereit, mit der OUTPUT-Klausel.  
  
-   Bei Auswahl des **Ja**, SSMA Wandelt eine RETURNING-Klausel in einer INSERT-Anweisung in die Ausgabe. Da Trigger für eine Tabelle mit Werten ändern können, der zurückgegebene Wert möglicherweise in anderen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] als DB2 vorlag.  
  
-   Bei Auswahl des **keine**, SSMA emuliert DB2-Funktionen durch Einfügen, und wählen Sie dann Werte aus einer Verweistabelle.  
  
Bei Auswahl einer Konvertierungsmodus in der **Modus** Feld SSMA gilt die folgende Einstellung:  
  
**Standard/optimistische/Full-Modus:** Ja  
  
### <a name="convert-returning-clause-in-update-statement-to-output"></a>RETURNING-Klausel in der UPDATE-Anweisung in die Ausgabe zu konvertieren.  
DB2 bietet eine RETURNING-Klausel als eine Möglichkeit, sofort aktualisierte Werte zu erhalten. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]stellt diese Funktionalität bereit, mit der OUTPUT-Klausel.  
  
-   Bei Auswahl des **Ja**, SSMA RETURNING-Klauseln in der UPDATE-Anweisungen in der OUTPUT-Klauseln konvertiert. Da Trigger für eine Tabelle mit Werten ändern können, der zurückgegebene Wert möglicherweise in anderen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] als DB2 vorlag.  
  
-   Bei Auswahl des **keine**, SSMA wird SELECT-Anweisungen generieren, nach dem UPDATE-Anweisungen zum Abrufen von Werten zurückgeben.  
  
Bei Auswahl einer Konvertierungsmodus in der **Modus** Feld SSMA gilt die folgende Einstellung:  
  
**Standard/optimistische/Full-Modus:** Ja  
  
## <a name="sequence-conversion"></a>Sequenz-Konvertierung  
  
### <a name="convert-sequence-generator"></a>Konvertieren Sie die Sequenz-Generator  
In DB2 können Sie eine Sequenz verwenden, um eindeutige Bezeichner zu generieren.  
  
SSMA kann Sequenzen wie folgt konvertiert werden.  
  
-   Verwenden SQL Server-Sequenz-Generator (diese Option ist nur verfügbar, wenn in SQL Server 2012 und SQL Server 2014 konvertiert wird).  
  
-   Verwenden SSMA-Sequenz-Generator.  
  
-   Verwenden die Identität der Spalte.  
  
Die Standardoption beim Konvertieren in SQL Server 2012 oder SQL Server 2014 ist die Verwendung von SQL Server-Sequenz-Generator. Allerdings SQL Server 2012 und SQL Server 2014 unterstützt keine aktuelle Sequenzwert (z. B. mit der DB2 Sequenz Currval-Methode) abrufen. Verweisen Sie auf Blog SSMA-Teamwebsite Anleitungen zur Migration von DB2 Sequenz Currval-Methode.  
  
SSMA bietet auch eine Option aus, um die DB2-Sequenz in SSMA Sequenz Emulator zu konvertieren. Dies ist die Standardoption, wenn Sie in SQL Server vor 2012 konvertieren  
  
Schließlich können Sie auch Sequenz zugewiesen werden, um eine Spalte in der Tabelle, um SQL Server-Identity-Werte konvertieren. Sie müssen angeben, dass die Zuordnung zwischen der Sequenzen, um eine Identitätsspalte in DB2 **Tabelle** Registerkarte  
  
### <a name="convert-currval-outside-triggers"></a>Konvertieren von CURRVAL außerhalb Trigger  
Nur sichtbar, wenn die Sequenz-Generator konvertiert, um festgelegt ist **mithilfe der Spalte Identity**. Da DB2 Sequenzen Objekte, die getrennt von Tabellen sind, verwenden viele Tabellen, die Sequenzen verwenden ein Triggers zu generieren, und fügen Sie einen neuen Sequenzwert. SSMA Kommentare, diese Anweisungen oder kennzeichnet diese als Fehler, wenn die Kommentare Out Fehler generieren.  
  
-   Bei Auswahl des **Ja**, SSMA werden alle Verweise auf außerhalb Trigger für die konvertierte CURRVAL mit einer Warnung Sequenz gekennzeichnet.  
  
-   Bei Auswahl des **keine**, SSMA werden alle Verweise auf außerhalb Trigger für die konvertierte CURRVAL mit einem Fehler Sequenz gekennzeichnet.  
  
## <a name="see-also"></a>Siehe auch  
[Referenz zur Benutzeroberfläche &#40; DB2ToSQL &#41;](../../ssma/db2/user-interface-reference-db2tosql.md)  
  

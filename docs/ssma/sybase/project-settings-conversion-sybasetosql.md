---
title: Projekteinstellungen (Konvertierung) (SybaseToSQL) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: eeb80fa5-f530-4f21-beee-25f5a4b8ace6
caps.latest.revision: "8"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 07ba161d9f053e35c80f9c22627a55a4f1cab003
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="project-settings-conversion-sybasetosql"></a>Projekteinstellungen (Konvertierung) (SybaseToSQL)
Die Seite "Konvertierung", der die **Projekteinstellungen** Dialogfeld enthält Einstellungen, anpassen, wie SSMA für Sybase Adaptive Server Enterprise (ASE)-Syntax, um konvertiert [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Syntax.  
  
Bereich Konvertierung finden Sie in der **Projekteinstellungen** und **Projekt Standardeinstellungen** Dialogfelder:  
  
-   Wenn Sie Einstellungen für alle SSMA-Projekte auf angeben möchten die **Tools** klicken Sie im Menü **Projekt Standardeinstellungen**, klicken Sie auf **allgemeine** am unteren Rand der linken Bereich, und klicken Sie dann auf **Konvertierung**.  
  
-   Zum Angeben von Einstellungen für das aktuelle Projekt auf die **Tools** klicken Sie im Menü **Projekteinstellungen**, klicken Sie auf **allgemeine** am unteren Rand der linken Bereich, und klicken Sie dann auf **Konvertierung**.  
  
## <a name="miscellaneous-options"></a>Sonstige Optionen  
**@@ERROR**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure und ASE verwenden die verschiedenen Fehlercodes.  
  
Mit dieser Einstellung können Sie den Typ der Nachricht ("Warnung" oder "Fehler") angeben, in der SSMA im Bereich "Ausgabe" oder "Fehlerliste" angezeigt, wenn er erkennt, dass einen Verweis auf **@@ERROR**  im ASE Code.  
  
-   Bei Auswahl des **konvertieren, und markieren Sie mit der Warnung**, SSMA konvertiert die Anweisungen und mit Warnungskommentare zu markieren.  
  
-   Bei Auswahl des **Markierung mit Fehler**, SSMA überspringt Konvertierung und markieren Sie die Anweisungen mit Fehler Kommentare.  
  
Bei Auswahl einer Konvertierungsmodus in der **Modus** Feld SSMA gilt die folgende Einstellung:  
  
**Standard/Optimistic-Modus:** konvertieren, und markieren Sie mit der Warnung  
  
**Vollmodus:** Markierung mit Fehler  
  
**Konvertierung von LIKE-operator**  
Gibt an, ob wie Operanden Sybase ASE Verhalten entsprechend konvertiert. Der Punkt ist, dass Sybase nachfolgende Leerzeichen in einer like-Muster anzupassen. Die problemumgehung besteht darin, von einer Typumwandlung der rechte Ausdruck in einem Datentyp fester Länge mit einer maximalen Genauigkeit.  
  
-   Wählen Sie **einfache Konvertierung** , die Ausdrücke ohne Korrektur zu konvertieren.  
  
-   Verwenden Sie die ASE Verhalten SELECT-Anweisung **fester Länge umgewandelt.**  
  
Bei der Auswahl einer Konvertierungsmodus im Modus gilt SSMA die folgende Einstellung:  
  
**Standard/Optimistic Modus**: einfache Konvertierung  
  
**Vollständige Modus**: umgewandelt fester Länge  
  
**KONVERTIEREN SIE ODER WANDELN SIE LEERE ZEICHENFOLGEN IN NUMERISCHE TYPEN**  
Gibt an, wie behandeln Eintrag oder leere Zeichenfolgen innerhalb von CONVERT oder CAST-Ausdrücken mit numerischen Typs als Datentyp-Argument. Die folgenden Optionen sind für diese Einstellung verfügbar:  
  
-   Wählen Sie **einfache Konvertierung** , die Ausdrücke ohne Korrektur zu konvertieren.  
  
-   Wenn **leere Zeichenfolge als 0 (null) numerische** ausgewählt ist, wird die Groß-/Kleinschreibung ltrim(rtrim({s})) Zeichenfolgenparameter {s} ersetzt werden beim "" dann 0 else {s} ENDAUSDRUCK  
  
Bei der Auswahl einer Konvertierungsmodus im Modus gilt SSMA die folgende Einstellung:  
  
**Standard/Optimistic Modus**: einfache Konvertierung  
  
**Vollständige Modus**: leere Zeichenfolge als 0 (null) numerisch  
  
**Verkettung von NULL**  
Diese Einstellung gibt an, wie das Verketten von Zeichenfolgen mit NULL zu konvertieren. Die folgenden Optionen können für diese bestimmte Einstellung festgelegt werden:  
  
-   **Umschließen mit ISNULL-Funktion:** , wenn diese Option festgelegt ist, jeder nicht-Konstante "String_expression" in der Verkettung ISNULL(string_expression) eingebunden werden wird und NULL-Werte werden durch eine leere Zeichenfolge ersetzt.  
  
-   **Behalten Sie die aktuelle syntax**  
  
Bei Auswahl einer Konvertierungsmodus in der **Modus** Feld SSMA gilt die folgende Einstellung:  
  
**Standard/Optimistic-Modus:** aktuellen Syntax beibehalten  
  
**Vollmodus:** Umschließen mit ISNULL-Funktion  
  
**Konvertierung von leeren Zeichenfolgen**  
Diese Einstellung gibt an, wie leere Zeichenfolgen zu konvertieren. Die folgenden Optionen können für diese bestimmte Einstellung festgelegt werden:  
  
-   **Ersetzen Sie alle Zeichenfolgenausdrücke mit Leerzeichen**  
  
-   **Ersetzen Sie leere Zeichenfolgenkonstanten mit Leerzeichen**  
  
-   Verwenden der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure-Verhalten, select **behalten Sie die aktuelle Syntax**.  
  
Bei Auswahl einer Konvertierungsmodus in der **Modus** Feld SSMA gilt die folgende Einstellung:  
  
**Standard/Optimistic-Modus:** aktuellen Syntax beibehalten  
  
**Vollmodus:** ersetzen alle Zeichenfolgenausdrücke mit Leerzeichen  
  
**KONVERTIERT, und die Umwandlung Binärzeichenfolge-Konvertierung**  
Die Konvertierung der Binärwerte in Zahlen kann auf verschiedenen Plattformen unterschiedliche Werte zurückgeben. Z. B. auf X86 Prozessoren, CONVERT (ganze Zahl, 0 x 00000100) zurückgibt, 65536 in ASE und 256 in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. ASE gibt auch verschiedene Werte je nach Bytereihenfolge zurück.  
  
Verwenden Sie diese Einstellung aus, um zu steuern, wie SSMA konvertiert konvertieren und CASE-Ausdrücke, die binäre Werte enthalten:  
  
-   Wählen Sie **einfache Konvertierung** , die Ausdrücke ohne Korrektur oder Warnungen zu konvertieren. Verwenden Sie diese Einstellung, wenn Sie wissen, dass dem ASE-Server eine Bytereihenfolge ist, die keine Änderungen des binären Werts erforderlich ist.  
  
-   Wählen Sie **konvertieren, und beheben Sie** haben SSMA konvertieren, und beheben Sie die Ausdrücke für die Verwendung auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Die Bytereihenfolge in literaler Konstanten werden rückgängig gemacht werden. Alle anderen binäre Werte (z. B. binäre Variablen und Spalten) werden mit Fehlern markiert. Verwenden Sie diesen Wert, wenn Sie wissen, dass die ASE-Server eine Bytereihenfolge besitzt, Änderungen an Binärwerte erfordert.  
  
-   Wählen Sie **konvertieren, und markieren Sie mit der Warnung** haben SSMA konvertieren, und beheben Sie die Ausdrücke, und markieren alle Ausdrücke mit Warnungskommentare konvertiert.  
  
Bei Auswahl einer Konvertierungsmodus in der **Modus** Feld SSMA gilt die folgende Einstellung:  
  
**Standardmodus:** konvertieren, und markieren Sie mit der Warnung  
  
**Optimistische Modus:** einfache Konvertierung  
  
**Vollmodus:** konvertieren, und beheben Sie  
  
**Dynamisches SQL**  
Verwenden Sie diese Einstellung, um den Typ der Nachricht (Warnung oder Fehler) anzugeben, die SSMA im Bereich "Ausgabe" oder "Fehlerliste" zeigt, dynamisches SQL im Code ASE stößt.  
  
-   Bei Auswahl des **konvertieren, und markieren Sie mit der Warnung**, SSMA dynamische SQL konvertiert und markieren Sie die Anweisungen mit Warnungskommentare.  
  
-   Bei Auswahl des **Markierung mit Fehler**, SSMA überspringt Konvertierung und markieren Sie die Anweisungen mit Fehler Kommentare.  
  
Bei Auswahl einer Konvertierungsmodus in der **Modus** Feld SSMA gilt die folgende Einstellung:  
  
**Standard/Optimistic-Modus:** konvertieren, und markieren Sie mit der Warnung  
  
**Vollmodus:** Markierung mit Fehler  
  
**Gleichheit Kontrollkästchen Konvertierung**  
In [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure, wenn die ANSI_NULLS-Einstellung on ist [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure Gibt UNKNOWN zurück, wenn alle Vergleiche auf Gleichheit einen null-Wert enthält. Wenn ANSI_NULLS deaktiviert ist, Übereinstimmungsvergleiche, die null-Werte enthalten "true" zurückgeben, wenn die verglichenen Spalte und Ausdruck oder zwei Ausdrücke beide sind null. Nach Standard (ANSINULL OFF) Sybase ASE Gleichheit Vergleiche Verhalten sich wie [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure mit ANSI_NULLS OFF.  
  
-   Bei Auswahl des **einfache Konvertierung**, SSMA konvertiert den Code ASE [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ Azure SQL-Syntax ohne zusätzliche Überprüfungen für null-Werte. Verwenden Sie diese Einstellung, wenn ANSI_NULLS auf off in ist [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure oder überarbeiten Sie die Durchführung von Gleichheitsvergleichen pro Fall zu Fall werden sollen.  
  
-   Bei Auswahl des **sollten Sie Nullwerte**, SSMA wird überprüft, null-Werte hinzufügen, indem Sie die Klauseln IS NULL und IS NOT NULL.  
  
Bei Auswahl einer Konvertierungsmodus in der **Modus** Feld SSMA gilt die folgende Einstellung:  
  
**Standard/Optimistic-Modus:** einfache Konvertierung  
  
**Vollmodus:** ggf. NULL Werte  
  
**Formatzeichenfolgen**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Oder nicht mehr unterstützt SQL Azure die *Format_string* Argument Print- und RAISERROR-Anweisungen. Die *Format_string* Variable unterstützt ersetzbare Parameter direkt in der Zeichenfolge einfügen, und klicken Sie dann die Parameter zur Laufzeit ersetzt. Stattdessen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] erfordert die vollständige Zeichenfolge über ein Zeichenfolgenliteral oder eine Zeichenfolge mit einer Variablen erstellt. Weitere Informationen finden Sie unter der "PRINT ([!INCLUDE[tsql](../../includes/tsql_md.md)])" im Thema [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Books Online.  
  
Wenn SSMA trifft eine *Format_string* Argument, es kann entweder ein Zeichenfolgenliteral mit den Variablen erstellen oder erstellen Sie eine neue Variable und erstellen Sie eine Zeichenfolge mithilfe dieser Variablen.  
  
-   Um ein Zeichenfolgenliteral für Print- und RAISERROR-Funktionen verwenden möchten, wählen **Erstellen der neuen Zeichenfolge**.  
  
    Wenn eine Print- oder RAISERROR-Anweisung keine Platzhalter und lokale Variablen verwendet, ist die Anweisung in diesem Modus kann nicht geändert. Doppelte Prozent Zeichen ("%") werden in ein einzelnes Prozentzeichen % in Zeichenfolgenliteralen drucken geändert.  
  
    Wenn eine Print- oder RAISERROR-Anweisung, Platzhalter und eine verwendet oder mehrere lokalen Variablen, wie im folgenden Beispiel:  
  
    ```  
    PRINT 'Total: %1!%%', @percent  
    ```  
    SSMA wandelt sie in der folgenden Syntax:  
  
    ```  
    PRINT 'Total: '+ CAST(@percent AS varchar(max)) + '%'  
    ```  
    Wenn *Format_string* ist eine Variable, wie in der folgenden Anweisung:  
  
    ```  
    PRINT @fmt, @arg1, @arg2  
    ```  
    SSMA eine einfache zeichenfolgenkonvertierung ist nicht möglich, und Sie müssen eine neue Variable erstellen:  
  
    ```  
    DECLARE @print_format_1 varchar(max)  
    SET @print_format_1  =   
        REPLACE (@fmt, '%%', '%')  
    SET @print_format_1  =   
        REPLACE (@print_format_1, '%1!',   
        CAST (@arg1 AS varchar(max)))  
    SET @print_format_1  =   
        REPLACE (@print_format_1, '%2!',   
        CAST (@arg2 AS varchar(max)))  
    PRINT @print_format_1  
    ```  
    Wenn es verwendet **Erstellen der neuen Zeichenfolge** Modus SSMA setzt voraus, dass die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Option CONCAT_NULL_YIELDS_NULL auf OFF gesetzt ist. SSMA überprüft daher nicht für null-Argumente.  
  
-   Wählen Sie zum Speichern SSMA für jede Print- und RAISERROR-Anweisung eine neue Variable erstellen und verwenden Sie diese Variable für den Zeichenfolgenwert **neue Variable erstellen**.  
  
    In diesem Modus Wenn eine Print- oder RAISERROR-Anweisung keine Platzhalter und lokale Variablen verwendet SSMA ersetzt alle doppelte Prozent Zeichen ("%") mit einzelnen Prozent Zeichen zur Einhaltung [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ Azure SQL-Syntax.  
  
    Wenn eine Print- oder RAISERROR-Anweisung, Platzhalter und eine verwendet oder mehrere lokalen Variablen, wie im folgenden Beispiel:  
  
    ```  
    PRINT 'Total: %1!%%', @percent  
    ```  
    SSMA wandelt sie in der folgenden Syntax:  
  
    ```  
    DECLARE @print_format_1 varchar(max)  
    SET @print_format_1 = 'Total: %1!%'  
    SET @print_format_1  =   
        REPLACE (@print_format_1, '%1!',   
        ISNULL(CAST (@percent AS VARCHAR(max)), ''))  
    PRINT @print_format_1  
    ```  
    Wenn *Format_string* ist eine Variable, wie in der folgenden Anweisung:  
  
    ```  
    PRINT @fmt, @arg1, @arg2  
    ```  
    SSMA erstellt eine neue Variable wie folgt Überprüfen auf null-Werte in jedem Argument:  
  
    ```  
    DECLARE @print_format_1 varchar(max)  
    SET @print_format_1  =   
        REPLACE (@fmt, '%%', '%')  
    SET @print_format_1  =   
        REPLACE (@print_format_1, '%1!',   
        ISNULL(CAST (@arg1 AS varchar(max)),''))  
    SET @print_format_1  =   
        REPLACE (@print_format_1, '%2!',   
        ISNULL(CAST (@arg2 AS varchar(max)),''))  
    PRINT @print_format_1  
    ```  
  
Bei Auswahl einer Konvertierungsmodus in der **Modus** Feld SSMA gilt die folgende Einstellung:  
  
**Standard/Optimistic-Modus:** neue Zeichenfolge erstellen  
  
**Vollmodus:** neue Variable erstellen  
  
**Legen Sie einen expliziten Wert in eine Timestamp-Spalte**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Oder Einfügen von expliziten Werten in eine Timestamp-Spalte unterstützt SQL Azure nicht.  
  
-   Wählen Sie zum Ausschließen von Timestamp-Spalten von INSERT-Anweisungen **ausschließen Spalte**.  
  
-   Aktivieren, um eine Fehlermeldung jedes Mal drucken, die eine Timestamp-Spalte in einer INSERT-Anweisung ist **Markierung mit Fehler**. In diesem Modus werden INSERT-Anweisungen nicht konvertiert werden und werden mit dem Fehler Kommentare gekennzeichnet werden.  
  
Bei Auswahl einer Konvertierungsmodus in der **Modus** Feld SSMA gilt die folgende Einstellung:  
  
**Standard/Optimistic-Modus:** Exclude-Spalte  
  
**Vollmodus:** Markierung mit Fehler  
  
**Speichern Sie temporäre Objekte, die in-Prozeduren definierten**  
Diese Einstellung gibt an, ob die temporäre Objekte-Definitionen der in den Verfahren erscheint während der Konvertierung in den Metadaten der Datenquelle gespeichert werden sollen.  
  
-   Wählen Sie **Ja** in Metadaten zu speichernde.  
  
-   Wählen Sie **keine** , wenn die Objekte nicht gespeichert werden müssen.  
  
**Standard/Optimistic-Modus:** Ja  
  
**Vollmodus:** Nein  
  
**Proxy-tabellenkonvertierung**  
Gibt an, ob ASE Proxytabellen konvertiert werden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure-Tabellen oder werden nicht konvertiert, und der Code ist mit Fehler Kommentare gekennzeichnet.  
  
-   Wählen Sie **konvertieren** Proxytabellen in regelmäßigen Tabellen konvertieren.  
  
-   Wählen Sie **Markierung mit Fehler** um den Proxycode für die Tabelle mit Kommentaren Fehler einfach zu markieren.  
  
Bei Auswahl einer Konvertierungsmodus in der **Modus** Feld SSMA gilt die folgende Einstellung:  
  
**Standard/Optimistic/Full-Modus:** Markierung mit Fehler  
  
**RAISERROR Basis Meldungsnummer**  
ASE Benutzernachrichten werden in jeder Datenbank gespeichert. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Benutzernachrichten zentral gespeichert und über zur Verfügung gestellt werden die **sys.messages** -Katalogsicht angezeigt. Darüber hinaus ASE Benutzernachrichten ausgehend von 20000, aber [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Fehlermeldungen an 50001 beginnen.  
  
Diese Einstellung gibt die Anzahl der ASE Benutzer Meldungsnummer umzuwandeln hinzuzufügende eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Meldung für den Benutzer. Wenn Ihre [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] hat der Benutzernachrichten in der **sys.messages** -Katalogsicht, möglicherweise müssen Sie diese Zahl auf einen höheren Wert zu ändern. Dies ist die konvertierte Nachricht Zahlen nicht mit vorhandenen Meldungsnummern in Konflikt stehen.  
  
Beachten Sie Folgendes:  
  
-   ASE Nachrichten im Bereich 17000 19999 aus der Sysmessages-Systemtabelle werden und werden nicht konvertiert.  
  
-   Wenn die Meldungsnummer, die in der RAISERROR-Anweisung verwiesen wird, eine Konstante ist, wird SSMA die Basis Meldungsnummer die Konstante zur Bestimmung der Anzahl der neue Benutzer Nachricht hinzufügen.  
  
-   Wenn die Meldungsnummer, auf die verwiesen wird, wird eine Variable oder ein Ausdruck ist, wird SSMA eine temporäre Variable erstellt.  
  
-   Im optimistischen Modus SSMA setzt voraus, dass die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Option CONCAT_NULL_YIELDS_NULL deaktiviert ist, und macht keine Überprüfungen für null-Argumente.  
  
-   Im vollständigen Modus überprüft SSMA null-Argumente.  
  
-   RAISERROR mit FEHLERDATEN *Liste* wird nicht konvertiert.  
  
Bei Auswahl einer Konvertierungsmodus in der **Modus** Feld SSMA gilt die folgende Einstellung:  
  
**Standard/optimistische/Full-Modus:** 30001  
  
**Systemobjekte anzeigen**  
Verwenden Sie diese Einstellung, um den Typ der Nachricht (Warnung oder Fehler) anzugeben, in der SSMA im Bereich "Ausgabe" oder "Fehlerliste" angezeigt, wenn die Verwendung von Systemobjekten ASE festgestellt wird.  
  
-   Bei Auswahl des **konvertieren, und markieren Sie mit der Warnung**, SSMA Verweise auf Systemobjekte konvertiert und werden in Anweisungen mit Warnungskommentare gekennzeichnet.  
  
-   Bei Auswahl des **Markierung mit Fehler**, SSMA nicht konvertiert werden, Verweise auf Systemobjekte und Anweisungen mit Kommentaren Fehler kennzeichnet.  
  
Bei Auswahl einer Konvertierungsmodus in der **Modus** Feld SSMA gilt die folgende Einstellung:  
  
**Standard/Optimistic-Modus:** konvertieren, und markieren Sie mit der Warnung  
  
**Vollmodus:** Markierung mit Fehler  
  
**Nicht aufgelöste Bezeichner**  
Verwenden Sie diese Einstellung, um den Typ der Nachricht (Warnung oder Fehler) anzugeben, in der SSMA im Bereich "Ausgabe" oder "Fehlerliste" angezeigt, wenn einen Bezeichner nicht auflösen kann.  
  
-   Bei Auswahl des **konvertieren, und markieren Sie mit der Warnung**, SSMA wird versucht, die Verweise auf nicht aufgelöste Bezeichner konvertieren und Anweisungen mit Warnungskommentare kennzeichnet.  
  
-   Bei Auswahl des **Markierung mit Fehler**, SSMA nicht konvertiert werden, verweisen auf nicht aufgelöste Bezeichner und Anweisungen mit Kommentaren Fehler kennzeichnet.  
  
Bei Auswahl einer Konvertierungsmodus in der **Modus** Feld SSMA gilt die folgende Einstellung:  
  
**Standard/Optimistic-Modus:** konvertieren, und markieren Sie mit der Warnung  
  
**Vollmodus:** Markierung mit Fehler  
  
## <a name="system-function-options"></a>Systemoptionen-Funktion  
**CHARINDEX-Funktion**  
In ASE gibt CHARINDEX NULL zurück, nur, wenn alle Eingabeausdrücke NULL sind. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure gibt NULL zurück, wenn jeder eingegebene Ausdruck NULL ist.  
  
-   Wählen Sie für die Verwendung der ASE Verhalten **Ersetzungsaktion**. Alle Aufrufe CHARINDEX-Funktion ist mit einem Aufruf von CHARINDEX_VARCHAR oder CHARINDEX_NVARCHAR eine benutzerdefinierte Funktion, die basierend auf dem Typ des übergebenen Parameter (in der Benutzerdatenbank unter dem Schema "s2ss" erstellt) zum Emulieren des Verhaltens Sybase ASE ersetzt.  
  
-   Verwenden der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure-Verhalten, select **behalten Sie die aktuelle Syntax**.  
  
Bei Auswahl einer Konvertierungsmodus in der **Modus** Feld SSMA gilt die folgende Einstellung:  
  
**Standard/Optimistic-Modus:** aktuellen Syntax beibehalten  
  
**Vollmodus:** Replace-Funktion  
  
**DATALENGTH-Funktion**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure und ASE unterscheiden sich in den Wert, der durch die DATALENGTH-Funktion zurückgegeben wird, wenn der Wert ein Leerzeichen ist. In diesem Fall [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure gibt 0 zurück und ASE gibt 1 zurück.  
  
-   Wählen Sie für die Verwendung der ASE Verhalten **Ersetzungsaktion**. Alle Aufrufe an die DATALENGTH-Funktion werden mit CASE-Ausdrucks zur Emulierung des Verhaltens von Sybase ASE durch ersetzt.  
  
-   Die Standardeinstellung verwenden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] / SQL Azure-Verhalten, wählen **behalten Sie die aktuelle Syntax**.  
  
Bei Auswahl einer Konvertierungsmodus in der **Modus** Feld SSMA gilt die folgende Einstellung:  
  
**Standard/Optimistic-Modus:** aktuellen Syntax beibehalten  
  
**Vollmodus:** Replace-Funktion  
  
**INDEX_COL-Funktion**  
ASE unterstützt eine optionale *User_id* Argument für die INDEX_COL-Funktion; allerdings [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure dieses Argument nicht unterstützt. Bei Verwendung der *User_id* Argument dieser Funktion kann nicht konvertiert werden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ Azure SQL-Syntax.  
  
-   Wählen Sie für die Verwendung der ASE Verhalten **Convert-Funktion**. Wenn der Code enthält die *User_id* Argument SSMA wird einen Fehler angezeigt.  
  
-   Um eine Fehlermeldung anzuzeigen, jedes Mal, wenn diese INDEX_COL gefunden wird, wählen **Markierung mit Fehler**. SSMA Verweise auf die Funktion nicht konvertiert, und Sie werden in die Anweisung mit Fehler Kommentare gekennzeichnet.  
  
**Standard/Optimistic/Full-Modus:** Markierung mit Fehler  
  
**INDEX_COLORDER-Funktion**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Oder eine Systemfunktion INDEX_COLORDER keinen SQL Azure.  
  
-   Wählen Sie für die Verwendung der ASE Verhalten **Convert-Funktion**. Alle Aufrufe INDEX_COLORDER-Funktion wird durch einen Aufruf an eine benutzerdefinierte Funktion mit demselben Namen INDEX_COLORDER (in der Benutzerdatenbank unter dem Schema "s2ss" erstellt), der emuliert das Verhalten für Sybase ASE ersetzt.  
  
-   Aktivieren, um eine Fehlermeldung zu drucken, jedes Mal, INDEX_COLORDER auftritt **Markierung mit Fehler**. SSMA Verweise auf die Funktion nicht konvertiert, und Sie werden in die Anweisung mit Fehler Kommentare gekennzeichnet.  
  
Bei Auswahl einer Konvertierungsmodus in der **Modus** Feld SSMA gilt die folgende Einstellung:  
  
**Standard/Optimistic/Full-Modus:** Markierung mit Fehler  
  
**Funktionen der linken und rechten**  
Links und rechts Funktionen von Sybase verhält sich anders für negative Length-Parameter.  
  
-   Wählen Sie für die Verwendung der ASE Verhalten **Ersetzen-Funktion**. Der Length-Parameter wird dann mit CASE-Ausdruck ersetzt dann würde für negativen Wert null zurückgegeben.  
  
-   Um das Verhalten von SQL Server verwenden möchten, wählen **aktuellen Syntax beibehalten**  
  
Bei Auswahl einer Konvertierungsmodus in der **Modus** Feld SSMA gilt die folgende Einstellung:  
  
**Standard/Optimistic-Modus:** aktuellen Syntax beibehalten  
  
**Vollmodus:** Replace-Funktion  
  
> [!NOTE]  
> Wenn der Length-Parameter einen Literalwert und nicht auf einen komplexen Ausdruck ist, wird der Längenwert immer mit Null, unabhängig von projekteinstellung ersetzt.  
  
**NEXT_IDENTITY-Funktion**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Oder eine Systemfunktion NEXT_IDENTITY keinen SQL Azure.  
  
-   Wählen Sie für die Verwendung der ASE Verhalten **Convert-Funktion**. Alle Aufrufe NEXT_IDENTITY-Funktion ersetzt wird, mit dem Ausdruck (IDENT_CURRENT(parameter Value) + IDENT_INCR(parameter Value) die emuliert das Verhalten für Sybase ASE.  
  
-   Aktivieren, um eine Fehlermeldung zu drucken, jedes Mal, NEXT_IDENTITY auftritt **Markierung mit Fehler**. SSMA Verweise auf die Funktion nicht konvertiert, und Sie werden in die Anweisung mit Fehler Kommentare gekennzeichnet.  
  
Bei Auswahl einer Konvertierungsmodus in der **Modus** Feld SSMA gilt die folgende Einstellung:  
  
**Standard/Optimistic/Full-Modus:** Markierung mit Fehler  
  
**PATINDEX-Funktion**  
Gibt an, ob PATINDEX-Funktion Sybase ASE Verhalten entsprechend konvertiert. Der Punkt ist, dass Sybase nachfolgende Leerzeichen in einem Suchmuster abschneidet. Die problemumgehung besteht darin, eine Umwandlung der Value-Ausdruck mit einer festen Länge stellen Daten mit einer maximalen Genauigkeit und wenden Sie Rtrim-Funktion, um Muster zu suchen.  
  
-   Verwenden Sie die ASE Verhalten SELECT-Anweisung **verwenden**.  
  
-   Die Standard- [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure-Verhalten, select **verwenden Sie keine**.  
  
Bei Auswahl einer Konvertierungsmodus in der **Modus** Feld SSMA gilt die folgende Einstellung:  
  
**Standard/Optimistic-Modus:** nicht verwenden  
  
**Vollmodus:** verwenden  
  
**REPLICATE-Funktion**  
Die REPLICATE-Funktion wird eine Zeichenfolge die angegebene Anzahl von Malen wiederholt. Wenn Sie angeben, dass die Zeichenfolge null-Mal wiederholen, ist das Ergebnis in ASE null. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure, das Ergebnis ist eine leere Zeichenfolge.  
  
-   Wählen Sie für die Verwendung der ASE Verhalten **Ersetzungsaktion**. Alle Aufrufe an die REPLICATE-Funktion ist mit einem Aufruf von REPLICATE_VARCHAR oder REPLICATE_NVARCHAR eine benutzerdefinierte Funktion, die basierend auf dem Typ des übergebenen Parameter (in der Benutzerdatenbank unter dem Schema "s2ss" erstellt) zum Emulieren des Verhaltens Sybase ASE ersetzt.  
  
-   Die Standardeinstellung verwenden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure-Verhalten, select **Ersetzen-Funktion**.  
  
Bei Auswahl einer Konvertierungsmodus in der **Modus** Feld SSMA gilt die folgende Einstellung:  
  
**Standard/Optimistic Modus/Full-Modus:** Replace-Funktion  
  
**TRIM (LTRIM, RTRIM)-Funktion**  
Diese Einstellung gibt an, ob Aufrufe von Funktionen Trim (LTRIM, RTRIM) mit der Sybase ASE äquivalente Syntax Funktionen ersetzen oder die aktuelle Syntax beibehalten. Die folgenden Optionen sind für diese bestimmte Einstellung vorhanden:  
  
-   **Replace-Funktion**  
  
-   **Behalten Sie die aktuelle syntax**  
  
Bei Auswahl einer Konvertierungsmodus in der **Modus** Feld SSMA gilt die folgende Einstellung:  
  
**Standard/Optimistic Modus/Full-Modus:** Replace-Funktion  
  
**SUBSTRING-Funktion**  
In ASE, die Funktion `SUBSTRING(expression, start, length)` gibt NULL zurück, wenn ein Startwert größer als die Anzahl der Zeichen im Ausdruck angegeben ist oder die Länge 0 (null) beträgt. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]/ SQL Azure der entsprechende Ausdruck eine leere Zeichenfolge zurückgegeben.  
  
-   Wählen Sie für die Verwendung der ASE Verhalten **Ersetzungsaktion**. Alle Aufrufe an die SUBSTRING-Funktion ist mit einem Aufruf von SUBSTRING_VARCHAR oder SUBSTRING_NVARCHAR oder SUBSTRING_VARBINARY eine benutzerdefinierte Funktion, die basierend auf dem Typ des übergebenen Parameter (in der Benutzerdatenbank unter dem Schema "s2ss" erstellt) zum Emulieren des Verhaltens Sybase ASE ersetzt.  
  
-   Verwenden der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] / SQL Azure-Verhalten, select **behalten Sie die aktuelle Syntax**.  
  
Bei Auswahl einer Konvertierungsmodus in der **Modus** Feld SSMA gilt die folgende Einstellung:  
  
**Standard/Optimistic-Modus:** aktuellen Syntax beibehalten  
  
**Vollmodus:** Replace-Funktion  
  
## <a name="tables"></a>TABLES  
**Primärschlüssel hinzufügen**  
Erstellt einen neuen primären Schlüssel in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Tabelle, wenn eine Access-Tabelle ohne Primärschlüssel oder eindeutigen Index verfügt.  
  
-   **Standardmodus**: "false"  
  
-   **Vollständige**: "false"  
  
-   **Vollständige Modus**: "true"  
  
> [!NOTE]  
> Wenn in SQL Azure verbunden ist, ist es standardmäßig "Wahr".  
  
## <a name="see-also"></a>Siehe auch  
[Referenz zur Benutzeroberfläche &#40; SybaseToSQL &#41;](../../ssma/sybase/user-interface-reference-sybasetosql.md)  
  

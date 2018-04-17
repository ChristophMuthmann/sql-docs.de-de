---
title: SQLColAttribute-Funktion | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SQLColAttribute
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLColAttribute
helpviewer_keywords:
- SQLColAttribute function [ODBC]
ms.assetid: 8c45c598-cb01-4789-a571-e93619a18ed9
caps.latest.revision: 42
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 765cdab2b8619501a29990c9b944b3b98797b4ed
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sqlcolattribute-function"></a>SQLColAttribute-Funktion
**Konformität**  
 Version eingeführt: ODBC 3.0 Standardkonformität: ISO-92  
  
 **Zusammenfassung**  
 **SQLColAttribute** Deskriptorinformationen für eine Spalte in einem Resultset zurückgegeben. Deskriptorinformationen wird als eine Zeichenfolge, einen Deskriptor abhängiges-Wert oder einen ganzzahligen Wert zurückgegeben.  
  
> [!NOTE]  
>  Weitere Informationen zu welcher der Treiber-Manager ordnet diese Funktion auf, wenn eine ODBC 3. *x* Anwendung arbeitet mit einer ODBC 2. *X* -Treiber verwenden, finden Sie unter [Ersatz-Zuordnungsfunktionen für Backward Compatibility Anwendungen](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLColAttribute (  
      SQLHSTMT        StatementHandle,  
      SQLUSMALLINT    ColumnNumber,  
      SQLUSMALLINT    FieldIdentifier,  
      SQLPOINTER      CharacterAttributePtr,  
      SQLSMALLINT     BufferLength,  
      SQLSMALLINT *   StringLengthPtr,  
      SQLLEN *        NumericAttributePtr);  
```  
  
## <a name="arguments"></a>Argumente  
 *StatementHandle*  
 [Eingabe] Anweisungshandle.  
  
 *ColumnNumber*  
 [Eingabe] Die Anzahl des Datensatzes in IRD dort der Wert des Felds wird abgerufen werden sollen. Dieses Argument entspricht die Spaltennummer der Ergebnisdaten, sequenziell sortiert in aufsteigender Spaltenreihenfolge, beginnend mit 1. Spalten können in beliebiger Reihenfolge beschrieben werden.  
  
 In diesem Argument kann die Spalte 0 angegeben werden, aber alle Werte außer SQL_DESC_TYPE und SQL_DESC_OCTET_LENGTH nicht definierte Werte zurück.  
  
 *FieldIdentifier*  
 [Eingabe] Die Deskriptorhandles. Dieses Handle wird definiert, welches Feld in IRD (z. B. SQL_COLUMN_TABLE_NAME) abgefragt werden soll.  
  
 *CharacterAttributePtr*  
 [Ausgabe] Zeiger auf einen Puffer, in dem den Wert in zurückgegeben der *FieldIdentifier* Feld der *ColumnNumber* Zeile vom IRD, wenn das Feld eine Zeichenfolge ist. Andernfalls wird das Feld nicht verwendet.  
  
 Wenn *CharacterAttributePtr* NULL ist, *StringLengthPtr* gibt weiterhin zurück, die Gesamtanzahl der Bytes (ausgenommen die Null-Terminierung Zeichen für Zeichendaten) verfügbar, die in den Puffer zurückgegeben verweist *CharacterAttributePtr*.  
  
 *Pufferlänge*  
 [Eingabe] Wenn *FieldIdentifier* ist ein ODBC-definierten Feld und *CharacterAttributePtr* zeigt auf einen Zeichenfolgen- oder binären Puffer, in dieses Argument muss die Länge des \*  *CharacterAttributePtr*. Wenn *FieldIdentifier* ist ein ODBC-definierten Feld und \* *CharacterAttribute*Ptr ist eine ganze Zahl, wird dieses Feld ignoriert. Wenn die  *\*CharacterAttributePtr* eine Unicode-Zeichenfolge (beim Aufrufen von **SQLColAttributeW**), wird die *Pufferlänge* Argument muss eine gerade Zahl sein. Wenn *FieldIdentifier* ist ein Feld treiberdefinierten die Anwendung zeigt die Art des Felds um den Treiber-Manager an, indem die *Pufferlänge* Argument. *Pufferlänge* können die folgenden Werte aufweisen:  
  
-   Wenn *CharacterAttributePtr* ist ein Zeiger auf einen Zeiger *Pufferlänge* müssen den Wert SQL_IS_POINTER.  
  
-   Wenn *CharacterAttributePtr* ist ein Zeiger auf eine Zeichenfolge, die *Pufferlänge* ist die Länge des Puffers.  
  
-   Wenn *CharacterAttributePtr* ist ein Zeiger auf einen binären Puffer, der Anwendung stellen das Ergebnis der SQL_LEN_BINARY_ATTR (*Länge*)-Makro im *Pufferlänge*. Dies setzt einen negativen Wert in *Pufferlänge*.  
  
-   Wenn *CharacterAttributePtr* ist ein Zeiger auf einen Datentyp mit fester Länge *Pufferlänge* muss eines der folgenden sein: SQL_IS_INTEGER, SQL_IS_UNINTEGER, SQL_SMALLINT oder SQLUSMALLINT.  
  
 *StringLengthPtr*  
 [Ausgabe] Zeiger auf einen Puffer, in dem die Gesamtanzahl der Bytes (ausgenommen die Null-Terminierung Byte für Zeichendaten) zurückgegeben zur Rückgabe in **CharacterAttributePtr*.  
  
 Bei Zeichendaten ist die Anzahl der zurückzugebenden verfügbaren Bytes größer als oder gleich *Pufferlänge*, das die Deskriptorinformationen in \* *CharacterAttributePtr* auf abgeschnitten *Pufferlänge* abzüglich der Länge des ein Null-Abschlusszeichen und wird vom Treiber Null-terminiert.  
  
 Für alle anderen Typen von Daten, den Wert der *Pufferlänge* wird ignoriert, und der Treiber geht davon aus, die Größe der **CharacterAttributePtr* beträgt 32 Bits.  
  
 *NumericAttributePtr*  
 [Ausgabe] Zeiger auf eine ganze Zahl-Puffer, in dem den Wert im zurückzugebenden der *FieldIdentifier* Feld der *ColumnNumber* Zeile vom IRD, wenn das Feld einen numerischen Deskriptortyp, z. B. SQL_DESC_COLUMN_LENGTH ist. Andernfalls wird das Feld nicht verwendet. Beachten Sie, dass einige Treiber nur die untere 32 Bit schreiben können oder 16-Bit, der einen Puffer und lassen Sie das Bit höherer Ordnung unverändert. Aus diesem Grund sollten Anwendungen den Wert auf 0 initialisiert werden, vor dem Aufrufen dieser Funktion.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR oder SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLColAttribute** gibt SQL_ERROR oder SQL_SUCCESS_WITH_INFO, ein zugeordneten SQLSTATE-Wert abgerufen werden kann, durch den Aufruf **SQLGetDiagRec** mit einem *HandleType*von SQL_HANDLE_STMT auf, und ein *behandeln* von *StatementHandle*. Die folgende Tabelle enthält die SQLSTATE-Werten, die häufig zurückgegebenes **SQLColAttribute** und erläutert, jeweils im Kontext dieser Funktion; die Notation "(DM)" vorangestellt ist, die Beschreibungen der SQLSTATEs, die vom Treiber-Manager zurückgegeben. Der Rückgabecode, der jeden SQLSTATE-Wert zugeordnet wird SQL_ERROR zurückgegeben, sofern nicht anders angegeben.  
  
|SQLSTATE|Fehler|Description|  
|--------------|-----------|-----------------|  
|01000|Allgemeine Warnung|Treiberspezifische Meldung dient zu Informationszwecken. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|01004|Zeichenfolgedaten wurden rechts abgeschnitten|Der Puffer \* *CharacterAttributePtr* war nicht groß genug für die gesamte Zeichenfolgenwert zurück, damit der Zeichenfolgenwert abgeschnitten wurde. Die Länge des Wertes ungekürzten Zeichenfolge wird zurückgegeben, **StringLengthPtr*. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|07005|Vorbereitete Anweisung keine *Cursor-Spezifikation*|Die zugeordnete Anweisung die *StatementHandle* ein Resultset zurückgibt und *FieldIdentifier* war nicht SQL_DESC_COUNT. Es wurden keine Spalten zu beschreiben.|  
|07009|Ungültiger Deskriptorindex|(DM) der angegebene Wert für *ColumnNumber* gleich 0 und das Anweisungsattribut SQL_ATTR_USE_BOOKMARKS wurde SQL_UB_OFF.<br /><br /> Der Wert für das Argument angegebene *ColumnNumber* war größer als die Anzahl der Spalten im Resultset.|  
|HY000|Allgemeiner Fehler|Für die es keine spezifischen SQLSTATE wurde und für die keine implementierungsabhängige SQLSTATE definiert wurde, ist ein Fehler aufgetreten. Die zurückgegebene Fehlermeldung **SQLGetDiagField** aus der Diagnosedaten Struktur beschreibt den Fehler und seiner Ursache.|  
|HY001|Fehler bei der speicherbelegung|Der Treiber konnte nicht belegt werden zur Unterstützung der Ausführung oder den Abschluss der Funktion erforderlich.|  
|HY008|Der Vorgang wurde abgebrochen|Asynchroner Verarbeitung wurde aktiviert, für die *StatementHandle*. Die Funktion aufgerufen wurde, und die Ausführung vor Abschluss **SQLCancel** oder **SQLCancelHandle** aufgerufen wurde, auf die *StatementHandle*. Und dann die Funktion erneut aufgerufen wurde, auf die *StatementHandle*.<br /><br /> Die Funktion aufgerufen wurde, und die Ausführung vor Abschluss **SQLCancel** oder **SQLCancelHandle** aufgerufen wurde, auf die *StatementHandle* aus einem anderen Thread in einem Multithread-Anwendung.|  
|HY010|Fehler bei Funktionssequenz|(DM) eine asynchron ausgeführte Funktion das, das zugeordnete Verbindungshandle hieß die *StatementHandle*. Diese Funktion Aynchronous wurde noch ausgeführt, beim Aufruf von SQLColAttribute.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, oder **SQLMoreResults** wurde aufgerufen, die *StatementHandle* und SQL_PARAM_DATA_ zurückgegeben VERFÜGBAR. Diese Funktion wurde aufgerufen, bevor Daten für alle gestreamte Parameter abgerufen wurde.<br /><br /> (DM) hieß die Funktion vor dem Aufruf **SQLPrepare**, **SQLExecDirect**, oder eine Katalogfunktion für die *StatementHandle*.<br /><br /> (DM) hieß eine asynchron ausgeführte Funktion (nicht auf dieses Objekt) für die *StatementHandle* und wurde noch ausgeführt werden, wenn diese Funktion aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oder **SQLSetPos** wurde aufgerufen, für die  *StatementHandle* und SQL_NEED_DATA zurückgegeben. Diese Funktion wurde aufgerufen, bevor die Daten für alle Data-at-Execution-Parameter oder Spalten gesendet wurden.|  
|HY013|Speicherverwaltungsfehler|Der Funktionsaufruf konnte nicht verarbeitet werden, da die zugrunde liegenden Speicherobjekte, möglicherweise aufgrund von unzureichendem Speicher konnte nicht zugegriffen werden.|  
|HY090|Ungültige Zeichenfolgen- oder Pufferlänge.|(DM)  *\*CharacterAttributePtr* ist eine Zeichenfolge und *Pufferlänge* war kleiner als 0, aber nicht SQL_NTS gleich.|  
|HY091|Ungültiger Deskriptorfeldbezeichner|Der Wert für das Argument angegebene *FieldIdentifier* war nicht das vorgegebenen Werten und kein Implementierung definierte Wert wurde.|  
|HY117|Verbindung wird aufgrund eines unbekannten Transaktionsstatus angehalten. Nur trennen, und nur-Lese Funktionen sind zulässig.|(DM) finden Sie weitere Informationen zum Zustand "angehalten" [SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Vom Treiber nicht unterstützt|Der Wert für das Argument angegebene *FieldIdentifier* wurde vom Treiber nicht unterstützt.|  
|HYT01|Verbindungstimeout abgelaufen|Das Verbindungstimeout ist abgelaufen, bevor die Datenquelle auf die Anforderung geantwortet hat. Das Verbindungstimeout wird über festgelegt **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Diese Funktion wird im Treiber nicht unterstützt.|(DM) der Treiber verknüpft sind, mit der *StatementHandle* der Funktion nicht unterstützt.|  
|IM017|Abrufintervall ist im Modus für asynchrone Benachrichtigung deaktiviert.|Sobald das Benachrichtigungsmodell verwendet wird, ist die Abruf deaktiviert.|  
|IM018|**SQLCompleteAsync** nicht zum Abschließen des vorherigen asynchrone Vorgangs auf diesem Handle aufgerufen wurde.|Wenn die vorherigen Funktionsaufruf auf das Handle SQL_STILL_EXECUTING zurückgibt und Benachrichtigungsmodus aktiviert ist, **SQLCompleteAsync** muss aufgerufen werden, auf das Handle nach der Verarbeitung und der Vorgang abgeschlossen werden.|  
  
 Wenn nach aufgerufen **SQLPrepare** und vor dem **SQLExecute**, **SQLColAttribute** zurückgeben kann eine beliebige SQLSTATE, die von zurückgegeben werden kann **SQLPrepare**oder **SQLExecute**, je nachdem, wenn die Datenquelle die zugeordnete SQL-Anweisung wertet den *StatementHandle*.  
  
 Aus Gründen der Leistung eine Anwendung sollte nicht aufrufen **SQLColAttribute** vor der Ausführung einer Anweisung.  
  
## <a name="comments"></a>Kommentare  
 Informationen zur Verwendung von Anwendungen zurückgegebene Informationen **SQLColAttribute**, finden Sie unter [Ergebnismetadaten festgelegt](../../../odbc/reference/develop-app/result-set-metadata.md).  
  
 **SQLColAttribute** gibt Informationen zurück, entweder in \* *NumericAttributePtr* oder im \* *CharacterAttributePtr*. Integer-Informationen werden zurückgegeben, \* *NumericAttributePtr* als SQLLEN-Wert; alle anderen Formate der Informationen zurückgegeben werden, \* *CharacterAttributePtr*. Bei Rückgabe Informationen \* *NumericAttributePtr*, ignoriert der Treiber *CharacterAttributePtr*, *Pufferlänge*, und  *StringLengthPtr*. Bei Rückgabe Informationen \* *CharacterAttributePtr*, ignoriert der Treiber *NumericAttributePtr*.  
  
 **SQLColAttribute** Werte aus den deskriptorfelder vom IRD zurückgegeben. Die Funktion wird mit einer Deskriptorhandles, anstatt ein Anweisungshandle aufgerufen. Die Rückgabewerte **SQLColAttribute** für die *FieldIdentifier* weiter unten in diesem Abschnitt aufgeführten Werte können auch durch den Aufruf abgerufen werden **SQLGetDescField** mit der entsprechende IRD-Handle.  
  
 Die aktuell definierten Descriptor-Felder, die Version von ODBC, in denen sie eingeführt wurden und in dem Informationen, für diese zurückgegeben werden Argumente werden weiter unten in diesem Abschnitt; Weitere Deskriptor Typen können von Treibern, die von verschiedenen Datenquellen nutzen definiert werden.  
  
 Eine ODBC-3. *x* Treiber muss einen Wert für jedes der deskriptorfelder zurück. Wenn ein Deskriptorfeld nicht für einen Treiber oder eine Datenquelle gilt und, sofern nichts anderes angegeben ist, der Treiber 0 in gibt \* *StringLengthPtr* oder eine leere Zeichenfolge in **CharacterAttributePtr*.  
  
## <a name="backward-compatibility"></a>Abwärtskompatibilität  
 Der ODBC-3. *x* Funktion **SQLColAttribute** ersetzt die veraltete ODBC 2. *X* Funktion **SQLColAttributes**. Bei der Zuordnung **SQLColAttributes** auf **SQLColAttribute** (bei einer ODBC 2. *X* Anwendung arbeitet mit einer ODBC-3. *X* Treiber), oder die Zuordnung **SQLColAttribute** auf **SQLColAttributes** (Wenn eine ODBC 3. *X* Anwendung arbeitet mit einer ODBC 2. *X* Treiber), der Treiber-Manager übergibt entweder den Wert des *FieldIdentifier* ordnet Sie diesen durch, um einen neuen Wert oder einen Fehler zurückgibt, wie folgt:  
  
> [!NOTE]  
>  Das Präfix *FieldIdentifier* Werte in ODBC 3. *X* wurde geändert, verwendet der 2 von ODBC. *X*. Das neue Präfix ist "SQL_DESC"; das alte Präfix wurde "SQL_COLUMN".  
  
-   Wenn die **#define** Wert von der ODBC 2. *X* *FieldIdentifier* ist identisch mit der **#define** Wert der ODBC-3. *X* *FieldIdentifier*, wird der Wert im Funktionsaufruf nur übergeben.  
  
-   Die **#define** Werte von der ODBC 2. *X* *FieldIdentifiers* SQL_COLUMN_LENGTH SQL_COLUMN_PRECISION und SQL_COLUMN_SCALE unterscheiden sich von der **#define** Werte von ODBC-3. *X* *FieldIdentifiers* SQL_DESC_SCALE, SQL_DESC_PRECISION und SQL_DESC_LENGTH. Eine ODBC-2. *x* Treiber muss nur die ODBC-2 unterstützt. *X* Werte. Eine ODBC-3. *x* -Treiber muss "SQL_COLUMN" und "SQL_DESC" Werte für diese drei unterstützen *FieldIdentifiers*. Diese Werte unterscheiden, da mit einfacher Genauigkeit, Dezimalstellen und Länge in ODBC 3. unterschiedlich definiert sind. *x* als in ODBC 2. waren. *X*. Weitere Informationen finden Sie unter [Spaltengröße, Dezimalstellen, Oktettlänge übertragen und Anzeigegröße](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).  
  
-   Wenn die **#define** Wert von der ODBC 2. *X* *FieldIdentifier* unterscheidet sich von der **#define** Wert der ODBC-3. *X* *FieldIdentifier*, der NULL zulässt, den Wert im Funktionsaufruf und dem entsprechenden Wert zugeordnet wird und wie mit der Anzahl, Namen, auftritt. Beispielsweise ist SQL_COLUMN_COUNT SQL_DESC_COUNT, zugeordnet und SQL_DESC_COUNT SQL_COLUMN_COUNT, je nach Richtung der Zuordnung zugeordnet ist.  
  
-   Wenn *FieldIdentifier* wird ein neuer Wert in ODBC 3. *X*, für die gab es keinen entsprechenden Wert in ODBC 2. *X*, wird es nicht zugeordnet werden, wenn eine ODBC 3. *X* Anwendung wird in einem Aufruf von **SQLColAttribute** in einer ODBC 2. *X* Treiber und der Aufruf SQLSTATE HY091 zurück (Ungültiger Deskriptorfeldbezeichner).  
  
 Die folgende Tabelle enthält die Deskriptor Typen zurückgegebenes **SQLColAttribute**. Der Typ für *NumericAttributePtr* Werte ist **SQLLEN \*** .  
  
|*FieldIdentifier*|Informationen<br /><br /> im zurückgegebenen|Description|  
|-----------------------|---------------------------------|-----------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE (ODBC 1.0)|*NumericAttributePtr*|SQL_TRUE, wenn die Spalte eine automatische Inkrementierung-Spalte ist.<br /><br /> SQL_FALSE, wenn die Spalte keine automatische Inkrementierung Spalte oder nicht numerisch ist.<br /><br /> Dieses Feld ist für numerische Spalten nur gültig. Eine Anwendung können Sie die Werte in eine Zeile mit einer Autoincrement-Spalte einfügen, jedoch Werte in der Spalte in der Regel kann nicht aktualisiert werden.<br /><br /> Wenn eine Einfügung in eine Autoincrement-Spalte ausgeführt wird, wird ein eindeutiger Wert zum Zeitpunkt des Einfügens in die Spalte eingefügt. Das Inkrement ist nicht definiert, aber Daten datenquellenspezifischen ist. Eine Anwendung sollte nicht davon ausgehen, dass eine Autoincrement-Spalte bei bestimmten Zeitpunkt kein(e) Inkremente ausnahmslos bestimmten startet.|  
|SQL_DESC_BASE_COLUMN_NAME (ODBC 3.0)|*CharacterAttributePtr*|Legen Sie für das Ergebnis der Name der Basisspalte Spalte ein. Wenn der Name der Basisspalte nicht (wie im Fall von Spalten, die Ausdrücke sind) vorhanden ist, enthält diese Variable eine leere Zeichenfolge.<br /><br /> Diese Informationen werden vom SQL_DESC_BASE_COLUMN_NAME-Datensatzfeld vom IRD zurückgegeben, die ein Feld schreibgeschützt ist.|  
|SQL_DESC_BASE_TABLE_NAME (ODBC 3.0)|*CharacterAttributePtr*|Der Name der Basistabelle, die die Spalte enthält. Wenn der Name der Basistabelle kann nicht definiert werden oder nicht anwendbar ist, enthält diese Variable eine leere Zeichenfolge.<br /><br /> Diese Informationen werden vom SQL_DESC_BASE_TABLE_NAME-Datensatzfeld vom IRD zurückgegeben, die ein Feld schreibgeschützt ist.|  
|SQL_DESC_CASE_SENSITIVE (ODBC 1.0)|*NumericAttributePtr*|SQL_TRUE, wenn die Spalte als Groß-/Kleinschreibung für Sortierungen und Vergleiche behandelt wird.<br /><br /> SQL_FALSE, wenn die Spalte nicht, wie Groß-/Kleinschreibung für Sortierungen und Vergleiche behandelt wird oder nicht auf Zeichen basierende ist.|  
|SQL_DESC_CATALOG_NAME (ODBC 2.0)|*CharacterAttributePtr*|Der Katalog der Tabelle, die die Spalte enthält. Der zurückgegebene Wert ist die Implementierung definiertes, wenn die Spalte ein Ausdruck ist, oder wenn die Spalte Teil einer Ansicht ist. Wenn die Datenquelle keine Kataloge unterstützt oder der Name des Katalogs kann nicht bestimmt werden, ist eine leere Zeichenfolge zurückgegeben. Dieses Feld der VARCHAR-Datensatz ist nicht auf 128 Zeichen beschränkt.|  
|SQL_DESC_CONCISE_TYPE (ODBC 1.0)|*NumericAttributePtr*|Der Datentyp präziser.<br /><br /> Für die Datentypen "DateTime" und das Intervall gibt dieses Feld den präzisen Datentyp zurück. z. B. SQL_TYPE_TIME oder SQL_INTERVAL_YEAR. (Weitere Informationen finden Sie unter [-datentypbezeichnungen und Deskriptoren](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md) in Anhang D:-Datentypen.)<br /><br /> Diese Informationen werden vom SQL_DESC_CONCISE_TYPE-Datensatzfeld vom IRD zurückgegeben.|  
|SQL_DESC_COUNT (ODBC 1.0)|*NumericAttributePtr*|Die Anzahl der Spalten im Resultset verfügbar sind. Dies gibt 0 zurück, wenn keine Spalten im Resultset vorhanden sind. Der Wert in der *ColumnNumber* Argument wird ignoriert.<br /><br /> Diese Informationen werden aus der SQL_DESC_COUNT-Headerfeld vom IRD zurückgegeben.|  
|SQL_DESC_DISPLAY_SIZE (ODBC 1.0)|*NumericAttributePtr*|Maximale Anzahl von Zeichen erforderlich sind, um Daten aus der Spalte anzuzeigen. Weitere Informationen zur Anzeigegröße finden Sie unter [Spaltengröße, Dezimalstellen, Oktettlänge übertragen und Größe anzeigen](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) in Anhang D:-Datentypen.|  
|SQL_DESC_FIXED_PREC_SCALE (ODBC 1.0)|*NumericAttributePtr*|SQL_TRUE, wenn die Spalte weist eine feste Genauigkeit und Dezimalstellen ungleich NULL, die Datenquelle spezifischen enthalten.<br /><br /> SQL_FALSE, wenn die Spalte keiner mit fester Genauigkeit und festen Dezimalstellen ungleich NULL, die Datenquelle spezifischen enthalten.|  
|SQL_DESC_LABEL (ODBC 2.0)|*CharacterAttributePtr*|Die spaltenbezeichnung oder die Titelleiste. Z. B. eine Spalte mit dem Namen EmpName möglicherweise Mitarbeiternamen Beschriftung oder mit einem Alias gekennzeichnet werden kann.<br /><br /> Wenn eine Spalte nicht über eine Bezeichnung verfügt, wird der Spaltenname zurückgegeben. Wenn die Spalte ohne Beschriftung und nicht benannt ist, wird eine leere Zeichenfolge zurückgegeben.|  
|SQL_DESC_LENGTH (ODBC 3.0)|*NumericAttributePtr*|Geben Sie einen numerischen Wert, der entweder die maximale oder tatsächlichen Zeichenlänge von Zeichendaten Zeichenfolgen- oder Binärdatentyps. Es ist die maximale Zeichenlänge für einen Datentyp mit fester Länge oder die tatsächliche Zeichenlänge für einen Datentyp mit variabler Länge. Der Wert schließt immer das Null-Terminierung Byte, das die Zeichenfolge endet.<br /><br /> Diese Informationen werden vom SQL_DESC_LENGTH-Datensatzfeld vom IRD zurückgegeben.<br /><br /> Weitere Informationen zu Länge, finden Sie unter [Spaltengröße, Dezimalstellen, Oktettlänge übertragen und Anzeigegröße](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) in Anhang D:-Datentypen.|  
|SQL_DESC_LITERAL_PREFIX (ODBC 3.0)|*CharacterAttributePtr*|Diese VARCHAR(128) Datensatzfeld enthält das Zeichen oder Zeichen, die der Treiber als Präfix für ein Literal dieses Datentyps erkennt. Dieses Feld enthält eine leere Zeichenfolge für einen Datentyp für den ein Zeichenfolgenliteral-Präfix nicht anwendbar ist. Weitere Informationen finden Sie unter [Literal Präfixe und Suffixe](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md).|  
|SQL_DESC_LITERAL_SUFFIX (ODBC 3.0)|*CharacterAttributePtr*|Diese VARCHAR(128) Datensatzfeld enthält das Zeichen oder Zeichen, die der Treiber als Suffix für ein Literal dieses Datentyps erkennt. Dieses Feld enthält eine leere Zeichenfolge für einen Datentyp für den ein literales Suffix nicht anwendbar ist. Weitere Informationen finden Sie unter [Literal Präfixe und Suffixe](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md).|  
|SQL_DESC_LOCAL_TYPE_NAME (ODBC 3.0)|*CharacterAttributePtr*|Diese VARCHAR(128) Datensatzfeld enthält einen beliebigen Namen lokalisierte (native Language) für den Datentyp, der sich vom Namen des Datentyps reguläre sein kann. Wenn kein lokalisierter Name vorhanden ist, wird eine leere Zeichenfolge zurückgegeben. Dieses Feld ist nur zu Anzeigezwecken. Der Zeichensatz der Zeichenfolge ist vom Gebietsschema abhängiges und in der Regel der Standardzeichensatz des Servers.|  
|SQL_DESC_NAME (ODBC 3.0)|*CharacterAttributePtr*|Der Spaltenalias, sofern zutreffend. Wenn der Spaltenalias nicht anwendbar ist, wird der Spaltenname zurückgegeben. In beiden Fällen wird SQL_DESC_UNNAMED auf SQL_NAMED festgelegt. Wenn Sie keinen Spaltennamen oder Spaltenalias vorhanden ist, wird eine leere Zeichenfolge zurückgegeben, und SQL_DESC_UNNAMED SQL_UNNAMED Wert.<br /><br /> Diese Informationen werden vom SQL_DESC_NAME-Datensatzfeld vom IRD zurückgegeben.|  
|SQL_DESC_NULLABLE (ODBC 3.0)|*NumericAttributePtr*|SQL_ NULL-Werte zulässt, wenn die Spalte NULL-Werte aufweisen darf; SQL_NO_NULLS, wenn die Spalte keinen NULL-Werte; oder SQL_NULLABLE_UNKNOWN, wenn nicht bekannt ist, ob die Spalte NULL-Werte annimmt.<br /><br /> Diese Informationen werden vom SQL_DESC_NULLABLE-Datensatzfeld vom IRD zurückgegeben.|  
|SQL_DESC_NUM_PREC_RADIX (ODBC 3.0)|*NumericAttributePtr*|Wenn der Datentyp im Feld SQL_DESC_TYPE einen ungefähren numerischen Datentyp ist, enthält dieses SQLINTEGER-Feld den Wert 2, weil das SQL_DESC_PRECISION-Feld die Anzahl der Bits enthält. Wenn der Datentyp im Feld SQL_DESC_TYPE einen exakten numerischen Datentyp ist, enthält dieses Feld einen Wert von 10, weil das SQL_DESC_PRECISION-Feld die Anzahl von Dezimalstellen enthält. Dieses Feld ist für alle nicht-numerische Datentypen auf 0 festgelegt.|  
|SQL_DESC_OCTET_LENGTH (ODBC 3.0)|*NumericAttributePtr*|Die Länge in Bytes, der einen Zeichendatentyp Zeichenfolgen- oder Binärdatentyps. Für Zeichen fester Länge oder binary-Typen ist dies die tatsächliche Länge in Bytes. Für variabler Länge Zeichen- oder Binärdatentypen ist dies die maximale Länge in Bytes. Dieser Wert umfasst nicht den null-Terminator.<br /><br /> Diese Informationen werden vom SQL_DESC_OCTET_LENGTH-Datensatzfeld vom IRD zurückgegeben.<br /><br /> Weitere Informationen zu Länge, finden Sie unter [Spaltengröße, Dezimalstellen, Oktettlänge übertragen und Anzeigegröße](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) in Anhang D:-Datentypen.|  
|SQL_DESC_PRECISION (ODBC 3.0)|*NumericAttributePtr*|Ein numerischer Wert, der für einen numerischen Datentyp anwendbare Genauigkeit kennzeichnet. Bei allen Datentypen SQL_TYPE_TIME SQL_TYPE_TIMESTAMP, und alle Interval-Datentypen, die ein Zeitintervall, dessen Wert darstellen, ist die anwendbaren Genauigkeit der Sekundenbruchteil-Komponente.<br /><br /> Diese Informationen werden vom SQL_DESC_PRECISION-Datensatzfeld vom IRD zurückgegeben.|  
|SQL_DESC_SCALE (ODBC 3.0)|*NumericAttributePtr*|Ein numerischer Wert, der die entsprechenden Dezimalstellen für einen numerischen Datentyp ist. Für die Datentypen DECIMAL und NUMERIC ist dies die definierten Anzahl von Dezimalstellen an. Es ist nicht für alle anderen Datentypen definiert.<br /><br /> Diese Informationen werden vom Skalierung-Datensatzfeld vom IRD zurückgegeben.|  
|SQL_DESC_SCHEMA_NAME (ODBC 2.0)|*CharacterAttributePtr*|Das Schema der Tabelle, die die Spalte enthält. Der zurückgegebene Wert ist die Implementierung definiertes, wenn die Spalte ein Ausdruck ist, oder wenn die Spalte Teil einer Ansicht ist. Wenn die Datenquelle keine Schemas unterstützt oder der Schemaname kann nicht bestimmt werden, ist eine leere Zeichenfolge zurückgegeben. Dieses Feld der VARCHAR-Datensatz ist nicht auf 128 Zeichen beschränkt.|  
|SQL_DESC_SEARCHABLE (ODBC 1.0)|*NumericAttributePtr*|SQL_PRED_NONE, wenn die Spalte in einer WHERE-Klausel verwendet werden kann. (Dies ist identisch mit der SQL_UNSEARCHABLE-Wert in ODBC 2. *x*.)<br /><br /> SQL_PRED_CHAR, ob die Spalte in einer WHERE-Klausel jedoch nur mit dem LIKE-Prädikat verwendet werden kann. (Dies ist identisch mit der SQL_LIKE_ONLY-Wert in ODBC 2. *x*.)<br /><br /> SQL_PRED_BASIC, ob die Spalte in einer WHERE-Klausel mit allen Vergleichsoperatoren mit Ausnahme von LIKE verwendet werden kann. (Dies ist identisch mit der SQL_EXCEPT_LIKE-Wert in ODBC 2. *x*.)<br /><br /> SQL_PRED_SEARCHABLE, ob die Spalte in einer WHERE-Klausel mit jedem Vergleichsoperator verwendet werden kann.<br /><br /> Spalten vom Datentyp SQL_LONGVARCHAR und SQL_LONGVARBINARY normalerweise return SQL_PRED_CHAR.|  
|SQL_DESC_TABLE_NAME (ODBC 2.0)|*CharacterAttributePtr*|Der Name der Tabelle, die die Spalte enthält. Der zurückgegebene Wert ist die Implementierung definiertes, wenn die Spalte ein Ausdruck ist, oder wenn die Spalte Teil einer Ansicht ist.<br /><br /> Wenn der Tabellenname nicht bestimmt werden kann, ist eine leere Zeichenfolge zurückgegeben.|  
|SQL_DESC_TYPE (ODBC 3.0)|*NumericAttributePtr*|Ein numerischer Wert, der angibt, den SQL-Datentyp.<br /><br /> Wenn *ColumnNumber* ist gleich 0 ist, wird SQL_BINARY für Lesezeichen variabler Länge zurückgegeben und SQL_INTEGER für Lesezeichen fester Länge ist.<br /><br /> Dieses Feld gibt den ausführlichen Datentyp für die Datentypen "DateTime" und das Intervall zurück: SQL_DATETIME oder SQL_INTERVAL. (Weitere Informationen finden Sie unter [-datentypbezeichnungen und Deskriptoren](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md) in Anhang D:-Datentypen.<br /><br /> Diese Informationen werden vom SQL_DESC_TYPE-Datensatzfeld vom IRD zurückgegeben. **Hinweis:** für ODBC 2. funktioniert. *X* Treiber, verwenden Sie stattdessen SQL_DESC_CONCISE_TYPE.|  
|SQL_DESC_TYPE_NAME (ODBC 1.0)|*CharacterAttributePtr*|Data Source – abhängiger Datentypname; "z. B. CHAR", "VARCHAR", "MONEY", "LONG VARBINARY" oder "CHAR () für BIT-Daten".<br /><br /> Wenn der Typ unbekannt ist, wird eine leere Zeichenfolge zurückgegeben.|  
|SQL_DESC_UNNAMED (ODBC 3.0)|*NumericAttributePtr*|SQL_NAMED oder SQL_UNNAMED. Wenn vom IRD SQL_DESC_NAME-Felds einen Spaltenalias oder einen Spaltennamen enthält, wird SQL_NAMED zurückgegeben. Wenn keine Spaltennamen oder Spaltenalias vorhanden ist, wird SQL_UNNAMED zurückgegeben.<br /><br /> Diese Informationen werden vom SQL_DESC_UNNAMED-Datensatzfeld vom IRD zurückgegeben.|  
|SQL_DESC_UNSIGNED (ODBC 1.0)|*NumericAttributePtr*|SQL_TRUE, wenn die Spalte ohne Vorzeichen (oder nicht numerische) ist.<br /><br /> SQL_FALSE, wenn die Spalte signiert ist.|  
|SQL_DESC_UPDATABLE (ODBC 1.0)|*NumericAttributePtr*|Spalte wird von den Werten der definierten Konstanten beschrieben:<br /><br /> SQL_ATTR_READONLY SQL_ATTR_WRITE SQL_ATTR_READWRITE_UNKNOWN<br /><br /> SQL_DESC_UPDATABLE beschreibt die aktualisierbarkeit der Spalte im Resultset, nicht die Spalte in der Basistabelle. Möglicherweise ungleich dem Wert in diesem Feld die aktualisierbarkeit der Basisspalte auf der Resultset-Spalte basiert. Ob eine Spalte aktualisiert werden kann, kann auf den Datentyp, Benutzerberechtigungen und die Definition des Resultsets selbst basieren. Wenn unklar ist, ob eine Spalte aktualisiert werden kann, sollte SQL_ATTR_READWRITE_UNKNOWN zurückgegeben werden.|  
  
 **SQLColAttribute** ist eine erweiterbare Alternative zum **SQLDescribeCol**. **SQLDescribeCol** gibt einen festen Satz von Deskriptorinformationen basierend auf ANSI-89 SQL. **SQLColAttribute** ermöglicht den Zugriff auf den umfangreicheren Reihe von Deskriptorinformationen in ANSI SQL-92 und DBMS-herstellererweiterungen verfügbar.  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Binden einen Puffer, an eine Spalte in einem Resultset|[SQLBindCol-Funktion](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Anweisungsverarbeitung Abbrechen|[SQLCancel-Funktion](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Zurückgeben von Informationen zu einer Spalte in einem Resultset|[SQLDescribeCol-Funktion](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|Abrufen eines Zeilenblocks von Daten oder einen Bildlauf durch die ein Ergebnis festlegen|[SQLFetchScroll-Funktion](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Das Abrufen mehrerer Datenzeilen|[SQLFetch-Funktion](../../../odbc/reference/syntax/sqlfetch-function.md)|  
  
## <a name="example"></a>Beispiel  
 Der folgende Beispielcode gibt keine Handles und Verbindungen frei. Finden Sie unter [SQLFreeHandle-Funktion](../../../odbc/reference/syntax/sqlfreehandle-function.md), [ODBC-Beispielprogramm](../../../odbc/reference/sample-odbc-program.md), und [SQLFreeStmt-Funktion](../../../odbc/reference/syntax/sqlfreestmt-function.md) für Codebeispiele Handles und Anweisungen frei.  
  
```  
// SQLColAttibute.cpp  
// compile with: user32.lib odbc32.lib  
  
#define UNICODE  
  
#include <windows.h>  
#include <sqlext.h>  
#include <strsafe.h>  
  
struct DataBinding {  
   SQLSMALLINT TargetType;  
   SQLPOINTER TargetValuePtr;  
   SQLINTEGER BufferLength;  
   SQLLEN StrLen_or_Ind;  
};  
  
void printStatementResult(SQLHSTMT hstmt) {  
   int bufferSize = 1024, i;  
   SQLRETURN retCode;  
   SQLSMALLINT numColumn = 0, bufferLenUsed;  
   SQLPOINTER* columnLabels = (SQLPOINTER *)malloc( numColumn * sizeof(SQLPOINTER*) );  
   struct DataBinding* columnData = (struct DataBinding*)malloc( numColumn * sizeof(struct DataBinding) );  
  
   retCode = SQLNumResultCols(hstmt, &numColumn);  
  
   printf( "Columns from that table:\n" );  
   for ( i = 0 ; i < numColumn ; i++ ) {  
      columnLabels[i] = (SQLPOINTER)malloc( bufferSize*sizeof(char) );  
  
      retCode = SQLColAttribute(hstmt, (SQLUSMALLINT)i + 1, SQL_DESC_LABEL, columnLabels[i], (SQLSMALLINT)bufferSize, &bufferLenUsed, NULL);  
      wprintf( L"Column %d: %s\n", i, (wchar_t*)columnLabels[i] );  
   }  
  
   // allocate memory for the binding  
   for ( i = 0 ; i < numColumn ; i++ ) {  
      columnData[i].TargetType = SQL_C_CHAR;  
      columnData[i].BufferLength = (bufferSize+1);  
      columnData[i].TargetValuePtr = malloc( sizeof(unsigned char)*columnData[i].BufferLength );  
   }  
  
   // setup the binding   
   for ( i = 0 ; i < numColumn ; i++ ) {  
      retCode = SQLBindCol(hstmt, (SQLUSMALLINT)i + 1, columnData[i].TargetType,   
         columnData[i].TargetValuePtr, columnData[i].BufferLength, &(columnData[i].StrLen_or_Ind));  
   }  
  
   printf( "Data from that table:\n" );  
   // fetch the data and print out the data  
   for ( retCode = SQLFetch(hstmt) ; retCode == SQL_SUCCESS || retCode == SQL_SUCCESS_WITH_INFO ; retCode = SQLFetch(hstmt) ) {  
      int j;  
      for ( j = 0 ; j < numColumn ; j++ )  
         wprintf( L"%s: %hs\n", columnLabels[j], columnData[j].TargetValuePtr );  
      printf( "\n" );  
   }  
   printf( "\n" );   
}  
  
int main() {  
   int bufferSize = 1024, i, count = 1, numCols = 5;  
   wchar_t firstTableName[1024], * dbName = (wchar_t *)malloc( sizeof(wchar_t)*bufferSize ), * userName = (wchar_t *)malloc( sizeof(wchar_t)*bufferSize );  
   HWND desktopHandle = GetDesktopWindow();   // desktop's window handle  
   SQLWCHAR connStrbuffer[1024];  
   SQLSMALLINT connStrBufferLen, bufferLen;  
   SQLRETURN retCode;  
  
   SQLHENV henv = NULL;   // Environment     
   SQLHDBC hdbc = NULL;   // Connection handle  
   SQLHSTMT hstmt = NULL;   // Statement handle  
  
   struct DataBinding* catalogResult = (struct DataBinding*) malloc( numCols * sizeof(struct DataBinding) );  
   SQLWCHAR* selectAllQuery = (SQLWCHAR *)malloc( sizeof(SQLWCHAR) * bufferSize );  
  
   // connect to database  
   retCode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retCode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLCHAR *)(void*)SQL_OV_ODBC3, -1);  
   retCode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
   retCode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)10, 0);  
   retCode = SQLDriverConnect(hdbc, desktopHandle, L"Driver={SQL Server}", SQL_NTS, connStrbuffer, 1025, &connStrBufferLen, SQL_DRIVER_PROMPT);  
   retCode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   // display the database information  
   retCode = SQLGetInfo(hdbc, SQL_DATABASE_NAME, dbName, (SQLSMALLINT)bufferSize, (SQLSMALLINT *)&bufferLen);  
   retCode = SQLGetInfo(hdbc, SQL_USER_NAME, userName, (SQLSMALLINT)bufferSize, &bufferLen);  
  
   for ( i = 0 ; i < numCols ; i++ ) {  
      catalogResult[i].TargetType = SQL_C_CHAR;  
      catalogResult[i].BufferLength = (bufferSize + 1);  
      catalogResult[i].TargetValuePtr = malloc( sizeof(unsigned char)*catalogResult[i].BufferLength );  
   }  
  
   // Set up the binding. This can be used even if the statement is closed by closeStatementHandle  
   for ( i = 0 ; i < numCols ; i++ )  
      retCode = SQLBindCol(hstmt, (SQLUSMALLINT)i + 1, catalogResult[i].TargetType, catalogResult[i].TargetValuePtr, catalogResult[i].BufferLength, &(catalogResult[i].StrLen_or_Ind));  
  
   retCode = SQLTables( hstmt, (SQLWCHAR*)SQL_ALL_CATALOGS, SQL_NTS, L"", SQL_NTS, L"", SQL_NTS, L"", SQL_NTS );  
   retCode = SQLFreeStmt(hstmt, SQL_CLOSE);  
  
   retCode = SQLTables( hstmt, dbName, SQL_NTS, userName, SQL_NTS, L"%", SQL_NTS, L"TABLE", SQL_NTS );  
  
   for ( retCode = SQLFetch(hstmt) ; retCode == SQL_SUCCESS || retCode == SQL_SUCCESS_WITH_INFO ; retCode = SQLFetch(hstmt), ++count )  
      if ( count == 1 )  
         StringCchPrintfW( firstTableName, 1024, L"%hs", catalogResult[2].TargetValuePtr );  
   retCode = SQLFreeStmt(hstmt, SQL_CLOSE);  
  
   wprintf( L"Select all data from the first table (%s)\n", firstTableName );  
   StringCchPrintfW( selectAllQuery, bufferSize, L"SELECT * FROM %s", firstTableName );  
  
   retCode = SQLExecDirect(hstmt, selectAllQuery, SQL_NTS);  
   printStatementResult(hstmt);  
}  
```  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)   
 [ODBC-Beispielprogramm](../../../odbc/reference/sample-odbc-program.md)

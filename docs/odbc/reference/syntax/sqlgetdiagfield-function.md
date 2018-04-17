---
title: SQLGetDiagField-Funktion | Microsoft Docs
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
- SQLGetDiagField
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetDiagField
helpviewer_keywords:
- SQLGetDiagField function [ODBC]
ms.assetid: 1dbc4398-97a8-4585-bb77-1f7ea75e24c4
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f337b8455ba860caaf5e4a5b1bd4be1d0ee86c37
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sqlgetdiagfield-function"></a>SQLGetDiagField-Funktion
**Konformität**  
 Version eingeführt: ODBC 3.0 Standardkonformität: ISO-92  
  
 **Zusammenfassung**  
 **SQLGetDiagField** gibt den aktuellen Wert eines Felds eines Datensatzes, der die Diagnosedaten-Struktur (mit einem angegebenen Handle zugeordnete), die Fehler, Warnung und Statusinformationen enthält.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLGetDiagField(  
     SQLSMALLINT     HandleType,  
     SQLHANDLE       Handle,  
     SQLSMALLINT     RecNumber,  
     SQLSMALLINT     DiagIdentifier,  
     SQLPOINTER      DiagInfoPtr,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   StringLengthPtr);  
```  
  
## <a name="arguments"></a>Argumente  
 *HandleType*  
 [Eingabe] Ein Bezeichner der Handle-Typ, der den Typ des Handles wird beschrieben, für die Diagnose erforderlich sind. Dies muss eine der folgenden Ressourcen sein:  
  
-   SQL_HANDLE_DBC AUF  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV AUF  
  
-   SQL_HANDLE_STMT AUF  
  
 SQL_HANDLE_DBC_INFO_TOKEN Handle wird nur durch das Treiber-Manager und Treiber verwendet. Anwendungen sollten diese Handletyp nicht verwenden. Weitere Informationen zu SQL_HANDLE_DBC_INFO_TOKEN, finden Sie unter [entwickeln Verbindungspool wissen in eine ODBC-Treiber](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).  
  
 *Handle*  
 [Eingabe] Ein Handle für die Diagnosedaten-Struktur, die vom angegebenen Typ *HandleType*. Wenn *HandleType* SQL_HANDLE_ENV auf, wird *behandeln* können eine freigegebene oder ein Umgebungshandle aufgehoben werden.  
  
 *RecNumber*  
 [Eingabe] Gibt den Status-Datensatz aus dem die Anwendung Informationen Suchvorgängen an. Statusdatensätze werden von 1 nummeriert. Wenn die *DiagIdentifier* Argument gibt ein Feld des Diagnose-Headers an *RecNumber* wird ignoriert. Wenn dies nicht der Fall ist, sollte größer als 0 sein.  
  
 *DiagIdentifier*  
 [Eingabe] Gibt das Feld der Diagnose, deren Wert zurückgegeben werden. Weitere Informationen finden Sie unter der "*DiagIdentifier* Argument" im Abschnitt "Kommentare".  
  
 *DiagInfoPtr*  
 [Ausgabe] Zeiger auf einen Puffer, in dem die Diagnoseinformationen zurückgegeben. Der Datentyp hängt vom Wert der *DiagIdentifier*. Wenn *DiagInfoPtr* ein Ganzzahltyp ist, Anwendungen einen Puffer von SQLULEN sollte verwendet werden, und initialisieren, die der Wert auf 0 vor dem Aufrufen dieser Funktion können als einige Treiber kann nur die unteren 32-Bit- oder 16-Bit-eines Puffers zu schreiben und lassen Sie die höherer Ordnung Bit unverändert.  
  
 Wenn *DiagInfoPtr* NULL ist, *StringLengthPtr* weiterhin die Gesamtanzahl der Bytes (ausgenommen die Null-Terminierung Zeichen für Zeichendaten) zurück in den Puffer verweist zurückzugebendenverfügbar *DiagInfoPtr*.  
  
 *Pufferlänge*  
 [Eingabe] Wenn *DiagIdentifier* ist ein ODBC-definierten Diagnose- und *DiagInfoPtr* zeigt auf eine Zeichenfolge oder einen binären Puffer, in dieses Argument muss die Länge des \* *DiagInfoPtr* . Wenn *DiagIdentifier* ist ein ODBC-definierten Feld und \* *DiagInfoPtr* ist eine ganze Zahl *Pufferlänge* wird ignoriert. Wenn der Wert in  *\*DiagInfoPtr* eine Unicode-Zeichenfolge (beim Aufrufen von **SQLGetDiagFieldW**), wird die *Pufferlänge* Argument muss eine gerade Zahl sein.  
  
 Wenn *DiagIdentifier* ist ein Feld treiberdefinierten die Anwendung zeigt die Art des Felds um den Treiber-Manager an, indem die *Pufferlänge* Argument. *Pufferlänge* können die folgenden Werte aufweisen:  
  
-   Wenn *DiagInfoPtr* ist ein Zeiger auf eine Zeichenfolge *Pufferlänge* ist die Länge der Zeichenfolge oder SQL_NTS.  
  
-   Wenn *DiagInfoPtr* ist ein Zeiger auf einen binären Puffer, der Anwendung stellen das Ergebnis der SQL_LEN_BINARY_ATTR (*Länge*)-Makro im *Pufferlänge*. Dies setzt einen negativen Wert in *Pufferlänge*.  
  
-   Wenn *DiagInfoPtr* ist ein Zeiger auf einen anderen Wert als eine Zeichenfolge oder Binärzeichenfolge, *Pufferlänge* müssen den Wert SQL_IS_POINTER.  
  
-   Wenn  *\*DiagInfoPtr* enthält einen Datentyp mit fester Länge *Pufferlänge* SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT oder SQL_IS_USMALLINT, nach Bedarf ist.  
  
 *StringLengthPtr*  
 [Ausgabe] Zeiger auf einen Puffer, in dem die Gesamtanzahl der Bytes (ausgenommen die Anzahl der Bytes, die erforderlich sind, für die Null-Abschlusszeichen) zurückgegeben verfügbar im zurückzugebenden \* *DiagInfoPtr*, für Zeichendaten. Wenn die Anzahl der Bytes, die für die Rückgabe verfügbar, größer als oder gleich ist *Pufferlänge*, den Text im \* *DiagInfoPtr* auf abgeschnitten *Pufferlänge* minus die Länge des ein Null-Abschlusszeichen.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE oder SQL_NO_DATA zurückgibt.  
  
## <a name="diagnostics"></a>Diagnose  
 **SQLGetDiagField** DiagnoseDatensätze für sich selbst wird nicht gesendet. Er verwendet die folgenden Rückgabewerte, um das Ergebnis der eigenen Ausführung melden:  
  
-   SQL_SUCCESS: Die Funktion wurde erfolgreich zurückgegeben Diagnoseinformationen.  
  
-   SQL_SUCCESS_WITH_INFO: \* *DiagInfoPtr* war zu klein für die angeforderte diagnostic-Feld enthalten. Aus diesem Grund wurden die Daten im Feld diagnostische abgeschnitten. Um zu ermitteln, die einen abgeschnittenen Daten, die Anwendung muss vergleichen *Pufferlänge* auf die tatsächliche Anzahl von Bytes verfügbar ist, die in geschrieben wird **StringLengthPtr*.  
  
-   SQL_INVALID_HANDLE: Das Handle erkennbar *HandleType* und *behandeln* war es sich nicht um ein gültiges Handle.  
  
-   SQL_ERROR: Eine der folgenden aufgetreten ist:  
  
    -   *Die DiagIdentifier* Argument war nicht der gültigen Werte.  
  
    -   *Die DiagIdentifier* Argument war SQL_DIAG_CURSOR_ROW_COUNT, SQL_DIAG_DYNAMIC_FUNCTION, SQL_DIAG_DYNAMIC_FUNCTION_CODE oder SQL_DIAG_ROW_COUNT, aber *behandeln* war es sich nicht um ein Anweisungshandle. (Der Treiber-Manager gibt dies diagnostische.)  
  
    -   *Die RecNumber* Argument war negativ oder 0 Wenn *DiagIdentifier* ein Feld aus einem Diagnosedatensatz angegeben. *RecNumber* für Headerfelder ignoriert wird.  
  
    -   Der Wert, der angefordert wurde, eine Zeichenfolge und *Pufferlänge* war kleiner als 0 (null).  
  
    -   Wenn Sie die asynchrone Benachrichtigung verwenden zu können, war der asynchrone Vorgang auf das Handle nicht abgeschlossen werden.  
  
-   SQL_NO_DATA: *RecNumber* war größer als die Zahl der DiagnoseDatensätze, die für das Handle im angegebenen vorhanden waren *behandeln.* Die Funktion gibt SQL_NO_DATA auch für eine beliebige positive Werte *RecNumber* treten keine DiagnoseDatensätze für *behandeln*.  
  
## <a name="comments"></a>Kommentare  
 Ruft eine Anwendung in der Regel **SQLGetDiagField** um eines der drei Ziele zu erreichen:  
  
1.  Bestimmte Fehler oder Warnungsinformationen abrufen, wenn ein Funktionsaufruf SQL_ERROR oder SQL_SUCCESS_WITH_INFO zurückgegeben hat (oder SQL_NEED_DATA zurück, für die **SQLBrowseConnect** Funktion).  
  
2.  Um die Anzahl der Zeilen in der Datenquelle zu ermitteln, die betroffen sind, wenn mit einem Aufruf von INSERT-, DELETE- oder Update-Vorgänge ausgeführt wurden **SQLExecute**, **SQLExecDirect**,  **SQLBulkOperations**, oder **SQLSetPos** (aus der SQL_DIAG_ROW_COUNT-Headerfeld), oder die Anzahl der Zeilen, die in der aktuellen geöffneten Cursor vorhanden ermitteln möchten, wenn der Treiber diese Informationen nicht bereitstellen kann (aus der SQL_DIAG_CURSOR_ROW_COUNT-Headerfeld).  
  
3.  Um zu bestimmen, welche Funktion durch einen Aufruf ausgeführt wurde **SQLExecDirect** oder **SQLExecute** (von Headerfelder SQL_DIAG_DYNAMIC_FUNCTION und SQL_DIAG_DYNAMIC_FUNCTION_CODE).  
  
 Eine ODBC-Funktion veröffentlichen kann 0 (null) oder mehrere DiagnoseDatensätze jedes Mal, wenn die It aufgerufen wird, damit eine Anwendung aufrufen kann **SQLGetDiagField** nach einem beliebigen ODBC-Funktionsaufruf. Es gibt keine Beschränkung der Anzahl der DiagnoseDatensätze, die jeweils gespeichert werden können. **SQLGetDiagField** ruft nur die zuletzt zugeordnete die Diagnosedaten-Struktur, die im angegebenen Diagnoseinformationen der *behandeln* Argument. Wenn die Anwendung eine ODBC-Funktion, außer aufruft **SQLGetDiagField** oder **SQLGetDiagRec**, Diagnoseinformationen aus einem vorherigen Aufruf mit dem gleichen Handle geht verloren.  
  
 Eine Anwendung kann alle DiagnoseDatensätze durch inkrementieren Scannen *RecNumber*, solange **SQLGetDiagField** gibt SQL_SUCCESS zurück. Die Anzahl der Statusdatensätze wird in das SQL_DIAG_NUMBER-Headerfeld angegeben. Aufrufe von **SQLGetDiagField** sind für die Header und Datensatz zerstörerisch. Die Anwendung kann Aufrufen **SQLGetDiagField** später noch einmal, um ein Feld aus einem Datensatz abzurufen, solange eine Funktion als den Diagnosefunktionen nicht in der Zwischenzeit aufgerufen wurde die Datensätze auf dasselbe Handle bereitstellen möchten.  
  
 Eine Anwendung kann Aufrufen **SQLGetDiagField** zurückzugebenden jedes diagnostische Feld zu einem beliebigen Zeitpunkt, mit Ausnahme von SQL_DIAG_CURSOR_ROW_COUNT oder SQL_DIAG_ROW_COUNT, die SQL_ERROR zurückgegeben wird, wenn *behandeln* ist kein Anweisungshandle. Wenn ein anderes diagnostische Feld definiert, wird der Aufruf von **SQLGetDiagField** gibt SQL_SUCCESS zurück, (vorausgesetzt, dass keine anderen Diagnose gefunden wird) und für das Feld ein nicht definierter Wert zurückgegeben.  
  
 Weitere Informationen finden Sie unter [mithilfe SQLGetDiagRec und SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md) und [implementieren SQLGetDiagRec und SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md).  
  
 Aufrufen einer API als dem, der asynchron ausgeführt wird, wird HY010 generieren "Function Sequenzfehler". Error-Datensatzes kann allerdings abgerufen werden, bevor der asynchrone Vorgang abgeschlossen ist.  
  
## <a name="handletype-argument"></a>HandleType-Argument  
 Jede Handletyp kann Diagnoseinformationen zugeordnet haben. Die *HandleType* Argument gibt den Handletyp des an *behandeln*.  
  
 Einige Felder "Header" und "Datensatz können für die Umgebung, Verbindung, anweisungs- und Deskriptorstatuswerte Handles zurückgegeben werden. Diese Handles, die für die ein Feld nicht anwendbar ist, werden in den Abschnitten "Headerfelder" und "Datensatzfelder", die nach angezeigt.  
  
 Wenn *HandleType* SQL_HANDLE_ENV auf, wird *behandeln* freigegeben werden oder nicht freigegebene Umgebungshandle werden können.  
  
 Keine Header treiberspezifische Diagnosefelder sollte ein Umgebungshandle zugeordnet werden.  
  
 Nur Diagnose Headerfelder, die für eine Deskriptorhandles definiert sind, sind SQL_DIAG_NUMBER und SQL_DIAG_RETURNCODE.  
  
## <a name="diagidentifier-argument"></a>DiagIdentifier-Argument  
 Dieses Argument gibt den Bezeichner des Felds aus der Struktur Diagnosedaten erforderlich. Wenn *RecNumber* ist größer als oder gleich 1 ist, die Daten in das Feld beschreibt die Diagnoseinformationen, die von einer Funktion zurückgegeben. Wenn *RecNumber* gleich 0 ist, das Feld in der Kopfzeile der Diagnosedaten Struktur und enthält daher Daten bezieht sich auf den Aufruf der Funktion, die die Diagnoseinformationen nicht an die spezifischen Informationen zurückgegeben.  
  
 Treiber können treiberspezifische Header und Datensatzfelder in der Struktur Diagnosedaten definieren.  
  
 Eine ODBC 3.*.x* Anwendung arbeiten mit einer ODBC 2.*.x* Treiber wird in der Lage, rufen Sie **SQLGetDiagField** nur mit einem *DiagIdentifier* Argument SQL_DIAG_CLASS_ORIGIN, SQL_DIAG_CLASS_SUBCLASS_ORIGIN, SQL_DIAG_CONNECTION_NAME, SQL_DIAG_MESSAGE_TEXT, SQL_DIAG_NATIVE, SQL_DIAG_NUMBER, SQL_DIAG_RETURNCODE, SQL_DIAG_SERVER_NAME oder SQL_DIAG_SQLSTATE. Alle anderen Diagnosefelder gibt SQL_ERROR zurück.  
  
## <a name="header-fields"></a>Headerfelder  
 Headerfelder, die in der folgenden Tabelle aufgeführten enthalten sein können, der *DiagIdentifier* Argument.  
  
|DiagIdentifier|Rückgabetyp|Rückgabewert|  
|--------------------|-----------------|-------------|  
|SQL_DIAG_CURSOR_ROW_COUNT|SQLLEN|Dieses Feld enthält die Anzahl der Zeilen im Cursor. Seine Semantik richten sich nach der **SQLGetInfo** SQL_DYNAMIC_CURSOR_ATTRIBUTES2, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2 SQL_KEYSET_CURSOR_ATTRIBUTES2 und SQL_STATIC_CURSOR_ATTRIBUTES2, was darauf hindeuten, die dass Typen von Informationen Zeilenanzahl sind verfügbar für jeden Cursortyp (in den SQL_CA2_CRC_EXACT und SQL_CA2_CRC_APPROXIMATE, Bits).<br /><br /> Der Inhalt dieses Felds wird definiert, nur für Anweisungshandles und erst nach **SQLExecute**, **SQLExecDirect**, oder **SQLMoreResults** aufgerufen wurde. Aufrufen von **SQLGetDiagField** mit einem *DiagIdentifier* von SQL_DIAG_CURSOR_ROW_COUNT auf als eine Anweisung Handle SQL_ERROR zurück.|  
|SQL_DIAG_DYNAMIC_FUNCTION|SQLCHAR *|Dies ist eine Zeichenfolge, die die SQL-Anweisung wird beschrieben, die die zugrunde liegende Funktion ausgeführt. (Siehe weiter unten in diesem Abschnitt "Werte der Felder dynamische Funktion" nach bestimmten Werten). Der Inhalt dieses Felds wird definiert, nur für Anweisungshandles und nur nach einem Aufruf von **SQLExecute**, **SQLExecDirect**, oder **SQLMoreResults**. Aufrufen von **SQLGetDiagField** mit einem *DiagIdentifier* von SQL_DIAG_DYNAMIC_FUNCTION auf als eine Anweisung Handle SQL_ERROR zurück. Der Wert dieses Felds ist nicht definiert, vor einem Aufruf von **SQLExecute** oder **SQLExecDirect**.|  
|SQL_DIAG_DYNAMIC_FUNCTION_CODE|SQLINTEGER|Dies ist ein numerischer Code, der die SQL-Anweisung beschreibt, die von der zugrunde liegenden Funktion ausgeführt wurde. (Siehe "Werte von der dynamischen Funktion Felder" weiter unten in diesem Abschnitt für bestimmte Wert). Der Inhalt dieses Felds wird definiert, nur für Anweisungshandles und nur nach einem Aufruf von **SQLExecute**, **SQLExecDirect**, oder **SQLMoreResults**. Aufrufen von **SQLGetDiagField** mit einem *DiagIdentifier* von SQL_DIAG_DYNAMIC_FUNCTION_CODE auf als eine Anweisung Handle SQL_ERROR zurück. Der Wert dieses Felds ist nicht definiert, vor einem Aufruf von **SQLExecute** oder **SQLExecDirect**.|  
|SQL_DIAG_NUMBER|SQLINTEGER|Die Anzahl der Statusdatensätze, die für das angegebene Handle verfügbar sind.|  
|SQL_DIAG_RETURNCODE|SQLRETURN|Der Rückgabecode von der Funktion zurückgegeben. Eine Liste von Rückgabecodes finden Sie [Rückgabecodes](../../../odbc/reference/develop-app/return-codes-odbc.md). Der Treiber keine SQL_DIAG_RETURNCODE implementiert; Es wird immer vom Treiber-Manager implementiert. Wenn für die noch keine Funktion aufgerufen wurde die *behandeln*, für SQL_DIAG_RETURNCODE wird SQL_SUCCESS zurückgegeben werden.|  
|SQL_DIAG_ROW_COUNT|SQLLEN|Die Anzahl der Zeilen, die von einer INSERT-, DELETE- oder Update, die von ausgeführten betroffen **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oder **SQLSetPos**. Es wird nach treiberdefinierten eine *Cursorspezifikation* ausgeführt wurde. Der Inhalt dieses Felds werden nur für Anweisungshandles definiert. Aufrufen von **SQLGetDiagField** mit einem *DiagIdentifier* von SQL_DIAG_ROW_COUNT auf als eine Anweisung Handle SQL_ERROR zurück. Die Daten in diesem Feld werden auch zurückgegeben, der *RowCountPtr* Argument **SQLRowCount**. Die Daten in dieses Feld ist nach jedem Funktionsaufruf nondiagnostic zurücksetzen, während von die Anzahl der Zeilen zurückgegeben **SQLRowCount** bleibt unverändert, bis die Anweisung wieder auf den vorbereiteten oder zugeordneten Status festgelegt wird.|  
  
## <a name="record-fields"></a>Datensatzfelder  
 Die Datensatzfelder, die in der folgenden Tabelle aufgeführten enthalten sein können, der *DiagIdentifier* Argument.  
  
|DiagIdentifier|Rückgabetyp|Rückgabewert|  
|--------------------|-----------------|-------------|  
|SQL_DIAG_CLASS_ORIGIN|SQLCHAR *|Eine Zeichenfolge, die das Dokument angibt, das die Klassenteil der SQLSTATE-Wert in diesem Datensatz definiert. Der Wert ist "ISO 9075" für alle SQLSTATEs durch Open Group und ISO-Call-Level-Interface definiert. Für ODBC-spezifische SQLSTATEs (alle Sprachen, deren SQLSTATE-Klasse im ist ""), ihr Wert ist "ODBC 3.0".|  
|SQL_DIAG_COLUMN_NUMBER|SQLINTEGER|Wenn das Feld SQL_DIAG_ROW_NUMBER eine gültige Zeilennummer ein Rowset oder einem Satz von Parametern ist, enthält dieses Feld den Wert, der die Nummer der Spalte im Resultset oder die Parameteranzahl in der Menge von Parametern darstellt. Resultset-Spalte, die die Versionsnummern sich immer bei 1 beginnen; Wenn dieser Status Datensatz zu einer Lesezeichenspalte bezieht, kann das Feld 0 (null) sein. Parameter die Versionsnummern beginnen bei 1. Wenn der Status-Datensatz nicht mit einem Nummer der Spalte oder Parameter Nr. zugeordnet ist, hat er Wert SQL_NO_COLUMN_NUMBER. Wenn der Treiber nicht ermitteln kann, die Nummer der Spalte oder Parameter mit der Nummer, die diesem Datensatz zugeordnet ist, ist dieses Feld den Wert SQL_COLUMN_NUMBER_UNKNOWN an.<br /><br /> Der Inhalt dieses Felds werden nur für Anweisungshandles definiert.|  
|SQL_DIAG_CONNECTION_NAME|SQLCHAR *|Eine Zeichenfolge, die den Namen der Verbindung, die angibt mit dem Diagnosedatensatz verknüpft. Dieses Feld ist treiberdefinierten. Für diagnostische Datenstrukturen, die das Umgebungshandle zugeordnet und für die Diagnose, die nicht auf eine beliebige Verbindung beziehen, ist dieses Feld eine Zeichenfolge der Länge 0 (null).|  
|SQL_DIAG_MESSAGE_TEXT|SQLCHAR *|Eine informative Meldung für den Fehler oder die Warnung. Dieses Feld wird formatiert, wie in beschrieben [Diagnosemeldungen](../../../odbc/reference/develop-app/diagnostic-messages.md). Es gibt keine maximale Länge für den Text diagnosemeldung ein.|  
|SQL_DIAG_NATIVE|SQLINTEGER|Ein Treiber/Data datenquellenspezifischen systemeigene Fehlercode. Der Treiber gibt 0 zurück, wenn es keine systemeigene Fehlercode ist.|  
|SQL_DIAG_ROW_NUMBER|SQLLEN|Dieses Feld enthält die Nummer der Zeile im Rowset oder die Parameteranzahl in der Menge der Parameter, die der Status Datensatz zugeordnet ist. Zeilennummern und Parameternummern beginnen mit 1. Dieses Feld hat den Wert SQL_NO_ROW_NUMBER aus, wenn dieser Status-Datensatz keine Zeilennummer oder Parameter Nr. zugeordnet ist. Wenn der Treiber nicht ermitteln kann, die Nummer der Zeile oder einen Parameter mit der Nummer, die diesem Datensatz zugeordnet ist, ist dieses Feld den Wert SQL_ROW_NUMBER_UNKNOWN an.<br /><br /> Der Inhalt dieses Felds werden nur für Anweisungshandles definiert.|  
|SQL_DIAG_SERVER_NAME|SQLCHAR *|Eine Zeichenfolge, die den Namen des Servers, dem angibt mit dem Diagnosedatensatz verknüpft. Es ist identisch mit den Rückgabewert für einen Aufruf **SQLGetInfo** mit der Option SQL_DATA_SOURCE_NAME. Für diagnostische Datenstrukturen, die das Umgebungshandle zugeordnet und für die Diagnose, die nicht auf einem beliebigen Server beziehen, ist dieses Feld eine Zeichenfolge der Länge 0 (null).|  
|SQL_DIAG_SQLSTATE|SQLCHAR *|Ein fünf Zeichen SQLSTATE diagnostische Code. Weitere Informationen finden Sie unter [SQLSTATEs](../../../odbc/reference/develop-app/sqlstates.md).|  
|SQL_DIAG_SUBCLASS_ORIGIN|SQLCHAR *|Eine Zeichenfolge mit dem gleichen Format und die gültigen Werte als SQL_DIAG_CLASS_ORIGIN, die den definierenden Teil der Unterklasse Teil des SQLSTATE-Codes identifiziert. Der ODBC-spezifische SQLSTATES für die "ODBC 3.0" zurückgegeben wird, umfassen Folgendes:<br /><br /> 01 S 00, 01 S 01, 01 S 02, 01S06, 01S07, 07S01, 08 S 01 21S01, 21S02, 25 S 01, 25S02, 25S03, 42S01, 42S02, 42S11, 42S12, 42S21, 42S22, HY095, HY097, HY098, HY099, HY100, HY101, HY105, HY107, HY109, HY110, HY111, HYT00, HYT01, IM001, IM002, IM003, IM004, IM005, IM006, IM007, IM008, IM010, IM011, IM012.|  
  
## <a name="values-of-the-dynamic-function-fields"></a>Werte der Felder dynamischen-Funktion  
 Die folgende Tabelle beschreibt die Werte der SQL_DIAG_DYNAMIC_FUNCTION und SQL_DIAG_DYNAMIC_FUNCTION_CODE, die für jeden Typ, der durch einen Aufruf von ausgeführte SQL-Anweisung gelten **SQLExecute** oder **SQLExecDirect**. Der Treiber kann die aufgeführten treiberdefinierten Werte hinzufügen.  
  
|SQL-Anweisung<br /><br /> ausgeführt|Wert des<br /><br /> SQL_DIAG_DYNAMIC_FUNCTION|Wert des<br /><br /> SQL_DIAG_DYNAMIC_FUNCTION_CODE|  
|--------------------------------|-----------------------------------------------|-----------------------------------------------------|  
|*Alter-Domain-Anweisung*|"ALTER DOMÄNE"|SQL_DIAG_ALTER_DOMAIN|  
|*Alter-Table-Anweisung*|"ALTER TABLE"|SQL_DIAG_ALTER_TABLE|  
|*Assertion-definition*|"CREATE ASSERTION"|SQL_DIAG_CREATE_ASSERTION|  
|*Zeichen Satzdefinition*|"ERSTELLEN SIE ZEICHENSATZ"|SQL_DIAG_CREATE_CHARACTER_SET|  
|*Collation-definition*|"ERSTELLEN SIE SORTIERUNG"|SQL_DIAG_CREATE_COLLATION|  
|*Create-Index-Anweisung*|"ERSTELLEN SIE INDEX"|SQL_DIAG_CREATE_INDEX|  
|*Erstellen Sie-Table-Anweisung*|"ERSTELLEN SIE TABELLE"|SQL_DIAG_CREATE_TABLE|  
|*Create-View-Anweisung*|"ERSTELLEN SIE ANSICHT"|SQL_DIAG_CREATE_VIEW|  
|*Cursor-Spezifikation*|"WÄHLEN SIE CURSOR"|SQL_DIAG_SELECT_CURSOR|  
|*DELETE-Anweisung positioniert*|"DELETE DYNAMISCHE CURSOR"|SQL_DIAG_DYNAMIC_DELETE_CURSOR|  
|*DELETE-Anweisung durchsucht*|"WHERE LÖSCHEN"|SQL_DIAG_DELETE_WHERE|  
n-Definition *|"ERSTELLEN SIE DOMÄNE"|SQL_DIAG_CREATE_DOMAIN|  
|*Drop-Assertion-Anweisung*|"DROP ASSERTION"|SQL_DIAG_DROP_ASSERTION|  
|*Drop-Zeichen-Set-Anweisung.*|"DROP ZEICHENSATZ"|SQL_DIAG_DROP_CHARACTER_SET|  
|*Drop-Sortierung-Anweisung*|"DROP COLLATION"|SQL_DIAG_DROP_COLLATION|  
|*Drop-Domain-Anweisung*|"DROP DOMÄNE"|SQL_DIAG_DROP_DOMAIN|  
|*Drop Index-Anweisung*|"DROP INDEX"|SQL_DIAG_DROP_INDEX|  
|*Drop-Schema-Anweisung*|"DROP SCHEMA"|SQL_DIAG_DROP_SCHEMA|  
|*Drop-Table-Anweisung*|"DROP TABLE"|SQL_DIAG_DROP_TABLE|  
|*Drop-Übersetzung-Anweisung*|"DROP ÜBERSETZUNG"|SQL_DIAG_DROP_TRANSLATION|  
|*Drop-View-Anweisung*|"DROP VIEW"|SQL_DIAG_DROP_VIEW|  
-Anweisung *|"GRANT"|SQL_DIAG_GRANT|  
|*INSERT-Anweisung*|"EINFÜGEN"|SQL_DIAG_INSERT|  
|*ODBC-Prozedur-Erweiterung*|"AUFRUF"|SQL_DIAG_ AUFRUF|  
|*REVOKE-Anweisung*|"REVOKE"|SQL_DIAG_REVOKE|  
|*Schema-definition*|"ERSTELLEN SIE SCHEMA"|SQL_DIAG_CREATE_SCHEMA|  
|*Translation-definition*|"ÜBERSETZUNG ZU ERSTELLEN"|SQL_DIAG_CREATE_TRANSLATION|  
|*Update-Anweisung positioniert*|"DYNAMISCHE AKTUALISIERUNG CURSOR"|SQL_DIAG_DYNAMIC_UPDATE_CURSOR|  
|*Update-Anweisung durchsucht*|"WHERE AKTUALISIEREN"|SQL_DIAG_UPDATE_WHERE|  
|Unknown|*Leere Zeichenfolge*|SQL_DIAG_UNKNOWN_STATEMENT|  
  
## <a name="sequence-of-status-records"></a>Sequenz der Statusdatensätze  
 Statusdatensätze werden in einer Sequenz basierend auf der Zeilennummer und den Typ der Diagnose positioniert. Der Treiber-Manager bestimmt die endgültige Reihenfolge in den statusdatensätzen zurückgegeben, die sie generiert. Der Treiber bestimmt die endgültige Reihenfolge in den statusdatensätzen zurückgegeben, die sie generiert.  
  
 Wenn der DiagnoseDatensätze von der Treiber-Manager und der Treiber bereitgestellt werden, ist der Treiber-Manager für ihre Anordnung verantwortlich.  
  
 Wenn zwei oder mehr Statusdatensätze vorhanden sind, ist die Reihenfolge der Datensätze zuerst Zeilennummer richtet. Die folgenden Regeln gelten für die Sequenz von Diagnosedatensätzen zeilenweise bestimmen:  
  
-   Datensätze, die nicht mit einer beliebigen Zeile übereinstimmen angezeigt vor Datensätze, die einer bestimmten Zeile entsprechen, da es sich bei SQL_NO_ROW_NUMBER – 1 definiert ist.  
  
-   Datensätze, die für die Nummer der Zeile unbekannt ist werden vor allen anderen Datensätzen angezeigt, da SQL_ROW_NUMBER_UNKNOWN definiert ist, um – 2 werden.  
  
-   Für alle Datensätze, die an bestimmten Zeilen betreffen, werden die Datensätze durch den Wert im Feld SQL_DIAG_ROW_NUMBER sortiert. Alle Fehler und Warnungen der ersten Zeile betroffen aufgeführt sind, und klicken Sie dann alle Fehler und Warnungen der nächsten Zeile betroffenen usw.  
  
> [!NOTE]  
>  Die ODBC 3.*.x* Treibermanager sortiert nicht Statusdatensätze in der Diagnose Warteschlange Wenn SQLSTATE 01 s 01 (Fehler in Zeile) wird zurückgegeben, von einer ODBC 2.*.x* Treiber oder, wenn SQLSTATE 01 s 01 (Fehler in Zeile) wird zurückgegeben, die von einer ODBC 3*.x* Treiber beim **SQLExtendedFetch** aufgerufen wird oder **SQLSetPos** wird aufgerufen, für einen Cursor, die mit positioniert **SQLExtendedFetch** .  
  
 Innerhalb jeder Zeile, oder für alle Datensätze, die für die Nummer der Zeile unbekannt ist oder eine Zeile nicht entsprechen, oder für alle diese Datensätze mit einer Zeilennummer SQL_NO_ROW_NUMBER gleich, richtet sich der erste Datensatz aufgeführt werden anhand eines Satzes von Regeln zu sortieren. Nach dem ersten Datensatz ist die Reihenfolge von den anderen Datensätzen, die Auswirkungen auf eine Zeile nicht definiert. Eine Anwendung kann nicht davon ausgehen, dass Fehler nach dem ersten Datensatz Warnungen vorausgehen. Anwendungen sollten die vollständige Diagnosedaten-Struktur, um vollständige Informationen zu einer nicht erfolgreichen Aufruf einer Funktion Abrufen überprüfen.  
  
 Die folgenden Regeln werden verwendet, um den ersten Datensatz innerhalb einer Zeile bestimmt. Der Datensatz mit dem höchsten Rang ist der erste Datensatz. Die Quelle eines Datensatzes (Treiber-Manager, Treiber, Gateway, usw.) wird nicht berücksichtigt, wenn Datensätze Rangfolge.  
  
-   **Fehler** Statusdatensätze, die Fehler zu beschreiben, haben den höchsten Rang. Die folgenden Regeln werden angewendet, um Fehler zu sortieren:  
  
    -   Datensätze, die Angabe eines Transaktionsfehler oder mögliche Transaktionsfehler outrank alle anderen Einträge.  
  
    -   Wenn zwei oder mehr Datensätze die gleiche fehlerbedingung beschreiben, outrank SQLSTATEs, die von der Open Group-CLI-Spezifikation (Klassen 03 durch HZ) definierten SQLSTATEs ODBC und Treiber definiert.  
  
-   **Die Implementierung definiertes keine Datenwerte** Statusdatensätze, die beschreiben, treiberdefinierten keine Daten Werte (Klasse 02) haben die zweite höchsten Rang.  
  
-   **Warnungen** Statusdatensätze, die beschreiben, Warnungen (01-Klasse) haben die niedrigsten Rang. Wenn zwei oder mehr Datensätze die gleichen warnungsbedingung, Warnung von der Open Group-CLI-Spezifikation definierten SQLSTATEs beschreiben outrank ODBC definiert und treiberdefinierten SQLSTATEs.  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Abrufen von mehreren Feldern einer Diagnosedaten-Struktur|[SQLGetDiagRec-Funktion](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)

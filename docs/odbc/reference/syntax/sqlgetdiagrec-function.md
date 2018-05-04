---
title: SQLGetDiagRec-Funktion | Microsoft Docs
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
ms.topic: conceptual
apiname:
- SQLGetDiagRec
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetDiagRec
helpviewer_keywords:
- SQLGetDiagRec function [ODBC]
ms.assetid: ebdbac93-3d68-438f-8416-ef1f08e04269
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cc6db91f2f68b4029f3f48f9765e8aa4679dfa3f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlgetdiagrec-function"></a>SQLGetDiagRec-Funktion
**Konformität**  
 Version eingeführt: ODBC 3.0 Standardkonformität: ISO-92  
  
 **Zusammenfassung**  
 **SQLGetDiagRec** gibt die aktuellen Werte aus mehreren Feldern des ein Diagnosedatensatz, die Fehler, Warnung und Statusinformationen enthält. Im Gegensatz zu **SQLGetDiagField**, womit eine Diagnose Feld pro Aufruf **SQLGetDiagRec** verschiedene, häufig verwendete Felder des ein Diagnosedatensatz, einschließlich SQLSTATE, der systemeigene Fehlercode zurückgibt und die diagnosemeldung Text.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLGetDiagRec(  
     SQLSMALLINT     HandleType,  
     SQLHANDLE       Handle,  
     SQLSMALLINT     RecNumber,  
     SQLCHAR *       SQLState,  
     SQLINTEGER *    NativeErrorPtr,  
     SQLCHAR *       MessageText,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   TextLengthPtr);  
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
 [Eingabe] Gibt den Status-Datensatz aus dem die Anwendung Informationen Suchvorgängen an. Statusdatensätze werden von 1 nummeriert.  
  
 *SQLState*  
 [Ausgabe] Zeiger auf einen Puffer, in dem eine fünf Zeichen SQLSTATE-Code (und das abschließende NULL-) für die Diagnosedatensatz zurückgegeben *RecNumber*. Die ersten beiden Zeichen anzugeben, die Klasse; die nächsten drei Geben Sie an die-Unterklasse. Diese Informationen sind im Feld SQL_DIAG_SQLSTATE Diagnose enthalten. Weitere Informationen finden Sie unter [SQLSTATEs](../../../odbc/reference/develop-app/sqlstates.md).  
  
 *NativeErrorPtr*  
 [Ausgabe] Zeiger auf einen Puffer, in dem den systemeigene Fehlercode für die Datenquelle spezifischen zurückgegeben. Diese Informationen sind im Feld SQL_DIAG_NATIVE Diagnose enthalten.  
  
 *MessageText*  
 [Ausgabe] Zeiger auf einen Puffer, in dem die diagnosemeldung Textzeichenfolge zurückgegeben. Diese Informationen sind im Feld SQL_DIAG_MESSAGE_TEXT Diagnose enthalten. Das Format der Zeichenfolge, finden Sie unter [Diagnosemeldungen](../../../odbc/reference/develop-app/diagnostic-messages.md).  
  
 Wenn *MessageText* NULL ist, *TextLengthPtr* gibt weiterhin zurück, die Gesamtzahl der Zeichen (mit Ausnahme der Null-Terminierung Zeichen für Zeichendaten) verfügbaren zurückzugebenden im Puffer verweist *MessageText*.  
  
 *Pufferlänge*  
 [Eingabe] Länge der **MessageText* -Puffers in Zeichen. Es gibt keine maximale Länge des Texts diagnosemeldung aus.  
  
 *TextLengthPtr*  
 [Ausgabe] Zeiger auf einen Puffer, in dem die Gesamtzahl der Zeichen enthalten (ohne die erforderliche Anzahl von Zeichen für die Null-Abschlusszeichen) zurückgegeben verfügbar im zurückzugebenden  *\*MessageText*. Ist die Anzahl der zurückzugebenden verfügbaren Zeichen ist größer als *Pufferlänge*, den Text diagnosemeldung in  *\*MessageText* auf abgeschnitten *Pufferlänge* abzüglich der Länge des ein Null-Abschlusszeichen.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR oder SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnose  
 **SQLGetDiagRec** DiagnoseDatensätze für sich selbst wird nicht gesendet. Er verwendet die folgenden Rückgabewerte, um das Ergebnis der eigenen Ausführung melden:  
  
-   SQL_SUCCESS: Die Funktion wurde erfolgreich zurückgegeben Diagnoseinformationen.  
  
-   SQL_SUCCESS_WITH_INFO: Die \* *MessageText* Formatnamenpuffer war zu klein, um die angeforderten diagnosemeldung aufzunehmen. Es wurden keine DiagnoseDatensätze generiert. Um zu ermitteln, die einen abgeschnittenen Daten, die Anwendung muss vergleichen *Pufferlänge* auf die tatsächliche Anzahl von Bytes verfügbar ist, die in geschrieben wird **StringLengthPtr*.  
  
-   SQL_INVALID_HANDLE: Das Handle erkennbar *HandleType* und *behandeln* war es sich nicht um ein gültiges Handle.  
  
-   SQL_ERROR: Eine der folgenden aufgetreten ist:  
  
    -   *RecNumber* war negativ oder 0.  
  
    -   *Pufferlänge* war kleiner als 0 (null).  
  
    -   Wenn Sie die asynchrone Benachrichtigung verwenden zu können, war der asynchrone Vorgang auf das Handle nicht abgeschlossen werden.  
  
-   SQL_NO_DATA: *RecNumber* war größer als die Zahl der DiagnoseDatensätze, die für das Handle im angegebenen vorhanden waren *behandeln.* Die Funktion gibt SQL_NO_DATA auch für eine beliebige positive Werte *RecNumber* treten keine DiagnoseDatensätze für *behandeln*.  
  
## <a name="comments"></a>Kommentare  
 Ruft eine Anwendung in der Regel **SQLGetDiagRec** bei ein vorherigen Aufruf einer ODBC-Funktion SQL_ERROR oder SQL_SUCCESS_WITH_INFO zurückgegeben hat. Da eine ODBC-Funktion 0 (null) oder mehrere DiagnoseDatensätze jedes Mal zurücksenden kann aufgerufen wird, eine Anwendung kann jedoch aufrufen **SQLGetDiagRec** nach einem beliebigen ODBC-Funktionsaufruf. Eine Anwendung kann Aufrufen **SQLGetDiagRec** mehrere Male auf, um einige oder alle Datensätze in der Struktur diagnostische Daten zurückgeben. ODBC erzwingt keine Begrenzung der Anzahl der DiagnoseDatensätze, die jeweils gespeichert werden können.  
  
 **SQLGetDiagRec** kann nicht verwendet werden, um Felder aus dem Header der Diagnosedaten Struktur zurückzugeben. (Die *RecNumber* Argument muss größer als 0 sein.) Die Anwendung sollte Aufrufen **SQLGetDiagField** für diesen Zweck.  
  
 **SQLGetDiagRec** ruft nur die zuletzt zugeordnete angegebene Handle Diagnoseinformationen der *behandeln* Argument. Wenn die Anwendung eine andere ODBC-Funktion aufruft, außer **SQLGetDiagRec**, **SQLGetDiagField**, oder **SQLError**, diagnostische Informationen aus den vorherigen Aufrufen auf der dasselbe Handle geht verloren.  
  
 Eine Anwendung kann Scannen alle DiagnoseDatensätze von Schleifen, Inkrementieren *RecNumber*, solange **SQLGetDiagRec** gibt SQL_SUCCESS zurück. Aufrufe von **SQLGetDiagRec** sind für die Header und Datensatz zerstörerisch. Die Anwendung aufrufen kann **SQLGetDiagRec** erneut zu einem späteren Zeitpunkt ein Feld aus einem Datensatz, wie lange Wartezeiten als keine anderen Funktion, mit Ausnahme von abzurufenden **SQLGetDiagRec**, **SQLGetDiagField**, oder **SQLError**, in der Zwischenzeit aufgerufen wurde. Anzahl der Gesamtzahl von Diagnosedatensätzen verfügbar kann auch durch Aufrufen von die Anwendung abrufen **SQLGetDiagField** zum Abrufen des Werts, der die SQL_DIAG_NUMBER Feld aufrufen und anschließend **SQLGetDiagRec**genauso oft.  
  
 Eine Beschreibung der Felder der Struktur Diagnosedaten, finden Sie unter [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md). Weitere Informationen finden Sie unter [mithilfe SQLGetDiagRec und SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md) und [implementieren SQLGetDiagRec und SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md).  
  
 Aufrufen einer API als dem, der asynchron ausgeführt wird, wird HY010 generieren "Function Sequenzfehler". Error-Datensatzes kann allerdings abgerufen werden, bevor der asynchrone Vorgang abgeschlossen ist.  
  
## <a name="handletype-argument"></a>HandleType-Argument  
 Jede Handletyp kann Diagnoseinformationen zugeordnet haben. Die *HandleType* Argument gibt den Handle der *behandeln* Argument.  
  
 Einige Felder "Header" und "Datensatz können für die Umgebung, Verbindung, anweisungs- und Deskriptorstatuswerte Handles zurückgegeben werden. Diese Handles, die für die ein Feld nicht anwendbar ist sind in den Abschnitten "Headerfelder" und "Datensatzfelder" gekennzeichnet [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md).  
  
 Ein Aufruf von **SQLGetDiagRec** gibt SQL_INVALID_HANDLE zurück, wenn *HandleType* SQL_HANDLE_SENV, das eine freigegebene Umgebungshandle bezeichnet wird. Jedoch wenn *HandleType* SQL_HANDLE_ENV auf, wird *behandeln* können eine freigegebene oder ein Umgebungshandle aufgehoben werden.  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Abrufen von einem Feld ein Diagnosedatensatz oder ein Feld des Diagnose-Headers|[SQLGetDiagField-Funktion](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)   
 [ODBC-Beispielprogramm](../../../odbc/reference/sample-odbc-program.md)

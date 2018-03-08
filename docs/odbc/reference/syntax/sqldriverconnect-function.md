---
title: SQLDriverConnect-Funktion | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLDriverConnect
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLDriverConnect
helpviewer_keywords: SQLDriverConnect function [ODBC]
ms.assetid: e299be1d-5c74-4ede-b6a3-430eb189134f
caps.latest.revision: "50"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 4600a76e303930e941c737313f1db4850f8d5e43
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="sqldriverconnect-function"></a>SQLDriveConnect-Funktion
**Konformität**  
 Version eingeführt: ODBC 1.0 Standardkonformität: ODBC  
  
 **Zusammenfassung**  
 **SQLDriverConnect** ist eine Alternative zum **SQLConnect**. Es unterstützt Datenquellen, die weitere Verbindungsinformationen als drei Argumente erfordern **SQLConnect**, Dialogfelder, um die benutzeraufforderung für alle Verbindungsinformationen und Datenquellen, die nicht im System definiert sind Informationen.  
  
 **SQLDriverConnect** bietet die folgenden Verbindungsattribute:  
  
-   Herstellen einer Verbindungs mit einer Verbindungszeichenfolge, die den Datenquellennamen, eine oder mehrere Benutzer-IDs, eine oder mehrere Kennwörter und andere erforderlichen Informationen enthält von der Datenquelle an.  
  
-   Herstellen einer Verbindungs mit eine Teilverbindungszeichenfolge oder keine zusätzlichen Informationen; der Treiber-Manager und der Treiber können jede in diesem Fall den Benutzer zur Verbindungsinformationen aufzufordern.  
  
-   Erstellen einer Verbindung mit einer Datenquelle, die nicht in die Systeminformationen definiert ist. Wenn die Anwendung eine Teilverbindungszeichenfolge bereitstellt, kann der Treiber den Benutzer zur Verbindungsinformationen aufzufordern.  
  
-   Erstellen einer Verbindung mit einer Datenquelle mithilfe einer Verbindungszeichenfolge, die aus den Informationen in einem DSN-Datei erstellt.  
  
 Nachdem eine Verbindung hergestellt wurde, **SQLDriverConnect** gibt die vervollständigte Verbindungszeichenfolge zurück. Die Anwendung kann diese Zeichenfolge für nachfolgende verbindungsanforderungen verwenden. Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit SQLDriverConnect](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLDriverConnect(  
     SQLHDBC         ConnectionHandle,  
     SQLHWND         WindowHandle,  
     SQLCHAR *       InConnectionString,  
     SQLSMALLINT     StringLength1,  
     SQLCHAR *       OutConnectionString,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   StringLength2Ptr,  
     SQLUSMALLINT    DriverCompletion);  
```  
  
## <a name="arguments"></a>Argumente  
 *Verbindungshandle*  
 [Eingabe] Verbindungshandle.  
  
 *WindowHandle*  
 [Eingabe] Das Fensterhandle. Die Anwendung kann das Handle des übergeordneten Fensters übergeben, sofern zutreffend, oder ein null-Zeiger, wenn entweder das Fensterhandle gilt nicht oder **SQLDriverConnect** alle Dialogfelder ist nicht vorhanden.  
  
 *InConnectionString*  
 [Eingabe] Eine vollständige Verbindungszeichenfolge (siehe die Syntax in "Kommentare"), eine Teilverbindungszeichenfolge oder eine leere Zeichenfolge.  
  
 *StringLength1*  
 [Eingabe] Länge des **InConnectionString*, in Zeichen, wenn die Zeichenfolge Unicode oder Bytes ist, wenn Zeichenfolge ANSI- oder DBCS ist.  
  
 *OutConnectionString*  
 [Ausgabe] Ein Zeiger auf einen Puffer für die vervollständigte Verbindungszeichenfolge. Bei erfolgreicher Verbindung an die Zieldatenquelle enthält dieser Puffer vervollständigte Verbindungszeichenfolge an. Anwendungen sollten mindestens 1.024 Zeichen für diesen Puffer zuweisen.  
  
 Wenn *OutConnectionString* NULL ist, *StringLength2Ptr* gibt weiterhin zurück, die Gesamtzahl der Zeichen (mit Ausnahme der Null-Terminierung Zeichen für Zeichendaten) verfügbar, die in den Puffer zurückgegeben verweist *OutConnectionString*.  
  
 *Pufferlänge*  
 [Eingabe] Länge der **OutConnectionString* Puffers in Zeichen.  
  
 *StringLength2Ptr*  
 [Ausgabe] Zeiger auf einen Puffer, in dem die Gesamtzahl der Zeichen (mit Ausnahme von Null-Abschlusszeichen) zurückgegeben verfügbar im zurückzugebenden \* *OutConnectionString*. Die Anzahl der zurückzugebenden verfügbaren Zeichen ist größer als oder gleich *Pufferlänge*, die Verbindungszeichenfolge in abgeschlossen \* *OutConnectionString* auf abgeschnitten  *Pufferlänge* abzüglich der Länge des ein Null-Abschlusszeichen.  
  
 *DriverCompletion*  
 [Eingabe] Flag, die angibt, ob der Treiber-Manager oder die Treiber muss weitere Verbindungsinformationen angefordert:  
  
 SQL_DRIVER_PROMPT, SQL_DRIVER_COMPLETE, sql_driver_complete_required lautet oder SQL_DRIVER_NOPROMPT.  
  
 (Weitere Informationen finden Sie unter "Kommentare".)  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR, SQL_INVALID_HANDLE oder SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLDriverConnect** gibt SQL_ERROR oder SQL_SUCCESS_WITH_INFO, ein zugeordneten SQLSTATE-Wert abgerufen werden kann, durch den Aufruf **SQLGetDiagRec** mit einem *fHandleType*SQL_HANDLE_DBC auf, und ein *hHandle* von *Verbindungshandle*. Die folgende Tabelle enthält die SQLSTATE-Werten, die häufig zurückgegebenes **SQLDriverConnect** und erläutert, jeweils im Kontext dieser Funktion; die Notation "(DM)" vorangestellt ist, die Beschreibungen der SQLSTATEs, die vom Treiber-Manager zurückgegeben. Der Rückgabecode, der jeden SQLSTATE-Wert zugeordnet wird SQL_ERROR zurückgegeben, sofern nicht anders angegeben.  
  
|SQLSTATE|Fehler|Description|  
|--------------|-----------|-----------------|  
|01000|Allgemeine Warnung|Treiberspezifische Meldung dient zu Informationszwecken. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|01004|Zeichenfolgedaten wurden rechts abgeschnitten|Der Puffer \* *OutConnectionString* war nicht groß genug, um die gesamte Verbindungszeichenfolge zurückzugeben, damit die Verbindungszeichenfolge abgeschnitten wurden. Die Länge der ungekürzte Verbindungszeichenfolge wird zurückgegeben, **StringLength2Ptr*. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|01 S 00|Ungültiges Attribut für Verbindungszeichenfolge|Ein ungültiges Attribut-Schlüsselwort in der Verbindungszeichenfolge angegeben wurde (*InConnectionString*), aber der Treiber wurde trotzdem eine Verbindung mit der Datenquelle herstellen können. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|01 S 02|Der Optionswert wurde geändert|Der Treiber nicht den angegebenen Wert verweist, zu der *ValuePtr* Argument in **SQLSetConnectAttr** und einen ähnlichen Wert ersetzt. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|01S08|Fehler beim Speichern der Datei-DSN|Die Zeichenfolge in  *\*InConnectionString* enthalten eine **FILEDSN** -Schlüsselwort, aber die DSN-Datei wurde nicht gespeichert. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|01S09|Ungültiges Schlüsselwort|(DM) der Zeichenfolge in  *\*InConnectionString* enthalten eine **SAVEFILE** Schlüsselwort jedoch kein **Treiber** oder ein **FILEDSN** Schlüsselwort. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|08001|Client kann keine Verbindung herstellen|Der Treiber konnte nicht zum Herstellen einer Verbindung mit der Datenquelle.|  
|08002|Name der Verbindung verwendet|(DM) dem angegebenen *Verbindungshandle* war bereits zum Herstellen einer Verbindung mit einer Datenquelle verwendet wurde und die Verbindung weiterhin geöffnet wurde.|  
|08004|Der Server wies die Verbindung|Die Datenquelle die Einrichtung der Verbindung Gründen abgelehnt Implementierung definiert.|  
|08S01|Kommunikations-Verbindungsfehler|Die Verbindung zwischen dem Treiber und die Datenquelle, die der Treiber versucht wurde, die Verbindung aufgetreten ist, bevor die **SQLDriverConnect** Verarbeitung Funktion abgeschlossen.|  
|28000|Ungültige Autorisierungsangabe|Der Bezeichner des Benutzers oder der autorisierungszeichenfolge oder beides, entsprechend den Angaben in der Verbindungszeichenfolge (*InConnectionString*), durch die Datenquelle definierten Einschränkungen verletzt.|  
|HY000|Allgemeiner Fehler|Für die es keine spezifischen SQLSTATE wurde und für die keine implementierungsabhängige SQLSTATE definiert wurde, ist ein Fehler aufgetreten. Die zurückgegebene Fehlermeldung **SQLGetDiagRec** in der  *\*SzMessageText* Puffer beschreibt den Fehler und seiner Ursache.|  
|HY000|Allgemeiner Fehler: Ungültige Datei-Dsn|(DM) der Zeichenfolge in **InConnectionString* ein Datei-DSN-Schlüsselwort enthalten, aber der Name des DSN-Datei wurde nicht gefunden.|  
|HY000|Allgemeiner Fehler: kann nicht erstellt werden Dateipuffers|(DM) der Zeichenfolge in **InConnectionString* ein Datei-DSN-Schlüsselwort enthalten, aber die DSN-Datei wurde nicht gelesen werden.|  
|HY001|Fehler bei der speicherbelegung|Der Treiber-Manager konnte nicht belegt werden zur Unterstützung der Ausführung oder den Abschluss erforderlich die **SQLDriverConnect** Funktion.<br /><br /> Der Treiber konnte nicht belegt werden zur Unterstützung der Ausführung oder den Abschluss der Funktion erforderlich.|  
|HY008|Der Vorgang wurde abgebrochen|Asynchroner Verarbeitung wurde aktiviert, für die *Verbindungshandle*. Die Funktion aufgerufen wurde, und die Ausführung vor Abschluss der [SQLCancelHandle-Funktion](../../../odbc/reference/syntax/sqlcancelhandle-function.md) aufgerufen wurde, auf die *Verbindungshandle*, und klicken Sie dann die **SQLDriverConnect** Funktion erneut aufgerufen wurde, auf die *Verbindungshandle*.<br /><br /> Or **SQLDriverConnect** Funktion aufgerufen wurde, und bevor es ausgeführt wurden, **SQLCancelHandle** aufgerufen wurde, auf die *Verbindungshandle* aus einem anderen Thread in einem Multithread-Anwendung.|  
|HY010|Fehler bei Funktionssequenz|(DM) eine andere asynchron ausgeführten Funktion (nicht **SQLDriverConnect**) aufgerufen wurde, für die *Verbindungshandle* und wurde noch ausgeführt, wenn die **SQLDriverConnect** Funktion aufgerufen wurde.|  
|HY013|Speicherverwaltungsfehler|Die **SQLDriverConnect** Funktionsaufruf konnte nicht verarbeitet werden, da die zugrunde liegenden Speicherobjekte, möglicherweise aufgrund von unzureichendem Speicher konnte nicht zugegriffen werden.|  
|HY090|Ungültige Zeichenfolgen- oder Pufferlänge.|(DM) für Argument angegebene Wert *StringLength1* kleiner als 0 und nicht wurde SQL_NTS gleich.<br /><br /> (DM) für Argument angegebene Wert *Pufferlänge* war kleiner als 0.|  
|HY092|Ungültiger Attribut-/Optionsbezeichner|(DM) die *DriverCompletion* Argument war SQL_DRIVER_PROMPT, und die *WindowHandle* Argument wurde ein null-Zeiger.|  
|HY110|Ungültiger Treiberabschluss|(DM) der Wert für das Argument angegebene *DriverCompletion* war nicht SQL_DRIVER_PROMPT, SQL_DRIVER_COMPLETE, sql_driver_complete_required lautet oder SQL_DRIVER_NOPROMPT gleich.<br /><br /> (DM) Verbindungspooling aktiviert wurde, und der angegebene Wert für das Argument *DriverCompletion* war nicht SQL_DRIVER_NOPROMPT gleich.|  
|HYC00|Optionales Feature nicht implementiert|Der Treiber unterstützt nicht die Version des ODBC-Verhalten, die die Anwendung angefordert.|  
|HYT00|Timeout abgelaufen|Das Timeout für die Anmeldung ist abgelaufen, bevor die Verbindung mit der Datenquelle abgeschlossen. Das Zeitlimit wird über festgelegt **SQLSetConnectAttr**, SQL_ATTR_LOGIN_TIMEOUT.|  
|HYT01|Verbindungstimeout abgelaufen|Das Verbindungstimeout ist abgelaufen, bevor die Datenquelle auf die Anforderung geantwortet hat. Das Verbindungstimeout wird über festgelegt **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Diese Funktion wird im Treiber nicht unterstützt.|(DM) der Treiber, der angegebene Name der Datenquelle entspricht der Funktion nicht unterstützt.|  
|IM002|Datenquelle wurde nicht gefunden und kein Standardtreiber angegeben|(DM) die Datenquelle in der Verbindungszeichenfolge angegebene Name (*InConnectionString*) wurde nicht in die Systeminformationen gefunden und gab es keine Standardspezifikation für den Treiber.<br /><br /> (DM) ODBC-Quelle und Standard-Treiber Dateninformationen konnte nicht in die Systeminformationen gefunden werden.|  
|IM003|Angegebene Treiber konnte nicht geladen werden|(DM) der Treiber aufgeführt, die in der Angabe der Datenquelle in die Systeminformationen oder gemäß der **Treiber** Schlüsselwort wurde nicht gefunden oder konnte nicht in einem anderen Grund geladen werden.|  
|IM004|Des Treibers **SQLAllocHandle** auf SQL_HANDLE_ENV auf Fehler|(DM) während der **SQLDriverConnect**, der Treiber-Manager aufgerufen, des Treibers **SQLAllocHandle** -Funktion mit einer *fHandleType* SQL_HANDLE_ENV und der Treiber zurückgegebenen ein Fehler.|  
|IM005|Des Treibers **SQLAllocHandle** auf SQL_HANDLE_DBC auf Fehler.|(DM) während der **SQLDriverConnect**, der Treiber-Manager aufgerufen, des Treibers **SQLAllocHandle** -Funktion mit einer *fHandleType* SQL_HANDLE_DBC auf, und der Treiber zurückgegeben ein Fehler.|  
|IM006|Des Treibers **SQLSetConnectAttr** fehlgeschlagen|(DM) während der **SQLDriverConnect**, der Treiber-Manager aufgerufen, des Treibers **SQLSetConnectAttr** -Funktion und der Treiber hat einen Fehler zurückgegeben.|  
|IM007|Keine Datenquelle oder Treiber angegeben; Dialogfeld nicht zulässig|Keine Datenquellennamen oder die Treiber in der Verbindungszeichenfolge angegeben wurde und *DriverCompletion* SQL_DRIVER_NOPROMPT wurde.|  
|IM008|Dialogfeld ' '|Der Treiber hat versucht, seine Anmeldedialogfeldes und Fehler.<br /><br /> *WindowHandle* wurde ein null-Zeiger und *DriverCompletion* war nicht SQL_DRIVER_NO_PROMPT.|  
|IM009|Kann nicht geladen werden Konvertierungs-DLL|Der Treiber konnte den Konvertierungs-DLL zu laden, die für die Datenquelle oder für die Verbindung angegeben wurde.|  
|IM010|Der Datenquellenname ist zu lang|(DM) wurde der Attributwert für das DSN-Schlüsselwort SQL_MAX_DSN_LENGTH Zeichen überschreitet.|  
|IM011|Der Treibername ist zu lang|(DM) das Attribut-Wert für die **Treiber** Schlüsselwort wurde mehr als 255 Zeichen.|  
|IM012|Treiber-Schlüsselwort-Syntaxfehler|(DM) der Schlüsselwort-Wert-Paar für die **Treiber** Schlüsselwort enthalten einen Syntaxfehler.<br /><br /> (DM) der Zeichenfolge in  *\*InConnectionString* enthalten eine **FILEDSN** -Schlüsselwort, aber die DSN-Datei enthielt keine **Treiber** Schlüsselwort oder ein  **DSN** Schlüsselwort.|  
|IM014|Der angegebene DSN enthält ein Architektur-Konflikt zwischen der Treiber und die Anwendung|(DM)-32-Bit-Anwendung wird einen DSN, Herstellen einer Verbindung mit einer 64-Bit-Treiber verwendet. oder umgekehrt.|  
|IM015|Fehler des Treibers SQLDriverConnect auf SQL_HANDLE_DBC_INFO_HANDLE|Wenn ein Treiber SQL_ERROR zurückgibt, der Treiber-Manager für die Anwendung SQL_ERROR zurück, und die Verbindung schlägt fehl.<br /><br /> Weitere Informationen zu SQL_HANDLE_DBC_INFO_TOKEN, finden Sie unter [entwickeln Verbindungspool wissen in eine ODBC-Treiber](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).|  
|IM017|Abrufintervall ist im Modus für asynchrone Benachrichtigung deaktiviert.|Sobald das Benachrichtigungsmodell verwendet wird, ist die Abruf deaktiviert.|  
|IM018|**SQLCompleteAsync** nicht zum Abschließen des vorherigen asynchrone Vorgangs auf diesem Handle aufgerufen wurde.|Wenn die vorherigen Funktionsaufruf auf das Handle SQL_STILL_EXECUTING zurückgibt und Benachrichtigungsmodus aktiviert ist, **SQLCompleteAsync** muss aufgerufen werden, auf das Handle nach der Verarbeitung und der Vorgang abgeschlossen werden.|  
|S1118|Asynchrone Benachrichtigung unterstützt-Treiber nicht.|Wenn der Treiber die asynchrone Benachrichtigung nicht unterstützt, kann nicht SQL_ATTR_ASYNC_DBC_EVENT oder SQL_ATTR_ASYNC_DBC_RETCODE_PTR festgelegt werden.|  
  
## <a name="comments"></a>Kommentare  
 Eine Verbindungszeichenfolge hat die folgende Syntax:  
  
 *Verbindungszeichenfolgen* :: = *leeren Zeichenfolgen*[;] &#124; *Attribut*[;] &#124; *Attribut*; *Verbindungszeichenfolgen*  
  
 *leere Zeichenfolge* :: =*Attribut* :: = *Attribut-Schlüsselwort*=*Attribut / Wert-* &#124; Treiber [{}] =*Attribut / Wert-*[}]  
  
 *Attribut-Schlüsselwort* :: = DSN &#124; UID &#124; PWD &#124; *-Treiber-definierten-Attribut-Schlüsselwort*  
  
 *Attribut / Wert-* :: = *-Zeichenfolge*  
  
 *Treiber-definierten-Attribut-Schlüsselwort* :: = *Bezeichner*  
  
 wobei *Zeichenfolge* wurde NULL oder mehr Zeichen; *Bezeichner* verfügt über eine oder mehrere Zeichen; *Attribut-Schlüsselwort* ist nicht beachtet werden soll; *Attribut / Wert-* möglicherweise Groß-/Kleinschreibung beachtet; und der Wert der **DSN** Schlüsselwort nicht ausschließlich aus Leerzeichen bestehen.  
  
 Aufgrund der Zeichenfolge und Initialisierung Datei Grammatik, Schlüsselwörter und Attribut Verbindungswerte, die die Zeichen enthalten **[] {} (),? \*=! @** eingeschlossen nicht mit Klammern sollte vermieden werden. Der Wert, der die **DSN** -Schlüsselwort darf nicht ausschließlich aus Leerzeichen bestehen und darf keine führende Leerzeichen enthalten. Aufgrund der Grammatik von Systeminformationen, Schlüsselwörter und Namen von Datenquellen können den umgekehrten Schrägstrich enthalten (\\) Zeichen.  
  
 Clientanwendungen müssen keine geschweiften Klammern, um den Wert des Attributs nach dem Hinzufügen der **Treiber** Schlüsselwort, wenn das Attribut ein Semikolon (;) enthält, in diesem Fall die Klammern sind erforderlich. Wenn der Wert des Attributs, den der Treiber empfängt geschweifte Klammern enthält, der Treiber sollten Sie nicht entfernen, aber Teil der zurückgegebenen Verbindungszeichenfolge sollte sein.  
  
 Ein Zeichenfolgenwert DSN- oder Verbindungszeichenfolge eingeschlossen in geschweifte Klammern ({}), enthält die Zeichen **[] {} (),? \*=! @** wird an den Treiber intakt übergeben. Wenn Sie diese Zeichen in einem Schlüsselwort zu verwenden, der Treiber-Manager einen Fehler zurück, bei der Arbeit mit Datei-DSNs jedoch übergibt die Verbindungszeichenfolge der Treiber für reguläre Verbindungszeichenfolgen. Verwenden Sie eingebettete geschweiften Klammern in einem Schlüsselwort-Wert.  
  
 Die Verbindungszeichenfolge kann eine beliebige Anzahl von treiberdefinierten Schlüsselwörter enthalten. Da die **Treiber** Schlüsselwort keine Informationen aus der Systeminformationen verwendet, der Treiber muss genügend Schlüsselwörter definieren, sodass ein Treiber mit einer Datenquelle, die ausschließlich anhand der Informationen in der Verbindungszeichenfolge eine Verbindung herstellen kann. (Weitere Informationen finden Sie unter "Treiber Richtlinien" weiter unten in diesem Abschnitt.) Der Treiber definiert, welche Schlüsselwörter für die Verbindung mit der Datenquelle erforderlich sind.  
  
 Die folgende Tabelle beschreibt die Attributwerte der **DSN**, **FILEDSN**, **Treiber**, **UID**, **PWD**, und **SAVEFILE** Schlüsselwörter.  
  
|Schlüsselwort|Beschreibung der Attribut-Wert|  
|-------------|---------------------------------|  
|**DSN**|Name einer Datenquelle, wie vom **SQLDataSources** oder das Dialogfeld Quellen von Daten des **SQLDriverConnect**.|  
|**DATEI-DSN**|Der Name einer DSN-Datei aus der die eine Verbindungszeichenfolge erstellt wird, für die Datenquelle. Diese Datenquellen werden Dateidatenquellen bezeichnet.|  
|**TREIBER**|Beschreibung des Treibers zurückgegebene der **SQLDrivers** Funktion. Der Rdb oder SQL Server.|  
|**UID**|Eine Benutzer-ID|  
|**PWD**|Das Kennwort, die Benutzer-ID oder eine leere Zeichenfolge entspricht, wenn kein für die Benutzer-ID Kennwort (PWD =;).|  
|**SAVEFILE**|Der Dateiname einer DSN-Datei, in dem die Attributwerte im Herstellen der Verbindungs vorhanden, erfolgreichen verwendeten Schlüsselwörter gespeichert werden soll.|  
  
 Weitere Informationen dazu, wie eine Anwendung eine Datenquelle oder Treiber auswählt, finden Sie unter [Auswählen der Datenquelle oder Treiber](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md).  
  
 Wenn keine Schlüsselwörter in der Verbindungszeichenfolge wiederholt werden, verwendet der Treiber den zugeordneten Wert durch das erste Vorkommen des Schlüsselworts. Wenn die **DSN** und **Treiber** Schlüsselwörter sind in derselben Verbindungszeichenfolge enthalten, die der Treiber-Manager und der Treiber verwenden, unabhängig davon, welche Schlüsselwort an erster Stelle steht.  
  
 Die **FILEDSN** und **DSN** Schlüsselwörter schließen sich gegenseitig: unabhängig davon, welche Schlüsselwort an erster Stelle steht, wird verwendet, und zweite angezeigt wird ignoriert. Die **FILEDSN** und **Treiber** Schlüsselwörter, andererseits, sind nicht gegenseitig. Wenn-Schlüsselworts in einer Verbindungszeichenfolge mit **FILEDSN**, und klicken Sie dann die Attributwert, der das Schlüsselwort in der Verbindungszeichenfolge anstelle der Attributwert des gleichen-Schlüsselworts in der DSN-Datei verwendet wird.  
  
 Wenn die **FILEDSN** Schlüsselwort verwendet wird, die Schlüsselwörter, die in einer DSN-Datei angegeben werden verwendet, um eine Verbindungszeichenfolge zu erstellen. (Weitere Informationen finden Sie unter "Datei Data Sources," weiter unten in diesem Abschnitt.) Die **UID** Schlüsselwort ist optional; eine DSN-Datei kann nur mit erstellt werden die **Treiber** Schlüsselwort. Die **PWD** Schlüsselwort ist nicht in einem DSN-Datei gespeichert. Das Standardverzeichnis für das Speichern und Laden von DSN-Datei werden eine Kombination von angegebene Pfad **CommonFileDir** Windows\CurrentVersion "hkey_local_machine\software\microsoft\" und "ODBC\DataSources". (Wenn CommonFileDir "C:\Program Files\Common Files" wäre, würde das Standardverzeichnis "C:\Programme\Microsoft c:\Programme\Gemeinsame Dateien\ODBC\Data Sources" sein.)  
  
> [!NOTE]  
>  DSN-Datei kann bearbeitet werden, direkt durch Aufrufen der [SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md) und [SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md) Funktionen in der DLL-Installer.  
  
 Wenn die **SAVEFILE** Schlüsselwort verwendet wird, werden die Attributwerte im Herstellen der Verbindungs vorhanden, erfolgreichen verwendeten Schlüsselwörter als DSN-Datei mit dem Namen, der den Wert des Attributs gespeichert werden die **SAVEFILE** Schlüsselwort. Die **SAVEFILE** Schlüsselwort muss verwendet werden, zusammen mit der **Treiber** -Schlüsselwort, die **FILEDSN** Schlüsselwort oder beides, oder die Funktion gibt SQL_SUCCESS_WITH_INFO mit SQLSTATE 01S09 (ungültiges Schlüsselwort). Die **SAVEFILE** Schlüsselwort muss angezeigt werden, bevor die **Treiber** Schlüsselwort in der Verbindungszeichenfolge oder die Ergebnisse nicht definiert.  
  
## <a name="driver-manager-guidelines"></a>Treiber-Manager-Richtlinien  
 Der Treiber-Manager erstellt eine Verbindungszeichenfolge für die Übergabe an den Treiber in den *InConnectionString* Argument des Treibers **SQLDriverConnect** Funktion. Der Treiber-Manager ändert nicht die *InConnectionString* Argument übergeben, von der Anwendung.  
  
 Die Aktion des Treiber-Managers ist auf Grundlage des Werts von der *DriverCompletion* Argument:  
  
-   SQL_DRIVER_PROMPT: Wenn die Verbindungszeichenfolge entweder keinen enthält die **Treiber**, **DSN**, oder **FILEDSN** Schlüsselwort, das der Treiber-Manager zeigt das Dialogfeld Datenquellen an. Er erstellt eine Verbindungszeichenfolge aus der Name der Datenquelle vom Dialogfeld zurückgegeben und allen anderen Schlüsselwörtern, die von der Anwendung übergeben werden. Wenn der Name der Datenquelle zurückgegeben werden, die im Dialogfeld leer ist, gibt der Treiber-Manager die Schlüsselwort-Wert-Paar DSN = Standard. (Dieses Dialogfeld wird eine Datenquelle mit dem Namen "Default" nicht angezeigt.)  
  
-   SQL_DRIVER_COMPLETE oder sql_driver_complete_required lautet: Wenn von der Anwendung angegebene Verbindungszeichenfolge enthält die **DSN** Schlüsselwort der Treiber-Manager kopiert die Verbindungszeichenfolge, die von der Anwendung angegeben. Anderenfalls wird die gleichen Aktionen wie beim *DriverCompletion* SQL_DRIVER_PROMPT ist.  
  
-   SQL_DRIVER_NOPROMPT: Der Treiber-Manager kopiert die Verbindungszeichenfolge, die von der Anwendung angegeben.  
  
 Wenn von der Anwendung angegebene Verbindungszeichenfolge enthält die **Treiber** Schlüsselwort der Treiber-Manager kopiert die Verbindungszeichenfolge, die von der Anwendung angegeben.  
  
 Verwenden die Verbindungszeichenfolge, die es erstellt wurde, der Treiber-Manager bestimmt, welche Treiber verwendet, eine Verbindung mit diesen Treiber her und übergibt die Verbindungszeichenfolge, die es erstellt wurde, an den Treiber; Weitere Informationen zur Interaktion der Treiber-Manager und der Treiber finden Sie im Abschnitt "Kommentare" [SQLConnect-Funktion](../../../odbc/reference/syntax/sqlconnect-function.md). Wenn keine die Verbindungszeichenfolge enthält der **Treiber** Schlüsselwort der Treiber-Manager bestimmt, welcher Treiber wie folgt verwenden:  
  
1.  Wenn die Verbindungszeichenfolge enthält die **DSN** -Schlüsselwort, ruft der Treiber-Manager ab, der Treiber die Datenquelle aus der Systeminformationen zugeordnet.  
  
2.  Wenn keine die Verbindungszeichenfolge enthält der **DSN** Schlüsselwort oder die Datenquelle nicht gefunden wird, der Treiber-Manager ruft des Treibers die Standarddatenquelle aus der Systeminformationen zugeordnet. (Weitere Informationen finden Sie unter [Standard Unterschlüssel](../../../odbc/reference/install/default-subkey.md).) Der Treiber-Manager ändert den Wert für die **DSN** Schlüsselwort in der Verbindungszeichenfolge auf "DEFAULT".  
  
3.  Wenn die **DSN** Schlüsselwort in der Verbindungszeichenfolge auf "Standard" festgelegt ist, wird der Treiber-Manager ruft des Treibers die Standarddatenquelle aus der Systeminformationen zugeordnet.  
  
4.  Wenn die Datenquelle wurde nicht gefunden, und die Standarddatenquelle wurde nicht gefunden, gibt der Treiber-Manager SQL_ERROR mit SQLSTATE IM002 (Datenquelle wurde nicht gefunden und kein Standardtreiber angegeben).  
  
## <a name="file-data-sources"></a>Dateidatenquellen  
 Wenn die Verbindungszeichenfolge von der Anwendung im Aufruf angegeben **SQLDriverConnect** enthält die **FILEDSN** -Schlüsselwort verwenden und dieses Schlüsselwort wird nicht ersetzt, entweder durch die **DSN**oder **Treiber** -Schlüsselwort, und klicken Sie dann auf den Treiber-Manager erstellt eine Verbindungszeichenfolge, die anhand der Informationen in den DSN-Datei und die *InConnectionString* Argument. Der Treiber-Manager wird wie folgt aus:  
  
1.  Überprüft, ob der Dateiname der DSN-Datei gültig ist. Wenn nicht der Fall, wird SQL_ERROR mit SQLSTATE IM014 zurückgegeben (Ungültiger Name der Datei-DSN). Der Dateiname ist eine leere Zeichenfolge ("") und SQL_DRIVER_NOPROMPT ist nicht angegeben wird, und klicken Sie dann die **geöffneten Datei** Dialogfeld wird angezeigt. Wenn der Dateiname einen gültigen Pfad jedoch kein Dateiname oder ein ungültiger Dateiname enthält und SQL_DRIVER_NOPROMPT nicht angegeben ist, und klicken Sie dann die **geöffneten Datei** Dialogfeld wird angezeigt, mit dem aktuellen Verzeichnis im Dateinamen angegebene festgelegt. Der Dateiname ist eine leere Zeichenfolge ("") oder der Dateiname enthält einen gültigen Pfad jedoch kein Dateiname oder ein ungültiger Dateiname SQL_DRIVER_NOPROMPT angegeben ist, und dann wird SQL_ERROR mit SQLSTATE IM014 zurückgegeben (Ungültiger Name der Datei-DSN).  
  
2.  Liest alle Schlüsselwörter im Abschnitt [ODBC], der die DSN-Datei an. Wenn die **Treiber** Schlüsselwort ist nicht vorhanden, es gibt SQL_ERROR mit SQLSTATE IM012 (Driver-Schlüsselwort Syntaxfehler), mit Ausnahme von, in dem die DSN-Datei ist Dateidatenquelle und enthält daher nur die **DSN** Schlüsselwort.  
  
     Wenn die Datei als Datenquelle Dateidatenquelle ist, liest der Treiber-Manager den Wert der **DSN** Schlüsselwort und nach Bedarf, um die Benutzer- oder Systemdaten-Datenquelle verweist, zu der Dateidatenquelle verbindet. Die Schritte 3 bis 5 werden nicht ausgeführt.  
  
3.  Erstellt eine Verbindungszeichenfolge für den Treiber an. Die Treiber-Verbindungszeichenfolge ist die Kombination der Schlüsselwörter in der DSN-Datei angegeben und die in die ursprüngliche Verbindungszeichenfolge für die Anwendung. Regeln für die Erstellung der Treiber-Verbindungszeichenfolge, die Schlüsselwörter, die sich überlappen sind wie folgt aus:  
  
    -   Wenn die **Treiber** Schlüsselwort vorhanden ist, in der Verbindungszeichenfolge der Anwendung und die Treiber, die gemäß der **Treiber** Schlüsselwörter sind nicht in die DSN-Datei und die Verbindungszeichenfolge der Anwendung, die Treiberinformationen in der DSN-Datei wird ignoriert, und die Treiberinformationen in der Verbindungszeichenfolge für die Anwendung dient. Wenn die Treiber, wird angegeben die **Treiber** Schlüsselwort entsprechen den in der DSN-Datei und die Verbindungszeichenfolge für die Anwendung, und klicken Sie dann bei allen Schlüsselwörtern überlappen ist, in der Verbindungszeichenfolge der Anwendung angegebenen haben Vorrang vor den in der DSN-Datei angegeben.  
  
    -   In der neuen Verbindungszeichenfolge die **FILEDSN** Schlüsselwort wird eliminiert.  
  
4.  Wird der Treiber anhand der im Registrierungseintrag HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCINST geladen. INI\\< Treibername\>\Driver, in denen \<Treibername > wird angegeben, indem die **Treiber** Schlüsselwort.  
  
5.  Wird dem Treiber die neue Verbindungszeichenfolge übergeben.  
  
 Beispiele für die DSN-Dateien finden Sie unter [Herstellen einer Verbindung mithilfe von Dateidatenquellen](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md).  
  
## <a name="savefile-keyword"></a>SAVEFILE-Schlüsselwort  
 Wenn von der Anwendung angegebene Verbindungszeichenfolge enthält die **SAVEFILE** -Schlüsselwort, und klicken Sie dann auf den Treiber-Manager speichert die Verbindungszeichenfolge in einer DSN-Datei. Der Treiber-Manager wird wie folgt aus:  
  
1.  Überprüft, ob der Dateiname der DSN-Datei als den Wert des Attributs enthalten die **SAVEFILE** -Schlüsselwort ist gültig. Wenn nicht der Fall, wird SQL_ERROR mit SQLSTATE IM014 zurückgegeben (Ungültiger Name der Datei-DSN). Die Gültigkeit des Dateinamens wird durch die Benennungsregeln Standardbetriebssystem bestimmt. Der Dateiname ist eine leere Zeichenfolge ("") und die *DriverCompletion* Argument nicht SQL_DRIVER_NOPROMPT, wird der Dateiname ist ungültig. Wenn der Dateiname bereits, wenn vorhanden ist *DriverCompletion* SQL_DRIVER_NOPROMPT lautet, wird die Datei überschrieben. Wenn *DriverCompletion* SQL_DRIVER_PROMPT, SQL_DRIVER_COMPLETE oder sql_driver_complete_required lautet, wird ein Dialogfeld fordert den Benutzer an, ob die Datei überschrieben werden soll. Wenn kein Wert eingegeben wird, und klicken Sie dann die **Datei zu speichern,** Dialogfeld wird angezeigt.  
  
2.  Wenn der Treiber gibt SQL_SUCCESS zurück, der Dateiname eine leere Zeichenfolge war, und der Treiber-Manager die Verbindungsinformationen, die zurückgegeben werden schreibt, der *OutConnectionString* Argument an die angegebene Datei mit dem Format im angegebenen Abschnitt "Verbindungszeichenfolgen" weiter oben in diesem Abschnitt.  
  
3.  Wenn der Treiber gibt SQL_SUCCESS zurück, und der Dateiname eine leere Zeichenfolge ist (""), und der Treiber-Manager ruft dann die **Datei zu speichern,** Standarddialogfeld mit der *Hwnd* angegeben und schreibt die Verbindungsinformationen im zurückgegebenen *OutConnectionString* in die Datei in das Standarddialogfeld Datei zu speichern, mit dem im Abschnitt "Verbindungszeichenfolgen" weiter oben in diesem Abschnitt angegebenen Format angegeben.  
  
4.  Wenn der Treiber gibt SQL_SUCCESS zurück, gibt die *OutConnectionString* Argument, das die Verbindungszeichenfolge für die Anwendung enthält.  
  
5.  Wenn der Treiber gibt SQL_SUCCESS_WITH_INFO oder SQL_ERROR zurück, gibt der Treiber-Manager den SQLSTATE an die Anwendung zurück.  
  
## <a name="driver-guidelines"></a>Treiber-Richtlinien  
 Der Treiber überprüft, ob die Verbindungszeichenfolge übergeben wird vom Treiber-Manager enthält die **DSN** oder **Treiber** Schlüsselwort. Wenn die Verbindungszeichenfolge enthält die **Treiber** Schlüsselwort der Treiber kann keine Informationen über die Datenquelle von der Systeminformationen abrufen. Wenn die Verbindungszeichenfolge enthält die **DSN** Schlüsselwort oder enthält keine der **DSN** oder **Treiber** -Schlüsselwort, der Treiber Abrufen von Informationen über die Datenquelle über die Systeminformationen wie folgt:  
  
1.  Wenn die Verbindungszeichenfolge enthält die **DSN** Schlüsselwort, das der Treiber Ruft die Informationen für die angegebene Datenquelle ab.  
  
2.  Wenn keine die Verbindungszeichenfolge enthält der **DSN** -Schlüsselwort, das die angegebene Datenquelle wurde nicht gefunden, oder die **DSN** Schlüsselwort "DEFAULT" festgelegt ist, ruft der Treiber die Informationen für die Standarddatenquelle .  
  
 Der Treiber verwendet die Daten, die abgerufen, von der Systeminformationen zu erweitern, die Informationen in der Verbindungszeichenfolge übergeben. Wenn die Informationen in die Systeminformationen Informationen in der Verbindungszeichenfolge dupliziert, verwendet der Treiber die Informationen in der Verbindungszeichenfolge angegeben.  
  
 Basierend auf den Wert der *DriverCompletion*, der Treiber fordert den Benutzer für die Verbindungsinformationen, z. B. die Benutzer-ID und Kennwort, und eine Verbindung mit der Datenquelle her:  
  
-   SQL_DRIVER_PROMPT: Der Treiber zeigt ein Dialogfeld mit den Werten aus den Verbindungsinformationen für Zeichenfolgen- und System (sofern vorhanden) als Anfangswerte. Wenn der Benutzer das Dialogfeld schließt, verbindet der Treiber mit der Datenquelle. Es erstellt außerdem eine Verbindungszeichenfolge aus dem Wert des der **DSN** oder **Treiber** -Schlüsselwort in \* *InConnectionString* und die Informationen zurückgegeben, die von der Das Dialogfeld. Speichert diese Verbindungszeichenfolge in der **OutConnectionString* Puffer.  
  
-   SQL_DRIVER_COMPLETE oder sql_driver_complete_required lautet: die Verbindungszeichenfolge genügend Informationen enthält, und diese Informationen korrekt ist, der Treiber stellt eine Verbindung mit der Datenquelle und die Kopien \* *InConnectionString*auf \* *OutConnectionString*. Wenn alle Informationen, die fehlen oder falsch ist, führt der Treiber die gleichen Aktionen an, wie beim *DriverCompletion* ist SQL_DRIVER_PROMPT, außer dass bei *DriverCompletion* SQL_DRIVER_COMPLETE_ ist ERFORDERLICH, deaktiviert der Treiber die Steuerelemente für alle Informationen, die nicht für die Verbindung mit der Datenquelle erforderlich sind.  
  
-   SQL_DRIVER_NOPROMPT: Die Verbindungszeichenfolge genügend Informationen enthält, der Treiber stellt eine Verbindung mit der Datenquelle und die Kopien \* *InConnectionString* auf \* *OutConnectionString*. Andernfalls gibt der Treiber SQL_ERROR für **SQLDriverConnect**.  
  
 Bei erfolgreichen Verbindung zur Datenquelle, setzt der Treiber auch \* *StringLength2Ptr* auf die Länge der Ausgabe-Verbindungszeichenfolge, die für die zurückzugebenden in verfügbar ist **OutConnectionString*.  
  
 Wenn der Benutzer ein Dialogfeld, das der Treiber-Manager oder der Treiber vorgelegte abbricht **SQLDriverConnect** gibt SQL_NO_DATA zurück.  
  
 Informationen über die Interaktion zwischen der Treiber-Manager und der Treiber während des Verbindungsvorgangs finden Sie unter [SQLConnect-Funktion](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
 Wenn ein Treiber unterstützt **SQLDriverConnect**, muss der Treiber Schlüsselwort Teil die Systeminformationen für den Treiber enthalten die **ConnectFunctions** Schlüsselwort mit dem zweiten Zeichen "Y" festgelegt.  
  
## <a name="connecting-when-connection-pooling-is-enabled"></a>Herstellen einer Verbindung bei aktiviertem Verbindungspooling  
 Verbindungs-pooling kann eine Anwendung eine Verbindung wiederzuverwenden, die bereits erstellt wurde. Wenn **SQLDriverConnect** aufgerufen wird, wird der Treiber-Manager versucht, zum Herstellen der Verbindung mit einer Verbindung, der einen Pool von Verbindungen in einer Umgebung gehört, die für das Verbindungspooling festgelegt wurde. Weitere Informationen zum Verbindungspooling finden Sie unter [SQLConnect-Funktion](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
 Eine Anwendung kann SQL_ATTR_RESET_CONNECTION vor dem Aufrufen von SQLDisconnect für eine Verbindung ist aktiviert, in dem festgelegt. Weitere Informationen finden Sie unter [Funktion SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md).  
  
 Die folgenden Einschränkungen gelten, wenn eine Anwendung ruft **SQLDriverConnect** für eine gepoolte Verbindung die Verbindung:  
  
-   Keine Verbindungspooling Verarbeitung erfolgt bei der **SAVEFILE** -Schlüsselwort in der Verbindungszeichenfolge angegeben ist.  
  
-   Wenn Verbindungspooling aktiviert ist, **SQLDriverConnect** kann aufgerufen werden, nur mit einer *DriverCompletion* Argument SQL_DRIVER_NOPROMPT; Wenn **SQLDriverConnect** wird aufgerufen Bei einem anderen *DriverCompletion*, SQLSTATE HY110 (Ungültiger Treiberabschluss) zurückgegeben werden.  
  
## <a name="connection-attributes"></a>Verbindungsattribute  
 Das Verbindungsattribut SQL_ATTR_LOGIN_TIMEOUT, legen Sie mithilfe von **SQLSetConnectAttr**, definiert die Anzahl der Sekunden für eine anmeldeanforderung, mit der eine erfolgreiche Verbindung vom Treiber abzuschließen, bevor Sie an die Anwendung zurückgegeben. Wenn der Benutzer aufgefordert wird, um die Verbindungszeichenfolge abzuschließen, startet eine Wartezeit für jede Anforderung für die Anmeldung bei der Treiber die Verbindung Prozessstart.  
  
 Der Treiber die Verbindung im Zugriffsmodus SQL_MODE_READ_WRITE standardmäßig geöffnet. Den Zugriffsmodus auf SQL_MODE_READ_ONLY festlegen möchten, muss die Anwendung aufrufen **SQLSetConnectAttr** mit dem Attribut SQL_ATTR_ACCESS_MODE vor dem Aufruf **SQLDriverConnect**.  
  
 Wenn eine Übersetzung Standardbibliothek in die Systeminformationen für die Datenquelle angegeben wird, wird Sie von der Treiber geladen. Kann einen anderen übersetzungsbibliothek geladen werden, durch den Aufruf **SQLSetConnectAttr** mit SQL_ATTR_TRANSLATE_LIB-Attribut. Eine Übersetzungsoption kann angegeben werden, durch den Aufruf **SQLSetConnectAttr** mit der Option SQL_ATTR_TRANSLATE_OPTION.  
  
 Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit SQLDriverConnect](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md).  
  
```  
// SQLDriverConnect_ref.cpp  
// compile with: odbc32.lib user32.lib  
#include <windows.h>  
#include <sqlext.h>  
  
int main() {  
   SQLHENV henv;  
   SQLHDBC hdbc;  
   SQLHSTMT hstmt;  
   SQLRETURN retcode;  
  
   SQLCHAR OutConnStr[255];  
   SQLSMALLINT OutConnStrLen;  
  
   HWND desktopHandle = GetDesktopWindow();   // desktop's window handle  
  
   // Allocate environment handle  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
  
   // Set the ODBC version environment attribute  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
      retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
  
      // Allocate connection handle  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
         retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
  
         // Set login timeout to 5 seconds  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
            SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
            retcode = SQLDriverConnect( // SQL_NULL_HDBC  
               hdbc,   
               desktopHandle,   
               (SQLCHAR*)"driver=SQL Server",   
               _countof("driver=SQL Server"),  
               OutConnStr,  
               255,   
               &OutConnStrLen,  
               SQL_DRIVER_PROMPT );  
  
            // Allocate statement handle  
            if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {                 
               retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);   
  
               // Process data  
               if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
                  SQLFreeHandle(SQL_HANDLE_STMT, hstmt);  
               }  
  
               SQLDisconnect(hdbc);  
            }  
  
            SQLFreeHandle(SQL_HANDLE_DBC, hdbc);  
         }  
      }  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
   }  
}  
```  
  
 Siehe auch [ODBC-Beispielprogramm](../../../odbc/reference/sample-odbc-program.md).  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Ein Handle zuordnen|[SQLAllocHandle-Funktion](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Ermitteln und Auflisten von Werten, die für die Verbindung mit einer Datenquelle|[SQLBrowseConnect-Funktion](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|Herstellen einer Verbindung mit einer Datenquelle|[SQLConnect-Funktion](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|Trennen von einer Datenquelle|[SQLDisconnect-Funktion](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|Zurückgeben von Beschreibungen der Treiber-Attribute|[SQLDrivers-Funktion](../../../odbc/reference/syntax/sqldrivers-function.md)|  
|Ein Handle freigeben|[SQLFreeHandle-Funktion](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|Ein Verbindungsattribut festlegen|[SQLSetConnectAttr-Funktion](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)

---
title: SQLSetConnectAttr-Funktion | Microsoft Docs
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
apiname: SQLSetConnectAttr
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLSetConnectAttr
helpviewer_keywords: SQLSetConnectAttr function [ODBC]
ms.assetid: 97fc7445-5a66-4eb9-8e77-10990b5fd685
caps.latest.revision: "83"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 806acdd35452ff22e922158ed071d41d8e45f031
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="sqlsetconnectattr-function"></a>SQLSetConnectAttr-Funktion
**Konformität**  
 Version eingeführt: ODBC 3.0 Standardkonformität: ISO-92  
  
 **Zusammenfassung**  
 **SQLSetConnectAttr** Legt Attribute, die Aspekte der Verbindungen zu steuern.  
  
> [!NOTE]  
>  Weitere Informationen, was der Treiber-Manager diese Funktion auf, wenn eine ODBC 3. ordnet*.x* Anwendung arbeitet mit einer ODBC 2.*.x* -Treiber verwenden, finden Sie unter [Ersatzfunktionen für rückwärts zuordnen Die Kompatibilität der Anwendungen](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLSetConnectAttr(  
     SQLHDBC       ConnectionHandle,  
     SQLINTEGER    Attribute,  
     SQLPOINTER    ValuePtr,  
     SQLINTEGER    StringLength);  
```  
  
## <a name="arguments"></a>Argumente  
 *Verbindungshandle*  
 [Eingabe] Verbindungshandle.  
  
 *Attribut*  
 [Eingabe] Attribut, das festgelegt wird, aufgelistet in "Kommentare".  
  
 *ValuePtr*  
 [Eingabe] Zeiger auf den Wert zugeordnet werden *Attribut*. Abhängig vom Wert der *Attribut*, *ValuePtr* werden unsigned Integer-Wert, oder zeigen auf eine Null-terminierte Zeichenfolge. Beachten Sie, die der ganzzahligen Typ der *Attribut* Argument Länge nicht behoben finden Sie im Abschnitt "Kommentare" auf Details.  
  
 *StringLength*  
 [Eingabe] Wenn *Attribut* ist ein ODBC-definierten Attribut und *ValuePtr* zeigt auf eine Zeichenfolge oder einen binären Puffer, in dieses Argument muss die Länge des **ValuePtr*. Für Zeichenfolgendaten sollte dieses Argument die Anzahl der Bytes in der Zeichenfolge enthalten.  
  
 Wenn *Attribut* ist ein ODBC-definierten Attribut und *ValuePtr* ist eine ganze Zahl *StringLength* wird ignoriert.  
  
 Wenn *Attribut* ist ein Attribut treiberdefinierten die Anwendung zeigt die Art des Attributs an den Treiber-Manager an, indem die *StringLength* Argument. *StringLength* können die folgenden Werte aufweisen:  
  
-   Wenn *ValuePtr* ist ein Zeiger auf eine Zeichenfolge *StringLength* ist die Länge der Zeichenfolge oder SQL_NTS.  
  
-   Wenn *ValuePtr* ist ein Zeiger auf einen binären Puffer, und klicken Sie dann die Anwendung das Ergebnis von der SQL_LEN_BINARY_ATTR eingefügt (*Länge*)-Makro im *StringLength*. Dies setzt einen negativen Wert in *StringLength*.  
  
-   Wenn *ValuePtr* ist ein Zeiger auf einen anderen Wert als eine Zeichenfolge oder eine binäre Zeichenfolge *StringLength* müssen den Wert SQL_IS_POINTER.  
  
-   Wenn *ValuePtr* enthält einen Wert fester Länge *StringLength* ist SQL_IS_INTEGER oder SQL_IS_UINTEGER, nach Bedarf.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE oder SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLSetConnectAttr** gibt SQL_ERROR oder SQL_SUCCESS_WITH_INFO, einen zugeordneten SQLSTATE-Wert abgerufen werden können, durch den Aufruf **SQLGetDiagRec** mit einem *HandleType* von SQL_HANDLE_DBC und ein *behandeln* von *Verbindungshandle*. Die folgende Tabelle enthält die SQLSTATE-Werten, die häufig zurückgegebenes **SQLSetConnectAttr** und erläutert, jeweils im Kontext dieser Funktion; die Notation "(DM)" vorangestellt ist, die Beschreibungen der SQLSTATEs, die vom Treiber-Manager zurückgegeben. Der Rückgabecode, der jeden SQLSTATE-Wert zugeordnet wird SQL_ERROR zurückgegeben, sofern nicht anders angegeben.  
  
 Der Treiber kann SQL_SUCCESS_WITH_INFO zurück, um Informationen zum Ergebnis der Festlegen einer Option zurück.  
  
|SQLSTATE|Fehler|Description|  
|--------------|-----------|-----------------|  
|01000|Allgemeine Warnung|Treiberspezifische Meldung dient zu Informationszwecken. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|01 S 02|Der Optionswert wurde geändert|Der Treiber nicht den Wert im angegebenen *ValuePtr* und einen ähnlichen Wert ersetzt. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|08002|Name der Verbindung verwendet|Die *Attribut* Argument wurde SQL_ATTR_ODBC_CURSORS und der Treiber wurde bereits mit der Datenquelle verbunden.|  
|08003|Verbindung nicht geöffnet|(DM) eine *Attribut* Wert wurde angegeben, die eine geöffnete Verbindung erforderlich, aber die *Verbindungshandle* war nicht verbunden.|  
|08S01|Kommunikations-Verbindungsfehler|Die Verbindung zwischen dem Treiber und die Datenquelle mit der der Treiber verbunden wurde aufgetreten ist, bevor die Verarbeitung für die Funktion abgeschlossen.|  
|24000|Ungültiger Cursorstatus|Die *Attribut* Argument SQL_ATTR_CURRENT_CATALOG und ein Resultset wurde ausstehend.|  
|25000|Ungültiger Vorgang in einer lokalen Transaktion|Eine Verbindung wurde in einer lokalen Transaktion beim Versuch, eine Eintragung in einer verteilten transaktionsverbindung (DTC) durch Festlegen des SQL_ATTR_ENLIST_IN_DTC-Verbindungsattribut.<br /><br /> Eine Verbindung ist bereits in einem DTC eingetragen.<br /><br /> Eine Verbindung wurde in einer verteilten transaktionsverbindung eingetragen, und eine lokale Transaktion wurde gestartet, indem Sie SQL_ATTR_AUTOCOMMIT auf SQL_AUTOCOMMIT_OFF festlegen.|  
|3D000|Ungültiger Katalogname|Die *Attribut* Argument wurde SQL_CURRENT_CATALOG und der Name des angegebenen Katalogs war ungültig.|  
|HY000|Allgemeiner Fehler|Für die es keine spezifischen SQLSTATE wurde und für die keine implementierungsabhängige SQLSTATE definiert wurde, ist ein Fehler aufgetreten. Die zurückgegebene Fehlermeldung **SQLGetDiagRec** in der  *\*MessageText* Puffer beschreibt den Fehler und seiner Ursache.|  
|HY001|Fehler bei der speicherbelegung|Der Treiber konnte nicht belegt werden zur Unterstützung der Ausführung oder den Abschluss der Funktion erforderlich.|  
|HY008|Der Vorgang wurde abgebrochen|Asynchroner Verarbeitung wurde aktiviert, für die *Verbindungshandle*. Die **SQLSetConnectAttr** Funktion aufgerufen wurde, und bevor es ausgeführt wurden, die [SQLCancelHandle-Funktion](../../../odbc/reference/syntax/sqlcancelhandle-function.md) aufgerufen wurde, auf die *Verbindungshandle*, und klicken Sie dann die **SQLSetConnectAttr** Funktion erneut aufgerufen wurde, auf die *Verbindungshandle*.<br /><br /> Or **SQLSetConnectAttr** Funktion aufgerufen wurde, und bevor es ausgeführt wurden, **SQLCancelHandle** aufgerufen wurde, auf die *Verbindungshandle* aus einem anderen Thread in eine multithread-Anwendung.|  
|HY009|Ungültige Verwendung des null-Zeiger|Die *Attribut* Argument identifiziert ein Verbindungsattribut, die einen Zeichenfolgenwert erforderlich und die *ValuePtr* Argument wurde ein null-Zeiger.|  
|HY010|Fehler bei Funktionssequenz|(DM) hieß eine asynchron ausgeführte Funktion für eine *StatementHandle* zugeordneten der *Verbindungshandle* und wurde noch ausgeführt, wenn **SQLSetConnectAttr**aufgerufen wurde.<br /><br /> (DM) hieß eine asynchron ausgeführte Funktion (nicht auf dieses Objekt) für die *Verbindungshandle* und wurde noch ausgeführt werden, wenn diese Funktion aufgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, oder **SQLMoreResults** für eines der zugeordneten Anweisungshandles hieß die *Verbindungshandle* und SQL_PARAM_DATA_AVAILABLE zurückgegeben. Diese Funktion wurde aufgerufen, bevor Daten für alle gestreamte Parameter abgerufen wurde.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oder **SQLSetPos** wurde aufgerufen, eine *StatementHandle*  zugeordneten der *Verbindungshandle* und SQL_NEED_DATA zurückgegeben. Diese Funktion wurde aufgerufen, bevor die Daten für alle Data-at-Execution-Parameter oder Spalten gesendet wurden.<br /><br /> (DM) **SQLBrowseConnect** wurde aufgerufen, die *Verbindungshandle* und SQL_NEED_DATA zurückgegeben. Diese Funktion aufgerufen wurde, bevor **SQLBrowseConnect** SQL_SUCCESS_WITH_INFO oder SQL_SUCCESS zurückgegeben.|  
|HY011|Attribut kann jetzt nicht festgelegt werden|Die *Attribut* Argument war SQL_ATTR_TXN_ISOLATION und eine Transaktion geöffnet wurde.|  
|HY013|Speicherverwaltungsfehler|Der Funktionsaufruf konnte nicht verarbeitet werden, da die zugrunde liegenden Speicherobjekte, möglicherweise aufgrund von unzureichendem Speicher konnte nicht zugegriffen werden.|  
|HY024|Ungültiger Attributwert|Berücksichtigung des angegebenen *Attribut* Wert, ein ungültiger Wert wurde angegeben, *ValuePtr*. (Der Treiber-Manager gibt SQLSTATE nur für Verbindungs- und Anweisungsattribute, die einen diskreten Satz von Werten, z. B. SQL_ATTR_ACCESS_MODE oder SQL_ATTR_ASYNC_ENABLE zu akzeptieren. Für alle anderen Verbindungs- und Anweisungsattribute der Treiber muss überprüfen Sie den Wert im angegebenen *ValuePtr*.)<br /><br /> Die *Attribut* Argument war SQL_ATTR_TRACEFILE oder SQL_ATTR_TRANSLATE_LIB, und *ValuePtr* wurde eine leere Zeichenfolge.|  
|HY090|Ungültige Zeichenfolgen- oder Pufferlänge.|*(DM) \*ValuePtr* ist eine Zeichenfolge, und die *StringLength* Argument war kleiner als 0 jedoch war nicht SQL_NTS.|  
|HY092|Ungültiger Attribut-/Optionsbezeichner|(DM) der Wert für das Argument angegebene *Attribut* war für die vom Treiber unterstützten ODBC-Version ungültig.<br /><br /> (DM) der Wert für das Argument angegebene *Attribut* wurde eine nur-Lese Attribut.|  
|HY114|Verbindungsebene asynchrone Ausführung unterstützt-Treiber nicht.|(DM) versucht eine Anwendung, die asynchrone Ausführung mit SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE für einen Treiber zu aktivieren, die asynchrone Verbindungsvorgänge nicht unterstützt.|  
|HY117|Verbindung wird aufgrund eines unbekannten Transaktionsstatus angehalten. Nur trennen, und nur-Lese Funktionen sind zulässig.|(DM) finden Sie weitere Informationen zum Zustand "angehalten" [SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HY121|Cursorbibliothek und Treiberfähiges Verbindungspooling können nicht gleichzeitig aktiviert werden|Weitere Informationen finden Sie unter [Treiberfähiges Verbindungspooling](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md).|  
|HYC00|Optionales Feature nicht implementiert|Der Wert für das Argument angegebene *Attribut* wurde eine ODBC-Verbindung oder für die Version des ODBC-Anweisungsattribut vom Treiber unterstützt, jedoch wurde vom Treiber nicht unterstützt.|  
|HYT01|Verbindungstimeout abgelaufen|Das Verbindungstimeout ist abgelaufen, bevor die Datenquelle auf die Anforderung geantwortet hat. Das Verbindungstimeout wird über festgelegt **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Diese Funktion wird im Treiber nicht unterstützt.|(DM) der Treiber verknüpft sind, mit der *Verbindungshandle* der Funktion nicht unterstützt.|  
|IM009|Kann nicht geladen werden Konvertierungs-DLL|Der Treiber konnte den Konvertierungs-DLL zu laden, die für die Verbindung angegeben wurde. Dieser Fehler kann zurückgegeben, wenn Sie nur, wenn *Attribut* SQL_ATTR_TRANSLATE_LIB wird.|  
|IM017|Abrufintervall ist im Modus für asynchrone Benachrichtigung deaktiviert.|Sobald das Benachrichtigungsmodell verwendet wird, ist die Abruf deaktiviert.|  
|IM018|**SQLCompleteAsync** nicht zum Abschließen des vorherigen asynchrone Vorgangs auf diesem Handle aufgerufen wurde.|Wenn die vorherigen Funktionsaufruf auf das Handle SQL_STILL_EXECUTING zurückgibt und Benachrichtigungsmodus aktiviert ist, **SQLCompleteAsync** muss aufgerufen werden, auf das Handle nach der Verarbeitung und der Vorgang abgeschlossen werden.|  
|S1118|Asynchrone Benachrichtigung unterstützt-Treiber nicht.|SQL_ATTR_ASYNC_DBC_EVENT (nachdem die Verbindung hergestellt wurde) festgelegt wurde, aber die asynchrone Benachrichtigung wird vom Treiber nicht unterstützt.|  
  
 Wenn *Attribut* ist ein Anweisungsattribut **SQLSetConnectAttr** kann eine beliebige SQLSTATEs zurückgegebenes zurückgeben **SQLSetStmtAttr**.  
  
## <a name="comments"></a>Kommentare  
 Allgemeine Informationen zu Verbindungsattributen finden Sie unter [Verbindungsattribute](../../../odbc/reference/develop-app/connection-attributes.md).  
  
 Die aktuell definierten Attribute und die Version von ODBC, in denen sie eingeführt wurden, werden in der Tabelle weiter unten in diesem Abschnitt angezeigt. Es wird erwartet, dass weitere Attribute definiert werden, um Daten von verschiedenen Datenquellen nutzen. ODBC ist ein Bereich von Attributen reserviert. Entwickler müssen Werte für die eigene Verwendung treiberspezifische von Open Group reservieren.  
  
> [!NOTE]  
>  Die Fähigkeit zum Festlegen von Anweisungsattribute auf der Verbindungsebene durch Aufrufen von **SQLSetConnectAttr** ist in ODBC 3. veraltet*.x*. ODBC 3.*.x* Anwendungen Anweisungsattribute auf Verbindungsebene darf nicht festgelegt werden. ODBC 3.*.x* Anweisungsattribute können nicht auf Verbindungsebene, mit Ausnahme der SQL_ATTR_METADATA_ID und SQL_ATTR_ASYNC_ENABLE-Attribute, die Verbindungsattribute und Anweisungsattribute sind und können nicht festgelegt werden Legen Sie auf der Verbindungsebene oder Anweisungsebene.  
>   
>  ODBC 3.*.x* Treiber müssen nur diese Funktionalität unterstützen, wenn sie mit ODBC 2. arbeiten sollten*.x* Anwendung, die ODBC 2. festlegt*.x* Anweisungsoptionen auf Verbindungsebene. Weitere Informationen finden Sie unter [SQLSetConnectOption Zuordnung](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md) in Anhang G: Treiber Richtlinien für die Abwärtskompatibilität.  
  
 Eine Anwendung kann Aufrufen **SQLSetConnectAttr** zu einem beliebigen Zeitpunkt zwischen dem Zeitpunkt die Verbindung zugeordnet und freigegeben wird. Alle Verbindungs- und Attribute, die von der Anwendung für die Verbindung erfolgreich festgelegt bleiben, bis **SQLFreeHandle** für die Verbindung aufgerufen wird. Z. B. wenn eine Anwendung ruft **SQLSetConnectAttr** vor dem Verbinden mit einer Datenquelle, behält das Attribut selbst wenn **SQLSetConnectAttr** im Treiber schlägt fehl, wenn die Anwendung eine Verbindung herstellt der Datenquelle Wenn eine Anwendung eine treiberspezifische Attribut festlegt, behält das Attribut, selbst wenn die Anwendung auf einen anderen Treiber für die Verbindung herstellt.  
  
 Einige Verbindungsattribute können festgelegt werden, nur verwendet werden, bevor eine Verbindung hergestellt wurde. andere können festgelegt werden, nachdem eine Verbindung hergestellt wurde. Die folgende Tabelle zeigt die Verbindungsattribute, die festgelegt werden müssen, bevor oder nachdem eine Verbindung hergestellt wurde. *Entweder* gibt an, dass das Attribut entweder vor oder nach der Verbindung festgelegt werden kann.  
  
|attribute|Legen Sie vor oder nach Verbindung?|  
|---------------|-------------------------------------|  
|SQL_ATTR_ACCESS_MODE|Entweder [1]|  
|SQL_ATTR_ASYNC_DBC_EVENT|Sowohl als auch|  
|SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE|Entweder [4]|  
|SQL_ATTR_ASYNC_DBC_PCALLBACK|Sowohl als auch|  
|SQL_ATTR_ASYNC_DBC_PCONTEXT|Sowohl als auch|  
|SQL_ATTR_ASYNC_ENABLE|[2]|  
|SQL_ATTR_AUTO_IPD|Sowohl als auch|  
|SQL_ATTR_AUTOCOMMIT|Entweder [5]|  
|SQL_ATTR_CONNECTION_DEAD|Nach|  
|SQL_ATTR_CONNECTION_TIMEOUT|Sowohl als auch|  
|SQL_ATTR_CURRENT_CATALOG|Entweder [1]|  
|SQL_ATTR_DBC_INFO_TOKEN|Nach|  
|SQL_ATTR_ENLIST_IN_DTC|Nach|  
|SQL_ATTR_LOGIN_TIMEOUT|vor|  
|SQL_ATTR_METADATA_ID|Sowohl als auch|  
|SQL_ATTR_ODBC_CURSORS|vor|  
|SQL_ATTR_PACKET_SIZE|vor|  
|SQL_ATTR_QUIET_MODE|Sowohl als auch|  
|SQL_ATTR_TRACE|Sowohl als auch|  
|SQL_ATTR_TRACEFILE|Sowohl als auch|  
|SQL_ATTR_TRANSLATE_LIB|Nach|  
|SQL_ATTR_TRANSLATE_OPTION|Nach|  
|SQL_ATTR_TXN_ISOLATION|Entweder [3]|  
  
 [1] SQL_ATTR_ACCESS_MODE und SQL_ATTR_CURRENT_CATALOG kann vor oder nach dem Herstellen einer Verbindung, je nach den Treiber festgelegt werden. Allerdings festgelegt interoperable Anwendungen ausführen können sie vor dem Herstellen einer Verbindung, da einige Treiber nicht unterstützen, ändern diese nach dem Herstellen einer Verbindung.  
  
 [2] SQL_ATTR_ASYNC_ENABLE muss festgelegt werden, bevor es eine aktive Anweisung ist.  
  
 [3] SQL_ATTR_TXN_ISOLATION kann festgelegt werden, nur dann, wenn keine offenen für die Verbindung Transaktionen. Einige Verbindungsattribute unterstützen einen ähnlichen Wert ersetzen, wenn die Datenquelle im angegebene Wert nicht unterstützt \* *ValuePtr*. In solchen Fällen gibt der Treiber SQL_SUCCESS_WITH_INFO und SQLSTATE 01 s 02 (Optionswert wurde geändert). Z. B. wenn *Attribut* ist SQL_ATTR_PACKET_SIZE und \* *ValuePtr* überschreitet die maximale Paketgröße, die der Treiber ersetzt die maximale Größe. Um ersetzten Werts zu ermitteln, eine Anwendung ruft **SQLGetConnectAttr**.  
  
 [4] Wenn SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE festgelegt ist, bevor eine Verbindung geöffnet ist, Festlegen der Treiber-Manager der Treiber-Attributs beim Laden des Treibers während eines Aufrufs **SQLBrowseConnect**, **SQLConnect**, oder **SQLDriverConnect**. Vor einem Aufruf von **SQLBrowseConnect**, **SQLConnect**, oder **SQLDriverConnect**, der Treiber-Manager nicht bekannt ist, welcher Treiber für die Verbindung und weiß nicht, ob die -Treiber unterstützt asynchrone Verbindungsvorgängen sendet. Der Treiber-Manager gibt daher immer SQL_SUCCESS zurück. Aber, für den Fall, dass der Treiber asynchrone Verbindungsvorgänge, den Aufruf von nicht unterstützt **SQLBrowseConnect**, **SQLConnect**, oder **SQLDriverConnect** schlägt fehl.  
  
 [5] Wenn SQL_ATTR_AUTOCOMMIT auf "false" festgelegt ist, sollten Anwendungen SQLEndTran(SQL_ROLLBACK) aufrufen, wenn eine beliebige API SQL_ERROR zurück, um die Transaktionskonsistenz sicherzustellen zurückgibt.  
  
 Das Format der Informationen den \* *ValuePtr* Puffer hängt von der angegebenen *Attribut*. **SQLSetConnectAttr** Attributinformationen in einem von zwei verschiedenen Formaten akzeptiert: einen Null-terminierte Zeichenfolge oder einen ganzzahligen Wert. Das Format der einzelnen wird in das Attribut Beschreibung aufgeführt. Zeichenfolgen, die durch die *ValuePtr* Argument **SQLSetConnectAttr** haben eine Länge von *StringLength* Bytes.  
  
 Die *StringLength* Argument wird ignoriert, wenn die Länge, die das Attribut definiert ist wie der Fall für alle Attribute in ODBC 2. eingeführt ist*.x* oder früher.  
  
|*Attribut*|*ValuePtr* Inhalt|  
|-----------------|-------------------------|  
|SQL_ATTR_ACCESS_MODE (ODBC 1.0)|Eine SQLUINTEGER-Wert. SQL_MODE_READ_ONLY wird von der Treiber oder die Datenquelle dies ein Hinweis darauf, die die Verbindung nicht erforderlich ist, um SQL-Anweisungen unterstützen, die dazu führen, dass Updates durchgeführt. In diesem Modus kann verwendet werden, um Sperren Strategien, transaktionsverwaltung oder anderen Bereichen nach Bedarf, um die Treiber oder die Datenquelle zu optimieren. Der Treiber ist nicht erforderlich, um zu verhindern, dass solche Anweisungen an die Datenquelle gesendet wird. Das Verhalten des Treibers und der Datenquelle, wenn Sie gefragt werden, um SQL-Anweisungen verarbeiten, die nicht schreibgeschützt sind und während einer nur-Lese Verbindung sind ist implementierungsdefiniert. SQL_MODE_READ_WRITE ist die Standardeinstellung.|  
|SQL_ATTR_ASYNC_DBC_EVENT (ODBC 3.8)|Ein SQLPOINTER-Wert, der ein Ereignishandle ist.<br /><br /> Benachrichtigung über den Abschluss des asynchronen Funktionen aktiviert ist, durch den Aufruf **SQLSetConnectAttr** mit dem SQL_ATTR_ASYNC_STMT_EVENT-Attribut und das Ereignishandle angeben. **Hinweis:** die Benachrichtigungsmethode wird mit der Cursorbibliothek nicht unterstützt. Eine Anwendung wird die Fehlermeldung angezeigt, wenn es versucht, die Cursorbibliothek über SQLSetConnectAttr, aktivieren, wenn die Benachrichtigungsmethode aktiviert ist.|  
|SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE (ODBC 3.8)|Eine SQLUINTEGER-Wert, der aktiviert oder deaktiviert die asynchrone Ausführung der ausgewählten Funktionen auf dem Verbindungshandle. Weitere Informationen finden Sie unter [asynchrone Ausführung (Methode abrufen)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md).<br /><br /> SQL_ASYNC_DBC_ENABLE_ON = asynchronen Vorgang zum Aktivieren der für die angegebene Verbindung bezogene Funktionen.<br /><br /> SQL_ASYNC_DBC_ENABLE_OFF = (Standard) deaktivieren asynchronen Vorgang für die angegebene Verbindung bezogene Funktionen.<br /><br /> Festlegen von SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE ist immer synchron (d. h. Es gibt keine zurück SQL_STILL_EXECUTING).<br /><br /> Asynchrone Ausführung der Anweisung Vorgänge sind mit SQL_ATTR_ASYNC_ENABLE aktiviert.|  
|SQL_ATTR_ASYNC_DBC_PCALLBACK (ODBC 3.8)|Ein SQLPOINTER-Wert, der auf Context-Struktur zeigt.<br /><br /> Nur der Treiber-Manager eines Treibers aufrufen können **SQLSetStmtAttr** Funktion mit diesem Attribut.|  
|SQL_ATTR_ASYNC_DBC_PCONTEXT (ODBC 3.8)|Ein SQLPOINTER-Wert, der auf das Context-Struktur zeigt.<br /><br /> Nur der Treiber-Manager eines Treibers aufrufen können **SQLSetStmtAttr** Funktion mit diesem Attribut.|  
|SQL_ATTR_ASYNC_ENABLE (ODBC 3.0)|Ein SQLULEN-Wert, der angibt, ob eine Funktion mit einer Anweisung für die angegebene Verbindung aufgerufen wird asynchron ausgeführt werden:<br /><br /> SQL_ASYNC_ENABLE_OFF = Disable Verbindung Ebene asynchrone Ausführung-Unterstützung für Anweisung Vorgänge (Standard).<br /><br /> SQL_ASYNC_ENABLE_ON = Enable Verbindung Ebene asynchrone Ausführung-Unterstützung für Vorgänge der Anweisung.<br /><br /> Dieses Attribut kann festlegen, ob **SQLGetInfo** mit den Informationen SQL_ASYNC_MODE Typ SQL_AM_CONNECTION oder SQL_AM_STATEMENT zurückgibt.|  
|SQL_ATTR_AUTO_IPD (ODBC 3.0)|Eine schreibgeschützte SQLUINTEGER-Wert, der angibt, ob automatische Auffüllung der die IPD nach einem Aufruf von **SQLPrepare** wird unterstützt:<br /><br /> SQL_TRUE = automatischen Auffüllung der die IPD nach einem Aufruf von **SQLPrepare** wird vom Treiber unterstützt.<br /><br /> SQL_FALSE = automatischen Auffüllung der die IPD nach einem Aufruf von **SQLPrepare** wird vom Treiber nicht unterstützt. Server, die nicht unterstützen, vorbereitete Anweisungen werden nicht die IPD automatisch aufgefüllt werden.<br /><br /> Wenn SQL_TRUE für das Verbindungsattribut SQL_ATTR_AUTO_IPD zurückgegeben wird, kann das Anweisungsattribut SQL_ATTR_ENABLE_AUTO_IPD zu aktivieren oder deaktivieren Sie die automatischen Auffüllung der die IPD festgelegt werden. Wenn SQL_ATTR_AUTO_IPD SQL_FALSE ist, kann die SQL_ATTR_ENABLE_AUTO_IPD auf SQL_TRUE festgelegt werden. Der Standardwert von SQL_ATTR_ENABLE_AUTO_IPD ist gleich dem Wert des SQL_ATTR_AUTO_IPD.<br /><br /> Dieses Verbindungsattribut zurückgegeben werden kann, indem **SQLGetConnectAttr** aber nicht festgelegt werden, indem **SQLSetConnectAttr**.|  
|SQL_ATTR_AUTOCOMMIT (ODBC 1.0)|Eine SQLUINTEGER-Wert, der angibt, ob Autocommit oder im Manualcommit-Modus verwendet:<br /><br /> SQL_AUTOCOMMIT_OFF = verwendet der Treiber Manualcommit-Modus und die Anwendung muss explizit einen commit oder Rollback für Transaktionen mit **SQLEndTran**.<br /><br /> SQL_AUTOCOMMIT_ON = den Treiber verwendet Autocommit-Modus. Jede Anweisung wird ein Commit ausgeführt wurde, sofort, nachdem er ausgeführt wird. Dies ist die Standardeinstellung. Alle offenen Transaktionen für die Verbindung werden übernommen, wenn SQL_ATTR_AUTOCOMMIT auf SQL_AUTOCOMMIT_ON festgelegt ist, so ändern Sie den Autocommit-Modus von Manualcommit-Modus.<br /><br /> Weitere Informationen finden Sie unter [Commit-Modus](../../../odbc/reference/develop-app/commit-mode.md). **Wichtig:** einige Datenquellen löschen, die Zugriffspläne und Schließen der Cursor für alle Anweisungen für eine Verbindung jedes Mal eine Anweisung wird ein Commit ausgeführt; Autocommit-Modus kann dazu führen, dass dies so erfolgen kann, nachdem jedes Nonquery-Anweisung ausgeführt wird oder wenn sich der Cursor befindet für eine Abfrage geschlossen. Weitere Informationen finden Sie unter den Informationstypen SQL_CURSOR_COMMIT_BEHAVIOR und SQL_CURSOR_ROLLBACK_BEHAVIOR in [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) und [Auswirkungen von Transaktionen für Cursor und vorbereitete Anweisungen](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md). <br /><br /> Wenn ein Batch im Autocommit-Modus ausgeführt wird, sind zwei Dinge möglich. Der gesamte Batch als eine Einheit Autocommitable behandelt werden kann, oder jede Anweisung in einem Batch wird als eine Einheit Autocommitable behandelt. Bestimmte Datenquellen unterstützen sowohl diese Verhaltensweisen und möglicherweise eine Möglichkeit zum Auswählen eines dieser Zuordnungsverfahren. Es ist treiberdefinierten gibt an, ob ein Batch als eine Einheit Autocommitable behandelt wird oder ob jede einzelne Anweisung im Batch Autocommitable ist.|  
|SQL_ATTR_CONNECTION_DEAD<br /><br /> (ODBC 3.5)|Ein nur-Lese SQLUINTEGER-Wert, der den Zustand der Verbindung angibt. Wenn SQL_CD_TRUE, die Verbindung unterbrochen wurde. Wenn SQL_CD_FALSE, die Verbindung noch aktiv ist.|  
|SQL_ATTR_CONNECTION_TIMEOUT (ODBC 3.0)|Eine SQLUINTEGER-Wert entspricht der Anzahl der Sekunden für jede Anforderung für die Verbindung ab, bevor Sie an die Anwendung zurückgegeben. Der Treiber sollte SQLSTATE HYT00 zurück (das Timeout ist abgelaufen) können Sie jederzeit, es ist möglich, zu einem Timeout führen in einer Situation nicht abfrageausführung oder Anmeldename zugeordnet ist.<br /><br /> Wenn *ValuePtr* ist gleich 0 (Standard), ist kein Timeout festgelegt.|  
|SQL_ATTR_CURRENT_CATALOG (ODBC 2.0)|Eine Zeichenfolge mit dem Namen des Katalogs ein, der von der Datenquelle verwendet werden. Z. B. in SQL Server, der Katalog ist eine Datenbank, damit der Treiber sendet eine **verwenden** *Datenbank* Anweisung mit der Datenquelle, in dem *Datenbank* wird in die Datenbank angegeben \* *ValuePtr*. Für einen ein-Ebenen-Treiber, der Katalog möglicherweise ein Verzeichnis ist, ändert der Treiber die ein aktuelle Verzeichnis in das Verzeichnis im angegebenen **ValuePtr*.|  
|SQL_ATTR_DBC_INFO_TOKEN (ODBC 3.8|SQLPOINTER Wert verwendet, um festzulegen, wieder das Verbindungstoken für die Informationen in der Datenbank behandeln beim [SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md)des (\**pRating*) Parameter ist nicht gleich 100.<br /><br /> SQL_ATTR_DBC_INFO_TOKEN kann nur Satz. Es ist nicht möglich, verwenden Sie **SQLGetConnectAttr** oder **SQLGetConnectOption** zum Abrufen dieses Werts. Der Treiber-Manager **SQLSetConnectAttr** SQL_ATTR_DBC_INFO_TOKEN, werden nicht akzeptiert werden, da dieses Attribut nicht in eine Anwendung festlegen sollten.<br /><br /> Ein Treiber SQL_ERROR zurück, nach dem SQL_ATTR_DBC_INFO_TOKEN festlegen, wird die Verbindung, die nur aus dem Pool abgerufen, freigegeben werden. Der Treiber-Manager versucht dann, eine andere Verbindung aus dem Pool zu erhalten. Finden Sie unter [entwickeln Verbindungspool wissen in eine ODBC-Treiber](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md) für Weitere Informationen.|  
|SQL_ATTR_ENLIST_IN_DTC (ODBC 3.0)|Ein SQLPOINTER-Wert, der angibt, ob den ODBC-Treiber an verteilten Transaktionen von Microsoft Component Services koordiniert verwendet.<br /><br /> Übergeben Sie ein DTC OLE Transaction Objekt, der angibt, die Transaktion zum Exportieren in SQL Server- oder SQL_DTC_DONE auf, um die Verbindung DTC-Zuordnung zu beenden.<br /><br /> Der Client Ruft die Microsoft Distributed Transaction Coordinator (MS DTC) OLE ITransactionDispenser:: BeginTransaction-Methode, um eine MS DTC-Transaktion zu beginnen, und erstellen Sie eine MS DTC-Transaktionsobjekt, das die Transaktion darstellt. Die Anwendung ruft dann SQLSetConnectAttr mit der SQL_ATTR_ENLIST_IN_DTC-Option, um die ODBC-Verbindung das Transaktionsobjekt zuzuordnen. Alle entsprechenden Datenbankaktivitäten werden unter dem Schutz der MS DTC-Transaktion durchgeführt. Die Anwendung ruft SQLSetConnectAttr mit SQL_DTC_DONE auf, um die Verbindung DTC-Zuordnung zu beenden. Weitere Informationen finden Sie in der MS DTC-Dokumentation.|  
|SQL_ATTR_LOGIN_TIMEOUT (ODBC 1.0)|Eine SQLUINTEGER-Wert entspricht der Anzahl der Sekunden für eine anmeldeanforderung ab, bevor Sie an die Anwendung zurückgegeben. Der Standardwert ist-Treiber abhängig. Wenn *ValuePtr* ist 0, das Timeout ist deaktiviert, und versucht, eine Verbindung wartet unbegrenzt.<br /><br /> Überschreitet das festgelegte Timeout der maximale Anmeldungstimeout in der Datenquelle, wird der Treiber ersetzt diesen Wert und gibt SQLSTATE 01 s 02 (Optionswert wurde geändert).|  
|SQL_ATTR_METADATA_ID (ODBC 3.0)|Eine SQLUINTEGER-Wert, der bestimmt, wie die Zeichenfolgenargumente von Katalogfunktionen behandelt werden.<br /><br /> Wenn SQL_TRUE, das Zeichenfolgenargument von Katalogfunktionen als Bezeichner behandelt werden. Die Groß-/Kleinschreibung ist nicht signifikant. Der Treiber entfernt nachgestellten Leerzeichen als begrenzungsbezeichnern Zeichenfolgen und die Zeichenfolge in Großbuchstaben gefaltet wird. Für durch Trennzeichen getrennten Zeichenfolgen der Treiber keine führenden oder nachfolgenden Leerzeichen entfernt und wird als solcher nach Belieben zwischen den Trennzeichen ist. Wenn eins dieser Argumente auf einen null-Zeiger festgelegt ist, gibt die Funktion SQL_ERROR und SQLSTATE HY009 (Ungültige Verwendung eines null-Zeiger).<br /><br /> Wenn SQL_FALSE, die Zeichenfolgenargumente von Katalogfunktionen nicht als Bezeichner behandelt werden. Die Groß-/Kleinschreibung spielt. Sie können entweder eine Zeichenfolge Suchmuster oder nicht, je nach dem Argument enthalten.<br /><br /> Der Standardwert ist SQL_FALSE.<br /><br /> Die *TableType* Argument **SQLTables**, der eine Liste mit Werten, akzeptiert wird durch dieses Attribut nicht beeinflusst.<br /><br /> SQL_ATTR_METADATA_ID kann auch auf der Anweisungsebene festgelegt werden. (Es ist das einzige Verbindung-Attribut, das auch ein Anweisungsattribut ist.)<br /><br /> Weitere Informationen finden Sie unter [Argumente in Katalogfunktionen](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).|  
|SQL_ATTR_ODBC_CURSORS (ODBC 2.0)|Ein SQLULEN-Wert, der angibt, wie der Treiber-Manager die ODBC-Cursorbibliothek verwendet wird:<br /><br /> SQL_CUR_USE_IF_NEEDED = der Treiber-Manager verwendet die ODBC-Cursorbibliothek nur, wenn er benötigt wird. Wenn der Treiber die SQL_FETCH_PRIOR-Option in unterstützt **SQLFetchScroll**, der Treiber-Manager verwendet das Durchführen eines Bildlaufs Funktionen des Treibers. Andernfalls verwendet es die ODBC-Cursorbibliothek.<br /><br /> SQL_CUR_USE_ODBC = der Treiber-Manager verwendet die ODBC-Cursorbibliothek.<br /><br /> SQL_CUR_USE_DRIVER = der Treiber-Manager verwendet das Durchführen eines Bildlaufs Funktionen des Treibers. Dies ist die Standardeinstellung.<br /><br /> Weitere Informationen zu den ODBC-Cursorbibliothek, finden Sie unter [Anhang F: ODBC-Cursorbibliothek](../../../odbc/reference/appendixes/appendix-f-odbc-cursor-library.md). **Warnung:** die Cursorbibliothek wird in einer zukünftigen Version von Windows entfernt. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen und Planen von Anwendungen zu ändern, die dieses Feature verwenden. Microsoft empfiehlt die Verwendung der Cursorfunktionalität der Treiber.|  
|SQL_ATTR_PACKET_SIZE (ODBC 2.0)|Eine SQLUINTEGER-Wert, die die Netzwerkpaketgröße in Bytes angibt. **Hinweis:** entweder unterstützen viele Datenquellen diese Option keine oder nur kann Rückgabewert jedoch nicht festgelegt die Netzwerk-Paketgröße. <br /><br /> Wenn die angegebene Größe die maximale Paketgröße überschreitet oder kleiner als die minimale Paketgröße ist, wird der Treiber ersetzt dieser Wert und gibt SQLSTATE 01 s 02 (Optionswert wurde geändert).<br /><br /> Wenn die Anwendung für die Paketgröße festlegt, nachdem bereits eine Verbindung hergestellt wurde, wird der Treiber SQLSTATE HY011 zurück (Attribut kann nicht jetzt festgelegt werden).|  
|SQL_ATTR_QUIET_MODE (ODBC 2.0)|Ein Fensterhandle (HWND).<br /><br /> Wenn das Handle des Fensters ein null-Zeiger ist, wird der Treiber keine Dialogfelder angezeigt.<br /><br /> Das Fensterhandle kein null-Zeiger ist, sollte das Handle des übergeordneten Fensters der Anwendung sein. Dies ist die Standardeinstellung. Der Treiber verwendet dieses Handle, um die Anzeige von Dialogfeldern. **Hinweis:** SQL_ATTR_QUIET_MODE-Verbindungsattribut gilt nicht für Dialogfelder, **SQLDriverConnect**.|  
|SQL_ATTR_TRACE (ODBC 1.0)|Eine SQLUINTEGER-Wert, der Treiber-Manager mitteilen, ob die Ablaufverfolgung ausgeführt:<br /><br /> SQL_OPT_TRACE_OFF = Ablaufverfolgung off (Standardeinstellung)<br /><br /> SQL_OPT_TRACE_ON = Ablaufverfolgung auf<br /><br /> Wenn Ablaufverfolgung aktiviert ist, schreibt der Treiber-Manager jedem ODBC-Funktionsaufruf in der Ablaufverfolgungsdatei. **Hinweis:** Wenn Ablaufverfolgung aktiviert ist, kann der Treiber-Manager SQLSTATE IM013 zurückgeben (Fehler in der Ablaufverfolgungsdatei) von einer Funktion. <br /><br /> Eine Anwendung gibt eine Ablaufverfolgungsdatei mit der Option SQL_ATTR_TRACEFILE an. Wenn die Datei bereits vorhanden ist, fügt der Treiber-Manager an die Datei. Andernfalls wird die Datei erstellt. Wenn die Ablaufverfolgung aktiviert ist und keine der Ablaufverfolgungsdatei angegeben wurde, schreibt der Treiber-Manager in der SQL-Datei. Melden Sie sich im Stammverzeichnis befindet.<br /><br /> Legen Sie eine Anwendung kann die Variable **ODBCSharedTraceFlag** zum Aktivieren der Ablaufverfolgung dynamisch. Ablaufverfolgung wird für alle derzeit ausgeführten ODBC-Anwendungen aktiviert. Wenn eine Anwendung die Protokollierung deaktiviert wird, wird er nur für diese Anwendung deaktiviert.<br /><br /> Wenn der **Ablaufverfolgung** -Schlüsselwort in die Systeminformationen auf 1 festgelegt ist, wenn eine Anwendung ruft **SQLAllocHandle** mit einer *HandleType* SQL_HANDLE_ENV auf, wird die Ablaufverfolgung für alle aktiviert behandelt. Es ist nur für die Anwendung, die aufgerufen aktiviert **SQLAllocHandle**.<br /><br /> Aufrufen **SQLSetConnectAttr** mit einer *Attribut* von SQL_ATTR_TRACE ist nicht erforderlich, die *Verbindungshandle* Argument gültig sein und nicht SQL_ERROR zurück, wenn *Verbindungshandle* ist NULL. Dieses Attribut gilt für alle Verbindungen.|  
|SQL_ATTR_TRACEFILE (ODBC 1.0)|Eine Null endende Zeichenfolge mit dem Namen der Ablaufverfolgungsdatei.<br /><br /> Der Standardwert des Attributs SQL_ATTR_TRACEFILE wird angegeben, mit der **TraceFile** -Schlüsselwort in die Systeminformationen. Weitere Informationen finden Sie unter [ODBC-Unterschlüssel](../../../odbc/reference/install/odbc-subkey.md).<br /><br /> Aufrufen **SQLSetConnectAttr** mit einer *Attribut* von SQL_ATTR_ TRACEFILE erfordert keine der *Verbindungshandle* Argument gültig ist und gibt keinen SQL_ERROR zurück, wenn *Verbindungshandle* ist ungültig. Dieses Attribut gilt für alle Verbindungen.|  
|SQL_ATTR_TRANSLATE_LIB (ODBC 1.0)|Eine Null-terminierte Zeichenfolge mit dem Namen einer Bibliothek, die die Funktionen enthalten **SQLDriverToDataSource** und **SQLDataSourceToDriver** , dass der Treiber zugreift, um Aufgaben auszuführen, z. B. Übersetzung des Zeichensatzes. Diese Option ist möglicherweise nur angegeben werden, wenn der Treiber mit der Datenquelle verbunden ist. Die Einstellung des Attributs bleiben über Verbindungen erhalten. Weitere Informationen zum Übersetzen von Daten finden Sie unter [Übersetzung DLLs](../../../odbc/reference/develop-app/translation-dlls.md) und [Übersetzung DLL-Funktionsreferenz](../../../odbc/reference/syntax/translation-dll-api-reference.md).|  
|SQL_ATTR_TRANSLATE_OPTION (ODBC 1.0)|Ein 32-Bit-Flagwert, der die Übersetzung DLL übergeben wird. Dieses Attribut kann nur angegeben werden, wenn der Treiber mit der Datenquelle verbunden ist. Informationen zum Übersetzen von Daten finden Sie unter [Übersetzung DLLs](../../../odbc/reference/develop-app/translation-dlls.md).|  
|SQL_ATTR_TXN_ISOLATION (ODBC 1.0)|Eine 32-Bit-Bitmaske, die die Transaktionsisolationsstufe für die aktuelle Verbindung legt diese fest. Muss eine Anwendung aufrufen **SQLEndTran** , einen commit oder Rollback alle offene Transaktionen für eine Verbindung, vor dem Aufruf **SQLSetConnectAttr** mit dieser Option.<br /><br /> Die gültigen Werte für *ValuePtr* kann bestimmt werden, durch den Aufruf **SQLGetInfo** mit *Infotyp* SQL_TXN_ISOLATION_OPTIONS gleich.<br /><br /> Eine Beschreibung der Isolationsstufen von Transaktionen, finden Sie in der Beschreibung des Typs SQL_DEFAULT_TXN_ISOLATION Informationen in [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) und [Isolationsstufen von Transaktionen](../../../odbc/reference/develop-app/transaction-isolation-levels.md).|  
  
 [1] für diese Funktionen können asynchron aufgerufen werden, nur, wenn der Deskriptor eine Implementierung Deskriptor, keine Anwendungsdiensts ist.  
  
## <a name="code-example"></a>Codebeispiel  
 Finden Sie unter [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Ein Handle zuordnen|[SQLAllocHandle-Funktion](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Die Einstellung der Verbindungsattribut zurückgeben|[SQLGetConnectAttr-Funktion](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)

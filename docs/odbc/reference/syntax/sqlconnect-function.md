---
title: SQLConnect-Funktion | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLConnect
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLConnect
helpviewer_keywords:
- SQLConnect function [ODBC]
ms.assetid: 59075e46-a0ca-47bf-972a-367b08bb518d
caps.latest.revision: 37
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f3954538b63739fe19435aeb5cd30449edbc9d24
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlconnect-function"></a>SQLConnect-Funktion
**Konformität**  
 Version eingeführt: ODBC 1.0 Standardkonformität: ISO-92  
  
 **Zusammenfassung**  
 **SQLConnect** stellt Verbindungen mit einem Treiber und einer Datenquelle her. Das Verbindungshandle verweist auf Speicher, der alle Informationen über die Verbindung mit der Datenquelle, einschließlich Status, des Zustands einer Transaktion und Fehlerinformationen.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLConnect(  
     SQLHDBC        ConnectionHandle,  
     SQLCHAR *      ServerName,  
     SQLSMALLINT    NameLength1,  
     SQLCHAR *      UserName,  
     SQLSMALLINT    NameLength2,  
     SQLCHAR *      Authentication,  
     SQLSMALLINT    NameLength3);  
```  
  
## <a name="arguments"></a>Argumente  
 *Verbindungshandle*  
 [Eingabe] Verbindungshandle.  
  
 *ServerName*  
 [Eingabe] Datenquellenname. Daten können sich auf demselben Computer wie das Programm oder auf einem anderen Computer an einer beliebigen Stelle in einem Netzwerk sein. Weitere Informationen dazu, wie eine Anwendung eine Datenquelle auswählt, finden Sie unter [Auswählen der Datenquelle oder Treiber](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md).  
  
 *NameLength1*  
 [Eingabe] Länge des **ServerName* in Zeichen.  
  
 *UserName*  
 [Eingabe] Benutzer-ID.  
  
 *NameLength2*  
 [Eingabe] Länge des **Benutzername* in Zeichen.  
  
 *Authentifizierung*  
 [Eingabe] Authentifizierungszeichenfolge (in der Regel das Kennwort).  
  
 *NameLength3*  
 [Eingabe] Länge des **Authentifizierung* in Zeichen.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE oder SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLConnect** gibt SQL_ERROR oder SQL_SUCCESS_WITH_INFO, einen zugeordneten SQLSTATE-Wert abgerufen werden können, durch den Aufruf **SQLGetDiagRec** mit einem *HandleType* von SQL_ HANDLE_DBC und ein *behandeln* von *Verbindungshandle*. Die folgende Tabelle enthält die SQLSTATE-Werten, die in der Regel zurückgegebenes **SQLConnect** und erläutert, jeweils im Kontext dieser Funktion; die Notation "(DM)" vorangestellt ist, die Beschreibungen der SQLSTATEs, die vom Treiber-Manager zurückgegeben. Der Rückgabecode, der jeden SQLSTATE-Wert zugeordnet wird SQL_ERROR zurückgegeben, sofern nicht anders angegeben.  
  
|SQLSTATE|Fehler|Description|  
|--------------|-----------|-----------------|  
|01000|Allgemeine Warnung|Treiberspezifische Meldung dient zu Informationszwecken. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|01 S 02|Der Optionswert wurde geändert|Der Treiber nicht den angegebenen Wert, der die *ValuePtr* Argument in **SQLSetConnectAttr** und einen ähnlichen Wert ersetzt. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|08001|Client kann keine Verbindung herstellen|Der Treiber konnte nicht zum Herstellen einer Verbindung mit der Datenquelle.|  
|08002|Name der Verbindung verwendet|(DM) dem angegebenen *Verbindungshandle* war bereits zum Herstellen einer Verbindung mit einer Datenquelle und die Verbindung weiterhin geöffnet wurde oder der Benutzer wurde für eine Verbindung suchen verwendet.|  
|08004|Der Server wies die Verbindung|Die Datenquelle die Einrichtung der Verbindung Gründen abgelehnt Implementierung definiert.|  
|08S01|Kommunikations-Verbindungsfehler|Die Verbindung zwischen dem Treiber und der Datenquelle, zu der der Treiber versucht hat, die Verbindung, konnte nicht vor der Verarbeitung für die Funktion abgeschlossen.|  
|28000|Ungültige Autorisierungsangabe|Der Wert für das Argument angegebene *Benutzername* oder den Wert für das Argument angegebene *Authentifizierung* durch die Datenquelle definierten Einschränkungen verletzt.|  
|HY000|Allgemeiner Fehler|Für die es keine spezifischen SQLSTATE wurde und für die keine implementierungsabhängige SQLSTATE definiert wurde, ist ein Fehler aufgetreten. Die zurückgegebene Fehlermeldung **SQLGetDiagRec** in der * \*MessageText* Puffer beschreibt den Fehler und seiner Ursache.|  
|HY001|Fehler bei der speicherbelegung|Der Treiber-Manager (DM) konnte nicht belegt werden, die zur Unterstützung der Ausführung oder den Abschluss der Funktion erforderlich ist.|  
|HY008|Der Vorgang wurde abgebrochen|Asynchroner Verarbeitung wurde aktiviert, für die *Verbindungshandle*. Die **SQLConnect** Funktion aufgerufen wurde, und bevor es ausgeführt wurden, [SQLCancelHandle Funktion](../../../odbc/reference/syntax/sqlcancelhandle-function.md) aufgerufen wurde, auf die *Verbindungshandle*, und klicken Sie dann die **SQLConnect** Funktion erneut aufgerufen wurde, auf die *Verbindungshandle*.<br /><br /> Or **SQLConnect** Funktion aufgerufen wurde, und bevor es ausgeführt wurden, **SQLCancelHandle** aufgerufen wurde, auf die *Verbindungshandle* aus einem anderen Thread in einem Multithread-Anwendung.|  
|HY010|Fehler bei Funktionssequenz|(DM) hieß eine asynchron ausgeführte Funktion (nicht auf dieses Objekt) für die *Verbindungshandle* und wurde noch ausgeführt werden, wenn diese Funktion aufgerufen wurde.|  
|HY013|Speicherverwaltungsfehler|Der Funktionsaufruf konnte nicht verarbeitet werden, da die zugrunde liegenden Speicherobjekte, möglicherweise aufgrund von unzureichendem Speicher konnte nicht zugegriffen werden.|  
|HY090|Ungültige Zeichenfolgen- oder Pufferlänge.|(DM) für Argument angegebene Wert *NameLength1*, *NameLength2*, oder *NameLength3* war kleiner als 0, aber nicht SQL_NTS gleich.<br /><br /> (DM) für Argument angegebene Wert *NameLength1* überschreitet die maximale Länge für einen Datenquellennamen.|  
|HYT00|Timeout abgelaufen|Zeitraum für das Timeout ist abgelaufen, bevor die Verbindung mit der Datenquelle abgeschlossen. Das Zeitlimit wird über festgelegt **SQLSetConnectAttr**, SQL_ATTR_LOGIN_TIMEOUT.|  
|HY114|Verbindung Ebene asynchrone Ausführung unterstützt-Treiber nicht.|(DM) aktiviert die Anwendung den asynchronen Vorgang auf dem Verbindungshandle vor dem Herstellen der Verbindung. Allerdings unterstützt der Treiber nicht asynchroner Vorgänge auf dem Verbindungshandle.|  
|HYT01|Verbindungstimeout abgelaufen|Das Verbindungstimeout ist abgelaufen, bevor die Datenquelle auf die Anforderung geantwortet hat. Das Verbindungstimeout wird über festgelegt **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Diese Funktion wird im Treiber nicht unterstützt.|(DM) des Treibers durch den Namen der Datenquelle angegeben die Funktion nicht unterstützt.|  
|IM002|Datenquelle wurde nicht gefunden und kein Standardtreiber angegeben|(DM) der Name der Datenquelle im Argument angegebene *ServerName* wurde nicht gefunden, in die Systeminformationen noch gab es eine Standard-Treiber-Spezifikation.|  
|IM003|Angegebene Treiber konnte keine Verbindung hergestellt werden|(DM) der Treiber aufgeführt, in den Daten Quellspezifikation in Systeminformationen wurde nicht gefunden oder konnte nicht mit einem anderen Grund verbunden werden.|  
|IM004|Fehler beim des Treibers SQLAllocHandle auf SQL_HANDLE_ENV auf.|(DM) während der **SQLConnect**, der Treiber-Manager aufgerufen, des Treibers **SQLAllocHandle** -Funktion mit einem *HandleType* SQL_HANDLE_ENV und der Treiber hat einen Fehler zurückgegeben.|  
|IM005|Fehler beim des Treibers SQLAllocHandle auf SQL_HANDLE_DBC auf.|(DM) während der **SQLConnect**, der Treiber-Manager aufgerufen, des Treibers **SQLAllocHandle** -Funktion mit einem *HandleType* SQL_HANDLE_DBC auf, und der Treiber hat einen Fehler zurückgegeben.|  
|IM006|Fehler des Treibers SQLSetConnectAttr|Während der **SQLConnect**, der Treiber-Manager aufgerufen, des Treibers **SQLSetConnectAttr** -Funktion und der Treiber hat einen Fehler zurückgegeben. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|IM009|Keine Verbindung zum Konvertierungs-DLL|Der Treiber konnte keine Verbindung zum Konvertierungs-DLL, die für die Datenquelle angegeben wurde.|  
|IM010|Der Datenquellenname ist zu lang|(DM) * \*ServerName* wurde mehr als SQL_MAX_DSN_LENGTH Zeichen enthalten.|  
|IM014|Der angegebene DSN enthält ein Architektur-Konflikt zwischen der Treiber und die Anwendung|(DM)-32-Bit-Anwendung wird einen DSN, Herstellen einer Verbindung mit einer 64-Bit-Treiber verwendet. oder umgekehrt.|  
|IM015|Fehler des Treibers SQLConnect auf SQL_HANDLE_DBC_INFO_HANDLE|Wenn ein Treiber SQL_ERROR zurückgibt, der Treiber-Manager für die Anwendung SQL_ERROR zurück, und die Verbindung schlägt fehl.<br /><br /> Weitere Informationen zu SQL_HANDLE_DBC_INFO_TOKEN, finden Sie unter [entwickeln Verbindungspool wissen in eine ODBC-Treiber](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).|  
|IM017|Abrufintervall ist im Modus für asynchrone Benachrichtigung deaktiviert.|Sobald das Benachrichtigungsmodell verwendet wird, ist die Abruf deaktiviert.|  
|IM018|**SQLCompleteAsync** nicht zum Abschließen des vorherigen asynchrone Vorgangs auf diesem Handle aufgerufen wurde.|Wenn die vorherigen Funktionsaufruf auf das Handle SQL_STILL_EXECUTING zurückgibt und Benachrichtigungsmodus aktiviert ist, **SQLCompleteAsync** muss aufgerufen werden, auf das Handle nach der Verarbeitung und der Vorgang abgeschlossen werden.|  
|S1118|Asynchrone Benachrichtigung unterstützt-Treiber nicht.|Wenn der Treiber die asynchrone Benachrichtigung nicht unterstützt, kann nicht SQL_ATTR_ASYNC_DBC_EVENT oder SQL_ATTR_ASYNC_DBC_RETCODE_PTR festgelegt werden.|  
  
## <a name="comments"></a>Kommentare  
 Informationen dazu, warum eine Anwendung verwendet **SQLConnect**, finden Sie unter [Herstellen einer Verbindung mit SQLConnect](../../../odbc/reference/develop-app/connecting-with-sqlconnect.md).  
  
 Der Treiber-Manager verbindet sich nicht mit einem Treiber, bis die Anwendung eine Funktion aufruft (**SQLConnect**, **SQLDriverConnect**, oder **SQLBrowseConnect**) zur Verbindung mit der Treiber. Bis zu diesem Zeitpunkt wird der Treiber-Manager arbeitet mit einem eigenen Handles und Verbindungsinformationen verwaltet. Wenn die Anwendung eine Verbindungsfunktion aufruft, wird der Treiber-Manager überprüft, ob ein Treiber für den angegebenen aktuell verbunden ist *Verbindungshandle*:  
  
-   Ein Treiber nicht mit verbunden ist, der Treiber-Manager stellt eine Verbindung mit dem Treiber und ruft **SQLAllocHandle** mit einem *HandleType* SQL_HANDLE_ENV auf, **SQLAllocHandle** mit einer *HandleType* SQL_HANDLE_DBC auf, **SQLSetConnectAttr** (wenn die Anwendung Verbindungsattribute angegeben), und die Verbindungsfunktion im Treiber. Der Treiber-Manager gibt SQLSTATE IM006 (des Treibers **SQLSetConnectOption** fehlgeschlagen) und SQL_SUCCESS_WITH_INFO für die Verbindungsfunktion, wenn der Treiber einen Fehler für zurückgegeben **SQLSetConnectAttr**. Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit einer Datenquelle oder Treiber](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md).  
  
-   Wenn der angegebene Treiber auf bereits verbunden ist die *Verbindungshandle*, der Treiber-Manager ruft nur die Verbindungsfunktion im Treiber. In diesem Fall der Treiber muss sicherstellen, dass alle für Verbindungsattribute die *Verbindungshandle* verwalten Sie ihre aktuellen Einstellungen.  
  
-   Wenn ein anderer Treiber mit verbunden ist, ruft der Treiber-Manager **SQLFreeHandle** mit einem *HandleType* SQL_HANDLE_DBC auf, und klicken Sie dann, wenn keine andere Treiber, in dieser Umgebung verbunden ist, ruft es **SQLFreeHandle** mit einem *HandleType* SQL_HANDLE_ENV auf, in der verbundenen Treiber, und klicken Sie dann diesen Treiber die Verbindung trennt. Er führt dann die gleichen Vorgänge wie bei ein Treiber nicht mit verbunden ist.  
  
 Der Treiber dann ordnet Handles und selbst initialisiert.  
  
 Wenn die Anwendung aufruft, **SQLDisconnect**, der Treiber-Manager ruft **SQLDisconnect** im Treiber. Den Treiber werden jedoch nicht getrennt. Dadurch wird den Treiber für Anwendungen, die wiederholt eine Verbindung mit herstellen und Trennen von einer Datenquelle im Arbeitsspeicher. Wenn die Anwendung aufruft, **SQLFreeHandle** mit einem *HandleType* SQL_HANDLE_DBC auf, ruft der Treiber-Manager **SQLFreeHandle** mit einem *HandleType * SQL_HANDLE_DBC auf, und klicken Sie dann **SQLFreeHandle** mit einem *HandleType* SQL_HANDLE_ENV auf, in der Treiber und trennt dann den Treiber.  
  
 Eine ODBC-Anwendung kann mehr als eine Verbindung herstellen.  
  
## <a name="driver-manager-guidelines"></a>Treiber-Manager-Richtlinien  
 Der Inhalt des **ServerName* beeinflussen, wie der Treiber-Manager und einen Treiber zusammenarbeiten, um eine Verbindung mit einer Datenquelle herzustellen.  
  
-   Wenn \* *ServerName* enthält einen gültigen Datenquellennamen der Treiber-Manager sucht nach der Angabe der entsprechenden Datenquelle in die Systeminformationen und eine Verbindung mit der zugehörigen Treiber her. Der Treiber-Manager übergibt jedes **SQLConnect** Argument an den Treiber.  
  
-   Wenn der Name der Datenquelle nicht gefunden werden kann oder *ServerName* ist ein null-Zeiger der Treiber-Manager sucht nach der Angabe der standardmäßige Datenquelle und eine Verbindung mit der zugehörigen Treiber her. Der Treiber-Manager an den Treiber übergibt die *Benutzername* und *Authentifizierung* Argumente unverändert bleiben sollen, und "DEFAULT" für die *ServerName* Argument.  
  
-   Wenn die *ServerName* Argument lautet "DEFAULT", der Treiber-Manager sucht nach der Angabe der standardmäßige Datenquelle und eine Verbindung mit der zugehörigen Treiber her. Der Treiber-Manager übergibt jedes **SQLConnect** Argument an den Treiber.  
  
-   Wenn der Name der Datenquelle nicht gefunden werden kann oder *ServerName* ist ein null-Zeiger und dem Standard-datenquellenspezifikation ist nicht vorhanden, die der Treiber-Manager gibt SQL_ERROR mit SQLSTATE IM002 (Datenquelle Namen wurde nicht gefunden und kein Standardwert Treiber angegeben).  
  
 Nachdem sie mit der Treiber-Manager verbunden ist, kann ein Treiber suchen Sie die entsprechenden datenquellenspezifikation in die Systeminformationen und treiberspezifische Informationen aus der Spezifikation verwenden, um einen Satz von erforderlichen Verbindungsinformationen abzuschließen.  
  
 Wenn eine Übersetzung Standardbibliothek in die Systeminformationen für die Datenquelle angegeben wird, der Treiber eine Verbindung damit her. Einer anderen übersetzungsbibliothek mit verbunden werden kann, durch den Aufruf **SQLSetConnectAttr** mit SQL_ATTR_TRANSLATE_LIB-Attribut. Eine Übersetzungsoption kann angegeben werden, durch den Aufruf **SQLSetConnectAttr** mit dem SQL_ATTR_TRANSLATE_OPTION-Attribut.  
  
 Wenn ein Treiber unterstützt **SQLConnect**, muss der Treiber Schlüsselwort Teil die Systeminformationen für den Treiber enthalten die **ConnectFunctions** Schlüsselwort mit dem ersten Zeichen legen Sie auf "Y" zurück.  
  
### <a name="connection-pooling"></a>Verbindungspooling  
 Verbindungs-pooling kann eine Anwendung eine Verbindung wiederzuverwenden, die bereits erstellt wurde. Wenn Verbindungspooling aktiviert ist und **SQLConnect** aufgerufen wurde, versucht der Treiber-Manager zum Herstellen der Verbindung mit einer Verbindung, der einen Pool von Verbindungen in einer Umgebung gehört, die für das Verbindungspooling festgelegt wurde. Diese Umgebung ist eine freigegebene Umgebung, die von allen Anwendungen verwendet wird, die Verbindungen im Pool zu verwenden.  
  
 Verbindungspooling aktiviert ist, bevor die Umgebung durch den Aufruf zugeordnet ist **SQLSetEnvAttr** SQL_ATTR_CONNECTION_POOLING SQL_CP_ONE_PER_DRIVER (der maximal einen Pool pro Treiber angegeben ist) oder SQL_CP_ONE_PER_HENV festlegen (die gibt maximal einen Pool pro Umgebung). **SQLSetEnvAttr** in diesem Fall mit heißt *EnvironmentHandle* auf Null gesetzt, wodurch dem Attribut ein Attribut auf Prozessebene. Wenn SQL_ATTR_CONNECTION_POOLING auf SQL_CP_OFF festgelegt ist, ist das Verbindungspooling deaktiviert.  
  
 Wenn Verbindungspooling aktiviert wurde, **SQLAllocHandle** mit einem *HandleType* SQL_HANDLE_ENV aufgerufen, um eine Umgebung zuzuweisen. Die Umgebung, die durch diesen Aufruf zugeordnet ist einer freigegebenen Umgebung aus, da Verbindungspooling aktiviert wurde. Die Umgebung, die verwendet werden, wird jedoch nicht bestimmt, bis **SQLAllocHandle** mit einem *HandleType* SQL_HANDLE_DBC auf aufgerufen wird.  
  
 **SQLAllocHandle** mit einem *HandleType* SQL_HANDLE_DBC auf aufgerufen, um eine Verbindung zuzuweisen. Der Treiber-Manager versucht, eine vorhandene freigegebene Umgebung finden, die die Umgebung Attribute, die von der Anwendung festgelegten entspricht. Wenn keine solche Umgebung vorhanden ist, wird eine erstellt, wie ein impliziter *freigegebenen Umgebung*. Wenn eine übereinstimmende freigegebene Umgebung gefunden wird, das Umgebungshandle an die Anwendung zurückgegeben, und dessen Verweiszähler erhöht.  
  
 Die Verbindung, die verwendet werden, wird jedoch nicht bestimmt, bis **SQLConnect** aufgerufen wird. An diesem Punkt versucht der Treiber-Manager auf eine vorhandene Verbindung im Verbindungspool zu suchen, die von der Anwendung angeforderte Kriterien entspricht. Diese Kriterien umfassen die Verbindungsoptionen im Aufruf der angeforderten **SQLConnect** (die Werte der *ServerName*, *Benutzername*, und * Authentifizierung* Schlüsselwörter) und weitere Verbindungsattribute gesetzt werden, da **SQLAllocHandle** mit einem *HandleType* SQL_HANDLE_DBC auf aufgerufen wurde. Der Treiber-Manager überprüft diese Kriterien für die entsprechenden Verbindungsschlüsselwörter und Attribute im Verbindungen im Pool. Wenn eine Übereinstimmung gefunden wird, wird die Verbindung im Pool verwendet. Wenn keine Übereinstimmung gefunden wird, wird eine neue Verbindung erstellt.  
  
 Wenn das Attribut der SQL_ATTR_CP_MATCH-Umgebung auf SQL_CP_STRICT_MATCH festgelegt ist, muss die Übereinstimmung genaue für eine Verbindung im Pool verwendet werden. Wenn das Attribut der SQL_ATTR_CP_MATCH-Umgebung auf SQL_CP_RELAXED_MATCH festgelegt ist, wird die Verbindung im Aufruf von Optionen **SQLConnect** überein, aber nicht alle Verbindungsattribute müssen übereinstimmen.  
  
 Die folgenden Regeln werden angewendet, wenn ein Verbindungsattribut als Satz von der Anwendung vor dem **SQLConnect** aufgerufen wird, das die Verbindung im Pool-Verbindungsattribut stimmt nicht überein:  
  
-   Wenn das Verbindungsattribut festgelegt werden muss, bevor die Verbindung hergestellt wird:  
  
     Wenn SQL_ATTR_CP_MATCH SQL_CP_STRICT_MATCH ist, müssen SQL_ATTR_PACKET_SIZE in die zusammengeführte Verbindung mit dem von der Anwendung festgelegtes Attribut identisch sein. Wenn SQL_CP_RELAXED_MATCH, die Werte der SQL_ATTR_PACKET_SIZE unterschiedlich sein kann.  
  
     Der Wert des SQL_ATTR_LOGIN_VALUE wirkt sich nicht auf die Übereinstimmung aus.  
  
-   Wenn das Verbindungsattribut festgelegt werden kann, bevor oder nachdem die Verbindung hergestellt wird:  
  
     Wenn das Verbindungsattribut nicht von der Anwendung festgelegt wurde, aber für die Verbindung im Pool festgelegt wurde, und es eine Standardoption ist, wird das Verbindungsattribut in die zusammengeführte Verbindung wieder auf den Standardwert festgelegt ist, und eine Übereinstimmung deklariert ist. Wenn kein Standardwert angegeben ist, wird die zusammengeführte Verbindung kein übereinstimmend angesehen.  
  
     Wenn das Verbindungsattribut von der Anwendung festgelegt wurde, aber es wurde nicht für die Verbindung im Pool festgelegt, wird das Verbindungsattribut für den Pool wird in diesem Satz von der Anwendung geändert, und es wird eine Übereinstimmung deklariert.  
  
     Wenn das Verbindungsattribut von der Anwendung festgelegt wurde, und wurde auch für die Verbindung im Pool festgelegt, aber die Werte abweichen voneinander, wird der Wert des Verbindungsattribut für die Anwendung verwendet wird, und eine Übereinstimmung wird deklariert.  
  
-   Wenn die Werte der treiberspezifische Verbindungsattribute nicht überein stimmen und SQL_ATTR_CP_MATCH auf SQL_CP_STRICT_MATCH festgelegt ist, wird die Verbindung im Pool nicht verwendet.  
  
 Wenn die Anwendung aufruft, **SQLDisconnect** zum Trennen die Verbindung an den Verbindungspool zurückgegeben werden soll, und wieder verfügbar ist.  
  
### <a name="optimizing-connection-pooling-performance"></a>Optimieren der Leistung für Verbindungspooling  
 Bei verteilte Transaktionen beteiligt sind, ist es möglich, Optimieren der Leistung mithilfe von Verbindungspooling **SQL_DTC_TRANSITION_COST**, also auf eine SQLUINTEGER-Bitmaske. Die genannten Übergänge sind Übergänge des Verbindungsattributs SQL_ATTR_ENLIST_IN_DTC Wechseln vom Wert 0 zu ungleich NULL, und umgekehrt. Dies ist eine Verbindung vom nicht eingetragen in einer verteilten Transaktion eingetragen, in einer verteilten Transaktion (und umgekehrt). Je nachdem, wie der Treiber Eintragung (Einstellung Verbindungsattribut SQL_ATTR_ENLIST_IN_DTC) implementiert wird diese Übergänge stark beanspruchen und sollte daher vermieden werden, um die bestmögliche Leistung.  
  
 Vom Treiber zurückgegebene Wert enthält eine beliebige Kombination der folgenden Bits:  
  
-   **SQL_DTC_ENLIST_EXPENSIVE**Wenn eingerichtet, der 0 (null) für den Übergang ungleich NULL ist deutlich teurer als Übergang von ungleich NULL in einen anderen Wert ungleich Null (eine zuvor eingetragene Verbindung in der nächsten Transaktion eintragen) angegeben.  
  
-   **SQL_DTC_UNENLIST_EXPENSIVE**Wenn eingerichtet, angegeben, der ungleich 0 (null) Übergang ist deutlich teurer als die Verwendung einer Verbindungs, deren SQL_ATTR_ENLIST_IN_DTC-Attributs ist bereits auf 0 (null) festgelegt.  
  
 Es ist eine Leistung und Verbindung Nutzung getroffen. Ein Treiber gibt an, dass eine oder mehrere dieser Übergänge teuer sind, antwortet dieser bleiben mehr Verbindungen im Pool Verbindungspoolfunktion des Treiber-Managers. Einige der Verbindungen im Pool sind für die Verwendung von nicht transaktionalen bevorzugte und einige sind der bevorzugte transaktional. Jedoch, wenn der Treiber gibt an, dass diese Übergänge nicht teuer sind, können weniger Verbindungen verwendet werden möglicherweise nicht transaktionalen und transaktionale Verwendung abwechselnd.  
  
 Treiber, die keine SQL_ATTR_ENLIST_IN_DTC unterstützen müssen nicht SQL_DTC_TRANSITION_COST unterstützen. Treiber, die SQL_ATTR_ENLIST_IN_DTC jedoch nicht SQL_DTC_TRANSITION_COST unterstützen, wird davon ausgegangen, dass die Übergänge nicht viel Leistung beanspruchen, als ob der Treiber 0 (keine festgelegten Bits) für diesen Wert zurückgegeben werden.  
  
 Obwohl SQL_DTC_TRANSITION_COST in ODBC 3.5 verwendet wird, eine ODBC-2 eingeführt wurde. *x* Treiber kann auch unterstützt, da der Treiber-Manager diese Informationen unabhängig von der Version des Treibers abfragt.  
  
### <a name="code-example"></a>Codebeispiel  
 Im folgenden Beispiel weist eine Anwendung umgebungs- und Handles. Klicken Sie dann eine Verbindung mit der SalesOrders-Datenquelle mit dem Benutzer-ID JohnS und das Kennwort Symbol, und die Daten verarbeitet. Beim Verarbeiten von Daten abgeschlossen wurde, von der Datenquelle getrennt und die Handles frei.  
  
```  
// SQLConnect_ref.cpp  
// compile with: odbc32.lib  
#include <windows.h>  
#include <sqlext.h>  
  
int main() {  
   SQLHENV henv;  
   SQLHDBC hdbc;  
   SQLHSTMT hstmt;  
   SQLRETURN retcode;  
  
   SQLCHAR * OutConnStr = (SQLCHAR * )malloc(255);  
   SQLSMALLINT * OutConnStrLen = (SQLSMALLINT *)malloc(255);  
  
   // Allocate environment handle  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
  
   // Set the ODBC version environment attribute  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
      retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (void*)SQL_OV_ODBC3, 0);   
  
      // Allocate connection handle  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
         retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
  
         // Set login timeout to 5 seconds  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
            SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
            // Connect to data source  
            retcode = SQLConnect(hdbc, (SQLCHAR*) "NorthWind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
  
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
  
### <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Ein Handle zuordnen|[SQLAllocHandle-Funktion](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Ermitteln und Auflisten von Werten, die für die Verbindung mit einer Datenquelle|[SQLBrowseConnect-Funktion](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|Trennen von einer Datenquelle|[SQLDisconnect-Funktion](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|Herstellen einer Verbindung mit einer Datenquelle mit einer Zeichenfolge oder ein Dialogfeld Verbindungsdialogfeld|[SQLDriverConnect-Funktion](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|Die Einstellung der Verbindungsattribut zurückgeben|[SQLGetConnectAttr-Funktion](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Ein Verbindungsattribut festlegen|[SQLSetConnectAttr-Funktion](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)

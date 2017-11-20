---
title: SQLAllocHandle-Funktion | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLAllocHandle
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLAllocHandle
helpviewer_keywords:
- SQLAllocHandle function [ODBC]
ms.assetid: 6e7fe420-8cf4-4e72-8dad-212affaff317
caps.latest.revision: 43
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 434b3b42c4e48724b42bdb1ed517b11b25e10db7
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlallochandle-function"></a>SQLAllocHandle-Funktion
**Konformität**  
 Version eingeführt: ODBC 3.0 Standardkonformität: ISO-92  
  
 **Zusammenfassung**  
 **SQLAllocHandle** reserviert ein Handle Umgebung, Verbindung, Anweisung oder Deskriptor.  
  
> [!NOTE]  
>  Diese Funktion ist eine generische Funktion für die Zuordnung von Handles, die die ODBC 2.0-Funktionen ersetzt **SQLAllocConnect**, **SQLAllocEnv**, und **SQLAllocStmt:**. Damit Anwendungen Aufrufen **SQLAllocHandle** zum Arbeiten mit ODBC 2.* X* -Treiber, die einen Aufruf von **SQLAllocHandle** zugeordnet ist, in der Treiber-Manager **SQLAllocConnect**, **SQLAllocEnv**, oder ** SQLAllocStmt:**je nach Bedarf. Weitere Informationen finden Sie unter "Kommentare". Weitere Informationen zu welcher der Treiber-Manager ordnet diese Funktion auf, wenn eine ODBC 3. *x* Anwendung arbeitet mit einer ODBC 2.* X* -Treiber verwenden, finden Sie unter [Ersatz-Zuordnungsfunktionen für Backward Compatibility Anwendungen](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLAllocHandle(  
      SQLSMALLINT   HandleType,  
      SQLHANDLE     InputHandle,  
      SQLHANDLE *   OutputHandlePtr);  
```  
  
## <a name="arguments"></a>Argumente  
 *HandleType*  
 [Eingabe] Der Typ des Handles von zugeordnet werden **SQLAllocHandle**. Dabei muss es sich um einen der folgenden Werte sein:  
  
-   SQL_HANDLE_DBC AUF  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV AUF  
  
-   SQL_HANDLE_STMT AUF  
  
 SQL_HANDLE_DBC_INFO_TOKEN Handle wird nur durch das Treiber-Manager und Treiber verwendet. Anwendungen sollten diese Handletyp nicht verwenden. Weitere Informationen zu SQL_HANDLE_DBC_INFO_TOKEN, finden Sie unter [entwickeln Verbindungspool wissen in eine ODBC-Treiber](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).  
  
 *InputHandle*  
 [Eingabe] Das Eingabe-Handle in das Kontext wird das neue Handle zugeordnet werden soll. Wenn *HandleType* SQL_HANDLE_ENV auf, ist dies die SQL_NULL_HANDLE ist. Wenn *HandleType* ist SQL_HANDLE_DBC auf, diese Angabe muss ein Umgebungshandle und wenn es SQL_HANDLE_STMT oder SQL_HANDLE_DESC handelt, muss er ein Verbindungshandle.  
  
 *OutputHandlePtr*  
 [Ausgabe] Zeiger auf einen Puffer, in dem das Handle auf die neu zugeordneten Datenstruktur zurückgegeben.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_INVALID_HANDLE oder SQL_ERROR zurück.  
  
 Wenn Sie ein Handle als ein Umgebungshandle zuordnen, wenn **SQLAllocHandle** gibt SQL_ERROR zurück, wird *OutputHandlePtr* SQL_NULL_HDBC, SQL_NULL_HSTMT oder SQL_NULL_HDESC, abhängig von der Wert des *HandleType*, es sei denn, das Argument für die Ausgabe ein null-Zeiger ist. Die Anwendung erhalten dann zusätzliche Informationen aus der Diagnosedaten-Struktur verknüpft sind, mit dem Handle in die *InputHandle* Argument.  
  
## <a name="environment-handle-allocation-errors"></a>Aufgrund von Zuordnungsfehlern der Umgebung Handle  
 Umgebung Zuordnung tritt auf, in der Treiber-Manager und in jeden Treiber. Der zurückgegebene Fehler **SQLAllocHandle** mit einem *HandleType* SQL_HANDLE_ENV auf, hängt von der Ebene, in dem der Fehler aufgetreten ist.  
  
 Wenn der Treiber-Manager Speicher zuordnen können * \*OutputHandlePtr* beim **SQLAllocHandle** mit einem *HandleType* SQL_HANDLE_ENV aufgerufen wird, oder die Anwendung enthält einen null-Zeiger für *OutputHandlePtr*, **SQLAllocHandle** gibt SQL_ERROR zurück. Der Treiber-Manager setzt **OutputHandlePtr* auf SQL_NULL_HENV (sofern die Anwendung einen null-Zeiger, die SQL_ERROR zurückgibt). Es ist kein Handle, mit dem zusätzliche Diagnoseinformationen zugeordnet werden soll.  
  
 Der Treiber-Manager wird nicht die Umgebung auf Treiberebene Handle Allocation-Funktion aufgerufen, bis die Anwendung ruft **SQLConnect**, **SQLBrowseConnect**, oder **SQLDriverConnect**. Bei einem in der Treiber-Ebene Fehler **SQLAllocHandle** -Funktion, und klicken Sie dann auf der Treiber-Manager – Ebene **SQLConnect**, **SQLBrowseConnect**, oder ** SQLDriverConnect** -Funktion gibt SQL_ERROR zurück. Die Diagnosedaten-Struktur enthält SQLSTATE IM004 (des Treibers **SQLAllocHandle** fehlgeschlagen). Der Fehler wird für ein Verbindungshandle zurückgegeben.  
  
 Weitere Informationen über den Fluss von Funktionsaufrufen zwischen der Treiber-Manager und einem Treiber finden Sie unter [SQLConnect-Funktion](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLAllocHandle** gibt SQL_ERROR oder SQL_SUCCESS_WITH_INFO, einen zugeordneten SQLSTATE-Wert abgerufen werden können, durch den Aufruf **SQLGetDiagRec** mit dem entsprechenden *HandleType* und *behandeln* legen Sie auf den Wert der *InputHandle*. SQL_SUCCESS_WITH_INFO (aber nicht SQL_ERROR) zurückgegeben werden kann, für die *OutputHandle* Argument. Die folgende Tabelle enthält die SQLSTATE-Werten, die in der Regel zurückgegebenes **SQLAllocHandle** und erläutert, jeweils im Kontext dieser Funktion; die Notation "(DM)" vorangestellt ist, die Beschreibungen der SQLSTATEs, die vom Treiber-Manager zurückgegeben. Der Rückgabecode, der jeden SQLSTATE-Wert zugeordnet wird SQL_ERROR zurückgegeben, sofern nicht anders angegeben.  
  
|SQLSTATE|Fehler|Description|  
|--------------|-----------|-----------------|  
|01000|Allgemeine Warnung|Treiberspezifische Meldung dient zu Informationszwecken. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|08003|Verbindung nicht geöffnet|(DM) die *HandleType* Argument war SQL_HANDLE_STMT oder SQL_HANDLE_DESC, aber die Verbindung angegeben wird, indem Sie die *InputHandle* Argument konnte nicht geöffnet werden. Der Verbindungsprozess erfolgreich abgeschlossen werden muss (und die Verbindung muss geöffnet sein) für den Treiber Zuweisen einer Anweisung oder den Deskriptor behandeln.|  
|HY000|Allgemeiner Fehler|Für die es keine spezifischen SQLSTATE wurde und für die keine implementierungsabhängige SQLSTATE definiert wurde, ist ein Fehler aufgetreten. Die zurückgegebene Fehlermeldung **SQLGetDiagRec** in der **MessageText* Puffer beschreibt den Fehler und seiner Ursache.|  
|HY001|Fehler bei der speicherbelegung|Der Treiber-Manager (DM) konnte nicht belegt werden für das angegebene Handle.<br /><br /> Der Treiber konnte nicht belegt werden für das angegebene Handle.|  
|HY009|Ungültige Verwendung des null-Zeiger|(DM) die *OutputHandlePtr* Argument wurde ein null-Zeiger.|  
|HY010|Fehler bei Funktionssequenz|(DM) die *HandleType* Argument war SQL_HANDLE_DBC auf, und **SQLSetEnvAttr** nicht aufgerufen wurde, um das SQL_ODBC_VERSION Umgebung Attribut festgelegt.<br /><br /> (DM) eine asynchron ausgeführte Funktion wurde aufgerufen, für die **InputHandle** und wurde noch ausgeführt, wenn die **SQLAllocHandle** Funktion aufgerufen wurde **HandleType** festlegen SQL_HANDLE_STMT oder SQL_HANDLE_DESC.|  
|HY013|Speicherverwaltungsfehler|Die *HandleType* Argument war SQL_HANDLE_DBC auf, SQL_HANDLE_STMT oder SQL_HANDLE_DESC; und der Funktionsaufruf konnte nicht verarbeitet werden, da die zugrunde liegenden Speicherobjekte, möglicherweise aufgrund von unzureichendem Arbeitsspeicher konnte nicht zugegriffen werden Bedingungen.|  
|HY014|Das Limit für die Anzahl von Handles wurde überschritten|Das treiberdefinierten Limit für die Anzahl der Handles, die für den Typ des Handle zugeordnet werden kann, angegeben durch die *HandleType* Argument wurde erreicht.|  
|HY092|Ungültiger Attribut-/Optionsbezeichner|(DM) die *HandleType* wurde Argument: SQL_HANDLE_ENV auf SQL_HANDLE_DBC auf, SQL_HANDLE_STMT oder SQL_HANDLE_DESC.|  
|HY117|Verbindung wird aufgrund eines unbekannten Transaktionsstatus angehalten. Nur trennen, und nur-Lese Funktionen sind zulässig.|(DM) finden Sie weitere Informationen zum Zustand "angehalten" [SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Optionales Feature nicht implementiert|Die *HandleType* Argument SQL_HANDLE_DESC und der Treiber wurde eine ODBC 2.* X* Treiber.|  
|HYT01|Verbindungstimeout abgelaufen|Das Verbindungstimeout ist abgelaufen, bevor die Datenquelle auf die Anforderung geantwortet hat. Das Verbindungstimeout wird über festgelegt **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Diese Funktion wird im Treiber nicht unterstützt.|(DM) die *HandleType* Argument SQL_HANDLE_STMT auf, und der Treiber nicht wurde eine gültige ODBC-Treiber.<br /><br /> (DM) die *HandleType* Argument wurde SQL_HANDLE_DESC und der Treiber unterstützt nicht das Zuordnen einer Deskriptorhandles.|  
  
## <a name="comments"></a>Kommentare  
 **SQLAllocHandle** dient zum Zuordnen von Handles für Umgebungen, Verbindungen, Anweisungen und Deskriptoren, wie in den folgenden Abschnitten beschrieben. Allgemeine Informationen zu Handles finden Sie unter [Handles](../../../odbc/reference/develop-app/handles.md).  
  
 Mehr als eine Umgebung, Verbindung oder Anweisung Handle kann von einer Anwendung zu einem Zeitpunkt zugeordnet werden, wenn mehrere Zuordnungen vom Treiber unterstützt werden. In ODBC wird keine Beschränkung definiert, auf die Anzahl der Umgebung, Verbindung, Anweisung oder Deskriptorhandles, die gleichzeitig zugeordnet werden kann. Treiber können es sich um eine Grenze für die Anzahl der Handles verursachen, die zu einem Zeitpunkt zugeordnet werden können; Weitere Informationen finden Sie unter der Treiberdokumentation.  
  
 Wenn die Anwendung aufruft, **SQLAllocHandle** mit * \*OutputHandlePtr* legen auf eine Umgebung, Verbindung, Anweisung oder Deskriptorhandles, die bereits vorhanden ist, der Treiber überschreibt die zugeordnete Informationen der *behandeln*, es sei denn, die Anwendung Connection pooling (siehe "Zuordnen von einer Umgebung Attribut für Verbindungs-Pooling" weiter unten in diesem Abschnitt) verwendet wird. Der Treiber-Manager überprüft nicht, um festzustellen, ob die *behandeln* in eingegeben * \*OutputHandlePtr* wird bereits verwendet wird, noch wird die bisherigen Inhalte der ein Handle überprüfen, bevor diese überschrieben werden .  
  
> [!NOTE]  
>  Falsche ODBC-anwendungsprogrammierung aufrufen ist **SQLAllocHandle** zweimal mit der gleichen Anwendungsvariablen für definiert * \*OutputHandlePtr* ohne Aufruf ** SQLFreeHandle** , bevor Sie es erneut zugewiesen werden, das Freigeben des Handles. Überschreiben von ODBC können Handles auf solche Weise Fehler seitens der ODBC-Treiber zu inkonsistentem Verhalten führen.  
  
 Unter Betriebssystemen, die mehrere Threads zu unterstützen, können Anwendungen in verschiedenen Threads dasselbe Handle Umgebung, Verbindung, Anweisung oder Deskriptor. Treiber müssen daher sicheren, multithread-Zugriff auf diese Informationen unterstützen; eine Möglichkeit, dies zu erreichen, z. B. ist mithilfe eines kritischen Abschnitts oder eine Semaphore. Weitere Informationen zu threading, finden Sie unter [Multithreading](../../../odbc/reference/develop-app/multithreading.md).  
  
 **SQLAllocHandle** SQL_ATTR_ODBC_VERSION-Umgebung-Attribut wird nicht festgelegt, wenn sie aufgerufen wird, ein Umgebungshandle; muss das Attribut für die Umgebung von der Anwendung oder SQLSTATE HY010 festgelegt werden (Funktionsreihenfolge) werden. zurückgegeben, wenn **SQLAllocHandle** aufgerufen, um ein Verbindungshandle zuzuweisen.  
  
 Mit Standards kompatible Anwendungen **SQLAllocHandle** zugeordnet **SQLAllocHandleStd** zum Zeitpunkt der Kompilierung. Der Unterschied zwischen diesen beiden Funktionen ist, dass **SQLAllocHandleStd** wird das SQL_ATTR_ODBC_VERSION-Umgebung-Attribut auf SQL_OV_ODBC3 fest, wenn beim Aufruf der *HandleType* -Argument auf SQL festgelegt _HANDLE_ENV. Dies geschieht, da mit Standards kompatible Anwendungen immer ODBC 3 sind. *x* Anwendungen. Darüber hinaus benötigen den Standards keine Version der Anwendung registriert werden. Dies ist der einzige Unterschied zwischen dieser zwei Funktionen. Andernfalls sind sie identisch. **SQLAllocHandleStd** zugeordnet **SQLAllocHandle** innerhalb der Treiber-Manager. Aus diesem Grund Drittanbieter-Treiber keine implementieren **SQLAllocHandleStd**.  
  
 Es sollten ODBC 3.8-Anwendungen verwenden:  
  
-   **SQLAllocHandle und nicht SQLAllocHandleStd** ein Umgebungshandle zuordnen.  
  
-   **SQLSetEnvAttr** für SQL_OV_ODBC3_80 SQL_ATTR_ODBC_VERSION Umgebung Attributs fest.  
  
## <a name="allocating-an-environment-handle"></a>Zuordnen eines Umgebungshandles  
 Ein Umgebungshandle ermöglicht den Zugriff auf globale Informationen wie gültige Verbindungshandles und aktiver Verbindungshandles. Allgemeine Informationen zu Umgebungshandles, finden Sie unter [Umgebungshandles](../../../odbc/reference/develop-app/environment-handles.md).  
  
 Um ein Umgebungshandle anzufordern, eine Anwendung ruft **SQLAllocHandle** mit einem *HandleType* SQL_HANDLE_ENV auf, und ein *InputHandle* von SQL_NULL_HANDLE. Der Treiber belegt Speicher für die Umgebungsinformationen und übergibt der Wert des zugeordneten Handles wieder in die * \*OutputHandlePtr* Argument. Die Anwendung übergibt die * \*OutputHandle* Wert bei allen nachfolgenden Aufrufen, die Umgebung Handle Argument erforderlich. Weitere Informationen finden Sie unter [Reservieren der Umgebung behandelt](../../../odbc/reference/develop-app/allocating-the-environment-handle.md).  
  
 Unter Umgebungshandle ein Treiber-Manager, wenn es bereits vorhanden ein Treiber Umgebungshandle, klicken Sie dann ist **SQLAllocHandle** mit einem *HandleType* SQL_HANDLE_ENV auf, wird in diesem Treiber nicht aufgerufen beim ein Verbindung hergestellt wird, nur **SQLAllocHandle** mit einem *HandleType* SQL_HANDLE_DBC auf. Wenn ein Treiber Umgebungshandle unter der Treiber-Manager-Umgebungshandle nicht vorhanden ist, SQLAllocHandle mit einem HandleTyp SQL_HANDLE_ENV auf, und mit einem HandleType SQL_HANDLE_DBC SQLAllocHandle heißen im Treiber bei der ersten Verbindung Handle der Umgebung ist für den Treiber verbunden.  
  
 Wenn der Treiber-Manager verarbeitet die **SQLAllocHandle** -Funktion mit einer *HandleType* SQL_HANDLE_ENV auf, überprüft er die **Trace** Schlüsselwort im Abschnitt [ODBC] des Systems Informationen. Wenn es auf 1 festgelegt ist, aktiviert der Treiber-Manager die Ablaufverfolgung für die aktuelle Anwendung. Wenn das Trace-Flag festgelegt ist, beginnt Ablaufverfolgung, wenn das erste Umgebungshandle zugeordnet ist, und endet, wenn das letzte Umgebungshandle freigegeben wird. Weitere Informationen finden Sie unter [Konfigurieren von Datenquellen](../../../odbc/reference/install/configuring-data-sources.md).  
  
 Nach dem Zuordnen eines Umgebungshandles, muss eine Anwendung aufrufen **SQLSetEnvAttr** auf das Umgebungshandle das SQL_ATTR_ODBC_VERSION Umgebung Attribut festgelegt. Wenn dieses Attribut nicht, vor dem festgelegt ist **SQLAllocHandle** aufgerufen, um ein Verbindungshandle zuzuweisen für die Umgebung gibt der Aufruf zum Reservieren der SQLSTATE HY010 zurück (Sequenzfehler-Funktion). Weitere Informationen finden Sie unter [deklarieren Sie der Anwendungsverzeichnis ODBC-Version von](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md).  
  
## <a name="allocating-shared-environments-for-connection-pooling"></a>Zuordnen von freigegebene Umgebungen für das Verbindungspooling  
 Umgebungen können für mehrere Komponenten auf einem einzelnen Prozess genutzt. Eine freigegebene Umgebung kann gleichzeitig von mehreren Komponenten verwendet werden. Wenn eine Komponente eine freigegebene Umgebung verwendet wird, können sie gepoolte Verbindungen verwenden, die zulässt, diese zu reservieren und eine vorhandene Verbindung verwenden, ohne die Verbindung neu zu erstellen.  
  
 Vor dem Zuordnen einer freigegebenen Umgebung, die für das Verbindungspooling verwendet werden kann, muss eine Anwendung aufrufen **SQLSetEnvAttr** Attributs Umgebung SQL_ATTR_CONNECTION_POOLING SQL_CP_ONE_PER_DRIVER oder SQL_CP_ONE_PER_ festlegen HENV. **SQLSetEnvAttr** in diesem Fall mit heißt *EnvironmentHandle* auf Null gesetzt, wodurch dem Attribut ein Attribut auf Prozessebene.  
  
 Nachdem die Verbindungspooling aktiviert wurde, eine Anwendung ruft **SQLAllocHandle** mit der *HandleType* -Argument auf SQL_HANDLE_ENV festgelegt. Eine implizite freigegebenen Umgebung kann von die Umgebung, die durch diesen Aufruf zugeordnet ist, werden, weil Verbindungspooling aktiviert wurde.  
  
 Bei eine freigegebene Umgebung zugeordnet ist, wird die Umgebung, die verwendet werden, nicht bis bestimmt **SQLAllocHandle** mit einem *HandleType* SQL_HANDLE_DBC auf aufgerufen wird. An diesem Punkt versucht der Treiber-Manager, eine vorhandene Umgebung zu finden, die von der Anwendung angeforderte Umgebung Attribute entspricht. Wenn keine solche Umgebung vorhanden ist, wird eine als einer freigegebenen Umgebung erstellt. Der Treiber-Manager verwaltet einen Verweiszähler für die einzelnen freigegebenen Umgebungen. die Anzahl wird auf 1 festgelegt, wenn die Umgebung erstellt wird. Wenn eine übereinstimmende Umgebung gefunden wird, das Handle für diese Umgebung an die Anwendung zurückgegeben, und der Verweiszähler erhöht wird. Ein Umgebungshandle zugeordnet, die auf diese Weise kann in eine ODBC-Funktion verwendet werden, das ein Umgebungshandle als Eingabeargument akzeptiert.  
  
## <a name="allocating-a-connection-handle"></a>Zuordnen eines Verbindungshandles  
 Ein Verbindungshandle ermöglicht den Zugriff auf Informationen, z. B. gültige Anweisung ein, und öffnen Sie Deskriptorhandles auf die Verbindung und gibt an, ob eine Transaktion aktuell ist. Allgemeine Informationen zu Verbindungshandles, finden Sie unter [Verbindungshandles](../../../odbc/reference/develop-app/connection-handles.md).  
  
 Um ein Verbindungshandle zu beantragen, eine Anwendung ruft **SQLAllocHandle** mit einem *HandleType* SQL_HANDLE_DBC auf. Die *InputHandle* Argument wird festgelegt, um das Umgebungshandle, die durch den Aufruf zurückgegeben wurde **SQLAllocHandle** , die dieses Handle zugeordnet. Der Treiber belegt Speicher für die Verbindungsinformationen und übergibt der Wert des zugeordneten Handles wieder * \*OutputHandlePtr*. Die Anwendung übergibt die * \*OutputHandlePtr* Wert bei allen nachfolgenden Aufrufen, die ein Verbindungshandle zu erfordern. Weitere Informationen finden Sie unter [zuzuordnen, eine Verbindung zu behandeln](../../../odbc/reference/develop-app/allocating-a-connection-handle-odbc.md).  
  
 Der Treiber-Manager verarbeitet die **SQLAllocHandle** -Funktion und des Treibers ruft **SQLAllocHandle** -Funktion, wenn die Anwendung aufruft, **SQLConnect**, **SQLBrowseConnect**, oder **SQLDriverConnect**. (Weitere Informationen finden Sie unter [SQLConnect-Funktion](../../../odbc/reference/syntax/sqlconnect-function.md).)  
  
 Wenn das Attribut der SQL_ATTR_ODBC_VERSION-Umgebung vor nicht festgelegt ist **SQLAllocHandle** aufgerufen, um ein Verbindungshandle zuzuweisen für die Umgebung gibt der Aufruf zum Reservieren der SQLSTATE HY010 zurück (Sequence-Funktion (Fehler).  
  
 Wenn eine Anwendung ruft **SQLAllocHandle** mit der *InputHandle* Argument auf SQL_HANDLE_DBC festgelegt wird und auch auf einer freigegebenen Umgebungshandle festlegen, versucht der Treiber-Manager einen vorhandenen freigegebenen zu finden Umgebung, die die Umgebung Attribute, die von der Anwendung festgelegtes übereinstimmt. Wenn keine solche Umgebung vorhanden ist, wird eine mit einer Verweisanzahl von 1 (werden vom Treiber-Manager) erstellt. Wenn ein entsprechender freigegeben Umgebung gefunden wird, dieses Handle wird an die Anwendung zurückgegeben, und der Verweiszähler erhöht.  
  
 Die tatsächliche Verbindung, die verwendet werden, richtet sich nicht vom Treiber-Manager bis **SQLConnect** oder **SQLDriverConnect** aufgerufen wird. Der Treiber-Manager verwendet die Verbindungsoptionen im Aufruf **SQLConnect** (oder die Schlüsselwörter im Aufruf **SQLDriverConnect**) und die Verbindungsattribute festlegen, nach der Zuordnung der Verbindung zu Ermitteln Sie, welche Verbindung im Pool verwendet werden soll. Weitere Informationen finden Sie unter [SQLConnect-Funktion](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
## <a name="allocating-a-statement-handle"></a>Zuordnen eines Anweisungshandles  
 Ein Anweisungshandle ermöglicht den Zugriff auf die Anweisungsinformationen, z. B. Fehlermeldungen, die Cursornamen und Statusinformationen für die Verarbeitung der SQL-Anweisung. Allgemeine Informationen zu Anweisungshandles, finden Sie unter [Anweisungshandles](../../../odbc/reference/develop-app/statement-handles.md).  
  
 Um ein Anweisungshandle anzufordern, eine Anwendung eine Verbindung mit einer Datenquelle her und ruft dann **SQLAllocHandle** , bevor sie SQL-Anweisungen übermittelt. In diesem Aufruf *HandleType* sollte auf SQL_HANDLE_STMT festgelegt werden und *InputHandle* sollte festgelegt werden, um das Verbindungshandle, die durch den Aufruf zurückgegeben wurde **SQLAllocHandle** Dieses Handle reserviert. Der Treiber belegt Speicher für die Anweisungsinformationen, ordnet die angegebene Verbindung, und übergibt der Wert des zugeordneten Handles wieder in das Anweisungshandle * \*OutputHandlePtr*. Die Anwendung übergibt die * \*OutputHandlePtr* Wert bei allen nachfolgenden Aufrufen, die ein Anweisungshandle erfordern. Weitere Informationen finden Sie unter [ein Anweisungshandle zuordnen](../../../odbc/reference/develop-app/allocating-a-statement-handle-odbc.md).  
  
 Wenn das Anweisungshandle zugeordnet ist, der Treiber automatisch ordnet einen Satz von vier Deskriptoren und weist die Handles für diese Deskriptoren der SQL_ATTR_APP_ROW_DESC, SQL_ATTR_APP_PARAM_DESC SQL_ATTR_IMP_ROW_DESC und SQL_ATTR_IMP_PARAM_DESC Anweisungsattribute. Diese werden als bezeichnet *implizit* Deskriptoren zugeordnet. Um eine Anwendungsdiensts explizit zu reservieren, finden Sie unter den folgenden Abschnitt "Zuweisen einer Deskriptorhandles."  
  
## <a name="allocating-a-descriptor-handle"></a>Zuordnen einer Deskriptorhandles  
 Wenn eine Anwendung ruft **SQLAllocHandle** mit einem *HandleType* von SQL_HANDLE_DESC, weist der Treiber eine Anwendungsdiensts. Diese werden als bezeichnet *explizit* Deskriptoren zugeordnet. Die Anwendung weist einen Treiber verwendet, einen explizit zugewiesenen Anwendungsdiensts statt einer automatisch zugeordneten für eine angegebene Anweisungshandle durch Aufrufen der **SQLSetStmtAttr** -Funktion mit dem SQL_ATTR_APP_ROW_DESC oder SQL_ATTR_APP_PARAM_DESC-Attribut. Ein Deskriptor für die Implementierung nicht explizit zugeordnet werden, noch kann in ein Implementierung Deskriptor angegeben werden ein **SQLSetStmtAttr** Funktionsaufruf.  
  
 Explizit zugewiesene Deskriptoren sind ein Verbindungshandle statt ein Anweisungshandle zugeordnet, (wie automatisch zugeordnete Deskriptoren sind). Nur, wenn eine Anwendung tatsächlich mit der Datenbank verbunden ist, werden die Deskriptoren Zuordnung beibehalten. Da explizit zugewiesene Deskriptoren ein Verbindungshandle zugeordnet sind, kann eine Anwendung einen explizit zugewiesenen Deskriptor mehr als eine Anweisung innerhalb einer Verbindung zuordnen. Ein Deskriptor implizit zugeordnete Anwendung kann nicht auf der anderen Seite mehr als ein Anweisungshandle zugeordnet werden. (Es kann keine Anweisungshandle als dasjenige, das sie für zugewiesen wurde zugeordnet werden.) Explizit zugeordneten Deskriptorhandles explizit freigegeben werden können von der Anwendung oder durch Aufrufen von **SQLFreeHandle** mit einem *HandleType* SQL_HANDLE_DESC oder implizit Verbindung geschlossen.  
  
 Wenn der explizit zugewiesene Deskriptor freigegeben wird, ist implizit zugeordneten Deskriptors erneut die Anweisung zugeordnet. (Das Attribut SQL_ATTR_APP_ROW_DESC oder SQL_ATTR_APP_PARAM_DESC für diese Anweisung wird erneut auf die implizit zugeordneten Deskriptorhandles festgelegt.) Dies gilt für alle Anweisungen, die den explizit zugewiesenen Deskriptor für die Verbindung zugeordnet waren.  
  
 Weitere Informationen zu Deskriptoren, finden Sie unter [Deskriptoren](../../../odbc/reference/develop-app/descriptors.md).  
  
## <a name="code-example"></a>Codebeispiel  
 Finden Sie unter [Beispiel-ODBC-Anwendung](../../../odbc/reference/sample-odbc-program.md), [SQLBrowseConnect-Funktion](../../../odbc/reference/syntax/sqlbrowseconnect-function.md), [SQLConnect-Funktion](../../../odbc/reference/syntax/sqlconnect-function.md), und [SQLSetCursorName-Funktion](../../../odbc/reference/syntax/sqlsetcursorname-function.md).  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Ausführen einer SQL­Anweisung|[SQLExecDirect-Funktion](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Ausführen einer vorbereiteten SQL­Anweisung|[SQLExecute-Funktion](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Eine Umgebung, Verbindung, Anweisung oder Deskriptor-Handle freigeben|[SQLFreeHandle-Funktion](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|Vorbereiten einer Anweisung für die Ausführung|[SQLPrepare-Funktion](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|Ein Verbindungsattribut festlegen|[SQLSetConnectAttr-Funktion](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|Festlegen eines Felds Deskriptor|[SQLSetDescField-Funktion](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|Wenn eine Umgebung-Attribut|[SQLSetEnvAttr-Funktion](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|Wenn eine Anweisungsattribut|[SQLSetStmtAttr-Funktion](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)


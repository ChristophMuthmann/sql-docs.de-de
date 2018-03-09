---
title: Verwenden von Multiple Active Resultsets (MARS) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client|features
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, MARS
- SQLNCLI, MARS
- data access [SQL Server Native Client], MARS
- Multiple Active Result Sets
- SQL Server Native Client, MARS
- MARS [SQL Server]
- SQL Server Native Client ODBC driver, MARS
ms.assetid: ecfd9c6b-7d29-41d8-af2e-89d7fb9a1d83
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 89795f3d6b11a93316a2a448dce2ed562db27d02
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="using-multiple-active-result-sets-mars"></a>Verwenden von Multiple Active Result Sets (MARS)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]führte die Unterstützung für mehrere aktive Resultsets (MARS) in Anwendungen, die Zugriff auf die [!INCLUDE[ssDE](../../../includes/ssde-md.md)]. In früheren Versionen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] konnten Datenbankanwendungen nicht mehrere aktive Anweisungen über eine Verbindung verwalten. Beim Verwenden von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Standardresultsets musste die Anwendung alle Resultsets aus einem Batch verarbeiten oder abbrechen, bevor ein anderer Batch auf dieser Verbindung ausgeführt werden konnte. In [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] wurde ein neues Verbindungsattribut eingeführt, das es Anwendungen ermöglicht, mehr als eine ausstehende Anforderung pro Verbindung und mehr als ein aktives Standardresultset pro Verbindung anzugeben.  
  
 MARS vereinfacht den Anwendungsentwurf mit den folgenden neuen Fähigkeiten:  
  
-   Anwendungen können mehrere Standardresultsets geöffnet haben und die Lesevorgänge daraus verschachteln.  
  
-   Anwendungen können bei geöffneten Standardresultsets andere Anweisungen ausführen (z. B. INSERT, UPDATE, DELETE und Aufrufe gespeicherter Prozeduren).  
  
 Für Anwendungen, die MARS verwenden, gelten die folgenden nützlichen Richtlinien:  
  
-   Standardresultsets sollten für kurzlebige oder kurze Resultsets verwendet werden, die durch einzelne SQL-Anweisungen generiert werden (SELECT, DML mit OUTPUT, RECEIVE, READ TEXT usw.).  
  
-   Servercursor sollten für längerlebige oder große Resultsets verwendet werden, die durch einzelne SQL-Anweisungen generierte werden.  
  
-   Lesen Sie bei Batches, die mehrere Ergebnisse zurückgeben, und bei Prozeduranforderungen immer bis zum Ende der Results, unabhängig davon, ob Ergebnisse zurückgeben werden oder nicht.  
  
-   Wo möglich, verwenden Sie anstelle von [!INCLUDE[tsql](../../../includes/tsql-md.md)]-Anweisungen API-Aufrufe, um Verbindungseigenschaften zu ändern und Transaktionen zu verwalten.  
  
-   In MARS wird ein Identitätswechsel im Bereich einer Sitzung verhindert, solange gleichzeitige Batches ausgeführt werden.  
  
> [!NOTE]  
>  Standardmäßig ist die MARS-Funktionalität nicht aktiviert. Um MARS bei der Verbindung mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] über [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client zu verwenden, müssen Sie die Funktionalität in einer Verbindungszeichenfolge explizit aktivieren. Weitere Informationen finden Sie in den Abschnitten zum [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client-OLE DB-Anbieter und dem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client-ODBC-Treiber weiter unten in diesem Thema.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client schränkt die Anzahl aktiver Anweisungen auf einer Verbindung nicht ein.  
  
 Typische Anwendungen, bei denen kein Bedarf für mehrere Batches oder gespeicherte Prozeduren aus mehreren gleichzeitig ausgeführten Anweisungen besteht, profitieren von MARS, ohne die Implementierung von MARS verstehen zu müssen. Anwendungen mit komplexeren Anforderungen müssen diese jedoch berücksichtigen.  
  
 MARS ermöglicht die verschachtelte Ausführung mehrerer Anforderungen innerhalb einer einzelnen Verbindung. Das bedeutet, dass innerhalb der Ausführung eines Batches eine weitere Anforderung ausgeführt werden kann. Beachten Sie jedoch, dass MARS mit Blick auf Interleaving, nicht die parallele Ausführung definiert ist.  
  
 Die MARS-Infrastruktur ermöglicht die verschachtelte Ausführung mehrerer Batches, die Ausführung kann jedoch nur an genau definierten Punkten gewechselt werden. Außerdem müssen die meisten Anweisungen innerhalb eines Batches atomar ausgeführt werden. Anweisungen, die Zeilen zurückgegeben, an den Client, die manchmal auch als bezeichnet werden *zwischenergebnispunkte*, um die Ausführung vor Abschluss verschachteln, während die Zeilen an den Client, z. B. gesendet werden dürfen:  
  
-   SELECT  
  
-   FETCH  
  
-   RECEIVE  
  
 Alle anderen Anweisungen, die im Rahmen einer gespeicherten Prozedur oder eines Batches ausgeführt werden, müssen zunächst abgeschlossen werden, ehe die Ausführung zu anderen MARS-Anforderungen umgeschaltet werden kann.  
  
 Wie Batches die Ausführung genau verschachteln, hängt von zahlreichen Faktoren ab, und die exakte Ausführungsfolge von Befehlen aus mehreren Batches mit Zwischenergebnispunkten lässt sich nur schwer vorhersagen. Achten Sie darauf, unerwünschte Nebeneffekte aufgrund der verschachtelten Ausführung solcher komplexer Batches zu vermeiden.  
  
 Sie vermeiden Probleme, indem Sie den Verbindungsstatus (SET, USE) und Transaktionen (BEGIN TRAN, COMMIT, ROLLBACK) an Stelle von [!INCLUDE[tsql](../../../includes/tsql-md.md)]-Anweisungen mit API-Aufrufen verwalten. Schließen Sie diese Anweisungen zudem nicht in Batches mit mehreren Anweisungen ein, die auch Zwischenergebnispunkte enthalten, und serialisieren Sie die Ausführung solcher Batches durch Verarbeitung oder Abbruch aller Ergebnisse.  
  
> [!NOTE]  
>  Ein Batch oder eine gespeicherte Prozedur, die bei Aktivierung von MARS eine manuelle oder implizite Transaktion startet, muss diese Transaktion vor Ausführung des Batchs abschließen. Andernfalls führt [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nach Abschluss des Batchs einen Rollback für alle von der Transaktion vorgenommenen Änderungen aus. Eine derartige Transaktion wird von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] als Transaktion im Bereich des Batchs verwaltet. Dieser Transaktionstyp wurde in [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] neu eingeführt, um vorhandene, gut konzipierte gespeicherte Prozeduren verwenden zu können, wenn MARS aktiviert ist. Weitere Informationen über Transaktionen im batchbereich finden Sie unter [Transaction-Anweisungen &#40; Transact-SQL &#41; ](~/t-sql/statements/statements.md).  
  
 Ein Beispiel der Verwendung von MARS aus ADO finden Sie unter [mithilfe von ADO mit SQL Server Native Client](../../../relational-databases/native-client/applications/using-ado-with-sql-server-native-client.md).  
  
## <a name="in-memory-oltp"></a>In-Memory OLTP  
 In-Memory OLTP unterstützt MARS mithilfe von Abfragen und systemintern kompilierte gespeicherte Prozeduren. MARS ermöglicht die anfordernde Daten aus mehreren Abfragen ohne die Notwendigkeit, jedes Resultset vor dem Senden einer Anforderung zum Abrufen von Zeilen aus einem neuen Resultset vollständig abzurufen. Zum Lesen von aus mehrere öffnen Ergebnis erfolgreich aktiviert Mengen, die Sie verwenden müssen, eine MARS Verbindung.  
  
 MARS ist standardmäßig deaktiviert, damit Sie sie explizit durch Hinzufügen von aktivieren müssen `MultipleActiveResultSets=True` auf eine Verbindungszeichenfolge. Im folgenden Beispiel wird veranschaulicht, wie eine Verbindung mit einer Instanz von SQL Server und angeben, dass MARS aktiviert ist:  
  
```  
Data Source=MSSQL; Initial Catalog=AdventureWorks; Integrated Security=SSPI; MultipleActiveResultSets=True  
```  
  
 MARS mit In-Memory OLTP ist im Wesentlichen identisch mit MARS im Rest des SQL-Datenbankmoduls. Im folgenden werden die Unterschiede beim Verwenden von MARS in speicheroptimierten Tabellen und systemintern gespeicherter Prozeduren kompilierter.  
  
 **MARS und Speicheroptimierte Tabellen**  
  
 Im folgenden sind die Unterschiede zwischen datenträgerbasierte und Speicheroptimierte Tabellen bei der Verbindung mit einer MARS aktiviert werden:  
  
-   Zwei Anweisungen können Daten in dasselbe Zielobjekt ändern, jedoch wenn beide versuchen, denselben Datensatz zu ändern führen ein Write-Write-Konflikt den neuen Vorgang fehlschlägt. Wenn beide Vorgänge unterschiedliche Datensätze ändern, jedoch erfolgreich die Vorgänge.  
  
-   Jede Anweisung unter momentaufnahmeisolation ausgeführt wird, damit neue Vorgänge von den vorhandenen Anweisungen vorgenommene Änderungen sehen können. Auch wenn die gleichzeitige Anweisungen innerhalb derselben Transaktion ausgeführt werden erstellt die SQL-Datenbankmodul batchbereich Transaktionen für jede Anweisung, die voneinander isoliert sind. Transaktionen mit batchbereich sind damit Rollback einer Transaktion mit batchbereich anderen werden im selben Batch wirkt sich jedoch weiterhin zusammen gebunden.  
  
-   DDL-Vorgänge sind in Benutzertransaktionen nicht zulässig, sodass sie sofort fehl.  
  
 **MARS und systemintern kompilierte gespeicherte Prozeduren**  
  
 Systemintern kompilierte gespeicherte Prozeduren können in den aktivierter MARS-Verbindungen ausführen und können die Ausführung auf einer anderen Anweisung zurückhalten, nur, wenn ein Yield-Punkt gefunden wird. Ein Yield-Punkt erfordert eine SELECT-Anweisung, also die einzige Anweisung in einer systemintern kompilierten gespeicherten Prozedur, die Ausführung einer anderen Anweisung ergeben können. Wenn eine SELECT-Anweisung nicht in die Prozedur vorhanden ist, nicht gedachten, wird sie vor anderen Anweisungen bis zum Abschluss ausgeführt.  
  
 **MARS und In-Memory OLTP-Transaktionen**  
  
 Von Anweisungen und atomic-Blöcken, die sich überlappen vorgenommenen Änderungen sind voneinander isoliert. Z. B. wenn eine Anweisung oder atomic-Block nimmt einige Änderungen vor, und klicken Sie dann setzt die Ausführung auf einer anderen Anweisung, sehen die neue Anweisung nicht durch die erste Anweisung vorgenommene Änderungen. Darüber hinaus bei der ersten Anweisung die Ausführung wird fortgesetzt, wird er keine Änderungen, die von allen anderen Anweisungen angezeigt. -Anweisungen können nur Änderungen sehen, die abgeschlossen und ein Commit ausgeführt, bevor die Anweisung beginnt.  
  
 Eine neue Benutzertransaktion innerhalb der aktuellen Benutzer Transaktions mithilfe der BEGIN TRANSACTION-Anweisung gestartet werden kann – dies ist nur im Interop-Modus unterstützt werden, damit die BEGIN TRANSACTION nur von einer T-SQL-Anweisung aufgerufen werden kann und nicht von innerhalb einer systemintern kompilierten gespeicherten die Prozedur. Sie können einen Sicherungspunkt erstellen, zeigen Sie mit SAVE TRANSACTION oder einen API-Aufruf Transaktion in einer Transaktion. Save(save_point_name), ein Rollback zu dem Sicherungspunkt ausgeführt. Dieses Feature wird auch nur von T-SQL-Anweisungen aktiviert und nicht von innerhalb von systemintern kompilierten gespeicherten Prozeduren.  
  
 **MARS und columnstore-Indizes**  
  
 SQL Server (ab 2016) unterstützt MARS mit columnstore-Indizes. SQL Server 2014 verwendet MARS für schreibgeschützte Verbindungen zu Tabellen mit einem columnstore-Index.    SQL Server 2014 unterstützt jedoch nicht MARS für gleichzeitige Data Manipulation Language (DML)-Vorgängen für eine Tabelle mit einem columnstore-Index. In diesem Fall wird SQL Server beendet die Verbindungen und Transaktionen abgebrochen.   SQL Server 2012 wurde nur-Lese columnstore-Indizes und MARS gilt nicht für sie.  
  
## <a name="sql-server-native-client-ole-db-provider"></a>SQL Server Native Client OLE DB-Anbieter  
 Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter unterstützt MARS durch Hinzufügen der SSPROP_INIT_MARSCONNECTION Initialisierungseigenschaft-Datenquellen, die in der Eigenschaftengruppe DBPROPSET_SQLSERVERDBINIT implementiert wird. Darüber hinaus eine neue Verbindungszeichenfolgen-Schlüsselwort, **MarsConn**aufgenommen wurde. Er akzeptiert **"true"** oder **"false"** Werte. **"false"** ist die Standardeinstellung.  
  
 Die Datenquelleneigenschaft DBPROP_MULTIPLECONNECTIONS ist standardmäßig auf VARIANT_TRUE festgelegt. Das bedeutet, der Anbieter erzeugt mehrere Verbindungen, um mehrere gleichzeitige Befehls- und Rowsetobjekte zu unterstützen. Wenn MARS aktiviert ist, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client können mehrere Befehls- und Rowsetobjekte Objekte über eine einzelne Verbindung unterstützen, daher ist MULTIPLE_CONNECTIONS standardmäßig auf VARIANT_FALSE festgelegt ist.  
  
 Weitere Informationen zu Verbesserungen am DBPROPSET_SQLSERVERDBINIT-Eigenschaftensatz finden Sie unter [Initialisierungs- und Autorisierungseigenschaften](../../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md).  
  
### <a name="sql-server-native-client-ole-db-provider-example"></a>OLE DB-Anbieter von SQL Server Native Client: Beispiel  
 In diesem Beispiel wird ein Datenquellenobjekt erstellt, mit der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native OLE DB-Anbieter und MARS ist aktiviert mithilfe der DBPROPSET_SQLSERVERDBINIT-Eigenschaftensatz, bevor das Sitzungsobjekt erstellt wird.  
  
```  
#include <sqlncli.h>  
  
IDBInitialize *pIDBInitialize = NULL;  
IDBCreateSession *pIDBCreateSession = NULL;  
IDBProperties *pIDBProperties = NULL;  
  
// Create the data source object.  
hr = CoCreateInstance(CLSID_SQLNCLI10, NULL,  
   CLSCTX_INPROC_SERVER,  
   IID_IDBInitialize,   
    (void**)&pIDBInitialize);  
  
hr = pIDBInitialize->QueryInterface(IID_IDBProperties, (void**)&pIDBProperties);  
  
// Set the MARS property.  
DBPROP rgPropMARS;  
  
// The following is necessary since MARS is off by default.  
rgPropMARS.dwPropertyID = SSPROP_INIT_MARSCONNECTION;  
rgPropMARS.dwOptions = DBPROPOPTIONS_REQUIRED;  
rgPropMARS.dwStatus = DBPROPSTATUS_OK;  
rgPropMARS.colid = DB_NULLID;  
V_VT(&(rgPropMARS.vValue)) = VT_BOOL;  
V_BOOL(&(rgPropMARS.vValue)) = VARIANT_TRUE;  
  
// Create the structure containing the properties.  
DBPROPSET PropSet;  
PropSet.rgProperties = &rgPropMARS;  
PropSet.cProperties = 1;  
PropSet.guidPropertySet = DBPROPSET_SQLSERVERDBINIT;  
  
// Get an IDBProperties pointer and set the initialization properties.  
pIDBProperties->SetProperties(1, &PropSet);  
pIDBProperties->Release();  
  
// Initialize the data source object.  
hr = pIDBInitialize->Initialize();  
  
//Create a session object from a data source object.  
IOpenRowset * pIOpenRowset = NULL;  
hr = IDBInitialize->QueryInterface(IID_IDBCreateSession, (void**)&pIDBCreateSession));  
hr = pIDBCreateSession->CreateSession(  
   NULL,             // pUnkOuter  
   IID_IOpenRowset,  // riid  
  &pIOpenRowset ));  // ppSession  
  
// Create a rowset with a firehose mode cursor.  
IRowset *pIRowset = NULL;  
DBPROP rgRowsetProperties[2];  
  
// To get a firehose mode cursor request a   
// forward only read only rowset.  
rgRowsetProperties[0].dwPropertyID = DBPROP_IRowsetLocate;  
rgRowsetProperties[0].dwOptions = DBPROPOPTIONS_REQUIRED;  
rgRowsetProperties[0].dwStatus = DBPROPSTATUS_OK;  
rgRowsetProperties[0].colid = DB_NULLID;  
VariantInit(&(rgRowsetProperties[0].vValue));  
rgRowsetProperties[0].vValue.vt = VARIANT_BOOL;  
rgRowsetProperties[0].vValue.boolVal = VARIANT_FALSE;  
  
rgRowsetProperties[1].dwPropertyID = DBPROP_IRowsetChange;  
rgRowsetProperties[1].dwOptions = DBPROPOPTIONS_REQUIRED;  
rgRowsetProperties[1].dwStatus = DBPROPSTATUS_OK;  
rgRowsetProperties[1].colid = DB_NULLID;  
VariantInit(&(rgRowsetProperties[1].vValue));  
rgRowsetProperties[1].vValue.vt = VARIANT_BOOL;  
rgRowsetProperties[1].vValue.boolVal = VARIANT_FALSE;  
  
DBPROPSET rgRowsetPropSet[1];  
rgRowsetPropSet[0].rgProperties = rgRowsetProperties  
rgRowsetPropSet[0].cProperties = 2  
rgRowsetPropSet[0].guidPropertySet = DBPROPSET_ROWSET;  
  
hr = pIOpenRowset->OpenRowset (NULL,  
   &TableID,  
   NULL,  
   IID_IRowset,  
   1,  
   rgRowsetPropSet  
   (IUnknown**)&pIRowset);  
```  
  
## <a name="sql-server-native-client-odbc-driver"></a>ODBC-Treiber für SQL Server Native Client  
 Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber unterstützt MARS durch Hinzufügungen zu den [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) und [SQLGetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md) Funktionen. SQL_COPT_SS_MARS_ENABLED wurde hinzugefügt, um entweder SQL_MARS_ENABLED_YES oder SQL_MARS_ENABLED_NO zu akzeptieren. Der Standardwert ist SQL_MARS_ENABLED_NO. Darüber hinaus eine neue Verbindungszeichenfolgen-Schlüsselwort, **Mars_Connection**aufgenommen wurde. Gültige Werte sind "Ja" oder "Nein", wobei "Nein" die Standardeinstellung ist.  
  
### <a name="sql-server-native-client-odbc-driver-example"></a>SQL Server Native Client-ODBC-Treiber: Beispiel  
 In diesem Beispiel wird die **SQLSetConnectAttr** Funktion dient zum Aktivieren von MARS vor dem Aufruf der **SQLDriverConnect** Funktion zum Verbinden mit der Datenbank. Sobald die Verbindung hergestellt wird, zwei **SQLExecDirect** Funktionen zum Erstellen von zwei gesonderte Resultsets für dieselbe Verbindung aufgerufen werden.  
  
```  
#include <sqlncli.h>  
  
SQLSetConnectAttr(hdbc, SQL_COPT_SS_MARS_ENABLED, SQL_MARS_ENABLED_YES, SQL_IS_UINTEGER);  
SQLDriverConnect(hdbc, hwnd,   
   "DRIVER=SQL Server Native Client 10.0;  
   SERVER=(local);trusted_connection=yes;", SQL_NTS, szOutConn,   
   MAX_CONN_OUT, &cbOutConn, SQL_DRIVER_COMPLETE);  
  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt1);  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt2);  
  
// The 2nd execute would have failed with connection busy error if  
// MARS were not enabled.  
SQLExecDirect(hstmt1, L”SELECT * FROM Authors”, SQL_NTS);  
SQLExecDirect(hstmt2, L”SELECT * FROM Titles”, SQL_NTS);  
  
// Result set processing can interleave.  
SQLFetch(hstmt1);  
SQLFetch(hstmt2);  
```  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server Native Client-Funktionen](../../../relational-databases/native-client/features/sql-server-native-client-features.md)   
 [Verwenden von SQL Server-Standardresultsets](../../../relational-databases/native-client-odbc-cursors/implementation/using-sql-server-default-result-sets.md)  
  
  

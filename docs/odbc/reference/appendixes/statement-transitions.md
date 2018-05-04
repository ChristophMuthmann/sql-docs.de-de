---
title: Anweisung Übergänge | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- transitioning states [ODBC], statement
- state transitions [ODBC], statement
- statement transitions [ODBC]
ms.assetid: 3d70e0e3-fe83-4b4d-beac-42c82495a05b
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5f20ec0efb42e877695c44f4d62c4ffc1ae79806
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="statement-transitions"></a>Anweisung Übergänge
ODBC-Anweisungen werden die folgenden Status haben.  
  
|Status|Description|  
|-----------|-----------------|  
|S0|Nicht zugeordnete Anweisung. (Der Zustand der Verbindung muss C4, C5 oder C6 sein. Weitere Informationen finden Sie unter [Verbindung Übergänge](../../../odbc/reference/appendixes/connection-transitions.md).)|  
|S1|Reservierte Anweisung.|  
|S2|Vorbereitete Anweisung. Es wird kein Resultset erstellt.|  
|S3|Vorbereitete Anweisung. Ein Resultset (möglicherweise leere) wird erstellt.|  
|S4|Anweisung ausgeführt wird und kein Resultset erstellt wurde.|  
|S5|Ausgeführte Anweisung und eine (möglicherweise leere) Resultset erstellt wurde. Der Cursor ist geöffnet und positioniert vor der ersten Zeile des Resultsets.|  
|S6|Cursor positioniert mit **SQLFetch** oder **SQLFetchScroll**.|  
|S7|Cursor positioniert mit **SQLExtendedFetch**.|  
|A8|Funktion benötigt Daten. **SQLParamData** nicht aufgerufen wurde.|  
|S9|Funktion benötigt Daten. **SQLPutData** nicht aufgerufen wurde.|  
|S10|Funktion benötigt Daten. **SQLPutData** aufgerufen wurde.|  
|S11|Noch ausgeführt wird. Eine Anweisung ist in diesem Zustand bleibt, nachdem eine Funktion, die asynchron ausgeführt wird SQL_STILL_EXECUTING zurückgibt. Eine Anweisung ist vorübergehend in diesem Zustand, bei der alle Funktionen, die akzeptiert ein Anweisungshandle ausgeführt wird. Temporäre Wohnort in S11 keine Statustabellen mit Ausnahme der Statustabelle für enthält **SQLCancel**. Während eine Anweisung vorübergehend im Zustand S11 befindet, kann die Funktion abgebrochen werden, durch den Aufruf **SQLCancel** aus einem anderen Thread.|  
|S12|Asynchrone Ausführung abgebrochen. In S12 muss eine Anwendung die abgebrochene-Funktion aufrufen, bis sie einen anderen Wert als SQL_STILL_EXECUTING zurückgibt. Die Funktion wurde erfolgreich abgebrochen, nur, wenn die Funktion SQL_ERROR und SQLSTATE HY008 zurückgibt (der Vorgang wurde abgebrochen). Wenn einen anderer Wert, z. B. SQL_SUCCESS, Fehler beim Vorgang "Abbrechen", und die Funktion, die normal ausgeführt zurückgegeben.|  
  
 Zustände S2 und S3 bekannt sind, als die vorbereiteten Status besagt S5 über S7 beim besagt, Zustände a8 über S10 als die Notwendigkeit von datenänderungen und S11 und S12 als die asynchronen Status besagt der Cursor. In jeder dieser Spaltengruppen werden die Übergänge separat angezeigt, nur, wenn sie für jeden Status in der Gruppe unterschiedlich sind. in den meisten Fällen Statusübergänge der für jede in den einzelnen eine Gruppe sind identisch.  
  
 Die folgenden Tabellen zeigen, wie jede ODBC-Funktion den Status der Anweisung auswirkt.  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|S0<br /><br /> Nicht zugeordnet|S1<br /><br /> Belegt|S2 – S3<br /><br /> Vorbereitet|S4<br /><br /> ausgeführt|S5 – S7<br /><br /> Cursor|A8 – S10<br /><br /> Daten erforderlich|S11 – S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1], [5], [6]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|--[2], [5]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|S1 [3]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|--[4], [5]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
  
 [1] für diese Zeile zeigt die Übergänge beim *HandleType* SQL_HANDLE_ENV wurde.  
  
 [2] für diese Zeile zeigt die Übergänge beim *HandleType* SQL_HANDLE_DBC wurde.  
  
 [3] für diese Zeile zeigt die Übergänge beim *HandleType* SQL_HANDLE_STMT wurde.  
  
 [4] für diese Zeile zeigt die Übergänge beim *HandleType* SQL_HANDLE_DESC wurde.  
  
 [5] aufrufen **SQLAllocHandle** mit *OutputHandlePtr* verweist auf ein gültiges Handle dieses Handle ohne Berücksichtigung überschreibt, für die bisherigen Inhalte auf, behandeln und für ODBC-Treiber Probleme verursachen. Falsche ODBC-anwendungsprogrammierung aufrufen ist **SQLAllocHandle** zweimal mit der gleichen Anwendungsvariablen für definiert  *\*OutputHandlePtr* ohne Aufruf  **SQLFreeHandle** , bevor Sie es erneut zugewiesen werden, das Freigeben des Handles. Überschreiben von ODBC könnte Handles auf solche Weise Fehler seitens der ODBC-Treiber zu inkonsistentem Verhalten führen.  
  
## <a name="sqlbindcol"></a>SQLBindCol  
  
|S0<br /><br /> Nicht zugeordnet|S1<br /><br /> Belegt|S2 – S3<br /><br /> Vorbereitet|S4<br /><br /> ausgeführt|S5 – S7<br /><br /> Cursor|A8 – S10<br /><br /> Daten erforderlich|S11 – S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|SODASS|--|--|--|--|HY010|HY010|  
  
## <a name="sqlbindparameter"></a>SQLBindParameter  
  
|S0<br /><br /> Nicht zugeordnet|S1<br /><br /> Belegt|S2 – S3<br /><br /> Vorbereitet|S4<br /><br /> ausgeführt|S5 – S7<br /><br /> Cursor|A8 – S10<br /><br /> Daten erforderlich|S11 – S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|SODASS|--|--|--|--|HY010|HY010|  
  
## <a name="sqlbrowseconnect-sqlconnect-and-sqldriverconnect"></a>SQLBrowseConnect SQLConnect und SQLDriverConnect  
  
|S0<br /><br /> Nicht zugeordnet|S1<br /><br /> Belegt|S2 – S3<br /><br /> Vorbereitet|S4<br /><br /> ausgeführt|S5 – S7<br /><br /> Cursor|A8 – S10<br /><br /> Daten erforderlich|S11 – S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|08002|08002|08002|08002|08002|08002|08002|  
  
## <a name="sqlbulkoperations"></a>SQLBulkOperations  
  
|S0<br /><br /> Nicht zugeordnet|S1<br /><br /> Belegt|S2 – S3<br /><br /> Vorbereitet|S4<br /><br /> ausgeführt|S5 – S7<br /><br /> Cursor|A8 – S10<br /><br /> Daten erforderlich|S11 – S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|SODASS|HY010|HY010|24000|Finden Sie in der nächsten Tabelle|HY010|Die HY010 o NS [c]|  
  
## <a name="sqlbulkoperations-cursor-states"></a>SQLBulkOperations (Cursor Staaten)  
  
|S5<br /><br /> Geöffnet|S6<br /><br /> SQLFetch oder SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|--[s] a8 [d] S11 [X]|--[s] a8 [d] S11 [X]|HY010|  
  
## <a name="sqlcancel"></a>SQLCancel  
  
|S0<br /><br /> Nicht zugeordnet|S1<br /><br /> Belegt|S2 – S3<br /><br /> Vorbereitet|S4<br /><br /> ausgeführt|S5 – S7<br /><br /> Cursor|A8 – S10<br /><br /> Daten erforderlich|S11 – S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|SODASS|--|--|--|--|S1 [1] S2 [Nr.] und [2] S3 [R] und [2] S5 [3] und [5] a6 ([3] oder [4]) und [6] S7 [4] und [7]|Finden Sie in der nächsten Tabelle|  
  
 [1] **SQLExecDirect** SQL_NEED_DATA zurückgegeben.  
  
 [2] **SQLExecute** SQL_NEED_DATA zurückgegeben.  
  
 [3] **SQLBulkOperations** SQL_NEED_DATA zurückgegeben.  
  
 [4] **SQLSetPos** SQL_NEED_DATA zurückgegeben.  
  
 [5] **SQLFetch**, **SQLFetchScroll**, oder **SQLExtendedFetch** nicht aufgerufen wurde.  
  
 [6] **SQLFetch** oder **SQLFetchScroll** hatte aufgerufen wurde.  
  
 [7] **SQLExtendedFetch** hatte aufgerufen wurde.  
  
## <a name="sqlcancel-asynchronous-states"></a>SQLCancel (asynchrone Zustand)  
  
|S11<br /><br /> Immer noch ausgeführt.|S12<br /><br /> Asynchrone abgebrochen|  
|-----------------------------|-----------------------------|  
|NS [1] S12 [2]|S12|  
  
 [1]. die Anweisung wurde vorübergehend im Zustand S11, während der Ausführung einer funktionsrückgabewerts. **SQLCancel** wurde von einem anderen Thread aufgerufen.  
  
 [2]-Anweisung war im Zustand S11, da eine Funktion, die asynchron aufgerufen SQL_STILL_EXECUTING zurückgegeben.  
  
## <a name="sqlclosecursor"></a>SQLCloseCursor  
  
|S0<br /><br /> Nicht zugeordnet|S1<br /><br /> Belegt|S2 – S3<br /><br /> Vorbereitet|S4<br /><br /> ausgeführt|S5 – S7<br /><br /> Cursor|A8 – S10<br /><br /> Daten erforderlich|S11 – S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|SODASS|24000|24000|24000|S1 [Np] S3 [p]|HY010|HY010|  
  
## <a name="sqlcolattribute"></a>SQLColAttribute  
  
|S0<br /><br /> Nicht zugeordnet|S1<br /><br /> Belegt|S2 – S3<br /><br /> Vorbereitet|S4<br /><br /> ausgeführt|S5 – S7<br /><br /> Cursor|A8 – S10<br /><br /> Daten erforderlich|S11 – S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|SODASS|HY010|Finden Sie in der nächsten Tabelle|24000|--[s] S11 [X]|HY010|Die HY010 o NS [c]|  
  
## <a name="sqlcolattribute-prepared-states"></a>SQLColAttribute (vorbereiteten Staaten)  
  
|S2<br /><br /> Keine Ergebnisse|S3<br /><br /> Ergebnisse|  
|-----------------------|--------------------|  
|--[1] 07005[2]|--[s] S11 X|  
  
 [1] *FieldIdentifier* SQL_DESC_COUNT wurde.  
  
 [2] *FieldIdentifier* war nicht SQL_DESC_COUNT.  
  
## <a name="sqlcolumnprivileges-sqlcolumns-sqlforeignkeys-sqlgettypeinfo-sqlprimarykeys-sqlprocedurecolumns-sqlprocedures-sqlspecialcolumns-sqlstatistics-sqltableprivileges-and-sqltables"></a>SQLColumnPrivileges, SQLColumns SQLForeignKeys, SQLGetTypeInfo, SQLPrimaryKeys, SQLProcedureColumns, SQLProcedures, SQLSpecialColumns, SQLStatistics, SQLTablePrivileges und SQLTables  
  
|S0<br /><br /> Nicht zugeordnet|S1<br /><br /> Belegt|S2 – S3<br /><br /> Vorbereitet|S4<br /><br /> ausgeführt|S5 – S7<br /><br /> Cursor|A8 – S10<br /><br /> Daten erforderlich|S11 – S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|S5 [s] S11 [X]|S1 [e] S5 [s] S11 [X]|S1 [e] und [1] S5 [s] und [1] S11 [X] und [1] 24000 [2]|Finden Sie in der nächsten Tabelle|HY010|Die HY010 o NS [c]|  
  
 [1] ' ist das aktuelle Ergebnis ist die letzte oder nur als Ergebnis zurück, oder es sind keine aktuellen Ergebnisse. Weitere Informationen zu verschiedenen Ergebnissen, finden Sie unter [mehrere Ergebnisse](../../../odbc/reference/develop-app/multiple-results.md).  
  
 [2] ' ist das aktuelle Ergebnis ist nicht das letzte Ergebnis.  
  
## <a name="sqlcolumnprivileges-sqlcolumns-sqlforeignkeys-sqlgettypeinfo-sqlprimarykeys-sqlprocedurecolumns-sqlprocedures-sqlspecialcolumns-sqlstatistics-sqltableprivileges-and-sqltables-cursor-states"></a>SQLColumnPrivileges, SQLColumns SQLForeignKeys, SQLGetTypeInfo, SQLPrimaryKeys, SQLProcedureColumns, SQLProcedures, SQLSpecialColumns, SQLStatistics, SQLTablePrivileges und SQLTables (Cursor Staaten)  
  
|S5<br /><br /> Geöffnet|S6<br /><br /> SQLFetch oder SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|24000[1]|24000|  
  
 [1]. dieser Fehler wird vom Treiber-Manager zurückgegeben, wenn **SQLFetch** oder **SQLFetchScroll** wurden keine SQL_NO_DATA zurückgegeben und wird vom Treiber zurückgegeben, wenn **SQLFetch** oder **SQLFetchScroll** SQL_NO_DATA zurückgegeben hat.  
  
## <a name="sqlcopydesc"></a>SQLCopyDesc  
  
|S0<br /><br /> Nicht zugeordnet|S1<br /><br /> Belegt|S2 – S3<br /><br /> Vorbereitet|S4<br /><br /> ausgeführt|S5 – S7<br /><br /> Cursor|A8 – S10<br /><br /> Daten erforderlich|S11 – S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|SODASS [1]|--|--|--|--|HY010|NS [c] und [3] HY010 [o] oder [4]|  
|SODASS [2]|HY010|Finden Sie in der nächsten Tabelle|24000|--[s] S11 X|HY010|NS [c] und [3] HY010 [o] oder [4]|  
  
 [1] für diese Zeile zeigt die Übergänge bei der *SourceDescHandle* Argument wurde ein ARD, APD oder IPD.  
  
 [2] für diese Zeile zeigt die Übergänge bei der *SourceDescHandle* Argument wurde ein IRD.  
  
 [3] der *SourceDescHandle* und *TargetDescHandle* Argumente wurden entspricht der Vorgehensweise in der **SQLCopyDesc** -Funktion, die asynchron ausgeführt wird.  
  
 [4] entweder die *SourceDescHandle* Argument oder die *TargetDescHandle* Argument (oder beides) wurden in puncto der **SQLCopyDesc** -Funktion, die ausgeführt wird asynchron.  
  
## <a name="sqlcopydesc-prepared-states"></a>SQLCopyDesc (vorbereiteten Staaten)  
  
|S2<br /><br /> Keine Ergebnisse|S3<br /><br /> Ergebnisse|  
|-----------------------|--------------------|  
|24000[1]|--[s] S11 [X]|  
  
 [1] Diese Zeile zeigt die Übergänge bei der *SourceDescHandle* Argument wurde ein IRD.  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSources und SQLDrivers  
  
|S0<br /><br /> Nicht zugeordnet|S1<br /><br /> Belegt|S2 – S3<br /><br /> Vorbereitet|S4<br /><br /> ausgeführt|S5 – S7<br /><br /> Cursor|A8 – S10<br /><br /> Daten erforderlich|S11 – S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqldescribecol"></a>SQLDescribeCol  
  
|S0<br /><br /> Nicht zugeordnet|S1<br /><br /> Belegt|S2 – S3<br /><br /> Vorbereitet|S4<br /><br /> ausgeführt|S5 – S7<br /><br /> Cursor|A8 – S10<br /><br /> Daten erforderlich|S11 – S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|SODASS|HY010|Finden Sie in der nächsten Tabelle|24000|--[s] S11 [X]|HY010|Die HY010 o NS [c]|  
  
## <a name="sqldescribecol-prepared-states"></a>SQLDescribeCol (vorbereiteten Staaten)  
  
|S2<br /><br /> Keine Ergebnisse|S3<br /><br /> Ergebnisse|  
|-----------------------|--------------------|  
|07005|--[s] S11 [X]|  
  
## <a name="sqldescribeparam"></a>SQLDescribeParam  
  
|S0<br /><br /> Nicht zugeordnet|S1<br /><br /> Belegt|S2 – S3<br /><br /> Vorbereitet|S4<br /><br /> ausgeführt|S5 – S7<br /><br /> Cursor|A8 – S10<br /><br /> Daten erforderlich|S11 – S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|SODASS|HY010|--[s] S11 [X]|HY010|HY010|HY010|NS [c] HY010 [o]|  
  
## <a name="sqldisconnect"></a>SQLDisconnect  
  
|S0<br /><br /> Nicht zugeordnet|S1<br /><br /> Belegt|S2 – S3<br /><br /> Vorbereitet|S4<br /><br /> ausgeführt|S5 – S7<br /><br /> Cursor|A8 – S10<br /><br /> Daten erforderlich|S11 – S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|S0 [1]|S0 [1]|S0 [1]|S0 [1]|(HY010)|(HY010)|  
  
 [1] aufrufen **SQLDisconnect** freigegeben alle Anweisungen, die der Verbindung zugeordnet. Darüber hinaus gibt dies den Verbindungsstatus in C2 zurück; der Verbindungsstatus muss C4 sein, bevor der Zustand der Anweisung S0 ist.  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|S0<br /><br /> Nicht zugeordnet|S1<br /><br /> Belegt|S2 – S3<br /><br /> Vorbereitet|S4<br /><br /> ausgeführt|S5 – S7<br /><br /> Cursor|A8 – S10<br /><br /> Daten erforderlich|S11 – S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--[2] oder [3] S1 [1]|--' [3] ' S1 [Np] und ([1] oder [2]) S1 [p] und [1] S2 [p] und [2]|--' [3] ' S1 [Np] und ([1] oder [2]) S1 [p] und [1] S3 [p] und [2]|(HY010)|(HY010)|  
  
 [1] der *' CompletionType '* Argument ist SQL_COMMIT und **SQLGetInfo** SQL_CB_DELETE für den Informationstyp SQL_CURSOR_COMMIT_BEHAVIOR zurückgegeben oder *' CompletionType '* Argument ist SQL_ROLLBACK und **SQLGetInfo** SQL_CB_DELETE für den Typ der SQL_CURSOR_ROLLBACK_BEHAVIOR Informationen zurückgegeben.  
  
 [2] der *' CompletionType '* Argument ist SQL_COMMIT und **SQLGetInfo** SQL_CB_CLOSE für den Informationstyp SQL_CURSOR_COMMIT_BEHAVIOR zurückgegeben oder *' CompletionType '* Argument ist SQL_ROLLBACK und **SQLGetInfo** SQL_CB_CLOSE für den Typ der SQL_CURSOR_ROLLBACK_BEHAVIOR Informationen zurückgegeben.  
  
 [3] der *' CompletionType '* Argument ist SQL_COMMIT und **SQLGetInfo** SQL_CB_PRESERVE für den Informationstyp SQL_CURSOR_COMMIT_BEHAVIOR zurückgegeben oder *' CompletionType '* Argument ist SQL_ROLLBACK und **SQLGetInfo** SQL_CB_PRESERVE für den Typ der SQL_CURSOR_ROLLBACK_BEHAVIOR Informationen zurückgegeben.  
  
## <a name="sqlexecdirect"></a>SQLExecDirect  
  
|S0<br /><br /> Nicht zugeordnet|S1<br /><br /> Belegt|S2 – S3<br /><br /> Vorbereitet|S4<br /><br /> ausgeführt|S5 – S7<br /><br /> Cursor|A8 – S10<br /><br /> Daten erforderlich|S11 – S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|S4 [s] und [Nr.] S5 [s] und [R] [d] a8 S11 [X]|--[e] und [1] S1 [e] und [2] S4 [s] und [Nr.] S5 [s] und [R] [d] a8 S11 [X]|--[e], [1] und [3] S1 [e], [2] und [3] S4 [s], [Nr.], und [3] S5 [s] [R], und a8 [3] [d] und [3] S11 [X] und [3] 24000 [4]|Finden Sie in der nächsten Tabelle|HY010|NS [c] HY010 [o]|  
  
 [1] der Fehler wurde vom Treiber-Manager zurückgegeben.  
  
 [2] der Fehler wurde vom Treiber-Manager nicht zurückgegeben.  
  
 [3] ' ist das aktuelle Ergebnis ist die letzte oder nur als Ergebnis zurück, oder es sind keine aktuellen Ergebnisse. Weitere Informationen zu verschiedenen Ergebnissen, finden Sie unter [mehrere Ergebnisse](../../../odbc/reference/develop-app/multiple-results.md).  
  
 [4] ' ist das aktuelle Ergebnis ist nicht das letzte Ergebnis.  
  
## <a name="sqlexecdirect-cursor-states"></a>SQLExecDirect (Cursor Staaten)  
  
|S5<br /><br /> Geöffnet|S6<br /><br /> SQLFetch oder SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|24000 [1]|24000|  
  
 [1]. dieser Fehler wird vom Treiber-Manager zurückgegeben, wenn **SQLFetch** oder **SQLFetchScroll** wurden keine SQL_NO_DATA zurückgegeben und wird vom Treiber zurückgegeben, wenn **SQLFetch** oder  **SQLFetchScroll** SQL_NO_DATA zurückgegeben hat.  
  
## <a name="sqlexecute"></a>SQLExecute  
  
|S0<br /><br /> Nicht zugeordnet|S1<br /><br /> Belegt|S2 – S3<br /><br /> Vorbereitet|S4<br /><br /> ausgeführt|S5 – S7<br /><br /> Cursor|A8 – S10<br /><br /> Daten erforderlich|S11 – S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|(HY010)|Finden Sie in der nächsten Tabelle|S2 [e], p und [1] S4 [s] [p], [Nr.], und [1] S5 [s] [p], [R] und [1] [d] a8 [p] und [1] S11 [x], [p], und [1] 24000 [p] und [2] HY010 [Np]|Finden Sie unter Cursor-Statustabelle|HY010|NS [c] HY010 [o]|  
  
 [1] ' ist das aktuelle Ergebnis ist die letzte oder nur als Ergebnis zurück, oder es sind keine aktuellen Ergebnisse. Weitere Informationen zu verschiedenen Ergebnissen, finden Sie unter [mehrere Ergebnisse](../../../odbc/reference/develop-app/multiple-results.md).  
  
 [2] ' ist das aktuelle Ergebnis ist nicht das letzte Ergebnis.  
  
## <a name="sqlexecute-prepared-states"></a>SQLExecute (vorbereiteten Staaten)  
  
|S2<br /><br /> Keine Ergebnisse|S3<br /><br /> Ergebnisse|  
|-----------------------|--------------------|  
|S4 [s] [d] a8 S11 [X]|S5 [s] [d] a8 S11 [X]|  
  
## <a name="sqlexecute-cursor-states"></a>SQLExecute (Cursor Staaten)  
  
|S5<br /><br /> Geöffnet|S6<br /><br /> SQLFetch oder SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000 [p] HY010 [Np]|24000 [p], [1] HY010 [Np]|24000 [p] HY010 [Np]|  
  
 [1]. dieser Fehler wird vom Treiber-Manager zurückgegeben, wenn **SQLFetch** oder **SQLFetchScroll** wurden keine SQL_NO_DATA zurückgegeben und wird vom Treiber zurückgegeben, wenn **SQLFetch** oder  **SQLFetchScroll** SQL_NO_DATA zurückgegeben hat.  
  
## <a name="sqlextendedfetch"></a>SQLExtendedFetch  
  
|S0<br /><br /> Nicht zugeordnet|S1<br /><br /> Belegt|S2 – S3<br /><br /> Vorbereitet|S4<br /><br /> ausgeführt|S5 – S7<br /><br /> Cursor|A8 – S10<br /><br /> Daten erforderlich|S11 – S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|SODASS|S1010|S1010|24000|Finden Sie in der nächsten Tabelle|S1010|NS [c] S1010 [o]|  
  
## <a name="sqlextendedfetch-cursor-states"></a>SQLExtendedFetch (Cursor Staaten)  
  
|S5<br /><br /> Geöffnet|S6<br /><br /> SQLFetch oder SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|S7 [s] oder [nf] S11 [X]|S1010|--[s] oder [nf] S11 [X]|  
  
## <a name="sqlfetch-and-sqlfetchscroll"></a>SQLFetch und SQLFetchScroll  
  
|S0<br /><br /> Nicht zugeordnet|S1<br /><br /> Belegt|S2 – S3<br /><br /> Vorbereitet|S4<br /><br /> ausgeführt|S5 – S7<br /><br /> Cursor|A8 – S10<br /><br /> Daten erforderlich|S11 – S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|SODASS|HY010|HY010|24000|Finden Sie in der nächsten Tabelle|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlfetch-and-sqlfetchscroll-cursor-states"></a>SQLFetch und SQLFetchScroll (Cursor Staaten)  
  
|S5<br /><br /> Geöffnet|S6<br /><br /> SQLFetch oder SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|A6 [s] oder [nf] S11 [X]|--[s] oder [nf] S11 [X]|HY010|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|S0<br /><br /> Nicht zugeordnet|S1<br /><br /> Belegt|S2 – S3<br /><br /> Vorbereitet|S4<br /><br /> ausgeführt|S5 – S7<br /><br /> Cursor|A8 – S10<br /><br /> Daten erforderlich|S11 – S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|-- [1]|HY010|HY010|HY010|HY010|HY010|HY010|  
|SODASS [2]|S0|S0|S0|S0|HY010|HY010|  
|-- [3]|--|--|--|--|--|--|  
  
 [1] für diese Zeile zeigt die Übergänge beim *HandleType* wurde SQL_HANDLE_ENV oder SQL_HANDLE_DBC auf.  
  
 [2] für diese Zeile zeigt die Übergänge beim *HandleType* SQL_HANDLE_STMT wurde.  
  
 [3] für diese Zeile zeigt die Übergänge beim *HandleType* SQL_HANDLE_DESC wurde und der Deskriptor explizit zugewiesen wurde.  
  
## <a name="sqlfreestmt"></a>'SQLFreeStmt'  
  
|S0<br /><br /> Nicht zugeordnet|S1<br /><br /> Belegt|S2 – S3<br /><br /> Vorbereitet|S4<br /><br /> ausgeführt|S5 – S7<br /><br /> Cursor|A8 – S10<br /><br /> Daten erforderlich|S11 – S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|SODASS [1]|--|--|S1 [Np] S2 [p]|S1 [Np] S3 [p]|HY010|HY010|  
|SODASS [2]|--|--|--|--|HY010|HY010|  
  
 [1] für diese Zeile zeigt die Übergänge beim *Option* SQL_CLOSE wurde.  
  
 [2] für diese Zeile zeigt die Übergänge beim *Option* SQL_UNBIND oder SQL_RESET_PARAMS wurde. Wenn die *Option* Argument wurde SQL_DROP und der zugrunde liegenden Treiber ist ein ODBC 3.*.x* Treiber, der Treiber-Manager ordnet dies zu einem Aufruf von **SQLFreeHandle** mit  *HandleType* auf SQL_HANDLE_STMT festgelegt wird. Weitere Informationen finden Sie in der Tabelle der Zustandsübergänge für [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md).  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
  
|S0<br /><br /> Nicht zugeordnet|S1<br /><br /> Belegt|S2 – S3<br /><br /> Vorbereitet|S4<br /><br /> ausgeführt|S5 – S7<br /><br /> Cursor|A8 – S10<br /><br /> Daten erforderlich|S11 – S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetcursorname"></a>SQLGetCursorName  
  
|S0<br /><br /> Nicht zugeordnet|S1<br /><br /> Belegt|S2 – S3<br /><br /> Vorbereitet|S4<br /><br /> ausgeführt|S5 – S7<br /><br /> Cursor|A8 – S10<br /><br /> Daten erforderlich|S11 – S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|SODASS|--|--|--|--|HY010|HY010|  
  
## <a name="sqlgetdata"></a>SQLGetData  
  
|S0<br /><br /> Nicht zugeordnet|S1<br /><br /> Belegt|S2 – S3<br /><br /> Vorbereitet|S4<br /><br /> ausgeführt|S5 – S7<br /><br /> Cursor|A8 – S10<br /><br /> Daten erforderlich|S11 – S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|SODASS|HY010|HY010|24000|Finden Sie in der nächsten Tabelle|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlgetdata-cursor-states"></a>SQLGetData (Cursor Staaten)  
  
|S5<br /><br /> Geöffnet|S6<br /><br /> SQLFetch oder SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|--[s] oder [nf] S11 [x] 24000 [b] HY109 [i]|--[s] oder [nf] S11 [x] 24000 [b] HY109 [i]|  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec"></a>SQLGetDescField und SQLGetDescRec  
  
|S0<br /><br /> Nicht zugeordnet|S1<br /><br /> Belegt|S2 – S3<br /><br /> Vorbereitet|S4<br /><br /> ausgeführt|S5 – S7<br /><br /> Cursor|A8 – S10<br /><br /> Daten erforderlich|S11 – S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|SODASS|--[1] oder [2] HY010 [3]|Finden Sie in der nächsten Tabelle|--[1] oder [2] 24000 [3]|--[1], [2] oder [3] S11 [3] und [X]|HY010|NS [c] oder [4] HY010 [o] und [5]|  
  
 [1] der *DescriptorHandle* Argument war ein APD oder ARD.  
  
 [2] der *DescriptorHandle* Argument wurde ein IPD.  
  
 [3] der *DescriptorHandle* Argument wurde ein IRD.  
  
 [4] der *DescriptorHandle* Argument wurde das gleiche wie der *DescriptorHandle* Argument in der **SQLGetDescField** oder **SQLGetDescRec** Funktion, die asynchron ausgeführt wird.  
  
 [5] der *DescriptorHandle* Argument war anders als die *DescriptorHandle* Argument in der **SQLGetDescField** oder **SQLGetDescRec**-Funktion, die asynchron ausgeführt wird.  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec-prepared-states"></a>SQLGetDescField und SQLGetDescRec (vorbereiteten Staaten)  
  
|S2<br /><br /> Keine Ergebnisse|S3<br /><br /> Ergebnisse|  
|-----------------------|--------------------|  
|--[1], [2] oder [3] S11 [2] und [X]|--[1], [2] oder [3] S11 [X]|  
  
 [1] der *DescriptorHandle* Argument war ein APD oder ARD.  
  
 [2] der *DescriptorHandle* Argument wurde ein IPD.  
  
 [3] der *DescriptorHandle* Argument wurde ein IRD. Beachten Sie, dass diese Funktionen SQL_NO_DATA immer in den Zustand S2 zurück Wenn *DescriptorHandle* wurde ein IRD.  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagField und SQLGetDiagRec  
  
|S0<br /><br /> Nicht zugeordnet|S1<br /><br /> Belegt|S2 – S3<br /><br /> Vorbereitet|S4<br /><br /> ausgeführt|S5 – S7<br /><br /> Cursor|A8 – S10<br /><br /> Daten erforderlich|S11 – S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|--|--|--|--|--|--|  
|SODASS [2]|--[3]|--[3]|--|--|--[3]|--[3]|  
  
 [1] für diese Zeile zeigt die Übergänge beim *HandleType* SQL_HANDLE_ENV auf SQL_HANDLE_DBC oder SQL_HANDLE_DESC wurde.  
  
 [2] für diese Zeile zeigt die Übergänge beim *HandleType* SQL_HANDLE_STMT wurde.  
  
 [3] **SQLGetDiagField** immer gibt einen Fehler in diesem Zustand über, wenn *DiagIdentifier* SQL_DIAG_ROW_COUNT ist.  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr  
  
|S0<br /><br /> Nicht zugeordnet|S1<br /><br /> Belegt|S2 – S3<br /><br /> Vorbereitet|S4<br /><br /> ausgeführt|S5 – S7<br /><br /> Cursor|A8 – S10<br /><br /> Daten erforderlich|S11 – S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetfunctions"></a>SQLGetFunctions  
  
|S0<br /><br /> Nicht zugeordnet|S1<br /><br /> Belegt|S2 – S3<br /><br /> Vorbereitet|S4<br /><br /> ausgeführt|S5 – S7<br /><br /> Cursor|A8 – S10<br /><br /> Daten erforderlich|S11 – S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetinfo"></a>SQLGetInfo  
  
|S0<br /><br /> Nicht zugeordnet|S1<br /><br /> Belegt|S2 – S3<br /><br /> Vorbereitet|S4<br /><br /> ausgeführt|S5 – S7<br /><br /> Cursor|A8 – S10<br /><br /> Daten erforderlich|S11 – S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetstmtattr"></a>'SQLGetStmtAttr'  
  
|S0<br /><br /> Nicht zugeordnet|S1<br /><br /> Belegt|S2 – S3<br /><br /> Vorbereitet|S4<br /><br /> ausgeführt|S5 – S7<br /><br /> Cursor|A8 – S10<br /><br /> Daten erforderlich|S11 – S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|SODASS|--[1] 24000[2]|--[1] 24000[2]|--[1] 24000[2]|Finden Sie in der nächsten Tabelle|HY010|HY010|  
  
 [1] das Anweisungsattribut war nicht SQL_ATTR_ROW_NUMBER.  
  
 [2] ' ist das Anweisungsattribut wurde SQL_ATTR_ROW_NUMBER.  
  
## <a name="sqlgetstmtattr-cursor-states"></a>SQLGetStmtAttr (Cursor Staaten)  
  
|S5<br /><br /> Geöffnet|S6<br /><br /> SQLFetch oder SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|--[1] 24000[2]|--[1] oder ([V] und [2]) 24000 [b] und [2] HY109 [i] und [2]|--[i] oder ([V] und [2]) 24000 [b] und [2] HY109 [1] und [2]|  
  
 [1] der *Attribut* Argument war kein SQL_ATTR_ROW_NUMBER.  
  
 [2] der *Attribut* Argument war SQL_ATTR_ROW_NUMBER.  
  
## <a name="sqlmoreresults"></a>SQLMoreResults  
  
|S0<br /><br /> Nicht zugeordnet|S1<br /><br /> Belegt|S2 – S3<br /><br /> Vorbereitet|S4<br /><br /> ausgeführt|S5 – S7<br /><br /> Cursor|A8 – S10<br /><br /> Daten erforderlich|S11 – S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|--[1]|--[1]|--[s] und [2] S1 [nf], [Np,] und [4] S2 [nf], [p] und [4] S5 [s] und [3] S11 [X]|S1 [nf], [Np,] und [4] S3 [nf], [p] und [4] S4 [s] und [2] S5 [s] und [3] S11 [X]|HY010|NS [c] HY010 [o]|  
  
 [1]. die Funktion gibt SQL_NO_DATA immer in diesem Status.  
  
 [2] ' ist das nächste Ergebnis ist die Zeilenanzahl.  
  
 [3] ' ist das nächste Ergebnis ist ein Resultset.  
  
 [4] ' ist das aktuelle Ergebnis ist das letzte Ergebnis.  
  
## <a name="sqlnativesql"></a>SQLNativeSql  
  
|S0<br /><br /> Nicht zugeordnet|S1<br /><br /> Belegt|S2 – S3<br /><br /> Vorbereitet|S4<br /><br /> ausgeführt|S5 – S7<br /><br /> Cursor|A8 – S10<br /><br /> Daten erforderlich|S11 – S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlnumparams"></a>SQLNumParams  
  
|S0<br /><br /> Nicht zugeordnet|S1<br /><br /> Belegt|S2 – S3<br /><br /> Vorbereitet|S4<br /><br /> ausgeführt|S5 – S7<br /><br /> Cursor|A8 – S10<br /><br /> Daten erforderlich|S11 – S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|SODASS|HY010|--[s] S11 [X]|--[s] S11 [X]|--[s] S11 [X]|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlnumresultcols"></a>SQLNumResultCols  
  
|S0<br /><br /> Nicht zugeordnet|S1<br /><br /> Belegt|S2 – S3<br /><br /> Vorbereitet|S4<br /><br /> ausgeführt|S5 – S7<br /><br /> Cursor|A8 – S10<br /><br /> Daten erforderlich|S11 – S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|SODASS|HY010|--[s] S11 [X]|--[s] S11 [X]|--[s] S11 [X]|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlparamdata"></a>SQLParamData  
  
|S0<br /><br /> Nicht zugeordnet|S1<br /><br /> Belegt|S2 – S3<br /><br /> Vorbereitet|S4<br /><br /> ausgeführt|S5 – S7<br /><br /> Cursor|A8 – S10<br /><br /> Daten erforderlich|S11 – S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|SODASS|HY010|HY010|HY010|HY010|Finden Sie in der nächsten Tabelle|NS [c] HY010 [o]|  
  
## <a name="sqlparamdata-need-data-states"></a>SQLParamData (müssen Daten Staaten)  
  
|A8<br /><br /> Daten erforderlich|S9<br /><br /> Darf höchstens|S10<br /><br /> Können einfügen|  
|----------------------|---------------------|---------------------|  
|S1 [e] und [1] S2 [e], [Nr.,] und [2] S3 [e], [R] und [2] S5 [e] und [4] a6 [e] und [5] S7 [e] und S9 [3] [d] S11 [X]|HY010|S1 [e] und [1] S2 [e], [Nr.], und [2] S3 [e] [R] und [2] S4 [s], [Nr.], und ([1] oder [2]) S5 [s] [R], und ([1] oder [2]) S5 ([s] "oder" [e]) und [4] a6 ([s] "oder" [e]) und [5] S7 ([s] "oder" [e]) und S9 [3] [d] S11 [X]|  
  
 [1] **SQLExecDirect** SQL_NEED_DATA zurückgegeben.  
  
 [2] **SQLExecute** SQL_NEED_DATA zurückgegeben.  
  
 [3] **SQLSetPos** SQL_NEED_DATA zurückgegeben und vom Zustand S7 aufgerufen wurde.  
  
 [4] **SQLBulkOperations** SQL_NEED_DATA zurückgegeben und vom Zustand S5 aufgerufen wurde.  
  
 [5] **SQLSetPos** oder **SQLBulkOperations** SQL_NEED_DATA zurückgegeben und vom Zustand a6 aufgerufen wurde.  
  
## <a name="sqlprepare"></a>SQLPrepare  
  
|S0<br /><br /> Nicht zugeordnet|S1<br /><br /> Belegt|S2 – S3<br /><br /> Vorbereitet|S4<br /><br /> ausgeführt|S5 – S7<br /><br /> Cursor|A8 – S10<br /><br /> Daten erforderlich|S11 – S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|S2 [s] und [Nr.] S3 [s] und [R] S11 [X]|--[s] oder ([e] und [1]) S1 [e] und [2] S11 [X]|S1 [e] und [3] S2 [s], [Nr.,] und [3] S3 [s] [R] und [3] S11 [X] und [3] 24000 [4]|Finden Sie in der nächsten Tabelle|HY010|NS [c] HY010 [o]|  
  
 [1] die Vorbereitung für einem anderen Grund als überprüfen die Anweisung schlägt fehl (SQLSTATE wurde HY009 [Ungültiger Argumentwert] oder HY090 [ungültige Zeichenfolgen- oder Pufferlänge.]).  
  
 [2] die Vorbereitung ein Fehler auftritt, während der Überprüfung der Anweisung (SQLSTATE war nicht HY009 [Ungültiger Argumentwert] oder HY090 [ungültige Zeichenfolgen- oder Pufferlänge.]).  
  
 [3] ' ist das aktuelle Ergebnis ist die letzte oder nur als Ergebnis zurück, oder es sind keine aktuellen Ergebnisse. Weitere Informationen zu verschiedenen Ergebnissen, finden Sie unter [mehrere Ergebnisse](../../../odbc/reference/develop-app/multiple-results.md).  
  
 [4] ' ist das aktuelle Ergebnis ist nicht das letzte Ergebnis.  
  
## <a name="sqlprepare-cursor-states"></a>SQLPrepare (Cursor Staaten)  
  
|S5<br /><br /> Geöffnet|S6<br /><br /> SQLFetch oder SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|24000|24000|  
  
## <a name="sqlputdata"></a>SQLPutData  
  
|S0<br /><br /> Nicht zugeordnet|S1<br /><br /> Belegt|S2 – S3<br /><br /> Vorbereitet|S4<br /><br /> ausgeführt|S5 – S7<br /><br /> Cursor|A8 – S10<br /><br /> Daten erforderlich|S11 – S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|SODASS|HY010|HY010|HY010|HY010|Finden Sie in der nächsten Tabelle|NS [c] HY010 [o]|  
  
## <a name="sqlputdata-need-data-states"></a>SQLPutData (müssen Daten Staaten)  
  
|A8<br /><br /> Daten erforderlich|S9<br /><br /> Darf höchstens|S10<br /><br /> Können einfügen|  
|----------------------|---------------------|---------------------|  
|HY010|S1 [e] und [1] S2 [e], [Nr.,] und [2] S3 [e], [R] und [2] S5 [e] und [4] a6 [e] und [5] S7 [e] und [3] S10 [s] S11 [X]|--[s] S1 [e] und [1] S2 [e], [Nr.,] und [2] S3 [e], [R] und [2] S5 [e] und [4] a6 [e] und [5] S7 [e] und [3] S11 [X] HY011 [6]|  
  
 [1] **SQLExecDirect** SQL_NEED_DATA zurückgegeben.  
  
 [2] **SQLExecute** SQL_NEED_DATA zurückgegeben.  
  
 [3] **SQLSetPos** SQL_NEED_DATA zurückgegeben und vom Zustand S7 aufgerufen wurde.  
  
 [4] **SQLBulkOperations** SQL_NEED_DATA zurückgegeben und vom Zustand S5 aufgerufen wurde.  
  
 [5] **SQLSetPos** oder **SQLBulkOperations** SQL_NEED_DATA zurückgegeben und vom Zustand a6 aufgerufen wurde.  
  
 [6] eine oder mehrere Aufrufe von **SQLPutData** für ein einzelnen Parameter SQL_SUCCESS zurück, und klicken Sie dann mit einem Aufruf von zurückgegebenen **SQLPutData** wurde versucht, für den gleichen Parameter mit *StrLen_or_Ind* festlegen auf SQL_NULL_DATA.  
  
## <a name="sqlrowcount"></a>SQLRowCount  
  
|S0<br /><br /> Nicht zugeordnet|S1<br /><br /> Belegt|S2 – S3<br /><br /> Vorbereitet|S4<br /><br /> ausgeführt|S5 – S7<br /><br /> Cursor|A8 – S10<br /><br /> Daten erforderlich|S11 – S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|(HY010)|(HY010)|--|--|(HY010)|(HY010)|  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
  
|S0<br /><br /> Nicht zugeordnet|S1<br /><br /> Belegt|S2 – S3<br /><br /> Vorbereitet|S4<br /><br /> ausgeführt|S5 – S7<br /><br /> Cursor|A8 – S10<br /><br /> Daten erforderlich|S11 – S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|--|--|--|--[2] 24000[3]|HY010|HY010|  
  
 [1] für diese Zeile zeigt die Übergänge beim *Attribut* wurde ein Verbindungsattribut. Für geht beim *Attribut* wurde eine Anweisung-Attribut angegeben wird, finden Sie in der Anweisung übergangstabelle **SQLSetStmtAttr**.  
  
 [2] der *Attribut* Argument war kein SQL_ATTR_CURRENT_CATALOG.  
  
 [3] der *Attribut* Argument war SQL_ATTR_CURRENT_CATALOG.  
  
## <a name="sqlsetcursorname"></a>SQLSetCursorName  
  
|S0<br /><br /> Nicht zugeordnet|S1<br /><br /> Belegt|S2 – S3<br /><br /> Vorbereitet|S4<br /><br /> ausgeführt|S5 – S7<br /><br /> Cursor|A8 – S10<br /><br /> Daten erforderlich|S11 – S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|SODASS|--|--|24000|24000|HY010|HY010|  
  
## <a name="sqlsetdescfield-and-sqlsetdescrec"></a>SQLSetDescField und SQLSetDescRec  
  
|S0<br /><br /> Nicht zugeordnet|S1<br /><br /> Belegt|S2 – S3<br /><br /> Vorbereitet|S4<br /><br /> ausgeführt|S5 – S7<br /><br /> Cursor|A8 – S10<br /><br /> Daten erforderlich|S11 – S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|SODASS [1]|--|--|--|--|HY010|HY010|  
  
 [1] für diese Zeile zeigt die Übergänge, in dem die *DescriptorHandle* Argument ist ein ARD, APD, IPD, oder (für **SQLSetDescField**) ein IRD bei der *FieldIdentifier* Argument ist SQL_ DESC_ARRAY_STATUS_PTR oder SQL_DESC_ROWS_PROCESSED_PTR. Es ist ein Fehler auf, rufen Sie **SQLSetDescField** für eine IRD beim *FieldIdentifier* beliebiger anderer Wert ist.  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|S0<br /><br /> Nicht zugeordnet|S1<br /><br /> Belegt|S2 – S3<br /><br /> Vorbereitet|S4<br /><br /> ausgeführt|S5 – S7<br /><br /> Cursor|A8 – S10<br /><br /> Daten erforderlich|S11 – S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|HY011|HY011|HY011|HY011|Y011|HY01|HY011|  
  
## <a name="sqlsetpos"></a>SQLSetPos  
  
|S0<br /><br /> Nicht zugeordnet|S1<br /><br /> Belegt|S2 – S3<br /><br /> Vorbereitet|S4<br /><br /> ausgeführt|S5 – S7<br /><br /> Cursor|A8 – S10<br /><br /> Daten erforderlich|S11 – S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|SODASS|HY010|HY010|24000|Finden Sie in der nächsten Tabelle|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlsetpos-cursor-states"></a>SQLSetPos (Cursor Staaten)  
  
|S5<br /><br /> Geöffnet|S6<br /><br /> SQLFetch oder SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|--[s] [d] a8 S11 [24000 [b] HY109 x] [i]|--[s] [d] a8 S11 [24000 [b] HY109 x] [i]|  
  
## <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
  
|S0<br /><br /> Nicht zugeordnet|S1<br /><br /> Belegt|S2 – S3<br /><br /> Vorbereitet|S4<br /><br /> ausgeführt|S5 – S7<br /><br /> Cursor|A8 – S10<br /><br /> Daten erforderlich|S11 – S12<br /><br /> Async|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|SODASS|--|--[1] HY011 [2]|--[1] 24000[2]|--[1] 24000[2]|HY010 [Np] oder [1] HY011 [p] und [2]|HY010 [Np] oder [1] HY011 [p] und [2]|  
  
 [1] der *Attribut* Argument war kein SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE, SQL_ATTR_SIMULATE_CURSOR, SQL_ATTR_USE_BOOKMARKS, SQL_ATTR_CURSOR_SCROLLABLE und SQL_ATTR_CURSOR_SENSITIVITY.  
  
 [2] der *Attribut* Argument war SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE, SQL_ATTR_SIMULATE_CURSOR, SQL_ATTR_USE_BOOKMARKS, SQL_ATTR_CURSOR_SCROLLABLE und SQL_ATTR_CURSOR_SENSITIVITY.

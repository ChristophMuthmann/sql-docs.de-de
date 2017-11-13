---
title: "Verbindung Übergänge | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transitioning states [ODBC], connection
- connection transitions [ODBC]
- state transitions [ODBC], connection
ms.assetid: 6b6e1a47-4a52-41c8-bb9e-7ddeae09913e
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8af5cd175cdd9ab7d96cdb141bcd0a6b6100ea80
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="connection-transitions"></a>Verbindung Übergänge
ODBC-Verbindungen werden die folgenden Status haben.  
  
|Status|Description|  
|-----------|-----------------|  
|C0|Nicht zugeordnete-Umgebung verfügbaren Verbindung|  
|C1|Zugeordnete-Umgebung verfügbaren Verbindung|  
|C2|Zugeordnete Verbindung zugeordneten-Umgebung|  
|C3|Verbindungsfunktion benötigt Daten.|  
|C4|Verbundene Verbindung|  
|C5|Verbindung zugeordnete Anweisung verbunden|  
|C6|Verbundene Verbindung, Transaktion ausgeführt. Es ist möglich, eine Verbindung herzustellen, die im Zustand C6 mit Anweisungen, die nicht für die Verbindung zugewiesen werden. Nehmen wir beispielsweise an, die Verbindung befindet sich im manuellen Commit-Modus und befindet sich im Status C4. Wenn eine Anweisung zugeordnet, (zum Starten einer Transaktion) ausgeführt und anschließend freigegeben, die Transaktion bleibt aktiv, aber es gibt keine Anweisungen für die Verbindung.|  
  
 Die folgenden Tabellen zeigen, wie jede ODBC-Funktion den Verbindungsstatus auswirkt.  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|C0<br /><br /> Keine Env.|Nicht zugewiesener C1|C2<br /><br /> Belegt|C3<br /><br /> Daten erforderlich|C4<br /><br /> Verbunden|C5<br /><br /> -Anweisung.|C6<br /><br /> Transaction|  
|--------------------|--------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|C1 [1]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|(SODASS) [2]|C2|--[5]|--[5]|--[5]|--[5]|--[5]|  
|(SODASS) [3]|(SODASS)|(08003)|(08003)|C5|--[5]|--[5]|  
|(SODASS) [4]|(SODASS)|(08003)|(08003)|--[5]|--[5]|--[5]|  
  
 [1] für diese Zeile zeigt die Übergänge beim *HandleType* SQL_HANDLE_ENV wurde.  
  
 [2] für diese Zeile zeigt die Übergänge beim *HandleType* SQL_HANDLE_DBC wurde.  
  
 [3] für diese Zeile zeigt die Übergänge beim *HandleType* SQL_HANDLE_STMT wurde.  
  
 [4] für diese Zeile zeigt die Übergänge beim *HandleType* SQL_HANDLE_DESC wurde.  
  
 [5] aufrufen **SQLAllocHandle** mit *OutputHandlePtr* überschreibt dieses Handle ohne Berücksichtigung der vorherige Inhalt Ofthat Handle auf ein gültiges Handle verweist, und für ODBC-Treiber Probleme verursachen. Falsche ODBC-anwendungsprogrammierung aufrufen ist **SQLAllocHandle** zweimal mit der gleichen Anwendungsvariablen für definiert  *\*OutputHandlePtr* ohne Aufruf  **SQLFreeHandle** , bevor Sie es erneut zugewiesen werden, das Freigeben des Handles. Überschreiben von ODBC können Handles auf solche Weise Fehler seitens der ODBC-Treiber zu inkonsistentem Verhalten führen.  
  
## <a name="sqlbrowseconnect"></a>SQLBrowseConnect  
  
|C0<br /><br /> Keine Env.|C1<br /><br /> Nicht zugeordnet|C2<br /><br /> Belegt|C3<br /><br /> Daten erforderlich|C4<br /><br /> Verbunden|C5<br /><br /> -Anweisung.|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(SODASS)|(SODASS)|C4 C3 [d] [s]|--[d] C2 [e] C4 [s]|(08002)|(08002)|(08002)|  
  
## <a name="sqlclosecursor"></a>SQLCloseCursor  
  
|C0<br /><br /> Keine Env.|C1<br /><br /> Nicht zugeordnet|C2<br /><br /> Belegt|C3<br /><br /> Daten erforderlich|C4<br /><br /> Verbunden|C5<br /><br /> -Anweisung.|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(SODASS)|(SODASS)|(SODASS)|(SODASS)|(SODASS)|--|--[1] C5 [2]|  
  
 [1]. die Verbindung wurde im Manualcommit Modus.  
  
 [2]. die Verbindung wurde im Autocommit Modus.  
  
## <a name="sqlcolumnprivileges-sqlcolumns-sqlforeignkeys-sqlgettypeinfo-sqlprimarykeys-sqlprocedurecolumns-sqlprocedures-sqlspecialcolumns-sqlstatistics-sqltableprivileges-and-sqltables"></a>SQLColumnPrivileges, SQLColumns SQLForeignKeys, SQLGetTypeInfo, SQLPrimaryKeys, SQLProcedureColumns, SQLProcedures, SQLSpecialColumns, SQLStatistics, SQLTablePrivileges und SQLTables  
  
|C0<br /><br /> Keine Env.|C1<br /><br /> Nicht zugeordnet|C2<br /><br /> Belegt|C3<br /><br /> Daten erforderlich|C4<br /><br /> Verbunden|C5<br /><br /> -Anweisung.|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(SODASS)|(SODASS)|(SODASS)|(SODASS)|(SODASS)|--[1] C6 [2]|--|  
  
 [1]. die Verbindung im Autocommit Modus wurde, oder die Datenquelle eine Transaktion nicht beginnen.  
  
 [2]. die Verbindung wurde im Manualcommit Modus, und die Datenquelle begonnen wurde, eine Transaktion.  
  
## <a name="sqlconnect"></a>SQLConnect  
  
|C0<br /><br /> Keine Env.|C1<br /><br /> Nicht zugeordnet|C2<br /><br /> Belegt|C3<br /><br /> Daten erforderlich|C4<br /><br /> Verbunden|C5<br /><br /> -Anweisung.|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(SODASS)|(SODASS)|C4|(08002)|(08002)|(08002)|(08002)|  
  
## <a name="sqlcopydesc-sqlgetdescfield-sqlgetdescrec-sqlsetdescfield-and-sqlsetdescrec"></a>SQLCopyDesc, SQLGetDescField SQLGetDescRec, SQLSetDescField und SQLSetDescRec  
  
|C0<br /><br /> Keine Env.|C1<br /><br /> Nicht zugeordnet|C2<br /><br /> Belegt|C3<br /><br /> Daten erforderlich|C4<br /><br /> Verbunden|C5<br /><br /> -Anweisung.|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(SODASS)|(SODASS)|(SODASS)|(SODASS)|--[1]|--|--|  
  
 [1] ' ist in diesem Zustand befindet werden die für die Anwendung verfügbar nur Deskriptoren Deskriptoren explizit zugeordnet.  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSources und SQLDrivers  
  
|C0<br /><br /> Keine Env.|C1<br /><br /> Nicht zugeordnet|C2<br /><br /> Belegt|C3<br /><br /> Daten erforderlich|C4<br /><br /> Verbunden|C5<br /><br /> -Anweisung.|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(SODASS)|--|--|--|--|--|--|  
  
## <a name="sqldisconnect"></a>SQLDisconnect  
  
|C0<br /><br /> Keine Env.|C1<br /><br /> Nicht zugeordnet|C2<br /><br /> Belegt|C3<br /><br /> Daten erforderlich|C4<br /><br /> Verbunden|C5<br /><br /> -Anweisung.|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(SODASS)|(SODASS)|(08003)|C2|C2|C2|25000|  
  
## <a name="sqldriverconnect"></a>SQLDriverConnect  
  
|C0<br /><br /> Keine Env.|C1<br /><br /> Nicht zugeordnet|C2<br /><br /> Belegt|C3<br /><br /> Daten erforderlich|C4<br /><br /> Verbunden|C5<br /><br /> -Anweisung.|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(SODASS)|(SODASS)|C4 s – n [f#]|(08002)|(08002)|(08002)|(08002)|  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|C0<br /><br /> Keine Env.|C1<br /><br /> Nicht zugeordnet|C2<br /><br /> Belegt|C3<br /><br /> Daten erforderlich|C4<br /><br /> Verbunden|C5<br /><br /> -Anweisung.|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(SODASS) [1]|--[3]|--[3]|--[3]|--|--|--[4] oder ([5], [6] und [8]) C4 [5] und [7] C5 [5], [6] und [9]|  
|(SODASS) [2]|(SODASS)|(08003)|(08003)|--|--|C5|  
  
 [1] für diese Zeile zeigt die Übergänge beim *HandleType* SQL_HANDLE_ENV wurde.  
  
 [2] für diese Zeile zeigt die Übergänge beim *HandleType* SQL_HANDLE_DBC wurde.  
  
 [3]. da die Verbindung nicht verbunden ist, ist es nicht von der Transaktion betroffen.  
  
 [4] das Commit oder Rollback ist für die Verbindung fehlgeschlagen. In diesem Fall gibt die Funktion SQL_ERROR zurück.  
  
 [5] für den Commit- oder Rollbackvorgang war erfolgreich für die Verbindung. Die Funktion gibt SQL_ERROR zurück, wenn die Commit- oder Rollback, die über eine andere Verbindung fehlgeschlagen ist oder die Funktion gibt SQL_SUCCESS zurück, wenn der Commit oder Rollback für alle Verbindungen erfolgreich war.  
  
 [6] Es wurde mindestens eine Anweisung, die für die Verbindung zugewiesen.  
  
 [7] gab es keine Anweisungen für die Verbindung zugewiesen.  
  
 [8] die Verbindung wurde mindestens eine Anweisung für die es wurde von einem geöffneten Cursor und die Datenquelle behält Cursor, wenn ein Commit oder ein Rollback für Transaktionen ausgeführt werden, welcher Vorgang angewendet wird (je nachdem, ob *' CompletionType '* SQL_ wurde Commit- oder SQL_ROLLBACK). Weitere Informationen finden Sie unter der Attribute SQL_CURSOR_COMMIT_BEHAVIOR und SQL_CURSOR_ROLLBACK_BEHAVIOR [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md).  
  
 [9] wäre die Verbindung alle Anweisungen für die geöffnete Cursor vorhanden waren, wurden die Cursor beim Commit oder Rollback der Transaktion nicht beibehalten.  
  
## <a name="sqlexecdirect-and-sqlexecute"></a>SQLExecDirect und SQLExecute  
  
|C0<br /><br /> Keine Env.|C1<br /><br /> Nicht zugeordnet|C2<br /><br /> Belegt|C3<br /><br /> Daten erforderlich|C4<br /><br /> Verbunden|C5<br /><br /> -Anweisung.|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(SODASS)|(SODASS)|(SODASS)|(SODASS)|(SODASS)|--C6 [1] C6 [2] [3]|--|  
  
 [1]. die Verbindung im Autocommit Modus, und die ausgeführte Anweisung nicht wurde eine *Cursor* *Spezifikation* (z. B. eine SELECT-Anweisung) oder die Verbindung wurde im Manualcommit-Modus, und die Anweisung Ausführung eine Transaktion konnte nicht begonnen.  
  
 [2]. die Verbindung im Autocommit Modus und die ausgeführte Anweisung wurde eine *Cursor* *Spezifikation* (z. B. eine SELECT-Anweisung).  
  
 [3]. die Verbindung wurde im Manualcommit Modus, und die Datenquelle begonnen wurde, eine Transaktion.  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|C0<br /><br /> Keine Env.|C1<br /><br /> Nicht zugeordnet|C2<br /><br /> Belegt|C3<br /><br /> Daten erforderlich|C4<br /><br /> Verbunden|C5<br /><br /> -Anweisung.|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(SODASS) [1]|C0|(HY010)|(HY010)|(HY010)|(HY010)|(HY010)|  
|(SODASS) [2]|(SODASS)|(C1)|(HY010)|(HY010)|(HY010)|(HY010)|  
|(SODASS) [3]|(SODASS)|(SODASS)|(SODASS)|(SODASS)|C4 [5] [6]|--[7] C4 [5] und [8] C5 [6] und [8]|  
|(SODASS) [4]|(SODASS)|(SODASS)|(SODASS)|--|--|--|  
  
 [1] für diese Zeile zeigt die Übergänge beim *HandleType* SQL_HANDLE_ENV wurde.  
  
 [2] für diese Zeile zeigt die Übergänge beim *HandleType* SQL_HANDLE_DBC wurde.  
  
 [3] für diese Zeile zeigt die Übergänge beim *HandleType* SQL_HANDLE_STMT wurde.  
  
 [4] für diese Zeile zeigt die Übergänge beim *HandleType* SQL_HANDLE_DESC wurde.  
  
 [5] gab es nur eine Anweisung, die für die Verbindung zugewiesen.  
  
 [6] gab es mehrere Anweisungen, die für die Verbindung zugewiesen.  
  
 [7] die Verbindung wurde im Manualcommit Modus.  
  
 [8] die Verbindung wurde im Autocommit Modus.  
  
## <a name="sqlfreestmt"></a>'SQLFreeStmt'  
  
|C0<br /><br /> Keine Env.|C1<br /><br /> Nicht zugeordnet|C2<br /><br /> Belegt|C3<br /><br /> Daten erforderlich|C4<br /><br /> Verbunden|C5<br /><br /> -Anweisung.|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(SODASS) [1]|(SODASS)|(SODASS)|(SODASS)|(SODASS)|--|C5 [3]: [4]|  
|(SODASS) [2]|(SODASS)|(SODASS)|(SODASS)|(SODASS)|--|--|  
  
 [1] für diese Zeile zeigt Transaktionen bei der *Option* Argument ist SQL_CLOSE.  
  
 [2] für diese Zeile zeigt Transaktionen bei der *Option* Argument ist SQL_UNBIND oder SQL_RESET_PARAMS.  
  
 [3] für die Verbindung im Autocommit Modus wurde und keine Cursor geöffnet, auf die Anweisungen, mit Ausnahme des vorliegenden waren.  
  
 [4] für die Verbindung wurde im Manualcommit-Modus oder im Autocommit Modus war und ein Cursor auf mindestens eine andere Anweisung geöffnet wurde.  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
  
|C0<br /><br /> Keine Env.|C1<br /><br /> Nicht zugeordnet|C2<br /><br /> Belegt|C3<br /><br /> Daten erforderlich|C4<br /><br /> Verbunden|C5<br /><br /> -Anweisung.|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|SODASS|SODASS|--[1] 08003[2]|HY010|--|--|--|  
  
 [1] der *Attribut* Argument war SQL_ATTR_ACCESS_MODE, SQL_ATTR_AUTOCOMMIT, SQL_ATTR_LOGIN_TIMEOUT, SQL_ATTR_ODBC_CURSORS, SQL_ATTR_TRACE oder SQL_ATTR_TRACEFILE oder ein Wert für das Verbindungsattribut festgelegt wurde.  
  
 [2] der *Attribut* Argument war kein SQL_ATTR_ACCESS_MODE, SQL_ATTR_AUTOCOMMIT, SQL_ATTR_LOGIN_TIMEOUT, SQL_ATTR_ODBC_CURSORS, SQL_ATTR_TRACE oder SQL_ATTR_TRACEFILE und ein Wert für die Verbindung wurde nicht festgelegt Das Attribut.  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagField und SQLGetDiagRec  
  
|C0<br /><br /> Keine Env.|C1<br /><br /> Nicht zugeordnet|C2<br /><br /> Belegt|C3<br /><br /> Daten erforderlich|C4<br /><br /> Verbunden|C5<br /><br /> -Anweisung.|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(SODASS) [1]|--|--|--|--|--|--|  
|(SODASS) [2]|(SODASS)|--|--|--|--|--|  
|(SODASS) [3]|(SODASS)|(SODASS)|(SODASS)|(SODASS)|--|--|  
|(SODASS) [4]|(SODASS)|(SODASS)|(SODASS)|--|--|--|  
  
 [1] für diese Zeile zeigt die Übergänge beim *HandleType* SQL_HANDLE_ENV wurde.  
  
 [2] für diese Zeile zeigt die Übergänge beim *HandleType* SQL_HANDLE_DBC wurde.  
  
 [3] für diese Zeile zeigt die Übergänge beim *HandleType* SQL_HANDLE_STMT wurde.  
  
 [4] für diese Zeile zeigt die Übergänge beim *HandleType* SQL_HANDLE_DESC wurde.  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr  
  
|C0<br /><br /> Keine Env.|C1<br /><br /> Nicht zugeordnet|C2<br /><br /> Belegt|C3<br /><br /> Daten erforderlich|C4<br /><br /> Verbunden|C5<br /><br /> -Anweisung.|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|SODASS|--|--|--|--|--|--|  
  
## <a name="sqlgetfunctions"></a>SQLGetFunctions  
  
|C0<br /><br /> Keine Env.|C1<br /><br /> Nicht zugeordnet|C2<br /><br /> Belegt|C3<br /><br /> Daten erforderlich|C4<br /><br /> Verbunden|C5<br /><br /> -Anweisung.|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|SODASS|SODASS|HY010|HY010|--|--|--|  
  
## <a name="sqlgetinfo"></a>SQLGetInfo  
  
|C0<br /><br /> Keine Env.|C1<br /><br /> Nicht zugeordnet|C2<br /><br /> Belegt|C3<br /><br /> Daten erforderlich|C4<br /><br /> Verbunden|C5<br /><br /> -Anweisung.|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|SODASS|SODASS|--[1] 08003[2]|08003|--|--|--|  
  
 [1] der *Infotyp* Argument war SQL_ODBC_VER.  
  
 [2] der *Infotyp* Argument war kein SQL_ODBC_VER.  
  
## <a name="sqlmoreresults"></a>SQLMoreResults  
  
|C0<br /><br /> Keine Env.|C1<br /><br /> Nicht zugeordnet|C2<br /><br /> Belegt|C3<br /><br /> Daten erforderlich|C4<br /><br /> Verbunden|C5<br /><br /> -Anweisung.|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(SODASS)|(SODASS)|(SODASS)|(SODASS)|(SODASS)|--[1] C6 [2]|--C5 [3] [1]|  
  
 [1]. die Verbindung wurde im Autocommit-Modus und der Aufruf von **SQLMoreResults** die Verarbeitung eines Resultsets einer Spezifikation Cursor wurde nicht initialisiert.  
  
 [2]. die Verbindung wurde im Autocommit-Modus und der Aufruf von **SQLMoreResults** die Verarbeitung eines Resultsets einer Spezifikation Cursor wurde initialisiert.  
  
 [3]. die Verbindung wurde im Manualcommit Modus.  
  
## <a name="sqlnativesql"></a>SQLNativeSql  
  
|C0<br /><br /> Keine Env.|C1<br /><br /> Nicht zugeordnet|C2<br /><br /> Belegt|C3<br /><br /> Daten erforderlich|C4<br /><br /> Verbunden|C5<br /><br /> -Anweisung.|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(SODASS)|(SODASS)|(08003)|(08003)|--|--|--|  
  
## <a name="sqlprepare"></a>SQLPrepare  
  
|C0<br /><br /> Keine Env.|C1<br /><br /> Nicht zugeordnet|C2<br /><br /> Belegt|C3<br /><br /> Daten erforderlich|C4<br /><br /> Verbunden|C5<br /><br /> -Anweisung.|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(SODASS)|(SODASS)|(SODASS)|(SODASS)|(SODASS)|--[1] C6 [2]|--|  
  
 [1]. die Verbindung im Autocommit Modus wurde, oder die Datenquelle eine Transaktion nicht beginnen.  
  
 [2]. die Verbindung wurde im Manualcommit-Modus, und die Datenquelle begonnen wurde, eine Transaktion.  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
  
|C0<br /><br /> Keine Env.|C1<br /><br /> Nicht zugeordnet|C2<br /><br /> Belegt|C3<br /><br /> Daten erforderlich|C4<br /><br /> Verbunden|C5<br /><br /> -Anweisung.|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|SODASS|SODASS|--[1] 08003[2]|HY010|--[3] 08002 [4] HY011 [5]|--[3] 08002 [4] HY011 [5]|--[3] und [6] C5 [8] [4] HY011-08002 [5] oder [7]|  
  
 [1] der *Attribut* Argument war kein SQL_ATTR_TRANSLATE_LIB oder SQL_ATTR_TRANSLATE_OPTION.  
  
 [2] der *Attribut* Argument war SQL_ATTR_TRANSLATE_LIB oder SQL_ATTR_TRANSLATE_OPTION.  
  
 [3] der *Attribut* Argument war kein SQL_ATTR_ODBC_CURSORS oder SQL_ATTR_PACKET_SIZE.  
  
 [4] der *Attribut* Argument war SQL_ATTR_ODBC_CURSORS.  
  
 [5] der *Attribut* Argument war SQL_ATTR_PACKET_SIZE.  
  
 [6] der *Attribut* Argument war kein SQL_ATTR_AUTOCOMMIT, oder die *Attribut* Argument war SQL_ATTR_AUTOCOMMIT und das Festlegen dieses Attributs keinen Commit für die Transaktion.  
  
 [7] der *Attribut* Argument war SQL_ATTR_TXN_ISOLATION.  
  
 [8] der *Attribut* Argument war SQL_ATTR_AUTOCOMMIT und das Festlegen dieses Attributs Commit der Transaktions.  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|C0<br /><br /> Keine Env.|C1<br /><br /> Nicht zugeordnet|C2<br /><br /> Belegt|C3<br /><br /> Daten erforderlich|C4<br /><br /> Verbunden|C5<br /><br /> -Anweisung.|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(SODASS)|--|--|(HY010)|--|--|--|  
  
## <a name="all-other-odbc-functions"></a>Alle anderen ODBC-Funktionen  
  
|C0<br /><br /> Keine Env.|C1<br /><br /> Nicht zugeordnet|C2<br /><br /> Belegt|C3<br /><br /> Daten erforderlich|C4<br /><br /> Verbunden|C5<br /><br /> -Anweisung.|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(SODASS)|(SODASS)|(SODASS)|(SODASS)|(SODASS)|--|--|


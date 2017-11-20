---
title: Schreiben von ODBC 3.x-Treiber | Microsoft Docs
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
helpviewer_keywords:
- upgrading drivers [ODBC]
- ODBC drivers [ODBC], upgrading
- backward compatibility [ODBC], drivers
- compatibility [ODBC], drivers
ms.assetid: 9b75f59b-623f-4711-9ca2-e751b3622e00
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 41ca6ddf1535899ed8e5e0f065cf2f5f0ca19dca
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="writing-odbc-3x-drivers"></a>Schreiben von ODBC 3.x-Treiber
Die folgende Tabelle zeigt die funktionsunterstützung in einer ODBC-3. *x* Treiber und eine ODBC-Anwendung und die Zuordnung, die vom Treiber-Manager ausgeführt, wenn die Funktionen für eine ODBC 3. aufgerufen werden. *X* Treiber.  
  
|Funktion|Unterstützt<br /><br /> durch eine<br /><br /> ODBC-3. *x*<br /><br /> Treiber?|Unterstützt<br /><br /> durch eine<br /><br /> ODBC-3. *x*<br /><br /> Anwendung?|Zugeordnet/unterstützt<br /><br /> durch die ODBC-3. *x*<br /><br /> Treiber-Manager<br /><br /> eine ODBC-3. *x* Treiber?|  
|--------------|----------------------------------------------------|---------------------------------------------------------|---------------------------------------------------------------------------------------------|  
|**SQLAllocConnect**|Nein|Keine [1]|ja|  
|**SQLAllocEnv**|Nein|Keine [1]|ja|  
|**SQLAllocHandle**|ja|ja|Nein|  
|**SQLAllocStmt:**|Nein|Keine [1]|ja|  
|**SQLBindCol**|ja|ja|Nein|  
|**SQLBindParam**|Nein|Ja [2]|ja|  
|**SQLBindParameter**|ja|ja|Nein|  
|**SQLBrowseConnect**|ja|ja|Nein|  
|**SQLBulkOperations**|ja|ja|Nein|  
|**SQLCancel**|ja|ja|Nein|  
|**SQLCloseCursor**|ja|ja|Nein|  
|**SQLColAttribute**|ja|ja|Nein|  
|**SQLColAttributes**|Keine [3]|Nein|ja|  
|**SQLColumnPrivileges**|ja|ja|Nein|  
|**SQLColumns**|ja|ja|Nein|  
|**SQLConnect**|ja|ja|Nein|  
|**SQLCopyDesc**|ja|ja|Ja [4]|  
|**SQLDataSources**|Nein|Ja|ja|  
|**SQLDescribeCol**|ja|ja|Nein|  
|**SQLDescribeParam**|ja|ja|Nein|  
|**SQLDisconnect**|ja|ja|Nein|  
|**SQLDriverConnect**|ja|ja|Nein|  
|**SQLDrivers**|Nein|Ja|ja|  
|**SQLEndTran**|ja|ja|Nein|  
|**SQLError**|Nein|Keine [1]|ja|  
|**SQLExecDirect**|ja|ja|Nein|  
|**SQLExecute**|ja|ja|Nein|  
|**SQLExtendedFetch**|ja|Nein|Nein|  
|**SQLFetch**|ja|ja|Nein|  
|**SQLFetchScroll**|ja|ja|Nein|  
|**SQLForeignKeys**|ja|ja|Nein|  
|**SQLFreeConnect**|Nein|Ja [1]|ja|  
|**SQLFreeEnv**|Nein|Ja [1]|ja|  
|**SQLFreeHandle**|ja|ja|Nein|  
|**SQLFreeStmt**|ja|ja|Nein|  
|**SQLGetConnectAttr**|ja|ja|Nein|  
|**SQLGetConnectOption**|Keine [5]|Keine [1]|ja|  
|**SQLGetCursorName**|ja|ja|Nein|  
|**SQLGetData**|ja|ja|Nein|  
|**SQLGetDescField**|ja|ja|Nein|  
|**SQLGetDescRec**|ja|ja|Nein|  
|**SQLGetDiagField**|ja|ja|Nein|  
|**SQLGetDiagRec**|ja|ja|Nein|  
|**SQLGetEnvAttr**|ja|ja|Nein|  
|**SQLGetFunctions**|Keine [6]|ja|ja|  
|**SQLGetInfo**|ja|ja|Nein|  
|**SQLGetStmtAttr**|ja|ja|Nein|  
|**SQLGetStmtOption**|Keine [5]|Keine [1]|ja|  
|**SQLGetTypeInfo**|ja|ja|Nein|  
|**SQLMoreResults**|ja|ja|Nein|  
|**SQLNativeSql**|ja|ja|Nein|  
|**SQLNumParams**|ja|ja|Nein|  
|**SQLNumResultCols**|ja|ja|Nein|  
|**SQLParamData**|ja|ja|Nein|  
|**SQLParamOptions**|Nein|Nein|ja|  
|**SQLPrepare**|ja|ja|Nein|  
|**SQLPrimaryKeys**|ja|ja|Nein|  
|**SQLProcedureColumns**|ja|ja|Nein|  
|**SQLProcedures**|ja|ja|Nein|  
|**SQLPutData**|ja|ja|Nein|  
|**SQLRowCount**|ja|ja|Nein|  
|**SQLSetConnectAttr**|ja|ja|Nein|  
|**SQLSetConnectOption**|Keine [5]|Keine [1]|ja|  
|**SQLSetCursorName**|ja|ja|Nein|  
|**SQLSetDescField**|ja|ja|Nein|  
|**SQLSetDescRec**|ja|ja|Nein|  
|**SQLSetEnvAttr**|ja|ja|Nein|  
|**SQLSetPos**|ja|ja|Nein|  
|**SQLSetParam**|Nein|Nein|ja|  
|**SQLSetScrollOption**|ja|ja|Nein|  
|**SQLSetStmtAttr**|ja|ja|Nein|  
|**SQLSetStmtOption**|Keine [5]|Keine [1]|ja|  
|**SQLSpecialColumns**|ja|ja|Nein|  
|**SQLStatistics**|ja|ja|Nein|  
|**SQLTablePrivileges**|ja|ja|Nein|  
|**SQLTables**|ja|ja|Nein|  
|**SQLTransact**|Nein|Keine [1]|ja|  
  
 [1] für diese Funktion ist in ODBC 3. veraltet. *x*. ODBC-3. *x* Anwendungen sollten diese Funktion nicht verwenden. Allerdings kann ein Open Group oder eine ISO-CLI-kompatible Anwendung diese Funktion aufrufen.  
  
 [2]-ODBC-3. *x* Anwendungen die zu verwendende **SQLBindParameter** anstelle von **SQLBindParam**. Allerdings kann ein Open Group oder eine ISO-CLI-kompatible Anwendung diese Funktion aufrufen.  
  
 [3]-Treiber Writer sollten beachten Sie, dass die ODBC-2. *x* SQL_COLUMN_PRECISION SQL_COLUMN_SCALE und SQL_COLUMN_LENGTH mit unterstützt werden müssen Spaltenattribute **SQLColAttribute**.  
  
 [4] **SQLCopyDesc** vom Treiber-Manager wird teilweise implementiert werden, wenn ein Deskriptor, der über Verbindungen kopiert wird, die zu verschiedenen Treiber gehören. Treiber müssen unterstützen **SQLCopyDesc** über zwei eigene Verbindungen. Funktionen wie **SQLDrivers**, die ausschließlich vom Treiber-Manager implementiert sind, werden in dieser Liste nicht angezeigt.  
  
 [5] unter bestimmten Umständen möglicherweise Treiber zur Unterstützung dieser Funktion. Weitere Informationen finden Sie unter dieser Funktion-Referenzseite.  
  
 [6] den Treiber zur Unterstützung auswählen kann **SQLGetFunctions** Wenn der Satz von Funktionen, die der Treiber unterstützt die Verbindung zu Verbindung variiert.


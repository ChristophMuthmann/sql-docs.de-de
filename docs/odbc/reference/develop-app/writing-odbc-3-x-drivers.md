---
title: Schreiben von ODBC 3.x-Treiber | Microsoft Docs
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
helpviewer_keywords:
- upgrading drivers [ODBC]
- ODBC drivers [ODBC], upgrading
- backward compatibility [ODBC], drivers
- compatibility [ODBC], drivers
ms.assetid: 9b75f59b-623f-4711-9ca2-e751b3622e00
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b73a32d607bb2fc2c1cd2392ab4d1b436e7ed94d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="writing-odbc-3x-drivers"></a>Schreiben von ODBC 3.x-Treiber
Die folgende Tabelle zeigt die funktionsunterstützung in einer ODBC-3. *x* Treiber und eine ODBC-Anwendung und die Zuordnung, die vom Treiber-Manager ausgeführt, wenn die Funktionen für eine ODBC 3. aufgerufen werden. *X* Treiber.  
  
|Funktion|Supported<br /><br /> durch eine<br /><br /> ODBC-3. *x*<br /><br /> Treiber?|Supported<br /><br /> durch eine<br /><br /> ODBC-3. *x*<br /><br /> Anwendung?|Zugeordnet/unterstützt<br /><br /> durch die ODBC-3. *x*<br /><br /> Treiber-Manager<br /><br /> eine ODBC-3. *x* Treiber?|  
|--------------|----------------------------------------------------|---------------------------------------------------------|---------------------------------------------------------------------------------------------|  
|**SQLAllocConnect**|nein|Keine [1]|ja|  
|**SQLAllocEnv**|nein|Keine [1]|ja|  
|**SQLAllocHandle**|ja|ja|nein|  
|**SQLAllocStmt:**|nein|Keine [1]|ja|  
|**SQLBindCol**|ja|ja|nein|  
|**SQLBindParam**|nein|Ja [2]|ja|  
|**SQLBindParameter**|ja|ja|nein|  
|**SQLBrowseConnect**|ja|ja|nein|  
|**SQLBulkOperations**|ja|ja|nein|  
|**SQLCancel**|ja|ja|nein|  
|**SQLCloseCursor**|ja|ja|nein|  
|**SQLColAttribute**|ja|ja|nein|  
|**SQLColAttributes**|Keine [3]|nein|ja|  
|**SQLColumnPrivileges**|ja|ja|nein|  
|**SQLColumns**|ja|ja|nein|  
|**SQLConnect**|ja|ja|nein|  
|**SQLCopyDesc**|ja|ja|Ja [4]|  
|**SQLDataSources**|nein|ja|ja|  
|**SQLDescribeCol**|ja|ja|nein|  
|**SQLDescribeParam**|ja|ja|nein|  
|**SQLDisconnect**|ja|ja|nein|  
|**SQLDriverConnect**|ja|ja|nein|  
|**SQLDrivers**|nein|ja|ja|  
|**SQLEndTran**|ja|ja|nein|  
|**SQLError**|nein|Keine [1]|ja|  
|**SQLExecDirect**|ja|ja|nein|  
|**SQLExecute**|ja|ja|nein|  
|**SQLExtendedFetch**|ja|nein|nein|  
|**SQLFetch**|ja|ja|nein|  
|**SQLFetchScroll**|ja|ja|nein|  
|**SQLForeignKeys**|ja|ja|nein|  
|**SQLFreeConnect**|nein|Ja [1]|ja|  
|**SQLFreeEnv**|nein|Ja [1]|ja|  
|**SQLFreeHandle**|ja|ja|nein|  
|**SQLFreeStmt**|ja|ja|nein|  
|**SQLGetConnectAttr**|ja|ja|nein|  
|**SQLGetConnectOption**|Keine [5]|Keine [1]|ja|  
|**SQLGetCursorName**|ja|ja|nein|  
|**SQLGetData**|ja|ja|nein|  
|**SQLGetDescField**|ja|ja|nein|  
|**SQLGetDescRec**|ja|ja|nein|  
|**SQLGetDiagField**|ja|ja|nein|  
|**SQLGetDiagRec**|ja|ja|nein|  
|**SQLGetEnvAttr**|ja|ja|nein|  
|**SQLGetFunctions**|Keine [6]|ja|ja|  
|**SQLGetInfo**|ja|ja|nein|  
|**SQLGetStmtAttr**|ja|ja|nein|  
|**SQLGetStmtOption**|Keine [5]|Keine [1]|ja|  
|**SQLGetTypeInfo**|ja|ja|nein|  
|**SQLMoreResults**|ja|ja|nein|  
|**SQLNativeSql**|ja|ja|nein|  
|**SQLNumParams**|ja|ja|nein|  
|**SQLNumResultCols**|ja|ja|nein|  
|**SQLParamData**|ja|ja|nein|  
|**SQLParamOptions**|nein|nein|ja|  
|**SQLPrepare**|ja|ja|nein|  
|**SQLPrimaryKeys**|ja|ja|nein|  
|**SQLProcedureColumns**|ja|ja|nein|  
|**SQLProcedures**|ja|ja|nein|  
|**SQLPutData**|ja|ja|nein|  
|**SQLRowCount**|ja|ja|nein|  
|**SQLSetConnectAttr**|ja|ja|nein|  
|**SQLSetConnectOption**|Keine [5]|Keine [1]|ja|  
|**SQLSetCursorName**|ja|ja|nein|  
|**SQLSetDescField**|ja|ja|nein|  
|**SQLSetDescRec**|ja|ja|nein|  
|**SQLSetEnvAttr**|ja|ja|nein|  
|**SQLSetPos**|ja|ja|nein|  
|**SQLSetParam**|nein|nein|ja|  
|**SQLSetScrollOption**|ja|ja|nein|  
|**SQLSetStmtAttr**|ja|ja|nein|  
|**SQLSetStmtOption**|Keine [5]|Keine [1]|ja|  
|**SQLSpecialColumns**|ja|ja|nein|  
|**SQLStatistics**|ja|ja|nein|  
|**SQLTablePrivileges**|ja|ja|nein|  
|**SQLTables**|ja|ja|nein|  
|**SQLTransact**|nein|Keine [1]|ja|  
  
 [1] für diese Funktion ist in ODBC 3. veraltet. *x*. ODBC-3. *x* Anwendungen sollten diese Funktion nicht verwenden. Allerdings kann ein Open Group oder eine ISO-CLI-kompatible Anwendung diese Funktion aufrufen.  
  
 [2]-ODBC-3. *x* Anwendungen die zu verwendende **SQLBindParameter** anstelle von **SQLBindParam**. Allerdings kann ein Open Group oder eine ISO-CLI-kompatible Anwendung diese Funktion aufrufen.  
  
 [3]-Treiber Writer sollten beachten Sie, dass die ODBC-2. *x* SQL_COLUMN_PRECISION SQL_COLUMN_SCALE und SQL_COLUMN_LENGTH mit unterstützt werden müssen Spaltenattribute **SQLColAttribute**.  
  
 [4] **SQLCopyDesc** vom Treiber-Manager wird teilweise implementiert werden, wenn ein Deskriptor, der über Verbindungen kopiert wird, die zu verschiedenen Treiber gehören. Treiber müssen unterstützen **SQLCopyDesc** über zwei eigene Verbindungen. Funktionen wie **SQLDrivers**, die ausschließlich vom Treiber-Manager implementiert sind, werden in dieser Liste nicht angezeigt.  
  
 [5] unter bestimmten Umständen möglicherweise Treiber zur Unterstützung dieser Funktion. Weitere Informationen finden Sie unter dieser Funktion-Referenzseite.  
  
 [6] den Treiber zur Unterstützung auswählen kann **SQLGetFunctions** Wenn der Satz von Funktionen, die der Treiber unterstützt die Verbindung zu Verbindung variiert.

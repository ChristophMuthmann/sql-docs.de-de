---
title: ODBC-Funktionen und die Cursorbibliothek | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c609d0fb-787a-4b39-9673-332d411b3d63
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5fe29e8cd03ded1ee2125d2729ede4c66f196838
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="odbc-functions-and-the-cursor-library"></a>ODBC-Funktionen und die Cursorbibliothek
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen und Planen von Anwendungen zu ändern, die dieses Feature verwenden. Microsoft empfiehlt die Verwendung der Cursorfunktionalität der Treiber.  
  
 Wenn die ODBC-Cursorbibliothek für eine Verbindung aktiviert ist, ruft der Treiber-Manager die Funktionen in die Cursorbibliothek statt im Treiber. Die Cursorbibliothek die Funktion ausgeführt, oder ruft es im angegebenen Treiber.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [ODBC-Funktionen, die von der Cursorbibliothek ausgeführt](../../../odbc/reference/appendixes/odbc-functions-executed-by-the-cursor-library.md)  
  
-   [ODBC-Funktionen, die von der Cursorbibliothek nicht ausgeführt werden](../../../odbc/reference/appendixes/odbc-functions-not-executed-by-the-cursor-library.md)  
  
-   [SQLBindCol (Cursor Library) (SQLBindCol (Cursorbibliothek))](../../../odbc/reference/appendixes/sqlbindcol-cursor-library.md)  
  
-   [SQLBindParameter (Cursor Library) (SQLBindParameter (Cursorbibliothek))](../../../odbc/reference/appendixes/sqlbindparameter-cursor-library.md)  
  
-   [SQLBulkOperations (Cursor Library)](../../../odbc/reference/appendixes/sqlbulkoperations-and-the-cursor-library.md)  
  
-   [SQLCloseCursor (Cursor Library)](../../../odbc/reference/appendixes/sqlclosecursor-odbc.md)  
  
-   [SQLEndTran (Cursor Library) (SQLEndTran (Cursorbibliothek))](../../../odbc/reference/appendixes/sqlendtran-cursor-library.md)  
  
-   [SQLExtendedFetch (Cursor Library) (SQLExtendedFetch (Cursorbibliothek))](../../../odbc/reference/appendixes/sqlextendedfetch-cursor-library.md)  
  
-   [SQLFetch (Cursor Library) (SQLFetch (Cursorbibliothek))](../../../odbc/reference/appendixes/sqlfetch-cursor-library.md)  
  
-   [SQLFetchScroll (Cursor Library) (SQLFetchScroll (Cursorbibliothek))](../../../odbc/reference/appendixes/sqlfetchscroll-cursor-library.md)  
  
-   [SQLFreeStmt (Cursor Library) (SQLFreeStmt (Cursorbibliothek))](../../../odbc/reference/appendixes/sqlfreestmt-cursor-library.md)  
  
-   [SQLGetData (Cursor Library) (SQLGetData (Cursorbibliothek))](../../../odbc/reference/appendixes/sqlgetdata-cursor-library.md)  
  
-   [SQLGetDescField und SQLGetDescRec (Cursorbibliothek)](../../../odbc/reference/appendixes/sqlgetdescfield-and-sqlgetdescrec-cursor-library.md)  
  
-   [SQLGetFunctions (Cursor Library) (SQLGetFunctions (Cursorbibliothek))](../../../odbc/reference/appendixes/sqlgetfunctions-cursor-library.md)  
  
-   [SQLGetInfo (Cursor Library) (SQLGetInfo (Cursorbibliothek))](../../../odbc/reference/appendixes/sqlgetinfo-cursor-library.md)  
  
-   [SQLGetStmtAttr (Cursor Library) (SQLGetStmtAttr (Cursorbibliothek))](../../../odbc/reference/appendixes/sqlgetstmtattr-cursor-library.md)  
  
-   [SQLGetStmtOption (Cursor Library) (SQLGetStmtOption (Cursorbibliothek))](../../../odbc/reference/appendixes/sqlgetstmtoption-cursor-library.md)  
  
-   [SQLNativeSql (Cursor Library) (SQLNativeSql (Cursorbibliothek))](../../../odbc/reference/appendixes/sqlnativesql-cursor-library.md)  
  
-   [SQLRowCount (Cursor Library) (SQLRowCount (Cursorbibliothek))](../../../odbc/reference/appendixes/sqlrowcount-cursor-library.md)  
  
-   [SQLSetConnectAttr (Cursor Library) (SQLSetConnectAttr (Cursorbibliothek))](../../../odbc/reference/appendixes/sqlsetconnectattr-cursor-library.md)  
  
-   [SQLSetDescField und SQLSetDescRec (Cursorbibliothek)](../../../odbc/reference/appendixes/sqlsetdescfield-and-sqlsetdescrec-cursor-library.md)  
  
-   [SQLSetEnvAttr (Cursor Library)](../../../odbc/reference/appendixes/sqlsetenvattr-and-the-cursor-library.md)  
  
-   [SQLSetPos (Cursor Library) (SQLSetPos (Cursorbibliothek))](../../../odbc/reference/appendixes/sqlsetpos-cursor-library.md)  
  
-   [SQLSetScrollOptions (Cursor Library) (SQLSetScrollOptions (Cursorbibliothek))](../../../odbc/reference/appendixes/sqlsetscrolloptions-cursor-library.md)  
  
-   [SQLSetStmtAttr (Cursor Library) (SQLSetStmtAttr (Cursorbibliothek))](../../../odbc/reference/appendixes/sqlsetstmtattr-cursor-library.md)

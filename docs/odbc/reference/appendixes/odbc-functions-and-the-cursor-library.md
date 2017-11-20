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
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c609d0fb-787a-4b39-9673-332d411b3d63
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6405c2a0890b9a5b43c420960f1b823b39ad9e60
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="odbc-functions-and-the-cursor-library"></a>ODBC-Funktionen und die Cursorbibliothek
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen und Planen von Anwendungen zu ändern, die dieses Feature verwenden. Microsoft empfiehlt die Verwendung der Cursorfunktionalität der Treiber.  
  
 Wenn die ODBC-Cursorbibliothek für eine Verbindung aktiviert ist, ruft der Treiber-Manager die Funktionen in die Cursorbibliothek statt im Treiber. Die Cursorbibliothek die Funktion ausgeführt, oder ruft es im angegebenen Treiber.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [ODBC-Funktionen, die von der Cursorbibliothek ausgeführt](../../../odbc/reference/appendixes/odbc-functions-executed-by-the-cursor-library.md)  
  
-   [ODBC-Funktionen, die von der Cursorbibliothek nicht ausgeführt.](../../../odbc/reference/appendixes/odbc-functions-not-executed-by-the-cursor-library.md)  
  
-   [SQLBindCol (Cursor Library)](../../../odbc/reference/appendixes/sqlbindcol-cursor-library.md)  
  
-   [SQLBindParameter (Cursor Library)](../../../odbc/reference/appendixes/sqlbindparameter-cursor-library.md)  
  
-   [SQLBulkOperations (Cursor Library)](../../../odbc/reference/appendixes/sqlbulkoperations-and-the-cursor-library.md)  
  
-   [SQLCloseCursor (Cursor Library)](../../../odbc/reference/appendixes/sqlclosecursor-odbc.md)  
  
-   [SQLEndTran (Cursor Library)](../../../odbc/reference/appendixes/sqlendtran-cursor-library.md)  
  
-   [SQLExtendedFetch (Cursor Library)](../../../odbc/reference/appendixes/sqlextendedfetch-cursor-library.md)  
  
-   [SQLFetch (Cursor Library)](../../../odbc/reference/appendixes/sqlfetch-cursor-library.md)  
  
-   [SQLFetchScroll (Cursor Library)](../../../odbc/reference/appendixes/sqlfetchscroll-cursor-library.md)  
  
-   [SQLFreeStmt (Cursor Library)](../../../odbc/reference/appendixes/sqlfreestmt-cursor-library.md)  
  
-   [SQLGetData (Cursor Library)](../../../odbc/reference/appendixes/sqlgetdata-cursor-library.md)  
  
-   [SQLGetDescField und SQLGetDescRec (Cursor Library)](../../../odbc/reference/appendixes/sqlgetdescfield-and-sqlgetdescrec-cursor-library.md)  
  
-   [SQLGetFunctions (Cursor Library)](../../../odbc/reference/appendixes/sqlgetfunctions-cursor-library.md)  
  
-   [SQLGetInfo (Cursor Library)](../../../odbc/reference/appendixes/sqlgetinfo-cursor-library.md)  
  
-   [SQLGetStmtAttr (Cursor Library)](../../../odbc/reference/appendixes/sqlgetstmtattr-cursor-library.md)  
  
-   [SQLGetStmtOption (Cursor Library)](../../../odbc/reference/appendixes/sqlgetstmtoption-cursor-library.md)  
  
-   [SQLNativeSql (Cursor Library)](../../../odbc/reference/appendixes/sqlnativesql-cursor-library.md)  
  
-   [SQLRowCount (Cursor Library)](../../../odbc/reference/appendixes/sqlrowcount-cursor-library.md)  
  
-   [SQLSetConnectAttr (Cursor Library)](../../../odbc/reference/appendixes/sqlsetconnectattr-cursor-library.md)  
  
-   [SQLSetDescField und SQLSetDescRec (Cursor Library)](../../../odbc/reference/appendixes/sqlsetdescfield-and-sqlsetdescrec-cursor-library.md)  
  
-   [SQLSetEnvAttr (Cursor Library)](../../../odbc/reference/appendixes/sqlsetenvattr-and-the-cursor-library.md)  
  
-   [SQLSetPos (Cursor Library)](../../../odbc/reference/appendixes/sqlsetpos-cursor-library.md)  
  
-   [SQLSetScrollOptions (Cursor Library)](../../../odbc/reference/appendixes/sqlsetscrolloptions-cursor-library.md)  
  
-   [SQLSetStmtAttr (Cursor Library)](../../../odbc/reference/appendixes/sqlsetstmtattr-cursor-library.md)


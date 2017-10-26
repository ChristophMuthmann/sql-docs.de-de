---
title: Zuordnung veraltete Funktionen | Microsoft Docs
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
- mapping deprecated functions [ODBC], about mapping deprecated functions
- backward compatibility [ODBC], mapping deprecated functions
- deprecated functions [ODBC]
- compatibility [ODBC], mapping deprecated functions
- functions [ODBC], mapping deprecated functions
- mapping deprecated functions [ODBC]
ms.assetid: ee462617-1d79-4c88-afeb-b129cff34cc6
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 61d05017039673989e1477501feb17b3da6d7220
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="mapping-deprecated-functions"></a>Zuordnung veraltete Funktionen
In diesem Abschnitt wird beschrieben, wie veraltete Funktionen zugeordnet werden, indem die ODBC 3.*.x* Treiber-Manager zum Gewährleisten der Abwärtskompatibilität von ODBC 3.*.x* Treiber, die mit ODBC-2 verwendet werden.* X* Anwendungen. Der Treiber-Manager führt diese Zuordnung unabhängig von der Version der Anwendung. Da jedes der ODBC-2. *x* Funktionen in der folgenden Liste wird die entsprechende ODBC 3. zugeordnet*.x* -Funktion bei Aufruf in einer ODBC 3.*.x* -Treiber verwenden, die ODBC 3.*.x*Treiber muss sich nicht in der ODBC 2. implementieren. *x* Funktionen.  
  
 Die Zuordnung in der Liste wird ausgelöst, wenn der Treiber eine ODBC 3.*.x* und den Treiber unterstützt nicht die Funktion, die zugeordnet wird.  
  
 Die folgende Tabelle enthält alle doppelten Funktionen, die in ODBC 3. eingeführte*.x*.  
  
|ODBC-2. *x* Funktion|ODBC 3.*.x* Funktion|  
|-------------------------|-------------------------|  
|**SQLAllocConnect**|**SQLAllocHandle**|  
|**SQLAllocEnv**|**SQLAllocHandle**|  
|**SQLAllocStmt:**|**SQLAllocHandle**|  
|**SQLBindParam**[1]|**SQLBindParameter**|  
|**SQLColAttributes**|**SQLColAttribute**|  
|**SQLError**|**SQLGetDiagRec**|  
|**SQLFreeConnect**|**SQLFreeHandle**|  
|**SQLFreeEnv**|**SQLFreeHandle**|  
|**SQLFreeStmt** mit einem *Option* von SQL_DROP|**SQLFreeHandle**|  
|**SQLGetConnectOption**|**SQLGetConnectAttr**|  
|**SQLGetStmtOption**|**SQLGetStmtAttr**|  
|**SQLParamOptions**|**SQLSetStmtAttr**|  
|**SQLSetConnectOption**|**SQLSetConnectAttr**|  
|**SQLSetParam**[2]|**SQLBindParameter**|  
|**SQLSetScrollOption**|**SQLSetStmtAttr**|  
|**SQLSetStmtOption**|**SQLSetStmtAttr**|  
|**SQLTransact**|**SQLEndTran**|  
  
 [1], obwohl diese Funktion nicht, in ODBC 2. vorhanden war*.x*, es ist in den Open Group und ISO-Standards.  
  
 [2] Dies ist ein ODBC-1.0-Funktion.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [SQLAllocConnect-Zuordnung](../../../odbc/reference/appendixes/sqlallocconnect-mapping.md)  
  
-   [SQLAllocEnv-Zuordnung](../../../odbc/reference/appendixes/sqlallocenv-mapping.md)  
  
-   [Zuordnung von SQLAllocStmt:](../../../odbc/reference/appendixes/sqlallocstmt-mapping.md)  
  
-   [SQLBindParam-Zuordnung](../../../odbc/reference/appendixes/sqlbindparam-mapping.md)  
  
-   [SQLColAttributes-Zuordnung](../../../odbc/reference/appendixes/sqlcolattributes-mapping.md)  
  
-   [SQLError-Zuordnung](../../../odbc/reference/appendixes/sqlerror-mapping.md)  
  
-   [SQLFreeConnect-Zuordnung](../../../odbc/reference/appendixes/sqlfreeconnect-mapping.md)  
  
-   [SQLFreeEnv-Zuordnung](../../../odbc/reference/appendixes/sqlfreeenv-mapping.md)  
  
-   [SQLFreeStmt-Zuordnung](../../../odbc/reference/appendixes/sqlfreestmt-mapping.md)  
  
-   [SQLGetConnectOption-Zuordnung](../../../odbc/reference/appendixes/sqlgetconnectoption-mapping.md)  
  
-   [SQLGetStmtOption-Zuordnung](../../../odbc/reference/appendixes/sqlgetstmtoption-mapping.md)  
  
-   [SQLInstallTranslator-Zuordnung](../../../odbc/reference/appendixes/sqlinstalltranslator-mapping.md)  
  
-   [SQLParamOptions-Zuordnung](../../../odbc/reference/appendixes/sqlparamoptions-mapping.md)  
  
-   [SQLSetConnectOption-Zuordnung](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md)  
  
-   [SQLSetParam-Zuordnung](../../../odbc/reference/appendixes/sqlsetparam-mapping.md)  
  
-   [SQLSetScrollOptions-Zuordnung](../../../odbc/reference/appendixes/sqlsetscrolloptions-mapping.md)  
  
-   [SQLSetStmtOption Zuordnung](../../../odbc/reference/appendixes/sqlsetstmtoption-mapping.md)  
  
-   [SQLTransact-Zuordnung](../../../odbc/reference/appendixes/sqltransact-mapping.md)


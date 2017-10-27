---
title: Funktionen, die Zeichenfolgenparameter akzeptiert | Microsoft Docs
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
- desktop database drivers [ODBC], string parameters
- ODBC desktop database drivers [ODBC], string parameters
- Jet-based ODBC drivers [ODBC], string parameters
- functions [ODBC], string parameters
- string parameters [ODBC]
ms.assetid: 869b8421-f71e-4dfd-adce-691bd3012b16
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bb438fa14f5367579d96c2640705f82589e71636
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="functions-accepting-string-parameters"></a>Funktionen, die Zeichenfolgenparameter akzeptieren
Alle Funktionen, die String-Parameter akzeptieren, werden in Unicode konvertiert werden. (Das Format "W" die Funktion wird exportiert werden.) Die Anzahl von Bytes wird konvertiert, um die Anzahl von Zeichen für die entsprechenden ODBC-APIs. Dies gilt für die folgenden Funktionen:  
  
-   **SQLConnect**  
  
-   **SQLDriverConnect**  
  
-   **SQLColAttributes**  
  
-   **SQLDescribeCol**  
  
-   **SQLError** (Fassung **SQLGetDiagField**)  
  
-   **SQLExecDirect**  
  
-   **SQLGetCursorName**  
  
-   **SQLSetCursorName**  
  
-   **SQLGetStmtAttr**  
  
-   **SQLGetInfo**  
  
-   **SQLGetStmtOption** (wird **SQLGetStmtAttr**)  
  
-   **SQLSetStmtOption** (wird **SQLSetStmtAttr**)  
  
-   **SQLGetConnectOption**  
  
-   **SQLSetConnectOption**  
  
-   **SQLGetTypeInfo**  
  
-   **SQLStatistics**  
  
-   **SQLTables**  
  
-   **SQLNativeSQL**  
  
-   **SQLSpecialColumns**  
  
-   **ConfigDSNEx**  
  
-   **ConfigDSN**


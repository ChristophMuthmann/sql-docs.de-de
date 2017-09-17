---
title: SQLGetStmtOption Zuordnung | Microsoft Docs
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
- SQLGetStmtOption function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLGetStmtOption
ms.assetid: fa599517-3f3e-4dad-a65a-b8596ae3f330
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 503af3ea0dbac61cee506b932f79eccab5dedcf8
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgetstmtoption-mapping"></a>SQLGetStmtOption-Zuordnung
Wenn eine Anwendung ruft **SQLGetStmtOption** auf eine ODBC 3.*.x* Treiber, die es den Aufruf von nicht unterstützt  
  
```  
SQLGetStmtOption(hstmt, fOption, pvParam)  
```  
  
 führt wie folgt:  
  
-   Wenn *fOption* gibt an, eine ODBC-definierten Anweisungsoption, die eine Zeichenfolge, die der Treiber-Manager ruft zurückgibt  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
-   Wenn *fOption* gibt an, eine ODBC-definierten Anweisungsoption, die einen 32-Bit-Ganzzahl-Wert, der Treiber-Manager ruft zurückgibt  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, 0, NULL)  
    ```  
  
-   Wenn *fOption* gibt eine treiberdefinierten Anweisungsoption Treibermanager-Aufrufe an  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
 In den vorhergehenden drei Fällen die *StatementHandle* Argument wird festgelegt, auf den Wert in *Befehls beschäftigt*, *Attribut* Argument wird festgelegt, auf den Wert in *fOption *, und die *ValuePtr* Argument wird festgelegt, auf den gleichen Wert wie *PvParam*.  
  
 Für ODBC definierte Zeichenfolge Verbindungsoptionen, legt der Treiber-Manager die *Pufferlänge* Argument im Aufruf **SQLGetConnectAttr** auf die vordefinierte maximale Länge (SQL_MAX_OPTION_STRING_LENGTH); für eine Verbindungsoption Objektressourcen *Pufferlänge* auf 0 festgelegt ist.  
  
 Die SQL_GET_BOOKMARK Option-Anweisung ist in ODBC 3. veraltet*.x*. Für eine ODBC 3.*.x* Treiber zum Arbeiten mit ODBC 2..* X* Anwendungen, SQL_GET_BOOKMARK, muss er SQL_GET_BOOKMARK unterstützen. Für eine ODBC 3.*.x* Treiber zum Arbeiten mit ODBC 2..* X* Anwendungen müssen entdeckt SQL_USE_BOOKMARKS auf SQL_UB_ON festlegen und sollte fester Länge Lesezeichen verfügt. Wenn eine ODBC 3.*.x* -Treiber unterstützt nur variabler Länge, Lesezeichen, Lesezeichen nicht fester Länge, sie muss SQLSTATE HYC00 zurückgeben (optionales Feature nicht implementiert) Wenn einer ODBC 2..* X* Anwendung versucht, SQL_UB_ON SQL_USE_BOOKMARKS fest.  
  
 Für eine ODBC 3.*.x* Treiber, der Treiber-Manager nicht mehr überprüft, ob *Option* zwischen SQL_STMT_OPT_MIN und SQL_STMT_OPT_MAX ist, oder SQL_CONNECT_OPT_DRVR_START größer ist. Der Treiber muss diese Option aktivieren.

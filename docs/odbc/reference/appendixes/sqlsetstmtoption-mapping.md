---
title: SQLSetStmtOption Zuordnung | Microsoft Docs
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
- mapping deprecated functions [ODBC], SQLSetStmtOption
- SQLSetStmtOption function [ODBC], mapping
ms.assetid: 6a9921aa-8a53-4668-9b13-87164062f1e5
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5759836011cdcd33687d0f623fe4947f18862b8e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="sqlsetstmtoption-mapping"></a>SQLSetStmtOption Zuordnung
Wenn eine Anwendung ruft **SQLSetStmtOption** über einen ODBC 3.*.x* Treiber, den Aufruf von  
  
```  
SQLSetStmtOption(StatementHandle, fOption, vParam)  
```  
  
 führt wie folgt:  
  
-   Wenn *fOption* gibt an, eine ODBC-definierten Anweisungsattribut, die eine Zeichenfolge, die Aufrufe der Treiber-Manager  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, SQL_NTS)  
    ```  
  
-   Wenn *fOption* gibt an, eine ODBC-definierten Anweisungsattribut, der einen 32-Bit-Ganzzahl-Wert, der Treiber-Manager ruft zurückgibt  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, 0)  
    ```  
  
-   Wenn *fOption* gibt eine treiberdefinierten Anweisungsattribut Treibermanager-Aufrufe an  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, BufferLength)  
    ```  
  
 In den vorhergehenden drei Fällen die **StatementHandle** Argument wird festgelegt, auf den Wert in *Befehls beschäftigt*, *Attribut* Argument wird festgelegt, auf den Wert in *fOption* , und die *ValuePtr* Argument wird festgelegt, auf den Wert als *vParam*.  
  
 Da der Treiber-Manager nicht weiß, ob das treiberdefinierten Anweisungsattribut 32-Bit-Ganzzahl-Wert oder eine Zeichenfolge erforderlich, wurde für die Übergabe in einen gültigen Wert für die *StringLength* Argument **SQLSetStmtAttr**. Wenn der Treiber verfügt über spezielle Semantik für treiberdefinierten Anweisungsattribute definiert und aufgerufen werden. muss **SQLSetStmtOption**, muss er unterstützen **SQLSetStmtOption**.  
  
 Wenn eine Anwendung ruft **SQLSetStmtOption** festzulegende treiberspezifische-Anweisungsoption in eine ODBC 3.*.x* Treiber und die Option wurde in einer ODBC 2. definiert. *X* Version des Treibers, eine neue manifestkonstante sollte definiert werden, für die Option in die ODBC 3.*.x* Treiber. Wenn die alten manifestkonstante, in dem Aufruf von verwendet wird **SQLSetStmtOption**, Treiber-Manager **SQLSetStmtAttr** mit der *StringLength* Argument auf 0 festgelegt.  
  
 Wenn eine Anwendung ruft **SQLSetStmtAttr** SQL_ATTR_USE_BOOKMARKS SQL_UB_ON in eine ODBC 3. festzulegende*.x* -Treiber verwenden, das SQL_ATTR_USE_BOOKMARKS-Anweisungsattribut auf SQL_UB_FIXED festgelegt ist. SQL_UB_ON ist die gleiche Konstante als SQL_UB_FIXED. Der Treiber-Manager übergibt SQL_UB_FIXED über an den Treiber. SQL_UB_FIXED ist in ODBC 3. veraltet*.x*, aber eine ODBC 3.*.x* Treiber muss diese für das Arbeiten mit ODBC 2. implementieren. *X* Anwendungen mit fester Länge Lesezeichen.  
  
 Für eine ODBC 3.*.x* Treiber, der Treiber-Manager nicht mehr überprüft, ob *Option* zwischen SQL_STMT_OPT_MIN und SQL_STMT_OPT_MAX ist, oder SQL_CONNECT_OPT_DRVR_START größer ist.

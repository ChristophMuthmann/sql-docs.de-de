---
title: Funktionsweise des Treiber-Manager | Microsoft Docs
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
- driver manager [ODBC], backward compatibility
- compatibility [ODBC], driver manager
- ODBC driver manager [ODBC]
- backward compatibility [ODBC], driver manager
ms.assetid: 57f65c38-d9ee-46c8-9051-128224a582c6
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 64c6fb04fe5c5c693da4982e1c12194bc7e42f98
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="what-the-driver-manager-does"></a>Was bewirkt, dass der Treiber-Manager
Die folgende Tabelle enthält wie die ODBC 3.*.x* Treibermanager ordnet Aufrufe an ODBC 2..* X* und ODBC 3.*.x* Treiber.  
  
|Funktion oder<br /><br /> Anweisungsattribut|Kommentare|  
|-----------------------------------------|--------------|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|Verweist auf das Lesezeichen für die Verwendung mit **SQLFetchScroll**. Im folgenden finden Details zur Implementierung:<br /><br /> – Wenn eine Anwendung dies in einer ODBC 2. festlegt. *x* -Treiber verwenden, die ODBC 3.*.x* -Treiber-Manager zwischengespeichert. Es dereferenziert den Zeiger und übergibt den Wert für die ODBC-2. *x* Treiber in den *FetchOffset* Argument **SQLExtendedFetch** Wenn **SQLFetchScroll** später von der Anwendung aufgerufen wird.<br />– Wenn eine Anwendung wird hiermit in einer ODBC 3.*.x* -Treiber verwenden, die ODBC 3.*.x* -Treiber-Manager wird den Aufruf an den Treiber übergeben.|  
|SQL_ATTR_ROW_STATUS_PTR|Verweist auf die zeilenstatusarray von ausgefüllt **SQLFetch**, **SQLFetchScroll**, **SQLBulkOperations**, und **SQLSetPos**. Im folgenden finden Details zur Implementierung:<br /><br /> – Wenn eine Anwendung dies in einer ODBC 2. festlegt. *x* -Treiber verwenden, die ODBC 3.*.x* -Treiber-Manager speichert dessen Wert. Dieser Wert wird mit der ODBC 2. übergibt. *x* -Treibers in den *RowStatusArray* Argument **SQLExtendedFetch** Wenn **SQLFetchScroll** oder **SQLFetch** aufgerufen wird.<br />– Wenn eine Anwendung wird hiermit in einer ODBC 3.*.x* -Treiber verwenden, die ODBC 3.*.x* -Treiber-Manager wird den Aufruf an den Treiber übergeben.<br />-Im Zustand S6, wenn eine Anwendung SQL_ATTR_ROW_STATUS_PTR und dann ruft **SQLBulkOperations** (mit einer *Vorgang* von SQL_ADD) oder **SQLSetPos** erst nach Aufrufen von **SQLFetch** oder **SQLFetchScroll**, SQLSTATE HY011 (Attribut kann nicht jetzt festgelegt werden) wird zurückgegeben.|  
|SQL_ATTR_ROWS_FETCHED_PTR FEST|Verweist auf den Puffer, in dem **SQLFetch** und **SQLFetchScroll** geben die Anzahl der abgerufenen Zeilen zurück. Im folgenden finden Details zur Implementierung:<br /><br /> – Wenn eine Anwendung dies in einer ODBC 2. festlegt. *x* -Treiber verwenden, die ODBC 3.*.x* -Treiber-Manager speichert dessen Wert. Dieser Wert wird mit der ODBC 2. übergibt. *x* -Treibers in den *RowCountPtr* Argument **SQLExtendedFetch** Wenn **SQLFetch** oder **SQLFetchScroll** , die von der Anwendung aufgerufen wird.<br />– Wenn eine Anwendung wird hiermit in einer ODBC 3.*.x* -Treiber verwenden, die ODBC 3.*.x* -Treiber-Manager wird den Aufruf an den Treiber übergeben.|  
|SQL_ATTR_ROW_ARRAY_SIZE|Legt die Größe des Rowsets fest. Im folgenden finden Details zur Implementierung:<br /><br /> – Wenn eine Anwendung dies in einer ODBC 2. festlegt. *x* -Treiber verwenden, die ODBC 3.*.x* Treibermanager ordnet das Anweisungsattribut SQL_ROWSET_SIZE setzen.<br />– Wenn eine Anwendung wird hiermit in einer ODBC 3.*.x* -Treiber verwenden, die ODBC 3.*.x* -Treiber-Manager wird den Aufruf an den Treiber übergeben.<br />– Wenn Sie eine Anwendung mit dem Arbeiten mit einer ODBC 3.*.x* Treiber ruft **SQLSetScrollOptions**, SQL_ROWSET_SIZE setzen festgelegt ist, auf den Wert in der *RowsetSize* Argument Wenn des zugrunde liegenden Treiber unterstützt keine **SQLSetScrollOptions**.|  
|SQL_ROWSET_SIZE SETZEN|Legt die Rowsetgröße von verwendeten **SQLExtendedFetch** Wenn **SQLExtendedFetch** wird von einer ODBC 2. aufgerufen*.x* Anwendung. Im folgenden finden Details zur Implementierung:<br /><br /> – Wenn eine Anwendung festlegt, die ODBC 3.*.x* -Treiber-Manager übergibt den Aufruf an den Treiber, unabhängig von der Treiberversion.<br />– Wenn Sie eine Anwendung mit einer ODBC 2. arbeiten. *x* Treiber ruft **SQLSetScrollOptions**, SQL_ROWSET_SIZE setzen festgelegt ist, auf den Wert in der **RowsetSize** Argument.|  
|**SQLBulkOperations**|Führt eine Insert-Vorgang oder Update, Delete oder Fetch von Lesezeichen-Vorgängen. Im folgenden finden Details zur Implementierung:<br /><br /> – Wenn eine Anwendung ruft **SQLBulkOperations** mit einem *Vorgang* von SQL_ADD in einer ODBC 2..* X* -Treiber verwenden, die ODBC 3.*.x* Treibermanager ordnet diesen **SQLSetPos** mit einem *Vorgang* von SQL_ADD.<br />– Wenn Sie mit einer ODBC 2. arbeiten zu können. *x* Treiber, der nicht unterstützt **SQLSetPos** mit einer *Vorgang* von SQL_ADD, die ODBC 3.*.x* -Treiber-Manager nicht zugeordnet**SQLSetPos** mit einer *Vorgang* von SQL_ADD auf **SQLBulkOperations** mit einer *Vorgang* von SQL_ADD. Grund hierfür ist, **SQLBulkOperations** kann nicht im Zustand S7, welche in ODBC 2. aufgerufen werden.* X* wurde der einzige Zustand, in dem **SQLSetPos** aufgerufen werden.<br />– Wenn die Anwendung aufruft, **SQLBulkOperations** mit einem *Vorgang* von SQL_ADD in einer ODBC 2..* X* Treiber vor dem Aufruf **SQLFetchScroll**, die ODBC 3.*.x* -Treiber-Manager einen Fehler zurück.|  
|**SQLExtendedFetch**|Gibt das angegebene Rowset zurück. Mit Ausnahme der Einschränkung soeben erwähnt, die ODBC 3.*.x* -Treiber-Manager übergibt, Aufrufe von **SQLExtendedFetch** an den Treiber, unabhängig von der Version des Treibers.|  
|**SQLFetch**|Gibt das nächste Rowset zurück. Im folgenden finden Details zur Implementierung:<br /><br /> – Wenn eine Anwendung ruft **SQLFetch** in einer ODBC 2..* X* -Treiber verwenden, die ODBC 3.*.x* Treibermanager ordnet diesen **SQLExtendedFetch**. Die *FetchOrientation* Argument **SQLExtendedFetch** auf SQL_FETCH_NEXT festgelegt ist. Der Treiber-Manager verwendet den zwischengespeicherten Wert des Attributs SQL_ATTR_ROW_STATUS_PTR-Anweisung für die *RowStatusArray* -Argument und den zwischengespeicherten Wert des Attributs SQL_ATTR_ROWS_FETCHED_PTR-Anweisung für die * RowCountPtr* Argument.<br />-Eine ODBC 3.*.x* Anwendung kann Aufrufe mischen **SQLFetch** und **SQLFetchScroll** in einer ODBC 2..* X* Treiber da die ODBC 3.*.x* Treibermanager ordnet **SQLFetch** auf **SQLExtendedFetch** Wenn Sie eine Anwendung ruft Sie es in einer ODBC 2..* X* Treiber.<br />-Wenn ein ODBC-2. *x* Treiber unterstützt keine **SQLExtendedFetch**, die ODBC 3.*.x* -Treiber-Manager ist nicht zugeordnet. **SQLFetch** oder ** SQLFetchScroll** auf **SQLExtendedFetch** Wenn Sie eine Anwendung ruft Sie es in diesen Treiber. Wenn die Anwendung versucht, Sie SQL_ATTR_ROW_ARRAY_SIZE auf einen Wert festgelegt wird, der größer als 1, SQLSTATE HYC00 (optionales Feature nicht implementiert) wird zurückgegeben.<br />– Mit Ausnahme von für die Einschränkungen nur erwähnt, die ODBC 3.*.x* -Treiber-Manager übergibt, Aufrufe von **SQLFetch** an den Treiber, unabhängig von der Version des Treibers.|  
|**SQLFetchScroll**|Gibt das angegebene Rowset zurück. Im folgenden finden Details zur Implementierung:<br /><br /> – Wenn eine Anwendung ruft **SQLFetchScroll** in einer ODBC 2..* X* -Treiber verwenden, die ODBC 3.*.x* Treibermanager ordnet diesen **SQLExtendedFetch**. Er verwendet den zwischengespeicherten Wert des Attributs SQL_ATTR_ROW_STATUS_PTR-Anweisung für die *RowStatusArray* -Argument und den zwischengespeicherten Wert des Attributs SQL_ATTR_ROWS_FETCHED_PTR-Anweisung für die *RowCountPtr* Argument. Wenn die *FetchOrientation* Argument in **SQLFetchScroll** sql_fetch_bookmark auf, wird er verwendet den zwischengespeicherten Wert des Attributs SQL_ATTR_FETCH_BOOKMARK_PTR-Anweisung für die *FetchOffset * Argument und gibt einen Fehler zurück, wenn die *FetchOffset* Argument **SQLFetchScroll** ist nicht 0 ist.<br />– Wenn Sie eine Anwendung ruft Sie dies in einer ODBC 3.*.x* -Treiber verwenden, die ODBC 3.*.x* -Treiber-Manager wird den Aufruf an den Treiber übergeben.|  
|**SQLSetPos**|Führt verschiedene positionierte Operationen. Die ODBC 3.*.x* -Treiber-Manager übergibt, Aufrufe von **SQLSetPos** an den Treiber, unabhängig von der Version des Treibers.|  
|**SQLSetScrollOptions**|Wenn der Treiber-Manager ordnet **SQLSetScrollOptions** für eine Anwendung mit dem Arbeiten mit einer ODBC 3.*.x* Treiber, der nicht unterstützt **SQLSetScrollOptions**, den Treiber -Manager setzt die SQL_ROWSET_SIZE setzen-Anweisungsoption nicht das SQL_ATTR_ROW_ARRAY_SIZE-Anweisungsattribut, zu der *RowsetSize* Argument in **SQLSetScrollOption**. Folglich **SQLSetScrollOptions** kann nicht von einer Anwendung verwendet werden, wenn mehrere Zeilen durch einen Aufruf zum Abrufen von **SQLFetch** oder **SQLFetchScroll**. Kann verwendet werden, nur dann, wenn durch einen Aufruf an das Abrufen mehrerer Zeilen **SQLExtendedFetch**.|


---
title: Neue Funktionen | Microsoft Docs
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
- backward compatibility [ODBC], new features in release
- ODBC drivers [ODBC], backward compatibility
- new features [ODBC]
- compatibility [ODBC], new features in release
- ODBC [ODBC], new features
ms.assetid: a8fcdd00-6cb3-4871-9489-6018b3d0d65f
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6e2b48097b6c398772e14d2594a583d89e6825e0
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="new-features"></a>Neue Funktionen
Die folgende neue Funktionen wurde in ODBC 3. eingeführt. *x*. Eine ODBC-3. *x* Anwendung arbeiten mit einer ODBC 2.*.x* Treiber wird nicht in der Lage, diese Funktionalität verwenden. Der ODBC-3. *x* -Treiber-Manager zugeordnet ist diese Funktionen bei der Arbeit mit einer ODBC 2.*.x* Treiber.  
  
-   Funktionen, die einen Deskriptor akzeptieren zu behandeln, als Argument: **SQLSetDescField**, **SQLGetDescField**, **SQLSetDescRec**, **SQLGetDescRec**, und **SQLCopyDesc**.  
  
-   Die Funktionen **SQLSetEnvAttr** und **SQLGetEnvAttr**.  
  
-   Die Verwendung von **SQLAllocHandle** eine Deskriptorhandles zuweisen. (Die Verwendung von **SQLAllocHandle** zuweisen Umgebung, Verbindungs- und Anweisung Handles ist doppelt vorhandenen, nicht für neue Funktionen.)  
  
-   Die Verwendung von **SQLGetConnectAttr** die Verbindungsattribute SQL_ATTR_AUTO_IPD abgerufen. (Die Verwendung von **SQLSetConnectAttr** festgelegt wird, und **SQLGetConnectAttr** um erhalten, ist die weiteren Verbindungsattributen doppelt vorhandenen, nicht für neue Funktionen.)  
  
-   Die Verwendung von **SQLSetStmtAttr** festgelegt wird, und **SQLGetStmtAttr** abgerufen, die folgenden Anweisungsattribute. (Die Verwendung von **SQLSetStmtAttr** festgelegt wird, und **SQLGetStmtAttr** um erhalten, andere Anweisungsattribute duplizierten, keine neuen Funktionen ist.)  
  
     SQL_ATTR_APP_ROW_DESC  
  
     SQL_ATTR_APP_PARAM_DESC  
  
     SQL_ATTR_ENABLE_AUTO_IPD  
  
     SQL_ATTR_FETCH_BOOKMARK_PTR  
  
     SQL_ATTR_BIND_OFFSET  
  
     SQL_ATTR_METADATA_ID  
  
     SQL_ATTR_PARAM_BIND_OFFSET_PTR  
  
     SQL_ATTR_PARAM_BIND_TYPE  
  
     SQL_ATTR_PARAM_OPERATION_PTR  
  
     SQL_DESC_PARAM_STATUS_PTR  
  
     SQL_ATTR_PARAMS_PROCESSED_PTR  
  
     SQL_ATTR_PARAMSET_SIZE  
  
     SQL_ATTR_ROW_BIND_OFFSET_PTR  
  
     SQL_ATTR_ROW_OPERATION_PTR  
  
     SQL_ATTR_ROW_ARRAY_SIZE  
  
-   Die Verwendung von **SQLGetStmtAttr** um die folgenden Anweisungsattribute abzurufen. (Die Verwendung von **SQLGetStmtAttr** andere Anweisung abzurufenden Attribute duplizierte Funktionalität, keine neuen Funktionen ist.)  
  
     SQL_ATTR_IMP_ROW_DESC SQL_ATTR_IMP_PARAM_DESC  
  
-   Die Verwendung der Intervall C-Datentyp, die Intervall-SQL-Datentypen, die BIGINT-C-Datentypen und die Datenstruktur SQL_C_NUMERIC.  
  
-   Die zeilenweise Bindung von Parametern.  
  
-   Offset-basierte Lesezeichen abruft, wie ein Aufruf **SQLFetchScroll** mit einem *FetchOrientation* Argument SQL_FETCH_BOOKMARK und Angeben eines Offsets ungleich 0.  
  
-   **SQLFetch** zurückgeben zeilenstatusarray Anzahl von Zeilen abgerufen, Abrufen mehrerer Zeilen, Vermischung Aufrufe mit **SQLFetchScroll**, und Vermischung Aufrufe mit **SQLBulkOperations** oder **SQLSetPos**. Weitere Informationen finden Sie im nächsten Abschnitt [Blockcursor, scrollfähige Cursor und Abwärtskompatibilität für ODBC 3.x-Anwendungen](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md).  
  
-   Benannte Parameter.  
  
-   Alle von der ODBC-3. *x*– bestimmte **SQLGetInfo** Optionen. (Bei einer ODBC-3. *x* Anwendung arbeiten mit einer ODBC 2..* X* Treiber Ruft die SQL_XXX_CURSOR_ATTRIBUTES1 Informationstypen, bei denen mehrere ODBC 2. ersetzt haben.* X* Informationstypen, einige Informationen möglicherweise zuverlässig, aber einige möglicherweise unzuverlässig. Weitere Informationen finden Sie unter [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md).)  
  
-   Binden Sie Offsets.  
  
-   Aktualisieren, aktualisieren und Löschen von Lesezeichen (durch einen Aufruf von **SQLBulkOperations**).  
  
-   Aufrufen von **SQLBulkOperations** oder **SQLSetPos** im Status "S5".  
  
-   Die ROW_NUMBER und Zeile/relative Felder in der Diagnosedatensatz (die aufweisen, mit dem die Ersetzung-Funktionen abgerufen werden **SQLGetDiagField** oder **SQLGetDiagRec**).  
  
-   Ungefähre Zeilenanzahl.  
  
-   Warnungsinformationen (SQL_ROW_SUCCESS_WITH_INFO aus **SQLFetchScroll**).  
  
-   Lesezeichen mit variabler Länge.  
  
-   Erweiterte Fehlerinformationen für Arrays von Parametern.  
  
-   Alle neuen Spalten in den Resultsets, die durch die Katalogfunktionen zurückgegeben.  
  
-   Verwenden von **SQLDescribeCol** und **SQLColAttribute** für die Spalte 0.  
  
-   Verwendung von jeder ODBC-3. *x*– Attribute der bestimmten Spalte in einem Aufruf von **SQLColAttribute**.  
  
-   Verwendung von mehreren Umgebungshandles.  
  
 Dieser Abschnitt enthält das folgende Thema.  
  
-   [Blockcursor, scrollfähige Cursor und Abwärtskompatibilität für ODBC 3.x-Anwendungen](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)


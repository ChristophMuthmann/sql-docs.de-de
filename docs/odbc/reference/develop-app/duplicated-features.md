---
title: Dupliziert Funktionen | Microsoft Docs
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
- duplicated functions [ODBC]
- compatibility [ODBC], duplicated functions
- ODBC drivers [ODBC], backward compatibility
- functions [ODBC], duplicated functions
- backward compatibility [ODBC], duplicated functions
ms.assetid: 641b16bc-f791-46d8-b093-31736473fe3d
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 911e36882d278a997126dbf0ee99bbab837c5125
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="duplicated-features"></a>Doppelte Funktionen
Die folgenden ODBC-2. *x* wurden Funktionen von ODBC 3. verdoppelt. *X* Funktionen. Als Ergebnis der ODBC-2. *x* -Funktionen sind veraltet, in ODBC 3.. *X*. Der ODBC-3. *x* Funktionen werden als Ersatzfunktionen bezeichnet.  
  
 Wenn eine Anwendung eine als veraltet markierte ODBC 2. verwendet. *x* -Funktion und der zugrunde liegenden Treiber ist ein ODBC 3.. *X* Treiber, der Treiber-Manager ordnet den Funktionsaufruf an die entsprechenden Ersetzungsfunktion. Die einzige Ausnahme dieser Regel wird **SQLExtendedFetch**. (Siehe die Fußnote am Ende der in der folgenden Tabelle.) Weitere Informationen zu diesen Zuordnungen finden Sie unter [veraltet Zuordnungsfunktionen](../../../odbc/reference/appendixes/mapping-deprecated-functions.md) in Anhang G: Treiber Richtlinien für die Abwärtskompatibilität.  
  
 Wenn eine Anwendung verwendet ein Ersatz-Funktion und der zugrunde liegenden Treiber ist ein ODBC-2. *x* -Treiber verwenden, wird der Treiber-Manager den Funktionsaufruf an die entsprechende als veraltet markierte Funktion zugeordnet.  
  
|ODBC-2. *x* Funktion|ODBC-3. *x* Funktion|  
|-------------------------|-------------------------|  
|**SQLAllocConnect**|**SQLAllocHandle**|  
|**SQLAllocEnv**|**SQLAllocHandle**|  
|**SQLAllocStmt:**|**SQLAllocHandle**|  
|**SQLColAttributes**|**SQLColAttribute**|  
|**SQLError**|**SQLGetDiagRec**|  
|**SQLExtendedFetch**[1]|**SQLFetchScroll**|  
|**SQLFreeConnect**|**SQLFreeHandle**|  
|**SQLFreeEnv**|**SQLFreeHandle**|  
|**SQLGetConnectOption**|**SQLGetConnectAttr**|  
|**SQLGetStmtOption**|**SQLGetStmtAttr**|  
|**SQLParamOptions**|**SQLSetStmtAttr**, **SQLGetStmtAttr**|  
|**SQLSetConnectOption**|**SQLSetConnectAttr**|  
|**SQLSetParam**|**SQLBindParameter**|  
|**SQLSetStmtOption**|**SQLSetStmtAttr**|  
|**SQLTransact**|**SQLEndTran**|  
  
 [1]. die Funktion **SQLExtendedFetch** sind doppelte Funktionen; **SQLFetchScroll** bietet die gleiche Funktionalität in ODBC 3.. *X*. Der Treiber-Manager ist jedoch nicht zugeordnet **SQLExtendedFetch** auf **SQLFetchScroll** wenn gegen eine ODBC 3.. *X* Treiber. Weitere Informationen finden Sie unter [der Treiber-Manager Wirkungsweise](../../../odbc/reference/appendixes/what-the-driver-manager-does.md) in Anhang G: Treiber Richtlinien für die Abwärtskompatibilität. Der Treiber-Manager ordnet **SQLFetchScroll** auf **SQLExtendedFetch** Wenn anhand einer ODBC 2.. *X* Treiber.  
  
> [!NOTE]  
>  Die Funktion **SQLBindParam** ist ein Sonderfall. **SQLBindParam** sind doppelt vorhandenen Funktionen. Dies ist keiner ODBC 2.*.x* -Funktion, aber eine Funktion, die in den Open Group und ISO-Standards vorhanden ist. Mithilfe dieser Funktion wird vollständig von der klassifiziert **SQLBindParameter**. Daher ordnet der Treiber-Manager einen Aufruf von **SQLBindParam** auf **SQLBindParameter** beim zugrunde liegenden Treiber ist ein ODBC 3.. *X* Treiber. Wenn die zugrunde liegenden Treiber ist jedoch ein ODBC 2.*.x* Treiber, der Treiber-Manager führt keine diese Zuordnung.

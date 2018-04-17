---
title: SQLSetStmtAttr (Cursorbibliothek) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLSetStmtAttr function [ODBC], Cursor Library
ms.assetid: 6018a733-c2c8-4047-92ec-92cf85031767
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8dd285982ff1483a38673a6e06ecb3293e503782
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sqlsetstmtattr-cursor-library"></a>SQLSetStmtAttr (Cursor Library)
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen und Planen von Anwendungen zu ändern, die dieses Feature verwenden. Microsoft empfiehlt die Verwendung der Cursorfunktionalität der Treiber.  
  
 In diesem Thema erläutert die Verwendung von der **SQLSetStmtAttr** -Funktion in der Cursorbibliothek. Allgemeine Informationen zur **SQLSetStmtAttr**, finden Sie unter [SQLSetStmtAttr-Funktion](../../../odbc/reference/syntax/sqlsetstmtattr-function.md).  
  
 Die Cursorbibliothek unterstützt die folgenden Anweisungsattribute mit **SQLSetStmtAttr**:  
  
|||  
|-|-|  
|SQL_ATTR_CONCURRENCY|SQL_ATTR_ROW_BIND_OFFSET_PTR|  
|SQL_ATTR_CURSOR_TYPE|SQL_ATTR_ROW_BIND_TYPE|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|SQL_ATTR_ROWSET_ARRAY_SIZE|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR|SQL_ATTR_SIMULATE_CURSOR|  
|SQL_ATTR_PARAM_BIND_TYPE|SQL_ATTR_USE_BOOKMARKS|  
  
 Die Cursorbibliothek unterstützt nur die SQL_CURSOR_FORWARD_ONLY und SQL_CURSOR_STATIC Werte des Attributs SQL_ATTR_CURSOR_TYPE-Anweisung.  
  
 Für Vorwärtscursor unterstützt die Cursorbibliothek die SQL_CONCUR_READ_ONLY-Wert, der das SQL_ATTR_CONCURRENCY-Anweisungsattribut auf. Für statische Cursor unterstützt die Cursorbibliothek die SQL_CONCUR_READ_ONLY und SQL_CONCUR_VALUES Werte der SQL_ATTR_CONCURRENCY-Anweisungsattribut auf.  
  
 Die Cursorbibliothek unterstützt nur den SQL_SC_NON_UNIQUE-Wert des Attributs SQL_ATTR_SIMULATE_CURSOR-Anweisung.  
  
 Obwohl die ODBC-Spezifikation Aufrufe unterstützt **SQLSetStmtAttr** mit den Attributen SQL_ATTR_PARAM_BIND_TYPE oder SQL_ATTR_ROW_BIND_TYPE nach **SQLFetch** oder **SQLFetchScroll**  aufgerufen wurde, den Cursor Library hingegen nicht. Bevor sie den Bindungstyp in die Cursorbibliothek ändern kann, muss die Anwendung den Cursor zu schließen. Die Cursorbibliothek unterstützt das Ändern der SQL_ATTR_ROW_BIND_OFFSET_PTR, SQL_ATTR_PARAM_BIND_OFFSET_PTR, SQL_ATTR_ROWS_FETCHED_PTR und SQL_ATTR_PARAMS_PROCESSED_PTR Anweisungsattribute, wenn ein Cursor geöffnet ist.  
  
 Eine Anwendung kann Aufrufen **SQLSetStmtAttr** mit einer **Attribut** von SQL_ATTR_ROW_ARRAY_SIZE, um die Größe des Rowsets zu ändern, während ein Cursor geöffnet ist. Die neue Rowsetgröße wirksam das nächste Mal **SQLFetchScroll** oder **SQLFetch** aufgerufen wird.  
  
 Die Cursorbibliothek unterstützt das Festlegen der SQL_ATTR_PARAM_BIND_OFFSET_PTR oder SQL_ATTR_ROW_BIND_OFFSET_PTR-Anweisungsattribut, um die Bindung Offsets zu aktivieren. Der Offset für die Bindung wird nicht für Aufrufe verwendet **SQLFetch** die Cursorbibliothek bei Verendung mit einer ODBC 2. *X* Treiber.  
  
 Die Cursorbibliothek unterstützt das SQL_ATTR_USE_BOOKMARKS-Anweisungsattribut auf SQL_UB_VARIABLE festlegen.

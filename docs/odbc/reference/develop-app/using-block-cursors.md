---
title: Verwenden von Blockcursorn | Microsoft Docs
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
- cursors [ODBC], block
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 2aad7d6b-216e-47e7-b3cb-f95ad096f21a
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 51f02b5b243286a650897fecdcac5d8778bd3f40
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="using-block-cursors"></a>Verwenden von Blockcursorn
Unterstützung für Blockcursor ist in ODBC 3. integriert. *x*. **SQLFetch** kann nur für mehrzeilige Abrufvorgängen beim Aufruf in ODBC 3. verwendet werden.* X*; Wenn eine ODBC-2.* X* Anwendung ruft **SQLFetch**, es wird nur einen einzeiliges, vorwärtsgerichteten Cursor geöffnet. Wenn eine ODBC-3. *x* Anwendung ruft **SQLFetch** in einer ODBC 2..* X* -Treiber verwenden, es eine einzelne Zeile zurückgibt, wenn der Treiber unterstützt **SQLExtendedFetch**. Weitere Informationen finden Sie unter [Blockcursor, scrollfähige Cursor und Abwärtskompatibilität](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) in Anhang G: Treiber Richtlinien für die Abwärtskompatibilität.  
  
 Zum Verwenden von Blockcursorn die Anwendung die Rowsetgröße wird festgelegt, bindet das Rowset-Puffer (wie im vorherigen Abschnitt beschrieben) optional legt die Anweisungsattribute SQL_ATTR_ROWS_FETCHED_PTR und SQL_ATTR_ROW_STATUS_PTR und Aufrufe **SQLFetch ** oder **SQLFetchScroll** , einen Zeilenblock abzurufen. Die Anwendung kann die Rowsetgröße ändern und neue Rowset Puffer zu binden (durch Aufrufen von **SQLBindCol** oder das Angeben eines Bindung Offsets) auch nach Zeilen abgerufen wurden.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Rowsetgröße](../../../odbc/reference/develop-app/rowset-size.md)  
  
-   [Anzahl der abgerufenen Zeilen und Status](../../../odbc/reference/develop-app/number-of-rows-fetched-and-status.md)  
  
-   [SQLGetData und Blockcursor; Grafikoberfläche zu blockieren](../../../odbc/reference/develop-app/sqlgetdata-and-block-cursors.md)


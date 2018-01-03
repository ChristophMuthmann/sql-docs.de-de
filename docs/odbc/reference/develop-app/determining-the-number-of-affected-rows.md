---
title: Bestimmen der Anzahl der betroffenen Zeilen | Microsoft Docs
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
- updating data [ODBC], number of rows affected
- number of rows affected by update [ODBC]
- data updates [ODBC], number of rows affected
ms.assetid: 1e56297d-a786-415e-b66d-b42d1b2a8d45
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ac4b30fc9bbbb2e289ca53094d5050f0808b3ec1
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="determining-the-number-of-affected-rows"></a>Bestimmen der Anzahl der betroffenen Zeilen
Nachdem eine Anwendung aktualisieren, löschen oder Einfügen von Zeilen, rufen sie **SQLRowCount** um zu bestimmen, wie viele Zeilen betroffen sind. **SQLRowCount** gibt diesen Wert zurück, unabhängig davon, ob die Zeilen wurden aktualisiert, gelöscht oder werden, durch das Ausführen eingefügt einer **UPDATE**, **löschen**, oder **einfügen** Anweisung, durch das Ausführen einer positionierte Update- oder Delete-Anweisung oder durch Aufrufen von **SQLSetPos**.  
  
 Wenn ein Batch von SQL-Anweisungen ausgeführt wird, kann die Anzahl der betroffenen Zeilen Gesamtzahl für alle Anweisungen im Batch oder die einzelnen Anzahlen für jede Anweisung im Batch sein. Weitere Informationen finden Sie unter [Batches von SQL-Anweisungen](../../../odbc/reference/develop-app/batches-of-sql-statements.md) und [mehrere Ergebnisse](../../../odbc/reference/develop-app/multiple-results.md).  
  
 Die Anzahl der betroffenen Zeilen wird auch in der Diagnose-Headerfeld SQL_DIAG_ROW_COUNT im Bereich "Diagnose" das Anweisungshandle zugeordneten zurückgegeben. Allerdings die Daten in diesem Feld werden zurückgesetzt, nachdem jeder Funktionsaufruf auf dem gleichen Anweisungshandle während der Rückgabewert von **SQLRowCount** bleibt unverändert, bis ein Aufruf **SQLBulkOperations**, **SQLExecute**, **SQLExecDirect**, **SQLPrepare**, oder **SQLSetPos**.

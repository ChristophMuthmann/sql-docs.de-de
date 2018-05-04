---
title: Bestimmen der Anzahl der betroffenen Zeilen | Microsoft Docs
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
ms.topic: conceptual
helpviewer_keywords:
- updating data [ODBC], number of rows affected
- number of rows affected by update [ODBC]
- data updates [ODBC], number of rows affected
ms.assetid: 1e56297d-a786-415e-b66d-b42d1b2a8d45
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2b826520d76b36eefab78de7e1d9db34ed202fb6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="determining-the-number-of-affected-rows"></a>Bestimmen der Anzahl der betroffenen Zeilen
Nachdem eine Anwendung aktualisieren, löschen oder Einfügen von Zeilen, rufen sie **SQLRowCount** um zu bestimmen, wie viele Zeilen betroffen sind. **SQLRowCount** gibt diesen Wert zurück, unabhängig davon, ob die Zeilen wurden aktualisiert, gelöscht oder werden, durch das Ausführen eingefügt einer **UPDATE**, **löschen**, oder **einfügen** -Anweisung durch das Ausführen einer positionierte update oder delete-Anweisung oder durch den Aufruf von **SQLSetPos**.  
  
 Wenn ein Batch von SQL-Anweisungen ausgeführt wird, kann die Anzahl der betroffenen Zeilen Gesamtzahl für alle Anweisungen im Batch oder die einzelnen Anzahlen für jede Anweisung im Batch sein. Weitere Informationen finden Sie unter [Batches von SQL-Anweisungen](../../../odbc/reference/develop-app/batches-of-sql-statements.md) und [mehrere Ergebnisse](../../../odbc/reference/develop-app/multiple-results.md).  
  
 Die Anzahl der betroffenen Zeilen wird auch in der Diagnose-Headerfeld SQL_DIAG_ROW_COUNT im Bereich "Diagnose" das Anweisungshandle zugeordneten zurückgegeben. Allerdings die Daten in diesem Feld werden zurückgesetzt, nachdem jeder Funktionsaufruf auf dem gleichen Anweisungshandle während der Rückgabewert von **SQLRowCount** bleibt unverändert, bis ein Aufruf **SQLBulkOperations**, **SQLExecute**, **SQLExecDirect**, **SQLPrepare**, oder **SQLSetPos**.

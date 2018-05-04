---
title: Fehler und Batches | Microsoft Docs
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
- batches [ODBC], errors
- sql_success_with_info [ODBC]
- sql_success [ODBC]
- SQL statements [ODBC], batches
- sql_error [ODBC]
ms.assetid: 6debd41d-9f4c-4f4c-a44b-2993da5306f0
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9f9ad11a7f9f0f89e2aa1320b221ce43ac04573e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="errors-and-batches"></a>Fehler und Batches
Tritt ein Fehler während der Ausführung eines Batches von SQL-Anweisungen, eine der folgenden vier Ergebnisse sind möglich. (Jede mögliches Ergebnis Daten datenquellenspezifischen und möglicherweise sogar richten sich nach den Anweisungen im Batch enthalten.)  
  
-   Es werden keine Anweisungen im Batch ausgeführt.  
  
-   Keine Anweisungen im Batch ausgeführt werden, und die Transaktion zurückgesetzt wird.  
  
-   Alle Anweisungen vor der Error-Anweisung ausgeführt werden.  
  
-   Alle Anweisungen mit Ausnahme der Error-Anweisung ausgeführt werden.  
  
 In den ersten beiden Fällen **SQLExecute** und **SQLExecDirect** SQL_ERROR zurück. In den letzten beiden Fällen können sie SQL_SUCCESS_WITH_INFO oder SQL_SUCCESS, je nach Implementierung zurückgeben. In allen Fällen weitere Fehlerinformationen abgerufen werden mit **SQLGetDiagField**, **SQLGetDiagRec**, oder **SQLError**. Die Art und Tiefe der diese Informationen sind jedoch Daten datenquellenspezifischen. Darüber hinaus sind diese Informationen wahrscheinlich nicht genau die Anweisung im Fehler zu identifizieren.

---
title: "Parallelitätstypen | Microsoft Docs"
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
- transactions [ODBC], concurrency control
- concurrency control [ODBC]
- locking concurrency control [ODBC]
- optimistic concurrency [ODBC]
- read-only concurrency control [ODBC]
ms.assetid: 46762ae5-17dd-4777-968e-58156f470fe1
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 737fadc881109457051cf30bfce9b493bd164f1c
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="concurrency-types"></a>Parallelitätstypen
Zum Lösen des Problems der reduzierter Parallelität in Cursorn macht ODBC vier verschiedene Typen von Cursorparallelität verfügbar:  
  
-   **Nur-Lese** Cursor Daten lesen, aber nicht aktualisieren oder Löschen von Daten kann. Dies ist der Standardtyp für die Parallelität. Obwohl das DBMS Zeilen, um die Repeatable Read und Serializable-Isolation Levels erzwingen sperren können, können Lesesperren anstelle von Schreibsperren. Dies führt zu höhere Parallelität, da die Daten von anderen Transaktionen mindestens lesen können.  
  
-   **Sperren** Cursor verwendet die niedrigste Ebene von Sperren erforderlich, um sicherzustellen, dass es zu aktualisieren oder Löschen von Zeilen im Resultset kann. Dies führt in der Regel sehr niedrigen Parallelitätsstufen, insbesondere auf die Transaktionsisolationsstufen Repeatable Read und Serializable.  
  
-   **Vollständige Parallelität, die mithilfe von Zeilenversionen und vollständige Parallelität mit Werten** der Cursor verwendet die vollständigen Parallelität: aktualisiert oder löscht Zeilen nur dann, wenn sie nicht geändert wurden, seit sie zuletzt gelesen wurden. Um die Änderungen zu erkennen, vergleicht er Zeilenversionen oder Werte. Es gibt keine Garantie, dass der Cursor wird in der Lage, aktualisieren oder Löschen einer Zeile sein, aber die Parallelität ist sehr viel höher als beim Sperren verwendet wird. Weitere Informationen finden Sie unter den folgenden Abschnitt [vollständige Parallelität](../../../odbc/reference/develop-app/optimistic-concurrency.md).  
  
 Eine Anwendung gibt an, welche Art von Parallelität des Cursors für die Verwendung mit der SQL_ATTR_CONCURRENCY-Anweisungsattribut werden sollen. Um zu bestimmen, welche Typen unterstützt werden, ruft er **SQLGetInfo** mit der Option SQL_SCROLL_CONCURRENCY.

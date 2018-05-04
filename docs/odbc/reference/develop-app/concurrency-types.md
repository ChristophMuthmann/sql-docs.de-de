---
title: Parallelitätstypen | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
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
manager: craigg
ms.openlocfilehash: 6b5970995d3b8f881b62556b0f12eac96d302760
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="concurrency-types"></a>Parallelitätstypen
Zum Lösen des Problems der reduzierter Parallelität in Cursorn macht ODBC vier verschiedene Typen von Cursorparallelität verfügbar:  
  
-   **Nur-Lese** Cursor Daten lesen, aber nicht aktualisieren oder Löschen von Daten kann. Dies ist der Standardtyp für die Parallelität. Obwohl das DBMS Zeilen, um die Repeatable Read und Serializable-Isolation Levels erzwingen sperren können, können Lesesperren anstelle von Schreibsperren. Dies führt zu höhere Parallelität, da die Daten von anderen Transaktionen mindestens lesen können.  
  
-   **Sperren** Cursor verwendet die niedrigste Ebene von Sperren erforderlich, um sicherzustellen, dass es zu aktualisieren oder Löschen von Zeilen im Resultset kann. Dies führt in der Regel sehr niedrigen Parallelitätsstufen, insbesondere auf die Transaktionsisolationsstufen Repeatable Read und Serializable.  
  
-   **Vollständige Parallelität, die mithilfe von Zeilenversionen und vollständige Parallelität mit Werten** der Cursor verwendet die vollständigen Parallelität: aktualisiert oder löscht Zeilen nur dann, wenn sie nicht geändert wurden, seit sie zuletzt gelesen wurden. Um die Änderungen zu erkennen, vergleicht er Zeilenversionen oder Werte. Es gibt keine Garantie, dass der Cursor wird in der Lage, aktualisieren oder Löschen einer Zeile sein, aber die Parallelität ist sehr viel höher als beim Sperren verwendet wird. Weitere Informationen finden Sie unter den folgenden Abschnitt [vollständige Parallelität](../../../odbc/reference/develop-app/optimistic-concurrency.md).  
  
 Eine Anwendung gibt an, welche Art von Parallelität des Cursors für die Verwendung mit der SQL_ATTR_CONCURRENCY-Anweisungsattribut werden sollen. Um zu bestimmen, welche Typen unterstützt werden, ruft er **SQLGetInfo** mit der Option SQL_SCROLL_CONCURRENCY.

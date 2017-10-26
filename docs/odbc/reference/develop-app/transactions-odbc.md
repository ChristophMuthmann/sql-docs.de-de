---
title: ODBC-Transaktionen | Microsoft Docs
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
- transactions [ODBC], about transactions
- transactions [ODBC]
ms.assetid: b4ca861a-c164-4e87-8672-d5de15e3823c
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d11b681fa324c2c0b514bfb43aa67d51ce19a1ba
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="transactions-odbc"></a>ODBC-Transaktionen
Ein *Transaktion* ist eine Arbeitseinheit, die als einzelne, atomaren Vorgang erfolgt; bedeutet, dass der Vorgang erfolgreich ist oder ein Fehler auftritt, als Ganzes. Betrachten Sie z. B. Geld von einem Bankkonto auf einen anderen übertragen. Dies umfasst zwei Schritte: das Geld vom ersten Konto das Abbuchen und es in der zweiten einzahlen. Es ist wichtig, dass beide Schritte erfolgreich sind. Es ist nicht akzeptabel ein Schritt erfolgreich ausgeführt werden kann und die andere fehlschlägt. Eine Datenbank, die Transaktionen unterstützt kann dies zu garantieren.  
  
 Transaktionen abgeschlossen werden können, indem Sie entweder *Commit* oder *Rollback*. Wenn eine Transaktion ein Commit ausgeführt wird, die Änderungen, da Transaktionen werden dauerhaft vorgenommen. Beim Rollback einer Transaktions ausgeführt wird, werden die betroffenen Zeilen in den Zustand versetzt, denen sie hatten, bevor die Transaktion gestartet wurde. Um das Konto Übertragung Beispiel erweitern, führt eine Anwendung eine SQL-Anweisung das erste Konto belastet und einer anderen SQL-Anweisung auf das zweite Konto haben. Wenn beide Anweisungen erfolgreich ausgeführt werden, führt die Anwendung dann Commit der Transaktion. Aber wenn entweder Anweisung aus irgendeinem Grund fehlschlägt, die Anwendung wird durch ein Rollback der Transaktion. In beiden Fällen wird die Anwendung einen konsistenten Status am Ende der Transaktion sichergestellt.  
  
 Eine einzelne Transaktion kann mehrere Datenbankvorgänge umfassen, die zu unterschiedlichen Zeiten auftreten. Wenn andere Transaktionen vollständigen Zugriff auf die Zwischenergebnisse hatten, möglicherweise die Transaktionen untereinander beeinträchtigen. Beispielsweise angenommen, eine Transaktion eine Zeile einfügt, liest eine zweite Transaktion diese Zeile und die erste Transaktion zurückgesetzt wird. Die zweite Transaktion jetzt hat Daten für eine Zeile, die nicht vorhanden ist.  
  
 Um dieses Problem zu lösen, stehen Ihnen verschiedene Schemas auf Transaktionen voneinander zu isolieren. *Transaktionsisolation* wird in der Regel implementiert, durch Sperren von Zeilen, die mehr als eine Transaktion von der Verwendung der gleichen Zeile zur gleichen Zeit, schließt. In einigen Datenbanken möglicherweise andere Zeilen beim Sperren einer Zeile auch sperren.  
  
 Erhöhte Transaction Isolation Klassentreiber reduzierte *Parallelität,* oder die Fähigkeit von zwei Transaktionen gleichzeitig dieselben Daten verwenden. Weitere Informationen finden Sie unter [Festlegen der Isolationsstufe für Transaktionen](../../../odbc/reference/develop-app/setting-the-transaction-isolation-level.md).  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Transaktionen in ODBC](../../../odbc/reference/develop-app/transactions-in-odbc-odbc.md)  
  
-   [Transaktionsisolation](../../../odbc/reference/develop-app/transaction-isolation.md)  
  
-   [Parallelitätssteuerung](../../../odbc/reference/develop-app/concurrency-control.md)


---
title: "Parallelitätssteuerung | Microsoft Docs"
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
ms.assetid: 75e4adb3-3d43-49c5-8c5e-8df96310d912
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a10dc30810a1ea71bd4e2c9d823ed010f7f611d4
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="concurrency-control"></a>Parallelitätssteuerung
*Parallelität* ist die Fähigkeit von zwei Transaktionen gleichzeitig dieselben Daten verwenden und mit erhöhter Transaction Isolation normalerweise reduzierten Parallelität ist. Dies ist, da die Isolation jeder Transaktion wird durch Sperren von Zeilen in der Regel implementiert, und wie weitere Zeilen gesperrt sind, weniger Transaktionen abgeschlossen werden, können ohne durch eine gesperrte Zeile zumindest vorübergehend blockiert. Während reduzierter Parallelität in der Regel als ein Kompromiss für höheren Isolationsstufen von Transaktionen für das Verwalten der Datenbankintegrität erforderlich akzeptiert wird, kann es ein Problem bei der interaktiven Anwendungen mit hoher Lese-/Schreibzugriff-Aktivität, die Cursor verwendet werden.  
  
 Nehmen wir beispielsweise an, die eine Anwendung führt die SQL-Anweisung **wählen \* FROM Orders**. Sie ruft **SQLFetchScroll** , um das Ergebnis zu scrollen festgelegt und ermöglicht es dem Benutzer zu aktualisieren, löschen oder Einfügen von Bestellungen. Nachdem der Benutzer aktualisieren, löschen oder einen Auftrag einfügt, wird die Anwendung die Transaktion bestätigt.  
  
 Wenn die Isolationsstufe Repeatable Read ist, wird die Transaktion möglicherweise – je nachdem, wie er implementiert wurde – Sperren Sie jede zurückgegebene Zeile **SQLFetchScroll**. Wenn die Isolationsstufe Serializable ist, möglicherweise die Transaktion die gesamte Orders-Tabelle gesperrt. In beiden Fällen gibt die Transaktion nur, wenn sie ein Commit oder Rollback ist ihre Sperren frei. Wenn der Benutzer viel Zeit Lesen von Bestellungen und nur wenig Zeit aktualisieren benötigt, löschen oder einfügen, die Transaktion einfach konnte Sperren Sie daher eine große Anzahl von Zeilen, die dadurch nicht verfügbar, anderen Benutzern.  
  
 Dies ist ein Problem, selbst wenn der Cursor schreibgeschützt ist, und die Anwendung der Benutzer nur vorhandene Bestellungen zu lesen kann. In diesem Fall die Anwendung führt einen Commit der Transaktion und Sperren frei, wenn es aufruft **SQLCloseCursor** (im Autocommit-Modus) oder **SQLEndTran** (im Manualcommit-Modus).  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Parallelitätstypen](../../../odbc/reference/develop-app/concurrency-types.md)  
  
-   [Vollständige Parallelität](../../../odbc/reference/develop-app/optimistic-concurrency.md)


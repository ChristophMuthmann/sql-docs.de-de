---
title: Batches von SQL-Anweisungen | Microsoft Docs
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
- batches [ODBC]
- SQL statements [ODBC], batches
- batches [ODBC], about batches
ms.assetid: 766488cc-450c-434c-9c88-467f6c57e17c
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: d2ae8d60d6e41536bc67bd14f9252c372fdeaa5c
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="batches-of-sql-statements"></a>Batches von SQL-Anweisungen
Ein Batch von SQL-Anweisungen ist eine Gruppe von mindestens zwei SQL-Anweisungen oder eine einzelne SQL-Anweisung, die dieselbe Wirkung wie eine Gruppe von mindestens zwei SQL-Anweisungen aufweist. In allen Implementationen wird die gesamte Batch-Anweisung ausgeführt, bevor Ergebnisse zur Verfügung stehen. Dies ist häufig effizienter als das Senden getrennter Anweisungen sein, da der Netzwerkdatenverkehr dadurch meist reduziert und die Datenquelle kann die Ausführung eines Batches von SQL-Anweisungen manchmal optimieren. In anderen Implementierungen Aufrufen **SQLMoreResults** löst die Ausführung die nächste Anweisung im Batch. ODBC unterstützt die folgenden Arten von Batches:  
  
-   **Explizite Batches** ein *explizite Batch* mindestens zwei SQL-Anweisungen, die durch Semikolons (;) getrennt ist. Beispielsweise wird der folgende Batch von SQL-Anweisungen einen neuen Verkaufsauftrag geöffnet. Dies erfordert das Einfügen von Zeilen in Tabellen der Aufträge und die Zeilen. Beachten Sie, dass kein Semikolon nach der letzten Anweisung vorhanden ist.  
  
    ```  
    INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
       VALUES (2002, 1001, {fn CURDATE()}, 'Garcia', 'OPEN');  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (2002, 1, 1234, 10);  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (2002, 2, 987, 8);  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (2002, 3, 566, 17);  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (2002, 4, 412, 500)  
    ```  
  
-   **Prozeduren** , wenn eine Prozedur mehr als eine SQL-Anweisung enthält, gilt es einen Batch von SQL-Anweisungen ausgeführt werden. Die folgende SQL Server-spezifische Anweisung erstellt z. B. eine Prozedur, die ein Resultset mit Informationen über ein Kunde und ein Resultset, das Auflisten aller offenen Aufträge für diesen Kunden zurückgibt:  
  
    ```  
    CREATE PROCEDURE GetCustInfo (@CustomerID INT) AS  
       SELECT * FROM Customers WHERE CustID = @CustomerID  
       SELECT OrderID FROM Orders  
          WHERE CustID = @CustomerID AND Status = 'OPEN'  
    ```  
  
     Die **CREATE PROCEDURE** -Anweisung selbst ist ein Batch von SQL-Anweisungen. Die Prozedur erstellt wird, ist jedoch ein Batch von SQL-Anweisungen. Keine Semikolons trennen Sie die beiden **wählen** Anweisungen da die **CREATE PROCEDURE** -Anweisung ist spezifisch für SQL Server und SQL Server erfordert keine Semikolons, um mehrere Anweisungen in einem  **CREATE PROCEDURE** Anweisung.  
  
-   **Arrays von Parametern** Arrays von Parametern mit einer parametrisierten SQL-Anweisung als eine effektive Möglichkeit für das Ausführen von Massenvorgängen verwendet werden können. Beispielsweise können Arrays von Parametern verwendet werden, mit den folgenden **einfügen** Anweisung mehrere Zeilen in der Tabelle Zeilen eingefügt werden, während der Ausführung nur einer einzelnen SQL-Anweisung:  
  
    ```  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (?, ?, ?, ?)  
    ```  
  
     Wenn Arrays von Parametern in eine Datenquelle nicht unterstützt wird, können Sie von der Treiber durch Ausführen der SQL-Anweisung einmal für jeden Satz von Parametern emuliert werden. Weitere Informationen finden Sie unter [Anweisungsparametern](../../../odbc/reference/develop-app/statement-parameters.md) und [Arrays von Parameterwerten](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)weiter unten in diesem Abschnitt.  
  
 Die verschiedenen Arten von Batches können nicht auf interoperable Weise gemischt werden. Also wie eine Anwendung bestimmt das Ergebnis der Ausführung eines expliziten Batches, die Prozedur aufruft, einen explizite Batch, der Arrays von Parametern, verwendet und den Aufruf einer Prozedur, der Arrays von Parametern verwendet wird, treiberspezifische.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Anweisungen mit generiertem Ergebnis und ohne Ergebnis](../../../odbc/reference/develop-app/result-generating-and-result-free-statements.md)  
  
-   [Ausführen von Batches](../../../odbc/reference/develop-app/executing-batches.md)  
  
-   [Fehler und Batches](../../../odbc/reference/develop-app/errors-and-batches.md)

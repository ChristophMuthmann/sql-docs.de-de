---
title: Abrufen von Ergebnissen (Basic) | Microsoft Docs
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
- result sets [ODBC], about result sets
- data sources [ODBC], result sets
- empty result sets [ODBC]
ms.assetid: 052870e3-3f3f-4f07-91da-b649348225f4
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 22969a69bf70e862335d48abae41bf9e37f6c24a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="retrieving-results-basic"></a>Abrufen von Ergebnissen (Basic)
Ein *Resultset* ist ein Satz von Zeilen in der Datenquelle, die bestimmten Kriterien entsprechen. Es ist eine grundlegende Tabelle, die Ergebnisse aus einer Abfrage und in tabellarischer Form, die für eine Anwendung verfügbar ist. **Wählen Sie** Anweisungen, Katalogfunktionen und einige Verfahren erstellen Sie Resultsets. Im folgenden Beispiel die erste SQL-Anweisung erstellt ein Resultset mit der alle Zeilen und alle Spalten in der Orders-Tabelle und die zweite SQL-Anweisung erstellt ein Resultset mit Spalten für OrderID, Vertriebsmitarbeiter, und den Status für die Zeilen in der Orders-Tabelle der Status ist in der "OPEN":  
  
```  
SELECT * FROM Orders  
SELECT OrderID, SalesPerson, Status FROM Orders WHERE Status = 'OPEN'  
```  
  
 Ein Resultset kann leer sein, unterscheidet sich vom überhaupt kein Resultset. Die folgende SQL-Anweisung erstellt z. B. ein leeres Resultset:  
  
```  
SELECT * FROM Orders WHERE 1 = 2  
```  
  
 Ein leeres Resultset unterscheidet sich nicht aus den anderen Ergebnissen, die festlegen, mit dem Unterschied, dass es keine Zeilen enthält. Die Anwendung z. B. Abrufen von Metadaten für das Resultset kann, kann versuchen, die Zeilen abzurufen und schließen Sie den Cursor über das Resultset muss.  
  
 Der Prozess des Abrufens von Zeilen aus der Datenquelle und deren Rückgabe an die Anwendung heißt *abrufen*. Dieser Abschnitt erläutert die grundlegenden Teile dieses Prozesses. Informationen zu den FORTFÜHRENDEN Themen, z. B. Blocks und bildlauffähigen Cursor finden Sie unter [Blockcursor](../../../odbc/reference/develop-app/block-cursors.md) und [bildlauffähige Cursor](../../../odbc/reference/develop-app/scrollable-cursors.md). Informationen zum Aktualisieren, löschen und Einfügen von Zeilen finden Sie unter [Übersicht über die Daten Aktualisierung](../../../odbc/reference/develop-app/updating-data-overview.md).  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Wurde ein Resultset erstellt?](../../../odbc/reference/develop-app/was-a-result-set-created.md)  
  
-   [Resultsetmetadaten](../../../odbc/reference/develop-app/result-set-metadata.md)  
  
-   [Binden von Spalten](../../../odbc/reference/develop-app/binding-columns.md)  
  
-   [Abrufen von Daten](../../../odbc/reference/develop-app/fetching-data.md)  
  
-   [Schließen des Cursors](../../../odbc/reference/develop-app/closing-the-cursor.md)

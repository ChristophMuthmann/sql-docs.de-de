---
title: "Bildlauffähige Cursor | Microsoft Docs"
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
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
ms.assetid: 2c8a5f50-9b37-452f-8160-05f42bc4d97e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 07e868f5798e759a9b84e9c28d2c1fa82bb34c4f
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="scrollable-cursors"></a>Bildlauffähige Cursor
In modernen Bildschirm basierende Anwendungen verschiebt der Benutzer rückwärts und Vorwärts durch die Daten an. Für solche Anwendungen ist die Rückgabe an einer zuvor abgerufenen Zeile ein Problem. Eine Möglichkeit besteht darin, zu schließen und erneut öffnen des Cursors und rufen Sie Zeilen an, bis der Cursor über die erforderlichen Zeile erreicht. Eine andere Möglichkeit besteht darin, lesen das Resultset, lokal zwischengespeichert und Durchführen eines Bildlaufs in der Anwendung zu implementieren. Beide Möglichkeiten funktionieren, auch nur mit kleinen Resultsets, und die zweite Möglichkeit ist schwierig zu implementieren. Eine bessere Lösung ist die Verwendung einer *bildlauffähigen Cursor* im Resultset vorwärts und rückwärts verschieben können.  
  
 Ein *bildlauffähigen Cursor* häufig im modernen Bildschirm basierende Anwendungen, in dem der Benutzer einen hin-und durch die Daten Bildlauf, verwendet wird. Allerdings sollten Anwendungen bildlauffähige Cursor verwenden, wenn Vorwärtscursor nicht den Auftrag werden als bildlauffähige Cursor in der Regel teurer als Vorwärtscursor sind.  
  
 Die Möglichkeit, rückwärts zu bewegen, löst eine Frage gilt nicht für Vorwärtscursor: sollte ein bildlauffähigen Cursor erkennen Änderungen an zuvor abgerufenen Zeilen? Erkennen es sollte also aktualisierte, gelöschte und neu eingefügte Zeilen?  
  
 Diese Frage tritt auf, da die Definition eines Ergebnisses festgelegt – die Menge der Zeilen, die bestimmte Kriterien erfüllt – nicht vorschreiben, wenn Zeilen überprüft werden, um festzustellen, ob sie die Kriterien übereinstimmen, noch wird mit dem Status Gibt an, ob Zeilen die gleichen Daten jedes Mal enthalten müssen Abrufvorgang ausgeführt werden. Die frühere Auslassung ermöglicht bildlauffähige Cursor zu ermitteln, ob Zeilen wurden eingefügt oder werden, gelöscht während Letzteres diese aktualisierte Daten erkennen kann.  
  
 Die Fähigkeit, Änderungen zu erkennen ist manchmal hilfreich, in einigen Fällen nicht. Beispielsweise benötigt eine Accounting-Anwendung einen Cursor, der alle Änderungen werden ignoriert; Lastenausgleich Bücher ist nicht möglich, wenn der Cursor die neuesten Änderungen angezeigt wird. Andererseits, benötigt eine Airline Reservierungssystem einen Cursor, der die neuesten Änderungen an den Daten zeigt; ohne einen Cursor müssen sie die Datenbank, um die Verfügbarkeit der aktuellsten Flight anzeigen ständig requery.  
  
 Damit die Anforderungen unterschiedlicher Anwendungen abgedeckt wird, definiert ODBC vier verschiedene Typen von scrollfähige Cursor. Diese Cursor variieren sowohl in der Ausgabe und in ihrer Fähigkeit zum Erkennen von Änderungen auf das Ergebnis festgelegt. Beachten Sie, dass wenn Sie ein bildlauffähigen Cursor Änderungen an Zeilen erkennen kann, nur diese erkannt werden können, wenn er versucht, diese Zeilen erneut abzurufen. Es gibt keine Möglichkeit für die Datenquelle den Cursor von Änderungen an den derzeit abgerufenen Zeilen informieren könnte. Beachten Sie auch, dass die Sichtbarkeit der Änderungen auch von der Transaktionsisolationsstufe gesteuert wird. Weitere Informationen finden Sie unter [Transaktionsisolation](../../../odbc/reference/develop-app/transaction-isolation.md).  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Bildlauffähige Cursortypen](../../../odbc/reference/develop-app/scrollable-cursor-types.md)  
  
-   [Bildlauffähige Cursor verwenden](../../../odbc/reference/develop-app/using-scrollable-cursors.md)  
  
-   [Relative und Absolute Durchführen eines Bildlaufs](../../../odbc/reference/develop-app/relative-and-absolute-scrolling.md)  
  
-   [Lesezeichen](../../../odbc/reference/develop-app/bookmarks-odbc.md)


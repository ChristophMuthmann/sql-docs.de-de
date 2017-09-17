---
title: Schreiben einer interoperablen Anwendung | Microsoft Docs
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
- interoperability [ODBC], feature support and variability
- interoperability [ODBC], writing interoperable applications
- feature support in interoperable applications [ODBC]
- feature variability in interoperable applications [ODBC]
ms.assetid: 8b42b8ae-7862-4b63-a0b3-2a204e0c43a5
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bab5be84b66571f7ca361a3b158921330c00007f
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="writing-an-interoperable-application"></a>Schreiben einer interoperablen Anwendung
Wenn eine Anwendung den gleichen Code für mehr als einen Treiber verwendet, muss diesen Code zwischen Treiber interoperabel sein. In den meisten Fällen ist dies eine einfache Aufgabe. Beispielsweise ist der Code zum Abrufen von Zeilen mit einem Vorwärtscursor für alle Treiber identisch. In einigen Fällen kann dies schwieriger sein. Beispielsweise muss der Code zum Konstruieren der Bezeichner für die Verwendung in SQL-Anweisungen Bezeichner Groß-/Kleinschreibung, zitieren und einteiliger, mit dem zweiteiligen und dreiteiligen Benennungskonventionen berücksichtigen.  
  
 Interoperable Code muss im allgemeinen Problemen mit der Unterstützung von Funktionen und Features Variabilität bewältigen. *-Funktionsunterstützung* bezieht sich auf, und zwar unabhängig davon, ob ein bestimmtes Feature unterstützt wird. Z. B. nicht alle DBMS Transaktionen unterstützt, und interoperable Code muss unabhängig von der Unterstützung von Transaktionen ordnungsgemäß funktionieren. *Feature Variabilität* verweist auf Variation auf die Weise, in dem ein bestimmtes Feature unterstützt wird. Katalognamen werden z. B. am Anfang von Bezeichnern in einigen DBMS und am Ende von Bezeichnern in anderen platziert.  
  
 Anwendungen können mit Unterstützung von Funktionen und Features Variabilität zur Entwurfszeit oder zur Laufzeit behandeln. Um zur Entwurfszeit mit Unterstützung von Funktionen und Variierbarkeit zu behandeln, ein Entwickler untersucht die Ziel-DBMS und die Treiber und stellt sicher, dass der gleiche Code untereinander interoperabel ist. Dies ist in der Regel die Möglichkeit, in der Anwendungen mit wenig oder nur eine begrenzte Interoperabilität diese Probleme behandelt.  
  
 Z. B. benötigt Wenn der Entwickler wird sichergestellt, dass eine vertikale Anwendung nur mit vier bestimmten DBMS geeignet ist und jede dieser DBMS-Transaktionen unterstützt, die Anwendung nicht Code zum Überprüfen der Unterstützung von Transaktionen zur Laufzeit. Kann sie immer davon ausgehen, dass aufgrund der Entscheidung zur Entwurfszeit mit nur vier DBMS Transaktionen verfügbar sind jeweils Transaktionen unterstützt.  
  
 Um zur Laufzeit mit Unterstützung von Funktionen und Variierbarkeit zu verarbeiten, muss die Anwendung zur Laufzeit für andere Funktionen zu testen und entsprechend agieren. Dies ist in der Regel die Möglichkeit, die in der äußerst interoperable Anwendungen diese Probleme behandelt. Probleme mit der Funktion bedeutet das Schreiben von Code, mit der die Funktion optional oder das Schreiben von Code, der die Funktion emuliert, wenn er nicht verfügbar ist. Für Funktion Variabilität Probleme bedeutet dies, Code schreiben, der alle mögliche Variationen unterstützt.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Überprüfung der Unterstützung von Funktionen und die Variabilität](../../../odbc/reference/develop-app/checking-feature-support-and-variability.md)  
  
-   [Funktionen, die Überwachung für](../../../odbc/reference/develop-app/features-to-watch-for.md)

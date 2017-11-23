---
title: Schreiben einer interoperablen Anwendung | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- interoperability [ODBC], feature support and variability
- interoperability [ODBC], writing interoperable applications
- feature support in interoperable applications [ODBC]
- feature variability in interoperable applications [ODBC]
ms.assetid: 8b42b8ae-7862-4b63-a0b3-2a204e0c43a5
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ec3f9821b729c593fac8cb280f8596eaf0dbed1d
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="writing-an-interoperable-application"></a>Schreiben einer interoperablen Anwendung
Wenn eine Anwendung den gleichen Code für mehr als einen Treiber verwendet, muss diesen Code zwischen Treiber interoperabel sein. In den meisten Fällen ist dies eine einfache Aufgabe. Beispielsweise ist der Code zum Abrufen von Zeilen mit einem Vorwärtscursor für alle Treiber identisch. In einigen Fällen kann dies schwieriger sein. Beispielsweise muss der Code zum Konstruieren der Bezeichner für die Verwendung in SQL-Anweisungen Bezeichner Groß-/Kleinschreibung, zitieren und einteiliger, mit dem zweiteiligen und dreiteiligen Benennungskonventionen berücksichtigen.  
  
 Interoperable Code muss im allgemeinen Problemen mit der Unterstützung von Funktionen und Features Variabilität bewältigen. *-Funktionsunterstützung* bezieht sich auf, und zwar unabhängig davon, ob ein bestimmtes Feature unterstützt wird. Z. B. nicht alle DBMS Transaktionen unterstützt, und interoperable Code muss unabhängig von der Unterstützung von Transaktionen ordnungsgemäß funktionieren. *Feature Variabilität* verweist auf Variation auf die Weise, in dem ein bestimmtes Feature unterstützt wird. Katalognamen werden z. B. am Anfang von Bezeichnern in einigen DBMS und am Ende von Bezeichnern in anderen platziert.  
  
 Anwendungen können mit Unterstützung von Funktionen und Features Variabilität zur Entwurfszeit oder zur Laufzeit behandeln. Um zur Entwurfszeit mit Unterstützung von Funktionen und Variierbarkeit zu behandeln, ein Entwickler untersucht die Ziel-DBMS und die Treiber und stellt sicher, dass der gleiche Code untereinander interoperabel ist. Dies ist in der Regel die Möglichkeit, in der Anwendungen mit wenig oder nur eine begrenzte Interoperabilität diese Probleme behandelt.  
  
 Z. B. benötigt Wenn der Entwickler wird sichergestellt, dass eine vertikale Anwendung nur mit vier bestimmten DBMS geeignet ist und jede dieser DBMS-Transaktionen unterstützt, die Anwendung nicht Code zum Überprüfen der Unterstützung von Transaktionen zur Laufzeit. Kann sie immer davon ausgehen, dass aufgrund der Entscheidung zur Entwurfszeit mit nur vier DBMS Transaktionen verfügbar sind jeweils Transaktionen unterstützt.  
  
 Um zur Laufzeit mit Unterstützung von Funktionen und Variierbarkeit zu verarbeiten, muss die Anwendung zur Laufzeit für andere Funktionen zu testen und entsprechend agieren. Dies ist in der Regel die Möglichkeit, die in der äußerst interoperable Anwendungen diese Probleme behandelt. Probleme mit der Funktion bedeutet das Schreiben von Code, mit der die Funktion optional oder das Schreiben von Code, der die Funktion emuliert, wenn er nicht verfügbar ist. Für Funktion Variabilität Probleme bedeutet dies, Code schreiben, der alle mögliche Variationen unterstützt.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Überprüfung der Unterstützung von Funktionen und Variabilität](../../../odbc/reference/develop-app/checking-feature-support-and-variability.md)  
  
-   [Funktionen, die überwacht werden müssen](../../../odbc/reference/develop-app/features-to-watch-for.md)

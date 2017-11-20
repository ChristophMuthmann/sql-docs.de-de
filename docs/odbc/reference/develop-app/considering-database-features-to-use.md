---
title: "Berücksichtigung Datenbankfunktionen zu verwendenden | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- interoperability [ODBC], database features
ms.assetid: 59760114-508e-46c5-81d2-8f2498c0d778
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d17758711dd0e4e1590a3b4176829d9709a5dfd0
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="considering-database-features-to-use"></a>Erwägen die Datenbankfunktionen verwenden
Nachdem das grundlegende Maß an Interoperabilität bekannt ist, müssen die Datenbankfunktionen, die von der Anwendung verwendeten berücksichtigt werden. Welche SQL-Anweisungen wird z. B. die Anwendung ausführen? Verwendet die Anwendung bildlauffähigen Cursor? Transaktionen? Verfahren? Long-Daten? Weitere Ideen zur welche Funktionen möglicherweise nicht von allen DBMS unterstützt werden müssen, finden Sie unter der [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md), [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md), und [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md) Funktion Beschreibungen und [ Anhang C: SQL-Grammatik](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md). Die Funktionen, die von einer Anwendung benötigt möglicherweise einige DBMS aus der Liste der Ziel-DBMS vermieden. Sie können auch anzeigen, dass die Anwendung leicht viele Datenbankmanagementsysteme Ziel verwendet werden kann.  
  
 Z. B. wenn die erforderlichen Features einfach sind, können sie in der Regel mit einem hohen Grad an Interoperabilität implementiert werden. Eine Anwendung, die eine einfache führt **wählen** -Anweisung und ruft Ergebnisse mit einem Vorwärtscursor ist wahrscheinlich aufgrund seiner Einfachheit äußerst interoperabler: fast alle Treiber und DBMS unterstützen die Funktionalität es muss.  
  
 Wenn die erforderlichen Features komplexer, z. B. bildlauffähige Cursor, positionierte Update- und Delete-Anweisungen und Prozeduren sind, müssen vor-und Nachteile häufig vorgenommen. Es gibt mehrere Möglichkeiten:  
  
-   **Niedrigere Interoperabilität, weitere Funktionen.** Die Anwendung enthält die Funktionen, aber kann nur mit DBMS-Systeme, die sie unterstützen.  
  
-   **Je höher die Interoperabilität, weniger Funktionen.** Die Anwendung löscht die Funktionen jedoch weitere DBMS verwendet.  
  
-   **Höhere Interoperabilität optionalen Features.** Die Anwendung schließt die Funktionen, jedoch werden sie nur mit diesen DBMS-Systeme, die sie unterstützen verfügbar gemacht.  
  
-   **Höhere Interoperabilität, weitere Funktionen.** Die Anwendung verwendet die Funktionen mit DBMS-Systeme, die sie unterstützen, und diese für DBMS-Systeme, die nicht emuliert.  
  
 Die ersten beiden Fälle sind relativ einfach zu implementieren, da die Funktionen mit allen unterstützten DBMS oder none verwendet werden. Die letzten beiden Fälle sind hingegen, komplexer. Es ist erforderlich, in beiden Fällen zu überprüfen, ob das DBMS die Funktionen unterstützt und im zweiten Fall schreiben Sie eine potenziell große Menge an Code, um diese Funktionen zu emulieren. Diese Schemas wird daher wahrscheinlich, dass weitere Entwicklungszeit erfordern und zur Laufzeit möglicherweise langsamer.  
  
 Erwägen Sie eine Standardabfrage-Anwendung, die eine Verbindung mit einer einzelnen Datenquelle herstellen kann. Die Anwendung akzeptiert eine Abfrage des Benutzers und die Ergebnisse in einem Fenster angezeigt. Jetzt nehmen diese Anwendung verfügt über eine Funktion, die Benutzern ermöglicht, die Ergebnisse anzuzeigen abgefragt, mehrere gleichzeitig. D. h. können sie Ausführen einer Abfrage und sehen Sie sich einige der Ergebnisse, führen Sie eine andere Abfrage sehen Sie sich einige der Ergebnisse und fahren Sie dann mit der ersten Abfrage. Dies stellt Interoperabilitätsfehler im Zusammenhang, da einige Treiber nur eine einzige aktive Anweisung unterstützt.  
  
 Die Anwendung bietet eine Reihe von Möglichkeiten zur Verfügung, die basierend auf was der Treiber für die Option SQL_MAX_CONCURRENT_ACTIVITIES in gibt **SQLGetInfo**:  
  
-   **Immer unterstützen Sie mehrere Abfragen.** Nach dem Herstellen einer Verbindung, um einen Treiber, überprüft die Anwendung die Anzahl der aktiven Anweisungen. Wenn der Treiber nur eine aktive Anweisung unterstützt, wird die Anwendung schließt die Verbindung und der Benutzer darüber informiert, dass der Treiber nicht die erforderlichen Funktionen unterstützt. Die Anwendung ist einfach zu implementieren und verfügt über sämtliche Funktionen jedoch niedriger Interoperabilität hat.  
  
-   **Unterstützen Sie niemals mehrere Abfragen.** Das Feature wird von die Anwendung vollständig löscht. Es ist einfach zu implementieren und hat hohe Interoperabilität weist aber weniger Funktionen.  
  
-   **Unterstützen Sie mehrere Abfragen nur, wenn der Treiber der Fall ist.** Nach dem Herstellen einer Verbindung, um einen Treiber, überprüft die Anwendung die Anzahl der aktiven Anweisungen. Die Anwendung kann der Benutzer eine neue Anweisung gestartet wird, wenn bereits einer nur aktiviert, wenn der Treiber mehrere aktive Anweisungen unterstützt. Die Anwendung verfügt über höhere Funktionalität und Interoperabilität, jedoch ist schwieriger zu implementieren.  
  
-   **Immer unterstützen Sie mehrere Abfragen zu und zu emulieren Sie, sie bei Bedarf.** Nach dem Herstellen einer Verbindung, um einen Treiber, überprüft die Anwendung die Anzahl der aktiven Anweisungen. Die Anwendung immer ermöglicht dem Benutzer eine neue Anweisung zu starten, wenn eine bereits aktiv ist. Wenn der Treiber nur eine aktive Anweisung unterstützt, wird die Anwendung wird eine zusätzliche Verbindung zu diesen Treiber geöffnet, und die neue Anweisung für diese Verbindung ausgeführt. Die Anwendung verfügt über sämtliche Funktionen und hohe Interoperabilität, jedoch ist schwieriger zu implementieren.


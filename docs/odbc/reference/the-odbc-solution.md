---
title: "Der ODBC-Lösung | Microsoft Docs"
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
- ODBC [ODBC], database access
- SQL [ODBC], database access
- database access [ODBC]
- standardizing database access [ODBC], using ODBC
ms.assetid: 34b80790-e010-4b90-8eaa-03189f5d8986
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c7288fcb9fad7b2567f7fec16cf0f407b2f6b2e4
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="the-odbc-solution"></a>Der ODBC-Lösung
Klicken Sie dann die Frage ist, wie ODBC Datenbankzugriff standardisieren? Es gibt zwei architektonische Anforderungen:  
  
-   Anwendungen müssen mehrere DBMS-Systeme, die mit dem gleichen Quellcode ohne Neukompilierung oder erneute zugreifen können.  
  
-   Anwendungen müssen mehrere DBMS gleichzeitig zugreifen können.  
  
 Und es ist eine weitere Frage aufgrund von Marketplace-Reality-Modus:  
  
-   Die DBMS-Funktionen sollten ODBC verfügbar machen? Nur Funktionen, die häufig bei allen DBMS oder eine beliebige Funktion, die in jeder DBMS verfügbar ist?  
  
 ODBC löst diese Probleme auf folgende Weise:  
  
-   **ODBC ist ein Call-Level-Interface.** Zur Lösung des Problems wie Anwendungen mehrere DBMS-Systeme, die mit dem gleichen Quellcode zugreifen, werden in ODBC eine standard-CLI definiert. Dieser Knoten enthält alle Funktionen der CLI-Spezifikationen von Open Group und ISO/IEC und bietet zusätzliche Funktionen, die häufig von Anwendungen benötigt werden.  
  
     Einer anderen Bibliothek oder einem Treiber verwenden, muss für jede DBMS, die ODBC unterstützt. Der Treiber implementiert die Funktionen der ODBC-API. Um einen anderen Treiber zu verwenden, muss die Anwendung nicht neu kompiliert oder neu verknüpft werden. Die Anwendung wird stattdessen einfach wird der neue Treiber geladen, und der Ruft die Funktionen in diese. Um mehrere DBMS gleichzeitig zugreifen zu können, lädt die Anwendung mehrere Treiber. Unterstützung von Treibern ist betriebssystemspezifischen. Beispielsweise sind die Treiber auf dem Betriebssystem Microsoft® Windows® Dynamic Link Libraries (DLLs).  
  
-   **ODBC definiert eine standard-SQL-Grammatik.** Zusätzlich zu einer standard Call-Level-Interface definiert ODBC eine standard-SQL-Grammatik. Diese Grammatik basiert auf der Open Group SQL CAE-Spezifikation. Unterschiede zwischen den zwei Grammatiken sind kleinere und aufgrund der Unterschiede zwischen der SQL-Grammatik vorgeschriebene in erster Linie die embedded SQL (Open Group) und eine CLI (ODBC). Es gibt auch einige Erweiterungen der Grammatik üblicherweise verfügbar Sprachfunktionen, die nicht von der Open Group-Grammatik abgedeckt verfügbar zu machen.  
  
     Anwendungen können mithilfe von ODBC oder DBMS-spezifische Grammatik Anweisungen senden. Wenn eine Anweisung ODBC-Grammatik, die vom DBMS-spezifische Grammatik unterscheidet verwendet, konvertiert der Treiber es vor dem Senden an die Datenquelle an. Solche Konvertierungen sind jedoch selten, da die meisten DBMS nutzen bereits die standardmäßige SQL-Grammatik.  
  
-   **ODBC stellt eine Treiber-Manager zum Verwalten der gleichzeitige Zugriff auf mehrere DBMS bereit.** Obwohl die Verwendung der Treiber das Problem des Zugriffs auf mehrere DBMS gleichzeitig gelöst hat, kann der Code dazu komplex sein. Anwendungen, die darauf ausgelegt sind, arbeiten alle Treiber können nicht statisch mit keine Treiber verknüpft werden. Sie müssen stattdessen Treiber zur Laufzeit laden und rufen Sie die Funktionen in diesen über eine Tabelle mit Funktionszeiger. Die Situation wird komplexer, wenn die Anwendung mehrere Treiber gleichzeitig verwendet werden.  
  
     Jede Anwendung zu diesem Zweck bietet,-ODBC-Treiber-Manager. Der Treiber-Manager implementiert alle ODBC-Funktionen – meistens als Pass-Through-Aufrufe an ODBC-Treiber Funktionen – und statisch mit der Anwendung verknüpft oder von der Anwendung zur Laufzeit geladen wird. Daher ruft die Anwendung ODBC-Funktionen, namentlich in der Treiber-Manager anstatt von Zeiger in jeder Treiber.  
  
     Wenn eine Anwendung einen bestimmten Treiber benötigt, fordert er zuerst ein Verbindungshandle zur Identifizierung der Treiber ein, und fordert an, dass der Treiber-Manager die Treiber zu laden. Der Treiber-Manager wird der Treiber geladen und speichert die Adresse für jede Funktion im Treiber. Zum Aufrufen einer ODBC-Funktion in der Treiber die Anwendung ruft diese Funktion in der Treiber-Manager und das Verbindungshandle für den Treiber übergeben. Der Treiber-Manager ruft dann die Funktion mithilfe der Adresse, die sie zuvor gespeichert.  
  
-   **ODBC macht eine Vielzahl von DBMS-Funktionen, aber keine Treiber zur Unterstützung von allen erforderlich.** Wenn ODBC nur Funktionen verfügbar, die auf allen DBMS gemeinsam verwendet werden gemacht, wäre es wenig; Nachdem alle ist der Grund so viele unterschiedliche DBMS heute vorhanden, dass sie verschiedene Funktionen aufweisen. Wenn ODBC jede Funktion verfügbar, die in jeder DBMS verfügbar ist gemacht, wäre es unmöglich Treiber zu implementieren.  
  
     Stattdessen ODBC macht eine Vielzahl von Funktionen – mehr als die von den meisten DBMS unterstützt werden, jedoch erfordern Treiber, um nur eine Teilmenge dieser Funktionen zu implementieren. Treiber implementieren die übrigen Funktionen nur, wenn sie von der zugrunde liegenden DBMS unterstützt werden, oder wenn sie sie emulieren möchten. Folglich können Anwendungen geschrieben werden, um die Funktionen von einer einzelnen DBMS auszunutzen, zur Verfügung gestellt, durch den Treiber für dieses DBMS, verwenden Sie nur die Funktionen, die von allen DBMS verwendet oder das für die Unterstützung einer bestimmten Funktion überprüfen und entsprechend reagieren.  
  
     Damit eine Anwendung bestimmen kann, welche Treiber features und DBMS unterstützt ODBC bietet zwei Funktionen (**SQLGetInfo** und **SQLGetFunctions**), die allgemeine Informationen über die Treiber und DBMS zurückgeben Funktionen und eine Liste der Funktionen der Treiber unterstützt. ODBC definiert auch die API und SQL-Grammatik Übereinstimmungsebenen, die allgemeine Bereiche vom Treiber unterstützten Funktionen angeben. Weitere Informationen finden Sie unter [Übereinstimmungsebenen](../../odbc/reference/develop-app/conformance-levels.md).  
  
     Es ist wichtig zu beachten, dass ODBC eine allgemeine Schnittstelle für alle Funktionen definiert, die sie verfügbar macht. Aus diesem Grund Anwendungen featurespezifische Code enthalten, nicht von DBMS-spezifischen Code, und alle Treiber, die die Features verfügbar machen können. Ein Vorteil besteht darin, dass Anwendungen müssen nicht aktualisiert werden, wenn die von einem DBMS unterstützten Funktionen erweitert werden; Stattdessen, wenn ein aktualisierter Treiber installiert ist, verwendet die Anwendung automatisch die Funktionen des Codes ist featurespezifische, nicht treiberspezifische oder DBMS-spezifische.


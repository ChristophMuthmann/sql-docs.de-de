---
title: Statusübergänge | Microsoft Docs
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
ms.topic: article
helpviewer_keywords:
- state transitions [ODBC]
- unallocated state [ODBC]
- handles [ODBC], state transitions
- allocated state [ODBC]
- connection state [ODBC]
ms.assetid: fc741611-6535-43cc-8156-6d897d04664e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c94806fae462803c3323c3e3c5768751e53a5467
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="state-transitions"></a>Statusübergänge
ODBC definiert diskrete *Zustände* für jede Umgebung, jede Verbindung und jede Anweisung. Die Umgebung verfügt beispielsweise über drei mögliche Zustände: verfügbaren (in dem keine Umgebung zugeordnet ist), zugewiesenem (in der eine Umgebung erhält jedoch keine Verbindungen zugeordnet sind) und die Verbindung (in der Umgebung und eine oder mehrere Verbindungen sind reserviert). Verbindungen werden sieben mögliche Zustände aufweisen; -Anweisungen verfügen über 13 mögliche Zustände.  
  
 Ein bestimmtes Element verschiebt, das durch das Handle von einem Zustand, wenn die Anwendung eine bestimmte Funktion oder Funktionen aufruft, und das Handle für dieses Element übergibt. Diese Bewegung wird aufgerufen, eine *Status Übergang*. Z. B. Zuordnen eines Umgebungshandles mit **SQLAllocHandle** verschiebt Sie die Umgebung aus nicht zugeordnet, in der zugeordneten und zum Freigeben dieses Handle mit **SQLFreeHandle** wird zugeordnet zu zurückgegeben Nicht zugeordnet. ODBC definiert eine begrenzte Anzahl von zulässigen Zustand übergeht, die eine andere Möglichkeit, die besagt, dass Funktionen in einer bestimmten Reihenfolge aufgerufen werden müssen.  
  
 Einige Funktionen wie **SQLGetConnectAttr**, haben keinen Einfluss auf Status an. Andere Funktionen wirken sich auf den Status eines einzelnen Elements aus. Beispielsweise **SQLDisconnect** eine Verbindung vom Zustand "Verbindung" in den zugeordneten Zustand wechselt. Einige Funktionen beeinflussen schließlich den Status der mehr als ein Element. Z. B. Zuordnen eines Verbindungshandles mit **SQLAllocHandle** bewegt sich eine Verbindung aus einer nicht zugeordnet zu einem zugeordneten Status und die Umgebung aus einem zugeordneten zum Zustand "Verbindung".  
  
 Wenn eine Anwendung eine Funktion außerhalb der Reihenfolge aufruft, gibt die Funktion eine *Status Übergang Fehler*. Wenn eine Umgebung in einen Zustand der Verbindung und die Anwendung ist beispielsweise Aufrufe **SQLFreeHandle** mit diesem Umgebungshandle **SQLFreeHandle** SQLSTATE HY010 zurückgibt (Sequenzfehler-Funktion), Da es aufgerufen werden kann nur verwendet werden, wenn die Umgebung im Zustand zugeordnet ist. Durch die Definition dieses als einen ungültigen Statusübergang, hindert ODBC-die Anwendung aus die Umgebung freigeben, während aktive Verbindungen vorhanden sind.  
  
 Einige Statusübergänge sind Multithreaddesigns die von ODBC. Beispielsweise ist es nicht möglich, ein Verbindungshandle zuordnen ohne erste ein Umgebungshandle zuzuordnen, da die Funktion, die ein Verbindungshandle ordnet ein Umgebungshandle erforderlich ist. Andere Statusübergänge werden durch den Treiber-Manager und die Treiber erzwungen. Beispielsweise **SQLExecute** führt eine vorbereitete Anweisung. Wenn das Anweisungshandle übergeben es ist nicht in einem Status ' vorbereitet ', **SQLExecute** SQLSTATE HY010 zurückgibt (Sequenzfehler-Funktion).  
  
 Aus Sicht der Anwendung Statusübergänge sind in der Regel einfach: rechtliche Statusübergänge tendenziell als Hand in Hand wechseln mit den Fluss einer gut geschriebene Anwendung. Statusübergänge sind komplexer für den Treiber-Manager und die Treiber, da sie den Status der Umgebung, jede Verbindung und jede Anweisung nachverfolgen müssen. Größte Teil dieser Arbeit erfolgt vom Treiber-Manager; Die meisten Aufgaben, die vom Treiber ausgeführt werden müssen, tritt bei-Anweisungen mit noch Ergebnisse ausstehen.  
  
 Teil 1 und 2 dieses Handbuchs ("Einführung in ODBC" und "Entwickeln von Anwendungen und-Treiber") eher nicht explizit Statusübergänge erwähnen. Stattdessen beschreiben sie die Reihenfolge, in der Funktionen aufgerufen werden müssen. "Ausführen von Anweisungen" gibt z. B. an, dass eine Anweisung vorbereitet sein muss, mit **SQLPrepare** , bevor sie mit ausgeführt werden kann **SQLExecute**. Eine vollständige Beschreibung der Zustände und Zustandsübergänge, z. B. die Übergänge vom Treiber-Manager überprüft werden und die durch Treiber, geprüft werden muss finden Sie unter [Anhang B: ODBC-Übergang-Statustabellen](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).

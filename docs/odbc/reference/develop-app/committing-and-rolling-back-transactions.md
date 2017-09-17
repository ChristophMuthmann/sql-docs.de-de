---
title: "Ausführen von Commits oder Rollbacks für Transaktionen | Microsoft Docs"
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
- rolling back transactions [ODBC]
- committing transactions [ODBC]
- transactions [ODBC], rolling back
- transactions [ODBC], committing
ms.assetid: 800f2c1a-6f79-4ed1-830b-aa1a62ff5165
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4090e609063b74fdcbef694c400272ee6af090c5
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="committing-and-rolling-back-transactions"></a>Ausführen von Commits oder Rollbacks von Transaktionen
Um einen commit oder Rollback einer Transaktions im Manualcommit Modus, eine Anwendung ruft **SQLEndTran**. Treiber für DBMS-Systeme, die Transaktionen, in der Regel unterstützen implementieren Sie diese Funktion durch das Ausführen einer **COMMIT** oder **ROLLBACK** Anweisung. Der Treiber-Manager nicht aufgerufen **SQLEndTran** die Verbindung im Autocommit-Modus ist einfach zurückgibt, wenn SQL_SUCCESS zurück, selbst wenn die Anwendung versucht, ein Rollback der Transaktion auszuführen. Da die Treiber für DBMS-Systeme, die keine Transaktionen unterstützen immer im Autocommit Modus sind, können sie entweder implementieren **SQLEndTran** SQL_SUCCESS zurück, ohne jegliche oder überhaupt nicht implementiert.  
  
> [!NOTE]  
>  Anwendungen sollten nicht einen commit oder Rollback für Transaktionen aus, durch das Ausführen **COMMIT** oder **ROLLBACK** -Anweisungen mit **SQLExecute** oder **SQLExecDirect**. Die Auswirkungen auf diese Weise sind nicht definiert. Mögliche Probleme umfassen den Treiber nicht mehr zu wissen, wann eine Transaktion aktiv ist und diese Anweisungen für Datenquellen, die keine Transaktionen unterstützen fehlschlagen. Diese Anwendungen sollten Aufrufen **SQLEndTran** stattdessen.  
  
 Wenn eine Anwendung, um das Umgebungshandle übergibt **SQLEndTran** aber grundsätzlich nicht bestanden ein Verbindungshandle der Treiber-Manager ruft **SQLEndTran** mit das Umgebungshandle für jeden Treiber, verfügt über eine oder mehrere aktive Verbindungen in der Umgebung. Der Treiber führt dann einen Commit für die Transaktionen für jede Verbindung in der Umgebung. Allerdings ist es wichtig zu verstehen, dass der Treiber weder der Treiber-Manager auf den Verbindungen in der Umgebung ein Zweiphasencommits führt; Dies ist lediglich eine Vereinfachung der Programmierung gleichzeitig aufrufen **SQLEndTran** für alle Verbindungen in der Umgebung.  
  
 (Ein *Zweiphasen-Commit* wird in der Regel verwendet werden, um ein commit für Transaktionen, die über mehrere Datenquellen verteilt werden. In der ersten Phase werden die Datenquellen abgerufen, um gibt an, ob sie ihren Teil der Transaktion verpflichten können. In der zweiten Phase wird die Transaktion bei all denjenigen Datenquellen tatsächlich ausgeführt. Wenn alle Datenquellen in der ersten Phase Antwort erhalten, dass sie die Transaktion kein commit möglich ist, erfolgt die zweite Phase nicht.)

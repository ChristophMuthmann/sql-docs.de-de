---
title: Auswirkungen von Transaktionen auf Cursor und vorbereitete Anweisungen | Microsoft Docs
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
- cursors [ODBC], transaction commits or roll backs
- prepared statements [ODBC]
- transactions [ODBC], cursors
ms.assetid: 523e22a2-7b53-4c25-97c1-ef0284aec76e
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2533778f9b0e837ce59850d4f70a3c4545f8be60
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="effect-of-transactions-on-cursors-and-prepared-statements"></a>Auswirkungen von Transaktionen auf Cursor und vorbereitete Anweisungen
Ein Commit oder Rollback wurde eine Transaktion folgende Auswirkungen auf den Cursor und Access-Pläne:  
  
-   Alle Cursor geschlossen sind, und Access-Pläne für vorbereitete Anweisungen für diese Verbindung gelöscht werden.  
  
-   Alle Cursor geschlossen sind, und Access-Pläne für vorbereitete Anweisungen für diese Verbindung jedoch intakt bleiben.  
  
-   Bleiben alle Cursor geöffnet, und Access-Pläne für vorbereitete Anweisungen für diese Verbindung jedoch intakt bleiben.  
  
 Nehmen Sie z. B. an, dass eine Datenquelle die erste Verhalten in dieser Liste die restriktivste diese Verhaltensweisen. Jetzt angenommen, eine Anwendung, die wie folgt vorgeht:  
  
1.  Legt den Commit-Modus auf Manualcommit-fest.  
  
2.  Erstellt ein Resultset von Verkaufsaufträgen in 1-Anweisung.  
  
3.  Erstellt ein Resultset Zeilen in einem Verkaufsauftrag in 2-Anweisung an, wenn der Benutzer diese Reihenfolge hervorhebt.  
  
4.  Aufrufe **SQLExecute** eine positioniertes Update-Anweisung, die vorbereitet wurde auf 3-Anweisung ausgeführt wird, wenn der Benutzer eine Zeile aktualisiert.  
  
5.  Aufrufe **SQLEndTran** die positionierte Update-Anweisung übergeben.  
  
 Aufgrund der Datenquelle Verhaltens der Aufruf von **SQLEndTran** in Schritt 5 bewirkt, dass Cursor bei 1 und 2-Anweisungen schließen und die Zugriffsplan für alle Anweisungen löschen. Die Anwendung muss Ausgangsstellung legt Anweisungen 1 und 2, um das Ergebnis neu zu erstellen und die Anweisung für Anweisung 3 reprepare.  
  
 Im Autocommit Modus, Funktionen außer **SQLEndTran** commit der Transaktionen:  
  
-   **SQLExecute** oder **SQLExecDirect** im vorherigen Beispiel der Aufruf von **SQLExecute** in Schritt 4 führt einen Commit für eine Transaktion. Dies bewirkt, dass die Datenquelle zum Schließen der Cursor bei 1 und 2-Anweisungen und die Zugriffsplan für alle Anweisungen für diese Verbindung löschen.  
  
-   **SQLBulkOperations** oder **SQLSetPos** im vorherigen Beispiel nehmen wir an, dass die in Schritt 4 die Anwendung aufruft, **SQLSetPos** mit der Option SQL_UPDATE auf 2-Anweisung anstelle der Ausführung ein positioniertes Update-Anweisung für Anweisung 3. Dies führt einen Commit für eine Transaktion und führt dazu, dass die Datenquelle, um den Cursor auf 1 und 2-Anweisungen zu schließen, und verwirft alle Access-Pläne für diese Verbindung.  
  
-   **SQLCloseCursor** im vorherigen Beispiel nehmen wir an, wenn der Benutzer auf einen anderen Auftrag hervorhebt, die Anwendung ruft **SQLCloseCursor** auf Anweisung 2 vor dem Erstellen ein Ergebnis der Linien für die neue Umsätze Reihenfolge. Der Aufruf von **SQLCloseCursor** führt einen Commit für die **wählen** -Anweisung, die das Resultset Zeilen erstellt und bewirkt, dass die Datenquelle zum Schließen des Cursors in 1-Anweisung dann verwirft alle Zugriffspläne auf, Verbindung.  
  
 Anwendungen, vor allem Bildschirm basierende Anwendungen in der der Benutzer einen Bildlauf durchführt, um das Resultset und Updates oder löscht Zeilen, muss Sie vorsichtig, um Code, um dieses Verhalten.  
  
 Um zu bestimmen, wie eine Datenquelle verhält, wenn eine Transaktion ein Commit oder Rollback ist, eine Anwendung ruft **SQLGetInfo** mit den Optionen SQL_CURSOR_COMMIT_BEHAVIOR und SQL_CURSOR_ROLLBACK_BEHAVIOR.

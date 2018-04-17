---
title: Cursors | Microsoft-Dokumentation
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
- forward-only cursors [ODBC]
- scrollable cursors [ODBC]
- cursors [ODBC], about cursors
- cursors [ODBC]
- fetches [ODBC], cursors
- result sets [ODBC], fetching
- block cursors [ODBC]
ms.assetid: 0b114352-3c63-4d33-9220-182ede90e4aa
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c0c6ae5b9bda276bcd1296fcb475063fea6db204
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="cursors"></a>Cursor
Eine Anwendung ruft die Daten mit einem *Cursor*. Ein Cursor unterscheidet sich von einem Resultset: ein Resultset ist der Satz von Zeilen, die bestimmten Suchkriterien entspricht, während ein Cursors auf die Software ist, die diese Zeilen an die Anwendung wird zurückgegeben. Der Name *Cursor* anwenden auf Datenbanken, sollten Sie wahrscheinlich die blinkender Cursor auf einem Computer terminal stammt. Ebenso wie diesem Cursor gibt an, die aktuelle Position auf dem Bildschirm und, wo die typisierte Wörter weiter angezeigt wird, gibt einen Cursor für ein Resultset der aktuellen Position im Resultset und welche Zeile als Nächstes zurückgegeben werden an.  
  
 Das Cursormodell in ODBC basiert auf das Cursormodell in embedded SQL. Ein deutlicher Unterschied zwischen diesen Modellen ist, dass die Möglichkeit Cursor geöffnet werden. In embedded SQL muss ein Cursor explizit deklariert und geöffnet werden, bevor er verwendet werden kann. In ODBC ist ein Cursor implizit geöffnet, wenn eine Anweisung, die ein Resultset erstellt ausgeführt wird. Wenn der Cursor geöffnet wird, wird er vor der ersten Zeile des Resultsets positioniert. In eingebetteten SQL- und ODBC muss ein Cursor geschlossen werden, nach die Anwendung verwenden.  
  
 Verschiedene Cursors haben unterschiedliche Eigenschaften. Die am häufigsten verwendete Typ der Cursor, der aufgerufen wird, eine *Vorwärtscursor,* können über das Resultset nur vorwärts bewegen. Um zu einer vorherigen Zeile zurückzugeben, die Anwendung schließen und erneut öffnen des Cursors und liest dann Zeilen vom Anfang des Resultsets, bis die erforderlichen Zeile erreicht. Vorwärtscursor bieten einen schnelle Mechanismus für ein Pass-through ein Resultset.  
  
 Vorwärtscursor sind weniger hilfreich für Bildschirm basierende Anwendungen, in denen rückwärts Bildlauf und durch die Daten weiterleiten. Solche Anwendungen können einen Vorwärtscursor verwenden, lesen Sie das Resultset, sobald die Daten lokal zwischenspeichern und Durchführen eines Bildlaufs selbst ausführen. Dies funktioniert jedoch nur mit kleinen Datenmengen. Eine bessere Lösung ist die Verwendung einer *bildlauffähigen Cursor* dem ermöglicht den wahlfreien Zugriff auf das Resultset. Solche Anwendungen können auch die Leistung steigern durch Abrufen von mehr als eine Zeile mit Daten zu einem Zeitpunkt mit den so genannten eine *Blockcursor.* Weitere Informationen zu Blockcursor, finden Sie unter [Verwenden von Blockcursorn](../../../odbc/reference/develop-app/using-block-cursors.md).  
  
 Die Vorwärtscursor ist der Standardcursortyp in ODBC und wird in den folgenden Abschnitten erläutert. Weitere Informationen zu Blockcursor und bildlauffähigen Cursorn finden Sie unter [Blockcursor](../../../odbc/reference/develop-app/block-cursors.md) und [bildlauffähige Cursor](../../../odbc/reference/develop-app/scrollable-cursors.md).  
  
> [!IMPORTANT]  
>  Ein Commit oder Rollback einer Transaktion, entweder durch explizites Aufrufen **SQLEndTran** oder durch im Autocommit-Modus ausgeführt wird, bewirkt, dass einige Datenquellen zu allen Cursorn für alle Anweisungen für eine Verbindung zu schließen. Weitere Informationen finden Sie unter der SQL_CURSOR_COMMIT_BEHAVIOR und SQL_CURSOR_ROLLBACK_BEHAVIOR Attribute in der [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) funktionsbeschreibung.

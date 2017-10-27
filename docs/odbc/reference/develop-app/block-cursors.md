---
title: Blockieren von Cursorn | Microsoft Docs
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
- cursors [ODBC], block
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 1a92b5d8-7c6e-4ce5-8c99-600a387026aa
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7747f421fe4a7356086cf27ecf62739f34acdd17
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="block-cursors"></a>Blockcursor
Viele Anwendungen verbringen sehr viel Zeit, die Daten über das Netzwerk eingebunden. Teil dieser Zeit wird aufgewendet, die Daten tatsächlich über das Netzwerk eingebunden und Teil davon ist für die netzwerkbelastung, z. B. des Aufrufs durch den Treiber auf eine Zeile mit Daten anfordern aufgewendet. Das zweite Mal kann reduziert werden, wenn die Anwendung effizient verwendet *Block,* oder *Fat,* *Cursor,* der kann mehr als eine Zeile zurückgeben, zu einem Zeitpunkt.  
  
 Eine Anwendung immer bietet die Möglichkeit der Verwendung eines Blockcursors. Für Datenquellen, die von denen jeweils nur eine Zeile abgerufen werden kann, müssen die Blockcursor im Treiber simuliert werden. Dies kann durch Ausführen von mehreren einzeiliges Abrufvorgänge erfolgen. Obgleich dies wahrscheinlich keine leistungsverbesserungen ist, wird er Verkaufschancen für Anwendungen geöffnet. Solche Anwendungen treten dann Leistungssteigerungen wie DBMS Blockcursor systemintern implementieren und die Treiber diese DBMS zugeordneten verfügbar werden gemacht.  
  
 In einer einzelnen FETCH-Anweisung mit einem Blockcursor zurückgegebenen Zeilen heißen die *Rowset*. Es ist wichtig, nicht zu verwechseln Sie das Rowset mit dem Resultset. Das Resultset wird in der Datenquelle beibehalten, während das Rowset Anwendungspuffer beibehalten wird. Während das Resultset behoben ist, wird das Rowset nicht ist – er ändert seine Position und den Inhalt jedes Mal ein neuer Satz von Zeilen wird abgerufen. Ebenso wie z. B. der herkömmlichen SQL-Vorwärtscursor, verweist auf eine aktuelle Zeile eines Cursors einzeiliges ein Blockcursors verweist, auf das Rowset als vorstellen kann *aktuelle Zeilen*.  
  
 Um die Vorgänge, die Vorgänge für eine einzelne Zeile, wenn mehrere Zeilen abgerufen wurden, muss die Anwendung zuerst angeben, welcher Zeile die aktuelle Zeile ist. Die aktuelle Zeile ist erforderlich, durch Aufrufe von **SQLGetData** und positioniert Update und delete-Anweisungen. Wenn ein Blockcursors ein Rowset zuerst zurückgegeben wird, ist die aktuelle Zeile der ersten Zeile des Rowsets. So ändern Sie die aktuelle Zeile, die Anwendung ruft **SQLSetPos** oder **SQLBulkOperations** (zum Aktualisieren von Lesezeichen). Die folgende Abbildung zeigt die Beziehung zwischen dem Resultset, Rowset parallelitätszeile, Rowset Cursor und Blockcursor. Weitere Informationen finden Sie unter [Verwenden von Blockcursorn](../../../odbc/reference/develop-app/using-block-cursors.md)weiter unten in diesem Abschnitt und [positioniert Update- und Delete-Anweisungen](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md) und [Aktualisieren von Daten mit SQLSetPos](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md).  
  
 ![Abrufen des nächsten, vor der ersten und letzten Rowsets](../../../odbc/reference/develop-app/media/pr20_2.gif "pr20_2")  
  
 Ob ein Cursor einem Blockcursor ist ist unabhängig von, ob es bildlauffähig ist. Z. B. die meiste Arbeit in einer Anwendung Berichts aufgewendet abrufen und Drucken von Zeilen. Aus diesem Grund wird es am schnellsten arbeiten mit einem Vorwärtscursor, Blockcursor. Ein Vorwärtscursor verwendet, um die Ausgaben für einen bildlauffähigen Cursor und eines Blockcursors reduziert den Netzwerkdatenverkehr zu vermeiden.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Binden von Spalten für die Verwendung mit Blockcursor](../../../odbc/reference/develop-app/binding-columns-for-use-with-block-cursors.md)  
  
-   [Verwenden von Blockcursorn](../../../odbc/reference/develop-app/using-block-cursors.md)  
  
-   [Zeilenstatusarray](../../../odbc/reference/develop-app/row-status-array.md)


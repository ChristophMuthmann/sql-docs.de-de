---
title: ODBC-Cursorn | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cursors [ODBC], dynamic
- dynamic cursors [ODBC]
ms.assetid: de709fd3-9eb2-44e1-a2f0-786e2b9602a6
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e0d82da741babc168ce305ed8134d8f44f682f57
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="odbc-dynamic-cursors"></a>ODBC-Cursorn
Ein dynamischer Cursor handelt es sich um: dynamische. Sie können erkennen, dass alle Änderungen an der Mitgliedschaft, Reihenfolge und Werte des Resultsets nach dem Öffnen des Cursors. Nehmen wir beispielsweise an ein dynamischer Cursor ruft zwei Zeilen ab, und eine andere Anwendung klicken Sie dann eine dieser Zeilen aktualisiert und löscht die andere. Wenn der dynamische Cursor dann versucht, diese Zeilen erneut abzurufen, wird die gelöschte Zeile nicht gefunden, aber die neuen Werte für die aktualisierte Zeile zurück.  
  
 Dynamische Cursor erkennen alle Updates, löscht und eingefügt wurden, sowohl ihre eigenen und die durch andere Benutzer. (Dies unterliegt die Isolation Level der Transaktion, wie durch das Verbindungsattribut SQL_ATTR_TXN_ISOLATION festgelegt.) Der zeilenstatusarray SQL_ATTR_ROW_STATUS_PTR-Anweisungsattribut gemäß gibt diese Änderungen und SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO, SQL_ROW_ERROR, SQL_ROW_UPDATED und SQL_ROW_ADDED enthalten. Es kann nicht SQL_ROW_DELETED zurückgegeben, da ein dynamisches Cursors gelöschte Zeilen, die außerhalb des Rowsets nicht wieder und daher nicht mehr das Vorhandensein von die gelöschte Zeile im Resultset oder das entsprechende Element in der zeilenstatusarray erkennt. SQL_ROW_ADDED wird nur zurückgegeben, wenn eine Zeile, durch den Aufruf von aktualisiert wird **SQLSetPos**, nicht verwendet werden, wenn sie von einem anderen Cursor aktualisiert wird.  
  
 Eine Möglichkeit zum Implementieren von dynamischer Cursors in der Datenbank wird durch Erstellen eines selektiven Indexes, das die Mitgliedschaft definiert und die Sortierung des Resultsets festgelegt. Da der Index aktualisiert werden, wenn andere Änderungen vornehmen, ist ein Cursor, die basierend auf solchen Index für alle Änderungen. Zusätzliche Auswahl des Resultsets, die von diesem Index definiert ist möglich, durch die Verarbeitung entlang des Indexes.  
  
 Dynamische Cursor können durch das Anfordern des Resultsets einen eindeutigen Schlüssel geordnet werden simuliert werden. Mit einer Einschränkung erfolgen Abrufvorgänge durch Ausführen einer **wählen** Anweisung jedes Mal der Cursor ruft Zeilen ab. Nehmen wir beispielsweise an das Resultset von dieser Anweisung definiert ist:  
  
```  
SELECT * FROM Customers ORDER BY Name, CustID  
```  
  
 Zum Abrufen des nächsten Rowsets in diesem Resultset legt der simulierte Cursor für die Parameter in der folgenden **wählen** Anweisung, um die Werte in der letzten Zeile des aktuellen Rowsets und führt dann diesen:  
  
```  
SELECT * FROM Customers WHERE (Name > ?) AND (CustID > ?)  
   ORDER BY Name, CustID  
```  
  
 Diese Anweisung erstellt ein zweites Resultset, von denen das erste Rowset das nächste Rowset im ursprünglichen Resultset wird – in diesem Fall wird der Satz von Zeilen in der Customers-Tabelle. Dieses Rowset wird von der Cursor an die Anwendung zurückgegeben.  
  
 Es ist interessant, beachten, dass ein dynamischer Cursor, die auf diese Weise implementiert viele Resultsets, tatsächlich erstellt, wodurch es zu Änderungen an der ursprünglichen Resultset zu erkennen. Die Anwendung nie erfährt, dass diese zusätzlichen Resultsets vorhanden ist; Er wird einfach angezeigt, als ob der Cursor kann Änderungen an der ursprünglichen Resultset zu erkennen ist.

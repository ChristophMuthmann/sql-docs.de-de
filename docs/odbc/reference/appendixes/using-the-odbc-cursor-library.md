---
title: Der ODBC-Cursorbibliothek mit | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], using cursor library
- cursor library [ODBC], using cursor library
ms.assetid: 9653f2f8-ccfc-4220-99ef-601dc0fa641c
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b9a5e1a11b5e8ba12308aaed342d6cf30e688e56
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="using-the-odbc-cursor-library"></a>Mithilfe der ODBC-Cursorbibliothek
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen und Planen von Anwendungen zu ändern, die dieses Feature verwenden. Microsoft empfiehlt die Verwendung der Cursorfunktionalität der Treiber.  
  
 So verwenden Sie die ODBC-Cursorbibliothek, eine Anwendung:  
  
1.  Aufrufe **SQLSetConnectAttr** mit einem *Attribut* des SQL_ATTR_ODBC_CURSORS angeben, wie die Cursorbibliothek mit einer bestimmten Verbindung verwendet werden soll. Die Cursorbibliothek kann immer (SQL_CUR_USE_ODBC) verwendet, nur, wenn Sie Treiber bildlauffähige Cursor (SQL_CUR_USE_IF_NEEDED) nicht unterstützt wird, oder nie verwendet (SQL_CUR_USE_DRIVER).  
  
2.  Aufrufe **SQLConnect**, **SQLDriverConnect**, oder **SQLBrowseConnect** für die Verbindung mit der Datenquelle.  
  
3.  Aufrufe **SQLSetStmtAttr** um den Cursortyp (SQL_ATTR_CURSOR_TYPE), die Parallelität (SQL_ATTR_CONCURRENCY) und die Rowsetgröße (SQL_ATTR_ROW_ARRAY_SIZE) anzugeben. Die Cursorbibliothek unterstützt Vorwärtscursor und statische Cursor. Vorwärtscursor müssen schreibgeschützt sein, während der statische Cursor können schreibgeschützt sein oder können Steuerung durch vollständige Parallelität, die Werte verglichen.  
  
4.  Weist einen oder mehrere Rowsets Puffer und Aufrufe **SQLBindCol** ein- oder mehrmals, um diesen Puffern zu Spalten führt zu binden.  
  
5.  Generiert ein Resultset, die durch das Ausführen einer **wählen** -Anweisung oder einer Prozedur, oder durch eine Katalogfunktion aufrufen. Wenn die Anwendung positionierte Update-Anweisungen ausgeführt wird, führen sie eine **für aktualisieren wählen** Anweisung, um das Resultset zu generieren.  
  
6.  Aufrufe **SQLFetch** oder **SQLFetchScroll** ein- oder mehrmals, über das Resultset zu scrollen.  
  
 Die Anwendung kann Datenwerte in den Puffern Rowset ändern. Um die Rowset-Puffer mit Daten aus der Cursorbibliothek Cache zu aktualisieren, eine Anwendung ruft **SQLFetchScroll** mit der *FetchOrientation* SQL_FETCH_RELATIVE-Argument festgelegt und die  *FetchOffset* Argument auf 0 festgelegt.  
  
 Zum Abrufen von Daten aus einer nicht gebundenen Spalte, die Anwendung ruft **SQLSetPos** zur Positionierung des Cursors in der gewünschten Zeile. Er ruft dann **SQLGetData** zum Abrufen der Daten.  
  
 Um die Anzahl der Zeilen zu bestimmen, die aus der Datenquelle abgerufen wurden, ruft die Anwendung **SQLRowCount**.

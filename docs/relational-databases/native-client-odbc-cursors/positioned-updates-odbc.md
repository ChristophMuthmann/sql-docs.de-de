---
title: Positionierte Aktualisierungen (ODBC) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-cursors
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, cursors
- SQLSetPos function
- SQLSetCursorName function
- ODBC applications, cursors
- cursors [ODBC], positioned updates
- positioned updates [ODBC]
- ODBC cursors, positioned updates
ms.assetid: ff404e02-630f-474d-b5d4-06442b756991
caps.latest.revision: "33"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: de1164ecd8c965dbd641f1a5a1db5c26b3163453
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="positioned-updates-odbc"></a>Positionierte Updates (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  ODBC unterstützt zwei Methoden für das Ausführen von positionierten Updates in einem Cursor:  
  
-   **SQLSetPos**  
  
-   WHERE CURRENT OF-Klausel  
  
 Gängigerer Ansatz ist die Verwendung **SQLSetPos**. Es bietet die folgenden Optionen.  
  
 SQL_POSITION  
 Positioniert den Cursor in einer bestimmten Zeile im aktuellen Rowset.  
  
 SQL_REFRESH  
 Aktualisiert die an die Resultsetspalten gebundenen Programmvariablen mit den Werten aus der Zeile, in der der Cursor zurzeit positioniert ist.  
  
 SQL_UPDATE  
 Aktualisiert die aktuelle Zeile im Cursor mit den Werten aus den an die Resultsetspalten gebundenen Programmvariablen.  
  
 SQL_DELETE  
 Löscht die aktuelle Zeile im Cursor.  
  
 **SQLSetPos** kann verwendet werden, mit einem anweisungsresultset, wenn die Anweisungshandle-Cursorattribute so festgelegt sind, um Servercursor zu verwenden. Die Resultsetspalten müssen an Programmvariablen gebunden sein. Sobald die Anwendung eine Zeile abgerufen hat aufruft **SQLSetPos**(SQL_POSTION) auf, um den Cursor in der Zeile positionieren. Die Anwendung könnte dann SQLSetPos(SQL_DELETE) aufrufen, um die aktuelle Zeile zu löschen, oder neue Datenwerte in die gebundenen Programmvariablen verschieben und SQLSetPos(SQL_UPDATE) aufrufen, um die aktuelle Zeile zu aktualisieren.  
  
 Anwendungen können aktualisieren oder löschen Sie eine beliebige Zeile im Rowset mit **SQLSetPos**. Aufrufen von **SQLSetPos** ist eine praktische Alternative zum Erstellen und Ausführen einer SQL-Anweisung. **SQLSetPos** ausgeführt wird, auf das aktuelle Rowset und kann verwendet werden, nur nach einem Aufruf von [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md).  
  
 Rowsetgröße wird durch einen Aufruf von [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) mit einem attributsargument von SQL_ATTR_ROW_ARRAY_SIZE. **SQLSetPos** verwendet eine neue Rowsetgröße, aber nur nach einem Aufruf von **SQLFetch** oder **SQLFetchScroll**. Wenn die Rowsetgröße geändert wird, z. B. **SQLSetPos** wird aufgerufen, und klicken Sie dann **SQLFetch** oder **SQLFetchScroll** aufgerufen wird. Der Aufruf von **SQLSetPos** die alte Rowsetgröße verwendet jedoch **SQLFetch** oder **SQLFetchScroll** neue Rowsetgröße verwendet.  
  
 Die erste Zeile im Rowset ist die Zeile 1. Das RowNumber-Argument in **SQLSetPos** muss eine Zeile im Rowset; identifizieren, also muss sein Wert im Bereich zwischen 1 und die Anzahl der zuletzt abgerufenen Zeilen. Diese ist eventuell kleiner als die Rowsetgröße. Wenn RowNumber 0 ist, gilt der Vorgang für jede Zeile im Rowset.  
  
 Der Löschvorgang des **SQLSetPos** macht die Datenquelle, die eine oder mehrere ausgewählte Zeilen einer Tabelle zu löschen. So löschen Sie Zeilen mit **SQLSetPos**, ruft die Anwendung **SQLSetPos** mit Operation auf SQL_DELETE und RowNumber auf die Nummer der Zeile zu löschen. Wenn RowNumber 0 ist, werden alle Zeilen im Rowset gelöscht.  
  
 Nach dem **SQLSetPos** zurückgibt, die gelöschte Zeile wird die aktuelle Zeile und der Status SQL_ROW_DELETED. Die Zeile kann nicht verwendet werden, in weiteren positionierten Vorgängen, z. B. Aufrufe der [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) oder **SQLSetPos**.  
  
 Wenn Sie alle Zeilen im Rowset löschen (RowNumber ist gleich 0), die Anwendung kann verhindern, dass den Treiber bestimmte Zeilen löscht, ebenso wie mit der Zeile Operation-Array für den Updatevorgang des **SQLSetPos**.  
  
 Jede Zeile, die gelöscht wird, sollte eine Zeile sein, die im Resultset vorhanden ist. Wenn die Anwendungspuffer beim Abrufen gefüllt werden und ein Zeilenstatusarray beibehalten wurde, sollten die Werte an jeder Zeilenposition nicht SQL_ROW_DELETED, SQL_ROW_ERROR oder SQL_ROW_NOROW sein.  
  
 Positionierte Updates können auch mit der WHERE CURRENT OF-Klausel für UPDATE-, DELETE- und INSERT-Anweisungen durchgeführt werden. CURRENT OF, in denen erfordert ein Cursorname, der von ODBC, generieren bei der [SQLGetCursorName](../../relational-databases/native-client-odbc-api/sqlgetcursorname.md) Funktion wird aufgerufen, oder Sie können angeben, durch den Aufruf **SQLSetCursorName**. Im Folgenden finden Sie allgemeine Schritte zum Durchführen eines WHERE CURRENT OF-Updates in einer ODBC-Anwendung:  
  
-   Rufen Sie **SQLSetCursorName** um einen Cursornamen für das Anweisungshandle einzurichten.  
  
-   Erstellen Sie eine SELECT-Anweisung mit einer FOR UPDATE OF-Klausel, und führen Sie sie aus.  
  
-   Rufen Sie **SQLFetchScroll** zum Abrufen eines Rowsets oder **SQLFetch** abrufen eine Zeile.  
  
-   Rufen Sie **SQLSetPos** (SQL_POSITION) auf, um den Cursor in der Zeile positionieren.  
  
-   Erstellen und Ausführen eine UPDATE-Anweisung mit einer WHERE CURRENT OF-Klausel mit dem cursornamensset mit **SQLSetCursorName**.  
  
 Sie können alternativ Aufrufen **SQLGetCursorName** nach dem Ausführen der SELECT-Anweisung statt **SQLSetCursorName** vor der Ausführung der SELECT-Anweisung. **SQLGetCursorName** gibt einen Standardnamen-Cursor von ODBC zugewiesen wird, wenn der Cursor mit nicht festgelegt **SQLSetCursorName**.  
  
 **SQLSetPos** über WHERE CURRENT OF bevorzugt wird, bei Verwendung von Servercursorn. Wenn Sie einen statischen, aktualisierbaren Cursor mit der ODBC-Cursorbibliothek verwenden, implementiert die Cursorbibliothek die WHERE CURRENT OF-Updates, indem eine WHERE-Klausel mit den Schlüsselwerten für die zugrunde liegende Tabelle hinzugefügt wird. Dies kann zu nicht beabsichtigten Updates führen, wenn die Schlüssel in der Tabelle nicht eindeutig sind.  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden von Cursorn &#40; ODBC &#41;](../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md)  
  
  

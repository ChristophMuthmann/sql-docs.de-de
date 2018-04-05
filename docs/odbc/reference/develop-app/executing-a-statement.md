---
title: Ausführen einer Anweisung | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
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
- SQL statements [ODBC], executing
ms.assetid: e5f0d2ee-0453-4faf-b007-12978dd300a1
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ddb265060dc0714ce4eafaa09ce336d289697309
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="executing-a-statement"></a>Ausführen einer Anweisung
Es gibt vier Möglichkeiten zum Ausführen einer Anweisung abhängig ist, wenn sie kompiliert werden (vorbereitet sind) durch das Datenbankmodul und wer diese definiert:  
  
-   **Direkte Ausführung** der Anwendung definiert die SQL-Anweisung. Es wird vorbereitet und ausgeführt wird, zur Laufzeit in einem einzigen Schritt.  
  
-   **Vorbereitete Ausführung** der Anwendung definiert die SQL-Anweisung. Es wird vorbereitet und ausgeführt wird, zur Laufzeit in separate Schritte. Die Anweisung einmal vorbereitet, und mehrere Male ausgeführt werden kann.  
  
-   **Prozeduren** die Anwendung definieren kann, und kompilieren Sie eine oder mehrere SQL-Anweisungen bei der Entwicklung Zeit, und speichern Sie diese Anweisungen für die Datenquelle als eine Prozedur. Die Prozedur wird ein oder zwei Mal zur Laufzeit ausgeführt. Die Anwendung kann verfügbare gespeicherte Prozeduren, die mithilfe von Katalogfunktionen aufgelistet werden.  
  
-   **Katalogfunktionen** der Treiber-Writer erstellt eine Funktion, die ein vordefiniertes Resultset zurückgibt. Diese Funktion wird in der Regel übermittelt eine vordefinierte SQL­Anweisung oder ruft eine Prozedur, die für diesen Zweck erstellt wurde. Die Funktion, die ein oder zwei Mal zur Laufzeit ausgeführt wird.  
  
 Eine bestimmte Anweisung (, das durch seine Anweisungshandle) kann eine beliebige Anzahl von Zeiten ausgeführt. Die Anweisung mit einer Vielzahl von anderen SQL-Anweisungen ausgeführt werden kann, oder es kann mit der gleichen SQL-Anweisung wiederholt ausgeführt werden. Der folgende Code verwendet beispielsweise dasselbe Anweisungshandle (*hstmt1*) abrufen und Anzeigen der Tabellen in der Sales-Datenbank. Klicken Sie dann wiederverwendet dieses Handle zum Abrufen der Spalten in einer Tabelle, die vom Benutzer ausgewählten.  
  
```  
SQLHSTMT    hstmt1;  
SQLCHAR *   Table;  
  
// Create a result set of all tables in the Sales database.  
SQLTables(hstmt1, "Sales", SQL_NTS, "sysadmin", SQL_NTS, NULL, 0, NULL, 0);  
  
// Fetch and display the table names; then close the cursor.  
// Code not shown.  
  
// Have the user select a particular table.  
SelectTable(Table);  
  
// Reuse hstmt1 to create a result set of all columns in Table.  
SQLColumns(hstmt1, "Sales", SQL_NTS, "sysadmin", SQL_NTS, Table, SQL_NTS, NULL, 0);  
  
// Fetch and display the column names in Table; then close the cursor.  
// Code not shown.  
```  
  
 Und der folgende Code zeigt, wie ein einzelnes Handle wiederholte Ausführen von der gleichen Anweisung zum Löschen von Zeilen aus einer Tabelle verwendet wird.  
  
```  
SQLHSTMT      hstmt1;  
SQLUINTEGER   OrderID;  
SQLINTEGER    OrderIDInd = 0;  
  
// Prepare a statement to delete orders from the Orders table.  
SQLPrepare(hstmt1, "DELETE FROM Orders WHERE OrderID = ?", SQL_NTS);  
  
// Bind OrderID to the parameter for the OrderID column.  
SQLBindParameter(hstmt1, 1, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 5, 0,  
                  &OrderID, 0, &OrderIDInd);  
  
// Repeatedly execute hstmt1 with different values of OrderID.  
while ((OrderID = GetOrderID()) != 0) {  
   SQLExecute(hstmt1);  
}  
```  
  
 Für zahlreiche Treiber ist die Zuordnung von Anweisungen als teuer, damit Wiederverwenden der gleichen Anweisung auf diese Weise in der Regel effizienter als die vorhandenen Anweisungen und poolreservierung neue Freigabe ist. Anwendungen, die Erstellen von Resultsets für eine Anweisung müssen darauf achten, schließen Sie den Cursor über das Ergebnis festlegen, bevor Sie die Anweisung reexecuting sein; Weitere Informationen finden Sie unter [Schließen des Cursors](../../../odbc/reference/develop-app/closing-the-cursor.md).  
  
 Wiederverwenden von Anweisungen erzwingt auch die Anwendung aus, um eine Begrenzung im einige Treiber, der die Anzahl von Anweisungen zu vermeiden, die gleichzeitig aktiv sein können. Die genaue Definition von "aktiv" ist treiberspezifische, häufig verweist jedoch auf eine Anweisung, die vorbereitet oder ausgeführt wurde und noch immer Ergebnisse zur Verfügung. Beispielsweise nach dem ein **einfügen** Anweisung vorbereitet wurde, gilt im Allgemeinen aktiv; werden nach einer **wählen** Anweisung ausgeführt wurde und der Cursor noch geöffnet ist, gilt im Allgemeinen auf aktiv sein; Nachdem eine **CREATE TABLE** Anweisung ausgeführt wurde, wird er nicht in der Regel betrachtet aktiv sein.  
  
 Eine Anwendung bestimmt, wie viele Anweisungen über eine einzelne Verbindung gleichzeitig aktiv sein können, durch den Aufruf **SQLGetInfo** mit der Option SQL_MAX_CONCURRENT_ACTIVITIES. Eine Anwendung kann viele aktive Anweisungen über diesem Grenzwert verwenden, indem Sie mehrere Verbindungen mit der Datenquelle öffnen; Da Verbindungen teuer sein können, sollte jedoch die Auswirkungen auf die Leistung berücksichtigt werden.  
  
 Anwendungen können die Zeitspanne, die für eine Anweisung ausführen mit SQL_ATTR_QUERY_TIMEOUT-Anweisungsattribut vorgesehene einschränken. Wenn das Timeout abläuft, bevor die Datenquelle Resultset zurückgibt, gibt die Funktion die SQL-Anweisung ausführen SQLSTATE HYT00 zurück (das Timeout ist abgelaufen). Standardmäßig ist es kein Timeout ein.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Direkte Ausführung](../../../odbc/reference/develop-app/direct-execution-odbc.md)  
  
-   [Vorbereitete Ausführung](../../../odbc/reference/develop-app/prepared-execution-odbc.md)  
  
-   [Vorgehensweisen](../../../odbc/reference/develop-app/procedures-odbc.md)  
  
-   [Batches von SQL-Anweisungen](../../../odbc/reference/develop-app/batches-of-sql-statements.md)  
  
-   [Ausführen von Katalogfunktionen](../../../odbc/reference/develop-app/executing-catalog-functions.md)

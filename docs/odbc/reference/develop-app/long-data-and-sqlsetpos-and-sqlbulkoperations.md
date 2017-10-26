---
title: Long-Daten und SQLSetPos und SQLBulkOperations | Microsoft Docs
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
- long data [ODBC]
- SQLSetPos function [ODBC], long data and SQLBulkOperations
- data updates [ODBC], long data
- updating data [ODBC], long data
- SQLBulkOperations function [ODBC], long data
ms.assetid: e2fdf842-5e4c-46ca-bb21-4625c3324f28
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 308e1ad6f2d99a0a6b7e73d8a82ac62362fea9a2
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="long-data-and-sqlsetpos-and-sqlbulkoperations"></a>Long-Daten und SQLSetPos und SQLBulkOperations
Wie bei Parametern in SQL-Anweisungen der Fall ist, long-Daten gesendet werden können, wenn die Aktualisierung mit Zeilen **SQLBulkOperations** oder **SQLSetPos** oder beim Einfügen von Zeilen mit **SQLBulkOperations**. Die Daten werden gesendet, in Teilen, mit mehreren Aufrufen an **SQLPutData**. Spalten, die für die Daten zum Zeitpunkt der Ausführung gesendet werden, werden als bezeichnet *Data-at-Execution-Spalten*.  
  
> [!NOTE]  
>  Eine-Anwendung tatsächlich senden kann jeden Datentyp zum Zeitpunkt der Ausführung mit **SQLPutData**, obwohl nur Zeichen- und Binärdaten in Teilen gesendet werden können. Wenn die Daten klein genug, um einen einzelnen Puffer zu groß ist, besteht jedoch im Allgemeinen kein Grund zur Verwendung **SQLPutData**. Es ist viel leichter, den Puffer zu binden, und lassen den Treiber, die Abrufen der Daten aus dem Puffer.  
  
 Da lange Datenspalten in der Regel nicht gebunden werden, muss die Anwendung die Spalte vor dem Aufruf binden **SQLBulkOperations** oder **SQLSetPos** und heben Sie die Bindung nach dem Aufruf **SQLBulkOperations ** oder **SQLSetPos**. Die Spalte gebunden werden muss, da **SQLBulkOperations** oder **SQLSetPos** kann nur für gebundene Spalten und aufgehoben werden muss, damit **SQLGetData** kann zum Abrufen von Daten verwendet werden aus der Spalte.  
  
 Zum Senden von Daten zum Zeitpunkt der Ausführung führt die Anwendung Folgendes aus:  
  
1.  Einen 32-Bit-Wert platziert im Rowset Puffer statt eines Datenwerts. Dieser Wert wird an die Anwendung später zurückgegeben werden, damit die Anwendung, die keinen sinnvollen Wert, z. B. die Anzahl der Spalte oder das Handle einer Datei mit Daten festgelegt werden soll.  
  
2.  Legt den Wert in die Längen-/Indikatorpuffers auf das Ergebnis der SQL_LEN_DATA_AT_EXEC (*Länge*) Makro. Dieser Wert gibt an, an den Treiber, die die Daten für den Parameter mit gesendet werden, **SQLPutData**. Die *Länge* Wert wird verwendet, wenn long-Daten mit einer Datenquelle zu senden, die muss wissen, wie viele Bytes an Daten vom Typ long gesendet werden, damit er Speicherplatz vorab zugeordnet werden kann. Um festzustellen, ob eine Datenquelle dieser Wert ist, ruft die Anwendung erfordert eine **SQLGetInfo** mit der Option SQL_NEED_LONG_DATA_LEN. Alle Treiber müssen dieses Makro unterstützt werden Wenn die Bytelänge in die Datenquelle nicht erforderlich ist, können Sie von der Treiber ignorieren.  
  
3.  Aufrufe **SQLBulkOperations** oder **SQLSetPos**. Der Treiber ermittelt, dass ein Längen-/Indikatorpuffers auf das Ergebnis der SQL_LEN_DATA_AT_EXEC enthält (*Länge*)-Makro und gibt SQL_NEED_DATA zurück, als der Rückgabewert der Funktion.  
  
4.  Aufrufe **SQLParamData** Rückgabewert als Antwort auf die SQL_NEED_DATA zurück. Wenn long-Daten gesendet werden, müssen **SQLParamData** wird SQL_NEED_DATA zurückgegeben. In den Puffer, die durch die *ValuePtrPtr* Argument, gibt der Treiber den eindeutigen Wert, der die Anwendung im Puffer Rowset eingefügt. Wenn mehr als ein Data-at-Execution-Spalte enthalten ist, verwendet die Anwendung diesen Wert, um zu bestimmen, welche Spalte zum Senden von Daten für; der Treiber ist nicht erforderlich, Anfordern von Daten für Data-at-Execution-Spalten in einer bestimmten Reihenfolge.  
  
5.  Aufrufe **SQLPutData** zum Senden der Spaltendaten an den Treiber. Wenn die Spaltendaten wie häufig der Fall mit long-Daten ist in einem einzigen Puffer nicht passt, die Anwendung aufruft, **SQLPutData** wiederholt zum Senden der Daten in Teilen; es obliegt dem Treiber und der Datenquelle, die Daten wieder zusammenzusetzen. Wenn die Anwendung auf Null endende Zeichenfolgendaten übergibt, muss die Treiber oder die Datenquelle der Null-Terminierung Zeichen als Teil des Prozesses für die Reassemblierung entfernen.  
  
6.  Aufrufe **SQLParamData** erneut aus, um anzugeben, dass sie alle Daten für die Spalte gesendet wurde. Wenn alle Data-at-Execution-Spalten, die für die Daten nicht gesendet wurden vorhanden sind, gibt der Treiber SQL_NEED_DATA sowie den eindeutigen Wert für die nächste Data-at-Execution-Spalte zurück; Gibt zurück, die Anwendung mit Schritt 5 fort. Wenn Daten für alle Data-at-Execution-Spalten gesendet wurde, werden die Daten für die Zeile an die Datenquelle gesendet. **SQLParamData** gibt SQL_SUCCESS oder SQL_SUCCESS_WITH_INFO und kann SQLSTATE zurückgeben **SQLBulkOperations** oder **SQLSetPos** zurückgeben kann.  
  
 Nach dem **SQLBulkOperations** oder **SQLSetPos** wird SQL_NEED_DATA zurückgegeben, und bevor die Daten vollständig für die letzte Data-at-Execution-Spalte gesendet wurde, wird die Anweisung in einem Zustand benötigen. In diesem Zustand befindet, kann die Anwendung nur aufrufen **SQLPutData**, **SQLParamData**, **SQLCancel**, **SQLGetDiagField**, oder **SQLGetDiagRec**; alle anderen Funktionen zurückgeben SQLSTATE HY010 (Sequenzfehler-Funktion). Aufrufen von **SQLCancel** bricht die Ausführung der Anweisung ab und gibt sie an den ursprünglichen Zustand zurück. Weitere Informationen finden Sie unter [Anhang B: ODBC-Übergang-Statustabellen](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).


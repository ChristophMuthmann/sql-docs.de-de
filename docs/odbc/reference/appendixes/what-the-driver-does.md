---
title: Was bewirkt, dass der Treiber | Microsoft Docs
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
- scrollable cursors [ODBC]
- cursors [ODBC], backward compatibility
- compatibility [ODBC], cursors
- backward compatibility [ODBC], cursors
- block cursors [ODBC]
ms.assetid: 75dcdea6-ff6b-4ac8-aa11-a1f9edbeb8e6
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 07e94046370f8140fdacec2cf708de0a62311a27
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="what-the-driver-does"></a>Was bewirkt, dass der Treiber
Die folgende Tabelle fasst zusammen, welche Funktionen und Anweisungsattribute eine ODBC 3.*.x* Treiber sollten für Blocks und bildlauffähigen Cursorn implementieren.  
  
|Funktion oder<br /><br /> Anweisungsattribut|Kommentare|  
|-----------------------------------------|--------------|  
|SQL_ATTR_ROW_STATUS_PTR|Legt die Adresse der zeilenstatusarray von ausgefüllt **SQLFetch** und **SQLFetchScroll**. Dieses Array wird auch durch gefüllt **SQLSetPos** Wenn **SQLSetPos** Anweisung Status a6 aufgerufen wird. Wenn **SQLSetPos** heißt Status S7, dieses Array wird nicht ausgefüllt, aber das Array verweist die *RowStatusArray* Argument **SQLExtendedFetch** gefüllt wird. Weitere Informationen finden Sie unter [Anweisung Übergänge](../../../odbc/reference/appendixes/statement-transitions.md) in Anhang B: ODBC-Übergang-Statustabellen.|  
|SQL_ATTR_ROWS_FETCHED_PTR FEST|Legt die Adresse des Puffers, in dem **SQLFetch** und **SQLFetchScroll** geben die Anzahl der abgerufenen Zeilen zurück. Wenn **SQLExtendedFetch** wird aufgerufen, wird dieser Puffer nicht ausgefüllt aber die *RowCountPtr* Argument verweist auf die Anzahl der abgerufenen Zeilen.|  
|SQL_ATTR_ROW_ARRAY_SIZE|Legt die Rowsetgröße von verwendeten **SQLFetch** und **SQLFetchScroll**.|  
|SQL_ROWSET_SIZE SETZEN|Legt die Rowsetgröße von verwendeten **SQLExtendedFetch**. ODBC 3.*.x* Treiber implementieren Sie dies, wenn sie mit ODBC 2. arbeiten möchten.* X* Anwendungen, die Aufrufen **SQLExtendedFetch** oder **SQLSetPos**.|  
|**SQLBulkOperations**|Wenn eine ODBC 3.*.x* Treiber sollte arbeiten mit ODBC 2..* X* Anwendungen, die **SQLSetPos** mit einer *Vorgang* von SQL_ADD, muss der Treiber unterstützen **SQLSetPos** mit einer * Vorgang* von SQL_ADD zusätzlich zu **SQLBulkOperations** mit einem *Vorgang* von SQL_ADD.|  
|**SQLExtendedFetch**|Gibt das angegebene Rowset zurück. ODBC 3.*.x* Treiber implementieren Sie dies, wenn sie mit ODBC 2. arbeiten möchten.* X* Anwendungen, die Aufrufen **SQLExtendedFetch** oder **SQLSetPos**. Im folgenden finden Details zur Implementierung:<br /><br /> -Der Treiber Ruft die Größe des Rowsets ab, aus dem Wert des Attributs Anweisung SQL_ROWSET_SIZE setzen.<br />-Der Treiber Ruft die Adresse der zeilenstatusarray aus der *RowStatusArray* Argument, nicht das Anweisungsattribut SQL_ATTR_ROW_STATUS_PTR. Die *RowStatusArray* Argument in einem Aufruf von **SQLExtendedFetch** darf nicht null-Zeiger sein. (Beachten Sie, dass in ODBC 3.*.x*, SQL_ATTR_ROW_STATUS_PTR-Anweisungsattribut kann ein null-Zeiger sein.)<br />-Der Treiber Ruft die Adresse des Puffers abgerufenen Zeilen aus der *RowCountPtr* Argument, nicht das SQL_ATTR_ROWS_FETCHED_PTR-Anweisungsattribut.<br />-Der Treiber gibt SQLSTATE 01 s 01 (Fehler in Zeile), um anzugeben, dass ein Fehler aufgetreten ist, während der abgerufenen Zeilen durch einen Aufruf von **SQLExtendedFetch**. Eine ODBC 3.*.x* Treiber sollte SQLSTATE 01 s 01 zurückgegeben (Fehler in Zeile) nur, wenn **SQLExtendedFetch** aufgerufen wird, nicht wenn **SQLFetch** oder **SQLFetchScroll** aufgerufen wird. Abwärtskompatibilität beibehalten beim SQLSTATE 01 s 01 (Fehler in Zeile) zurückgegebene **SQLExtendedFetch**, sortiert der Treiber-Manager Statusdatensätze nicht in der Fehlerwarteschlange gemäß den Regeln in der "Reihenfolge der Status angegeben Zeichnet"im Abschnitt [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md).|  
|**SQLFetch**|Gibt das nächste Rowset zurück. Im folgenden finden Details zur Implementierung:<br /><br /> -Der Treiber Ruft die Größe des Rowsets aus dem Wert des Attributs SQL_ATTR_ROW_ARRAY_SIZE-Anweisung ab.<br />-Der Treiber Ruft die Adresse des Arrays Status Zeile aus der SQL_ATTR_ROW_STATUS_PTR-Anweisungsattribut ab.<br />-Der Treiber Ruft die Adresse der Puffer aus das SQL_ATTR_ROWS_FETCHED_PTR-Anweisungsattribut abgerufenen Zeilen ab.<br />– Die Anwendung kann Aufrufe zwischen mischen **SQLFetchScroll** und **SQLFetch**.<br />-   **SQLFetch** Lesezeichen zurückgegeben, wenn die Spalte 0 gebunden ist.<br />-   **SQLFetch** aufgerufen werden, um mehr als eine Zeile zurückgeben.<br />-Der Treiber keinen SQLSTATE 01 s 01 zurückgibt (Fehler in Zeile), um anzugeben, dass ein Fehler aufgetreten ist, während der abgerufenen Zeilen durch einen Aufruf von **SQLFetch**.|  
|**SQLFetchScroll**|Gibt das angegebene Rowset zurück. Im folgenden finden Details zur Implementierung:<br /><br /> -Der Treiber Ruft die Größe des Rowsets aus dem SQL_ATTR_ROW_ARRAY_SIZE-Anweisungsattribut ab.<br />-Der Treiber Ruft die Adresse des Arrays Status Zeile aus der SQL_ATTR_ROW_STATUS_PTR-Anweisungsattribut ab.<br />-Der Treiber Ruft die Adresse der Puffer aus das SQL_ATTR_ROWS_FETCHED_PTR-Anweisungsattribut abgerufenen Zeilen ab.<br />– Die Anwendung kann Aufrufe zwischen mischen **SQLFetchScroll** und **SQLFetch**.<br />-Der Treiber keinen SQLSTATE 01 s 01 zurückgibt (Fehler in Zeile), um anzugeben, dass ein Fehler aufgetreten ist, während der abgerufenen Zeilen durch einen Aufruf von **SQLFetchScroll**.|  
|**SQLSetPos**|Führt verschiedene positionierte Operationen. Im folgenden finden Details zur Implementierung:<br /><br /> -Dies kann in der Anweisung Statuswerte a6 oder S7 aufgerufen werden. Weitere Informationen finden Sie unter [Anweisung Übergänge](../../../odbc/reference/appendixes/statement-transitions.md) in Anhang B: ODBC-Übergang-Statustabellen.<br />– Wenn diese Anweisung weist S5 oder a6 aufgerufen wird, ruft der Treiber die Rowsetgröße von das SQL_ATTR_ROWS_FETCHED_PTR-Anweisungsattribut und die Adresse des dem zeilenstatusarray aus SQL_ATTR_ROW_STATUS_PTR-Anweisungsattribut ab.<br />– Wenn diese Anweisung weist S7 aufgerufen wird, ruft der Treiber die Rowsetgröße von das Anweisungsattribut SQL_ROWSET_SIZE setzen und die Adresse des Arrays Status Zeile aus der *RowStatusArray* Argument ** SQLExtendedFetch**.<br />-Der Treiber gibt SQLSTATE 01 s 01 (Fehler in Zeile) nur, um anzugeben, dass ein Fehler aufgetreten ist, während der abgerufenen Zeilen durch einen Aufruf von **SQLSetPos** einen Massenvorgang ausführen, wenn die Funktion im Zustand S7 aufgerufen wird. Um Abwärtskompatibilität zu gewährleisten, wenn beibehalten SQLSTATE 01 s 01 (Fehler in Zeile) zurückgegebene **SQLSetPos**, sortiert der Treiber-Manager Statusdatensätze nicht in der Fehlerwarteschlange gemäß den Regeln in den "Sequenz von Statusdatensätzen" angegeben im Abschnitt [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md).<br />– Wenn der Treiber für ODBC 2. geeignet sein sollte. *x* Anwendungen, die aufgerufen werden **SQLSetPos** mit einem *Vorgang* Argument SQL_ADD, der Treiber muss unterstützen **SQLSetPos** mit einer * Vorgang* SQL_ADD Argument.|

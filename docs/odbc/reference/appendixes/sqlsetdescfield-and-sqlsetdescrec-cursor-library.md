---
title: SQLSetDescField und SQLSetDescRec (Cursorbibliothek) | Microsoft Docs
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
- SQLSetDescField function [ODBC], Cursor Library
- SQLSetDescRec function [ODBC], Cursor Library
ms.assetid: 4ccff067-85cd-4bfa-a6cd-7f28051fb5b9
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 04c3fd1c3c64140b7669cdeeb35937498249ac66
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlsetdescfield-and-sqlsetdescrec-cursor-library"></a>SQLSetDescField und SQLSetDescRec (Cursor Library)
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen und Planen von Anwendungen zu ändern, die dieses Feature verwenden. Microsoft empfiehlt die Verwendung der Cursorfunktionalität der Treiber.  
  
 In diesem Thema erläutert die Verwendung von der **SQLSetDescField** und **SQLSetDescRec** Funktionen in die Cursorbibliothek. Allgemeine Informationen zu diesen Funktionen finden Sie unter [SQLSetDescField-Funktion](../../../odbc/reference/syntax/sqlsetdescfield-function.md) und [SQLSetDescRec-Funktion](../../../odbc/reference/syntax/sqlsetdescrec-function.md).  
  
 Führt die Cursorbibliothek **SQLSetDescField** Wenn sie aufgerufen wird, um den Wert der Felder zurückzugeben für Lesezeichenspalten festgelegt:  
  
 SQL_DESC_DATA_PTR  
  
 SQL_DESC_INDICATOR_PTR  
  
 SQL_DESC_OCTET_LENGTH_PTR  
  
 SQL_DESC_LENGTH  
  
 SQL_DESC_OCTET_LENGTH  
  
 SQL_DESC_DATETIME_INTERVAL_CODE  
  
 SQL_DESC_SCALE  
  
 SQL_DESC_PRECISION  
  
 SQL_DESC_TYPE  
  
 SQL_DESC_NAME  
  
 SQL_DESC_UNNAMED  
  
 SQL_DESC_NULLABLE  
  
 Die Cursorbibliothek führt Aufrufe **SQLSetDescRec** für eine Lesezeichenspalte.  
  
 Wenn Sie mit einer ODBC 2. arbeiten zu können. *x* -Treiber verwenden, gibt die Cursorbibliothek SQLSTATE HY090 zurück (ungültige Zeichenfolgen- oder Pufferlänge.) Wenn **SQLSetDescField** oder **SQLSetDescRec** wird aufgerufen, um die SQL_DESC_OCTET_ festlegen Das Längenfeld des Lesezeichen-Datensatzes, der ein ARD auf einen Wert, der nicht gleich 4. Bei der Arbeit mit einer ODBC 3.*.x* -Treiber die Cursorbibliothek ermöglicht den Puffer, in beliebiger Größe sein.  
  
 Führt die Cursorbibliothek **SQLSetDescField** wenn er aufgerufen wird, um den Wert des Felds SQL_DESC_BIND_OFFSET_PTR, SQL_DESC_BIND_TYPE, SQL_DESC_ROW_ARRAY_SIZE oder SQL_DESC_ROW_STATUS_PTR zurück. Diese Felder können für jede Zeile wird nicht nur die Lesezeichen-Zeile zurückgegeben werden.  
  
 Die Cursorbibliothek wird nicht ausgeführt. **SQLSetDescField** alle Deskriptorfeld als die zuvor aufgeführten Felder ändern. Wenn eine Anwendung ruft **SQLSetDescField** um jedes andere Feld festzulegen, während die Cursorbibliothek geladen ist, der Aufruf über den Treiber übergeben wird.  
  
 Die Cursorbibliothek unterstützt die SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR und SQL_DESC_OCTET_LENGTH_PTR Felder einer Zeile von einer Anwendung Zeilendeskriptor dynamisch ändern (nach einem Aufruf von **SQLExtendedFetch**, **SQLFetch**, oder **SQLFetchScroll**). Das Feld SQL_DESC_OCTET_LENGTH_PTR kann ein null-Zeiger nur für den Puffer Länge für eine Spalte aufheben der Bindung geändert werden.  
  
 Die Cursorbibliothek unterstützt nicht das SQL_DESC_BIND_TYPE-Feld in einem APD oder ARD ändern, wenn ein Cursor geöffnet ist. Das Feld SQL_DESC_BIND_TYPE kann geändert werden, nur, nachdem der Cursor geschlossen ist, und bevor Sie ein neuer Cursor geöffnet wird. Sind die einzige deskriptorfelder, dass die Cursorbibliothek ändern unterstützt, wenn ein Cursor geöffnet ist, SQL_DESC_ARRAY_STATUS_PTR, SQL_DESC_BIND_OFFSET_PTR SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR, SQL_DESC_OCTET_LENGTH_PTR und SQL_DESC_ROWS_PROCESSED_ PTR-WERT.  
  
 Die Cursorbibliothek unterstützt nicht das SQL_DESC_COUNT Feld von der ARD nach dem Ändern **SQLExtendedFetch** oder **SQLFetchScroll** aufgerufen wurde und bevor der Cursor geschlossen wurde.

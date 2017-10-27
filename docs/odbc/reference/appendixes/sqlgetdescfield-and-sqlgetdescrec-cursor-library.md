---
title: SQLGetDescField und SQLGetDescRec (Cursorbibliothek) | Microsoft Docs
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
- SQLGetDescField function [ODBC], Cursor Library
- SQLGetDescRec function [ODBC], Cursor Library
ms.assetid: 1a801f22-6fea-48aa-a723-3187a2ad852b
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ff32edcc14799980c1d8ec9e05bd27456d71a132
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgetdescfield-and-sqlgetdescrec-cursor-library"></a>SQLGetDescField und SQLGetDescRec (Cursor Library)
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen und Planen von Anwendungen zu ändern, die dieses Feature verwenden. Microsoft empfiehlt die Verwendung der Cursorfunktionalität der Treiber.  
  
 In diesem Thema erläutert die Verwendung von der **SQLGetDescField** und **SQLGetDescRec** Funktionen in die Cursorbibliothek. Allgemeine Informationen zu diesen Funktionen finden Sie unter [SQLGetDescField-Funktion](../../../odbc/reference/syntax/sqlgetdescfield-function.md) und [SQLGetDescRec-Funktion](../../../odbc/reference/syntax/sqlgetdescrec-function.md).  
  
 Führt die Cursorbibliothek **SQLGetDescRec** Metadaten für Lesezeichenspalten zurückgegeben. Führt die Cursorbibliothek **SQLGetDescField** zurückzugebenden dieselben Felder zurückgegebenes **SQLGetDescRec**, SQL_DESC_NAME, SQL_DESC_TYPE, SQL_DESC_DATETIME_INTERVAL_CODE, SQL_DESC_OCTET_ sind Länge, SQL_DESC_PRECISION SQL_DESC_SCALE und SQL_DESC_NULLABLE. Aus Gründen der Konsistenz **SQLGetDescField** SQL_DESC_UNNAMED ebenfalls zurück.  
  
 Führt die Cursorbibliothek **SQLGetDescField** Wenn sie aufgerufen wird, zurückgeben, der Wert der folgenden Felder, die zum Binden von Lesezeichenspalten festgelegt sind: SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR und SQL_DESC_OCTET_LENGTH_PTR, und SQL_DESC_LENGTH.  
  
 Führt die Cursorbibliothek **SQLGetDescField** wenn er aufgerufen wird, um den Wert des Felds SQL_DESC_BIND_OFFSET_PTR, SQL_DESC_BIND_TYPE, SQL_DESC_ROW_ARRAY_SIZE oder SQL_DESC_ROW_STATUS_PTR zurück. Diese Felder können für jede Zeile wird nicht nur die Lesezeichen-Zeile zurückgegeben werden.  
  
 Wenn eine Anwendung ruft **SQLGetDescField** um den Wert eines Felds andere als die bereits erwähnten zurückzugeben, die Cursorbibliothek den Aufruf an den Treiber übergeben.


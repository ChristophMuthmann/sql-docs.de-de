---
title: "Einfügen von Zeilen mit SQLBulkOperations | Microsoft Docs"
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
- SQLBulkOperations function [ODBC], inserting rows
- data updates [ODBC], SQLBulkOperations
- updating data [ODBC], SQLBulkOperations
ms.assetid: ed585ea7-4d56-4df9-8dc3-53ca82382450
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bd79255e4cda68d1fd4d425544702e589f44336b
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="inserting-rows-with-sqlbulkoperations"></a>Einfügen von Zeilen mit SQLBulkOperations
Einfügen von Daten mit **SQLBulkOperations** ähnelt dem Aktualisieren von Daten mit **SQLBulkOperations** , da er Daten aus den gebundenen Anwendungspuffer verwendet.  
  
 So, dass jede Spalte in der neuen Zeile einen Wert hat, alle Spalten mit dem Wert Längenindikator/SQL_COLUMN_IGNORE gebunden, und alle ungebundene Spalten müssen entweder NULL-Werte akzeptieren oder einen Standardwert aufweisen.  
  
 Zum Einfügen von Zeilen mit **SQLBulkOperations**, die Anwendung bewirkt Folgendes:  
  
1.  Legt das SQL_ATTR_ROW_ARRAY_SIZE-Anweisungsattribut auf die Anzahl der einzufügenden Zeilen und die neuen Datenwerte in den Puffern mit gebundenen Anwendung platziert. Informationen zum Senden von long-Daten mit **SQLBulkOperations**, finden Sie unter [Long-Daten und SQLSetPos und SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md).  
  
2.  Legt den Wert in jeder Spalte Längen-/Indikatorpuffers nach Bedarf. Dies ist die Bytelänge der Daten oder SQL_NTS für Spalten gebunden auf Zeichenfolgepuffer, die Bytelänge der Daten für Spalten gebunden, binäre Puffer und SQL_NULL_DATA für alle Spalten auf NULL festgelegt werden. Die Anwendung legt den Wert in diesen Spalten, die auf ihre Standardeinstellung festgelegt wird (falls vorhanden) oder NULL (falls eine nicht der Fall ist), um SQL_COLUMN_IGNORE Längen-/Indikatorpuffers auf.  
  
3.  Aufrufe **SQLBulkOperations** mit der *Vorgang* -Argument auf SQL_ADD festgelegt.  
  
 Nach dem **SQLBulkOperations** zurückgibt, die aktuelle Zeile unverändert ist. Wenn das (0) Lesezeichenspalte gebunden ist, **SQLBulkOperations** gibt das Lesezeichen der eingefügten Zeilen im Rowset Puffer an diese Spalte gebunden.


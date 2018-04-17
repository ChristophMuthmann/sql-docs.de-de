---
title: Aktualisieren von Zeilen durch Lesezeichen mit SQLBulkOperations | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
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
- data updates [ODBC], bookmarks
- SQLBulkOperations function [ODBC], updating rows
- data updates [ODBC], SQLBulkOperations
- bookmarks [ODBC]
- updating data [ODBC], bookmarks
- updating data [ODBC], SQLBulkOperations
ms.assetid: c9ad82b7-8dba-45b0-bdb9-f4668b37c0d6
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c5a561fe33a54f31bcbe554dbf34525812c234e5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="updating-rows-by-bookmark-with-sqlbulkoperations"></a>Aktualisieren von Zeilen durch Lesezeichen mit SQLBulkOperations
Beim Aktualisieren einer Zeile von Lesezeichen, **SQLBulkOperations** macht die Datenquelle, die eine oder mehrere Zeilen der Tabelle zu aktualisieren. Die Zeilen werden durch das Lesezeichen in einer Lesezeichenspalte gebundenen identifiziert. Die Zeile wird aktualisiert, mit der Daten in die Anwendungspuffer für jede gebundene Spalte (außer wenn der Wert in die Längen-/Indikatorpuffers für eine Spalte SQL_COLUMN_IGNORE ist). Ungebundene Spalten werden nicht aktualisiert werden.  
  
 Zum Aktualisieren von Zeilen durch Lesezeichen mit **SQLBulkOperations**, die Anwendung:  
  
1.  Ruft ab und speichert die Textmarken aller Zeilen aktualisiert werden. Wenn mehrere Lesezeichen vorhanden ist, und spaltenbezogene Bindungen verwendet wird, werden die Lesezeichen in einem Array gespeichert. Wenn mehrere Lesezeichen vorhanden ist, und die zeilenweise Bindung verwendet wird, werden Lesezeichen in einem Array von Zeilenstrukturen gespeichert.  
  
2.  Legt das SQL_ATTR_ROW_ARRAY_SIZE-Anweisungsattribut auf die Anzahl von Lesezeichen und bindet den Puffer mit der Lesezeichenwert, oder das Array von Lesezeichen, um die Spalte 0.  
  
3.  Stellen Sie die neuen Datenwerte in den Puffern Rowset. Informationen zum Senden von long-Daten mit **SQLBulkOperations**, finden Sie unter [Long-Daten und SQLSetPos und SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md).  
  
4.  Legt den Wert in jeder Spalte Längen-/Indikatorpuffers nach Bedarf. Dies ist die Bytelänge der Daten oder SQL_NTS für Spalten gebunden auf Zeichenfolgepuffer, die Bytelänge der Daten für Spalten gebunden, binäre Puffer und SQL_NULL_DATA für alle Spalten auf NULL festgelegt werden.  
  
5.  Legt den Wert in die Längen-/Indikatorpuffers dieser Spalten, die nicht auf SQL_COLUMN_IGNORE aktualisiert werden. Obwohl die Anwendung kann diesen Schritt überspringen und vorhandene Daten senden, dies ist ineffizient und Risiken, senden die Werte mit der Datenquelle, die abgeschnitten wurden, wenn sie gelesen wurden.  
  
6.  Aufrufe **SQLBulkOperations** mit der *Vorgang* -Argument auf SQL_UPDATE_BY_BOOKMARK festgelegt.  
  
 Für jede Zeile, die mit der Datenquelle als Update gesendet wird, sollte die Anwendungspuffer gültige Zeilendaten haben. Wenn die Anwendungspuffer durch Abrufen, aufgefüllt wurden, falls ein zeilenstatusarray beibehalten wurde, und der Statuswert für eine Zeile SQL_ROW_DELETED, SQL_ROW_ERROR oder SQL_ROW_NOROW ist, konnte die ungültige Daten versehentlich an die Datenquelle gesendet werden.

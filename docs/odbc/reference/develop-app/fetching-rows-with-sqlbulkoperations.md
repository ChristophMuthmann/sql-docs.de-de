---
title: Abrufen von Zeilen mit SQLBulkOperations | Microsoft Docs
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
- data updates [ODBC], bookmarks
- SQLBulkOperations function [ODBC], fetching rows
- data updates [ODBC], SQLBulkOperations
- bookmarks [ODBC]
- updating data [ODBC], bookmarks
- updating data [ODBC], SQLBulkOperations
ms.assetid: 0efee2d6-ce94-411e-9976-97ba28b8da37
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5b3af3d83d9d0dab4735842621bbcb49fab69a4c
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="fetching-rows-with-sqlbulkoperations"></a>Abrufen von Zeilen mit SQLBulkOperations
Daten können in ein Rowset mithilfe von Lesezeichen erneut abgerufen werden, durch den Aufruf von **SQLBulkOperations.** Die Zeilen abgerufen werden sollen, werden durch die Lesezeichen in einer Lesezeichenspalte gebundenen identifiziert. Spalten mit einem Wert von SQL_COLUMN_IGNORE werden nicht abgerufen.  
  
 Zum Ausführen der Bulk-Abrufe mit **SQLBulkOperations**, die Anwendung bewirkt Folgendes:  
  
1.  Ruft ab und speichert die Textmarken aller Zeilen aktualisiert werden. Wenn mehrere Lesezeichen vorhanden ist, und spaltenbezogene Bindungen verwendet wird, werden die Lesezeichen in einem Array gespeichert. Wenn mehrere Lesezeichen vorhanden ist, und die zeilenweise Bindung verwendet wird, werden Lesezeichen in einem Array von Zeilenstrukturen gespeichert.  
  
2.  Legt SQL_ATTR_ROW_ARRAY_SIZE-Anweisungsattribut auf die Anzahl der abzurufenden Zeilen fest, und bindet den Puffer mit der Lesezeichenwert, oder das Array von Lesezeichen, um die Spalte 0.  
  
3.  Legt den Wert in jeder Spalte Längen-/Indikatorpuffers nach Bedarf. Dies ist die Bytelänge der Daten oder SQL_NTS für Spalten gebunden auf Zeichenfolgepuffer, die Bytelänge der Daten für Spalten gebunden, binäre Puffer und SQL_NULL_DATA für alle Spalten auf NULL festgelegt werden. Die Anwendung legt den Wert in diesen Spalten, die auf ihre Standardeinstellung festgelegt wird (falls vorhanden) oder NULL (falls eine nicht der Fall ist), um SQL_COLUMN_IGNORE Längen-/Indikatorpuffers auf.  
  
4.  Aufrufe **SQLBulkOperations** mit der *Vorgang* -Argument auf SQL_FETCH_BY_BOOKMARK festgelegt.  
  
 Besteht keine Notwendigkeit für die Anwendung auf die Zeile Operation-Array verwenden, um den Vorgang zu verhindern, dass in bestimmte Spalten ausgeführt werden. Die Anwendung wählt die Zeilen, die abgerufen werden nur die Lesezeichen für die Zeilen in die gebundenen Lesezeichen Array kopiert werden sollen.

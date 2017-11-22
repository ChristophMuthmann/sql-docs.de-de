---
title: "Relative und Absolute Durchführen eines Bildlaufs | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- absolute scrolling [ODBC]
- relative scrolling [ODBC]
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
ms.assetid: 3d0ff48d-fef5-4c01-bb1d-a583e6269b66
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 32782c2fe59aaf36fa8741870a798163d923a3a1
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="relative-and-absolute-scrolling"></a>Relative und Absolute Durchführen eines Bildlaufs
Durchführen eines Bildlaufs Optionen in den meisten **SQLFetchScroll** positionieren Sie den Cursor relativ zur aktuellen Position oder eine absolute Position. **SQLFetchScroll** unterstützt das Abrufen des nächsten, vorherigen, ersten und letzten Rowsets als auch als relativen abrufen (das Rowset abrufen,  *n*  Zeilen vom Anfang des aktuellen Rowsets) und absoluten abrufen (Fetch die Rowset ab Zeile  *n* ). Wenn  *n*  ist in einem absoluten Abruf negativ ist, werden Zeilen aus dem Ende des Resultsets gezählt. Folglich bedeutet, dass ein absoluter Abruf von Zeile – 1, das Rowset abzurufen, das mit der letzten Zeile im Resultset beginnt.  
  
 Dynamische Cursor erkennen Zeilen eingefügt und aus dem Resultset gelöscht werden, damit es keine einfache Möglichkeit für dynamische Cursor die Zeile an eine bestimmte Anzahl als das Lesen vom Beginn des Resultsets, abrufen, die Wahrscheinlichkeit gibt zu langsam ausgeführt wird. Darüber hinaus ist absoluten abrufen nicht sehr sinnvoll bei dynamischen Cursorn da Zeilennummern ändern, wie Zeilen eingefügt und gelöscht werden; aus diesem Grund kann die gleiche Anzahl von Zeilen nacheinander abrufen unterschiedliche Zeilen ergeben.  
  
 Anwendungen, die **SQLFetchScroll** nur Cursor-Funktionen, z. B. Berichte, sind wahrscheinlich für die Weiterleitung über das Resultset auf eines einzigen Mal und verwenden die Option zum Abrufen des nächsten Rowsets. Bildschirmbasierte Anwendungen andererseits, nutzen die Funktionen des **SQLFetchScroll**. Wenn die Anwendung die Rowsetgröße auf die Anzahl der Zeilen, die auf dem Bildschirm angezeigt legt, und die Bildschirmpuffer an das Resultset bindet, können sie Vorgänge der Bildlaufleiste direkt in Aufrufe an übersetzen **SQLFetchScroll**.  
  
|Bildlaufleistenvorgang|SQLFetchScroll-Bildlaufoption|  
|--------------------------|-------------------------------------|  
|Bild auf|SQL_FETCH_PRIOR|  
|Bild ab|SQL_FETCH_NEXT|  
|Zeile auf|SQL_FETCH_RELATIVE mit *FetchOffset* ungleich – 1|  
|Zeile ab|SQL_FETCH_RELATIVE mit *FetchOffset* gleich 1|  
|Das Bildlauffeld oben|SQL_FETCH_FIRST|  
|Das Bildlauffeld unten|SQL_FETCH_LAST|  
|Zufällige Bildlauffeldposition|SQL_FETCH_ABSOLUTE|  
  
 Solche Anwendungen müssen auch das Bildlauffeld nach einem Vorgang durchführen eines Bildlaufs positionieren, das die aktuelle Zeilennummer und die Anzahl der Zeilen erforderlich ist. Für die aktuelle Zeilennummer Anwendungen können entweder Nachverfolgen von der aktuellen Zeilennummer oder Aufruf **SQLGetStmtAttr** mit dem SQL_ATTR_ROW_NUMBER-Attribut, um sie abzurufen.  
  
 Die Anzahl der Zeilen im Cursor, der die Größe des Ergebnisses ist festgelegt, wird als Feld SQL_DIAG_CURSOR_ROW_COUNT des Diagnose-Headers zur Verfügung. Der Wert in diesem Feld wird erst nach definiert **SQLExecute**, **SQLExecDirect**, oder **SQLMoreResult** aufgerufen wurde. Diese Anzahl kann die geschätzte Anzahl oder eine genaue Anzahl, abhängig von den Funktionen des Treibers. Der Treiber kann bestimmt werden, durch den Aufruf **SQLGetInfo** mit Informationen die Cursortypen-Attribute und überprüfen, ob das Bit SQL_CA2_CRC_APPROXIMATE oder SQL_CA2_CRC_EXACT für den Typ des Cursors zurückgegeben wird.  
  
 Eine genaue Zeilenanzahl wird nie für einen dynamischen Cursor unterstützt. Für andere Typen von Cursorn kann der Treiber entweder genaue oder Ungefähre Zeilenanzahl, aber nicht beide unterstützen. Wenn der Treiber unterstützt, weder genaue oder Ungefähre Zeilenanzahl für einen bestimmten Cursortyp, das SQL_DIAG_CURSOR_ROW_COUNT-Feld enthält die Anzahl der Zeilen, die bisher abgerufen wurde. Unabhängig davon, welche der Treiber unterstützt **SQLFetchScroll** mit einem *Vorgang* SQL_FETCH_LAST, kann das SQL_DIAG_CURSOR_ROW_COUNT-Feld, um die genaue Zeilenanzahl enthalten.

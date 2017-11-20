---
title: "Daten zu Puffern Länge | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data buffers [ODBC], length
- buffers [ODBC], data
- length of data buffers [ODBC]
- buffers [ODBC], length
ms.assetid: 7288d143-f9e5-4f90-9b31-2549df79c109
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 84bacf4e45760b14515d44a9d81f46de4485ee5f
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="data-buffer-length"></a>Datenlänge für Puffer
Die Anwendung übergibt die Bytelänge des Datenpuffers des Treibers in ein Argument, das mit dem Namen *Pufferlänge* oder einem ähnlichen Namen. Z. B. im folgenden Aufruf **SQLBindCol**, die Anwendung gibt die Länge der *ValuePtr* Puffer (**"sizeof" (***ValuePtr***)**):  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLenOrInd;  
SQLBindCol(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr), &ValueLenOrInd);  
```  
  
 Ein Treiber wird immer die Anzahl der Bytes, nicht die Anzahl von Zeichen, d. h. in den Puffer-Längenargument von jeder Funktion zurückgegeben, die ein Zeichenfolgenargument Ausgabe aufweist.  
  
 Puffer Datenlängen sind nur für Ausgabepuffern erforderlich; der Treiber verwendet diese um zu schreiben, hinter das Ende des Puffers zu vermeiden. Allerdings überprüft der Treiber die Länge des Puffers, nur, wenn der Puffer mit variabler Länge, die Daten, z. B. Zeichen- oder Binärdaten enthält. Wenn der Puffer fester Länge, die Daten, z. B. eine Struktur Ganzzahl- oder Datumsdatentypen enthält wird der Treiber ignoriert die Länge des Puffers und setzt voraus, dass der Puffer groß genug zum Speichern der Daten ist; d. h. schneidet nie Daten fester Länge ab. Es ist wichtig, dass die Anwendung einen ausreichend großen Puffer für Daten fester Länge zu reservieren.  
  
 Tritt bei der ein Abschneiden von nicht-Zeichenfolgen Ausgabe (z. B. der Name des Cursors für zurückgegeben **SQLGetCursorName**), die zurückgegebene Länge in Puffer Length-Argument ist die maximale Zeichenlänge möglich.  
  
 Puffer Datenlängen sind nicht für den Eingabepuffer erforderlich, da der Treiber nicht auf diesen Puffer geschrieben wird.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Anhand der Längenindikator/Werte](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)  
  
-   [Die Länge der Pufferlänge und Abschneiden](../../../odbc/reference/develop-app/data-length-buffer-length-and-truncation.md)  
  
-   [Zeichendaten und C-Zeichenfolgen](../../../odbc/reference/develop-app/character-data-and-c-strings.md)


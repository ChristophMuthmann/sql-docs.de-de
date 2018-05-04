---
title: Konvertieren von Daten von C-in SQL-Datentypen | Microsoft Docs
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
ms.topic: conceptual
helpviewer_keywords:
- converting data from c to SQL types [ODBC], about converting
- converting data from c to SQL types [ODBC]
- data conversions from C to SQL types [ODBC], about converting
- data types [ODBC], C data types
- data types [ODBC], converting data
- SQL data types [ODBC], converting from C types
- data types [ODBC], SQL data types
- data conversions from C to SQL types [ODBC]
- C data types [ODBC], converting to SQL types
ms.assetid: ee0afe78-b58f-4d34-ad9b-616bb23653bd
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4006d78d46168f6f7be272ce3c6e4557f8305b57
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="converting-data-from-c-to-sql-data-types"></a>Konvertieren von Daten von C-in SQL-Datentypen
Wenn eine Anwendung ruft **SQLExecute** oder **SQLExecDirect**, ruft der Treiber die Daten für alle Parameter über gebunden **SQLBindParameter** aus Speicherorte in die Anwendung. Wenn eine Anwendung ruft **SQLSetPos**, der Treiber Ruft die Daten für ein Update oder das Hinzufügen von Spalten mit gebundenen **SQLBindCol**. Für Data-at-Execution-Parameter, die Anwendung sendet die Parameterdaten mit **SQLPutData**. Wenn erforderlich, der Treiber die Daten aus der angegebenen Datentyp konvertiert der *ValueType* Argument in **SQLBindParameter** an der angegebenen Datentyp die *ParameterType*Argument in **SQLBindParameter**, und klicken Sie dann die Daten an die Datenquelle sendet.  
  
 Die folgende Tabelle zeigt die unterstützten Konvertierungen von ODBC C-Datentypen in ODBC-SQL-Datentypen. Ein ausgefüllte Kreis gibt an, die Standard-Konvertierung für einen SQL-Datentyp (C-Datentyp, von dem die Daten werden, wenn konvertiert werden, der Wert der *ValueType* oder das Deskriptorfeld SQL_DESC_CONCISE_TYPE SQL_C_DEFAULT). Ein Kreis gibt eine unterstützte Konvertierung an.  
  
 Das Format der konvertierten Daten wird durch die Einstellung der Windows® Land nicht beeinflusst.  
  
 ![Unterstützte Konvertierungen: ODBC C-in SQL-Datentypen](../../../odbc/reference/appendixes/media/apd1b.gif "apd1b")  
  
 Die Tabellen in den folgenden Abschnitten wird beschrieben, wie konvertiert der Treiber oder die Datenquelle die Daten an die Datenquelle gesendet werden; Treiber sind erforderlich, um Konvertierungen von alle ODBC C-Datentypen in der ODBC-SQL-Datentypen zu unterstützen, die sie unterstützen. Für einen bestimmten ODBC C-Datentyp die erste Spalte der Tabelle die zulässige Eingabewerte von Listet die *ParameterType* Argument in **SQLBindParameter**. Die zweite Spalte enthält die Ergebnisse eines Tests, die der Treiber führt, um zu bestimmen, wenn die Daten konvertiert werden kann. Die dritte Spalte enthält den Wert SQLSTATE zurückgegeben, die für jedes Ergebnis, indem **SQLExecDirect**, **SQLExecute**, **SQLBulkOperations**, **SQLSetPos**, oder **SQLPutData**. Daten werden an die Datenquelle gesendet werden, nur wenn SQL_SUCCESS zurückgegeben wird.  
  
 Wenn die *ParameterType* Argument in **SQLBindParameter** enthält den Bezeichner eines ODBC SQL-Datentyps, die in der Tabelle für einen bestimmten C-Datentyp nicht angezeigt wird **SQLBindParameter**SQLSTATE 07006 zurückgibt (eingeschränkte Datentypattribut). Wenn die *ParameterType* -Argument enthält einen Treiber-spezifische Bezeichner und der Treiber unterstützt nicht die Konvertierung von der spezifische ODBC C-Datentyp in diesen treiberspezifischen SQL-Datentyp, **SQLBindParameter** SQLSTATE HYC00 zurückgibt (optionales Feature nicht implementiert).  
  
 Wenn die *ParameterValuePtr* und *StrLen_or_IndPtr* im angegebenen Argumente **SQLBindParameter** sind beide null-Zeiger, diese Funktion über HY009 SQLSTATE zurückgegeben (ungültige die Verwendung eines null-Zeiger). Auch wenn es nicht in den Tabellen angezeigt wird, wird eine Anwendung legt den Wert des Längen-/Indikatorpuffers verweist, zu der *StrLen_or_IndPtr* Argument **SQLBindParameter** oder der Wert von der  *StrLen_or_IndPtr* Argument **SQLPutData** auf SQL_NULL_DATA, um einen Datenwert NULL SQL anzugeben. (Die *StrLen_or_IndPtr* Argument entspricht dem Feld SQL_DESC_OCTET_LENGTH_PTR in APD.) Die Anwendung wird diese Werte auf SQL_NTS angeben, dass den Wert in \* *ParameterValuePtr* in **SQLBindParameter** oder \* *DataPtr*in **SQLPutData** (verweist das SQL_DESC_DATA_PTR-Feld des APD) ist eine Null-terminierte Zeichenfolge.  
  
 Die folgenden Begriffe werden in den Tabellen verwendet:  
  
-   **Die Bytelänge der Daten** – Anzahl der Bytes der SQL-Daten, die mit der Datenquelle zu senden, und zwar unabhängig davon, ob Daten abgeschnitten werden, bevor sie mit der Datenquelle gesendet wird. Bei Zeichenfolgendaten umfasst dies nicht Speicherplatz für die Null-Abschlusszeichen.  
  
-   **Spalte Bytelänge** – Anzahl der Bytes, die zum Speichern der Daten in der Datenquelle erforderlich sind.  
  
-   **Zeichenlänge des Byte** – maximale Anzahl von Bytes, die zum Anzeigen von Daten in Form von Zeichen erforderlich. Dies ist für jeden SQL-Datentyp in gemäß [Größe anzeigen](../../../odbc/reference/appendixes/display-size.md), außer dass Bytelänge Zeichen in Bytes ist, während die Größe der Anzeige in Zeichen ist.  
  
-   **Anzahl der Ziffern** – Anzahl von Zeichen verwendet, um eine Zahl ist, z. B. das Minuszeichen (-), Dezimaltrennzeichen und einem Exponenten (falls erforderlich) darzustellen.  
  
-   **Wörter im**   
     ***Italics*** – Elemente der SQL-Grammatik. Die Syntax der Grammatikelemente, finden Sie unter [Anhang C: SQL-Grammatik](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md).  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [C to SQL: Character (C zu SQL: Zeichen)](../../../odbc/reference/appendixes/c-to-sql-character.md)  
  
-   [C to SQL: Numeric (C zu SQL: Numerisch)](../../../odbc/reference/appendixes/c-to-sql-numeric.md)  
  
-   [C to SQL: Bit (C zu SQL: Bit)](../../../odbc/reference/appendixes/c-to-sql-bit.md)  
  
-   [C to SQL: Binary (C zu SQL: Binär)](../../../odbc/reference/appendixes/c-to-sql-binary.md)  
  
-   [C to SQL: Date (C zu SQL: Datum)](../../../odbc/reference/appendixes/c-to-sql-date.md)  
  
-   [C to SQL: GUID (C zu SQL: GUID)](../../../odbc/reference/appendixes/c-to-sql-guid.md)  
  
-   [C to SQL: Time (C zu SQL: Zeit)](../../../odbc/reference/appendixes/c-to-sql-time.md)  
  
-   [C to SQL: Timestamp (C zu SQL: Zeitstempel)](../../../odbc/reference/appendixes/c-to-sql-timestamp.md)  
  
-   [C to SQL: Year-Month Intervals (C zu SQL: Jahr-Monat-Intervalle)](../../../odbc/reference/appendixes/c-to-sql-year-month-intervals.md)  
  
-   [C to SQL: Day-Time Intervals (C zu SQL: Taginvervalle)](../../../odbc/reference/appendixes/c-to-sql-day-time-intervals.md)  
  
-   [C to SQL Data Conversion Examples (Beispiele für die Datenkonvertierung von C zu SQL)](../../../odbc/reference/appendixes/c-to-sql-data-conversion-examples.md)

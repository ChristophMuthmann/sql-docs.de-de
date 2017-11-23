---
title: Konvertieren von Daten von SQL-in C-Datentypen | Microsoft Docs
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
- data conversions from SQL to C types [ODBC]
- data conversions from SQL to C types [ODBC], about converting
- data types [ODBC], C data types
- data types [ODBC], converting data
- data types [ODBC], SQL data types
- SQL data types [ODBC], converting to C types
- converting data from SQL to c types [ODBC]
- converting data from SQL to c types [ODBC], about converting
- C data types [ODBC], converting from SQL types
ms.assetid: 029727f6-d3f0-499a-911c-bcaf9714e43b
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0fef5a663ecbb3ec1f162dcf453691f04183d732
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="converting-data-from-sql-to-c-data-types"></a>Konvertieren von Daten von SQL-in C-Datentypen
Wenn eine Anwendung ruft **SQLFetch**, **SQLFetchScroll**, oder **SQLGetData**, ruft der Treiber die Daten aus der Datenquelle. Wenn erforderlich, in dem der Treiber es an der angegebenen Datentyp abgerufen, die Daten vom Datentyp konvertiert die *TargetType* Argument in **SQLBindCol** oder **SQLGetData.** Schließlich speichert die Daten in den Speicherort, auf die *TargetValuePtr* Argument in **SQLBindCol** oder **SQLGetData** (und das SQL_DESC_DATA_PTR-Feld der ARD).  
  
 Die folgende Tabelle zeigt die unterstützten Konvertierungen von ODBC-SQL-Datentypen in ODBC C-Datentypen. Ein ausgefüllte Kreis gibt an, die Standard-Konvertierung für einen SQL-Datentyp (die C-Datentyp, der die Daten werden, wenn konvertiert werden, der Wert der *TargetType* SQL_C_DEFAULT ist). Ein Kreis gibt eine unterstützte Konvertierung an.  
  
 Für eine ODBC 3.*.x* Anwendung arbeiten mit einer ODBC 2.. *X* Treiber, Konvertierung von treiberspezifischen Daten Typen wird möglicherweise nicht unterstützt.  
  
 Das Format der konvertierten Daten wird durch die Einstellung der Windows® Land nicht beeinflusst.  
  
 Die Tabellen in den folgenden Abschnitten wird beschrieben, wie der Treiber oder die Datenquelle aus der Datenquelle abgerufene Daten konvertiert; Treiber sind erforderlich, um Konvertierungen in alle ODBC C-Datentypen von den ODBC-SQL-Datentypen zu unterstützen, die sie unterstützen. Für einen bestimmten ODBC-SQL-Datentyp die erste Spalte der Tabelle die zulässige Eingabewerte von Listet die *TargetType* Argument in **SQLBindCol** und **SQLGetData**. Die zweite Spalte enthält die Ergebnisse eines Tests, die häufig mit der *Pufferlänge* angegebene Argument in **SQLBindCol** oder **SQLGetData**, die der Treiber zum ausführt Bestimmen Sie, ob die Daten zu konvertieren. Für jedes Ergebnis Auflisten der dritten und vierten Spalte die Werte in den Puffern gemäß platziert die *TargetValuePtr* und *StrLen_or_IndPtr* im angegebenen Argumente **SQLBindCol** oder **SQLGetData** nachdem der Treiber versucht hat, um die Daten zu konvertieren. (Die *StrLen_or_IndPtr* Argument entspricht dem Feld SQL_DESC_OCTET_LENGTH_PTR der ARD.) Die letzte Spalte listet zurückgegeben, die für jedes Ergebnis, indem SQLSTATE **SQLFetch**, **SQLFetchScroll**, oder **SQLGetData**.  
  
 Wenn die *TargetType* Argument in **SQLBindCol** oder **SQLGetData** enthält einen Bezeichner für eine ODBC-C-Datentyp, der nicht in der Tabelle für einen bestimmten ODBC-SQL-Datentyp dargestellten  **SQLFetch**, **SQLFetchScroll**, oder **SQLGetData** SQLSTATE 07006 zurückgibt (eingeschränkte Datentypattribut). Wenn die *TargetType* -Argument enthält einen Bezeichner, der eine Konvertierung von einem treiberspezifischen SQL-Datentyp in einen ODBC-C-Datentyp gibt an, und diese Konvertierung wird nicht vom Treiber unterstützt **SQLFetch**, **SQLFetchScroll**, oder **SQLGetData** SQLSTATE HYC00 zurückgibt (optionales Feature nicht implementiert).  
  
 Auch wenn es nicht in den Tabellen angezeigt wird, gibt der Treiber SQL_NULL_DATA im Puffer, die gemäß der *StrLen_or_IndPtr* Argument, wenn der SQL-Datenwert NULL ist. Eine Erläuterung der Verwendung von *StrLen_or_IndPtr* Wenn mehrere Aufrufe zum Abrufen von Daten vorgenommen werden, finden Sie unter der [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)funktionsbeschreibung. Wenn SQL-Daten in C-Zeichendaten konvertiert werden, wird die Anzahl der Zeichen zurückgegeben \* *StrLen_or_IndPtr* enthält keine Null-Terminierung Byte. Wenn *TargetValuePtr* ist ein null-Zeiger **SQLGetData** SQLSTATE HY009 zurückgegeben (Ungültige Verwendung eines null-Zeiger), in **SQLBindCol**, dies hebt die Bindung der Spalte.  
  
 In den Tabellen werden die folgenden Begriffe und Konventionen verwendet:  
  
-   **Die Bytelänge der Daten** ist die Anzahl der Bytes des Datensegments zurückzugebenden in C **TargetValuePtr*, unabhängig davon, ob Daten abgeschnitten werden, bevor sie an die Anwendung zurückgegeben werden. Bei Zeichenfolgendaten umfasst dies nicht den Speicherplatz für die Null-Abschlusszeichen.  
  
-   **Zeichenlänge des Byte** ist die Gesamtzahl der Bytes, die zum Anzeigen der Daten im Zeichenformat benötigt. Dies ist für jede C-Datentyp im Abschnitt definiert [Größe anzeigen](../../../odbc/reference/appendixes/display-size.md), außer dass Bytelänge in Bytes ist, während die Größe der Anzeige in Zeichen ist.  
  
-   Wörter im *Kursiv* Funktionsargumente oder Elemente an die SQL-Grammatik darstellen. Die Syntax der Grammatikelemente, finden Sie unter [Anhang C: SQL-Grammatik](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md).  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [SQL to C: Character (SQL zu C: Zeichen)](../../../odbc/reference/appendixes/sql-to-c-character.md)  
  
-   [SQL to C: Numeric (SQL zu C: Numerisch)](../../../odbc/reference/appendixes/sql-to-c-numeric.md)  
  
-   [SQL to C: Bit (SQL zu C: Bit)](../../../odbc/reference/appendixes/sql-to-c-bit.md)  
  
-   [SQL to C: Binary (SQL zu C: Binär)](../../../odbc/reference/appendixes/sql-to-c-binary.md)  
  
-   [SQL to C: Date (SQL zu C: Datum)](../../../odbc/reference/appendixes/sql-to-c-date.md)  
  
-   [SQL to C: GUID (SQL zu C: GUID)](../../../odbc/reference/appendixes/sql-to-c-guid.md)  
  
-   [SQL to C: Time (SQL zu C: Zeit)](../../../odbc/reference/appendixes/sql-to-c-time.md)  
  
-   [SQL to C: Timestamp (SQL zu C: Zeitstempel)](../../../odbc/reference/appendixes/sql-to-c-timestamp.md)  
  
-   [SQL to C: Year-Month Intervals (SQL zu C: Jahr-Monat-Intervalle)](../../../odbc/reference/appendixes/sql-to-c-year-month-intervals.md)  
  
-   [SQL to C: Day-Time Intervals (SQL zu C: Taginvervalle)](../../../odbc/reference/appendixes/sql-to-c-day-time-intervals.md)  
  
-   [SQL to C Data Conversion Examples (Beispiele für die Datenkonvertierung von SQL zu C)](../../../odbc/reference/appendixes/sql-to-c-data-conversion-examples.md)

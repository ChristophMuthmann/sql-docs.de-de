---
title: SQL in "c:" Tag-Zeitintervalle | Microsoft Docs
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
- converting data from SQL to C types [ODBC], day-time intervals
- day-time intervals [ODBC]
- data conversions from SQL to C types [ODBC], day-time intervals
- intervals [ODBC], converting
ms.assetid: 8ea84d69-2292-4128-89a0-f184f68abb98
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 20021634b3bdb97f8a93048093872015438490d8
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="sql-to-c-day-time-intervals"></a>SQL in "c:" Tag-Zeiträume
Der Bezeichner für die Tag-Zeitintervall ODBC SQL-Datentypen sind:  
  
 SQL_INTERVAL_DAY  
  
 SQL_INTERVAL_DAY_TO_MINUTE  
  
 SQL_INTERVAL_HOUR  
  
 SQL_INTERVAL_DAY_TO_SECOND  
  
 SQL_INTERVAL_MINUTE  
  
 SQL_INTERVAL_HOUR_TO_MINUTE  
  
 SQL_INTERVAL_SECOND  
  
 SQL_INTERVAL_HOUR_TO_SECOND  
  
 SQL_INTERVAL_DAY_TO_HOUR  
  
 SQL_INTERVAL_MINUTE_TO_SECOND  
  
 Die folgende Tabelle zeigt ODBC C-Datentypen in die Tag-Zeitintervall SQL-Daten konvertiert werden kann. Eine Erläuterung der Begriffe in der Tabelle und Spalten, finden Sie unter [Konvertieren von Daten aus SQL in C-Datentypen](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|C-Typ-ID|Test|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|Alle Tag-Time-C-Intervall-Typen|Nachfolgende Felder Teil nicht abgeschnitten.<br /><br /> Nachfolgende Felder Teil abgeschnitten<br /><br /> Führende Genauigkeit des Ziels ist nicht groß genug zum Speichern von Daten aus der Quelle|data<br /><br /> Abgeschnittene Daten<br /><br /> Nicht definiert|Länge der Daten<br /><br /> Länge der Daten<br /><br /> Nicht definiert|–<br /><br /> 01S07<br /><br /> 22015|  
|SQL_C_STINYINT [b] der SQL_C_UTINYINT [b] SQL_C_USHORT [b] SQL_C_SHORT [b] SQL_C_SLONG [b] SQL_C_ULONG [b] SQL_C_NUMERIC [b] SQL_C_BIGINT [b]|Intervall Genauigkeit wurde ein einzelnes Feld und die Daten ohne Abschneiden konvertiert wurde<br /><br /> Intervall Genauigkeit wurde von einem einzelnen Feld und Sekundenbruchteile abgeschnitten<br /><br /> Intervall Genauigkeit wurde ein einzelnes Feld und das gesamte abgeschnittene<br /><br /> Intervall Genauigkeit war es sich nicht um ein einzelnes Feld|data<br /><br /> Abgeschnittene Daten<br /><br /> Abgeschnittene Daten<br /><br /> Nicht definiert|Größe der C-Datentyp<br /><br /> Länge der Daten<br /><br /> Länge der Daten<br /><br /> Größe der C-Datentyp|–<br /><br /> 01S07<br /><br /> 22003<br /><br /> 07006|  
|SQL_C_BINARY|Die Bytelänge der Daten < = *Pufferlänge*<br /><br /> Die Bytelänge der Daten > *Pufferlänge*|data<br /><br /> Nicht definiert|Länge der Daten<br /><br /> Nicht definiert|–<br /><br /> 22003|  
|SQL_C_CHAR|Zeichenlänge des Byte < *Pufferlänge*<br /><br /> Anzahl von ganzen (im Gegensatz zu Sekundenbruchteile) Ziffern < *Pufferlänge*<br /><br /> Anzahl der Ziffern ganze (im Gegensatz zu Sekundenbruchteile) > = *Pufferlänge*|data<br /><br /> Abgeschnittene Daten<br /><br /> Nicht definiert|Größe der C-Datentyp<br /><br /> Größe der C-Datentyp<br /><br /> Nicht definiert|–<br /><br /> 01004<br /><br /> 22003|  
_C_WCHAR|Zeichenlänge des < *Pufferlänge*<br /><br /> Anzahl von ganzen (im Gegensatz zu Sekundenbruchteile) Ziffern < *Pufferlänge*<br /><br /> Anzahl der Ziffern ganze (im Gegensatz zu Sekundenbruchteile) > = *Pufferlänge*|data<br /><br /> Abgeschnittene Daten<br /><br /> Nicht definiert|Größe der C-Datentyp<br /><br /> Größe der C-Datentyp<br /><br /> Nicht definiert|–<br /><br /> 01004<br /><br /> 22003|  
  
 [a] ein-Tag-Zeitintervall SQL-Typ kann in jeden Tag Zeitintervall C-Typ konvertiert werden.  
  
 [b] Wenn die Intervall-Genauigkeit ein einzelnes Feld (einem der Tag, Stunde, MINUTE oder Sekunde) ist, kann das Intervall für den SQL in einer beliebigen exakten numerischen (SQL_C_STINYINT, SQL_C_UTINYINT, SQL_C_USHORT, SQL_C_SHORT, SQL_C_SLONG, SQL_C_ULONG oder SQL_C_NUMERIC) konvertiert werden.  
  
 Die Standard-Konvertierung eines Intervalls SQL-Typ ist in den entsprechenden Datentyp der C-Intervall. Die Anwendung dann bindet die Spalte oder Parameter (oder legt das SQL_DESC_DATA_PTR-Feld in den entsprechenden Datensatz von der ARD), zeigen Sie auf die initialisierte SQL_INTERVAL_STRUCT-Struktur (oder übergibt einen Zeiger auf die SQL_ INTERVAL_STRUCT-Struktur wie die *TargetValuePtr* Argument in einem Aufruf von **SQLGetData**).  
  
 Im folgende Beispiel wird veranschaulicht, wie Daten aus einer Spalte vom Typ SQL_INTERVAL_DAY_TO_MINUTE in der Struktur SQL_INTERVAL_STRUCT übertragen, sodass er als Intervall DAY_TO_HOUR eintrifft.  
  
```  
SQL_INTERVAL_STRUCT is;  
SQLINTEGER    cbValue;  
SQLUINTEGER   days, hours;  
  
// Execute a select statement; "interval_column" is a column  
// whose data type is SQL_INTERVAL_DAY_TO_MINUTE.  
SQLExecDirect(hstmt, "SELECT interval_column FROM table", SQL_NTS);  
  
// Bind  
SQLBindCol(hstmt, 1, SQL_C_INTERVAL_DAY_TO_MINUTE, &is, sizeof(SQL_INTERVAL_STRUCT), &cbValue);  
  
// Fetch  
SQLFetch(hstmt);  
  
// Process data  
days = is.intval.day_second.day;  
hours = is.intval.day_second.hour;  
```

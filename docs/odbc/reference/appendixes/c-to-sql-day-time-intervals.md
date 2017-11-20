---
title: 'C, um SQL: Tag-Zeitintervalle | Microsoft Docs'
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
- day-time intervals [ODBC]
- data conversions from C to SQL types [ODBC], day-time intervals
- converting data from c to SQL types [ODBC], day-time intervals
- intervals [ODBC], converting
ms.assetid: f9ee1ddb-dec7-4f78-b6e2-5ba34e7d6f59
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 61c271a9de10bbc43db116f576b0c34589f899f3
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="c-to-sql-day-time-intervals"></a>C, um SQL: Tag-Zeiträume
Der Bezeichner für die Tag-Zeitintervall ODBC C-Datentypen sind:  
  
 SQL_C_INTERVAL_DAY  
  
 SQL_C_INTERVAL_HOUR  
  
 SQL_C_INTERVAL_MINUTE  
  
 SQL_C_INTERVAL_SECOND  
  
 SQL_C_INTERVAL_DAY_TO_HOUR  
  
 SQL_C_INTERVAL_DAY_TO_MINUTE  
  
 SQL_C_INTERVAL_DAY_TO_SECOND  
  
 SQL_C_INTERVAL_HOUR_TO_MINUTE  
  
 SQL_C_INTERVAL_HOUR_TO_SECOND  
  
 SQL_C_INTERVAL_MINUTE_TO_SECOND  
  
 In der folgenden Tabelle zeigt die ODBC-SQL-Datentypen in die Intervall-C-Daten konvertiert werden kann. Eine Erläuterung der Begriffe in der Tabelle und Spalten, finden Sie unter [Daten von C-in SQL-Datentypen konvertieren](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|SQL-Typ-ID|Test|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR [a]<br /><br /> SQL_VARCHAR [a]<br /><br /> SQL_LONGVARCHAR [a]|Byte-Spaltenlänge > = Byte Zeichenlänge<br /><br /> Spalte Bytelänge < Zeichenlänge Byte [a]<br /><br /> Datenwert ist es sich nicht um ein gültiges Zeichenfolgenliteral Intervall|–<br /><br /> 22001<br /><br /> 22015|  
|SQL_WCHAR [a]<br /><br /> SQL_WVARCHAR [a]<br /><br /> SQL_WLONGVARCHAR [a]|Zeichenlänge Spalte > = Zeichenlänge von Daten<br /><br /> Zeichenlänge der Spalte < Zeichenlänge von Daten [a]<br /><br /> Datenwert ist es sich nicht um ein gültiges Zeichenfolgenliteral Intervall|–<br /><br /> 22001<br /><br /> 22015|  
|SQL_TINYINT [b]<br /><br /> SQL_SMALLINT [b] SQL_INTEGER [b]<br /><br /> SQL_BIGINT [b] SQL_NUMERIC [b]<br /><br /> SQL_DECIMAL [b]|Die Konvertierung eines Intervalls Einzelfeld führten nicht Abschneiden von ganzen Zahlen<br /><br /> Konvertierung Verzeichnisdiensts Abschneiden von ganzen Zahlen|–<br /><br /> 22003|  
|SQL_INTERVAL_DAY<br /><br /> SQL_INTERVAL_HOUR<br /><br /> SQL_INTERVAL_MINUTE<br /><br /> SQL_INTERVAL_SECOND<br /><br /> SQL_INTERVAL_DAY_TO_HOUR<br /><br /> SQL_INTERVAL_DAY_TO_MINUTE<br /><br /> SQL_INTERVAL_DAY_TO_SECOND<br /><br /> SQL_INTERVAL_HOUR_TO_MINUTE<br /><br /> SQL_INTERVAL_HOUR_TO_SECOND<br /><br /> SQL_INTERVAL_MINUTE_TO_SECOND|Datenwert wurde ohne Abschneiden jedes konvertiert.<br /><br /> Ein oder mehrere Felder Datenwerts wurden während der Konvertierung abgeschnitten.|–<br /><br /> 22015|  
  
 [a] alle C-Intervall-Datentypen können in einen Zeichendatentyp konvertiert werden.  
  
 [b] ist das Typfeld in der Struktur Intervall, für die das Intervall ein einzelnes Feld (SQL_DAY, SQL_HOUR, SQL_MINUTE oder SQL_SECOND) entspricht, kann das Intervall C-Typ in einer beliebigen exakten numerischen (SQL_TINYINT SQL_SMALLINT, SQL_INTEGER, SQL_BIGINT konvertiert werden SQL_DECIMAL oder SQL_NUMERIC).  
  
 Die Standard-Konvertierung von C Intervalltyp werden das entsprechende Tag-Zeitintervall SQL-Typ ab.  
  
 Der Treiber ignoriert den Längenindikator /-Wert, wenn Daten aus dem Intervall C-Datentyp zu konvertieren und setzt voraus, dass die Größe des Datenpuffers die Größe des Intervalls C-Datentyp ist. Der Längenindikator /-Wert übergeben der *StrLen_or_Ind* Argument in **SQLPutData** und in den Puffer mit angegebenen der *StrLen_or_IndPtr* Argument in **SQLBindParameter**. Datenpuffer wird angegeben, mit der *DataPtr* Argument in **SQLPutData** und die *ParameterValuePtr* Argument in **SQLBindParameter**.  
  
 Im folgenden Beispiel wird veranschaulicht, wie zum Senden von C Intervalldaten, die in der SQL_INTERVAL_STRUCT-Struktur in eine Datenbankspalte gespeichert wird. Die Intervall-Struktur enthält ein Intervall DAY_TO_SECOND; Es wird in einer Datenbankspalte vom Typ SQL_INTERVAL_DAY_TO_MINUTE gespeichert werden.  
  
```  
SQL_INTERVAL_STRUCT is;  
SQLINTEGER cbValue;  
  
// Initialize the interval struct to contain the DAY_TO_SECOND  
// interval "154 days, 22 hours, 44 minutes, and 10 seconds"  
is.intval.day_second.day      = 154;  
is.intval.day_second.hour     = 22;  
is.intval.day_second.minute   = 44;  
is.intval.day_second.second   = 10;  
is.interval_sign              = SQL_FALSE;  
  
// Bind the dynamic parameter  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_INTERVAL_DAY_TO_SECOND,  
                  SQL_INTERVAL_DAY_TO_MINUTE, 0, 0, &is,  
                  sizeof(SQL_INTERVAL_STRUCT), &cbValue);  
  
// Execute an insert statement; "interval_column" is a column  
// whose data type is SQL_INTERVAL_DAY_TO_MINUTE.  
SQLExecDirect(hstmt,"INSERT INTO table(interval_column) VALUES (?)",SQL_NTS);  
```


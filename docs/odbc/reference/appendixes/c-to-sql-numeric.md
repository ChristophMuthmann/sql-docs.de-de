---
title: 'C, um SQL: numerische | Microsoft Docs'
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
- numeric data type [ODBC], converting
- data conversions from C to SQL types [ODBC], numeric
- converting data from c to SQL types [ODBC], numeric
ms.assetid: af4095ff-06c3-4b04-83bf-19f9ee098dc2
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 788a317dc58eaa83b0caadd3d2a6c02d49398d7c
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="c-to-sql-numeric"></a>C, um SQL: numerische
Der Bezeichner für die numerische ODBC C-Datentypen sind:  
  
 SQL_C_STINYINT  
  
 SQL_C_SLONG  
  
 SQL_C_UTINYINT  
  
 SQL_C_ULONG  
  
 SQL_C_TINYINT  
  
 SQL_C_LONG  
  
 SQL_C_SSHORT  
  
 SQL_C_FLOAT  
  
 SQL_C_USHORT  
  
 SQL_C_DOUBLE  
  
 SQL_C_SHORT  
  
 SQL_C_NUMERIC  
  
 SQL_C_SBIGINT  
  
 SQL_C_UBIGINT  
  
 In der folgenden Tabelle zeigt die ODBC-SQL-Datentypen, die in die numerische C-Daten konvertiert werden können. Eine Erläuterung der Begriffe in der Tabelle und Spalten, finden Sie unter [Daten von C-in SQL-Datentypen konvertieren](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|SQL-Typ-ID|Test|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|Anzahl der Ziffern < = Byte Spaltenlänge<br /><br /> Anzahl der Ziffern > Byte Spaltenlänge|–<br /><br /> 22001|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|Anzahl der Zeichen < Zeichen Spaltenlänge =<br /><br /> Anzahl der Zeichen > Spalte Zeichenlänge|–<br /><br /> 22001|  
|SQL_DECIMAL [b]<br /><br /> SQL_NUMERIC [b]<br /><br /> SQL_TINYINT [b]<br /><br /> SQL_SMALLINT [b]<br /><br /> SQL_INTEGER [b]<br /><br /> SQL_BIGINT [b]|Daten konvertiert werden, ohne abgeschnitten oder mit Nachkommastellen abgeschnitten<br /><br /> Daten, die mit Abschneiden von ganzen Zahlen konvertiert|–<br /><br /> 22003|  
|SQL_REAL<br /><br /> SQL_FLOAT<br /><br /> SQL_DOUBLE|Daten werden innerhalb des Bereichs des Datentyps, der die Anzahl konvertiert wird<br /><br /> Daten sind außerhalb des Bereichs des Datentyps, der die Anzahl konvertiert wird|–<br /><br /> 22003|  
|SQL_BIT|Daten sind 0 oder 1<br /><br /> Daten sind größer als 0 (null) kleiner als 2, und nicht gleich 1<br /><br /> Daten ist kleiner als 0 oder größer als oder gleich 2|–<br /><br /> 22001<br /><br /> 22003|  
|SQL_INTERVAL_YEAR [a]<br /><br /> SQL_INTERVAL_MONTH [a]<br /><br /> SQL_INTERVAL_DAY [a]<br /><br /> SQL_INTERVAL_HOUR [a]<br /><br /> SQL_INTERVAL_MINUTE [a]<br /><br /> SQL_INTERVAL_SECOND [a]|Die Daten nicht abgeschnitten.<br /><br /> Daten wurden abgeschnitten.|–<br /><br /> 22015|  
  
 [a] diese Konvertierungen werden nur für die genaue numerische Datentypen (SQL_C_STINYINT, SQL_C_UTINYINT, SQL_C_SSHORT, SQL_C_USHORT, SQL_C_SLONG, SQL_C_ULONG oder SQL_C_NUMERIC) unterstützt. Sie sind nicht für die ungefähre numerische Datentypen (SQL_C_FLOAT oder SQL_C_DOUBLE) unterstützt. Genaue numerische C-Datentypen können nicht auf ein Intervall SQL-Typ konvertiert werden, deren Genauigkeit Intervall kein einzelnes Datenfeld ist.  
  
 [b] für den Fall "n/v" kann ein Treiber optional zurückgeben, SQL_SUCCESS_WITH_INFO und 01S07 Wenn Sekundenbruchteile abgeschnitten sind.  
  
 Der Treiber ignoriert den Längenindikator /-Wert, wenn Daten aus der numerischen C-Datentypen konvertieren und wird davon ausgegangen, dass die Größe des Datenpuffers die Größe des numerischen Datentyps C. Der Längenindikator /-Wert übergeben der *StrLen_or_Ind* Argument in **SQLPutData** und in den Puffer mit angegebenen der *StrLen_or_IndPtr* Argument in **SQLBindParameter**. Datenpuffer wird angegeben, mit der *DataPtr* Argument in **SQLPutData** und die *ParameterValuePtr* Argument in **SQLBindParameter**.

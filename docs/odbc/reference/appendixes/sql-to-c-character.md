---
title: SQL in "c:" Zeichen | Microsoft Docs
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
- converting data from SQL to C types [ODBC], character
- character data type [ODBC]
- data conversions from SQL to C types [ODBC], character
ms.assetid: 7fdb7f38-b64d-48f2-bcb4-1ca96b2bbdb6
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3ba39caca1a4ad37437f35918545ed54a5dd2266
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sql-to-c-character"></a>SQL in "c:"-Zeichen
Der Bezeichner für die ODBC-SQL-Zeichendatentypen sind:  
  
 SQL_CHAR  
  
 SQL_VARCHAR  
  
 SQL_LONGVARCHAR  
  
 SQL_WCHAR  
  
 SQL_WVARCHAR  
  
 SQL_WLONGVARCHAR  
  
 Die folgende Tabelle zeigt ODBC C-Datentypen in die SQL-Zeichendaten konvertiert werden können. Eine Erläuterung der Begriffe in der Tabelle und Spalten, finden Sie unter [Konvertieren von Daten aus SQL in C-Datentypen](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|C-Typ-ID|Test|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|Die Bytelänge der Daten < *Pufferlänge*<br /><br /> Die Bytelänge der Daten > = *Pufferlänge*|data<br /><br /> Abgeschnittene Daten|Länge der Daten in bytes<br /><br /> Länge der Daten in bytes|–<br /><br /> 01004|  
|SQL_C_WCHAR|Zeichenlänge von Daten < *Pufferlänge*<br /><br /> Zeichenlänge von Daten > = *Pufferlänge*|data<br /><br /> Abgeschnittene Daten|Länge der Daten in Zeichen<br /><br /> Länge der Daten in Zeichen|–<br /><br /> 01004|  
|SQL_C_STINYINT SQL_C_UTINYINT SQL_C_TINYINT SQL_C_SBIGINT SQL_C_UBIGINT SQL_C_SSHORT SQL_C_USHORT SQL_C_SHORT SQL_C_SLONG SQL_C_ULONG SQL_C_LONG SQL_C_NUMERIC|Daten konvertiert werden, ohne Abschneiden [b]<br /><br /> Daten konvertiert, wobei das Abschneiden von Dezimalstellen [a]<br /><br /> Konvertierung von Daten führt zu einem Verlust von ganzen (im Gegensatz zu Sekundenbruchteile) Ziffern [a]<br /><br /> Daten sind ein *numerische Literal*[b] '.|data<br /><br /> Abgeschnittene Daten<br /><br /> Nicht definiert<br /><br /> Nicht definiert|Anzahl der Bytes der C-Datentyp<br /><br /> Anzahl der Bytes der C-Datentyp<br /><br /> Nicht definiert<br /><br /> Nicht definiert|–<br /><br /> 01S07<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_FLOAT SQL_C_DOUBLE|Daten sind innerhalb des Bereichs des Datentyps in den die Anzahl konvertiert [a]<br /><br /> Daten sind außerhalb des Bereichs des Datentyps in den die Anzahl konvertiert [a]<br /><br /> Daten sind ein *numerische Literal*[b] '.|data<br /><br /> Nicht definiert<br /><br /> Nicht definiert|Größe der C-Datentyp<br /><br /> Nicht definiert<br /><br /> Nicht definiert|–<br /><br /> 22003<br /><br /> 22018|  
_C_BIT|Daten sind 0 oder 1<br /><br /> Daten sind größer als 0 (null) kleiner als 2, und nicht gleich 1<br /><br /> Daten ist kleiner als 0 oder größer als oder gleich 2<br /><br /> Daten sind ein *numerische Literal*|data<br /><br /> Abgeschnittene Daten<br /><br /> Nicht definiert<br /><br /> Nicht definiert|1 [b]<br /><br /> 1 [b]<br /><br /> Nicht definiert<br /><br /> Nicht definiert|–<br /><br /> 01S07<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_BINARY|Die Bytelänge der Daten < = *Pufferlänge*<br /><br /> Die Bytelänge der Daten > *Pufferlänge*|data<br /><br /> Abgeschnittene Daten|Länge der Daten in bytes<br /><br /> Länge der Daten|–<br /><br /> 01004|  
|SQL_C_TYPE_DATE|Datenwert ist ein gültiger *Datumswert*[a]<br /><br /> Datenwert ist ein gültiger *Timestamp-Wert*; Uhrzeitteil ist 0 (null) [a]<br /><br /> Datenwert ist ein gültiger *Timestamp-Wert*; Uhrzeitteil ist ungleich Null [a], [c]<br /><br /> Datenwert ist kein gültiger *Datumswert* oder *Timestamp-Wert*[a]|data<br /><br /> data<br /><br /> Abgeschnittene Daten<br /><br /> Nicht definiert|6 [b]<br /><br /> 6 [b]<br /><br /> 6 [b]<br /><br /> Nicht definiert|–<br /><br /> –<br /><br /> 01S07<br /><br /> 22018|  
|SQL_C_TYPE_TIME|Datenwert ist ein gültiger *Zeit-Wert und die Sekundenbruchteile, 0 wird*[a]<br /><br /> Datenwert ist ein gültiger *Timestamp-Wert oder ein gültiger Zeitwert*; Bruchteilen Sekundenangabe ist 0 (null) [a] [d]<br /><br /> Datenwert ist ein gültiger *Timestamp-Wert*; Bruchteilen Sekundenangabe ist ungleich Null [a] [d], [e]<br /><br /> Datenwert ist kein gültiger *Zeitwert* oder *Timestamp-Wert*[a]|data<br /><br /> data<br /><br /> Abgeschnittene Daten<br /><br /> Nicht definiert|6 [b]<br /><br /> 6 [b]<br /><br /> 6 [b]<br /><br /> Nicht definiert|–<br /><br /> –<br /><br /> 01S07<br /><br /> 22018|  
_C_TYPE_TIMESTAMP|Datenwert ist ein gültiger *Timestamp-Wert oder ein gültiger Zeitwert*; Bruchteilen Sekundenangabe nicht abgeschnitten, [a]<br /><br /> Datenwert ist ein gültiger *Timestamp-Wert oder ein gültiger Zeitwert*; Bruchteilen Sekundenangabe abgeschnitten, [a]<br /><br /> Datenwert ist ein gültiger *Datumswert*[a]<br /><br /> Datenwert ist ein gültiger *Zeitwert*[a]<br /><br /> Datenwert ist kein gültiger *Datumswert*, *Zeitwert*, oder *Timestamp-Wert*[a]|data<br /><br /> Abgeschnittene Daten<br /><br /> Daten [f#]<br /><br /> Daten [g]<br /><br /> Nicht definiert|16 [b]<br /><br /> 16 [b]<br /><br /> 16 [b]<br /><br /> 16 [b]<br /><br /> Nicht definiert|–<br /><br /> 01S07<br /><br /> –<br /><br /> –<br /><br /> 22018|  
|Alle C-Intervall-Typen|Datenwert ist ein gültiger *Intervallwert*; keine Kürzung<br /><br /> Datenwert ist ein gültiger *Intervallwert*; Abschneiden von ein oder mehrere nachfolgende Felder<br /><br /> Daten sind gültige Intervall; Feld erhebliche Genauigkeit für anführenden ist verloren gegangen<br /><br /> Der Datenwert ist kein gültiges Intervallwert|data<br /><br /> Abgeschnittene Daten<br /><br /> Nicht definiert<br /><br /> Nicht definiert|Länge der Daten in bytes<br /><br /> Länge der Daten in bytes<br /><br /> Nicht definiert<br /><br /> Nicht definiert|–<br /><br /> 01S07<br /><br /> 22015<br /><br /> 22018|  
  
 [a] der Wert der *Pufferlänge* für diese Konvertierung ignoriert wird. Der Treiber setzt voraus, dass die Größe der **TargetValuePtr* ist die Größe der C-Datentyp.  
  
 [b] Dies ist die Größe des entsprechenden C-Datentyp.  
  
 [c] den Zeitbereich der *Timestamp-Wert* wird abgeschnitten.  
  
 [d] der Date-Teil der *Timestamp-Wert* wird ignoriert.  
  
 [e] der Sekundenbruchteile des Zeitstempels wird abgeschnitten.  
  
 [f# der timestampstruktur] Zeitfelder werden auf 0 (null) festgelegt.  
  
 [g der timestampstruktur] Datumsfelder werden auf das aktuelle Datum festgelegt.  
  
 Wenn SQL-Zeichendaten in numerische konvertiert werden, werden die Datums-, Zeit-, Timestamp, oder Intervall C, führende und nachfolgende Leerzeichen ignoriert.


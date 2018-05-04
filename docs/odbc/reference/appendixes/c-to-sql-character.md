---
title: 'C, um SQL: Zeichen | Microsoft Docs'
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
- character data type [ODBC]
- data conversions from C to SQL types [ODBC], character
- converting data from c to SQL types [ODBC], character
ms.assetid: be66188a-ebdb-4c9e-af72-c379886766fa
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d104581a54a16064eec791ad3419770b1538ff1e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="c-to-sql-character"></a>C, um SQL: Zeichen
Der Bezeichner für das Zeichen ODBC C-Datentyp sind:  
  
 SQL_C_CHAR  
  
 SQL_C_WCHAR  
  
 In der folgenden Tabelle zeigt die ODBC-SQL-Datentypen, die in die C-Zeichendaten konvertiert werden können. Eine Erläuterung der Begriffe in der Tabelle und Spalten, finden Sie unter [Daten von C-in SQL-Datentypen konvertieren](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
> [!NOTE]  
>  Wenn Zeichendaten C in Unicode SQL-Daten konvertiert werden, muss die Länge der Unicode-Daten eine gerade Zahl sein.  
  
|SQL-Typ-ID|Test|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|Die Bytelänge der Daten < = Spaltenlänge.<br /><br /> Die Bytelänge der Daten > Spaltenlänge.|–<br /><br /> 22001|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|Zeichenlänge von Daten < = Spaltenlänge.<br /><br /> Zeichenlänge von Daten > Spaltenlänge.|–<br /><br /> 22001|  
|SQL_DECIMAL<br /><br /> SQL_NUMERIC<br /><br /> SQL_TINYINT<br /><br /> SQL_SMALLINT<br /><br /> SQL_INTEGER SQL_BIGINT|Daten, die konvertiert werden, ohne abgeschnitten<br /><br /> Daten konvertiert, wobei das Abschneiden von Dezimalstellen [e]<br /><br /> Konvertierung von Daten führt zu einem Verlust von ganzen (im Gegensatz zu Sekundenbruchteile) Ziffern [e]<br /><br /> Datenwert ist eine *numerische Literal*|–<br /><br /> 22001<br /><br /> 22001<br /><br /> 22018|  
|SQL_REAL<br /><br /> SQL_FLOAT<br /><br /> SQL_DOUBLE|Daten werden innerhalb des Bereichs des Datentyps, der die Anzahl konvertiert wird<br /><br /> Daten sind außerhalb des Bereichs des Datentyps, der die Anzahl konvertiert wird<br /><br /> Datenwert ist eine *numerische Literal*|–<br /><br /> 22003<br /><br /> 22018|  
|SQL_BIT|Daten sind 0 oder 1<br /><br /> Daten sind größer als 0 (null) kleiner als 2, und nicht gleich 1<br /><br /> Daten ist kleiner als 0 oder größer als oder gleich 2<br /><br /> Daten sind ein *numerische Literal*|–<br /><br /> 22001<br /><br /> 22003<br /><br /> 22018|  
|SQL_BINARY<br /><br /> SQL_VARBINARY<br /><br /> SQL_LONGVARBINARY|(Bytelänge der Daten) / 2 < = Byte Spaltenlänge<br /><br /> (Bytelänge der Daten) / 2 > Byte Spaltenlänge<br /><br /> Datenwert ist nicht mit einem hexadezimalen Wert|–<br /><br /> 22001<br /><br /> 22018|  
|SQL_TYPE_DATE|Datenwert ist ein gültiger *ODBC-Datum-Literal*<br /><br /> Datenwert ist ein gültiger *ODBC-Zeitstempel-Literal*; Uhrzeitteil ist 0 (null)<br /><br /> Datenwert ist ein gültiger *ODBC-Zeitstempel-Literal*; Uhrzeitteil ist ungleich Null [a]<br /><br /> Datenwert ist kein gültiger *ODBC-Datum-Literal* oder *ODBC-Zeitstempel-Literal*|–<br /><br /> –<br /><br /> 22008<br /><br /> 22018|  
|SQL_TYPE_TIME|Datenwert ist ein gültiger *ODBC-Uhrzeit-Literal*<br /><br /> Datenwert ist ein gültiger *ODBC-Zeitstempel-Literal*; Bruchteilen Sekundenangabe ist 0 (null) [b]<br /><br /> Datenwert ist ein gültiger *ODBC-Zeitstempel-Literal*; Bruchteilen Sekundenangabe ist ungleich Null [b]<br /><br /> Datenwert ist kein gültiger *ODBC-Uhrzeit-Literal* oder *ODBC-Zeitstempel-Literal*|–<br /><br /> –<br /><br /> 22008<br /><br /> 22018|  
|SQL_TYPE_TIMESTAMP|Datenwert ist ein gültiger *ODBC-Zeitstempel-Literal*; Bruchteilen Sekundenangabe nicht abgeschnitten.<br /><br /> Datenwert ist ein gültiger *ODBC-Zeitstempel-Literal*; Nachkommastellen abgeschnitten Sekundenangabe<br /><br /> Datenwert ist ein gültiger *ODBC-Datum-Literal*[c]<br /><br /> Datenwert ist ein gültiger *ODBC-Uhrzeit-Literal*[d]<br /><br /> Datenwert ist kein gültiger *ODBC-Datum-Literal*, *ODBC-Uhrzeit-Literal*, oder *ODBC-Zeitstempel-Literal*|–<br /><br /> 22008<br /><br /> –<br /><br /> –<br /><br /> 22018|  
|Alle SQL-Intervall-Typen|Datenwert ist ein gültiger *Intervallwert*; keine Kürzung<br /><br /> Datenwert ist ein gültiger *Intervallwert*; der Wert in eines der Felder wird abgeschnitten.<br /><br /> Der Datenwert ist ein gültiges Zeichenfolgenliteral Intervall|–<br /><br /> 22015<br /><br /> 22018|  
  
 [a] den Uhrzeitteil des Zeitstempels wird abgeschnitten.  
  
 [b] der Datumsteil des Zeitstempels wird ignoriert.  
  
 [c] den Uhrzeitteil des Zeitstempels wird auf 0 (null) festgelegt.  
  
 [d] der Datumsteil des Zeitstempels wird auf das aktuelle Datum festgelegt.  
  
 [e] die Treiber/Datenquelle effektiv wartet, bis die gesamte Zeichenfolge empfangen wurden (auch wenn die Zeichendaten in Teilen, durch Aufrufe von gesendet werden **SQLPutData**) vor dem Durchführen der Konvertierung.  
  
 Wenn Zeichendaten C konvertierte numerischen, Datums-, Uhrzeit oder Zeitstempel SQL-Daten ist, werden führende und nachfolgende Leerzeichen ignoriert.  
  
 Wenn Zeichendaten C in SQL-Binärdaten konvertiert werden, werden jeweils zwei Byte von Zeichendaten in ein einzelnes Byte (8 Bit) von Binärdaten konvertiert. Eine Zahl in hexadezimaler Form darstellen, jeweils zwei Byte Zeichendaten. Beispielsweise ist "01" in eine binäre 00000001 konvertiert und "FF" in eine binäre 11111111 konvertiert wird.  
  
 Der Treiber immer Paare von Hexadezimalziffern auf einzelne Bytes konvertiert und ignoriert das Null-Terminierung Byte. Wenn die Länge der Zeichenfolge ungerade ist, ist, wird das letzte Byte der Zeichenfolge (ohne das Null-Terminierung Byte, sofern vorhanden) aus diesem Grund nicht konvertiert.  
  
> [!NOTE]  
>  Anwendungsentwickler sind davon abgeraten, Binden von C-Zeichendaten in einen binären SQL-Datentyp. Diese Konvertierung ist in der Regel ineffizient und zeitaufwändig.

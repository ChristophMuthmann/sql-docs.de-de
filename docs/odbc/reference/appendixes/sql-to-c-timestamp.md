---
title: SQL in "c:" Timestamp | Microsoft Docs
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
- timestamp data type [ODBC]
- converting data from SQL to C types [ODBC], timestamp
- data conversions from SQL to C types [ODBC], timestamp
ms.assetid: 6a0617cf-d8c0-4316-8bb4-e6ddb45d7bf1
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a551d51a434d17162a5f5bcf0091e593d25f283a
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sql-to-c-timestamp"></a>SQL in "c:" Timestamp
Der Bezeichner für den Timestamp ODBC SQL-Datentyp ist:  
  
 SQL_TYPE_TIMESTAMP  
  
 In der folgenden Tabelle wird gezeigt, auf den ODBC C-Datentypen, die in die Timestamp-SQL-Datentyp konvertiert werden können. Eine Erläuterung der Begriffe in der Tabelle und Spalten, finden Sie unter [Konvertieren von Daten aus SQL in C-Datentypen](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|C-Typ-ID|Test|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*Pufferlänge* > Byte Zeichenlänge<br /><br /> 20 < = *Pufferlänge* < = Byte Zeichenlänge<br /><br /> *Pufferlänge* < 20|data<br /><br /> Abgeschnittene Daten [b]<br /><br /> Nicht definiert|Länge der Daten in bytes<br /><br /> Länge der Daten in bytes<br /><br /> Nicht definiert|–<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*Pufferlänge* > Zeichenlänge<br /><br /> 20 < = *Pufferlänge* < = Zeichenlänge<br /><br /> *Pufferlänge* < 20|data<br /><br /> Abgeschnittene Daten [b]<br /><br /> Nicht definiert|Länge der Daten in Zeichen<br /><br /> Länge der Daten in Zeichen<br /><br /> Nicht definiert|–<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|Die Bytelänge der Daten < = *Pufferlänge*<br /><br /> Die Bytelänge der Daten > *Pufferlänge*|data<br /><br /> Nicht definiert|Länge der Daten in bytes<br /><br /> Nicht definiert|–<br /><br /> 22003|  
|SQL_C_TYPE_DATE|Time-Teil des Zeitstempels ist 0 (null) [a]<br /><br /> Time-Teil des Zeitstempels ist ungleich Null [a]|data<br /><br /> Abgeschnittene Daten [c#]|6 [f#]<br /><br /> 6 [f#]|–<br /><br /> 01S07|  
|SQL_C_TYPE_TIME|Sekundenbruchteile von Timestamp ist 0 (null) [a]<br /><br /> Sekundenbruchteile von Timestamp ist ungleich Null [a]|Daten [d]<br /><br /> Abgeschnittene Daten [d], [e]|6 [f#]<br /><br /> 6 [f#]|–<br /><br /> 01S07|  
_C_TYPE_TIMESTAMP|Sekundenbruchteile von Timestamp wird nicht abgeschnitten, [a]<br /><br /> Sekundenbruchteile von Timestamp wird abgeschnitten, [a]|Daten [e]<br /><br /> Abgeschnittene Daten [e]|16 [f#]<br /><br /> 16 [f#]|–<br /><br /> 01S07|  
  
 [a] der Wert der *Pufferlänge* für diese Konvertierung ignoriert wird. Der Treiber setzt voraus, dass die Größe der **TargetValuePtr* ist die Größe der C-Datentyp.  
  
 [b] die Sekundenbruchteile des Zeitstempels werden abgeschnitten.  
  
 [c] den Uhrzeitteil des Zeitstempels wird abgeschnitten.  
  
 [d] der Datumsteil des Zeitstempels wird ignoriert.  
  
 [e] der Sekundenbruchteile des Zeitstempels wird abgeschnitten.  
  
 [f] Dies ist die Größe des entsprechenden C-Datentyp.  
  
 Wenn SQL-Zeitstempeldaten in C-Zeichendaten konvertiert werden, wird die resultierende Zeichenfolge der "*Yyyy*-*mm*-*Dd* *" hh "* :*mm*:*ss*[. *f...* ] "-Format, in denen bis zu neun Ziffern für Sekundenbruchteile verwendet werden kann. Dieses Format wird durch die Einstellung der Windows® Land nicht beeinflusst. (Mit Ausnahme des Dezimaltrennzeichen und Bruchteilen von Sekunden, muss die gesamte Format, unabhängig von der Genauigkeit von der SQL-Datentyp Timestamp verwendet werden.)


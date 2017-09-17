---
title: 'C, um SQL: Timestamp | Microsoft Docs'
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
- data conversions from C to SQL types [ODBC], timestamp
- timestamp data type [ODBC]
- converting data from c to SQL types [ODBC], timestamp
ms.assetid: 0e08bfff-68f9-4648-9558-09b57fea08ad
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bbb6396dc1a49d984834ec6f105b3a9ba42d95c4
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="c-to-sql-timestamp"></a>C, um SQL: Timestamp
Der Bezeichner für den Timestamp ODBC C-Datentyp ist:  
  
 SQL_C_TYPE_TIMESTAMP  
  
 In der folgenden Tabelle wird gezeigt, auf die ODBC-SQL-Datentypen in die Timestamp-C-Datentyp konvertiert werden kann. Eine Erläuterung der Begriffe in der Tabelle und Spalten, finden Sie unter [Daten von C-in SQL-Datentypen konvertieren](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|SQL-Typ-ID|Test|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|Byte-Spaltenlänge > = Byte Zeichenlänge<br /><br /> 19 < Byte Spaltenlänge = < Byte Zeichenlänge<br /><br /> Spalte Byte Länge < 19<br /><br /> Datenwert ist es sich nicht um einen gültigen Zeitstempel an|–<br /><br /> 22001<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|Zeichenlänge Spalte > = Zeichenlänge von Daten<br /><br /> 19 < Zeichen Spaltenlänge = < Zeichenlänge von Daten<br /><br /> Spalte Zeichen Länge < 19<br /><br /> Datenwert ist es sich nicht um einen gültigen Zeitstempel an|–<br /><br /> 22001<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_DATE|Time-Felder sind 0 (null)<br /><br /> Zeitfelder werden ungleich null<br /><br /> Datenwert enthält kein gültiges Datum|–<br /><br /> 22008<br /><br /> 22007|  
|SQL_TYPE_TIME|Felder für Sekundenbruchteile sind 0 (null) [a]<br /><br /> Felder für Sekundenbruchteile sind ungleich Null [a]<br /><br /> Datenwert enthält keine gültige Zeit|–<br /><br /> 22008<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|Felder für Sekundenbruchteile werden nicht abgeschnitten.<br /><br /> Felder für Sekundenbruchteile werden abgeschnitten.<br /><br /> Datenwert ist es sich nicht um einen gültigen Zeitstempel an|–<br /><br /> 22008<br /><br /> 22007|  
  
 [a] das Datum, die Felder der zeitstempelstruktur ignoriert werden.  
  
 Informationen, welche Werte in einer Struktur SQL_C_TIMESTAMP gültig sind, finden Sie unter [C-Datentypen](../../../odbc/reference/appendixes/c-data-types.md)weiter oben in diesem Anhang.  
  
 Wenn Zeitstempeldaten C in SQL-Zeichendaten konvertiert werden, werden die resultierende Zeichendaten der "*Yyyy*-*mm*-*Dd* *"hh"*:*mm*:*ss*[.* f... *] "Format.  
  
 Der Treiber ignoriert den Längenindikator /-Wert, wenn Daten aus der C-Timestamp-Datentyp zu konvertieren und wird davon ausgegangen, dass die Größe des Datenpuffers die Größe des C-Timestamp-Datentyps. Der Längenindikator /-Wert übergeben der *StrLen_or_Ind* Argument in **SQLPutData** und in den Puffer mit angegebenen der *StrLen_or_IndPtr* Argument in **SQLBindParameter**. Datenpuffer wird angegeben, mit der *DataPtr* Argument in **SQLPutData** und die *ParameterValuePtr* Argument in **SQLBindParameter**.

---
title: Spaltengröße | Microsoft Docs
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
ms.topic: article
helpviewer_keywords:
- data types [ODBC], column size
- size of data types [ODBC]
- SQL data types [ODBC], column characteristics
- column size of data types [ODBC]
ms.assetid: 541b83ab-b16d-4714-bcb2-3c3daa9a963b
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2178697aef549d86fedfa3d4bb70c8b45ba1f68e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="column-size"></a>Spaltengröße
Die Spalte (oder Parameter) Größe des numerischen Datentypen wird als die maximale Anzahl von Ziffern nach dem Datentyp der Spalte oder Parameter oder die Genauigkeit der Daten definiert. Für Zeichentypen entspricht ist dies die Länge in Zeichen der Daten. für binäre Datentypen wird die Spaltengröße als die Länge in Bytes der Daten definiert. Für die Zeit, Timestamp und alle Intervalldatentypen ist dies die Anzahl der Zeichen in die zeichendarstellung dieser Daten. Die Größe der Spalte für jeden präzise SQL-Datentyp definiert ist in der folgenden Tabelle gezeigt.  
  
|SQL-Typ-ID|Spaltengröße|  
|-------------------------|-----------------|  
|Alle Typen mit Zeichen [a] [b] '.|Die definierten oder maximale Spaltenlänge Größe in Zeichen der Spalte oder des Parameters (wie in der SQL_DESC_LENGTH Deskriptorfeld enthalten). Die Spaltengröße einer Single-Byte-Zeichen-Spalte als CHAR(10) definiert ist z. B. 10.|  
|SQL_DECIMAL SQL_NUMERIC|Die festgelegte Anzahl von Ziffern. Die Genauigkeit einer Spalte, die als "NUMERIC(10,3)" definiert ist z. B. 10.|  
|SQL_BIT [c]|1|  
|SQL_TINYINT [c]|3|  
|SQL_SMALLINT [c]|5|  
|SQL_INTEGER [c]|10|  
|SQL_BIGINT [c]|19 (sofern signiert) oder 20 (falls ohne Vorzeichen)|  
|SQL_REAL [c]|7|  
|SQL_FLOAT [c]|15|  
|SQL_DOUBLE [c]|15|  
|Alle binären Typen [a] [b].|Die definierten oder maximale Länge in Bytes der Spalte oder des Parameters. Die Länge einer Spalte, die als "("Binary(10)")." definiert ist z. B. 10.|  
|SQL_TYPE_DATE [c]|10 (die Anzahl der Zeichen in der *jjjj-mm-tt* Format).|  
|SQL_TYPE_TIME [c]|8 (die Anzahl der Zeichen in der *Hh-mm-ss* Format), oder 9 + *s* (die Anzahl der Zeichen in der *hh: mm:*[ss.fff...]-Format, in dem *s*Sekunden Genauigkeit).|  
|SQL_TYPE_TIMESTAMP|16 (die Anzahl der Zeichen in der *jjjj-mm-tt hh: mm* Format)<br /><br /> 19 (die Anzahl der Zeichen in der *jjjj-mm-tt* *hh: mm:* Format)<br /><br /> oder<br /><br /> 20 + *s* (die Anzahl der Zeichen in der *jjjj-mm-tt hh: mm:*[ss.fff...]-Format, in dem *s* Sekunden Genauigkeit).|  
|SQL_INTERVAL_SECOND|Wobei *p* ist die Genauigkeit für anführenden Intervallwert und *s* ist die Genauigkeit Sekunden *p* (Wenn *s*= 0) oder *p* + *s*+ 1 (Wenn *s*> 0). [ d]|  
|SQL_INTERVAL_DAY_TO_SECOND|Wobei *p* ist die Genauigkeit für anführenden Intervallwert und *s* Sekunden Genauigkeit, 9 +*p* (Wenn *s*= 0) oder 10 +*p* + *s* (Wenn *s*> 0). [ d]|  
|SQL_INTERVAL_HOUR_TO_SECOND|Wobei *p* ist die Genauigkeit für anführenden Intervallwert und *s* Sekunden Genauigkeit, 6 und höher*p* (Wenn *s*= 0) oder 7 +*p* + *s* (Wenn *s*> 0). [ d]|  
|SQL_INTERVAL_MINUTE_TO_SECOND|Wobei *p* ist die Genauigkeit für anführenden Intervallwert und *s* Sekunden Genauigkeit, 3 und höher*p* (Wenn *s*= 0) oder 4 +*p* + *s* (Wenn *s*> 0). [ d]|  
|SQL_INTERVAL_YEAR SQL_INTERVAL_MONTH SQL_INTERVAL_DAY SQL_INTERVAL_HOUR SQL_INTERVAL_MINUTE|*p*, wobei *p* ist die Genauigkeit für anführenden Intervallwert. [ d]|  
|SQL_INTERVAL_YEAR_TO_MONTH SQL_INTERVAL_DAY_TO_HOUR|3 +*p*, wobei *p* ist die Genauigkeit für anführenden Intervallwert. [ d]|  
|SQL_INTERVAL_DAY_TO_MINUTE|6 +*p*, wobei *p* ist die Genauigkeit für anführenden Intervallwert. [ d]|  
|SQL_INTERVAL_HOUR_TO_MINUTE|3 +*p*, wobei *p* ist die Genauigkeit für anführenden Intervallwert. [ d]|  
|SQL_GUID|36 (die Anzahl der Zeichen in der *Aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee* Format)|  
  
 [a] für eine ODBC-1.0 aufrufende **SQLSetParam** in ODBC 2.0-Treiber und für eine aufrufende ODBC 2.0 **SQLBindParameter** in ein 1.0 ODBC-Treiber, wenn \*  *StrLen_or_IndPtr* SQL_DATA_AT_EXEC für einen Typ SQL_LONGVARCHAR oder SQL_LONGVARBINARY wird *ColumnSize* muss auf die gesamte Länge der Daten festgelegt werden, um gesendet werden, nicht die Genauigkeit wie in dieser Tabelle definiert.  
  
 [b] Wenn der Treiber die Spalten- oder Parameternamen Länge für einen Variablentyp nicht ermitteln kann, gibt es SQL_NO_TOTAL zurück.  
  
 [c] der *ColumnSize* Argument **SQLBindParameter** wird für diesen Datentyp ignoriert.  
  
 [d] für allgemeine Regeln zur Spaltenlänge in Interval-Datentypen finden Sie unter [Intervall Datentyplänge](../../../odbc/reference/appendixes/interval-data-type-length.md)weiter oben in diesem Anhang.  
  
 Die zurückgegebenen Werte für die Größe der Spalte (oder Parameter) müssen nicht auf die Werte in jedem Deskriptorfeld für einen entsprechen. Die Werte können aus der SQL_DESC_PRECISION oder Feld SQL_DESC_LENGTH je nach Art der Daten stammen, wie in der folgenden Tabelle gezeigt.  
  
|SQL-Typ|Deskriptorfeld entspricht<br /><br /> Spalte oder Parameter-Größe|  
|--------------|--------------------------------------------------------------------|  
|Alle Zeichen- und Binärtypen|LENGTH|  
|Alle numerischen Typen|PRECISION|  
|Alle Typen von "DateTime" und das Intervall|LENGTH|  
|SQL_BIT|LENGTH|

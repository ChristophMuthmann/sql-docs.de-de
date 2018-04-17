---
title: SQL-Datentypen | Microsoft Docs
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
- SQL data types [ODBC]
- SQL data types [ODBC], about SQL data types
- data types [ODBC], SQL data types
ms.assetid: 1b22f985-f5e4-4779-87eb-e43329a442b1
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 2c1bb7ad5ce2523f4ee4e5404608e1359b216178
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sql-data-types"></a>SQL-Datentypen
Jede DBMS definiert eine eigene SQL-Typen. Jede ODBC-Treiber stellt nur die SQL-Datentypen, die die zugeordneten DBMS definiert. Informationen wie ein Treiber ordnet DBMS SQL-Typen zu den SQL ODBC-definierten Typ-IDs und wie ein Treiber DBMS-SQL-Typen einen eigenen Treiber-spezifische SQL-Typ-IDs zugeordnet wird zurückgegeben, durch einen Aufruf von **SQLGetTypeInfo**. Ein Treiber gibt auch die SQL-Datentypen beim Beschreiben der Datentypen der Spalten und Parametern über Aufrufe von **SQLColAttribute**, **SQLColumns**, **SQLDescribeCol**, **SQLDescribeParam**, **SQLProcedureColumns**, und **SQLSpecialColumns**.  
  
> [!NOTE]  
>  Die SQL-Datentypen sind in den Feldern SQL_DESC_ CONCISE_TYPE, SQL_DESC_TYPE und SQL_DESC_DATETIME_INTERVAL_CODE die Deskriptoren Implementierung enthalten. Merkmale der SQL-Datentypen sind in den Feldern SQL_DESC_PRECISION, SQL_DESC_SCALE SQL_DESC_LENGTH und SQL_DESC_OCTET_LENGTH die Deskriptoren Implementierung enthalten. Weitere Informationen finden Sie unter [-datentypbezeichnungen und Deskriptoren](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md) weiter unten in diesem Anhang.  
  
 Eine bestimmte Treiber und die Datenquelle nicht notwendigerweise unterstützt alle SQL-Datentypen, die in diesem Anhang definiert sind. Ein Treiber-Unterstützung für SQL-Datentypen hängt von der Ebene der SQL-92, die der Treiber entspricht. Die Ebene der SQL-92-Grammatik, die vom Treiber unterstützt werden um zu ermitteln, die eine Anwendung ruft **SQLGetInfo** mit dem Typ der SQL_SQL_CONFORMANCE-Informationen. Darüber hinaus kann eine bestimmte Treiber und die Datenquelle zusätzliche, treiberspezifischen SQL-Datentypen unterstützen. Um zu bestimmen, welche Datentypen einen Treiber unterstützt, werden Aufrufe von einer Anwendung **SQLGetTypeInfo**. Informationen zu treiberspezifischen SQL-Datentypen finden Sie unter der Treiber-Dokumentation. Informationen zu den Datentypen in einer bestimmten Datenquelle finden Sie in der Dokumentation für diese Datenquelle.  
  
> [!IMPORTANT]  
>  Die Tabellen in diesem Anhang werden nur Richtlinien und Namen anzeigen, die in der Regel verwendet, Bereiche und Einschränkungen der SQL-Datentypen. Eine bestimmten Datenquelle unterstützen möglicherweise nur einige der aufgeführten Datentypen und die Eigenschaften der unterstützten Datentypen können von den aufgeführten abweichen.  
  
 Die folgende Tabelle enthält gültige SQL-Typ-IDs für alle SQL-Datentypen. Die Tabelle enthält auch den Namen und die Beschreibung des entsprechenden Datentyps von SQL-92 (falls vorhanden).  
  
|SQL-Typ-ID [1]|Typische SQL-Daten<br /><br /> Typ [2]|Typische Beschreibung|  
|------------------------------|------------------------------------|------------------------------|  
|SQL_CHAR|CHAR (*n*)|Zeichen von Zeichenfolge mit einer Zeichenfolge fester Länge *n*.|  
|SQL_VARCHAR|VARCHAR (*n*)|Zeichenfolge mit variabler Länge mit einer maximalen Zeichenfolgenlänge *n*.|  
|SQL_LONGVARCHAR|LONG VARCHAR|Zeichendaten variabler Länge. Maximale Länge ist datenquellenabhängig. [9]|  
|SQL_WCHAR|WCHAR (*n*)|Unicode-Zeichenfolge, Zeichenfolge fester Länge *n*|  
|SQL_WVARCHAR|VARWCHAR (*n*)|Unicode-Zeichenfolge mit dem Wert variabler Länge mit einer maximalen Zeichenfolgenlänge *n*|  
|SQL_WLONGVARCHAR|LONGWVARCHAR|Unicode-Zeichen von variabler Länge, die Daten. Maximale Länge ist datenquellenabhängig|  
|SQL_DECIMAL|DECIMAL (*p*,*s*)|Signiert, genauen numerischen Wert mit einer Genauigkeit von mindestens *p* und Skalierung *s.* (Die maximale Genauigkeit treiberdefinierten ist). (1 < = *p* < = 15. *s* <= *p*). [ 4]|  
|SQL_NUMERIC|NUMERISCHE (*p*,*s*)|Signiert wird, exakten numerischen Wert mit einer Genauigkeit *p* und Skalierung *s* (1 < = *p* < = 15. *s* <= *p*). [ 4]|  
|SQL_SMALLINT|SMALLINT|Genauen numerischen Wert mit einer Genauigkeit von 5 und Skalierung von 0 (signiert: – 32.768 < = *n* < = 32.767, unsigniert: 0 < = *n* < 65.535 =) [3].|  
_INTEGER|INTEGER|Genauen numerischen Wert mit einer Genauigkeit von 10 und Skalierung von 0 (signiert: – 2 [31] < = *n* < = 2 [31] – 1, unsigniert: 0 < = *n* < = 2 [32] – 1) [3].|  
|SQL_REAL|real|Signiert, ungefähren numerischen Wert mit einer Genauigkeit 24 (0 (null) oder absoluten Wert 10 [–38] 10[38]).|  
|SQL_FLOAT|FLOAT (*p*)|Signiert, ungefähren numerischen Wert mit einer Genauigkeit von mindestens *p*. (Die maximale Genauigkeit treiberdefinierten ist). [5]|  
|SQL_DOUBLE|DOUBLE PRECISION|Signiert, ungefähren numerischen Wert mit einer binären Genauigkeit von 53 (0 (null) oder absoluten Wert 10 [–308] 10[308]).|  
|SQL_BIT|BIT|Einzelnes Bit Binärdaten. [8]|  
|SQL_TINYINT|TINYINT|Genauen numerischen Wert mit einer Genauigkeit von 3 und Skalierung von 0 (signiert: – 128 < = *n* < = 127, unsigniert: 0 < = *n* < = 255) [3].|  
_BIGINT|bigint|Genauen numerischen Wert mit einer Genauigkeit von 19 (sofern signiert) oder 20 (falls ohne Vorzeichen) und Skalierung von 0 (signiert: – 2 [63] < = *n* < = 2 [63] – 1, unsigniert: 0 < = *n* < = 2 [64] – 1) [3], [9].|  
|SQL_BINARY|Binär (*n*)|Binärdaten fester Länge *n*. [ 9]|  
|SQL_VARBINARY|VARBINARY (*n*)|Binärdaten variabler Länge, maximale Länge *n*. Die maximale wird vom Benutzer festgelegt. [9]|  
|SQL_LONGVARBINARY|LANGE VARBINARY|Binärdaten variabler Länge. Maximale Länge ist datenquellenabhängig. [9]|  
|SQL_TYPE_DATE [6]|DATE|Jahr, Monat und Tag-Felder, die gemäß den Regeln des gregorianischen Kalenders. (Siehe [Einschränkungen des gregorianischen Kalenders](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md)weiter unten in diesem Anhang.)|  
|SQL_TYPE_TIME [6]|Zeit (*p*)|Stunde, Minute und Sekunde Feldern, die gültige Werte für Stunden der gültigen Werte von 00 bis 23, von 00 bis 59 Minuten und gültige Werte für Sekunden von 00 bis 61. Genauigkeit *p* die Genauigkeit für die Sekunden angibt.|  
|SQL_TYPE_TIMESTAMP [6]|Zeitstempel (*p*)|Jahr, Monat, Tag, Stunde, Minute und zweite Felder mit gültigen Werten für die Datentypen für Datum und Uhrzeit definiert.|  
_TYPE_UTCDATETIME|UTCDATETIME|Jahr, Monat, Tag, Stunde, Minute, Sekunde, Utchour und Utcminute Felder. Die Felder Utchour und Utcminute haben Genauigkeit von 1/10 in Mikrosekunden.|  
|SQL_TYPE_UTCTIME|UTC-ZEIT|Felder für Stunde, Minute, Sekunde, Utchour und Utcminute. Die Felder Utchour und Utcminute haben Genauigkeit von 1/10 in Mikrosekunden...|  
|SQL_INTERVAL_MONTH [7]|Intervall Monat (*p*)|Die Anzahl der Monate zwischen zwei Datumsangaben; *p* ist die Genauigkeit für anführenden Intervallwert.|  
|SQL_INTERVAL_YEAR [7]|Intervall Jahr (*p*)|Die Anzahl der Jahre zwischen zwei Datumsangaben; *p* ist die Genauigkeit für anführenden Intervallwert.|  
|SQL_INTERVAL_YEAR_TO_MONTH [7]|Intervall Jahr (*p*) auf den Monat|Die Anzahl der Jahre oder Monate zwischen zwei Datumsangaben; *p* ist die Genauigkeit für anführenden Intervallwert.|  
|SQL_INTERVAL_DAY [7]|Intervall Tag (*p*)|Die Anzahl von Tagen zwischen zwei Datumsangaben; *p* ist die Genauigkeit für anführenden Intervallwert.|  
|SQL_INTERVAL_HOUR [7]|Intervall Stunde (*p*)|Anzahl von Stunden zwischen zwei Datumsangaben und Uhrzeiten; *p* ist die Genauigkeit für anführenden Intervallwert.|  
|SQL_INTERVAL_MINUTE [7]|Intervall MINUTE (*p*)|Anzahl der Minuten zwischen zwei Datumsangaben und Uhrzeiten; *p* ist die Genauigkeit für anführenden Intervallwert.|  
|SQL_INTERVAL_SECOND [7]|Intervall zweite (*p*,*q*)|Anzahl der Sekunden zwischen zwei Datumsangaben und Uhrzeiten; *p* ist die Genauigkeit für anführenden Intervallwert und *q* Intervall Sekunden Genauigkeit.|  
_INTERVAL_DAY_TO_HOUR [7]|Intervall Tag (*p*), die Stunde|Anzahl der Tage/Stunden zwischen zwei Datumsangaben und Uhrzeiten; *p* ist die Genauigkeit für anführenden Intervallwert.|  
|SQL_INTERVAL_DAY_TO_MINUTE [7]|Intervall Tag (*p*) auf die MINUTE|Anzahl der Tage/Stunden/Minuten zwischen zwei Datumsangaben und Uhrzeiten; *p* ist die Genauigkeit für anführenden Intervallwert.|  
|SQL_INTERVAL_DAY_TO_SECOND [7]|Intervall Tag (*p*) zweiten (*q*)|Anzahl der Tage/Stunden/Minuten/Sekunden zwischen zwei Datumsangaben und Uhrzeiten; *p* ist die Genauigkeit für anführenden Intervallwert und *q* Intervall Sekunden Genauigkeit.|  
|SQL_INTERVAL_HOUR_TO_MINUTE [7]|Intervall Stunde (*p*) auf die MINUTE|Anzahl der Stunden/Minuten zwischen zwei Datumsangaben und Uhrzeiten; *p* ist die Genauigkeit für anführenden Intervallwert.|  
|SQL_INTERVAL_HOUR_TO_SECOND [7]|Intervall Stunde (*p*) zweiten (*q*)|Anzahl der Stunden/Minuten/Sekunden zwischen zwei Datumsangaben und Uhrzeiten; *p* ist die Genauigkeit für anführenden Intervallwert und *q* Intervall Sekunden Genauigkeit.|  
_INTERVAL_MINUTE_TO_SECOND [7]|Intervall MINUTE (*p*) zweiten (*q*)|Anzahl von Minuten/Sekunden zwischen zwei Datumsangaben und Uhrzeiten; *p* ist die Genauigkeit für anführenden Intervallwert und *q* Intervall Sekunden Genauigkeit.|  
|SQL_GUID|GUID|Feste Länge GUID.|  
  
 [1]. Dies ist der zurückgegebene Wert in der DATA_TYPE-Spalte durch einen Aufruf von **SQLGetTypeInfo**.  
  
 [2] Dies ist der Wert in der Spalte NAME und PARAMS erstellen durch einen Aufruf zurückgegebene **SQLGetTypeInfo**. Die NAME-Spalte gibt die Bezeichnung – z. B. CHAR – während die erstellen PARAMS-Spalte gibt eine durch Trennzeichen getrennte Liste der Erstellungsparameter z. B. mit einfacher Genauigkeit, Dezimalstellen und Länge zurück.  
  
 [3] eine Anwendung verwendet **SQLGetTypeInfo** oder **SQLColAttribute** zu bestimmen, ob ein bestimmter Datentyp oder eine bestimmte Spalte in einem Resultset nicht signiert ist.  
  
 [4] Datentypen SQL_DECIMAL und SQL_NUMERIC unterscheiden sich nur hinsichtlich ihrer Genauigkeit. Die Genauigkeit einer Dezimalzahl (*p*,*s*) ist eine implementierungsdefinierte decimal-Genauigkeit, die nicht kleiner als *p*, während die Genauigkeit einer numerischen (*p* ,*s*) entspricht genau *p*.  
  
 [5] je nach der Implementierung kann die Genauigkeit der SQL_FLOAT 24 oder 53 sein: er 24 SQL_FLOAT-Datentyp ist, identisch mit SQL_REAL; ist er 53, ist der Datentyp SQL_FLOAT SQL_DOUBLE identisch.  
  
 [6] ' ist in ODBC 3.*.x*, die SQL-Date, Time und Timestamp-Datentypen sind SQL_TYPE_DATE, SQL_TYPE_TIME und SQL_TYPE_TIMESTAMP, bzw.; in ODBC 2. *X*, SQL_DATE, SQL_TIME und SQL_TIMESTAMP werden.  
  
 [7] Weitere Informationen zu den Intervall SQL-Datentypen finden Sie unter der [Intervalldatentypen](../../../odbc/reference/appendixes/interval-data-types.md) weiter unten in diesem Anhang.  
  
 [8] der SQL_BIT Daten weist andere Eigenschaften als die Bit-Typ in der SQL-92.  
  
 [9] dieser Datentyp hat keine entsprechende Daten in SQL-92.  
  
 Dieser Abschnitt enthält das folgende Beispiel.  
  
-   [Example SQLGetTypeInfo Result Set (Beispielergebnis des SQLGetTypeInfo-Resultsets)](../../../odbc/reference/appendixes/example-sqlgettypeinfo-result-set.md)

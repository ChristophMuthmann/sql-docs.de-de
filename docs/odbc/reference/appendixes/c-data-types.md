---
title: C-Datentypen | Microsoft Docs
ms.custom: 
ms.date: 07/12/2017
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
- data types [ODBC], C data types
- C data types [ODBC], about C data types
- C data types [ODBC]
- C buffers [ODBC]
ms.assetid: b681d260-3dbb-47df-a616-4910d727add7
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0fe266052c52b46b7f206869bdf89ff5377daf3b
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="c-data-types"></a>C-Datentypen
ODBC C-Datentypen angeben, den Datentyp der C-Puffer zum Speichern von Daten in der Anwendung verwendet wird.  
  
 Alle Treiber müssen alle C-Datentypen unterstützen. Dies ist erforderlich, da alle Treiber alle C-Typen unterstützen müssen, die in die SQL-Typen, die sie unterstützen konvertiert werden können, und alle Treiber unterstützen mindestens ein Zeichen SQL-Typ. Da der SQL-Zeichentyp in und aus allen C-Datentypen konvertiert werden kann, müssen alle Treiber alle C-Typen unterstützen.  
  
 Die C-Datentyp wird angegeben, der **SQLBindCol** und **SQLGetData** Funktionen mit der *TargetType* Argument und klicken Sie in der **SQLBindParameter**-Funktion mit dem *ValueType* Argument. Es kann auch durch den Aufruf angegeben werden **SQLSetDescField** festzulegende Feld SQL_DESC_CONCISE_TYPE eines ARD oder APD oder durch Aufrufen **SQLSetDescRec** mit der *Typ* Argument (und die *Untertyp* Argument bei Bedarf) und die *DescriptorHandle* -Argument auf das Handle eines ARD oder APD festgelegt.  
  
 In den folgenden Tabellen sind die gültigen Typ-IDs für die C-Datentypen aufgeführt. Die Tabelle enthält auch die ODBC-C-Datentyp, der jeden Bezeichner und die Definition dieses Datentyps entspricht.  
  
|C-Typ-ID|ODBC C-Typdefinition|C-Typ|  
|-----------------------|--------------------|------------|  
|SQL_C_CHAR|SQLCHAR *|unsigned Char *|  
|SQL_C_WCHAR|SQLWCHAR *|Wchar_t *|  
|SQL_C_SSHORT [j]|SQLSMALLINT|short int|  
|SQL_C_USHORT [j]|SQLUSMALLINT|short Int ohne Vorzeichen|  
|SQL_C_SLONG [j]|SQLINTEGER|Long int|  
|SQL_C_ULONG [j]|SQLUINTEGER|unsigned long int|  
|SQL_C_FLOAT|SQLREAL|float|  
|SQL_C_DOUBLE|SQLDOUBLE SQLFLOAT|double|  
|SQL_C_BIT|SQLCHAR|ohne Vorzeichen|  
|SQL_C_STINYINT [j]|SQLSCHAR|Char mit Vorzeichen|  
|Der SQL_C_UTINYINT [j]|SQLCHAR|ohne Vorzeichen|  
|SQL_C_SBIGINT|SQLBIGINT|_int64 [h]|  
|SQL_C_UBIGINT|SQLUBIGINT|ohne Vorzeichen _int64 [h]|  
|SQL_C_BINARY|SQLCHAR *|unsigned Char *|  
|SQL_C_BOOKMARK [i]|LESEZEICHEN|unsigned long Int [d]|  
|SQL_C_VARBOOKMARK|SQLCHAR *|unsigned Char *|  
|Alle C-Intervall-Datentypen|SQL_INTERVAL_STRUCT|Finden Sie unter der [C-Intervall-Struktur](../../../odbc/reference/appendixes/c-interval-structure.md) weiter unten in diesem Anhang.|  
  
 **C-Typbezeichner** SQL_C_TYPE_DATE [c]  
  
 **ODBC C-Typdefinition** SQL_DATE_STRUCT  
  
 **C-Typ**  
  
```  
struct tagDATE_STRUCT {  
   SQLSMALLINT year;  
   SQLUSMALLINT month;  
   SQLUSMALLINT day;    
} DATE_STRUCT;[a]  
```  
  
 **C-Typbezeichner** SQL_C_TYPE_TIME [c]  
  
 **ODBC C-Typdefinition** SQL_TIME_STRUCT  
  
 **C-Typ**  
  
```  
struct tagTIME_STRUCT {  
   SQLUSMALLINT hour;  
   SQLUSMALLINT minute;  
   SQLUSMALLINT second;  
} TIME_STRUCT;[a]  
```  
  
 **C-Typbezeichner** SQL_C_TYPE_TIMESTAMP [c]  
  
 **ODBC C-Typdefinition** SQL_TIMESTAMP_STRUCT  
  
 **C-Typ**  
  
```  
struct tagTIMESTAMP_STRUCT {  
   SQLSMALLINT year;  
   SQLUSMALLINT month;  
   SQLUSMALLINT day;  
   SQLUSMALLINT hour;  
   SQLUSMALLINT minute;  
   SQLUSMALLINT second;  
   SQLUINTEGER fraction;[b]   
} TIMESTAMP_STRUCT;[a]  
```  
  
 **C-Typbezeichner** SQL_C_NUMERIC  
  
 **ODBC C-Typdefinition** SQL_NUMERIC_STRUCT  
  
 **C-Typ**  
  
```  
struct tagSQL_NUMERIC_STRUCT {  
   SQLCHAR precision;  
   SQLSCHAR scale;  
   SQLCHAR sign[g];  
   SQLCHAR val[SQL_MAX_NUMERIC_LEN];[e], [f]   
} SQL_NUMERIC_STRUCT;  
```  
  
 **C-Typbezeichner** SQL_C_GUID  
  
 **ODBC C-Typdefinition** SQLGUID  
  
 **C-Typ**  
  
```  
struct tagSQLGUID {  
   DWORD Data1;  
   WORD Data2;  
   WORD Data3;  
   BYTE Data4[8];  
} SQLGUID;[k]  
```  
  
 [a] die Werte der Jahr, Monat, Tag, Stunde, Minute und Sekunde Felder in den "DateTime" C-Datentypen müssen den Einschränkungen des gregorianischen Kalenders entsprechen. (Siehe [Einschränkungen des gregorianischen Kalenders](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md) weiter unten in diesem Anhang.)  
  
 [b] der Wert des Felds Teiler ist die Anzahl der milliardste Teil einer Sekunde und im Bereich von 0 bis 999.999.999 (1 weniger als 1 Milliarde). Beispielsweise ist der Wert des Felds Anteil für eine halbe Sekunde 500,000,000, für ein Tausendstel einer Sekunde (eine Millisekunde) ist 1.000.000, für ein Millionstel einer Sekunde (einer Mikrosekunde) ist 1.000, und für eine den milliardsten Teil eine Sekunde (einer Nanosekunde) ist 1.  
  
 [c] ' ist in ODBC 2. *x*, die C-Date, Time und Timestamp-Datentypen sind SQL_C_DATE, SQL_C_TIME und SQL_C_TIMESTAMP.  
  
 [d] ODBC 3.*.x* Anwendungen SQL_C_VARBOOKMARK nicht SQL_C_BOOKMARK sollte verwendet werden. Wenn eine ODBC 3.*.x* Anwendung arbeitet mit einer ODBC 2..* X* -Treiber verwenden, die ODBC 3.*.x* Treibermanager SQL_C_BOOKMARK SQL_C_VARBOOKMARK ordnen.  
  
 [e] ein Anzahl wird gespeichert, der *Val* -Feld der Struktur SQL_NUMERIC_STRUCT als skalierte eine ganze Zahl im little-endian-Modus (das am weitesten links stehende Byte wird das unwichtigste Byte). Beispielsweise ist die Anzahl 10,001 Basis-10, mit einer Skala von 4, auf eine ganze Zahl des 100010 skaliert. Da dies 186AA im Hexadezimalformat angegeben ist, wäre der Wert in SQL_NUMERIC_STRUCT "AA 86 01 00 00... 00", mit der Anzahl von Bytes, die durch die SQL_MAX_NUMERIC_LEN definierten **#define**.  
  
 Weitere Informationen zu **SQL_NUMERIC_STRUCT**, finden Sie unter [so wird's gemacht: Abrufen von numerischen Daten SQL_NUMERIC_STRUCT](retrieve-numeric-data-sql-numeric-struct-kb222831.md).  
  
 [f] die Genauigkeit und Dezimalstellenanzahl Felder des ausgewählten SQL_C_NUMERIC geben Areused für die Eingabe aus einer Anwendung und für die Ausgabe aus dem Treiber an die Anwendung. Wenn der Treiber einen numerischen Wert in der SQL_NUMERIC_STRUCT schreibt, verwenden sie treiberspezifische standardmäßig als Wert für die *Genauigkeit* Feld, und er verwendet den Wert im Feld SQL_DESC_SCALE, der die Anwendung Deskriptor ( Das hat den Standardwert 0) für die *Skalierung* Feld. Eine Anwendung kann über eigene Eigenschaftenwerte für Genauigkeit und Dezimalstellenanzahl bereitstellen, durch die Felder SQL_DESC_PRECISION und SQL_DESC_SCALE des Deskriptors Anwendung festlegen.  
  
 [g] Anmelde-Feld ist 1, wenn positiv ist, 0, wenn negative.  
  
 [h] bei einigen Compilern möglicherweise nicht _int64 angegeben werden.  
  
 [i] _SQL_C_BOOKMARK ist in ODBC 3. veraltet*.x*.  
  
 [j] _SQL_C_SHORT SQL_C_LONG und SQL_C_TINYINT wurden in ODBC durch ersetzt mit und ohne Vorzeichen Typen: SQL_C_SSHORT und SQL_C_USHORT, SQL_C_SLONG und SQL_C_ULONG, und SQL_C_STINYINT und SQL_C_UTINYINT. Eine ODBC 3.*.x* Treiber, die mit ODBC 2. arbeiten sollten.* X* Anwendungen sollten SQL_C_SHORT, SQL_C_LONG und SQL_C_TINYINT, unterstützt, da bei der sie aufgerufen werden, der Treiber-Manager über den Treiber übergibt.  
  
 [k] SQL_C_GUID kann nur für SQL_CHAR oder SQL_WCHAR konvertiert werden.  
  
 Dieser Abschnitt enthält das folgende Thema.  
  
-   [64-Bit-Ganzzahl-Strukturen](../../../odbc/reference/appendixes/64-bit-integer-structures.md)  
  
## <a name="see-also"></a>Siehe auch  
 [C-Datentypen in ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)


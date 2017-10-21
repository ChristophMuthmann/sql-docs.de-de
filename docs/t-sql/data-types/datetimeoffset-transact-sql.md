---
title: "\"DateTimeOffset\" (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 7/23/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- datetimeoffset_TSQL
- datetimeoffset
dev_langs:
- TSQL
helpviewer_keywords:
- time [SQL Server], data types
- date and time [SQL Server], datetimeoffset
- datetimeoffset data type [SQL Server]
- dates [SQL Server], data types
- data types [SQL Server], date and time
- time zones [SQL Server]
ms.assetid: a0455b71-ca25-476e-a7a8-0770f1860bb7
caps.latest.revision: 41
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9a6c143380711d1af39a6c11f311e9ce3caf87c7
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="datetimeoffset-transact-sql"></a>datetimeoffset (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Definiert ein auf dem 24-Stunden-Format basierendes Datum, das mit einer Uhrzeit kombiniert ist, bei der die Zeitzone beachtet wird.
  
## <a name="datetimeoffset-description"></a>"DateTimeOffset"-Beschreibung
  
|Eigenschaft|Wert|  
|---|---|
|Syntax|**"DateTimeOffset"** [(*Genauigkeit in Sekundenbruchteilen*)]|  
|Verwendung|Deklarieren Sie @MyDatetimeoffset **datetimeoffset(7)**<br /><br /> Erstellen der Tabelle Table1 (Column1 **datetimeoffset(7)** )|  
|Standardmäßige Formate der Zeichenfolgenliterale (wird für Downlevelclients verwendet)|JJJJ-MM-TT HH: mm [.nnnnnnn]: [{+ &#124;-} hh: mm]<br /><br /> Weitere Informationen finden Sie unter den folgenden Abschnitt "Abwärtskompatibilität für Downlevelclients".|  
|Datumsbereich|0001-01-01 bis 9999-12-31<br /><br /> 1. Januar 1 CE bis zum 31. Dezember 9999 CE|  
|Uhrzeitbereich|00:00:00 bis 23:59:59.9999999 (Sekundenbruchteile werden in Informatica – nicht unterstützt)|  
|Zeitzonenoffsetbereich|-14: 00 bis + 14:00 (der Zeitzonenoffset wird im Informatica – ignoriert)|  
|Elementbereiche|Bei YYYY handelt es sich um vier Ziffern im Bereich von 0001 bis 9999, die ein Jahr darstellen.<br /><br /> MM handelt es sich zwei Ziffern im Bereich von 01 bis 12, die im angegebenen Jahr einen Monat darstellen.<br /><br /> Bei DD handelt es sich um zwei Ziffern im Bereich von 01 bis 31, die im angegebenen Monat einen Tag darstellen.<br /><br /> Bei hh handelt es sich um zwei Ziffern im Bereich von 00 bis 23, die die Stunde darstellen.<br /><br /> Bei mm handelt es sich um zwei Ziffern im Bereich von 00 bis 59, die die Minute darstellen.<br /><br /> Bei ss handelt es sich um zwei Ziffern im Bereich von 00 bis 59, die die Sekunde darstellen.<br /><br /> Bei n* handelt es sich um bis zu sieben Ziffern im Bereich von 0 bis 9999999, die die Sekundenbruchteile darstellen. Sekundenbruchteile werden im Informatica – nicht unterstützt.<br /><br /> Bei hh handelt es sich um zwei Ziffern im Bereich von -14 bis +14. Der Zeitzonenoffset wird im Informatica – ignoriert.<br /><br /> Bei mm handelt es sich um zwei Ziffern im Bereich von 00 bis 59. Der Zeitzonenoffset wird im Informatica – ignoriert.|  
|Zeichenlänge|mindestens 26 Positionen (YYYY-MM-DD HH: mm: {+ &#124;-} hh: mm) bis maximal 34 (JJJJ-MM-TT ss.nnnnnnn {+ &#124;-} hh: mm)|  
|Genauigkeit, Dezimalstellen|Finden Sie in der folgenden Tabelle aus.|  
|Speichergröße|Standardmäßig 10 Bytes fest, wobei die Standardgenauigkeit in Sekundenbruchteilen 100 ns beträgt.|  
|Genauigkeit|100 Nanosekunden|  
|Standardwert|1900-01-01 00:00:00 00:00|  
|Kalender|Gregorianisch|  
|Benutzerdefinierte Genauigkeit in Sekundenbruchteilen|ja|  
|Beachtung und Beibehaltung des Zeitzonenoffsets|ja|  
|Beachtung der Sommerzeit|Nein|  
  
|Angegebene Dezimalstelle|Ergebnis (Genauigkeit, Dezimalstellen)|Spaltenlänge (in Bytes)|Genauigkeit in Millisekunden|  
|---|---|---|---|
|**datetimeoffset**|(34,7)|10|7|  
|**DateTimeOffset(0)**|(26,0)|8|0-2|  
|**DateTimeOffset(1)**|(28,1)|8|0-2|  
|**DateTimeOffset(2)**|(29,2)|8|0-2|  
|**DateTimeOffset(3)**|(30,3)|9|3-4|  
|**DateTimeOffset(4)**|(31,4)|9|3-4|  
|**DateTimeOffset(5)**|(32,5)|10|5-7|  
|**DateTimeOffset(6)**|(33,6)|10|5-7|  
|**DateTimeOffset(7)**|(34,7)|10|5-7|  
  
## <a name="supported-string-literal-formats-for-datetimeoffset"></a>Unterstützte Formate der Zeichenfolgenliterale für datetimeoffset
Die folgende Tabelle enthält die unterstützten ISO 8601 Formate der Zeichenfolgenliterale für **"DateTimeOffset"**. Informationen zu alphabetischen, numerischen, unstrukturierte und Time-Formate für die Datums- und Uhrzeitteile von **"DateTimeOffset"**, finden Sie unter [Datum &#40; Transact-SQL &#41; ](../../t-sql/data-types/date-transact-sql.md) und [Zeit &#40; Transact-SQL &#41; ](../../t-sql/data-types/time-transact-sql.md).
  
|ISO 8601|Description|  
|---|---|
|JJJJ-MM-ddTHH [.nnnnnnn] [{+ &#124;-} hh: mm]|Diese beiden Formate werden nicht von den Gebietsschemaeinstellungen für Sitzungen SET LANGUAGE und SET DATEFORMAT beeinflusst. Leerzeichen sind nicht zulässig, zwischen den **"DateTimeOffset"** und **"DateTime"** teilen.|  
|YYYY-MM-DDThh:mm:ss[.nnnnnnn]Z (UTC)|Dieses Format gemäß ISO-Definition gibt die **"DateTime"** -Teil in koordinierter Weltzeit (UTC) ausgedrückt werden soll. Beispiel: 1999-12-12 12:30:30.12345 -07:00 soll als 1999-12-12 19:30:30.12345Z dargestellt werden.|  
  
## <a name="time-zone-offset"></a>Zeitzonenoffset
Ein Zeitzonenoffset gibt den zonenoffset von UTC für einen **Zeit** oder **"DateTime"** Wert. Der Zeitzonenoffset kann im Format [+|-] hh:mm dargestellt werden:
-   Bei hh handelt es sich um zwei Ziffern im Bereich von 00 bis 14, die die Anzahl der Stunden im Zeitzonenoffset darstellen.  
-   Bei "mm" handelt es sich um zwei Ziffern im Bereich von 00 bis 59, die die Anzahl der zusätzlichen Minuten im Zeitzonenoffset darstellen.  
-   \+(plus) oder – (Minus) ist das erforderliche Zeichen für einen Zeitzonenoffset. Dies gibt an, ob der Zeitzonenoffset zur UTC-Zeit addiert oder von dieser subtrahiert wird, um die lokale Zeit zu bestimmen. Der gültige Zeitzonenoffset liegt im Bereich von -14: 00 bis +14: 00.  
  
Der Zeitzonenoffsetbereich entspricht dem W3C XML-Standard für die XSD-Schemadefinition und weicht geringfügig von der SQL 2003-Standarddefinition (12:59 bis +14:00) ab.
  
Der optionale Parameter vom Typ *Genauigkeit in Sekundenbruchteilen* gibt die Anzahl von Ziffern für den Bruchteil der Sekunden an. Dieser Wert kann eine ganze Zahl von 0 bis 7 (100 Nanosekunden) sein. Die Standardeinstellung *Genauigkeit in Sekundenbruchteilen* beträgt 100 ns (sieben Ziffern für den Bruchteil der Sekunden).
  
Die Daten werden in der Datenbank gespeichert und auf dem Server entsprechend der UTC-Zeit verarbeitet, verglichen, sortiert und indiziert. Der Zeitzonenoffset bleibt in der Datenbank zum Abruf erhalten.
  
Der angegebene Zeitzonenoffset wird als gegeben angenommen Sommerzeit (DST) berücksichtigt und für jedes entsprechend angepasst werden **"DateTime"** , die sich in der Sommerzeit liegt.
  
Für **"DateTimeOffset"** eingeben, um zu UTC und lokale (auf den persistenten oder konvertierten Zeitzonenoffset) **"DateTime"** Wert wird während INSERT-, Update-, arithmetische, Convert oder weisen Vorgänge überprüft werden. Die Erkennung von ungültigen UTC oder lokal (in den persistenten oder konvertierten Zeitzonenoffset) **"DateTime"** Wert wird ein ungültiger Wert Fehler ausgelöst. 9999-12-31 10:10:00 ist z. B. im UTC-Format gültig, führt bei der lokalen Zeit aber zu einer Überschreitung des Zeitzonenoffsets +13:50.
  
Konvertiert ein Datum in ein entsprechendes **"DateTimeOffset"** Wert in einem Ziel-Zeitzone finden Sie unter [AT TIME ZONE &#40; Transact-SQL &#41; ](../../t-sql/queries/at-time-zone-transact-sql.md).
  
## <a name="ansi-and-iso-8601-compliance"></a>Kompatibilität mit ANSI und ISO 8601  
Die Abschnitte ANSI- und ISO 8601-Kompatibilität, der die [Datum](../../t-sql/data-types/date-transact-sql.md) und [Zeit](../../t-sql/data-types/time-transact-sql.md) Themen beziehen sich auf **"DateTimeOffset"**.
  
## <a name="backward-compatibility-for-down-level-clients"></a>Abwärtskompatibilität für Downlevelclients
Einige Clients früherer unterstützen nicht die **Zeit**, **Datum**, **datetime2** und **"DateTimeOffset"** -Datentypen. In der folgenden Tabelle wird die Typzuordnung zwischen einer Instanz höherer Ebene in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und Downlevelclients gezeigt.
  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Datentyp|Standardmäßiges Format des an Downlevelclients übergebenen Zeichenfolgenliterals|ODBC früherer Versionen|OLEDB früherer Versionen|JDBC früherer Versionen|SQLCLIENT früherer Versionen|  
|---|---|---|---|---|---|
|**Uhrzeit**|hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR oder SQL_VARCHAR|DBTYPE_WSTR oder DBTYPE_STR|Java.sql.String|Zeichenfolge oder SqString|  
|**Datum**|YYYY-MM-DD|SQL_WVARCHAR oder SQL_VARCHAR|DBTYPE_WSTR oder DBTYPE_STR|Java.sql.String|Zeichenfolge oder SqString|  
|**datetime2**|YYYY-MM-DD hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR oder SQL_VARCHAR|DBTYPE_WSTR oder DBTYPE_STR|Java.sql.String|Zeichenfolge oder SqString|  
|**datetimeoffset**|JJJJ-MM-TT HH: mm: [.nnnnnnn] [+ &#124;-] hh: mm|SQL_WVARCHAR oder SQL_VARCHAR|DBTYPE_WSTR oder DBTYPE_STR|Java.sql.String|Zeichenfolge oder SqString|  
  
## <a name="converting-date-and-time-data"></a>Konvertieren von Datums-und Uhrzeitdaten
Beim Konvertieren in date- und time-Datentypen lehnt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] alle Werte ab, die nicht als Datum oder Uhrzeit erkannt werden. Informationen zum Verwenden von CAST und CONVERT-Funktionen mit Datums-und Uhrzeitdaten finden Sie unter [CAST und CONVERT &#40; Transact-SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
Beim Konvertieren in **Datum**, Jahr, Monat und Tag werden kopiert. Der folgende Code zeigt die Ergebnisse der Konvertierung eines `datetimeoffset(4)`-Werts in einen `date`-Wert.  
  
```sql
DECLARE @datetimeoffset datetimeoffset(4) = '12-10-25 12:32:10 +01:00';  
DECLARE @date date= @datetimeoffset;  
  
SELECT @datetimeoffset AS '@datetimeoffset ', @date AS 'date';  
  
--Result  
--@datetimeoffset                date  
-------------------------------- ----------  
--2025-12-10 12:32:10.0000 +01:0 2025-12-10  
--  
--(1 row(s) affected)  
  
```  
  
Ist die Konvertierung **Time(n)-Werte**, die unsere, Minute, Sekunde und Sekundenbruchteile werden kopiert. Der Zeitzonenwert wird abgeschnitten. Wenn die Genauigkeit des der **DateTimeOffset (n)** Wert ist größer als die Genauigkeit des der **Time(n)-Werte** Wert, der Wert aufgerundet wird. Der folgende Code zeigt die Ergebnisse der Konvertierung eines `datetimeoffset(4)`-Werts in einen `time(3)`-Wert.
  
```sql
DECLARE @datetimeoffset datetimeoffset(4) = '12-10-25 12:32:10.1237 +01:0';  
DECLARE @time time(3) = @datetimeoffset;  
  
SELECT @datetimeoffset AS '@datetimeoffset ', @time AS 'time';  
  
--Result  
--@datetimeoffset                time  
-------------------------------- ------------  
-- 2025-12-10 12:32:10.1237 +01:00    12:32:10.124  
  
--  
--(1 row(s) affected)  
  
```  
  
Beim Konvertieren in**"DateTime"**, die Werte für Datum und Uhrzeit werden kopiert und die Zeitzone wird abgeschnitten. Bei der Genauigkeit von Bruchteilen der **DateTimeOffset (n)** Wert größer ist als drei Ziffern, wird der Wert abgeschnitten. Der folgende Code zeigt die Ergebnisse der Konvertierung eines `datetimeoffset(4)`-Werts in einen `datetime`-Wert.
  
```sql
DECLARE @datetimeoffset datetimeoffset(4) = '12-10-25 12:32:10.1237 +01:0';  
DECLARE @datetime datetime = @datetimeoffset;  
  
SELECT @datetimeoffset AS '@datetimeoffset ', @datetime AS 'datetime';  
  
--Result  
--@datetimeoffset                datetime  
-------------------------------- -----------------------  
--2025-12-10 12:32:10.1237 +01:0 2025-12-10 12:32:10.123  
--  
--(1 row(s) affected)  
```  
  
Für die Konvertierung in **Smalldatetime**, das Datum und die Stunden werden kopiert. Die Minuten werden in Bezug auf den Sekundenwert aufgerundet, und die Sekunden werden auf 0 festgelegt. Der folgende Code zeigt die Ergebnisse der Konvertierung eines `datetimeoffset(3)`-Werts in einen `smalldatetime`-Wert.  
  
```sql
DECLARE @datetimeoffset datetimeoffset(3) = '1912-10-25 12:24:32 +10:0';  
DECLARE @smalldatetime smalldatetime = @datetimeoffset;  
  
SELECT @datetimeoffset AS '@datetimeoffset', @smalldatetime AS '@smalldatetime';  
  
--Result  
--@datetimeoffset                @smalldatetime  
-------------------------------- -----------------------  
--1912-10-25 12:24:32.000 +10:00 1912-10-25 12:25:00  
--  
--(1 row(s) affected)  
```  
  
Ist die Konvertierung **datetime2(n)**, Datum und Uhrzeit werden kopiert, um die **datetime2** Wert und die Zeitzone wird abgeschnitten. Wenn die Genauigkeit des der **datetime2(n)** Wert ist größer als die Genauigkeit des der **DateTimeOffset (n)** Wert, die Sekundenbruchteile werden abgeschnitten. Der folgende Code zeigt die Ergebnisse der Konvertierung eines `datetimeoffset(4)`-Werts in einen `datetime2(3)`-Wert.
  
```sql
DECLARE @datetimeoffset datetimeoffset(4) = '1912-10-25 12:24:32.1277 +10:0';  
DECLARE @datetime2 datetime2(3)=@datetimeoffset;  
  
SELECT @datetimeoffset AS '@datetimeoffset', @datetime2 AS '@datetime2';  
  
--Result  
@datetimeoffset                    @datetime2  
---------------------------------- ----------------------  
1912-10-25 12:24:32.1277 +10:00    1912-10-25 12:24:32.12  
  
--(1 row(s) affected)  
```  
  
### <a name="converting-datetimeoffset-data-type-to-other-date-and-time-types"></a>Konvertieren von Datetimeoffset-Datentyp, um andere Datums- und Uhrzeittypen
In der folgenden Tabelle wird beschrieben, was geschieht, wenn eine **"DateTimeOffset"** -Datentyp in andere Datentypen für Datum und Uhrzeit konvertiert wird.
  
### <a name="converting-string-literals-to-datetimeoffset"></a>Konvertieren von Zeichenfolgenliteralen in datetimeoffset
Konvertierungen von Zeichenfolgenliteralen in Datums- und Zeitwerte sind erlaubt, wenn alle Teile der Zeichenfolge in gültigen Formaten vorliegen. Andernfalls wird ein Laufzeitfehler ausgelöst. Wird bei impliziten oder expliziten Konvertierungen von Datums- und Zeitwerten in Zeichenfolgenliterale kein Stil angegeben, wird das Standardformat der aktuellen Sitzung verwendet. Die folgende Tabelle zeigt die Regeln zum Konvertieren einer Zeichenfolge Zeichenfolgenliteral an die **"DateTimeOffset"** -Datentyp.
  
|Eingabezeichenfolgenliteral|**DateTimeOffset (n)**|  
|---|---|
|ODBC DATE|ODBC-Zeichenfolgenliterale zugeordnet sind, um die **"DateTime"** -Datentyp. Jede Zuweisungsoperation von ODBC DATETIME-literalen zu **"DateTimeOffset"** Typen führt dazu, dass eine implizite Konvertierung zwischen **"DateTime"** und dieses Typs gemäß den Konvertierungsregeln.|  
|ODBC TIME|Siehe vorherige ODBC DATE-Regel.|  
|ODBC DATETIME|Siehe vorherige ODBC DATE-Regel.|  
|Nur DATE|Der TIME-Teil wird standardmäßig auf 00:00:00 festgelegt. Die ZEITZONE wird standardmäßig auf + 00:00 Uhr.|  
|Nur TIME|Der DATE-Teil wird standardmäßig auf 1900-1-1 festgelegt. TIMEZONE wird standardmäßig auf +00:00 festgelegt.|  
|Nur TIMEZONE|Standardwerte werden festgelegt|  
|DATE + TIME|Die ZEITZONE wird standardmäßig auf + 00:00 Uhr.|  
|DATE + TIMEZONE|Nicht zulässig|  
|TIME + TIMEZONE|Der DATE-Teil wird standardmäßig auf 1900-1-1 festgelegt.|  
|DATE + TIME + TIMEZONE|Trivial|  
  
## <a name="examples"></a>Beispiele  
Das folgende Beispiel vergleicht die Ergebnisse der Umwandlung einer Zeichenfolge in alle **Datum** und **Zeit** -Datentyp.
  
```sql
SELECT   
     CAST('2007-05-08 12:35:29. 1234567 +12:15' AS time(7)) AS 'time'   
    ,CAST('2007-05-08 12:35:29. 1234567 +12:15' AS date) AS 'date'   
    ,CAST('2007-05-08 12:35:29.123' AS smalldatetime) AS   
        'smalldatetime'   
    ,CAST('2007-05-08 12:35:29.123' AS datetime) AS 'datetime'   
    ,CAST('2007-05-08 12:35:29.1234567+12:15' AS datetime2(7)) AS   
        'datetime2'  
    ,CAST('2007-05-08 12:35:29.1234567 +12:15' AS datetimeoffset(7)) AS   
        'datetimeoffset'  
    ,CAST('2007-05-08 12:35:29.1234567+12:15' AS datetimeoffset(7)) AS  
        'datetimeoffset IS08601';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
|Datentyp|Ausgabe|  
|---|---|
|**Zeit**|12:35:29. 1234567|  
|**Datum**|2007-05-08|  
|**Smalldatetime**|2007-05-08 12:35:00|  
|**Datetime**|2007-05-08 12:35:29.123|  
|**datetime2**|2007-05-08 12:35:29. 1234567|  
|**"DateTimeOffset"**|2007-05-08 12:35:29.1234567 +12:15|  
  
## <a name="see-also"></a>Siehe auch
[CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[ZEITZONE &AMP; #40; Transact-SQL &#41;](../../t-sql/queries/at-time-zone-transact-sql.md)
  
  


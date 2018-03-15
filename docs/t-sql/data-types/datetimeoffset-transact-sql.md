---
title: datetimeoffset (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 7/23/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: b1b8fba166243143cd9ab8c03303fcfd7448e7a3
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="datetimeoffset-transact-sql"></a>datetimeoffset (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Definiert ein auf dem 24-Stunden-Format basierendes Datum, das mit einer Uhrzeit kombiniert ist, bei der die Zeitzone beachtet wird.
  
## <a name="datetimeoffset-description"></a>Beschreibung von datetimeoffset
  
|Eigenschaft|value|  
|---|---|
|Syntax|**datetimeoffset** [ (*Sekundenbruchteil-Genauigkeit*) ]|  
|Verwendung|DECLARE @MyDatetimeoffset **datetimeoffset(7)**<br /><br /> CREATE TABLE Table1 ( Column1 **datetimeoffset(7)** )|  
|Standardmäßige Formate der Zeichenfolgenliterale (wird für Downlevelclients verwendet)|YYYY-MM-DD hh:mm:ss[.nnnnnnn] [{+&#124;-}hh:mm]<br /><br /> Weitere Informationen finden Sie im Abschnitt „Abwärtskompatibilität für Downlevelclients“|  
|Datumsbereich|0001-01-01 bis 9999-12-31<br /><br /> 1. Januar 1 n. Chr. bis 31. Dezember 9999|  
|Uhrzeitbereich|00:00:00 bis 23:59:59.9999999 (Sekundenbruchteile werden in Informatica nicht unterstützt)|  
|Zeitzonenoffsetbereich|–14: 00 bis +14:00 (der Zeitzonenoffset wird in Informatica ignoriert)|  
|Elementbereiche|Bei YYYY handelt es sich um vier Ziffern im Bereich von 0001 bis 9999, die ein Jahr darstellen.<br /><br /> Bei MM handelt es sich um zwei Ziffern im Bereich von 01 bis 12, die im angegebenen Jahr einen Monat darstellen.<br /><br /> Bei DD handelt es sich um zwei Ziffern im Bereich von 01 bis 31, die im angegebenen Monat einen Tag darstellen.<br /><br /> Bei hh handelt es sich um zwei Ziffern im Bereich von 00 bis 23, die die Stunde darstellen.<br /><br /> Bei mm handelt es sich um zwei Ziffern im Bereich von 00 bis 59, die die Minute darstellen.<br /><br /> Bei ss handelt es sich um zwei Ziffern im Bereich von 00 bis 59, die die Sekunde darstellen.<br /><br /> Bei n* handelt es sich um bis zu sieben Ziffern im Bereich von 0 bis 9999999, die die Sekundenbruchteile darstellen. Sekundenbruchteile werden in Informatica nicht unterstützt.<br /><br /> Bei hh handelt es sich um zwei Ziffern im Bereich von -14 bis +14. Der Zeitzonenoffset wird in Informatica ignoriert.<br /><br /> Bei mm handelt es sich um zwei Ziffern im Bereich von 00 bis 59. Der Zeitzonenoffset wird in Informatica ignoriert.|  
|Zeichenlänge|Mindestens 26 Positionen (YYYY-MM-DD hh:mm:ss {+&#124;-}hh:mm) bis maximal 34 Positionen (YYYY-MM-DD hh:mm:ss.nnnnnnn {+&#124;-}hh:mm)|  
|Genauigkeit, Dezimalstellen|Siehe Tabelle unten.|  
|Speichergröße|Standardmäßig 10 Bytes fest, wobei die Standardgenauigkeit in Sekundenbruchteilen 100 ns beträgt.|  
|Genauigkeit|100 Nanosekunden|  
|Standardwert|1900-01-01 00:00:00 00:00|  
|Kalender|Gregorianisch|  
|Benutzerdefinierte Genauigkeit in Sekundenbruchteilen|ja|  
|Beachtung und Beibehaltung des Zeitzonenoffsets|ja|  
|Beachtung der Sommerzeit|nein|  
  
|Angegebene Dezimalstelle|Ergebnis (Genauigkeit, Dezimalstellen)|Spaltenlänge (in Bytes)|Genauigkeit in Millisekunden|  
|---|---|---|---|
|**datetimeoffset**|(34,7)|10|7|  
|**datetimeoffset(0)**|(26,0)|8|0–2|  
|**datetimeoffset(1)**|(28,1)|8|0–2|  
|**datetimeoffset(2)**|(29,2)|8|0–2|  
|**datetimeoffset(3)**|(30,3)|9|3–4|  
|**datetimeoffset(4)**|(31,4)|9|3–4|  
|**datetimeoffset(5)**|(32,5)|10|5–7|  
|**datetimeoffset(6)**|(33,6)|10|5–7|  
|**datetimeoffset(7)**|(34,7)|10|5–7|  
  
## <a name="supported-string-literal-formats-for-datetimeoffset"></a>Unterstützte Formate der Zeichenfolgenliterale für datetimeoffset
In der folgenden Tabelle werden die unterstützten ISO 8601-Zeichenfolgenliterale für **datetimeoffset** aufgelistet. Informationen zu alphabetischen, numerischen und unstrukturierten Formaten sowie zu Zeitformaten für die Datums- und Uhrzeitteile von **datetimeoffset** finden Sie unter [date &#40;Transact-SQL&#41;](../../t-sql/data-types/date-transact-sql.md) und [time &#40;Transact-SQL&#41;](../../t-sql/data-types/time-transact-sql.md).
  
|ISO 8601|Description|  
|---|---|
|JJJJ-MM-TTThh:mm:ss[.nnnnnnn][{+&#124;-}hh:mm]|Diese beiden Formate werden nicht von den Gebietsschemaeinstellungen für Sitzungen SET LANGUAGE und SET DATEFORMAT beeinflusst. Leerzeichen zwischen **datetimeoffset**- und **datetime**-Teilen sind nicht zulässig.|  
|YYYY-MM-DDThh:mm:ss[.nnnnnnn]Z (UTC)|Dieses Format gibt gemäß ISO-Definition an, dass der **datetime**-Teil in koordinierter Weltzeit (Coordinated Universal Time; UTC) ausgedrückt werden soll. Beispiel: 1999-12-12 12:30:30.12345 -07:00 soll als 1999-12-12 19:30:30.12345Z dargestellt werden.|  
  
## <a name="time-zone-offset"></a>Zeitzonenoffset
Ein Zeitzonenoffset gibt den Zonenoffset der UTC-Zeit für einen **time**- oder einen **datetime**-Wert an. Der Zeitzonenoffset kann im Format [+|-] hh:mm dargestellt werden:
-   Bei hh handelt es sich um zwei Ziffern im Bereich von 00 bis 14, die die Anzahl der Stunden im Zeitzonenoffset darstellen.  
-   Bei "mm" handelt es sich um zwei Ziffern im Bereich von 00 bis 59, die die Anzahl der zusätzlichen Minuten im Zeitzonenoffset darstellen.  
-   \+ (plus) oder – (minus) ist das erforderliche Zeichen für einen Zeitzonenoffset. Dies gibt an, ob der Zeitzonenoffset zur UTC-Zeit addiert oder von dieser subtrahiert wird, um die lokale Zeit zu bestimmen. Der gültige Zeitzonenoffset liegt im Bereich von -14: 00 bis +14: 00.  
  
Der Zeitzonenoffsetbereich entspricht dem W3C XML-Standard für die XSD-Schemadefinition und weicht geringfügig von der SQL 2003-Standarddefinition (12:59 bis +14:00) ab.
  
Der optionale Typparameter *Sekundenbruchteil-Genauigkeit* gibt die Anzahl der Ziffern für den Bruchteil der Sekunden an. Dieser Wert kann eine ganze Zahl von 0 bis 7 (100 Nanosekunden) sein. Der Standardwert der *Sekundenbruchteil-Genauigkeit* beträgt 100 ns (sieben Ziffern für den Bruchteil der Sekunden).
  
Die Daten werden in der Datenbank gespeichert und auf dem Server entsprechend der UTC-Zeit verarbeitet, verglichen, sortiert und indiziert. Der Zeitzonenoffset bleibt in der Datenbank zum Abruf erhalten.
  
Es wird davon ausgegangen, dass für den angegebenen Zeitzonenoffset die Sommerzeit beachtet und für jeden angegebenen **datetime**-Wert, der in der Sommerzeit liegt, angepasst wird.
  
Beim **datetimeoffset**-Typ wird bei Einfüge-, Aktualisierungs-, Konvertierungs- oder Zuweisungsvorgängen oder bei arithmetischen Vorgängen sowohl der UTC-Wert als auch der (für den persistenten oder konvertierten Zeitzonenoffset) lokale **datetime**-Wert überprüft. Wird ein ungültiger UTC-Wert oder (für den persistenten oder konvertierten Zeitzonenoffset) lokaler **datetime**-Wert erkannt, wird ein Fehler wegen eines ungültigen Werts ausgelöst. 9999-12-31 10:10:00 ist z. B. im UTC-Format gültig, führt bei der lokalen Zeit aber zu einer Überschreitung des Zeitzonenoffsets +13:50.
  
Informationen zum Konvertieren eines Datums in einen entsprechenden **datetimeoffset**-Wert einer Zielzeitzone finden Sie unter [AT TIME ZONE &#40;Transact-SQL&#41;](../../t-sql/queries/at-time-zone-transact-sql.md).
  
## <a name="ansi-and-iso-8601-compliance"></a>Kompatibilität mit ANSI und ISO 8601  
Die Abschnitte zur Kompatibilität mit ANSI und ISO 8601 der Artikel [date](../../t-sql/data-types/date-transact-sql.md) und [time](../../t-sql/data-types/time-transact-sql.md) gelten auch für **datetimeoffset**.
  
## <a name="backward-compatibility-for-down-level-clients"></a>Abwärtskompatibilität für Downlevelclients
Einige Downlevelclients unterstützen nicht die Datentypen **time**, **date**, **datetime2** und **datetimeoffset**. In der folgenden Tabelle wird die Typzuordnung zwischen einer Instanz höherer Ebene in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und Downlevelclients gezeigt.
  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datentyp|Standardmäßiges Format des an Downlevelclients übergebenen Zeichenfolgenliterals|ODBC früherer Versionen|OLEDB früherer Versionen|JDBC früherer Versionen|SQLCLIENT früherer Versionen|  
|---|---|---|---|---|---|
|**Uhrzeit**|hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR oder SQL_VARCHAR|DBTYPE_WSTR oder DBTYPE_STR|Java.sql.String|Zeichenfolge oder SqString|  
|**Datum**|YYYY-MM-DD|SQL_WVARCHAR oder SQL_VARCHAR|DBTYPE_WSTR oder DBTYPE_STR|Java.sql.String|Zeichenfolge oder SqString|  
|**datetime2**|YYYY-MM-DD hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR oder SQL_VARCHAR|DBTYPE_WSTR oder DBTYPE_STR|Java.sql.String|Zeichenfolge oder SqString|  
|**datetimeoffset**|YYYY-MM-DD hh:mm:ss[.nnnnnnn] [+&#124;-]hh:mm|SQL_WVARCHAR oder SQL_VARCHAR|DBTYPE_WSTR oder DBTYPE_STR|Java.sql.String|Zeichenfolge oder SqString|  
  
## <a name="converting-date-and-time-data"></a>Konvertieren von Datums- und Uhrzeitdaten
Beim Konvertieren in date- und time-Datentypen lehnt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] alle Werte ab, die nicht als Datum oder Uhrzeit erkannt werden. Informationen zur Verwendung der CAST-Funktion und der CONVERT-Funktion mit Datums- und Uhrzeitdaten finden Sie unter [CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md).
  
Beim Konvertieren in **date** werden das Jahr, der Monat und der Tag kopiert. Der folgende Code zeigt die Ergebnisse der Konvertierung eines `datetimeoffset(4)`-Werts in einen `date`-Wert.  
  
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
  
Wenn ein Wert in **time(n)** konvertiert wird, werden die Stunde, Minute, Sekunde und die Sekundenbruchteile kopiert. Der Zeitzonenwert wird abgeschnitten. Wenn die Genauigkeit des **datetimeoffset(n)**-Werts höher als die Genauigkeit des **time(n)**-Werts ist, wird der Wert aufgerundet. Der folgende Code zeigt die Ergebnisse der Konvertierung eines `datetimeoffset(4)`-Werts in einen `time(3)`-Wert.
  
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
  
Wenn ein Wert in **datetime** konvertiert wird, werden die Datums- und Zeitwerte kopiert, und die Zeitzone wird abgeschnitten. Wenn die Sekundenbruchteil-Genauigkeit des **datetimeoffset(n)**-Werts um mehr als drei Stellen abweicht, wird der Wert gekürzt. Der folgende Code zeigt die Ergebnisse der Konvertierung eines `datetimeoffset(4)`-Werts in einen `datetime`-Wert.
  
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
  
Bei Konvertierungen in **smalldatetime** werden das Datum und die Stunden kopiert. Die Minuten werden in Bezug auf den Sekundenwert aufgerundet, und die Sekunden werden auf 0 festgelegt. Der folgende Code zeigt die Ergebnisse der Konvertierung eines `datetimeoffset(3)`-Werts in einen `smalldatetime`-Wert.  
  
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
  
Bei Konvertierungen in **datetime2(n)** werden das Datum und die Zeit in einen **datetime2**-Wert konvertiert, und die Zeitzone wird abgeschnitten. Wenn die Sekundenbruchteil-Genauigkeit des **datetime2(n)**-Werts höher ist als die Genauigkeit des **datetimeoffset(n)**-Werts, wird der Wert gekürzt. Der folgende Code zeigt die Ergebnisse der Konvertierung eines `datetimeoffset(4)`-Werts in einen `datetime2(3)`-Wert.
  
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
  
### <a name="converting-datetimeoffset-data-type-to-other-date-and-time-types"></a>Konvertieren des datetimeoffset-Datentyps in andere Datums- und Uhrzeittypen
Die folgende Tabelle veranschaulicht die Abläufe bei der Konvertierung des **datetimeoffset**-Datentyps in andere Datums- und Uhrzeitdatentypen.
  
### <a name="converting-string-literals-to-datetimeoffset"></a>Konvertieren von Zeichenfolgenliteralen in datetimeoffset
Konvertierungen von Zeichenfolgenliteralen in Datums- und Zeitwerte sind erlaubt, wenn alle Teile der Zeichenfolge in gültigen Formaten vorliegen. Andernfalls wird ein Laufzeitfehler ausgelöst. Wird bei impliziten oder expliziten Konvertierungen von Datums- und Zeitwerten in Zeichenfolgenliterale kein Stil angegeben, wird das Standardformat der aktuellen Sitzung verwendet. In der folgenden Tabelle werden die Regeln zum Konvertieren eines Zeichenfolgenliterals in den **datetimeoffset**-Datentyp dargestellt.
  
|Eingabezeichenfolgenliteral|**datetimeoffset(n)**|  
|---|---|
|ODBC DATE|Dem **datetime**-Datentyp werden ODBC-Zeichenfolgenliterale zugeordnet. Jede Zuweisungsoperation von ODBC DATETIME-Literalen zu **datetimeoffset**-Typen bewirkt eine in den Konvertierungsregeln definierte implizite Konvertierung zwischen **datetime** und diesen Typen.|  
|ODBC TIME|Siehe vorherige ODBC DATE-Regel.|  
|ODBC DATETIME|Siehe vorherige ODBC DATE-Regel.|  
|Nur DATE|Der TIME-Teil wird standardmäßig auf 00:00:00 festgelegt. TIMEZONE wird standardmäßig auf +00:00 festgelegt.|  
|Nur TIME|Der DATE-Teil wird standardmäßig auf 1900-1-1 festgelegt. TIMEZONE wird standardmäßig auf +00:00 festgelegt.|  
|Nur TIMEZONE|Standardwerte werden festgelegt|  
|DATE + TIME|TIMEZONE wird standardmäßig auf +00:00 festgelegt.|  
|DATE + TIMEZONE|Nicht zulässig|  
|TIME + TIMEZONE|Der DATE-Teil wird standardmäßig auf 1900-1-1 festgelegt.|  
|DATE + TIME + TIMEZONE|Trivial|  
  
## <a name="examples"></a>Beispiele  
Im folgenden Beispiel werden die Ergebnisse der Umwandlung von einer Zeichenfolge in alle **date**- und **time**-Datentypen verglichen.
  
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
|**datetimeoffset**|2007-05-08 12:35:29.1234567 +12:15|  
  
## <a name="see-also"></a>Siehe auch
[CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[AT TIME ZONE &#40;Transact-SQL&#41;](../../t-sql/queries/at-time-zone-transact-sql.md)
  
  

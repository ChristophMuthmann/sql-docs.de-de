---
title: datetime2 (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/23/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- datetime2
- datetime2_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- time [SQL Server], data types
- dates [SQL Server], data types
- date and time [SQL Server], datetime2
- data types [SQL Server], date and time
- datetime2 data type [SQL Server]
ms.assetid: 868017f3-214f-43ef-8536-cc1632a2288f
caps.latest.revision: 58
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 13766b3d0cb86780c2eca55c7f36e8fd16e973c5
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="datetime2-transact-sql"></a>datetime2 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Definiert ein Datum, das mit einer Uhrzeit kombiniert ist und auf dem 24-Stunden-Format basiert. **datetime2** berücksichtigt werden können, als Erweiterung des vorhandenen **"DateTime"** Typ, der einen größeren Datumsbereich, eine größere standardgenauigkeit bei Sekundenbruchteilen und eine optionale vom Benutzer angegebene Genauigkeit besitzt.
  
## <a name="datetime2-description"></a>Beschreibung von datetime2
  
|Eigenschaft|Wert|  
|--------------|-----------|  
|Syntax|**datetime2** [(*Genauigkeit in Sekundenbruchteilen*)]|  
|Verwendung|Deklarieren Sie @MyDatetime2 **datetime2(7)**<br /><br /> Erstellen der Tabelle Table1 (Column1 **datetime2(7)** )|  
|Standardmäßiges Format der Zeichenfolgenliterale<br /><br /> (wird für Downlevelclients verwendet)|YYYY-MM-DD hh:mm:ss [.Sekundenbruchteile]<br /><br /> Weitere Informationen finden Sie unter den folgenden Abschnitt "Abwärtskompatibilität für Downlevelclients".|  
|Datumsbereich|0001-01-01 bis 9999-12-31<br /><br /> Januar 1,1 CE bis zum 31. Dezember 9999 CE|  
|Uhrzeitbereich|00:00:00 bis 23:59:590,9999999|  
|Zeitzonenoffsetbereich|Keine|  
|Elementbereiche|Bei YYYY handelt es sich um eine vierstellige Zahl im Bereich von 0001 bis 9999, die ein Jahr darstellt.<br /><br /> Bei MM handelt es sich um eine zweistellige Zahl im Bereich von 01 bis 12, die im angegebenen Jahr einen Monat darstellt.<br /><br /> Bei DD handelt es sich um eine zweistellige Zahl im Bereich von 01 bis 31, die im angegebenen Monat einen Tag darstellt.<br /><br /> Bei hh handelt es sich um eine zweistellige Zahl im Bereich von 00 bis 23, die die Stunde darstellt.<br /><br /> Bei mm handelt es sich um eine zweistellige Zahl im Bereich von 00 bis 59, die die Minute darstellt.<br /><br /> Bei ss handelt es sich um eine zweistellige Zahl im Bereich von 00 bis 59, die die Sekunde darstellt.<br /><br /> Bei n* handelt es sich um eine null- bis siebenstellige Zahl von 0 bis 9999999, die die Sekundenbruchteile darstellt. Klicken Sie im Informatica –, werden die Sekundenbruchteile abgeschnitten, wenn n > 3.|  
|Zeichenlänge|Mindestens 19 Positionen (YYYY-MM-DD hh:mm:ss) bis maximal 27 Positionen (YYYY-MM-DD hh:mm:ss .0000000)|  
|Genauigkeit, Dezimalstellen|0 bis 7 Stellen mit einer Genauigkeit von 100 ns. Die Standardgenauigkeit beträgt 7 Stellen.|  
|Speichergröße|6 Byte für Genauigkeiten unter 3; 7 Byte für Genauigkeiten von 3 und 4. Alle anderen Genauigkeiten erfordern 8 Bytes.|  
|Genauigkeit|100 Nanosekunden|  
|Standardwert|1900-01-01 00:00:00|  
|Kalender|Gregorianisch|  
|Benutzerdefinierte Genauigkeit in Sekundenbruchteilen|ja|  
|Beachtung und Beibehaltung des Zeitzonenoffsets|Nein|  
|Beachtung der Sommerzeit|Nein|  
  
Datentyp-Metadaten finden Sie unter [sys.systypes &#40; Transact-SQL &#41; ](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md) oder [TYPEPROPERTY &#40; Transact-SQL &#41; ](../../t-sql/functions/typeproperty-transact-sql.md). Für einige Datums- und Uhrzeitdatentypen sind die Genauigkeit und die Dezimalstellenanzahl variabel. Um die Genauigkeit und Dezimalstellenanzahl für eine Spalte zu erhalten, finden Sie unter [COLUMNPROPERTY &#40; Transact-SQL &#41; ](../../t-sql/functions/columnproperty-transact-sql.md), [COL_LENGTH &#40; Transact-SQL &#41; ](../../t-sql/functions/col-length-transact-sql.md), oder [sys.columns &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md).
  
## <a name="supported-string-literal-formats-for-datetime2"></a>Unterstützte Formate der Zeichenfolgenliterale für datetime2
Die folgenden Tabellen enthalten die unterstützten ISO 8601- und ODBC-Formate der Zeichenfolgenliterale für **datetime2**. Informationen zu alphabetischen, numerischen Prozedure und Zeit Formate für Datum und Uhrzeit Bestandteile **datetime2**, finden Sie unter [Datum &#40; Transact-SQL &#41; ](../../t-sql/data-types/date-transact-sql.md) und [Zeit &#40; Transact-SQL &#41; ](../../t-sql/data-types/time-transact-sql.md).
  
|ISO 8601|Beschreibungen|  
|---|---|
|YYYY-MM-DDThh:mm:ss[.nnnnnnn]<br /><br /> YYYY-MM-DDThh:mm:ss[.nnnnnnn]|Dieses Format wird nicht von den SET LANGUAGE- und SET DATEFORMAT-Gebietsschemaeinstellungen für Sitzungen beeinflusst. Die **T**, die Doppelpunkte (:) und Punkt (.) sind in enthalten das Zeichenfolgenliteral, z. B. ' 2007-05-02T19:58:47.1234567 ".|  
  
|ODBC|Description|  
|---|---|
|{ ts 'yyyy-mm-dd hh:mm:ss[.Sekundenbruchteile]' }|ODBC-API-spezifisch:<br /><br /> Für die Anzahl der Stellen rechts vom Dezimaltrennzeichen, die den Sekundenbruchteil darstellen, kann 0 bis 7 (100 Nanosekunden) angegeben werden.|  
  
## <a name="ansi-and-iso-8601-compliance"></a>Kompatibilität mit ANSI und ISO 8601  
Die Kompatibilität mit ANSI und ISO 8601 von [Datum](../../t-sql/data-types/date-transact-sql.md) und [Zeit](../../t-sql/data-types/time-transact-sql.md) gelten für **datetime2**.
  
##  <a name="backward-compatibility-for-down-level-clients"></a>Abwärtskompatibilität für Downlevelclients  
Einige Clients früherer unterstützen nicht die **Zeit**, **Datum**, **datetime2** und **"DateTimeOffset"** -Datentypen. In der folgenden Tabelle wird die Typzuordnung zwischen einer Instanz höherer Ebene in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und Downlevelclients gezeigt.
  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Datentyp|Standardmäßiges Format des an Downlevelclients übergebenen Zeichenfolgenliterals|ODBC früherer Versionen|OLEDB früherer Versionen|JDBC früherer Versionen|SQLCLIENT früherer Versionen|  
| --- | --- | --- | --- | --- | --- |
|**Uhrzeit**|hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR oder SQL_VARCHAR|DBTYPE_WSTR oder DBTYPE_STR|Java.sql.String|Zeichenfolge oder SqString|  
|**Datum**|YYYY-MM-DD|SQL_WVARCHAR oder SQL_VARCHAR|DBTYPE_WSTR oder DBTYPE_STR|Java.sql.String|Zeichenfolge oder SqString|  
|**datetime2**|YYYY-MM-DD hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR oder SQL_VARCHAR|DBTYPE_WSTR oder DBTYPE_STR|Java.sql.String|Zeichenfolge oder SqString|  
|**datetimeoffset**|JJJJ-MM-TT HH: mm: [.nnnnnnn] [+ &#124;-] hh: mm|SQL_WVARCHAR oder SQL_VARCHAR|DBTYPE_WSTR oder DBTYPE_STR|Java.sql.String|Zeichenfolge oder SqString|  
  
## <a name="converting-date-and-time-data"></a>Konvertieren von Datums-und Uhrzeitdaten
Beim Konvertieren in date- und time-Datentypen lehnt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] alle Werte ab, die nicht als Datum oder Uhrzeit erkannt werden. Informationen zum Verwenden von CAST und CONVERT-Funktionen mit Datums-und Uhrzeitdaten finden Sie unter [CAST und CONVERT &#40; Transact-SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
### <a name="converting-other-date-and-time-types-to-the-datetime2-data-type"></a>Konvertieren von anderen Datums- und Uhrzeittypen in den datetime2-Datentyp
In diesem Abschnitt wird beschrieben, was geschieht, wenn andere Datentypen für Datum und Uhrzeit, um konvertiert werden die **datetime2** -Datentyp.  
  
Wenn die Konvertierung von ist **Datum**, Jahr, Monat und Tag werden kopiert.  Die Zeitkomponente wird auf 00:00:00.0000000 festgelegt.  Der folgende Code zeigt die Ergebnisse der Konvertierung eines `date`-Werts in einen `datetime2`-Wert.  
  
```sql
DECLARE @date date = '12-21-16';
DECLARE @datetime2 datetime2 = @date;

SELECT @datetime2 AS '@datetime2', @date AS '@date';
  
--Result  
--@datetime2                  @date
----------------------------- ----------
--2016-12-21 00:00:00.0000000 2016-12-21
```  
  
Wenn die Konvertierung von ist **Time(n)-Werte**, die Zeitkomponente wird kopiert, und die Datumskomponente wird festgelegt, um "1900-01-01". Das folgende Beispiel zeigt die Ergebnisse der Konvertierung eines `time(7)`-Werts in einen `datetime2`-Wert.  
  
```sql
DECLARE @time time(7) = '12:10:16.1234567';
DECLARE @datetime2 datetime2 = @time;

SELECT @datetime2 AS '@datetime2', @time AS '@time';
  
--Result  
--@datetime2                  @time
----------------------------- ----------------
--1900-01-01 12:10:16.1234567 12:10:16.1234567
```  
  
Wenn die Konvertierung von ist **Smalldatetime**, in Stunden und Minuten werden kopiert. Die Sekunden und die Sekundenbruchteile werden auf 0 festgelegt. Der folgende Code zeigt die Ergebnisse der Konvertierung eines `smalldatetime`-Werts in einen `datetime2`-Wert.  
  
```sql
DECLARE @smalldatetime smalldatetime = '12-01-16 12:32';
DECLARE @datetime2 datetime2 = @smalldatetime;

SELECT @datetime2 AS '@datetime2', @smalldatetime AS '@smalldatetime'; 
  
--Result  
--@datetime2                  @smalldatetime
----------------------------- -----------------------
--2016-12-01 12:32:00.0000000 2016-12-01 12:32:00 
```  
  
Wenn die Konvertierung von ist **DateTimeOffset (n)**, die Datums- und Zeitkomponenten werden kopiert. Die Zeitzone wird abgeschnitten. Das folgende Beispiel zeigt die Ergebnisse der Konvertierung eines `datetimeoffset(7)`-Werts in einen `datetime2`-Wert.  
  
```sql
DECLARE @datetimeoffset datetimeoffset(7) = '2016-10-23 12:45:37.1234567 +10:0';
DECLARE @datetime2 datetime2 = @datetimeoffset;

SELECT @datetime2 AS '@datetime2', @datetimeoffset AS '@datetimeoffset'; 
  
--Result  
--@datetime2                  @datetimeoffset
----------------------------- ----------------------------------
--2016-10-23 12:45:37.1234567 2016-10-23 12:45:37.1234567 +10:00
```  

Wenn die Konvertierung von ist **"DateTime"**, Datum und Uhrzeit werden kopiert.  Die Genauigkeit von Bruchteile wird bis 7 Stellen erweitert.  Das folgende Beispiel zeigt die Ergebnisse der Konvertierung eines `datetime`-Werts in einen `datetime2`-Wert.

```sql
DECLARE @datetime datetime = '2016-10-23 12:45:37.333';
DECLARE @datetime2 datetime2 = @datetime;

SELECT @datetime2 AS '@datetime2', @datetime AS '@datetime';
   
--Result  
--@datetime2                  @datetime
------------------------- ---------------------------
--2016-10-23 12:45:37.3333333 2016-10-23 12:45:37.333
```  
  
### <a name="converting-string-literals-to-datetime2"></a>Konvertieren von Zeichenfolgenliteralen in datetime2  
Konvertierungen von Zeichenfolgenliteralen in Datums- und Zeitwerte sind erlaubt, wenn alle Teile der Zeichenfolge in gültigen Formaten vorliegen. Andernfalls wird ein Laufzeitfehler ausgelöst. Wird bei impliziten oder expliziten Konvertierungen von Datums- und Zeitwerten in Zeichenfolgenliterale kein Stil angegeben, wird das Standardformat der aktuellen Sitzung verwendet. Die folgende Tabelle zeigt die Regeln zum Konvertieren einer Zeichenfolge Zeichenfolgenliteral an die **datetime2** -Datentyp.
  
|Eingabezeichenfolgenliteral|**datetime2(n)**|  
|---|---|
|ODBC DATE|ODBC-Zeichenfolgenliterale zugeordnet sind, um die **"DateTime"** -Datentyp. Jede Zuweisungsoperation von ODBC DATETIME-literalen zu **datetime2** Typen führt dazu, dass eine implizite Konvertierung zwischen **"DateTime"** und dieses Typs gemäß den Konvertierungsregeln.|  
|ODBC TIME|Siehe vorherige ODBC DATE-Regel.|  
|ODBC DATETIME|Siehe vorherige ODBC DATE-Regel.|  
|Nur DATE|Der TIME-Teil wird standardmäßig auf 00:00:00 festgelegt.|  
|Nur TIME|Der DATE-Teil wird standardmäßig auf 1900-1-1 festgelegt.|  
|Nur TIMEZONE|Standardwerte werden festgelegt.|  
|DATE + TIME|Trivial|  
|DATE + TIMEZONE|Nicht zulässig.|  
|TIME + TIMEZONE|Der DATE-Teil wird standardmäßig auf 1900-1-1 festgelegt. TIMEZONE-Eingabe wird ignoriert.|  
|DATE + TIME + TIMEZONE|Die lokale DATETIME wird verwendet.|  
  
## <a name="examples"></a>Beispiele  
Das folgende Beispiel vergleicht die Ergebnisse der Umwandlung einer Zeichenfolge in alle **Datum** und **Zeit** -Datentyp.
  
```sql
SELECT   
     CAST('2007-05-08 12:35:29. 1234567 +12:15' AS time(7)) AS 'time'   
    ,CAST('2007-05-08 12:35:29. 1234567 +12:15' AS date) AS 'date'   
    ,CAST('2007-05-08 12:35:29.123' AS smalldatetime) AS   
        'smalldatetime'   
    ,CAST('2007-05-08 12:35:29.123' AS datetime) AS 'datetime'   
    ,CAST('2007-05-08 12:35:29. 1234567 +12:15' AS datetime2(7)) AS   
        'datetime2'  
    ,CAST('2007-05-08 12:35:29.1234567 +12:15' AS datetimeoffset(7)) AS   
        'datetimeoffset';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
|Datentyp|Ausgabe|  
|---|---|
|**Uhrzeit**|12:35:29. 1234567|  
|**Datum**|2007-05-08|  
|**smalldatetime**|2007-05-08 12:35:00|  
|**datetime**|2007-05-08 12:35:29.123|  
|**datetime2**|2007-05-08 12:35:29. 1234567|  
|**datetimeoffset**|2007-05-08 12:35:29.1234567 +12:15|  
  
## <a name="see-also"></a>Siehe auch
[CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  


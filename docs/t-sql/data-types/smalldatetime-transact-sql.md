---
title: smalldatetime (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 7/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|data-types
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- smalldatetime_TSQL
- smalldatetime
dev_langs:
- TSQL
helpviewer_keywords:
- time [SQL Server], data types
- smalldatetime data type [SQL Server]
- dates [SQL Server], data types
- date and time [SQL Server], smalldatetime
- data types [SQL Server], date and time
ms.assetid: 68b74610-d54c-4c8e-b4b2-7e3747546ee0
caps.latest.revision: 50
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: cf5273a362de4a4eb86f266d252fe4c853900e1c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="smalldatetime-transact-sql"></a>smalldatetime (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Definiert ein Datum, das mit einer Uhrzeit kombiniert wird. Die Uhrzeit basiert auf dem 24-Stunden-Format, wobei die Sekunden immer 0 sind (:00) und es keine Sekundenbruchteile gibt.
  
> [!NOTE]  
>  Verwenden Sie die Datentypen **time**, **date**, **datetime2** und **datetimeoffset** für neue Arbeiten. Diese Typen entsprechen dem SQL-Standard. Sie lassen sich besser portieren. Durch **time**, **datetime2** and **datetimeoffset** wird eine höhere Genauigkeit in Sekunden unterstützt. **datetimeoffset** unterstützt Zeitzonen für global bereitgestellte Anwendungen.  
  
## <a name="smalldatetime-description"></a>Beschreibung von „smalldatetime“
  
|||  
|-|-|  
|Syntax|**smalldatetime**|  
|Verwendung|DECLARE @MySmalldatetime **smalldatetime**<br /><br /> CREATE TABLE Table1 ( Column1 **smalldatetime** )|  
|Standardmäßige Formate der Zeichenfolgenliterale<br /><br /> (wird für Downlevelclients verwendet)|Nicht verfügbar|  
|Datumsbereich|1900-01-01 bis 2079-06-06<br /><br /> Zwischen dem 1. Januar 1900 und dem 6. Juni 2079|  
|Uhrzeitbereich|00:00:00 bis 23:59:59<br /><br /> 2007-05-09 23:59:59 wird aufgerundet auf<br /><br /> 2007-05-10 00:00:00|  
|Elementbereiche|Bei YYYY handelt es sich um vier Ziffern im Berich von 1900 bis 2079, die ein Jahr darstellen.<br /><br /> Bei MM handelt es sich um zwei Ziffern im Bereich von 01 bis 12, die im angegebenen Jahr einen Monat darstellen.<br /><br /> Bei DD handelt es sich um zwei Ziffern im Bereich von 01 bis 31, die im angegebenen Monat einen Tag darstellen.<br /><br /> Bei hh handelt es sich um zwei Ziffern im Bereich von 00 bis 23, die die Stunde darstellen.<br /><br /> Bei mm handelt es sich um zwei Ziffern im Bereich von 00 bis 59, die die Minute darstellen.<br /><br /> Bei ss handelt es sich um zwei Ziffern im Bereich von 00 bis 59, die die Sekunde darstellen. Werte, die kleiner oder gleich 29,998 Sekunden sind, werden auf die nächste Minute abgerundet; Werte, die größer oder gleich 29,999 Sekunden sind, werden auf die nächste Minute aufgerundet.|  
|Zeichenlänge|Maximal 19 Positionen|  
|Speichergröße|4 Bytes, feste Größe|  
|Genauigkeit|Eine Minute|  
|Standardwert|1900-01-01 00:00:00|  
|Kalender|Gregorianisch<br /><br /> (schließt nicht den vollständigen Bereich von Jahren ein)|  
|Benutzerdefinierte Genauigkeit in Sekundenbruchteilen|nein|  
|Beachtung und Beibehaltung des Zeitzonenoffsets|nein|  
|Beachtung der Sommerzeit|nein|  
  
## <a name="ansi-and-iso-8601-compliance"></a>Kompatibilität mit ANSI und ISO 8601  
**smalldatetime** ist nicht mit ANSI oder ISO 8601 kompatibel.
  
## <a name="converting-date-and-time-data"></a>Konvertieren von Datums- und Uhrzeitdaten
Beim Konvertieren in date- und time-Datentypen lehnt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] alle Werte ab, die nicht als Datum oder Uhrzeit erkannt werden. Informationen zur Verwendung der CAST-Funktion und der CONVERT-Funktion mit Datums- und Uhrzeitdaten finden Sie unter [CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md).
  
### <a name="converting-smalldatetime-to-other-date-and-time-types"></a>Konvertieren von smalldatetime-Werten in andere Datums- und Uhrzeittypen
Der folgende Abschnitt veranschaulicht die Abläufe bei der Konvertierung des **smalldatetime**-Datentyps in andere Datums- und Uhrzeitdatentypen.
  
Beim Konvertieren in **date** werden das Jahr, der Monat und der Tag kopiert. Der folgende Code zeigt die Ergebnisse der Konvertierung eines `smalldatetime`-Werts in einen `date`-Wert.
  
```sql
DECLARE @smalldatetime smalldatetime = '1955-12-13 12:43:10';  
DECLARE @date date = @smalldatetime  
  
SELECT @smalldatetime AS '@smalldatetime', @date AS 'date';  
  
--Result  
--@smalldatetime          date  
------------------------- ----------  
--1955-12-13 12:43:00     1955-12-13  
--  
--(1 row(s) affected)  
```  
  
Beim Konvertieren in **time(n)** werden die Stunden, die Minuten und die Sekunden kopiert. Die Sekundenbruchteile werden auf 0 festgelegt. Der folgende Code zeigt die Ergebnisse der Konvertierung eines `smalldatetime`-Werts in einen `time(4)`-Wert.
  
```sql
DECLARE @smalldatetime smalldatetime = '1955-12-13 12:43:10';  
DECLARE @time time(4) = @smalldatetime;  
  
SELECT @smalldatetime AS '@smalldatetime', @time AS 'time';  
  
--Result  
--@smalldatetime          time  
------------------------- -------------  
--1955-12-13 12:43:00     12:43:00.0000  
--  
--(1 row(s) affected)  
```  
  
Beim Konvertieren in **datetime** wird der **smalldatetime**-Wert in den **datetime**-Wert kopiert. Die Sekundenbruchteile werden auf 0 festgelegt. Der folgende Code zeigt die Ergebnisse der Konvertierung eines `smalldatetime`-Werts in einen `datetime`-Wert.
  
```sql
DECLARE @smalldatetime smalldatetime = '1955-12-13 12:43:10';  
DECLARE @datetime datetime = @smalldatetime;  
  
SELECT @smalldatetime AS '@smalldatetime', @datetime AS 'datetime';  
  
--Result  
--@smalldatetime          datetime  
------------------------- -----------------------  
--1955-12-13 12:43:00     1955-12-13 12:43:00.000  
--  
--(1 row(s) affected)  
```  
  
Beim Konvertieren in **datetimeoffset(n)** wird der **smalldatetime**-Wert in den **datetimeoffset(n)**-Wert kopiert. Die Sekundenbruchteile werden auf 0 und der Zeitzonenoffset auf +00:0 festgelegt. Der folgende Code zeigt die Ergebnisse der Konvertierung eines `smalldatetime`-Werts in einen `datetimeoffset(4)`-Wert.
  
```sql
DECLARE @smalldatetime smalldatetime = '1955-12-13 12:43:10';  
DECLARE @datetimeoffset datetimeoffset(4) = @smalldatetime;  
  
SELECT @smalldatetime AS '@smalldatetime', @datetimeoffset AS 'datetimeoffset(4)';  
  
--Result  
--@smalldatetime          datetimeoffset(4)  
------------------------- ------------------------------  
--1955-12-13 12:43:00     1955-12-13 12:43:00.0000 +00:0  
--  
--(1 row(s) affected)  
```  
  
Beim Konvertieren in **datetime2(n)** wird der **smalldatetime**-Wert in den **datetime2(n)**-Wert kopiert. Die Sekundenbruchteile werden auf 0 festgelegt. Der folgende Code zeigt die Ergebnisse der Konvertierung eines `smalldatetime`-Werts in einen `datetime2(4)`-Wert.
  
```sql
DECLARE @smalldatetime smalldatetime = '1955-12-13 12:43:10';  
DECLARE @datetime2 datetime2(4) = @smalldatetime;  
  
SELECT @smalldatetime AS '@smalldatetime', @datetime2 AS ' datetime2(4)';  
  
--Result  
--@smalldatetime           datetime2(4)  
------------------------- ------------------------  
--1955-12-13 12:43:00     1955-12-13 12:43:00.0000  
--  
--(1 row(s) affected)  
```  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-casting-string-literals-with-seconds-to-smalldatetime"></a>A. Umwandeln von Zeichenfolgenliteralen mit Sekunden in smalldatetime  
Im folgenden Beispiel wird die Konvertierung von Sekunden in Zeichenfolgenliteralen in `smalldatetime` verglichen.
  
```sql
SELECT   
     CAST('2007-05-08 12:35:29'     AS smalldatetime)  
    ,CAST('2007-05-08 12:35:30'     AS smalldatetime)  
    ,CAST('2007-05-08 12:59:59.998' AS smalldatetime);  
```  
  
|Eingabe|Ausgabe|  
|---|---|
|2007-05-08 12:35:29|2007-05-08 12:35:00|  
|2007-05-08 12:35:30|2007-05-08 12:36:00|  
|2007-05-08 12:59:59.998|2007-05-08 13:00:00|  
  
### <a name="b-comparing-date-and-time-data-types"></a>B. Vergleich von Datums- und Uhrzeitdatentypen  
Im folgenden Beispiel werden die Ergebnisse der Umwandlung von einer Zeichenfolge in alle Datums- und Uhrzeitdatentypen verglichen.
  
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
  
  

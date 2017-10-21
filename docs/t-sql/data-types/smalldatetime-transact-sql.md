---
title: Smalldatetime (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 07012d85a54292fa763a7b291d1b7318b6969ca4
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="smalldatetime-transact-sql"></a>smalldatetime (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Definiert ein Datum, das mit einer Uhrzeit kombiniert wird. Die Uhrzeit basiert auf dem 24-Stunden-Format, wobei die Sekunden immer 0 sind (:00) und es keine Sekundenbruchteile gibt.
  
> [!NOTE]  
>  Verwenden der **Zeit**, **Datum**, **datetime2** und **"DateTimeOffset"** Datentypen auf neue Arbeit. Diese Typen entsprechen dem SQL-Standard. Sie lassen sich besser portieren. **Zeit**, **datetime2** und **"DateTimeOffset"** bieten eine höhere Genauigkeit in Millisekunden. **"DateTimeOffset"** bietet zeitzonenunterstützung für Global bereitgestellte Anwendungen.  
  
## <a name="smalldatetime-description"></a>Beschreibung von smalldatetime
  
|||  
|-|-|  
|Syntax|**smalldatetime**|  
|Verwendung|Deklarieren Sie @MySmalldatetime **Smalldatetime**<br /><br /> Erstellen Sie Tabelle Table1 (Column1 **Smalldatetime** )|  
|Standardmäßige Formate der Zeichenfolgenliterale<br /><br /> (wird für Downlevelclients verwendet)|Nicht verfügbar|  
|Datumsbereich|1900-01-01 bis 2079-06-06<br /><br /> Zwischen dem 1. Januar 1900 und dem 6. Juni 2079|  
|Uhrzeitbereich|00:00:00 bis 23:59:59<br /><br /> 2007-05-09 23:59:59 wird aufgerundet auf<br /><br /> 2007-05-10 00:00:00|  
|Elementbereiche|Bei YYYY handelt es sich um vier Ziffern im Berich von 1900 bis 2079, die ein Jahr darstellen.<br /><br /> MM handelt es sich zwei Ziffern im Bereich von 01 bis 12, die im angegebenen Jahr einen Monat darstellen.<br /><br /> Bei DD handelt es sich um zwei Ziffern im Bereich von 01 bis 31, die im angegebenen Monat einen Tag darstellen.<br /><br /> Bei hh handelt es sich um zwei Ziffern im Bereich von 00 bis 23, die die Stunde darstellen.<br /><br /> Bei mm handelt es sich um zwei Ziffern im Bereich von 00 bis 59, die die Minute darstellen.<br /><br /> Bei ss handelt es sich um zwei Ziffern im Bereich von 00 bis 59, die die Sekunde darstellen. Werte, die kleiner oder gleich 29,998 Sekunden sind, werden auf die nächste Minute abgerundet; Werte, die größer oder gleich 29,999 Sekunden sind, werden auf die nächste Minute aufgerundet.|  
|Zeichenlänge|Maximal 19 Positionen|  
|Speichergröße|4 Bytes, feste Größe|  
|Genauigkeit|Eine Minute|  
|Standardwert|1900-01-01 00:00:00|  
|Kalender|Gregorianisch<br /><br /> (schließt nicht den vollständigen Bereich von Jahren ein)|  
|Benutzerdefinierte Genauigkeit in Sekundenbruchteilen|Nein|  
|Beachtung und Beibehaltung des Zeitzonenoffsets|Nein|  
|Beachtung der Sommerzeit|Nein|  
  
## <a name="ansi-and-iso-8601-compliance"></a>Kompatibilität mit ANSI und ISO 8601  
**Smalldatetime** ist nicht ANSI oder ISO 8601 kompatibel.
  
## <a name="converting-date-and-time-data"></a>Konvertieren von Datums-und Uhrzeitdaten
Beim Konvertieren in date- und time-Datentypen lehnt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] alle Werte ab, die nicht als Datum oder Uhrzeit erkannt werden. Informationen zum Verwenden von CAST und CONVERT-Funktionen mit Datums-und Uhrzeitdaten finden Sie unter [CAST und CONVERT &#40; Transact-SQL &#41; ](../../t-sql/functions/cast-and-convert-transact-sql.md).
  
### <a name="converting-smalldatetime-to-other-date-and-time-types"></a>Konvertieren von Smalldatetime in andere Datums- und Uhrzeittypen
In diesem Abschnitt wird beschrieben, was geschieht, wenn eine **Smalldatetime** -Datentyp in andere Datentypen für Datum und Uhrzeit konvertiert wird.
  
Bei der Konvertierung in **Datum**, Jahr, Monat und Tag werden kopiert. Der folgende Code zeigt die Ergebnisse der Konvertierung eines `smalldatetime`-Werts in einen `date`-Wert.
  
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
  
Wenn die Konvertierung erfolgt in **Time(n)-Werte**, die Stunden, Minuten und Sekunden werden kopiert. Die Sekundenbruchteile werden auf 0 festgelegt. Der folgende Code zeigt die Ergebnisse der Konvertierung eines `smalldatetime`-Werts in einen `time(4)`-Wert.
  
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
  
Wenn die Konvertierung erfolgt in **"DateTime"**, **Smalldatetime** Wert wird kopiert, um die **"DateTime"** Wert. Die Sekundenbruchteile werden auf 0 festgelegt. Der folgende Code zeigt die Ergebnisse der Konvertierung eines `smalldatetime`-Werts in einen `datetime`-Wert.
  
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
  
Bei der Konvertierung in **DateTimeOffset (n)**, **Smalldatetime** Wert wird kopiert, um die **DateTimeOffset (n)** Wert. Die Sekundenbruchteile werden auf 0 und der Zeitzonenoffset auf +00:0 festgelegt. Der folgende Code zeigt die Ergebnisse der Konvertierung eines `smalldatetime`-Werts in einen `datetimeoffset(4)`-Wert.
  
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
  
Für die Konvertierung in **datetime2(n)**, **Smalldatetime** Wert wird kopiert, um die **datetime2(n)** Wert. Die Sekundenbruchteile werden auf 0 festgelegt. Der folgende Code zeigt die Ergebnisse der Konvertierung eines `smalldatetime`-Werts in einen `datetime2(4)`-Wert.
  
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
  
### <a name="b-comparing-date-and-time-data-types"></a>B. Vergleichen von Datums-und Uhrzeitdatentypen  
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
  
  


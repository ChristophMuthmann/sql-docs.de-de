---
title: DateTime (Transact-SQL) | Microsoft Docs
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
- datetime_TSQL
- datetime
dev_langs:
- TSQL
helpviewer_keywords:
- time [SQL Server], data types
- date and time [SQL Server], datetime
- dates [SQL Server], data types
- datetime data type [SQL Server]
- data types [SQL Server], date and time
ms.assetid: 9bd1cc5b-227b-4032-95d6-7581ddcc9924
caps.latest.revision: 64
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ae40eaacd6fd441ce0bdbadd3af02b7b189704a2
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="datetime-transact-sql"></a>datetime (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Definiert ein Datum, das mit einer Uhrzeit mit Sekundenbruchteilen kombiniert ist und auf dem 24-Stunden-Format basiert.
  
> [!NOTE]  
>  Verwenden der **Zeit**, **Datum**, **datetime2** und **"DateTimeOffset"** Datentypen auf neue Arbeit. Diese Typen entsprechen dem SQL-Standard. Sie lassen sich besser portieren. **Zeit**, **datetime2** und **"DateTimeOffset"** bieten eine höhere Genauigkeit in Millisekunden. **"DateTimeOffset"** bietet zeitzonenunterstützung für Global bereitgestellte Anwendungen.  
  
## <a name="datetime-description"></a>Beschreibung von datetime  
  
|Eigenschaft|Wert|  
|---|---|
|Syntax|**datetime**|  
|Verwendung|Deklarieren Sie @MyDatetime **"DateTime"**<br /><br /> Erstellen Sie Tabelle Table1 (Column1 **"DateTime"** )|  
|Standardmäßige Formate der Zeichenfolgenliterale<br /><br /> (wird für Downlevelclients verwendet)|Nicht verfügbar|  
|Datumsbereich|Zwischen dem 01.01.53 und dem 31.12.99|  
|Uhrzeitbereich|00:00:00 bis 23:59:59.997|  
|Zeitzonenoffsetbereich|Keine|  
|Elementbereiche|Bei YYYY handelt es sich um vier Ziffern von 1753 bis 9999, die ein Jahr darstellen.<br /><br /> MM handelt es sich zwei Ziffern im Bereich von 01 bis 12, die im angegebenen Jahr einen Monat darstellen.<br /><br /> Bei DD handelt es sich um zwei Ziffern im Bereich von 01 bis 31, die im angegebenen Monat einen Tag darstellen.<br /><br /> Bei hh handelt es sich um zwei Ziffern im Bereich von 00 bis 23, die die Stunde darstellen.<br /><br /> Bei mm handelt es sich um zwei Ziffern im Bereich von 00 bis 59, die die Minute darstellen.<br /><br /> Bei ss handelt es sich um zwei Ziffern im Bereich von 00 bis 59, die die Sekunde darstellen.<br /><br /> Bei n* handelt es sich um drei Ziffern im Bereich von 0 bis 999, die die Sekundenbruchteile darstellen.|  
|Zeichenlänge|Mindestens 19 Positionen bis maximal 23 Positionen|  
|Speichergröße|8 Byte|  
|Genauigkeit|Gerundet in Inkrementen von 0,000, 0,003 oder 0,007 Sekunden|  
|Standardwert|1900-01-01 00:00:00|  
|Kalender|Gregorianisch (schließt nicht den vollständigen Bereich von Jahren ein)|  
|Benutzerdefinierte Genauigkeit in Sekundenbruchteilen|Nein|  
|Beachtung und Beibehaltung des Zeitzonenoffsets|Nein|  
|Beachtung der Sommerzeit|Nein|  
  
## <a name="supported-string-literal-formats-for-datetime"></a>Unterstützte Formate der Zeichenfolgenliterale für datetime  
Die folgenden Tabellen enthalten die unterstützten Formate der Zeichenfolgenliterale für **"DateTime"**. Außer bei ODBC stehen **"DateTime"** Zeichenfolgenliterale sind in einfache Anführungszeichen ('), z. B. 'String_literaL'. Wenn die Umgebung nicht **Us_english**, sollten die Zeichenfolgenliterale in das Format N 'String_literaL' sein.
  
|Numerisch|Description|  
|---|---|
|Datumsformate:<br /><br /> [0]4/15/[19]96 -- (mdy)<br /><br /> [0]4-15-[19]96 -- (mdy)<br /><br /> [0]4.15.[19]96 -- (mdy)<br /><br /> [0]4/[19]96/15 -- (myd)<br /><br /> 15/[0]4/[19]96 -- (dmy)<br /><br /> 15/[19]96/[0]4 -- (dym)<br /><br /> [19]96/15/[0]4 -- (ydm)<br /><br /> [19]96/[0]4/15 -- (ymd)<br /><br /> Zeitformate:<br /><br /> 14:30<br /><br /> 14:30[:20:999]<br /><br /> 14:30[:20.9]<br /><br /> 4am<br /><br /> 4 PM|Sie können Datumsdaten mit der numerischen Angabe eines Monats angeben. So stellt z. B. das Datum 5/20/97 das Jahr 1997 und den zwanzigsten Tag des Monats Mai dar. Wenn Sie das numerische Datumsformat verwenden, müssen Sie den Monat, den Tag und das Jahr in einer Zeichenfolge mit Schrägstrichen (/), Bindestrichen (-) oder Punkten (.) als Trennzeichen angeben. Diese Zeichenfolge muss das folgende Format haben:<br /><br /> *Zahl Trennzeichen Zahl Trennzeichen Zahl [Time] [Uhrzeit]*<br /><br /> <br /><br /> Wenn die festgelegte Sprache **Us_english**, die Standardreihenfolge für das Datum wird Mdy. Sie können die Reihenfolge ändern, indem Sie mit der [SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md) Anweisung.<br /><br /> Die SET DATEFORMAT-Einstellung bestimmt, wie Datumsangaben interpretiert werden. Wenn die Reihenfolge nicht mit der Einstellung übereinstimmt, werden die Werte nicht als Datumsangabe interpretiert, da sie außerhalb des Bereichs liegen, oder die Werte werden falsch interpretiert. Beispielsweise gibt es für 12/10/08 je nach der DATEFORMAT-Einstellung sechs verschiedene Interpretationen. Eine vierstellige Jahresangabe wird als Jahr interpretiert.|  
  
|Alphabetische|Description|  
|---|---|
|Apr[il] [15][,] 1996<br /><br /> Apr[il] 15[,] [19]96<br /><br /> Apr[il] 1996 [15]<br /><br /> [15] Apr[il][,] 1996<br /><br /> 15 Apr[il][,][19]96<br /><br /> 15 [19]96 apr[il]<br /><br /> [15] 1996 apr[il]<br /><br /> 1996 APR[IL] [15]<br /><br /> 1996 [15] APR[IL]|Sie können Datumsdaten mit einem Monat angeben, der mit dem vollständigen Monatsnamen angegeben wird. Dabei können Sie beispielsweise den vollständigen Monatsnamen April oder die in der aktuellen Sprache angegebene Abkürzung für den Monat, z. B. Apr, angeben. Kommas können optional verwendet werden; die Groß-/Kleinschreibung wird ignoriert.<br /><br /> Es folgen einige Richtlinien für die Verwendung von alphabetischen Datumsformaten:<br /><br /> (1) schließen Sie die Datums- und Zeitdaten in einfache Anführungszeichen ('). Verwenden Sie N' für andere Sprachen als Englisch.<br /><br /> (2)-Zeichen, die in Klammern eingeschlossen sind, sind optional.<br /><br /> (3) Wenn Sie nur die letzten zwei Ziffern des Jahres angeben, Werte, die niedriger als die letzten zwei Ziffern des Werts der [konfigurieren two Digit Year cutoff Server Configuration Option](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md) -Konfigurationsoption gelten, gelten im selben Jahrhundert wie das Umstellungsjahr . Werte größer als oder gleich dem Wert dieser Option werden in dem Jahrhundert, das dem Umstellungsjahr vorangeht. Z. B. wenn **zweistelligen Jahresangabe Umstellungsjahr für Angaben mit** Wert 2050 hat (Standardeinstellung), 25 als 2025 interpretiert und 50 als 1950 interpretiert. Um Mehrdeutigkeiten zu vermeiden, sollten Sie vierstellige Jahreszahlen verwenden.<br /><br /> (4) Wenn der Tag fehlt, wird der erste Tag des Monats bereitgestellt.<br /><br /> <br /><br /> Die SET DATEFORMAT-Sitzungseinstellung wird nicht angewendet, wenn Sie den Monat in alphabetischer Form (als Wort) angeben.|  
  
|ISO 8601|Description|  
|---|---|
|YYYY-MM-DDThh:mm:ss[.mmm]<br /><br /> YYYYMMDD[ hh:mm:ss[.mmm]]|Beispiele:<br /><br /> (1) 2004-05-23T14:25:10<br /><br /> (2) 2004-05-23T14:25:10.487<br /><br /> <br /><br /> Wenn Sie das ISO 8601-Format verwenden, müssen Sie jedes Element in diesem Format angeben. Dies beinhaltet auch die **T**, die Doppelpunkte (:) und den Punkt (.), die in diesem Format aufgeführt werden.<br /><br /> Die eckigen Klammern zeigen, dass der Teil, der die Sekunden angibt, optional ist. Die Uhrzeit wird im 24-Stunden-Format angegeben.<br /><br /> Der Buchstabe T Zeigt den Beginn des Uhrzeitteils des der **"DateTime"** Wert.<br /><br /> Der Vorteil der Verwendung des ISO 8601-Formats liegt darin, dass es sich um einen internationalen Standard mit eindeutigen Angaben handelt. Darüber hinaus wird dieses Format nicht durch die SET DATEFORMAT beeinflusst oder [SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md) Einstellung.|  
  
|Unstrukturiert|Description|  
|---|---|
|YYYYMMDD hh:mm:ss[.mmm]||  
  
|ODBC|Description|  
|---|---|
|{ ts '1998-05-02 01:23:56.123' }<br /><br /> { d '1990-10-02' }<br /><br /> { t '13:33:41' }|Die ODBC-API definiert Escapesequenzen zur Darstellung von Datums- und Uhrzeitwerten, die in der ODBC-Terminologie als Zeitstempel-Daten bezeichnet werden. Dieses ODBC-Zeitstempel-Format wird auch von der OLE DB-Sprachendefinition (DBGUID-SQL) unterstützt, indem Sie unterstützt die [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB-Anbieter für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Anwendungen, die die ADO-, OLE DB- und ODBC-basierten APIs verwenden, können dieses ODBC-Zeitstempel-Format zur Darstellung von Datums- und Zeitangaben verwenden.<br /><br /> Escapesequenzen für ODBC-Zeitstempel weisen das Format: { *Literal_type* "*für Constant_value*"}:<br /><br /> <br /><br /> - *Literal_type* gibt die Art der Escapesequenz. Zeitstempel-Daten besitzen drei *Literal_type* Spezifizierer:<br />(1) d = nur Datum<br />(2) t = nur Uhrzeit<br />(3) ts = Zeitstempel (Uhrzeit + Datum)<br /><br /> <br /><br /> -"*für Constant_value*" ist der Wert der Escapesequenz. *für Constant_value* führen Sie diese Formate müssen für jeden *Literal_type*.<br />d: jjjj-mm-tt<br />t: hh: mm: [ss.fff]<br />TS: jjjj-mm-tt hh: mm: [ss.fff]|  
  
## <a name="rounding-of-datetime-fractional-second-precision"></a>Runden der Genauigkeit in Sekundenbruchteilen von datetime  
**"DateTime"** Werte werden in Inkrementen von.000,.003 oder.007 Sekunden gerundet, wie in der folgenden Tabelle gezeigt.
  
|Vom Benutzer angegebener Wert|Gespeicherter Systemwert|  
|---|---|
|01/01/98 23:59:59.999|1998-01-02 00:00:00.000|  
|01/01/98 23:59:59.995<br /><br /> 01/01/98 23:59:59.996<br /><br /> 01/01/98 23:59:59.997<br /><br /> 01/01/98 23:59:59.998|1998-01-01 23:59:59.997|  
|01/01/98 23:59:59.992<br /><br /> 01/01/98 23:59:59.993<br /><br /> 01/01/98 23:59:59.994|1998-01-01 23:59:59.993|  
|01/01/98 23:59:59.990<br /><br /> 01/01/98 23:59:59.991|1998-01-01 23:59:59.990|  
  
## <a name="ansi-and-iso-8601-compliance"></a>Kompatibilität mit ANSI und ISO 8601  
**"DateTime"** ist nicht ANSI oder ISO 8601 kompatibel.
  
##  <a name="_datetime"></a>Konvertieren von Datums- und Zeitdaten  
Beim Konvertieren in date- und time-Datentypen lehnt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] alle Werte ab, die nicht als Datum oder Uhrzeit erkannt werden. Informationen zum Verwenden von CAST und CONVERT-Funktionen mit Datums-und Uhrzeitdaten finden Sie unter [CAST und CONVERT &#40; Transact-SQL &#41; ](../../t-sql/functions/cast-and-convert-transact-sql.md).
  
### <a name="converting-other-date-and-time-types-to-the-datetime-data-type"></a>Konvertieren andere Datums- und Uhrzeittypen in den Datentyp "DateTime" 
In diesem Abschnitt wird beschrieben, was geschieht, wenn andere Datentypen für Datum und Uhrzeit, um konvertiert werden die **"DateTime"** -Datentyp.  
  
Wenn die Konvertierung von ist **Datum**, Jahr, Monat und Tag werden kopiert. Die Zeitkomponente wird auf 00:00:00.000 festgelegt. Der folgende Code zeigt die Ergebnisse der Konvertierung eines `date`-Werts in einen `datetime`-Wert.  
  
```sql
DECLARE @date date = '12-21-16';  
DECLARE @datetime datetime = @date;  
  
SELECT @datetime AS '@datetime', @date AS '@date';  
  
--Result  
--@datetime               @date  
------------------------- ----------  
--2016-12-21 00:00:00.000 2016-12-21  
```  
  
Wenn die Konvertierung von ist **Time(n)-Werte**, die Zeitkomponente wird kopiert, und die Datumskomponente wird festgelegt, um "1900-01-01". Bei der Genauigkeit von Bruchteilen der **Time(n)-Werte** Wert größer ist als drei Ziffern, wird der Wert entsprechend abgeschnitten. Das folgende Beispiel zeigt die Ergebnisse der Konvertierung eines `time(4)`-Werts in einen `datetime`-Wert.  
  
```sql
DECLARE @time time(4) = '12:10:05.1237';  
DECLARE @datetime datetime = @time;  
  
SELECT @datetime AS '@datetime', @time AS '@time';  
  
--Result  
--@datetime               @time  
------------------------- -------------  
--1900-01-01 12:10:05.123 12:10:05.1237  
```  
  
Wenn die Konvertierung von ist **Smalldatetime**, in Stunden und Minuten werden kopiert. Die Sekunden und die Sekundenbruchteile werden auf 0 festgelegt. Der folgende Code zeigt die Ergebnisse der Konvertierung eines `smalldatetime`-Werts in einen `datetime`-Wert.  
  
```sql
DECLARE @smalldatetime smalldatetime = '12-01-16 12:32';  
DECLARE @datetime datetime = @smalldatetime;  
  
SELECT @datetime AS '@datetime', @smalldatetime AS '@smalldatetime';  
  
--Result  
--@datetime               @smalldatetime  
------------------------- -----------------------  
--2016-12-01 12:32:00.000 2016-12-01 12:32:00  
```  
  
Wenn die Konvertierung von ist **DateTimeOffset (n)**, die Datums- und Zeitkomponenten werden kopiert. Die Zeitzone wird abgeschnitten. Bei der Genauigkeit von Bruchteilen der **DateTimeOffset (n)** Wert größer ist als drei Ziffern, wird der Wert abgeschnitten. Das folgende Beispiel zeigt die Ergebnisse der Konvertierung eines `datetimeoffset(4)`-Werts in einen `datetime`-Wert.  
  
```sql
DECLARE @datetimeoffset datetimeoffset(4) = '1968-10-23 12:45:37.1234 +10:0';  
DECLARE @datetime datetime = @datetimeoffset;  
  
SELECT @datetime AS '@datetime', @datetimeoffset AS '@datetimeoffset';  
  
--Result  
--@datetime               @datetimeoffset  
------------------------- ------------------------------  
--1968-10-23 12:45:37.123 1968-10-23 12:45:37.1237 +01:0   
```  
  
Wenn die Konvertierung von ist **datetime2(n)**, Datum und Uhrzeit werden kopiert. Bei der Genauigkeit von Bruchteilen der **datetime2(n)** Wert größer ist als drei Ziffern, wird der Wert abgeschnitten. Das folgende Beispiel zeigt die Ergebnisse der Konvertierung eines `datetime2(4)`-Werts in einen `datetime`-Wert.  
  
```sql
DECLARE @datetime2 datetime2(4) = '1968-10-23 12:45:37.1237';  
DECLARE @datetime datetime = @datetime2;  
  
SELECT @datetime AS '@datetime', @datetime2 AS '@datetime2';  
  
--Result  
--@datetime               @datetime2  
------------------------- ------------------------  
--1968-10-23 12:45:37.123 1968-10-23 12:45:37.1237  
```  
  
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
  
  


---
title: datetime (Transact-SQL) | Microsoft-Dokumentation
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 4493e165efbc0410d444f34fc41e30cc08e90307
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="datetime-transact-sql"></a>datetime (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Definiert ein Datum, das mit einer Uhrzeit mit Sekundenbruchteilen kombiniert ist und auf dem 24-Stunden-Format basiert.
  
> [!NOTE]  
>  Verwenden Sie die Datentypen **time**, **date**, **datetime2** und **datetimeoffset** für neue Arbeiten. Diese Typen entsprechen dem SQL-Standard. Sie lassen sich besser portieren. Durch **time**, **datetime2** and **datetimeoffset** wird eine höhere Genauigkeit in Sekunden unterstützt. **datetimeoffset** unterstützt Zeitzonen für global bereitgestellte Anwendungen.  
  
## <a name="datetime-description"></a>Beschreibung von datetime  
  
|Eigenschaft|value|  
|---|---|
|Syntax|**datetime**|  
|Verwendung|DECLARE @MyDatetime **datetime**<br /><br /> CREATE TABLE Table1 ( Column1 **datetime** )|  
|Standardmäßige Formate der Zeichenfolgenliterale<br /><br /> (wird für Downlevelclients verwendet)|Nicht verfügbar|  
|Datumsbereich|Zwischen dem 01.01.53 und dem 31.12.99|  
|Uhrzeitbereich|00:00:00 bis 23:59:59.997|  
|Zeitzonenoffsetbereich|InclusionThresholdSetting|  
|Elementbereiche|Bei YYYY handelt es sich um vier Ziffern von 1753 bis 9999, die ein Jahr darstellen.<br /><br /> Bei MM handelt es sich um zwei Ziffern im Bereich von 01 bis 12, die im angegebenen Jahr einen Monat darstellen.<br /><br /> Bei DD handelt es sich um zwei Ziffern im Bereich von 01 bis 31, die im angegebenen Monat einen Tag darstellen.<br /><br /> Bei hh handelt es sich um zwei Ziffern im Bereich von 00 bis 23, die die Stunde darstellen.<br /><br /> Bei mm handelt es sich um zwei Ziffern im Bereich von 00 bis 59, die die Minute darstellen.<br /><br /> Bei ss handelt es sich um zwei Ziffern im Bereich von 00 bis 59, die die Sekunde darstellen.<br /><br /> Bei n* handelt es sich um drei Ziffern im Bereich von 0 bis 999, die die Sekundenbruchteile darstellen.|  
|Zeichenlänge|Mindestens 19 Positionen bis maximal 23 Positionen|  
|Speichergröße|8 Byte|  
|Genauigkeit|Gerundet in Inkrementen von 0,000, 0,003 oder 0,007 Sekunden|  
|Standardwert|1900-01-01 00:00:00|  
|Kalender|Gregorianisch (schließt nicht den vollständigen Bereich von Jahren ein)|  
|Benutzerdefinierte Genauigkeit in Sekundenbruchteilen|nein|  
|Beachtung und Beibehaltung des Zeitzonenoffsets|nein|  
|Beachtung der Sommerzeit|nein|  
  
## <a name="supported-string-literal-formats-for-datetime"></a>Unterstützte Formate der Zeichenfolgenliterale für datetime  
In den folgenden Tabellen werden die unterstützten Formate für Zeichenfolgenliterale für **datetime** aufgelistet. Außer bei ODBC stehen **datetime**-Zeichenfolgenliterale in einfachen Anführungszeichen ('), z.B. 'string_literaL'. Wenn die Umgebung nicht **us_english** lautet, sollten die Zeichenfolgenliterale das Format N'string_literaL' aufweisen.
  
|Numerisch|Description|  
|---|---|
|Datumsformate:<br /><br /> [0]4/15/[19]96 -- (mdy)<br /><br /> [0]4-15-[19]96 -- (mdy)<br /><br /> [0]4.15.[19]96 -- (mdy)<br /><br /> [0]4/[19]96/15 -- (myd)<br /><br /> 15/[0]4/[19]96 -- (dmy)<br /><br /> 15/[19]96/[0]4 -- (dym)<br /><br /> [19]96/15/[0]4 -- (ydm)<br /><br /> [19]96/[0]4/15 -- (ymd)<br /><br /> Zeitformate:<br /><br /> 14:30<br /><br /> 14:30[:20:999]<br /><br /> 14:30[:20.9]<br /><br /> 4am<br /><br /> 4 PM|Sie können Datumsdaten mit der numerischen Angabe eines Monats angeben. So stellt z. B. das Datum 5/20/97 das Jahr 1997 und den zwanzigsten Tag des Monats Mai dar. Wenn Sie das numerische Datumsformat verwenden, müssen Sie den Monat, den Tag und das Jahr in einer Zeichenfolge mit Schrägstrichen (/), Bindestrichen (-) oder Punkten (.) als Trennzeichen angeben. Diese Zeichenfolge muss das folgende Format haben:<br /><br /> *Zahl Trennzeichen Zahl Trennzeichen number [time] [time]*<br /><br /> <br /><br /> Wenn die festgelegte Sprache **us_english** ist, gilt als Standarddatumsformat mdy. Sie können das Datumsformat mithilfe der [SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md)-Anweisung ändern.<br /><br /> Die SET DATEFORMAT-Einstellung bestimmt, wie Datumsangaben interpretiert werden. Wenn die Reihenfolge nicht mit der Einstellung übereinstimmt, werden die Werte nicht als Datumsangabe interpretiert, da sie außerhalb des Bereichs liegen, oder die Werte werden falsch interpretiert. Beispielsweise gibt es für 12/10/08 je nach der DATEFORMAT-Einstellung sechs verschiedene Interpretationen. Eine vierstellige Jahresangabe wird als Jahr interpretiert.|  
  
|Alphabetisch|Description|  
|---|---|
|Apr[il] [15][,] 1996<br /><br /> Apr[il] 15[,] [19]96<br /><br /> Apr[il] 1996 [15]<br /><br /> [15] Apr[il][,] 1996<br /><br /> 15 Apr[il][,][19]96<br /><br /> 15 [19]96 apr[il]<br /><br /> [15] 1996 apr[il]<br /><br /> 1996 APR[IL] [15]<br /><br /> 1996 [15] APR[IL]|Sie können Datumsdaten mit einem Monat angeben, der mit dem vollständigen Monatsnamen angegeben wird. Dabei können Sie beispielsweise den vollständigen Monatsnamen April oder die in der aktuellen Sprache angegebene Abkürzung für den Monat, z. B. Apr, angeben. Kommas können optional verwendet werden; die Groß-/Kleinschreibung wird ignoriert.<br /><br /> Es folgen einige Richtlinien für die Verwendung von alphabetischen Datumsformaten:<br /><br /> 1) Schließen Sie die Datums- und Zeitdaten in einfache Anführungszeichen ein ('). Verwenden Sie N' für andere Sprachen als Englisch.<br /><br /> 2) Zeichen, die in Klammern eingeschlossen werden, sind optional.<br /><br /> 3) Wenn Sie nur die letzten zwei Ziffern des Jahres angeben, liegen Werte, die niedriger als die letzten zwei Ziffern des Werts von [Konfigurieren des Umstellungsjahres für Angaben mit zwei Ziffern (Serverkonfigurationsoption)](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md) sind, im selben Jahrhundert wie das Umstellungsjahr. Werte, die größer als oder gleich dem Wert dieser Option sind, liegen in dem Jahrhundert, das dem Umstellungsjahr vorangeht. Wenn z.B. **Umstellungsjahr für Angaben mit zwei Ziffern** den Wert 2050 hat (Standardeinstellung), wird das zweistellige Jahr 25 als 2025 und das zweistellige Jahr 50 als 1950 interpretiert. Um Mehrdeutigkeiten zu vermeiden, sollten Sie vierstellige Jahreszahlen verwenden.<br /><br /> 4) Wenn der Tag fehlt, wird der erste Tag des Monats angegeben.<br /><br /> <br /><br /> Die SET DATEFORMAT-Sitzungseinstellung wird nicht angewendet, wenn Sie den Monat in alphabetischer Form (als Wort) angeben.|  
  
|ISO 8601|Description|  
|---|---|
|YYYY-MM-DDThh:mm:ss[.mmm]<br /><br /> YYYYMMDD[ hh:mm:ss[.mmm]]|Beispiele:<br /><br /> 1) 2004-05-23T14:25:10<br /><br /> 2) 2004-05-23T14:25:10.487<br /><br /> <br /><br /> Wenn Sie das ISO 8601-Format verwenden, müssen Sie jedes Element in diesem Format angeben. Dazu gehören auch **T**, die Doppelpunkte (:) und der Punkt (.), die in diesem Format aufgeführt werden.<br /><br /> Die eckigen Klammern zeigen, dass der Teil, der die Sekunden angibt, optional ist. Die Uhrzeit wird im 24-Stunden-Format angegeben.<br /><br /> Der Buchstabe T zeigt den Beginn des Uhrzeitabschnitts des **datetime**-Werts an.<br /><br /> Der Vorteil der Verwendung des ISO 8601-Formats liegt darin, dass es sich um einen internationalen Standard mit eindeutigen Angaben handelt. Außerdem wird dieses Format nicht von der SET DATEFORMAT-Einstellung oder der [SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md)-Einstellung beeinflusst.|  
  
|Unstrukturiert|Description|  
|---|---|
|YYYYMMDD hh:mm:ss[.mmm]||  
  
|ODBC|Description|  
|---|---|
|{ ts '1998-05-02 01:23:56.123' }<br /><br /> { d '1990-10-02' }<br /><br /> { t '13:33:41' }|Die ODBC-API definiert Escapesequenzen zur Darstellung von Datums- und Uhrzeitwerten, die in der ODBC-Terminologie als Zeitstempel-Daten bezeichnet werden. Dieses ODBC-Zeitstempel-Format wird auch von der OLE DB-Sprachendefinition (DBGUID-SQL) unterstützt, die vom OLE DB-Anbieter [!INCLUDE[msCoName](../../includes/msconame-md.md)] für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt wird. Anwendungen, die die ADO-, OLE DB- und ODBC-basierten APIs verwenden, können dieses ODBC-Zeitstempel-Format zur Darstellung von Datums- und Zeitangaben verwenden.<br /><br /> Escapesequenzen für ODBC-Zeitstempel-Daten haben das folgende Format: { *literal_type* '*constant_value*' }:<br /><br /> <br /><br /> - *literal_type* gibt die Art der Escapesequenz an. Zeitstempel-Daten besitzen drei *literal_type*-Bezeichner:<br />1) d = Nur Datum<br />2) t = Nur Uhrzeit<br />3) ts = Zeitstempel (Uhrzeit + Datum)<br /><br /> <br /><br /> *constant_value* ist der Wert der Escapesequenz. Für *constant_value* müssen folgende Formate für jeden *literal_type* gelten.<br />d : yyyy-mm-dd<br />t : hh:mm:ss[.fff]<br />ts : yyyy-mm-dd hh:mm:ss[.fff]|  
  
## <a name="rounding-of-datetime-fractional-second-precision"></a>Runden der Genauigkeit in Sekundenbruchteilen von datetime  
**datetime**-Werte werden in Abschnitten von 0,000, 0,003 oder 0,007 Sekunden gerundet, wie in der folgenden Tabelle dargestellt.
  
|Vom Benutzer angegebener Wert|Gespeicherter Systemwert|  
|---|---|
|01/01/98 23:59:59.999|1998-01-02 00:00:00.000|  
|01/01/98 23:59:59.995<br /><br /> 01/01/98 23:59:59.996<br /><br /> 01/01/98 23:59:59.997<br /><br /> 01/01/98 23:59:59.998|1998-01-01 23:59:59.997|  
|01/01/98 23:59:59.992<br /><br /> 01/01/98 23:59:59.993<br /><br /> 01/01/98 23:59:59.994|1998-01-01 23:59:59.993|  
|01/01/98 23:59:59.990<br /><br /> 01/01/98 23:59:59.991|1998-01-01 23:59:59.990|  
  
## <a name="ansi-and-iso-8601-compliance"></a>Kompatibilität mit ANSI und ISO 8601  
**datetime** ist nicht mit ANSI oder ISO 8601 kompatibel.
  
##  <a name="_datetime"></a> Konvertieren von Datums- und Zeitdaten  
Beim Konvertieren in date- und time-Datentypen lehnt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] alle Werte ab, die nicht als Datum oder Uhrzeit erkannt werden. Informationen zur Verwendung der CAST-Funktion und der CONVERT-Funktion mit Datums- und Uhrzeitdaten finden Sie unter [CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md).
  
### <a name="converting-other-date-and-time-types-to-the-datetime-data-type"></a>Konvertieren anderer Datums- und Uhrzeittypen in den datetime-Datentyp 
Der folgende Abschnitt veranschaulicht die Abläufe bei der Konvertierung des **datetime**-Datentyps in andere Datums- und Uhrzeitdatentypen.  
  
Beim Konvertieren in **date** werden das Jahr, der Monat und der Tag kopiert. Die Zeitkomponente wird auf 00:00:00.000 festgelegt. Der folgende Code zeigt die Ergebnisse der Konvertierung eines `date`-Werts in einen `datetime`-Wert.  
  
```sql
DECLARE @date date = '12-21-16';  
DECLARE @datetime datetime = @date;  
  
SELECT @datetime AS '@datetime', @date AS '@date';  
  
--Result  
--@datetime               @date  
------------------------- ----------  
--2016-12-21 00:00:00.000 2016-12-21  
```  
  
Beim Konvertieren von **time(n)** wird die Zeitkomponente kopiert, und die Datumskomponente wird auf „1900-01-01“ festgelegt. Wenn die Genauigkeit des **time(n)**-Werts größer ist als drei Sekundenbruchteile, wird der Wert gekürzt, damit er passt. Das folgende Beispiel zeigt die Ergebnisse der Konvertierung eines `time(4)`-Werts in einen `datetime`-Wert.  
  
```sql
DECLARE @time time(4) = '12:10:05.1237';  
DECLARE @datetime datetime = @time;  
  
SELECT @datetime AS '@datetime', @time AS '@time';  
  
--Result  
--@datetime               @time  
------------------------- -------------  
--1900-01-01 12:10:05.123 12:10:05.1237  
```  
  
Wenn die Konvertierung von **samlldatetime** erfolgt, werden die Stunden und Minuten kopiert. Die Sekunden und die Sekundenbruchteile werden auf 0 festgelegt. Der folgende Code zeigt die Ergebnisse der Konvertierung eines `smalldatetime`-Werts in einen `datetime`-Wert.  
  
```sql
DECLARE @smalldatetime smalldatetime = '12-01-16 12:32';  
DECLARE @datetime datetime = @smalldatetime;  
  
SELECT @datetime AS '@datetime', @smalldatetime AS '@smalldatetime';  
  
--Result  
--@datetime               @smalldatetime  
------------------------- -----------------------  
--2016-12-01 12:32:00.000 2016-12-01 12:32:00  
```  
  
Wenn die Konvertierung von **datetimeoffset(n)** erfolgt, werden die Datums- und Uhrzeitkomponenten kopiert. Die Zeitzone wird abgeschnitten. Wenn die Sekundenbruchteil-Genauigkeit des **datetimeoffset(n)**-Werts um mehr als drei Stellen abweicht, wird der Wert gekürzt. Das folgende Beispiel zeigt die Ergebnisse der Konvertierung eines `datetimeoffset(4)`-Werts in einen `datetime`-Wert.  
  
```sql
DECLARE @datetimeoffset datetimeoffset(4) = '1968-10-23 12:45:37.1234 +10:0';  
DECLARE @datetime datetime = @datetimeoffset;  
  
SELECT @datetime AS '@datetime', @datetimeoffset AS '@datetimeoffset';  
  
--Result  
--@datetime               @datetimeoffset  
------------------------- ------------------------------  
--1968-10-23 12:45:37.123 1968-10-23 12:45:37.1237 +01:0   
```  
  
Wenn die Konvertierung von **datetime2(n)** erfolgt, werden Datum und Uhrzeit kopiert. Wenn die Sekundenbruchteil-Genauigkeit des **datetime2(n)**-Werts um mehr als drei Stellen abweicht, wird der Wert gekürzt. Das folgende Beispiel zeigt die Ergebnisse der Konvertierung eines `datetime2(4)`-Werts in einen `datetime`-Wert.  
  
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
Im folgenden Beispiel werden die Ergebnisse der Umwandlung einer Zeichenfolge in alle **date**- und **time**-Datentypen verglichen.
  
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
  
  

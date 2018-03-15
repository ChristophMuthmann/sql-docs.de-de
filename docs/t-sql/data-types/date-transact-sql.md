---
title: date (Transact-SQL) | Microsoft-Dokumentation
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
- date_TSQL
- date
dev_langs:
- TSQL
helpviewer_keywords:
- data types [SQL Server], date
- date and time [SQL Server], date
- dates [SQL Server], data types
- date data type [SQL Server]
- data types [SQL Server], date and time
ms.assetid: c963e8b4-5a85-4bd0-9d48-3f8da8f6516b
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 1776f70f2136f7b46fe3aa9205f76108a2807170
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/08/2018
---
# <a name="date-transact-sql"></a>date (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Definiert ein Datum in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
## <a name="date-description"></a>Beschreibung von „date“
  
|Eigenschaft|value|  
|--------------|-----------|  
|Syntax|**Datum**|  
|Verwendung|Deklarieren Sie @MyDate **date**.<br /><br /> CREATE TABLE Table1 ( Column1 **date** )|  
|Standardmäßiges Format der Zeichenfolgenliterale<br /><br /> (wird für Downlevelclients verwendet)|YYYY-MM-DD<br /><br /> Weitere Informationen finden Sie im nachfolgenden Abschnitt „Abwärtskompatibilität für Downlevelclients“.|  
|Bereich|0001-01-01 bis 9999-12-31 (1582-10-15 bis 9999-12-31 für Informatica)<br /><br /> 1. Januar 1 bis zum 31. Dezember 9999 (15. Oktober 1582 bis zum 31. Dezember 9999 für Informatica)|  
|Elementbereiche|Bei YYYY handelt es sich um vier Ziffern von 0001 bis 9999, die ein Jahr darstellen. Für Informatica ist JJJJ auf den Bereich 1582 bis 9999 beschränkt.<br /><br /> Bei MM handelt es sich um zwei Ziffern von 01 bis 12, die im angegebenen Jahr einen Monat darstellen.<br /><br /> Bei DD handelt es sich um zwei Ziffern von 01 bis 31, die im angegebenen Monat einen Tag darstellen.|  
|Zeichenlänge|10 Stellen|  
|Genauigkeit, Dezimalstellen|10, 0|  
|Speichergröße|3 Bytes, feste Größe|  
|Speicherstruktur|1 ganze Zahl mit 3 Bytes speichert das Datum.|  
|Genauigkeit|Ein Tag|  
|Standardwert|1900-01-01<br /><br /> Dieser Wert wird für den angefügten Datumsteil für eine implizite Konvertierung von **time** in **datetime2** oder **DateTimeOffset** verwendet.|  
|Kalender|Gregorianisch|  
|Benutzerdefinierte Genauigkeit in Sekundenbruchteilen|nein|  
|Beachtung und Beibehaltung des Zeitzonenoffsets|nein|  
|Beachtung der Sommerzeit|nein|  
  
## <a name="supported-string-literal-formats-for-date"></a>Unterstützte Formate der Zeichenfolgenliterale für date
In den folgenden Tabellen werden die gültigen Formate der Zeichenfolgenliterale für den **date**-Datentyp aufgeführt.
  
|Numerisch|Description|  
|-------------|-----------------|  
|dmy<br /><br /> [m]m/dd/[yy]yy<br /><br /> [m]m-dd-[yy]yy<br /><br /> [m]m.dd.[yy]yy<br /><br /> myd<br /><br /> mm/[yy]yy/dd<br /><br /> mm-[yy]yy/dd<br /><br /> [m]m.[yy]yy.dd<br /><br /> dmy<br /><br /> dd/[m]m/[yy]yy<br /><br /> dd-[m]m-[yy]yy<br /><br /> dd.[m]m.[yy]yy<br /><br /> dym<br /><br /> dd/[yy]yy/[m]m<br /><br /> dd-[yy]yy-[m]m<br /><br /> dd.[yy]yy.[m]m<br /><br /> ymd<br /><br /> [yy]yy/[m]m/dd<br /><br /> [yy]yy-[m]m-dd<br /><br /> [yy]yy-[m]m-dd|[m]m, dd und [yy]yy stellen den Monat, den Tag und das Jahr in einer Zeichenfolge mit Schrägstrichen (/), Bindestrichen (-) oder Punkten (.) als Trennzeichen dar.<br /><br /> Es werden nur vier- oder zweistellige Jahreszahlen unterstützt. Verwenden Sie nach Möglichkeit immer vierstellige Jahreszahlen. Verwenden Sie die Option [Konfigurieren des Umstellungsjahres für Angaben mit zwei Ziffern](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md), um eine ganze Zahl zwischen 0001 und 9999 anzugeben, die das Umstellungsjahr für das Interpretieren zweistelliger Jahre als vierstellige Jahre darstellt.<br /><br /> **Hinweis!** Für Informatica ist JJJJ auf den Bereich 1582 bis 9999 beschränkt.<br /><br /> Ein zweistelliges Jahr, das kleiner als oder gleich den letzten zwei Ziffern des Umstellungsjahres ist, liegt im selben Jahrhundert wie das Umstellungsjahr. Ein zweistelliges Jahr, das größer als die letzten zwei Ziffern des Umstellungsjahres ist, liegt im Jahrhundert vor dem Umstellungsjahr. Wenn z. B. two-digit year cutoff den Standardwert 2049 annimmt, wird das zweistellige Jahr 49 als 2049 und das zweistellige Jahr 50 als 1950 interpretiert.<br /><br /> Das Standarddatumsformat wird von der aktuellen Spracheinstellung bestimmt. Sie können das Datumsformat ändern, indem Sie die Anweisungen [SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md) und [SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md) verwenden.<br /><br /> Das **ydm**-Format wird nicht für **date** unterstützt.|  
  
|Alphabetisch|Description|  
|------------------|-----------------|  
|mon [dd][,] yyyy<br /><br /> mon dd[,] [yy]yy<br /><br /> mon yyyy [dd]<br /><br /> [dd] mon[,] yyyy<br /><br /> dd mon[,][yy]yy<br /><br /> dd [yy]yy mon<br /><br /> [dd] yyyy mon<br /><br /> yyyy mon [dd]<br /><br /> yyyy [dd] mon|**mon** stellt den vollständigen Monatsnamen oder die in der aktuellen Sprache angegebene Monatsabkürzung dar. Kommas sind optional, und die Großschreibung wird ignoriert.<br /><br /> Um Mehrdeutigkeiten zu vermeiden, sollten Sie vierstellige Jahreszahlen verwenden.<br /><br /> Wenn der Tag fehlt, wird der erste Tag des Monats angegeben.|  
  
|ISO 8601|Beschreibung|  
|--------------|----------------|  
|YYYY-MM-DD<br /><br /> YYYYMMDD|Identisch mit dem SQL-Standard. Dies ist das einzige Format, das als internationaler Standard definiert ist.|  
  
|Unstrukturiert|Description|  
|-----------------|-----------------|  
|[yy]yymmdd<br /><br /> yyyy[mm][dd]|Die **date**-Daten können mit vier, sechs oder acht Ziffern angegeben werden. Eine Zeichenfolge mit sechs oder acht Ziffern wird immer als **ymd** interpretiert. Monat und Tag müssen immer zweistellig sein. Eine vierstellige Zeichenfolge wird als Jahr interpretiert.|  
  
|ODBC|Description|  
|----------|-----------------|  
|{ d 'yyyy-mm-dd' }|ODBC-API-spezifisch|  
  
|W3C XML-Format|Description|  
|--------------------|-----------------|  
|yyyy-mm-ddTZD|Speziell unterstützt für die XML/SOAP-Verwendung.<br /><br /> TZD ist der Zeitzonenkennzeichner (Z oder +hh:mm oder -hh:mm):<br /><br /> – Der Zeitzonenoffset wird durch hh:mm angegeben. Bei hh handelt es sich um zwei Ziffern im Bereich von 0 bis 14, die die Anzahl der Stunden im Zeitzonenoffset darstellen.<br />– Bei MM handelt es sich um zwei Ziffern im Bereich von 0 bis 59, die die Anzahl der zusätzlichen Minuten im Zeitzonenoffset darstellen.<br />– + (plus) oder – (minus) ist das erforderliche Zeichen des Zeitzonenoffsets. Dieses gibt an, ob der Zeitzonenoffset zu der koordinierten Weltzeit (Coordinated Universal Time, UTC) addiert oder von dieser subtrahiert wird, um die lokale Zeit zu erhalten. Der gültige Zeitzonenoffset liegt im Bereich von -14: 00 bis +14: 00.|  
  
## <a name="ansi-and-iso-8601-compliance"></a>Kompatibilität mit ANSI und ISO 8601  
**date** ist mit der ANSI SQL-Standarddefinition für den gregorianischen Kalender kompatibel: "NOTE 85 - Datetime data types will allow dates in the Gregorian format to be stored in the date range 0001–01–01 CE through 9999–12–31 CE."
  
Das standardmäßige Format der Zeichenfolgenliterale, das für Downlevelclients verwendet wird, ist mit dem SQL-Standard konform, der als YYYY-MM-DD definiert ist. Dieses Format ist mit der Definition von ISO 8601 für DATE identisch.
  
> [!NOTE]  
>  Für Informatica ist der Bereich auf 1582-10-15 (15. Oktober 1582) bis 9999-12-31 (31. Dezember 9999) beschränkt.  
  
## <a name="backward-compatibility-for-down-level-clients"></a>Abwärtskompatibilität für Downlevelclients
Einige Downlevelclients unterstützen nicht die Datentypen **time**, **date**, **datetime2** und **datetimeoffset**. In der folgenden Tabelle wird die Typzuordnung zwischen einer Instanz höherer Ebene in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und Downlevelclients gezeigt.
  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datentyp|Standardmäßiges Format des an Downlevelclients übergebenen Zeichenfolgenliterals|ODBC früherer Versionen|OLEDB früherer Versionen|JDBC früherer Versionen|SQLCLIENT früherer Versionen|  
| --- | --- | --- | --- | --- | --- |
|**Uhrzeit**|hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR oder SQL_VARCHAR|DBTYPE_WSTR oder DBTYPE_STR|Java.sql.String|Zeichenfolge oder SqString|  
|**Datum**|YYYY-MM-DD|SQL_WVARCHAR oder SQL_VARCHAR|DBTYPE_WSTR oder DBTYPE_STR|Java.sql.String|Zeichenfolge oder SqString|  
|**datetime2**|YYYY-MM-DD hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR oder SQL_VARCHAR|DBTYPE_WSTR oder DBTYPE_STR|Java.sql.String|Zeichenfolge oder SqString|  
|**datetimeoffset**|YYYY-MM-DD hh:mm:ss[.nnnnnnn] [+&#124;-]hh:mm|SQL_WVARCHAR oder SQL_VARCHAR|DBTYPE_WSTR oder DBTYPE_STR|Java.sql.String|Zeichenfolge oder SqString|  
  
## <a name="converting-date-and-time-data"></a>Konvertieren von Datums- und Uhrzeitdaten
Beim Konvertieren in date- und time-Datentypen lehnt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] alle Werte ab, die nicht als Datum oder Uhrzeit erkannt werden. Informationen zur Verwendung der CAST-Funktion und der CONVERT-Funktion mit Datums- und Uhrzeitdaten finden Sie unter [CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md).  
  
### <a name="converting-date-to-other-date-and-time-types"></a>Konvertieren von date-Werten in andere Datums- und Uhrzeittypen
Der folgende Abschnitt veranschaulicht die Abläufe bei der Konvertierung des **date**-Datentyps in andere Datums- und Uhrzeittypen.
  
Beim Konvertieren in **time(n)** schlägt die Konvertierung fehl, und die Fehlermeldung 206 "Operandentypkollision: date ist inkompatibel mit time" wird ausgegeben.
  
Beim Konvertieren in **datetime** wird das Datum kopiert. Der folgende Code zeigt die Ergebnisse der Konvertierung eines `date`-Werts in einen `datetime`-Wert.
  
```sql
DECLARE @date date= '12-10-25';  
DECLARE @datetime datetime= @date;  
  
SELECT @date AS '@date', @datetime AS '@datetime';  
  
--Result  
--@date      @datetime  
------------ -----------------------  
--2025-12-10 2025-12-10 00:00:00.000  
--  
--(1 row(s) affected)  
```  
  
Beim Konvertieren in **smalldatetime** liegt der **Datum**-Wert im Bereich von [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md), die Datumskomponente wird kopiert, und die Uhrzeitkomponente wird auf „00:00:00.000“ festgelegt. Wenn der **date**-Wert außerhalb des Bereichs eines **smalldatetime**-Werts liegt, wird die Fehlermeldung 242 "Bei der Konvertierung eines date-Datentyps in einen smalldatetime-Datentyp liegt der Wert außerhalb des gültigen Bereichs" ausgegeben, und der **smalldatetime**-Wert wird auf NULL gesetzt. Der folgende Code zeigt die Ergebnisse der Konvertierung eines `date`-Werts in einen `smalldatetime`-Wert.
  
```sql
DECLARE @date date= '1912-10-25';  
DECLARE @smalldatetime smalldatetime = @date;  
  
SELECT @date AS '@date', @smalldatetime AS '@smalldatetime';  
  
--Result  
--@date      @smalldatetime  
------------ -----------------------  
--1912-10-25 1912-10-25 00:00:00  
--  
--(1 row(s) affected)  
```  
  
Beim Konvertieren in **datetimeoffset(n)** wird das Datum kopiert, und die Uhrzeit wird auf „00:00.0000000 +00:00“ festgelegt.  Der folgende Code zeigt die Ergebnisse der Konvertierung eines `date`-Werts in einen `datetimeoffset(3)`-Wert.
  
```sql
DECLARE @date date = '1912-10-25';  
DECLARE @datetimeoffset datetimeoffset(3) = @date;  
  
SELECT @date AS '@date', @datetimeoffset AS '@datetimeoffset';  
  
--Result  
--@date      @datetimeoffset  
------------ ------------------------------  
--1912-10-25 1912-10-25 00:00:00.000 +00:00  
--  
--(1 row(s) affected)  
```  
  
Beim Konvertieren in **datetime2(n)** wird die Datumskomponente kopiert, und die Uhrzeitkomponente wird auf „00:00.000000“ festgelegt. Der folgende Code zeigt die Ergebnisse der Konvertierung eines `date`-Werts in einen `datetime2(3)`-Wert.
  
```sql
DECLARE @date date = '1912-10-25'  
DECLARE @datetime2 datetime2(3) = @date;  
  
SELECT @date AS '@date', @datetime2 AS '@datetime2(3)';  
  
--Result  
--@date      @datetime2(3)  
------------ -----------------------  
--1912-10-25 1912-10-25 00:00:00.000  
--  
--(1 row(s) affected)  
```  
  
### <a name="converting-string-literals-to-date"></a>Konvertieren von Zeichenfolgenliteralen in ein Datum
Konvertierungen von Zeichenfolgenliteralen in Datums- und Zeitwerte sind erlaubt, wenn alle Teile der Zeichenfolge in gültigen Formaten vorliegen. Andernfalls wird ein Laufzeitfehler ausgelöst. Wird bei impliziten oder expliziten Konvertierungen von Datums- und Zeitwerten in Zeichenfolgenliterale kein Stil angegeben, wird das Standardformat der aktuellen Sitzung verwendet. In der folgenden Tabelle werden die Regeln zum Konvertieren eines Zeichenfolgenliterals in den **date**-Datentyp dargestellt.
  
|Eingabezeichenfolgenliteral|**Datum**|  
|---|---|
|ODBC DATE|Dem **datetime**-Datentyp werden ODBC-Zeichenfolgenliterale zugeordnet. Jede Zuweisungsoperation von ODBC DATETIME-Literalen zu **date**-Typen bewirkt eine implizite Konvertierung zwischen **datetime** und diesen Typen, wie in den Konvertierungsregeln definiert.|  
|ODBC TIME|Siehe vorherige ODBC DATE-Regel.|  
|ODBC DATETIME|Siehe vorherige ODBC DATE-Regel.|  
|Nur DATE|Trivial|  
|Nur TIME|Standardwerte werden festgelegt.|  
|Nur TIMEZONE|Standardwerte werden festgelegt.|  
|DATE + TIME|Der DATE-Teil der Eingabezeichenfolge wird verwendet.|  
|DATE + TIMEZONE|Nicht zulässig.|  
|TIME + TIMEZONE|Standardwerte werden festgelegt.|  
|DATE + TIME + TIMEZONE|Der DATE-Teil von lokalem DATETIME wird verwendet.|  
  
## <a name="examples"></a>Beispiele  
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
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
|Datentyp|Ausgabe|  
|---------------|------------|  
|**Uhrzeit**|12:35:29. 1234567|  
|**Datum**|2007-05-08|  
|**smalldatetime**|2007-05-08 12:35:00|  
|**datetime**|2007-05-08 12:35:29.123|  
|**datetime2**|2007-05-08 12:35:29. 1234567|  
|**datetimeoffset**|2007-05-08 12:35:29.1234567 +12:15|  
  
## <a name="see-also"></a>Siehe auch
[CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  

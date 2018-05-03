---
title: time (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 6/7/2017
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
- time_TSQL
- time
dev_langs:
- TSQL
helpviewer_keywords:
- time [SQL Server], data types
- time [SQL Server]
- date and time [SQL Server], time
- data types [SQL Server], date and time
- time data type [SQL Server]
ms.assetid: 30a6c681-8190-48e4-94d0-78182290a402
caps.latest.revision: 45
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 81a0b19c21ac231e49dd6c6dad23de7beaaa6b35
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="time-transact-sql"></a>time (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Definiert eine Uhrzeit. Die Uhrzeit basiert auf einem 24-Stunden-Format und beachtet keine Zeitzonen.  
  
  > [!NOTE]  
  > PDW-Benutzer, die den Informatica Connector verwenden, erhalten Informationen zu Informatica. 
  
## <a name="time-description"></a>Beschreibung des time-Datentyps  
  
|Eigenschaft|value|  
|--------------|-----------|  
|Syntax|**time** [ (*fractional second scale*) ]|  
|Verwendung|DECLARE @MyTime **time(7)**<br /><br /> CREATE TABLE Table1 ( Column1 **time(7)** )|  
|*fractional seconds scale*|Definiert die Anzahl der Stellen für den Bruchteil der Sekunden.<br /><br /> Dies kann eine ganze Zahl zwischen 0 und 7 sein. Im Zusammenhang mit Informatica kann dies eine ganze Zahl zwischen 0 und 3 sein.<br /><br /> Der Standardwert für den Bruchteil beträgt 7 (100 ns).|  
|Standardmäßiges Format der Zeichenfolgenliterale<br /><br /> (wird für Downlevelclients verwendet)|hh:mm:ss[.nnnnnnn] für Informatica)<br /><br /> Weitere Informationen finden Sie im nachfolgenden Abschnitt "Abwärtskompatibilität für Downlevelclients".|  
|Bereich|00:00:00.0000000 bis 23:59:59.9999999 (00:00:00.000 bis 23:59:59.999 für Informatica)|  
|Elementbereiche|Bei hh handelt es sich um zwei Ziffern im Bereich von 0 bis 23, die die Stunde darstellen.<br /><br /> Bei mm handelt es sich um zwei Ziffern im Bereich von 0 bis 59, die die Minute darstellen.<br /><br /> Bei ss handelt es sich um zwei Ziffern im Bereich von 0 bis 59, die die Sekunde darstellen.<br /><br /> Bei n\* handelt es sich um bis zu sieben Ziffern im Bereich von 0 bis 9999999, die die Sekundenbruchteile darstellen. Für Informatica umfasst n\* bis zu drei Ziffern im Bereich von 0 bis 999.|  
|Zeichenlänge|Mindestens 8 Positionen (hh:mm:ss) bis maximal 16 Positionen (hh:mm:ss.nnnnnnn). Für Informatica sind es höchstens 12 Positionen (hh:mm:ss.nnn).|  
|Genauigkeit, Dezimalstellen<br /><br /> (Benutzer gibt nur Dezimalstellen an)|Siehe Tabelle unten.|  
|Speichergröße|Standardmäßig 5 Bytes fest, wobei die Standardgenauigkeit in Sekundenbruchteilen 100 ns beträgt. In Informatica sind es standardmäßig 4 Byte (fest), wobei die Standardgenauigkeit in Sekundenbruchteilen 1 ms beträgt.|  
|Genauigkeit|100 ns (1 ms in Informatica)|  
|Standardwert|00:00:00<br /><br /> Dieser Wert wird für den angefügten Datumsteil für eine implizite Konvertierung von **date** in **datetime2** oder **datetimeoffset** verwendet.|  
|Benutzerdefinierte Genauigkeit in Sekundenbruchteilen|ja|  
|Beachtung und Beibehaltung des Zeitzonenoffsets|nein|  
|Beachtung der Sommerzeit|nein|  
  
|Angegebene Dezimalstelle|Ergebnis (Genauigkeit, Dezimalstellen)|Spaltenlänge (in Bytes)|Bruchteil<br /><br /> Sekunden<br /><br /> precision|  
|---------------------|---------------------------------|-----------------------------|------------------------------------------|  
|**Uhrzeit**|(16,7) [(12,3) in Informatica]|5 (4 in Informatica)|7 (3 in Informatica)|  
|**time(0)**|(8,0)|3|0–2|  
|**time(1)**|(10,1)|3|0–2|  
|**time(2)**|(11,2)|3|0–2|  
|**time(3)**|(12,3)|4|3–4|  
|**time(4)**<br /><br /> Wird in Informatica nicht unterstützt.|(13,4)|4|3–4|  
|**time(5)**<br /><br /> Wird in Informatica nicht unterstützt.|(14,5)|5|5–7|  
|**time(6)**<br /><br /> Wird in Informatica nicht unterstützt.|(15,6)|5|5–7|  
|**time(7)**<br /><br /> Wird in Informatica nicht unterstützt.|(16,7)|5|5–7|  
  
## <a name="supported-string-literal-formats-for-time"></a>Unterstützte Formate der Zeichenfolgenliterale für time  
 In der folgenden Tabelle werden die gültigen Formate der Zeichenfolgenliterale für den **time**-Datentyp aufgeführt.  
  
|SQL Server|Description|  
|----------------|-----------------|  
|hh:mm[:ss][:Sekundenbruchteile][AM][PM]<br /><br /> hh:mm[:ss][.Sekundenbruchteile][AM][PM]<br /><br /> hhAM[PM]<br /><br /> hh AM[PM]|Der Stundenwert von 0 stellt die Stunde nach Mitternacht (AM) dar, unabhängig davon, ob AM angegeben ist. Wenn für die Stunde der Wert 0 festgelegt ist, kann PM nicht angegeben werden.<br /><br /> Stundenwerte von 01 bis 11 stellen die Stunden vor 12 Uhr mittags dar, wenn weder AM noch PM angegeben wurde. Die Werte stellen die Stunden vor 12 Uhr mittags dar, wenn AM angegeben wurde. Sie stellen die Stunden nach 12 Uhr mittags dar, wenn PM angegeben wurde.<br /><br /> Der Stundenwert 12 stellt die Stunde, beginnend mit 12 Uhr mittags, dar, wenn weder AM noch PM angegeben wurde. Wurde AM angegeben, stellt der Wert die Stunde dar, die um Mitternacht beginnt. Wurde PM angegeben, stellt der Wert die Stunde dar, die um 12 Uhr mittags beginnt. Beispiel: 12:01 ist eine Minute nach 12 Uhr mittags, genauso wie 12:01 PM, während 12:01 AM eine Minute nach Mitternacht ist. Die Angabe 12:01 AM ist identisch mit der Angabe 00:01 oder 00:01 AM.<br /><br /> Stundenwerte von 13 bis 23 stellen die Stunden nach 12 Uhr mittags dar, wenn weder AM noch PM angegeben wurde. Die Werte stellen darüber hinaus die Stunden nach 12 Uhr mittags dar, wenn PM angegeben wurde. AM kann nicht angegeben werden, wenn der Stundenwert zwischen 13 und 23 liegt.<br /><br /> Ein Stundenwert von 24 ist ungültig. Um Mitternacht darzustellen, verwenden Sie 12:00 AM oder 00:00.<br /><br /> Vor Millisekundenangaben kann entweder ein Doppelpunkt (:) oder ein Punkt (.) stehen. Wenn ein Doppelpunkt verwendet wird, bedeutet das, dass die folgende Zahl Tausendstelsekunden darstellt. Wenn ein Punkt verwendet wird, bedeutet das, dass eine einzelne folgende Ziffer Zehntelsekunden, zwei Folgeziffern Hundertstelsekunden und drei Folgeziffern Tausendstelsekunden darstellen. Beispielsweise zeigt 12:30:20:1 zwanzig Sekunden und eine Tausendstelsekunde nach 12:30 an, während 12:30:20.1 zwanzig Sekunden und eine Zehntelsekunde nach 12:30 anzeigt.|  
  
|ISO 8601|Hinweise|  
|--------------|-----------|  
|hh:mm:ss<br /><br /> hh:mm[:ss][.Millisekunden]|Bei hh handelt es sich um zwei Ziffern im Bereich von 0 bis 14, die die Anzahl der Stunden im Zeitzonenoffset darstellen.<br /><br /> Bei mm handelt es sich um zwei Ziffern im Bereich von 0 bis 59, die die Anzahl der zusätzlichen Minuten im Zeitzonenoffset darstellen.|  
  
|ODBC|Hinweise|  
|----------|-----------|  
|{t 'hh:mm:ss[.Millisekunden]'}|ODBC-API-spezifisch|  
  
## <a name="compliance-with-ansi-and-iso-8601-standards"></a>Kompatibilität mit ANSI- und ISO 8601-Standards  
 Die Verwendung des Stundenwerts 24 zur Darstellung von Mitternacht sowie von Schaltsekunden größer als 59, gemäß ISO 8601 (5.3.2 und 5.3), sind nicht abwärtskompatibel und stimmen möglicherweise nicht mit den bestehenden Datums- und Uhrzeittypen überein.  
  
 Das standardmäßige Format der Zeichenfolgenliterale (wird für Downlevelclients verwendet) entspricht dem SQL-Standard, der als hh:mm:ss[.nnnnnnn] definiert ist. Dieses Format ähnelt der ISO 8601-Definition für TIME unter Ausschluss der Sekundenbruchteile.  
  
##  <a name="BackwardCompatibilityforDownlevelClients"></a> Abwärtskompatibilität für Clients aus Vorgängerversionen  
 Einige Downlevelclients unterstützen nicht die Datentypen **time**, **date**, **datetime2** und **datetimeoffset**. In der folgenden Tabelle wird die Typzuordnung zwischen einer Instanz höherer Ebene in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und Downlevelclients gezeigt.  
  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datentyp|Standardmäßiges Format des an Downlevelclients übergebenen Zeichenfolgenliterals|ODBC früherer Versionen|OLEDB früherer Versionen|JDBC früherer Versionen|SQLCLIENT früherer Versionen|  
|-----------------------------------------|----------------------------------------------------------------|----------------------|-----------------------|----------------------|---------------------------|  
|**Uhrzeit**|hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR oder SQL_VARCHAR|DBTYPE_WSTR oder DBTYPE_STR|Java.sql.String|Zeichenfolge oder SqString|  
|**Datum**|YYYY-MM-DD|SQL_WVARCHAR oder SQL_VARCHAR|DBTYPE_WSTR oder DBTYPE_STR|Java.sql.String|Zeichenfolge oder SqString|  
|**datetime2**|YYYY-MM-DD hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR oder SQL_VARCHAR|DBTYPE_WSTR oder DBTYPE_STR|Java.sql.String|Zeichenfolge oder SqString|  
|**datetimeoffset**|YYYY-MM-DD hh:mm:ss[.nnnnnnn] [+&#124;-]hh:mm|SQL_WVARCHAR oder SQL_VARCHAR|DBTYPE_WSTR oder DBTYPE_STR|Java.sql.String|Zeichenfolge oder SqString|  
  
## <a name="converting-date-and-time-data"></a>Konvertieren von Datums- und Zeitdaten  
 Beim Konvertieren in date- und time-Datentypen lehnt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] alle Werte ab, die nicht als Datum oder Uhrzeit erkannt werden. Informationen zur Verwendung der CAST-Funktion und der CONVERT-Funktion mit Datums- und Uhrzeitdaten finden Sie unter [CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md).  
  
### <a name="converting-timen-data-type-to-other-date-and-time-types"></a>Konvertieren des time(n)-Datentyps in andere Datums- und Uhrzeittypen  
 Der folgende Abschnitt veranschaulicht die Abläufe bei der Konvertierung des **time**-Datentyps in andere Datums- und Uhrzeittypen.  
  
 Beim Konvertieren in **time(n)** werden die Stunde, die Minute und die Sekunden kopiert. Wenn die Genauigkeit des Quellwerts die Genauigkeit des Zielwerts übersteigt, werden die Sekundenbruchteile entsprechend der Genauigkeit des Zielwerts aufgerundet. Das folgende Beispiel zeigt die Ergebnisse der Konvertierung eines `time(4)`-Werts in einen `time(3)`-Wert.  
  
```  
DECLARE @timeFrom time(4) = '12:34:54.1237';  
DECLARE @timeTo time(3) = @timeFrom;  
  
SELECT @timeTo AS 'time(3)', @timeFrom AS 'time(4)';  
  
--Results  
--time(3)      time(4)  
-------------- -------------  
--12:34:54.124 12:34:54.1237  
--  
--(1 row(s) affected)  
```  
  
 Wenn eine Konvertierung in  
                    **date** vorgenommen wird, schlägt die Konvertierung fehl, und die Fehlermeldung 206 "Operand type clash: date is incompatible with time." (Operandentypkollision: date ist inkompatibel mit time.) wird ausgegeben.  
  
 Wenn eine Konvertierung in **datetime** vorgenommen wird, werden die Werte für Stunden, Minuten und Sekunden kopiert, und die Datumskomponente wird auf 1900-01-01 festgelegt. Wenn die Genauigkeit des **time(n)**-Werts größer ist als drei Sekundenbruchteile, wird das **datetime**-Ergebnis gekürzt. Der folgende Code zeigt die Ergebnisse der Konvertierung eines `time(4)`-Werts in einen `datetime`-Wert.  
  
```  
DECLARE @time time(4) = '12:15:04.1237';  
DECLARE @datetime datetime= @time;  
SELECT @time AS '@time', @datetime AS '@datetime';  
  
--Result  
--@time         @datetime  
--------------- -----------------------  
--12:15:04.1237 1900-01-01 12:15:04.123  
--  
--(1 row(s) affected)  
  
```  
  
 Wenn eine Konvertierung in **smalldatetime** vorgenommen wird, wird das Datum auf 1900-01-01 festgelegt, und die Werte für Stunden und Minuten werden aufgerundet. Die Sekunden und die Sekundenbruchteile werden auf 0 festgelegt. Der folgende Code zeigt die Ergebnisse der Konvertierung eines `time(4)`-Werts in einen `smalldatetime`-Wert.  
  
```  
-- Shows rounding up of the minute value.  
DECLARE @time time(4) = '12:15:59.9999';   
DECLARE @smalldatetime smalldatetime= @time;    
SELECT @time AS '@time', @smalldatetime AS '@smalldatetime';   
  
--Result  
@time            @smalldatetime  
---------------- -----------------------  
12:15:59.9999    1900-01-01 12:16:00--  
--(1 row(s) affected)  
  
-- Shows rounding up of the hour value.  
DECLARE @time time(4) = '12:59:59.9999';   
DECLARE @smalldatetime smalldatetime= @time;    
  
SELECT @time AS '@time', @smalldatetime AS '@smalldatetime';  
@time            @smalldatetime  
---------------- -----------------------  
12:59:59.9999    1900-01-01 13:00:00  
  
(1 row(s) affected)  
  
```  
  
 Wenn eine Konvertierung in **datetimeoffset(n)** vorgenommen wird, wird das Datum auf 1900-01-01 festgelegt und die Uhrzeit kopiert. Der Zeitzonenoffset wird auf +00:00 festgelegt. Wenn die Genauigkeit in Sekundenbruchteilen des **time(n)**-Werts größer ist als die Genauigkeit des **datetimeoffset(n)**-Werts, wird der Wert entsprechend aufgerundet. Das folgende Beispiel zeigt die Ergebnisse der Konvertierung eines `time(4)`-Werts in einen `datetimeoffset(3)`-Typ.  
  
```  
DECLARE @time time(4) = '12:15:04.1237';  
DECLARE @datetimeoffset datetimeoffset(3) = @time;  
  
SELECT @time AS '@time', @datetimeoffset AS '@datetimeoffset';  
  
--Result  
--@time         @datetimeoffset  
--------------- ------------------------------  
--12:15:04.1237 1900-01-01 12:15:04.124 +00:00  
--  
--(1 row(s) affected)  
  
```  
  
 Wenn eine Konvertierung in **datetime2(n)** vorgenommen wird, wird das Datum auf 1900-01-01 festgelegt, die Zeitkomponente wird kopiert, und der Zeitzonenoffset wird auf 00:00 festgelegt. Wenn die Genauigkeit in Sekundenbruchteilen des **datetime2(n)**-Werts größer ist als die Genauigkeit des **time(n)**-Werts, wird der Wert entsprechend aufgerundet.  Das folgende Beispiel zeigt die Ergebnisse der Konvertierung eines `time(4)`-Werts in einen `datetime2(2)`-Wert.  
  
```  
DECLARE @time time(4) = '12:15:04.1237';  
DECLARE @datetime2 datetime2(3) = @time;  
  
SELECT @datetime2 AS '@datetime2', @time AS '@time';  
  
--Result  
--@datetime2              @time  
------------------------- -------------  
--1900-01-01 12:15:04.124 12:15:04.1237  
--  
--(1 row(s) affected)  
```  
  
### <a name="converting-string-literals-to-timen"></a>Konvertieren von Zeichenfolgenliteralen in time(n)-Werte  
 Konvertierungen von Zeichenfolgenliteralen in Datums- und Zeitwerte sind erlaubt, wenn alle Teile der Zeichenfolge in gültigen Formaten vorliegen. Andernfalls wird ein Laufzeitfehler ausgelöst. Wird bei impliziten oder expliziten Konvertierungen von Datums- und Zeitwerten in Zeichenfolgenliterale kein Stil angegeben, wird das Standardformat der aktuellen Sitzung verwendet. In der folgenden Tabelle werden die Regeln zum Konvertieren eines Zeichenfolgenliterals in den **time**-Datentyp dargestellt.  
  
|Eingabezeichenfolgenliteral|Konvertierungsregel|  
|--------------------------|---------------------|  
|ODBC DATE|Dem **datetime**-Datentyp werden ODBC-Zeichenfolgenliterale zugeordnet. Jede Zuweisungsoperation von ODBC DATETIME-Literalen zu **time**-Typen bewirkt eine in den Konvertierungsregeln definierte implizite Konvertierung zwischen **datetime** und diesen Typen.|  
|ODBC TIME|Weitere Informationen enthält die ODBC DATE-Regel weiter oben.|  
|ODBC DATETIME|Weitere Informationen enthält die ODBC DATE-Regel weiter oben.|  
|Nur DATE|Standardwerte werden festgelegt.|  
|Nur TIME|Trivial|  
|Nur TIMEZONE|Standardwerte werden festgelegt.|  
|DATE + TIME|Die TIME-Komponente der Eingabezeichenfolge wird verwendet.|  
|DATE + TIMEZONE|Nicht zulässig.|  
|TIME + TIMEZONE|Die TIME-Komponente der Eingabezeichenfolge wird verwendet.|  
|DATE + TIME + TIMEZONE|Die TIME-Komponente des lokalen DATETIME wird verwendet.|  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-comparing-date-and-time-data-types"></a>A. Vergleichen des date-Datentyps mit dem time-Datentyp  
 Im folgenden Beispiel werden die Ergebnisse der Umwandlung von einer Zeichenfolge in alle **date**- und **time**-Datentypen verglichen.  
  
```  
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
|---------------|------------|  
|**Uhrzeit**|12:35:29. 1234567|  
|**Datum**|2007-05-08|  
|**smalldatetime**|2007-05-08 12:35:00|  
|**datetime**|2007-05-08 12:35:29.123|  
|**datetime2**|2007-05-08 12:35:29. 1234567|  
|**datetimeoffset**|2007-05-08 12:35:29.1234567 +12:15|  
  
###  <a name="ExampleB"></a> B. Einfügen von gültigen time-Zeichenfolgenliteralen in eine time(7)-Spalte  
 In der folgenden Tabelle werden neben den unterschiedlichen Zeichenfolgenliteralen, die in eine Spalte des Datentyps **time(7)** eingefügt werden können, auch die Werte aufgelistet, die anschließend in der entsprechenden Spalte gespeichert werden.  
  
|Formattyp des Zeichenfolgenliterals|Eingefügtes Zeichenfolgenliteral|Gespeicherter time(7)-Wert|Description|  
|--------------------------------|-----------------------------|------------------------------------|-----------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|'01:01:01:123AM'|01:01:01.1230000|Wenn vor der Genauigkeit der Sekundenbruchteile ein Doppelpunkt (:) steht, können die Dezimalstellen mit maximal 3 Positionen angegeben werden. Andernfalls wird ein Fehler ausgegeben.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|'01:01:01.1234567 AM'|01:01:01.1234567|Wenn AM oder PM angegeben ist, wird die Uhrzeit im 24-Stunden-Format ohne das Literal AM oder PM gespeichert.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|'01:01:01.1234567 PM'|13:01:01.1234567|Wenn AM oder PM angegeben ist, wird die Uhrzeit im 24-Stunden-Format ohne das Literal AM oder PM gespeichert.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|'01:01:01.1234567PM'|13:01:01.1234567|Ein Leerzeichen vor AM oder PM ist optional.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|'01AM'|01:00:00.0000000|Wenn nur die Stunde angegeben wird, sind alle anderen Werte 0.|  
|SQL Server|'01 AM'|01:00:00.0000000|Ein Leerzeichen vor AM oder PM ist optional.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|'01:01:01'|01:01:01.0000000|Wenn keine Genauigkeit der Sekundenbruchteile angegeben wird, wird jede Position, die durch den Datentyp definiert ist, auf 0 festgelegt.|  
|ISO 8601|'01:01:01.1234567'|01:01:01.1234567|Zur Erfüllung des ISO 8601-Standards verwenden Sie das 24-Stunden-Format ohne Angabe von AM oder PM.|  
|ISO 8601|'01:01:01.1234567 +01:01'|01:01:01.1234567|Der optionale Zeitzonenunterschied (TZD) ist bei der Eingabe zugelassen, wird aber nicht gespeichert.|  
  
### <a name="c-inserting-time-string-literal-into-columns-of-each-date-and-time-date-type"></a>C. Einfügen von time-Zeichenfolgenliteralen in die Spalten der einzelnen date-Datentypen und time-Datentypen  
 Die folgende Tabelle zeigt in der ersten Spalte ein time-Zeichenfolgenliteral, das in eine Datenbanktabellen-Spalte des Datentyps date oder time (wird in der zweiten Spalte angezeigt) eingefügt werden soll. Die dritte Spalte zeigt den Wert, der in der Datenbanktabellen-Spalte gespeichert wird.  
  
|Eingefügtes Zeichenfolgenliteral|Spaltendatentyp|Wert, der in der Spalte gespeichert wird|Description|  
|-----------------------------|----------------------|------------------------------------|-----------------|  
|'12:12:12.1234567'|**time(7)**|12:12:12.1234567|Wenn die Genauigkeit der Sekundenbruchteile den für die Spalte angegebenen Wert überschreitet, wird die Zeichenfolge abgeschnitten, ohne einen Fehler zu verursachen.|  
|'2007-05-07'|**Datum**|NULL|Jeder time-Wert führt zu einer fehlerhaften INSERT-Anweisung.|  
|'12:12:12'|**smalldatetime**|1900-01-01 12:12:00|Jeder Wert für die Genauigkeit der Sekundenbruchteile führt zu einer fehlerhaften INSERT-Anweisung.|  
|'12:12:12.123'|**datetime**|1900-01-01 12:12:12.123|Jede Sekundengenauigkeit, die mehr als 3 Stellen umfasst, führt zu einer fehlerhaften INSERT-Anweisung.|  
|'12:12:12.1234567'|**datetime2(7)**|1900-01-01 12:12:12.1234567|Wenn die Genauigkeit der Sekundenbruchteile den für die Spalte angegebenen Wert überschreitet, wird die Zeichenfolge abgeschnitten, ohne einen Fehler zu verursachen.|  
|'12:12:12.1234567'|**datetimeoffset(7)**|1900-01-01 12:12:12.1234567 +00:00|Wenn die Genauigkeit der Sekundenbruchteile den für die Spalte angegebenen Wert überschreitet, wird die Zeichenfolge abgeschnitten, ohne einen Fehler zu verursachen.|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  

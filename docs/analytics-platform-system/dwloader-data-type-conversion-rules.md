---
title: Dwloader Datentyp Konvertierungsregeln - Parallel Data Warehouse | Microsoft Docs
description: Dieses Thema beschreibt die Eingabedaten-Formate und impliziten datentypkonvertierungen, Dwloader, Command-Line-Ladeprogramm unterstützt, wenn Daten in Parallel Data Warehouse (PDW) geladen."
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: ecfc29c92bc99827ee943ff665524ff49e82a8df
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/19/2018
---
# <a name="data-type-conversion-rules-for-dwloader---parallel-data-warehouse"></a>Konvertierungsregeln für Dwloader – Parallel Data Warehouse-Datentyp
In diesem Thema wird beschrieben, die Eingabedaten-Formate und impliziten datentypkonvertierungen, [Dwloader Command-Line-Ladeprogramm](dwloader.md) beim Laden von Daten in PDW unterstützt. Die implizite datenkonvertierungen auftreten, wenn die Eingabedaten nicht den Datentyp in der SQL Server PDW-Zieltabelle übereinstimmt. Verwenden Sie diese Informationen beim Entwerfen Ihrer Ladevorgang, um sicherzustellen, dass Ihre Daten in SQL Server PDW erfolgreich geladen wird.  
   
  
## <a name="InsertBinaryTypes"></a>Literale in Binärtypen eingefügt.  
In der folgenden Tabelle definiert, der akzeptierten Literaltypen, Format und Konvertierungsregeln für einen literalen Wert in einer SQL Server PDW-Spalte vom Typ laden **binäre** (*n*) oder **Varbinary** (*n*).  
  
|Input-Datentyp|Beispiele für die Eingabedaten|Die Konvertierung in Binary oder Varbinary-Datentyp|  
|-------------------|-----------------------|-----------------------------------------------|  
|Binäres literal|[0 X] *Hexidecimal_string*<br /><br />Beispiel: 12Ef oder 0x12Ef|Das Präfix 0 X ist optional.<br /><br />Die Länge der Quelle darf die angegebene Anzahl von Bytes für den Datentyp nicht überschreiten.<br /><br />Wenn die Länge der Quelle geringer als ist die **binäre** -Datentyp, werden die Daten nach rechts mit Nullen aufgefüllt, um die Größe der Daten zu erreichen aufgefüllt.|  
  
## <a name="InsertDateTimeTypes"></a>Einfügen von Literalen in Datums- und Uhrzeittypen  
Datum und Uhrzeit-Literale werden mithilfe von Zeichenfolgenliteralen in bestimmten Formaten, eingeschlossen in einfache Anführungszeichen dargestellt. In den folgenden Tabellen definieren, die zulässige Literaltypen, Format und Konvertierungsregeln zum Laden ein Datum oder Uhrzeit-literal in einer Spalte vom Typ **"DateTime"**, **Smalldatetime**, **Datum**, **Zeit**, **"DateTimeOffset"**, oder **datetime2**. Die Tabellen definieren, das Standardformat für den angegebenen Datentyp. Andere Formate, die angegeben werden können, sind im Abschnitt definiert [Datetime-Formate](#DateFormats). Datums- und Zeitliterale darf keine führende oder nachgestellte Leerzeichen enthalten. **Datum**, **Smalldatetime**, null-Werte können nicht geladen werden, im Modus mit fester Breite.  
  
### <a name="datetime-data-type"></a>datetime-Datentyp  
In der folgenden Tabelle definiert, das Standardformat und die Regeln zum Laden von literalen Werten in einer Spalte vom Typ **"DateTime"**. Der Standardwert ist eine leere Zeichenfolge (") konvertiert" 12:00:00.000 1900-01-01 ". Zeichenfolgen, die nur Leerstellen enthalten ("") ein Fehler generiert.  
  
|Input-Datentyp|Beispiele für die Eingabedaten|Die Konvertierung in Datetime-Datentyp|  
|-------------------|-----------------------|------------------------------------|  
|Zeichenfolgenliteral im **"DateTime"** Format|"Yyyy-MM-Dd hh: mm: [ss.fff]"<br /><br />Beispiel: "2007-05-08-12:35:29.123"|Fehlende Dezimalstellen werden auf 0 festgelegt, wenn der Wert eingefügt wird. Angenommen, das Literal "2007-05-08 12:35 ' wird als eingefügt" 2007-05-08-12:35:00.000 ".|  
|Zeichenfolgenliteral im **Smalldatetime** Format|"Yyyy-MM-Dd hh: mm"<br /><br />Beispiel: "2007-05-08 12:35"|Sekunden und die restlichen Dezimalstellen werden auf 0 festgelegt, wenn der Wert eingefügt wird.|  
|Zeichenfolgenliteral im **Datum** Format|"JJJJ-MM-TT"<br /><br />Beispiel: "2007-05-08"|Time-Werten (Stunde, Minuten, Sekunden und Sekundenbruchteile) werden auf 12:00:00.000 festgelegt, wenn der Wert eingefügt wird.|  
|Zeichenfolgenliteral im **datetime2** Format|"JJJJ-MM-tt hh:mm:ss.fffffff"<br /><br />Beispiel: "2007-05-08-12:35:29.1234567"|Die Quelldaten darf drei Dezimalstellen nicht überschreiten. Z. B. das Literal "2007-05-08-12:35:29.123" eingefügt werden, aber der Wert "2007-05-8 12:35:29.1234567" wird ein Fehler generiert.|  
  
### <a name="smalldatetime-data-type"></a>smalldatetime-Datentyp  
In der folgenden Tabelle definiert, das Standardformat und die Regeln zum Laden von literalen Werten in einer Spalte vom Typ **Smalldatetime**. Der Standardwert ist eine leere Zeichenfolge (") konvertiert" 1900-01-01 – 12:00 ". Zeichenfolgen, die nur Leerstellen enthalten ("") ein Fehler generiert.  
  
|Input-Datentyp|Beispiele für die Eingabedaten|Die Konvertierung in den Smalldatetime-Datentyp|  
|-------------------|-----------------------|-----------------------------------------|  
|Zeichenfolgenliteral im **Smalldatetime** Format|"Yyyy-MM-Dd hh: mm" oder "Yyyy-MM-Dd hh: mm:"<br /><br />Beispiel: "2007-05-08 12:00 ' oder ' 2007-05-08 12:00:15 Uhr"|Die Quelldaten müssen Werte für Jahr, Monat, Datum, Stunde und Minute aufweisen. Sekunden sind optional und, falls vorhanden, müssen auf den Wert 00 festgelegt werden. Jeder andere Wert wird einen Fehler generiert.<br /><br />Sekunden ist optional. Beim Laden in einen Smalldatetime-Spalte wird Dwloader Sekunden und Sekundenbruchteile gerundet. Beispielsweise wird als 01-05-20:11 1999-01-05-20:10:35.123 geladen werden.|  
|Zeichenfolgenliteral im **Datum** Format|"JJJJ-MM-TT"<br /><br />Beispiel: "2007-05-08"|Time-Werten (Stunde, Minuten, Sekunden und Sekundenbruchteile) werden auf 0 festgelegt, wenn der Wert eingefügt wird.|  
  
### <a name="date-data-type"></a>date-Datumstyp  
In der folgenden Tabelle definiert, das Standardformat und die Regeln zum Laden von literalen Werten in einer Spalte vom Typ **Datum**. Der Standardwert ist eine leere Zeichenfolge (") konvertiert" 1900-01-01 ". Zeichenfolgen, die nur Leerstellen enthalten ("") ein Fehler generiert.  
  
|Input-Datentyp|Beispiele für die Eingabedaten|Die Konvertierung in Date-Datentyp|  
|-------------------|-----------------------|--------------------------------|  
|Zeichenfolgenliteral im **Datum** Format|"JJJJ-MM-TT"<br /><br />Beispiel: "2007-05-08"||  
  
### <a name="time-data-type"></a>Time-Datentyp  
In der folgenden Tabelle definiert, das Standardformat und die Regeln zum Laden von literalen Werten in einer Spalte vom Typ **Zeit**. Eine leere Zeichenfolge (") wird auf den Standardwert"00:00:00.0000"konvertiert. Zeichenfolgen, die nur Leerstellen enthalten ("") ein Fehler generiert.  
  
|Input-Datentyp|Beispiele für die Eingabedaten|Die Konvertierung in Time-Datentyp|  
|-------------------|-----------------------|--------------------------------|  
|Zeichenfolgenliteral im **Zeit** Format|"hh:mm:ss.fffffff"<br /><br />Beispiel: "12:35:29.1234567"|Wenn die Datenquelle eine Genauigkeit kleinere oder gleich (Anzahl der Dezimalstellen) als die Genauigkeit des enthält die **Zeit** -Datentyp, werden die Daten auf die rechte Seite mit Nullen aufgefüllt. Beispielsweise wird ein Literalwert "12:35:29.123" als "12:35:29.1230000" eingefügt.|  
  
### <a name="datetimeoffset-data-type"></a>DateTimeOffset-Datentyp  
In der folgenden Tabelle definiert, das Standardformat und die Regeln zum Laden von literalen Werten in einer Spalte vom Typ **"DateTimeOffset"** (*n*). Das Standardformat ist ' Yyyy-MM-tt hh:mm:ss.fffffff {+ |-} hh: mm ". Der Standardwert ist eine leere Zeichenfolge (") konvertiert" 1900-01-01 12:00:00.0000000 + 00:00 ". Zeichenfolgen, die nur Leerstellen enthalten ("") ein Fehler generiert. Die Anzahl der Dezimalstellen, hängt von der Definition der Spalte ab. Angenommen, eine Spalte, die als definiert **"DateTimeOffset"** (2) hat zwei Dezimalstellen.  
  
|Input-Datentyp|Beispiele für die Eingabedaten|Die Konvertierung in das Datetimeoffset-Datentyp|  
|-------------------|-----------------------|------------------------------------------|  
|Zeichenfolgenliteral im **"DateTime"** Format|"Yyyy-MM-Dd hh: mm: [ss.fff]"<br /><br />Beispiel: "2007-05-08-12:35:29.123"|Fehlende Dezimalstellen und Offset-Werte werden auf 0 festgelegt, wenn der Wert eingefügt wird. Angenommen, das Literal "2007-05-08-12:35:29.123" als eingefügt "2007-05-08-12:35:29.1230000 + 00:00".|  
|Zeichenfolgenliteral im **Smalldatetime** Format|"Yyyy-MM-Dd hh: mm"<br /><br />Beispiel: "2007-05-08 12:35"|Sekunden, die restlichen Dezimalstellen und die Offset-Werte werden auf 0 festgelegt, wenn der Wert eingefügt wird.|  
|Zeichenfolgenliteral im **Datum** Format|"JJJJ-MM-TT"<br /><br />Beispiel: "2007-05-08"|Time-Werten (Stunde, Minuten, Sekunden und Sekundenbruchteile) werden auf 0 festgelegt, wenn der Wert eingefügt wird. Z. B., das literal "2007-05-08' wird als eingefügt" 2007-05-08-00:00:00.0000000 + 00:00 ".|  
|Zeichenfolgenliteral im **datetime2** Format|"JJJJ-MM-tt hh:mm:ss.fffffff"<br /><br />Beispiel: "2007-05-08-12:35:29.1234567"|Die Quelldaten darf die angegebene Anzahl von Sekundenbruchteilen in der Spalte "DateTimeOffset" nicht überschreiten. Wenn die Datenquelle eine Zahl kleinere oder gleich der Bruchteile von Sekunden enthält, wird auf die rechte Seite mit Nullen aufgefüllt. Angenommen, der Datentyp "DateTimeOffset" (5), der literale Wert ist "2007-05-08-12:35:29.123 + 12:15 ' wird als eingefügt" 12:35:29.12300 + 12:15 '.|  
|Zeichenfolgenliteral im **"DateTimeOffset"** Format|"JJJJ-MM-tt hh:mm:ss.fffffff {+&#124;-} hh: mm"<br /><br />Beispiel: "2007-05-08-12:35:29.1234567 + 12:15 '|Die Quelldaten darf die angegebene Anzahl von Sekundenbruchteilen in der Spalte "DateTimeOffset" nicht überschreiten. Wenn die Datenquelle eine Zahl kleinere oder gleich der Bruchteile von Sekunden enthält, wird auf die rechte Seite mit Nullen aufgefüllt. Angenommen, der Datentyp "DateTimeOffset" (5), der literale Wert ist "2007-05-08-12:35:29.123 + 12:15 ' wird als eingefügt" 12:35:29.12300 + 12:15 '.|  
  
### <a name="datetime2-data-type"></a>datetime2-Datentyp  
In der folgenden Tabelle definiert, das Standardformat und die Regeln zum Laden von literalen Werten in einer Spalte vom Typ **datetime2** (*n*). Das Standardformat ist "Yyyy-MM-Dd hh:mm:ss.fffffff". Der Standardwert ist eine leere Zeichenfolge (") konvertiert" 1900-01-01 – 12:00:00 ". Zeichenfolgen, die nur Leerstellen enthalten ("") ein Fehler generiert. Die Anzahl der Dezimalstellen, hängt von der Definition der Spalte ab. Angenommen, eine Spalte, die als definiert **datetime2** (2) hat zwei Dezimalstellen.  
  
|Input-Datentyp|Beispiele für die Eingabedaten|Konvertierung in datetime2-Datentyp|  
|-------------------|-----------------------|-------------------------------------|  
|Zeichenfolgenliteral im **"DateTime"** Format|"Yyyy-MM-Dd hh: mm: [ss.fff]"<br /><br />Beispiel: "2007-05-08-12:35:29.123"|Sekundenbruchteile sind optional und werden auf 0 festgelegt, wenn der Wert eingefügt wird.|  
|Zeichenfolgenliteral im **Smalldatetime** Format|"Yyyy-MM-Dd hh: mm"<br /><br />Beispiel: "2007-05-08-12"|Optionale Sekunden und die restlichen Dezimalstellen werden auf 0 festgelegt, wenn der Wert eingefügt wird.|  
|Zeichenfolgenliteral im **Datum** Format|"JJJJ-MM-TT"<br /><br />Beispiel: "2007-05-08"|Time-Werten (Stunde, Minuten, Sekunden und Sekundenbruchteile) werden auf 0 festgelegt, wenn der Wert eingefügt wird. Z. B., das literal "2007-05-08' wird als eingefügt" 2007-05-08-12:00:00.0000000 ".|  
|Zeichenfolgenliteral im **datetime2** Format|"JJJJ-MM-tt Hh:mm:ss:fffffff"<br /><br />Beispiel: "2007-05-08-12:35:29.1234567"|Wenn die Datenquelle und der Zeitpunkt der Komponenten enthält, die kleiner oder gleich dem Wert im angegebenen **datetime2**(*n*), die Daten eingefügt, da andernfalls ein Fehler ausgelöst wird.|  
  
### <a name="DateFormats"></a>DateTime-Formate  
Dwloader unterstützt die folgenden Formate für die Eingabedaten, die sie in SQL Server PDW geladen wird. Weitere Details sind nach der Tabelle aufgeführt.  
  
|datetime|smalldatetime|Datum|datetime2|datetimeoffset|  
|------------|-----------------|--------|-------------|------------------|  
|[M[M]]M-[T]T-[JJ]JJ HH:mm:ss[.fff]|[M[M]]M-[T]T-[JJ]JJ HH:mm[:00]|[M[M]]M-[T]T-[JJ]JJ|[M[M]]M-[T]T-[JJ]JJ HH:mm:ss[.fffffff]|[M[M]]M-[T]T-[JJ]JJ HH:mm:ss[.fffffff] zzz|  
|[M[M]]M-[T]T-[JJ]JJ hh:mm:ss[.fff][tt]|[M[M]]M-[T]T-[JJ]JJ hh:mm[:00][tt]||[M[M]]M-[T]T-[JJ]JJ hh:mm:ss[.fffffff][tt]|[M[M]]M-[T]T-[JJ]JJ hh:mm:ss[.fffffff][tt] zzz|  
|[M[M]]M-[JJ]JJ-[T]T HH:mm:ss[.fff]|[M[M]]M-[JJ]JJ-[T]T HH:mm[:00]|[M[M]]M-[JJ]JJ-[T]T|[M[M]]M-[JJ]JJ-[T]T HH:mm:ss[.fffffff]|[M[M]]M-[JJ]JJ-[T]T HH:mm:ss[.fffffff] zzz|  
|[M[M]]M-[JJ]JJ-[T]T hh:mm:ss[.fff][tt]|[M[M]]M-[JJ]JJ-[T]T hh:mm[:00][tt]||[M[M]]M-[JJ]JJ-[T]T hh:mm:ss[.fffffff][tt]|[M[M]]M-[JJ]JJ-[T]T hh:mm:ss[.fffffff][tt] zzz|  
|[JJ]JJ-[M[M]]M-[T]T HH:mm:ss[.fff]|[JJ]JJ-[M[M]]M-[T]T HH:mm[:00]|[JJ]JJ-[M[M]]M-[T]T|[JJ]JJ-[M[M]]M-[T]T HH:mm:ss[.fffffff]|[JJ]JJ-[M[M]]M-[T]T HH:mm:ss[.fffffff] zzz|  
|[JJ]JJ-[M[M]]M-[T]T hh:mm:ss[.fff][tt]|[JJ]JJ-[M[M]]M-[T]T hh:mm[:00][tt]||[JJ]JJ-[M[M]]M-[T]T hh:mm:ss[.fffffff][tt]|[JJ]JJ-[M[M]]M-[T]T hh:mm:ss[.fffffff][tt] zzz|  
|[JJ]JJ-[T]T-[M[M]]M HH:mm:ss[.fff]|[JJ]JJ-[T]T-[M[M]]M HH:mm[:00]|[JJ]JJ-[T]T-[M[M]]M|[JJ]JJ-[T]T-[M[M]]M HH:mm:ss[.fffffff]|[JJ]JJ-[T]T-[M[M]]M HH:mm:ss[.fffffff] zzz|  
|[JJ]JJ-[T]T-[M[M]]M hh:mm:ss[.fff][tt]|[JJ]JJ-[T]T-[M[M]]M hh:mm[:00][tt]||[JJ]JJ-[T]T-[M[M]]M hh:mm:ss[.fffffff][tt]|[JJ]JJ-[T]T-[M[M]]M hh:mm:ss[.fffffff][tt] zzz|  
|[T]T-[M[M]]M-[JJ]JJ HH:mm:ss[.fff]|[T]T-[M[M]]M-[JJ]JJ HH:mm[:00]|[T]T-[M[M]]M-[JJ]JJ|[T]T-[M[M]]M-[JJ]JJ :mm:ss[.fffffff]|[T]T-[M[M]]M-[JJ]JJ HH:mm:ss[.fffffff] zzz|  
|[T]T-[M[M]]M-[JJ]JJ hh:mm:ss[.fff][tt]|[T]T-[M[M]]M-[JJ]JJ hh:mm[:00][tt]||[T]T-[M[M]]M-[JJ]JJ hh:mm:ss[.fffffff][tt]|[T]T-[M[M]]M-[JJ]JJ hh:mm:ss[.fffffff][tt] zzz|  
|[T]T-[JJ]JJ-[M[M]]M HH:mm:ss[.fff]|[T]T-[JJ]JJ-[M[M]]M HH:mm[:00]|[T]T-[JJ]JJ-[M[M]]M|[T]T-[JJ]JJ-[M[M]]M HH:mm:ss[.fffffff]|[T]T-[JJ]JJ-[M[M]]M HH:mm:ss[.fffffff] zzz|  
|[T]T-[JJ]JJ-[M[M]]M hh:mm:ss[.fff][tt]|[T]T-[JJ]JJ-[M[M]]M hh:mm[:00][tt]||[T]T-[JJ]JJ-[M[M]]M hh:mm:ss[.fffffff][tt]|[T]T-[JJ]JJ-[M[M]]M hh:mm:ss[.fffffff][tt] zzz|  
  
Details:  
  
-   Um Werte für Monat, Tag und Jahr zu trennen, können Sie '–', '/' oder '. '. Der Einfachheit halber wird in die Tabelle nur das Trennzeichen „–“ verwendet.  
  
-   Zum Angeben der Monat als Text, verwenden drei oder mehr Zeichen. Monate mit 1 oder 2 Zeichen werden als Zahl interpretiert.  
  
-   Verwenden Sie zum Trennen der Time-Werten die ': ' Symbol.  
  
-   Buchstaben in eckigen Klammern sind optional.  
  
-   Die Buchstaben „tt“ kennzeichnen [AM|PM|am|pm]. AM ist die Standardeinstellung. Wenn „tt“ angegeben ist, muss der Wert für die Stunde (hh) in einem Bereich von 0 bis 12 liegen.  
  
-   Die Buchstaben „zzz“ kennzeichnen den Offsetwert für die Zeitzone für die aktuelle Zeitzone des Systems im Format {+|-}HH:ss].  
  
## <a name="InsertNumerictypes"></a>Einfügen von Literalen in numerische Typen  
In den folgenden Tabellen definieren, die Standardregeln Format und Konvertierung zum Laden eines literalen Wert in eine SQL Server PDW-Spalte, die einen numerischen Typ verwendet wird.  
  
### <a name="bit-data-type"></a>Bit-Datentyp  
In der folgenden Tabelle definiert, das Standardformat und die Regeln zum Laden von literalen Werten in einer Spalte vom Typ **Bit**. Eine leere Zeichenfolge (") oder eine Zeichenfolge, die nur Leerstellen enthalten (" ") wird in 0 konvertiert.  
  
|Input-Datentyp|Beispiele für die Eingabedaten|Die Konvertierung in den bit-Datentyp|  
|-------------------|-----------------------|-------------------------------|  
|Zeichenfolgenliteral im **Ganzzahl** Format|"Ffffffffff"<br /><br />Beispiel: "1" oder "321"|Ein Ganzzahlwert, formatiert als Zeichenfolgenliteral darf keinen negativen Wert enthalten. Der Wert "-123" generiert z. B. einen Fehler.<br /><br />Ein Wert größer als 1 wird in 1 konvertiert. Beispielsweise wird der Wert "123" in 1 konvertiert.|  
|Ein Zeichenfolgenliteral handeln|'TRUE' oder 'FALSE'<br /><br />Beispiel: "true"|Der Wert "TRUE" wird in 1 konvertiert. der Wert "FALSE" wird in 0 konvertiert.|  
|Integer-literal|fffffffn<br /><br />Beispiel: 1 oder 321|Ein Wert größer als 1 oder kleiner als 0 wird in 1 konvertiert. Beispielsweise werden Werte 123 "und"-123 in 1 konvertiert.|  
|Decimal-literal|fffnn.fffn<br /><br />Beispiel: 1234.5678|Ein Wert größer als 1 oder kleiner als 0 wird in 1 konvertiert. Beispielsweise werden Werte 123,45 "und"-123.45 in 1 konvertiert.|  
  
### <a name="decimal-data-type"></a>Decimal-Datentyp  
In der folgenden Tabelle definiert die Regeln zum Laden von literalen Werten in einer Spalte vom Typ **decimal** (*p, s*). Regeln für die Konvertierung von Daten sind die gleichen wie für SQL Server. Weitere Informationen finden Sie unter [Datentypkonvertierung (Datenbankmodul)](http://go.microsoft.com/fwlink/?LinkId=202128) auf MSDN.  
  
|Input-Datentyp|Beispiele für die Eingabedaten|  
|-------------------|-----------------------|  
|Integer-literal|321312313123|  
|Decimal-literal|123344.34455|  
  
### <a name="float-and-real-data-types"></a>float- und Real-Datentypen  
In der folgenden Tabelle definiert die Regeln zum Laden von literalen Werten in einer Spalte vom Typ **"float"** oder **echte**. Regeln für die Konvertierung von Daten sind die gleichen wie für SQL Server. Weitere Informationen finden Sie unter [Datentypkonvertierung (Datenbankmodul)](../t-sql/data-types/data-type-conversion-database-engine.md) auf MSDN.  
  
|Input-Datentyp|Beispiele für die Eingabedaten|  
|-------------------|-----------------------|  
|Integer-literal|321312313123|  
|Decimal-literal|123344.34455|  
|Floating-Point-literal|3.12323E + 14|  
  
### <a name="int-bigint-tinyint-smallint-data-types"></a>"Int", "bigint", "tinyint", "smallint"-Datentypen  
In der folgenden Tabelle definiert die Regeln zum Laden von literalen Werten in einer Spalte vom Typ **Int**, **"bigint"**, **"tinyint"**, oder **"smallint"**. Die Datenquelle kann nicht die für den angegebenen Datentyp zulässigen Bereichs nicht überschreiten. Z. B. den Bereich für **"tinyint"** ist 0 bis 255 und der Bereich für **Int** wird von – 2.147.483.648 bis 2.147.483.647.  
  
|Input-Datentyp|Beispiele für die Eingabedaten|Die Konvertierung in Integer-Datentypen|  
|-------------------|-----------------------|------------------------------------|  
|Integer-literal|321312313123||  
|Decimal-literal|123344.34455|Die Werte, die rechts neben dem Dezimaltrennzeichen werden abgeschnitten.|  
  
### <a name="money-and-smallmoney-data-types"></a>Datentypen Money und smallmoney  
Money-Literalwerte werden als eine Folge von Ziffern mit einem optionalen Dezimaltrennzeichen und einem optionalen Währungssymbol als Präfix dargestellt. Die Datenquelle kann nicht die für den angegebenen Datentyp zulässigen Bereichs nicht überschreiten. Z. B. den Bereich für **Smallmoney** ist-214,748.3648 214.748,3647 und der Bereich für **Money** 922.337.203.685.477,5808 bis 922.337.203.685.477,5807 ist. In der folgenden Tabelle definiert die Regeln zum Laden von literalen Werten in einer Spalte vom Typ **Money** oder **Smallmoney**.  
  
|Input-Datentyp|Beispiele für die Eingabedaten|Konvertierung zu Money oder Smallmoney-Datentyp|  
|-------------------|-----------------------|-----------------------------------------------|  
|Integer-literal|321312|Fehlende Ziffern nach dem Dezimaltrennzeichen werden auf 0 festgelegt, wenn der Wert eingefügt wird. Das literal 12345 wird beispielsweise als 12345.0000 eingefügt.|  
|Decimal-literal|123344.34455|Wenn die Anzahl der Ziffern nach dem Dezimaltrennzeichen 4 überschreiten, wird der Wert auf den nächsten Wert aufgerundet. Beispielsweise wird der Wert 123344.34455 als 123344.3446 eingefügt.|  
|Money-literal|$123456.7890|Das Währungssymbol wird nicht mit dem Wert eingefügt.<br /><br />Wenn die Anzahl der Ziffern nach dem Dezimaltrennzeichen 4 überschreiten, wird der Wert auf den nächsten Wert aufgerundet.|  
  
## <a name="InsertStringTypes"></a>Literale in Zeichenfolgentypen eingefügt.  
In den folgenden Tabellen definieren, die Standardregeln Format und Konvertierung zum Laden eines literalen Wert in eine SQL Server PDW-Spalte, die einen String-Datentyp verwendet wird.  
  
### <a name="char-varchar-nchar-and-nvarchar-data-types"></a>Char, Varchar, Nchar und Nvarchar-Datentypen  
In der folgenden Tabelle definiert, das Standardformat und die Regeln zum Laden von literalen Werten in einer Spalte vom Typ **Char**, **Varchar**, **Nchar** und **Nvarchar** . Die Länge der Quelle kann nicht für den Datentyp angegebene Größe nicht überschreiten. Wenn die Länge der Quelle geringer als ist die **Char** oder **Nchar** -Datentyp, werden die Daten nach rechts mit Leerzeichen, um die Größe der Daten zu erreichen aufgefüllt.  
  
|Input-Datentyp|Beispiele für die Eingabedaten|Konvertierung in Zeichen-Datentypen|  
|---------------|-------------------|----------------------------------|  
|Ein Zeichenfolgenliteral handeln|Format: "Zeichenfolge"<br /><br />Beispiel: 'Abc'| NA |  
|Unicode-Zeichenfolgenliteral|: Formatzeichenfolge N'character "<br /><br />Beispiel: N '| NA |  
|Integer-literal|Format: Ffffffffffn<br /><br />Beispiel: 321312313123| NA |  
|Decimal-literal|Format: ffffff.fffffff<br /><br />Beispiel: 12344.34455| NA |  
|Money-literal|Format: $ffffff.fffnn<br /><br />Beispiel: $123456.99|Die optionalen Währungssymbol ist nicht mit dem Wert eingefügt. Um das Währungssymbol einzufügen, geben Sie den Wert als Zeichenfolgenliteral. Dadurch wird das Format der das Ladeprogramm entsprechen denen jedes Literal als Zeichenfolgenliteral behandelt.<br /><br />Kommas sind nicht zulässig.<br /><br />Wenn die Anzahl der Ziffern nach dem Dezimaltrennzeichen 2 überschreitet, wird der Wert auf den nächsten Wert aufgerundet. Beispielsweise wird der Wert 123.946789 als 123.95 eingefügt.<br /><br />Nur das Standardformat 0 (keine Kommas und 2 Ziffern nach dem Dezimaltrennzeichen) ist zulässig, wenn die CONVERT-Funktion zu verwenden, um Money Literale einzufügen.|  
  
### <a name="general-remarks"></a>Allgemeine Hinweise  
**Dwloader** führt die gleichen implizite Konvertierungen aus, dass SMP SQL Server ausführt, unterstützt jedoch nicht alle impliziten Konvertierungen SMP SQLServer unterstützt.  
 
<!-- MISSING LINKS 
## See Also  
[Grant Permissions to Load Data &#40;SQL Server PDW&#41;](../sqlpdw/grant-permissions-to-load-data-sql-server-pdw.md)  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  

-->
  

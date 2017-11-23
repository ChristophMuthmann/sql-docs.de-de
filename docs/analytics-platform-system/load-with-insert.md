---
title: Laden von Daten mit INSERT
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.suite: sql
ms.custom: 
ms.technology: mpp-data-warehouse
description: "Sie können die t-SQL-INSERT-Anweisung verwenden, zum Laden von Daten in eine SQLServer Parallel Datawarehouse (PDW) verteilt, oder der replizierten Tabelle."
ms.date: 10/20/2016
ms.topic: article
ms.assetid: 6e951b0e-e95b-4fd1-b5f3-c65607aee0d8
caps.latest.revision: "21"
ms.openlocfilehash: 059dc1e8601fb02aac9a91631a161bae1e995389
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="load-data-with-insert"></a>Laden von Daten mit INSERT

Sie können die t-SQL-INSERT-Anweisung verwenden, zum Laden von Daten in eine SQLServer Parallel Datawarehouse (PDW) verteilt, oder der replizierten Tabelle. Weitere Informationen zum Einfügen, finden Sie unter [einfügen](../t-sql/statements/insert-transact-sql.md). Für replizierte Tabellen und alle nichtverteilungsspalte Spalten in einer verteilten Tabelle verwendet PDW SQL Server, um die Datenwerte in der Anweisung in den Datentyp der Spalte "Ziel" angegebenen implizit zu konvertieren. Weitere Informationen zu Konvertierungsregeln für SQL Server-Daten, finden Sie unter [datentypkonvertierung für SQL](http://msdn.microsoft.com/library/ms191530&#40;v=sql11&#40;.aspx). Für verteilungsspalten unterstützt PDW jedoch nur eine Teilmenge von impliziten Konvertierungen, die SQL Server unterstützt. Wenn Sie die INSERT-Anweisung zum Laden von Daten in eine verteilungsspalte verwenden, müssen daher die Quelldaten in eines der Formate, die in den folgenden Tabellen definiert angegeben werden.  
  
  
## <a name="InsertingLiteralsBinary"></a>Binärtypen Literale einfügen  
In der folgenden Tabelle definiert, der akzeptierten Literaltypen, Format und Konvertierungsregeln für einen literalen Wert in eine verteilungsspalte vom Typ eingefügt **binäre** (*n*) oder  **Varbinary**(*n*).  
  
|Literaltypzeichen|Format|Aufgrund von Konvertierungsregeln|  
|----------------|----------|--------------------|  
|Binäres literal|0 X*Hexidecimal_string*<br /><br />Beispiel: 0x12Ef|Binäre Literale müssen 0 X vorangestellt werden.<br /><br />Die Länge der Quelle darf die angegebene Anzahl von Bytes für den Datentyp nicht überschreiten.<br /><br />Wenn die Länge der Quelle geringer als ist die **binäre** -Datentyp, werden die Daten nach rechts mit Nullen aufgefüllt, um die Größe der Daten zu erreichen aufgefüllt.|  
  
## <a name="InsertingLiteralsDateTime"></a>Legen Sie Literale in Datums- und Uhrzeittypen  
Mit Zeichenwerten enthalten, die in bestimmten Formaten, die in einfache Anführungszeichen eingeschlossen werden Datums- und Zeitliterale dargestellt. In den folgenden Tabellen definieren, die zulässige Literaltypen, Format und Konvertierungsregeln zum Einfügen von Datum oder Uhrzeit-literal in einer SQL Server PDW-Distribution-Spalte vom Typ **"DateTime"**, **Smalldatetime**, **Datum**, **Zeit**, **"DateTimeOffset"**, oder **datetime2**.  
  
### <a name="datetime-data-type"></a>DateTime-Datentyp  
In der folgenden Tabelle definiert, die akzeptierte Formate und die Regeln zum Einfügen von Literalwerten in eine verteilungsspalte des Typs **"DateTime"**. Eine leere Zeichenfolge (") wird auf den Standardwert konvertiert" 12:00:00.000 1900-01-01 ". Zeichenfolgen, die nur Leerstellen enthalten ("") ein Fehler generiert.  
  
|Literaltypzeichen|Format|Aufgrund von Konvertierungsregeln|  
|----------------|----------|--------------------|  
|Zeichenfolgenliteral im **"DateTime"** Format|"YYYY-MM-DD HH: mm: [.nnn]"<br /><br />Beispiel: "2007-05-08-12:35:29.123"|Fehlende Dezimalstellen werden auf 0 festgelegt, wenn der Wert eingefügt wird. Angenommen, das Literal "2007-05-08 12:35 ' wird als eingefügt" 2007-05-08-12:35:00.000 ".|  
|Zeichenfolgenliteral im **Smalldatetime** Format|"YYYY-MM-DD HH: mm"<br /><br />Beispiel: "2007-05-08 12:35"|Sekunden und die restlichen Dezimalstellen werden auf 0 festgelegt, wenn der Wert eingefügt wird.|  
|Zeichenfolgenliteral im **Datum** Format|"JJJJ-MM-TT"<br /><br />Beispiel: "2007-05-08"|Time-Werten (Stunde, Minuten, Sekunden und Sekundenbruchteile) werden auf 12:00:00.000 festgelegt, wenn der Wert eingefügt wird.|  
|Zeichenfolgenliteral im **datetime2** Format|"JJJJ-MM-TT ss.nnnnnnn"<br /><br />Beispiel: "2007-05-08-12:35:29.1234567"|Die Quelldaten darf drei Dezimalstellen nicht überschreiten. Z. B. das Literal "2007-05-08-12:35:29.123" eingefügt werden, aber der Wert "2007-05-08-12:35:29.1234567" wird ein Fehler generiert.|  
  
### <a name="smalldatetime-data-type"></a>Smalldatetime-Datentyp  
In der folgenden Tabelle definiert, die akzeptierte Formate und die Regeln zum Einfügen von Literalwerten in eine verteilungsspalte des Typs **Smalldatetime**. Eine leere Zeichenfolge (") wird auf den Standardwert konvertiert" 1900-01-01 12:00 ". Zeichenfolgen, die nur Leerstellen enthalten ("") ein Fehler generiert.  
  
|Literaltypzeichen|Format|Aufgrund von Konvertierungsregeln|  
|----------------|----------|--------------------|  
|Zeichenfolgenliteral im **Smalldatetime** Format|"YYYY-MM-DD HH: mm" oder "JJJJ-MM-tt Hh:mm:00"<br /><br />Beispiel: "2007-05-08 12:00 ' oder ' 2007-05-08 12:00:00"|Die Quelldaten müssen Werte für Jahr, Monat, Datum, Stunde und Minute aufweisen. Sekunden sind optional und, falls vorhanden, müssen auf den Wert 00 festgelegt werden. Jeder andere Wert wird einen Fehler generiert.|  
|Zeichenfolgenliteral im **Datum** Format|"JJJJ-MM-TT"<br /><br />Beispiel: "2007-05-08"|Time-Werten (Stunde, Minuten, Sekunden und Sekundenbruchteile) werden auf 0 festgelegt, wenn der Wert eingefügt wird.|  
  
### <a name="date-data-type"></a>Date-Datentyp  
In der folgenden Tabelle definiert, die akzeptierte Formate und die Regeln zum Einfügen von Literalwerten in eine verteilungsspalte des Typs **Datum**. Eine leere Zeichenfolge (") wird auf den Standardwert konvertiert" 1900-01-01 ". Zeichenfolgen, die nur Leerstellen enthalten ("") ein Fehler generiert.  
  
|Literaltypzeichen|Format|Aufgrund von Konvertierungsregeln|  
|----------------|----------|--------------------|  
|Zeichenfolgenliteral im **Datum** Format|"JJJJ-MM-TT"<br /><br />Beispiel: "2007-05-08"|Dies ist der einzige akzeptierte Format.|  
  
### <a name="time-data-type"></a>Zeitdatentyp  
In der folgenden Tabelle definiert, die akzeptierte Formate und die Regeln zum Einfügen von Literalwerten in eine verteilungsspalte des Typs **Zeit**. Eine leere Zeichenfolge (") wird auf den Standardwert"00:00:00.0000"konvertiert. Zeichenfolgen, die nur Leerstellen enthalten ("") ein Fehler generiert.  
  
|Literaltypzeichen|Format|Aufgrund von Konvertierungsregeln|  
|----------------|----------|--------------------|  
|Zeichenfolgenliteral im **Zeit** Format|"ss.nnnnnnn"<br /><br />Beispiel: "12:35:29.1234567"|Wenn die Datenquelle eine Genauigkeit kleinere oder gleich (Anzahl der Dezimalstellen) als die Genauigkeit des enthält die **Zeit** -Datentyp, werden die Daten auf die rechte Seite mit Nullen aufgefüllt. Beispielsweise wird ein Literalwert "12:35:29.123" als "12:35:29.1230000" eingefügt.<br /><br />Ein Wert, der eine größere Genauigkeit als den Zieldatentyp wurde abgelehnt.|  
  
### <a name="datetimeoffset-data-type"></a>DateTimeOffset-Datentyp  
In der folgenden Tabelle definiert, die akzeptierte Formate und die Regeln zum Einfügen von Literalwerten in eine verteilungsspalte des Typs **"DateTimeOffset"** (*n*). Das Standardformat ist ' YYYY-MM-DD ss.nnnnnnn {+ |-} hh: mm ". Der Standardwert ist eine leere Zeichenfolge (") konvertiert" 1900-01-01 12:00:00.0000000 + 00:00 ". Zeichenfolgen, die nur Leerstellen enthalten ("") ein Fehler generiert. Die Anzahl der Dezimalstellen, hängt von der Definition der Spalte ab. Angenommen, eine Spalte, die als definiert **"DateTimeOffset"** (2) hat zwei Dezimalstellen.  
  
|Literaltypzeichen|Format|Aufgrund von Konvertierungsregeln|  
|----------------|----------|--------------------|  
|Zeichenfolgenliteral im **"DateTime"** Format|"YYYY-MM-DD HH: mm: [.nnn]"<br /><br />Beispiel: "2007-05-08-12:35:29.123"|Fehlende Dezimalstellen und Offset-Werte werden auf 0 festgelegt, wenn der Wert eingefügt wird. Angenommen, das Literal "2007-05-08-12:35:29.123" als eingefügt "2007-05-08-12:35:29.1230000 + 00:00".|  
|Zeichenfolgenliteral im **Smalldatetime** Format|"YYYY-MM-DD HH: mm"<br /><br />Beispiel: "2007-05-08 12:35"|Sekunden, die restlichen Dezimalstellen und die Offset-Werte werden auf 0 festgelegt, wenn der Wert eingefügt wird.|  
|Zeichenfolgenliteral im **Datum** Format|"JJJJ-MM-TT"<br /><br />Beispiel: "2007-05-08"|Time-Werten (Stunde, Minuten, Sekunden und Sekundenbruchteile) werden auf 0 festgelegt, wenn der Wert eingefügt wird. Z. B., das literal "2007-05-08' wird als eingefügt" 2007-05-08-00:00:00.0000000 + 00:00 ".|  
|Zeichenfolgenliteral im **datetime2** Format|"JJJJ-MM-TT ss.nnnnnnn"<br /><br />Beispiel: "2007-05-08-12:35:29.1234567"|Die Quelldaten darf die angegebene Anzahl von Sekundenbruchteilen in der Spalte "DateTimeOffset" nicht überschreiten. Wenn die Datenquelle eine Zahl kleinere oder gleich der Bruchteile von Sekunden enthält, wird auf die rechte Seite mit Nullen aufgefüllt. Angenommen, der Datentyp "DateTimeOffset" (5), der literale Wert ist "2007-05-08-12:35:29.123 + 12:15 ' wird als eingefügt" 12:35:29.12300 + 12:15 '.|  
|Zeichenfolgenliteral im **"DateTimeOffset"** Format|"JJJJ-MM-TT ss.nnnnnnn {+ &#124;;-} hh: mm"<br /><br />Beispiel: "2007-05-08-12:35:29.1234567 + 12:15 '|Die Quelldaten darf die angegebene Anzahl von Sekundenbruchteilen in der Spalte "DateTimeOffset" nicht überschreiten. Wenn die Datenquelle eine Zahl kleinere oder gleich der Bruchteile von Sekunden enthält, wird auf die rechte Seite mit Nullen aufgefüllt. Angenommen, der Datentyp "DateTimeOffset" (5), der literale Wert ist "2007-05-08-12:35:29.123 + 12:15 ' wird als eingefügt" 12:35:29.12300 + 12:15 '.|  
  
### <a name="datetime2-data-type"></a>datetime2-Datentyp  
In der folgenden Tabelle definiert, die akzeptierte Formate und die Regeln zum Einfügen von Literalwerten in eine verteilungsspalte des Typs **datetime2** (*n*). Das Standardformat ist "YYYY-MM-DD ss.nnnnnnn". Der Standardwert ist eine leere Zeichenfolge (") konvertiert" 1900-01-01 – 12:00:00 ". Zeichenfolgen, die nur Leerstellen enthalten ("") ein Fehler generiert. Die Anzahl der Dezimalstellen, hängt von der Definition der Spalte ab. Angenommen, eine Spalte, die als definiert **datetime2** (2) hat zwei Dezimalstellen.  
  
|Literaltypzeichen|Format|Aufgrund von Konvertierungsregeln|  
|----------------|----------|--------------------|  
|Zeichenfolgenliteral im **"DateTime"** Format|"YYYY-MM-DD HH: mm: [.nnn]"<br /><br />Beispiel: "2007-05-08-12:35:29.123"|Sekundenbruchteile sind optional und werden auf 0 festgelegt, wenn der Wert eingefügt wird.<br /><br />Ein Wert mit mehr Dezimalstellen als den Zieldatentyp wird abgelehnt.|  
|Zeichenfolgenliteral im **Smalldatetime** Format|"YYYY-MM-DD HH: mm"<br /><br />Beispiel: "2007-05-08-12"|Optionale Sekunden und die restlichen Dezimalstellen werden auf 0 festgelegt, wenn der Wert eingefügt wird.|  
|Zeichenfolgenliteral im **Datum** Format|"JJJJ-MM-TT"<br /><br />Beispiel: "2007-05-08"|Time-Werten (Stunde, Minuten, Sekunden und Sekundenbruchteile) werden auf 0 festgelegt, wenn der Wert eingefügt wird. Z. B., das literal "2007-05-08' wird als eingefügt" 2007-05-08-12:00:00.0000000 ".|  
|Zeichenfolgenliteral im **datetime2** Format|"JJJJ-MM-tt Hh:mm:ss:nnnnnnn"<br /><br />Beispiel: "2007-05-08-12:35:29.1234567"|Wenn die Datenquelle und der Zeitpunkt der Komponenten enthält, die kleiner oder gleich dem Wert im angegebenen **datetime2**(*n*), die Daten eingefügt, da andernfalls ein Fehler ausgelöst wird.|  
  
## <a name="InsertLiteralsNumeric"></a>Einfügen von Literalen in numerische Typen  
In den folgenden Tabellen definieren die akzeptierte Formate und Konvertierungsregeln zum Einfügen von einen literalen Wert in eine SQL Server PDW-verteilungsspalte, die einen numerischen Typ verwendet.  
  
### <a name="bit-data-type"></a>bit-Datentyp  
In der folgenden Tabelle definiert, die akzeptierte Formate und die Regeln zum Einfügen von Literalwerten in eine verteilungsspalte des Typs **Bit**. Eine leere Zeichenfolge (") oder eine Zeichenfolge, die nur Leerstellen enthalten (" ") wird in 0 konvertiert.  
  
|Literaltypzeichen|format|Aufgrund von Konvertierungsregeln|  
|----------------|----------|--------------------|  
|Zeichenfolgenliteral im **Ganzzahl** Format|"Nnnnnnnnnn"<br /><br />Beispiel: "1" oder "321"|Ein Ganzzahlwert, formatiert als Zeichenfolgenliteral darf keinen negativen Wert enthalten. Der Wert "-123" generiert z. B. einen Fehler.<br /><br />Ein Wert größer als 1 wird in 1 konvertiert. Beispielsweise wird der Wert "123" in 1 konvertiert.|  
|Ein Zeichenfolgenliteral handeln|'TRUE' oder 'FALSE'<br /><br />Beispiel: "true"|Der Wert "TRUE" wird in 1 konvertiert. der Wert "FALSE" wird in 0 konvertiert.|  
|Integer-literal|nnnnnnnn<br /><br />Beispiel: 1 oder 321|Ein Wert größer als 1 oder kleiner als 0 wird in 1 konvertiert. Beispielsweise werden Werte 123 "und"-123 in 1 konvertiert.|  
|Decimal-literal|nnnnn.nnnn<br /><br />Beispiel: 1234.5678|Ein Wert größer als 1 oder kleiner als 0 wird in 1 konvertiert. Beispielsweise werden Werte 123,45 "und"-123.45 in 1 konvertiert.|  
  
### <a name="decimal-data-type"></a>decimal-Datentyp  
In der folgenden Tabelle definiert, die akzeptierte Formate und die Regeln zum Einfügen von Literalwerten in eine verteilungsspalte des Typs **decimal** (*p, s*). Die Konvertierungsregeln für die Daten werden genauso wie bei SQL Server. Weitere Informationen finden Sie unter [datentypkonvertierung](http://msdn.microsoft.com/library/ms191530&#40;v=sql11&#40;.aspx) auf MSDN.  
  
|Literaltypzeichen|Format|  
|----------------|----------|  
|Zeichenfolgenliteral im **Ganzzahl** Format|"Nnnnnnnnnnnn"<br /><br />Beispiel: "321312313123"|  
|Zeichenfolgenliteral im **decimal** Format|"nnnnnn.nnnnn"<br /><br />Beispiel: "123344.34455"|  
|Integer-literal|nnnnnnnnnnnn<br /><br />Beispiel: 321312313123|  
|Decimal-literal|nnnnnn.nnnnn<br /><br />Beispiel: "123344.34455"|  
  
### <a name="float-and-real-data-types"></a>float- und Real-Datentypen  
In der folgenden Tabelle definiert, die akzeptierte Formate und die Regeln zum Einfügen von Literalwerten in eine verteilungsspalte des Typs **"float"** oder **echte**. Regeln für die Konvertierung von Daten sind die gleichen wie für SQL Server. Weitere Informationen finden Sie unter [datentypkonvertierung](http://msdn.microsoft.com/library/ms191530&#40;v=sql11&#40;.aspx) auf MSDN.  
  
|Literaltypzeichen|Format|  
|----------------|----------|  
|Zeichenfolgenliteral im **Ganzzahl** Format|"Nnnnnnnnnnnn"<br /><br />Beispiel: "321312313123"|  
|Zeichenfolgenliteral im **decimal** Format|"nnnnnn.nnnnn"<br /><br />Beispiel: "123344.34455"|  
|Zeichenfolgenliteral im **Gleitkomma** Format|"n.nnnnnE+nn"<br /><br />Beispiel: "3.12323E + 14"|  
|Integer-literal|nnnnnnnnnnnn<br /><br />Beispiel: 321312313123|  
|Decimal-literal|nnnnnn.nnnnn<br /><br />Beispiel: 123344.34455|  
|Floating-Point-literal|n.nnnnnE+nn<br /><br />Beispiel: 3.12323E + 14|  
  
### <a name="int-bigint-tinyint-smallint-data-types"></a>Int, Bigint, "tinyint", "smallint"-Datentypen  
In der folgenden Tabelle definiert, die akzeptierte Formate und die Regeln zum Einfügen von Literalwerten in eine verteilungsspalte des Typs **Int**, **"bigint"**, **"tinyint"**, oder **"smallint"**. Die Datenquelle kann nicht die für den angegebenen Datentyp zulässigen Bereichs nicht überschreiten. Z. B. den Bereich für **"tinyint"** ist 0 bis 255 und der Bereich für **Int** wird von – 2.147.483.648 bis 2.147.483.647.  
  
|Literaltyp|Format|Aufgrund von Konvertierungsregeln|  
|------------|------|----------------|
|Zeichenfolgenliteral im **Ganzzahl** Format|"Nnnnnnnnnnnnnn"<br /><br />Beispiel: "321312313123"| Keine |  
|Integer-literal|nnnnnnnnnnnnnn<br /><br />Beispiel: 321312313123| Keine|  
|Decimal-literal|nnnnnn.nnnnn<br /><br />Beispiel: 123344.34455|Die Werte, die rechts neben dem Dezimaltrennzeichen werden abgeschnitten.|  
  
### <a name="money-and-smallmoney-data-types"></a>Datentypen Money und smallmoney  
Money-Literalwerte werden als Zahlen mit einem optionalen Dezimaltrennzeichen und das Währungssymbol als Präfix dargestellt. Die Datenquelle kann nicht die für den angegebenen Datentyp zulässigen Bereichs nicht überschreiten. Z. B. den Bereich für **Smallmoney** ist-214,748.3648 214.748,3647 und der Bereich für **Money** 922.337.203.685.477,5808 bis 922.337.203.685.477,5807 ist. In der folgenden Tabelle definiert, die akzeptierte Formate und die Regeln zum Einfügen von Literalwerten in eine verteilungsspalte des Typs **Money** oder **Smallmoney**.  
  
|Literaltypzeichen|Format|Aufgrund von Konvertierungsregeln|  
|----------------|----------|--------------------|  
|Zeichenfolgenliteral im **Ganzzahl** Format|"Nnnnnnnn"<br /><br />Beispiel: "123433"|Fehlende Ziffern nach dem Dezimaltrennzeichen werden auf 0 festgelegt, wenn der Wert eingefügt wird. Beispielsweise wird das literal "12345" als 12345.0000 eingefügt.|  
|Zeichenfolgenliteral im **decimal** Format|"nnnnnn.nnnnn"<br /><br />Beispiel: "123344.34455"|Wenn die Anzahl der Ziffern nach dem Dezimaltrennzeichen 4 überschreiten, wird der Wert auf den nächsten Wert aufgerundet. Beispielsweise wird der Wert "123344.34455" als 123344.3446 eingefügt.|  
|Zeichenfolgenliteral im **Money** Format|"$nnnnnn.nnnn"<br /><br />Beispiel: "$123456.7890"|Die optionalen Währungssymbol ist nicht mit dem Wert eingefügt.<br /><br />Wenn die Anzahl der Ziffern nach dem Dezimaltrennzeichen 4 überschreiten, wird der Wert auf den nächsten Wert aufgerundet.|  
|Integer-literal|nnnnnnnn<br /><br />Beispiel: 123433|Fehlende Ziffern nach dem Dezimaltrennzeichen werden auf 0 festgelegt, wenn der Wert eingefügt wird. Beispielsweise wird das literal 12345 als 12345.0000 eingefügt.|  
|Decimal-literal|nnnnnn.nnnnn<br /><br />Beispiel: 123344.34455|Wenn die Anzahl der Ziffern nach dem Dezimaltrennzeichen 4 überschreiten, wird der Wert auf den nächsten Wert aufgerundet. Beispielsweise wird der Wert 123344.34455 als 123344.3446 eingefügt.|  
|Money-literal|$nnnnnn.nnnn<br /><br />Beispiel: $123456.7890|Die optionalen Währungssymbol ist nicht mit dem Wert eingefügt.<br /><br />Wenn die Anzahl der Ziffern nach dem Dezimaltrennzeichen 4 überschreiten, wird der Wert auf den nächsten Wert aufgerundet.|  
  
## <a name="InsertLiteralsString"></a>Literale in Zeichenfolgentypen eingefügt.  
In den folgenden Tabellen definieren die akzeptierte Formate und Konvertierungsregeln zum Einfügen von einen literalen Wert in eine SQL Server PDW-Spalte, die einen String-Datentyp verwendet.  
  
### <a name="char-varchar-nchar-and-nvarchar-data-types"></a>Char, Varchar, Nchar und Nvarchar-Datentypen  
In der folgenden Tabelle definiert, die akzeptierte Formate und die Regeln zum Einfügen von Literalwerten in eine verteilungsspalte des Typs **Char**, **Varchar**, **Nchar** und **Nvarchar**. Die Länge der Quelle kann nicht für den Datentyp angegebene Größe nicht überschreiten. Wenn die Länge der Quelle geringer als ist die **Char** oder **Nchar** -Datentyp, werden die Daten nach rechts mit Leerzeichen, um die Größe der Daten zu erreichen aufgefüllt.  
  
|Literaltyp|Format|Aufgrund von Konvertierungsregeln|  
|----------------|----------|--------------------|  
|Ein Zeichenfolgenliteral handeln|Format: "Zeichenfolge"<br /><br />Beispiel: 'Abc'| Keine|  
|Unicode-Zeichenfolgenliteral|: Formatzeichenfolge N'character "<br /><br />Beispiel: N '|  Keine |  
|Integer-literal|Format: Nnnnnnnnnnn<br /><br />Beispiel: 321312313123| Keine |  
|Decimal-literal|Format: nnnnnn.nnnnnnn<br /><br />Beispiel: 12344.34455| Keine |  
|Money-literal|Format: $nnnnnn.nnnnn<br /><br />Beispiel: $123456.99|Das Währungssymbol wird nicht mit dem Wert eingefügt. Um das Währungssymbol einzufügen, geben Sie den Wert als Zeichenfolgenliteral. Dies entspricht das Format der **Dwloader** Tool, das jedes Literal als Zeichenfolgenliteral behandelt.<br /><br />Kommas sind nicht zulässig.<br /><br />Wenn die Anzahl der Ziffern nach dem Dezimaltrennzeichen 2 überschreitet, wird der Wert auf den nächsten Wert aufgerundet. Beispielsweise wird der Wert 123.946789 als 123.95 eingefügt.<br /><br />Nur das Standardformat 0 (keine Kommas und 2 Ziffern nach dem Dezimaltrennzeichen) ist zulässig, wenn die CONVERT-Funktion zu verwenden, um Money Literale einzufügen.|  

  
## <a name="see-also"></a>Siehe auch  
 
[Verteilte Daten](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-distributed-data/)  
[INSERT](../t-sql/statements/insert-transact-sql.md)  
  
<!-- MISSING LINKS
[Grant permissions to load data](grant-permissions-to-load-data.md)  
[Metadata query examples](metadata-query-examples.md) 
-->

---
title: DATEDIFF_BIG (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DATEDIFF_BIG
- DATEDIFF_BIG_TSQL
helpviewer_keywords:
- DATEDIFF_BIG function [SQL Server]
- dates [SQL Server]. functions
- date and time [SQL Server], DATEDIFF_BIG
- functions [SQL Server], time
- functions [SQL Server], date and time
- time [SQL Server], functions
ms.assetid: 19ac1693-3cfa-400d-bf83-20a9cb46599a
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 6c8228f0db3e37fe3bf6425d60fd4f9067e92220
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="datediffbig-transact-sql"></a>DATEDIFF_BIG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Gibt die Anzahl (große ganze Zahl mit Vorzeichen) der angegebenen *datepart*-Begrenzungen zurück, die zwischen den angegebenen Werten für *startdate* und *enddate* überschritten wurden.
  
Eine Übersicht über alle Datums- und Uhrzeitdatentypen und zugehörige Funktionen für [!INCLUDE[tsql](../../includes/tsql-md.md)] finden Sie unter [Datums- und Uhrzeitdatentypen und zugehörige Funktionen &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
  
DATEDIFF_BIG ( datepart , startdate , enddate )  
```  
  
## <a name="arguments"></a>Argumente  
*datepart*  
Der Teil von *startdate* und *enddate*, der den Typ der überschrittenen Begrenzung angibt. In der folgenden Tabelle werden alle gültigen *datepart*-Argumente aufgeführt. Benutzerdefinierte Variablenentsprechungen sind nicht gültig.
  
|*datepart*|Abkürzungen|  
|---|---|
|**year**|**yy, yyyy**|  
|**quarter**|**qq, q**|  
|**month**|**mm, m**|  
|**dayofyear**|**dy, y**|  
|**day**|**dd, d**|  
|**week**|**wk, ww**|  
|**hour**|**hh**|  
|**minute**|**mi, n**|  
|**second**|**ss, s**|  
|**millisecond**|**ms**|  
|**microsecond**|**mcs**|  
|**nanosecond**|**ns**|  
  
*startdate*  
Ein Ausdruck, der in einen der folgenden Werte aufgelöst werden kann: **time**, **date**, **smalldatetime**, **datetime**, **datetime2** oder **datetimeoffset**. *date* kann ein Ausdruck, ein Spaltenausdruck, eine benutzerdefinierte Variable oder ein Zeichenfolgenliteral sein. *startdate* wird von *enddate* abgezogen.  
Um Mehrdeutigkeiten zu vermeiden, sollten Sie vierstellige Jahreszahlen verwenden. Informationen zu zweistelligen Jahreszahlen finden Sie unter [Konfigurieren der Serverkonfigurationsoption „Umstellungsjahr für Angaben mit zwei Ziffern“](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md).
  
*enddate*  
Weitere Informationen finden Sie unter *startdate*.
  
## <a name="return-type"></a>Rückgabetyp  
 Signiert   
        **bigint**  
  
## <a name="return-value"></a>Rückgabewert  
Gibt die Anzahl (große ganze Zahl mit Vorzeichen) der angegebenen datepart-Begrenzungen zurück, die zwischen den angegebenen Werten für „startdate“ und „enddate“ überschritten wurden.
-   Jedes *datepart*-Argument und die zugehörigen Abkürzungen geben den gleichen Wert zurück.  
  
Wenn der Rückgabewert außerhalb des Bereichs für **int** liegt (–9.223.372.036.854.775.808 bis +9.223.372.036.854.775.807), wird ein Fehler zurückgegeben. Der maximale Unterschied zwischen *startdate* und *enddate* beträgt für **millisecond** 24 Tage, 20 Stunden, 31 Minuten und 23,647 Sekunden. Für **second** beträgt der maximale Unterschied 68 Jahre.
  
Wenn *startdate* und *enddate* jeweils nur einen Uhrzeitwert zugeordnet ist und *datepart* kein Zeit-*datepart* ist, wird 0 (null) zurückgegeben.
  
Beim Berechnen des Rückgabewerts wird keine Komponente von *startdate* oder *enddate* für den Zeitzonenoffset verwendet.
  
Da [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md) nur auf die Minute genaue Werte zurückgibt, wenn bei einem **smalldatetime**-Wert *startdate* oder *enddate* verwendet wird, werden im Rückgabewert die Sekunden und die Millisekunden immer auf 0 (null) festgelegt.
  
Wenn zu einer Variablen eines Datumsdatentyps nur ein Uhrzeitwert zugeordnet wird, wird für den Wert des fehlenden Datumsteils der Standardwert festgelegt: 1900-01-01. Wenn zu einer Variablen eines Uhrzeit- oder Datumsdatentyps nur ein Datumswert zugeordnet wird, wird für den Wert des fehlenden Uhrzeitteils der Standardwert festgelegt: 00-00-00. Wenn entweder *startdate* oder *enddate* nur über einen Uhrzeitteil und der andere nur über einen Datumsteil verfügen, werden für die fehlenden Uhrzeit- und Datumstypen die Standardwerte festgelegt.
  
Wenn *startdate* und *enddate* unterschiedliche Datumsdatentypen darstellen und ein Datentyp mehr Uhrzeitteile oder eine höhere Genauigkeit bezüglich der Bruchteile von Sekunden aufweist als der andere Teil, wird für die fehlenden Teile des anderen Datentyps 0 (null) festgelegt.
  
## <a name="datepart-boundaries"></a>datepart-Begrenzungen
Die folgenden Anweisungen verfügen über den gleichen Wert für *startdate* und den gleichen Wert für *enddate*. Die Datumsangaben folgen aufeinander und unterscheiden sich in der Uhrzeit um 0,0000001 Sekunden. Der Unterschied zwischen *startdate* und *enddate* in jeder Anweisung überschreitet eine Kalender- oder Uhrzeitbegrenzung des zugehörigen *datepart*. Jede Anweisung gibt 1 zurück. Wenn für dieses Beispiel unterschiedliche Jahre verwendet werden und sowohl *startdate* als auch *enddate* in derselben Kalenderwoche liegen, entspricht der Rückgabewert für **week** dem Wert 0 (null).

```sql
SELECT DATEDIFF_BIG(year, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(quarter, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(month, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(dayofyear, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(day, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(week, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(hour, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(minute, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(second, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(millisecond, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
```
  
## <a name="remarks"></a>Remarks  
DATEDIFF_BIG kann in den Klauseln WHERE, HAVING, GROUP BY und ORDER BY der Auswahlliste verwendet werden.
  
DATEDIFF_BIG wandelt Zeichenfolgenliterale implizit in den **datetime2**-Typ um. Daher unterstützt DATEDIFF_BIG das Format YDM nicht, wenn das Datum als Zeichenfolge übergeben wird. Sie müssen die Zeichenfolge explizit in den Typ **datetime** oder **smalldatetime** umwandeln, um das YDM-Format zu verwenden.
  
Das Angeben von SET DATEFIRST hat keine Auswirkungen auf DATEDIFF_BIG. DATEDIFF_BIG verwendet immer Sonntag als ersten Wochentag, um zu gewährleisten, dass die Funktion deterministisch ist.
  
## <a name="examples"></a>Beispiele  
In den folgenden Beispielen werden verschiedene Typen von Ausdrücken als Argumente für den *startdate*- und den *enddate*-Parameter verwendet.
  
### <a name="specifying-columns-for-startdate-and-enddate"></a>Angeben von Spalten für startdate und enddate  
Im folgenden Beispiel wird die Anzahl der Tagesbegrenzungen berechnet, die von den Datumsangaben in zwei Spalten in einer Tabelle überschritten wurden.
  
```sql
CREATE TABLE dbo.Duration  
    (  
    startDate datetime2  
    ,endDate datetime2  
    );  
INSERT INTO dbo.Duration(startDate,endDate)  
    VALUES('2007-05-06 12:10:09','2007-05-07 12:10:09');  
SELECT DATEDIFF_BIG(day,startDate,endDate) AS 'Duration'  
FROM dbo.Duration;  
-- Returns: 1  
```  
  
Viele weitere Beispiele finden Sie in den eng verwandten Beispielen unter [DATEDIFF &#40;Transact-SQL&#41;](../../t-sql/functions/datediff-transact-sql.md).
  
## <a name="see-also"></a>Siehe auch
[CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[DATEDIFF &#40;Transact-SQL&#41;](../../t-sql/functions/datediff-transact-sql.md)
  
  

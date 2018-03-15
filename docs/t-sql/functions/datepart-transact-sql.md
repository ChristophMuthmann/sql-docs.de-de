---
title: DATEPART (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DATEPART_TSQL
- DATEPART
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- date and time [SQL Server], DATEPART
- dateparts [SQL Server]
- functions [SQL Server], time
- functions [SQL Server], date and time
- time [SQL Server], functions
- dateparts [SQL Server], datepart
- comparing dates times [SQL Server]
- DATEPART function [SQL Server]
- dates [SQL Server], dateparts
ms.assetid: 15f1a5bc-4c0c-4c48-848d-8ec03473e6c1
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: a972e0646d68620b915fe441e35ebfb617d06859
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="datepart-transact-sql"></a>DATEPART (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Gibt einen Integer zurück, der den angegebenen *datepart*-Wert des angegebenen *date*-Werts darstellt.
  
Eine Übersicht über alle Datums- und Uhrzeitdatentypen und zugehörige Funktionen für [!INCLUDE[tsql](../../includes/tsql-md.md)] finden Sie unter [Datums- und Uhrzeitdatentypen und zugehörige Funktionen &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
DATEPART ( datepart , date )  
```  
  
## <a name="arguments"></a>Argumente  
*datepart*  
Der *date*-Teil (ein Datums- oder Zeitwert), für den ein **Integer** zurückgegeben wird. In der folgenden Tabelle werden alle gültigen *datepart*-Argumente aufgeführt. Benutzerdefinierte Variablenentsprechungen sind nicht gültig.
  
|*datepart*|Abkürzungen|  
|---|---|
|**year**|**yy**, **yyyy**|  
|**quarter**|**qq**, **q**|  
|**month**|**mm**, **m**|  
|**dayofyear**|**dy**, **y**|  
|**day**|**dd**, **d**|  
|**week**|**wk**, **ww**|  
|**weekday**|**dw**|  
|**hour**|**hh**|  
|**minute**|**mi, n**|  
|**second**|**ss**, **s**|  
|**millisecond**|**ms**|  
|**microsecond**|**mcs**|  
|**nanosecond**|**ns**|  
|**TZoffset**|**tz**|  
|**ISO_WEEK**|**isowk**, **isoww**|  
  
*Datum*  
Ein Ausdruck, der in einen der folgenden Werte aufgelöst werden kann: **time**, **date**, **smalldatetime**, **datetime**, **datetime2** oder **datetimeoffset**. *date* kann ein Ausdruck, ein Spaltenausdruck, eine benutzerdefinierte Variable oder ein Zeichenfolgenliteral sein.  
Um Mehrdeutigkeiten zu vermeiden, sollten Sie vierstellige Jahreszahlen verwenden. Informationen zu zweistelligen Jahreszahlen finden Sie unter [Konfigurieren der Serverkonfigurationsoption „Umstellungsjahr für Angaben mit zwei Ziffern“](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md).
  
## <a name="return-type"></a>Rückgabetyp  
 **int**  
  
## <a name="return-value"></a>Rückgabewert  
Jedes *datepart*-Argument und die zugehörigen Abkürzungen geben denselben Wert zurück.
  
Der Rückgabewert hängt von der Sprachumgebung ab, die durch [SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md) und durch die [Konfiguration der Serverkonfigurationsoption „Standardsprache“](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md) für die Anmeldung festgelegt wurde. Wenn *date* ein Zeichenfolgenliteral für einige Formate darstellt, hängt der Rückgabewert von dem Format ab, das mit [SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md) festgelegt wurde. SET DATEFORMAT wirkt sich nicht auf den Rückgabewert aus, wenn das Datum ein Spaltenausdruck für Daten vom Typ Datum oder Uhrzeit darstellt.
  
In der folgenden Tabelle werden alle *datepart*-Argumente mit den entsprechenden Rückgabewerten für die Anweisung `SELECT DATEPART(datepart,'2007-10-30 12:15:32.1234567 +05:10')` aufgelistet. Der Datentyp des *date*-Arguments ist **datetimeoffset(7)**. Der **nanosecond**-Rückgabewert von *datetime* verfügt über 9 Dezimalstellen (,123456700), wobei die letzten beiden Stellen immer 00 sind.
  
|*datepart*|Rückgabewert|  
|---|---|
|**year, yyyy, yy**|2007|  
|**quarter, qq, q**|4|  
|**month, mm, m**|10|  
|**dayofyear, dy, y**|303|  
|**day, dd, d**|30|  
|**week, wk, ww**|45|  
|**weekday, dw**|1|  
|**hour, hh**|12|  
|**minute, n**|15|  
|**second, ss, s**|32|  
|**millisecond, ms**|123|  
|**microsecond, mcs**|123456|  
|**nanosecond, ns**|123456700|  
|**TZoffset, tz**|310|  
  
## <a name="week-and-weekday-datepart-arguments"></a>datepart-Argumente des Typs week und weekday
Wenn für *datepart* **week** (**wk**, **ww**) oder **weekday** (**dw**) angegeben wurde, hängt der Rückgabewert von dem Wert ab, der durch [SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md) festgelegt wurde.
  
Der 1. Januar eines Jahres definiert die Anfangszahl für das *datepart*-Argument **week**. Beispiel: DATEPART (**wk**, 'Jan 1, *xxx*x') = 1, wobei *xxxx* ein beliebiges Jahr ist.
  
In der folgenden Tabelle wird für jedes SET DATEFIRST-Argument der Rückgabewert des Arguments **week** und **weekday** von *datepart* für '2007-04-21' aufgelistet. Der 1. Januar ist im Jahr 2007 ein Montag. Der 21. April ist im Jahr 2007 ein Samstag. SET DATEFIRST 7 (Sonntag) ist die Standardeinstellung für Englisch (USA). Englisch.
  
|SET DATEFIRST<br /><br /> Argument|week<br /><br /> hat zurückgegeben|weekday<br /><br /> hat zurückgegeben|  
|---|---|---|
|1|16|6|  
|2|17|5|  
|3|17|4|  
|4|17|3|  
|5|17|2|  
|6|17|1|  
|7|16|7|  
  
## <a name="year-month-and-day-datepart-arguments"></a>datepart-Argumente des Typs year, month und day  
Die für DATEPART (**year**, *date*), DATEPART (**month**, *date*) und DATEPART (**day**, *date*) zurückgegebenen Werte entsprechen den jeweiligen Rückgabewerten der Funktionen [YEAR](../../t-sql/functions/year-transact-sql.md), [MONTH](../../t-sql/functions/month-transact-sql.md) und [DAY](../../t-sql/functions/day-transact-sql.md).
  
## <a name="isoweek-datepart"></a>ISO_WEEK datepart  
ISO 8601 schließt das ISO-Wochensystem zur Nummerierung von Wochen ein. Die einzelnen Wochen werden mit dem Jahr verknüpft, in dem Donnerstag auftritt. Beispielsweise startet die Woche 1 im Jahr 2004 (2004W01) am 29. Dezember 2003 (Montag) und endet am 4. Januar 2004 (Sonntag). Die höchste Wochennummer kann in einem Jahr 52 oder 53 sein. Diese Art der Nummerierung wird in der Regel in europäischen Ländern bzw. Regionen verwendet. In anderen Ländern wird sie eher selten angewendet.
  
Das Nummerierungssystem in anderen Ländern oder Regionen entspricht möglicherweise nicht dem ISO-Standard. Es gibt mindestens sechs Möglichkeiten, wie in der folgenden Tabelle dargestellt.
  
|Erster Tag der Woche|Erste Woche im Jahr enthält|Doppelt zugewiesene Wochen|Verwendet von/in|  
|---|---|---|---|
|Sonntag|1. Januar<br /><br /> Erster Samstag<br /><br /> 1–7 Tage im Jahr|ja|United States|  
|Montag|1. Januar<br /><br /> Erster Sonntag<br /><br /> 1–7 Tage im Jahr|ja|Die meisten Länder Europas und das Vereinigte Königreich|  
|Montag|4. Januar<br /><br /> Erster Donnerstag<br /><br /> 4–7 Tage im Jahr|nein|ISO 8601, Norwegen und Schweden|  
|Montag|7. Januar,<br /><br /> Erster Montag<br /><br /> 7 Tage im Jahr|nein||  
|Mittwoch|1. Januar<br /><br /> Erster Dienstag<br /><br /> 1–7 Tage im Jahr|ja||  
|Samstag|1. Januar<br /><br /> Erster Freitag<br /><br /> 1–7 Tage im Jahr|ja||  
  
## <a name="tzoffset"></a>TZoffset  
Das Argument **TZoffset** (**tz**) wird als die Anzahl der Minuten (mit Vorzeichen) zurückgegeben. Die folgende Anweisung gibt ein Zeitzonenoffset von 310 Minuten zurück.
  
```sql
SELECT DATEPART (TZoffset, '2007-05-10  00:00:01.1234567 +05:10');  
```  
Der TZoffset wird wie folgt dargestellt:
- Für datetimeoffset und datetime2 gibt TZoffset den Zeitoffset in Minuten an, wobei der Offset für datetime2 immer 0 Minuten beträgt.
- Für Datentypen, die implizit in datetimeoffset oder datetime2 konvertiert werden können, wird mit Ausnahme der anderen date/time-Datentypen der Zeitoffset in Minuten zurückgegeben.
- Parameter aller anderen Typen führen zu einem Fehler.
  
  
## <a name="smalldatetime-date-argument"></a>date-Argument des Typs smalldatetime  
Wenn *date* vom Typ [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md) ist, werden Sekunden in der Form 00 zurückgegeben.
  
## <a name="default-returned-for-a-datepart-that-is-not-in-a-date-argument"></a>Zurückgeben des Standardwerts für ein datepart-Argument, das nicht in einem date-Argument enthalten ist  
Enthält der Datentyp des *date*-Arguments keine Angabe zu *datepart*, wird der Standardwert für *datepart* nur zurückgegeben, wenn für *date* ein Literal angegeben ist.
  
Beispielsweise wird bei Jahr-Monat-Tag für jeden **date**-Datentyp standardmäßig der Wert 1900-01-01 angegeben. Die folgende Anweisung verfügt über datepart-Argumente für *datepart*, ein time-Argument für *date* und gibt `1900, 1, 1, 1, 2` zurück.
  
```sql
SELECT DATEPART(year, '12:10:30.123')  
    ,DATEPART(month, '12:10:30.123')  
    ,DATEPART(day, '12:10:30.123')  
    ,DATEPART(dayofyear, '12:10:30.123')  
    ,DATEPART(weekday, '12:10:30.123');  
```  
  
Wenn *date* als Variable oder Tabellenspalte angegeben ist und der Datentyp für diese Variable oder Spalte nicht über das angegebene *datepart*-Argument verfügt, wird der Fehler 9810 zurückgegeben. Im folgenden Codebeispiel tritt ein Fehler auf, weil der year-Datumsteil für den für die *@t*-Variable deklarierten **time**-Datentyp nicht gültig ist.
  
```sql
DECLARE @t time = '12:10:30.123';   
SELECT DATEPART(year, @t);  
```  
  
## <a name="fractional-seconds"></a>Sekundenbruchteile
Die folgenden Anweisungen verdeutlichen, wie Sekundenbruchteile zurückgegeben werden:
  
```sql
SELECT DATEPART(millisecond, '00:00:01.1234567'); -- Returns 123  
SELECT DATEPART(microsecond, '00:00:01.1234567'); -- Returns 123456  
SELECT DATEPART(nanosecond,  '00:00:01.1234567'); -- Returns 123456700  
```  
  
## <a name="remarks"></a>Remarks  
DATEPART kann in den Klauseln WHERE, HAVING, GROUP BY und ORDER BY der SELECT-Liste verwendet werden.
  
In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] wandelt DATEPART Zeichenfolgenliterale implizit in den **datetime2**-Typ um. Daher unterstützt DATEPART das Format YDM nicht, wenn das Datum als Zeichenfolge übergeben wird. Sie müssen die Zeichenfolge explizit in den Typ **datetime** oder **smalldatetime** umwandeln, um das YDM-Format zu verwenden.
  
## <a name="examples"></a>Beispiele  
Das folgende Beispiel gibt das Basisjahr zurück. Das Basisjahr ist für Datumsberechnungen nützlich. Im Beispiel wird das Datum in Form einer Zahl angegeben. Beachten Sie, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] den Wert 0 als 1. Januar 1900 interpretiert.
  
```sql
SELECT DATEPART(year, 0), DATEPART(month, 0), DATEPART(day, 0);  
-- Returns: 1900    1    1 */  
```  
  
Im folgenden Beispiel wird der Tag des Datums `12/20/1974` zurückgegeben.
  
```sql
-- Uses AdventureWorks  
  
SELECT TOP(1) DATEPART (day,'12/20/1974') FROM dbo.DimCustomer;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
--------
20
```  
  
Im folgenden Beispiel wird das Jahr des Datums `12/20/1974` zurückgegeben.
  
```sql
-- Uses AdventureWorks  
  
SELECT TOP(1) DATEPART (year,'12/20/1974') FROM dbo.DimCustomer;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
--------
1974
```  
  
## <a name="see-also"></a>Siehe auch
[CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  

---
title: DATEPART (Transact-SQL) | Microsoft Docs
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
caps.latest.revision: 57
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 05547f2dd50d7f130438d6a07b6952b8c29ec816
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="datepart-transact-sql"></a>DATEPART (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Gibt eine ganze Zahl, die den angegebenen darstellt *Datepart* des angegebenen *Datum*.
  
Eine Übersicht über alle [!INCLUDE[tsql](../../includes/tsql-md.md)] Datums-und Uhrzeitdatentypen und Funktionen finden Sie unter [Datums- und Uhrzeitdatentypen und-Funktionen &#40; Transact-SQL &#41; ](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
DATEPART ( datepart , date )  
```  
  
## <a name="arguments"></a>Argumente  
*datepart*  
Ist der Teil des *Datum* (ein Wert für Datum oder Uhrzeit) für die ein **Ganzzahl** zurückgegeben werden. Die folgende Tabelle enthält alle gültigen *Datepart* Argumente. Benutzerdefinierte Variablenentsprechungen sind nicht gültig.
  
|*datepart*|Abkürzungen|  
|---|---|
|**Jahr**|**Yy**, **JJJJ**|  
|**Quartal**|**Qq**, **q**|  
|**Monat**|**mm**, **m**|  
|**DayOfYear**|**dy**, **y**|  
|**Tag**|**Dd**, **d**|  
|**Woche**|**wk**, **weltweit**|  
|**Wochentag**|**Data Warehouse**|  
|**Stunde**|**hh**|  
|**Minute**|**Mi, n**|  
|**Sekunde**|**ss**, **s**|  
|**Millisekunde**|**MS**|  
|**in Mikrosekunden**|**MCS**|  
|**Nanosekunden**|**Notification Services**|  
|**TZoffset**|**Tz**|  
|**ISO_WEEK**|**Isowk**, **Isoww**|  
  
*Datum*  
Ist ein Ausdruck, der in aufgelöst werden kann ein **Zeit**, **Datum**, **Smalldatetime**, **"DateTime"**, **datetime2**, oder **"DateTimeOffset"** Wert. *Datum* können einen Ausdruck, Spaltenausdruck, eine benutzerdefinierte Variable oder Zeichenfolge literal sein.  
Um Mehrdeutigkeiten zu vermeiden, sollten Sie vierstellige Jahreszahlen verwenden. Informationen zu zweistelligen Jahreszahlen finden Sie unter [konfigurieren two Digit Year cutoff Server Configuration Option](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md).
  
## <a name="return-type"></a>Rückgabetyp  
 **int**  
  
## <a name="return-value"></a>Rückgabewert  
Jede *Datepart* und zugehörigen Abkürzungen geben denselben Wert zurück.
  
Der Rückgabewert hängt von der sprachumgebung Festlegung mithilfe von [SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md) und durch die [Konfigurieren der Serverkonfigurationsoption Standardsprache](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md) der Anmeldung. Wenn *Datum* ist eine Zeichenfolge Zeichenfolgenliteral für einige Formate, der Rückgabewert hängt von dem mit angegebenen Format [SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md). SET DATEFORMAT wirkt sich nicht auf den Rückgabewert aus, wenn das Datum ein Spaltenausdruck für Daten vom Typ Datum oder Uhrzeit darstellt.
  
Die folgende Tabelle enthält alle *Datepart* -Argumente mit den entsprechenden Rückgabewerten für die Anweisung `SELECT DATEPART(datepart,'2007-10-30 12:15:32.1234567 +05:10')`. Der Datentyp der *Datum* Argument ist **datetimeoffset(7)**. Die **Nanosekunden***Datepart* -Rückgabewert verfügt über 9 Dezimalstellen (. 123456700) und die letzten beiden Stellen immer 00.
  
|*datepart*|Rückgabewert|  
|---|---|
|**Jahr, JJJJ, JJ**|2007|  
|**Quartal, Qq, q**|4|  
|**Monat, mm, m**|10|  
|**DayOfYear dy, y**|303|  
|**Day "," Dd "," d**|30|  
|**Woche "," wk "," ww-**|45|  
|**Wochentag, dw**|1|  
|**Stunde, "hh"**|12|  
|**Minute, n**|15|  
|**Sekunde "," ss "," s**|32|  
|**Millisekunden, ms**|123|  
|**in Mikrosekunden, die mcs**|123456|  
|**Nanosekunden, ns**|123456700|  
|**TZoffset tz**|310|  
  
## <a name="week-and-weekday-datepart-arguments"></a>Week und Weekday Datepart-Argumente
Wenn *Datepart* ist **Woche** (**wk**, **weltweit**) oder **Wochentag** (**dw**), der zurückgegebene Wert hängt vom Wert ab, der durch ist [SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md).
  
1. Januar eines Jahres definiert die Anfangszahl für die **Woche***Datepart*, z. B.: DATEPART (**wk**, ' Jan 1, *Xxx*X') = 1, in dem *Xxxx* beliebiges Jahr ist.
  
Die folgende Tabelle enthält den Rückgabewert für **Woche** und **Wochentag***Datepart* für "2007-04-21' für jedes SET DATEFIRST-Argument. Der 1. Januar ist im Jahr 2007 ein Montag. Der 21. April ist im Jahr 2007 ein Samstag. SET DATEFIRST 7, ist Sonntag, die Standardeinstellung für USA Englisch.
  
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
Die Werte, die für DatePart-Wert zurückgegeben werden (**Jahr**, *Datum*), DATEPART (**Monat**, *Datum*), "und" DATEPART (**Tag** , *Datum*) sind identisch mit denen von der Funktion zurückgegebenen [Jahr](../../t-sql/functions/year-transact-sql.md), [Monat](../../t-sql/functions/month-transact-sql.md), und [Tag](../../t-sql/functions/day-transact-sql.md), f bzw..
  
## <a name="isoweek-datepart"></a>ISO_WEEK datepart  
ISO 8601 schließt das ISO-Wochensystem zur Nummerierung von Wochen ein. Die einzelnen Wochen werden mit dem Jahr verknüpft, in dem Donnerstag auftritt. Beispielsweise startet die Woche 1 im Jahr 2004 (2004W01) am 29. Dezember 2003 (Montag) und endet am 4. Januar 2004 (Sonntag). Die höchste Wochennummer kann in einem Jahr 52 oder 53 sein. Diese Art der Nummerierung wird in der Regel in europäischen Ländern bzw. Regionen verwendet. In anderen Ländern wird sie eher selten angewendet.
  
Das Nummerierungssystem in anderen Ländern oder Regionen entspricht möglicherweise nicht dem ISO-Standard. Es gibt mindestens sechs Möglichkeiten, wie in der folgenden Tabelle dargestellt.
  
|Erster Tag der Woche|Erste Woche im Jahr enthält|Doppelt zugewiesene Wochen|Verwendet von/in|  
|---|---|---|---|
|Sonntag|1. Januar<br /><br /> Erster Samstag<br /><br /> 1–7 Tage im Jahr|ja|USA|  
|Montag|1. Januar<br /><br /> Erster Sonntag<br /><br /> 1–7 Tage im Jahr|ja|Die meisten Länder Europas und das Vereinigte Königreich|  
|Montag|4. Januar<br /><br /> Erster Donnerstag<br /><br /> 4 – 7 Tage im Jahr|Nein|ISO 8601, Norwegen und Schweden|  
|Montag|7 Januar<br /><br /> Erster Montag<br /><br /> 7 Tage im Jahr|Nein||  
|Mittwoch|1. Januar<br /><br /> Erster Dienstag<br /><br /> 1–7 Tage im Jahr|ja||  
|Samstag|1. Januar<br /><br /> Erster Freitag<br /><br /> 1–7 Tage im Jahr|ja||  
  
## <a name="tzoffset"></a>TZoffset  
Die **TZoffset** (**Tz**) wird als die Anzahl der Minuten (signiert) zurückgegeben. Die folgende Anweisung gibt ein Zeitzonenoffset von 310 Minuten zurück.
  
```sql
SELECT DATEPART (TZoffset, '2007-05-10  00:00:01.1234567 +05:10');  
```  
Der Wert des Typs TZoffset wird wie folgt gerendert:
- Für "DateTimeOffset" und datetime2 zurückgegeben, TZoffset die zeitverschiebung in Minuten an, ist der Offset für datetime2 immer 0 Minuten.
- Für Datentypen, die implizit in "DateTimeOffset" oder in datetime2, mit Ausnahme von der andere Datum/Uhrzeit-Datentypen konvertiert werden können wird die zeitverschiebung in Minuten zurückgegeben.
- Parameter für alle anderen Typen führen zu einem Fehler.
  
  
## <a name="smalldatetime-date-argument"></a>date-Argument des Typs smalldatetime  
Wenn *Datum* ist [Smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md), werden Sekunden als 00 zurückgegeben.
  
## <a name="default-returned-for-a-datepart-that-is-not-in-a-date-argument"></a>Zurückgeben des Standardwerts für ein datepart-Argument, das nicht in einem date-Argument enthalten ist  
Wenn der Datentyp der *Datum* Argument weist nicht auf den angegebenen *Datepart*, der Standardwert für diese *Datepart* zurückgegeben, wenn ein Literal für angegebenwird*Datum*.
  
Beispielsweise die Standardeinstellung Jahr-Monat-Tag für eine beliebige **Datum** -Datentyp ist 1900-01-01. Die folgende Anweisung verfügt über DatePart-Argumente für *Datepart*, ein Time-Argument für *Datum*, und gibt `1900, 1, 1, 1, 2`.
  
```sql
SELECT DATEPART(year, '12:10:30.123')  
    ,DATEPART(month, '12:10:30.123')  
    ,DATEPART(day, '12:10:30.123')  
    ,DATEPART(dayofyear, '12:10:30.123')  
    ,DATEPART(weekday, '12:10:30.123');  
```  
  
Wenn *Datum* wird angegeben, wie eine Variable oder Tabellenspalte und die Daten geben, dass Variablen oder Spalte nicht dem angegebenen *Datepart*, Fehler 9810 zurückgegeben. Im folgenden Codebeispiel wird ein Fehler auftritt, weil das Year-Datumsteil kein gültiger für ist die **Zeit** -Datentyp, der für die Variable deklariert wird  *@t* .
  
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
  
## <a name="remarks"></a>Hinweise  
DATEPART kann in den Klauseln WHERE, HAVING, GROUP BY und ORDER BY der SELECT-Liste verwendet werden.
  
In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], wandelt DATEPART Zeichenfolgenliterale als implizit eine **datetime2** Typ. Daher unterstützt DATEPART das Format YDM nicht, wenn das Datum als Zeichenfolge übergeben wird. Sie müssen die Zeichenfolge, die explizit Umwandeln einer **"DateTime"** oder **Smalldatetime** Typ das YDM-Format verwendet.
  
## <a name="examples"></a>Beispiele  
Das folgende Beispiel gibt das Basisjahr zurück. Das Basisjahr ist für Datumsberechnungen nützlich. Im Beispiel wird das Datum in Form einer Zahl angegeben. Beachten Sie, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] den Wert 0 als 1. Januar 1900 interpretiert.
  
```sql
SELECT DATEPART(year, 0), DATEPART(month, 0), DATEPART(day, 0);  
-- Returns: 1900    1    1 */  
```  
  
Das folgende Beispiel gibt die Tagesangabe des Datums `12/20/1974`.
  
```sql
-- Uses AdventureWorks  
  
SELECT TOP(1) DATEPART (day,'12/20/1974') FROM dbo.DimCustomer;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
--------
20
```  
  
Das folgende Beispiel gibt den Jahresteil des Datums `12/20/1974`.
  
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
  
  


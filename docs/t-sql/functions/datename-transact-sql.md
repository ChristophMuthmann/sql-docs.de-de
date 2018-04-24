---
title: DATENAME (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DATENAME_TSQL
- DATENAME
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- DATENAME function [SQL Server
- functions [SQL Server], time
- functions [SQL Server], date and time
- dateparts [SQL Server], datename
- date and time [SQL Server], DATENAME
- comparing dates times [SQL Server]
- dates [SQL Server], dateparts
ms.assetid: 11855b56-c554-495d-aad4-ba446990153b
caps.latest.revision: 59
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: a8803278c567f01888b7b530885e82e4543c966a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="datename-transact-sql"></a>DATENAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Gibt eine Zeichenfolge zurück, die den angegebenen *datepart*-Wert des angegebenen *Datums* darstellt.
  
Eine Übersicht über alle Datums- und Uhrzeitdatentypen und zugehörige Funktionen für [!INCLUDE[tsql](../../includes/tsql-md.md)] finden Sie unter [Date and Time Data Types and Functions &#40;Transact-SQL&#41; (Datums- und Uhrzeitdatentypen und zugehörige Funktionen)](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
DATENAME ( datepart , date )  
```  
  
## <a name="arguments"></a>Argumente  
*datepart*  
Ist der Teil von *date*, der zurückgegeben werden soll. In der folgenden Tabelle werden alle gültigen *datepart*-Argumente aufgeführt. Benutzerdefinierte Variablenentsprechungen sind nicht gültig.
  
|*datepart*|Abkürzungen|  
|---|---|
|**year**|**yy, yyyy**|  
|**quarter**|**qq, q**|  
|**month**|**mm, m**|  
|**dayofyear**|**dy, y**|  
|**day**|**dd, d**|  
|**week**|**wk, ww**|  
|**weekday**|**dw, w**|  
|**hour**|**hh**|  
|**minute**|**mi, n**|  
|**second**|**ss, s**|  
|**millisecond**|**ms**|  
|**microsecond**|**mcs**|  
|**nanosecond**|**ns**|  
|**TZoffset**|**tz**|  
|**ISO_WEEK**|**ISOWK, ISOWW**|  
  
*Datum*  
Ein Ausdruck, der in einen der folgenden Werte aufgelöst werden kann: **time**, **date**, **smalldatetime**, **datetime**, **datetime2** oder **datetimeoffset**. *date* kann ein Ausdruck, ein Spaltenausdruck, eine benutzerdefinierte Variable oder ein Zeichenfolgenliteral sein.  
Um Mehrdeutigkeiten zu vermeiden, sollten Sie vierstellige Jahreszahlen verwenden. Informationen zu zweistelligen Jahreszahlen finden Sie unter [Konfigurieren der Serverkonfigurationsoption „Umstellungsjahr für Angaben mit zwei Ziffern“](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md).
  
## <a name="return-type"></a>Rückgabetyp  
**nvarchar**
  
## <a name="return-value"></a>Rückgabewert  
  
-   Jedes *datepart*-Argument und die zugehörigen Abkürzungen geben den gleichen Wert zurück.  
  
Der Rückgabewert hängt von der Sprachumgebung ab, die durch [SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md) und durch die [Konfiguration der Serverkonfigurationsoption „Standardsprache“](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md) für die Anmeldung festgelegt wurde. Der Rückgabewert hängt von der Option [SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md) ab, wenn *date* ein Zeichenfolgenliteral einiger Formate darstellt. SET DATEFORMAT wirkt sich nicht auf den Rückgabewert aus, wenn das Datum ein Spaltenausdruck für Daten vom Typ Datum oder Uhrzeit darstellt.
  
Wenn der *date*-Parameter ein **date**-Datentypargument aufweist, hängt der Rückgabewert von der Einstellung ab, die mit [SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md) angegeben wurde.
  
## <a name="tzoffset-datepart-argument"></a>datepart-Argumentdes Typs TZoffset  
Wenn das *datepart*-Argument **TZoffset** (**tz**) lautet und das *date*-Argument über keinen Zeitzonenoffset verfügt, wird 0 zurückgegeben.
  
## <a name="smalldatetime-date-argument"></a>date-Argument des Typs smalldatetime  
Wenn *date* vom Typ [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md) ist, werden Sekunden in der Form 00 zurückgegeben.
  
## <a name="default-returned-for-a-datepart-that-is-not-in-the-date-argument"></a>Zurückgeben des Standardwerts für ein datepart-Argument, das nicht im date-Argument enthalten ist  
Enthält der Datentyp des *date*-Arguments keine Angabe zu *datepart*, wird der Standardwert für *datepart* nur zurückgegeben, wenn für *date* ein Literal angegeben ist.
  
Beispielsweise wird bei Jahr-Monat-Tag für jeden **date**-Datentyp standardmäßig der Wert 1900-01-01 angegeben. Die folgende Anweisung verfügt über datepart-Argumente für *datepart*, ein time-Argument für *date* und gibt `1900, January, 1, 1, Monday` zurück.
  
```sql
SELECT DATENAME(year, '12:10:30.123')  
    ,DATENAME(month, '12:10:30.123')  
    ,DATENAME(day, '12:10:30.123')  
    ,DATENAME(dayofyear, '12:10:30.123')  
    ,DATENAME(weekday, '12:10:30.123');  
```  
  
Wenn *date* als Variable oder Tabellenspalte angegeben ist und der Datentyp für diese Variable oder Spalte nicht über das angegebene *datepart*-Argument verfügt, wird der Fehler 9810 zurückgegeben. Im folgenden Codebeispiel tritt ein Fehler auf, weil der year-Datumsteil für den für die *@t*-Variable deklarierten **time**-Datentyp nicht gültig ist.
  
```sql
DECLARE @t time = '12:10:30.123';   
SELECT DATENAME(year, @t);  
```  
  
## <a name="remarks"></a>Remarks  
DATENAME kann in den Klauseln WHERE, HAVING, GROUP BY und ORDER BY der SELECT-Liste verwendet werden.
  
In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] wandelt DATENAME Zeichenfolgenliterale implizit in den **datetime2**-Typ um. Daher unterstützt DATENAME das Format YDM nicht, wenn das Datum als Zeichenfolge übergeben wird. Sie müssen die Zeichenfolge explizit in den Typ **datetime** oder **smalldatetime** umwandeln, um das YDM-Format zu verwenden.
  
## <a name="examples"></a>Beispiele  
Im folgenden Beispiel werden die Datumsteile für das angegebene Datum zurückgegeben.
  
`SELECT DATENAME(datepart,'2007-10-30 12:15:32.1234567 +05:10');`
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
|*datepart*|Rückgabewert|  
|---|---|
|**year, yyyy, yy**|2007|  
|**quarter, qq, q**|4|  
|**month, mm, m**|October|  
|**dayofyear, dy, y**|303|  
|**day, dd, d**|30|  
|**week, wk, ww**|44|  
|**weekday, dw**|Dienstag|  
|**hour, hh**|12|  
|**minute, n**|15|  
|**second, ss, s**|32|  
|**millisecond, ms**|123|  
|**microsecond, mcs**|123456|  
|**nanosecond, ns**|123456700|  
|**TZoffset, tz**|310|  
|**ISO_WEEK, ISOWK, ISOWW**|44|  
  
[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

Im folgenden Beispiel werden die Datumsteile für das angegebene Datum zurückgegeben.
  
```sql
SELECT DATENAME(datepart,'2007-10-30 12:15:32.1234567 +05:10');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
|*datepart*|Rückgabewert|  
|---|---|
|**year, yyyy, yy**|2007|  
|**quarter, qq, q**|4|  
|**month, mm, m**|October|  
|**dayofyear, dy, y**|303|  
|**day, dd, d**|30|  
|**week, wk, ww**|44|  
|**weekday, dw**|Dienstag|  
|**hour, hh**|12|  
|**minute, n**|15|  
|**second, ss, s**|32|  
|**millisecond, ms**|123|  
|**microsecond, mcs**|123456|  
|**nanosecond, ns**|123456700|  
|**TZoffset, tz**|310|  
|**ISO_WEEK, ISOWK, ISOWW**|44|  
  
## <a name="see-also"></a>Siehe auch
[CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  


---
title: DATENAME (Transact-SQL) | Microsoft Docs
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 22dc10851e3185512527f82f593fdc2cdb2b765f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="datename-transact-sql"></a>DATENAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Gibt eine Zeichenfolge, die den angegebenen darstellt *Datepart* des angegebenen *Datum*
  
Eine Übersicht über alle [!INCLUDE[tsql](../../includes/tsql-md.md)] Datums-und Uhrzeitdatentypen und Funktionen finden Sie unter [Datums- und Uhrzeitdatentypen und-Funktionen &#40; Transact-SQL &#41; ](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
DATENAME ( datepart , date )  
```  
  
## <a name="arguments"></a>Argumente  
*datepart*  
Ist der Teil der *Datum* zurückgegeben. Die folgende Tabelle enthält alle gültigen *Datepart* Argumente. Benutzerdefinierte Variablenentsprechungen sind nicht gültig.
  
|*datepart*|Abkürzungen|  
|---|---|
|**Jahr**|**Yy, yyyy**|  
|**Quartal**|**Qq, q**|  
|**Monat**|**mm, m**|  
|**DayOfYear**|**dy, y**|  
|**Tag**|**tt, d**|  
|**Woche**|**wk weltweit**|  
|**Wochentag**|**DW, w**|  
|**Stunde**|**hh**|  
|**Minute**|**Mi, n**|  
|**Sekunde**|**ss, s**|  
|**Millisekunde**|**MS**|  
|**in Mikrosekunden**|**MCS**|  
|**Nanosekunden**|**Notification Services**|  
|**TZoffset**|**Tz**|  
|**ISO_WEEK**|**ISOWK ISOWW**|  
  
*Datum*  
Ist ein Ausdruck, der in aufgelöst werden kann ein **Zeit**, **Datum**, **Smalldatetime**, **"DateTime"**, **datetime2**, oder **"DateTimeOffset"** Wert. *Datum* können einen Ausdruck, Spaltenausdruck, eine benutzerdefinierte Variable oder Zeichenfolge literal sein.  
Um Mehrdeutigkeiten zu vermeiden, sollten Sie vierstellige Jahreszahlen verwenden. Informationen zu zweistelligen Jahresangaben, finden Sie unter [konfigurieren two Digit Year cutoff Server Configuration Option](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md).
  
## <a name="return-type"></a>Rückgabetyp  
**nvarchar**
  
## <a name="return-value"></a>Rückgabewert  
  
-   Jede *Datepart* und zugehörigen Abkürzungen geben denselben Wert zurück.  
  
Der Rückgabewert hängt von der sprachumgebung Festlegung mithilfe von [SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md) und durch die [Konfigurieren der Serverkonfigurationsoption Standardsprache](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md) der Anmeldung. Der Rückgabewert ist abhängigen auf [SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md) Wenn *Datum* ist eine Zeichenfolge Zeichenfolgenliteral einiger Formate. SET DATEFORMAT wirkt sich nicht auf den Rückgabewert aus, wenn das Datum ein Spaltenausdruck für Daten vom Typ Datum oder Uhrzeit darstellt.
  
Wenn die *Datum* Parameter hat eine **Datum** datentypargument, der Rückgabewert hängt von der Einstellung, die mithilfe von angegeben [SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md).
  
## <a name="tzoffset-datepart-argument"></a>datepart-Argumentdes Typs TZoffset  
Wenn *Datepart* Argument ist **TZoffset** (**Tz**) und die *Datum* Argument über keinen Zeitzonenoffset verfügt, wird 0 zurückgegeben.
  
## <a name="smalldatetime-date-argument"></a>date-Argument des Typs smalldatetime  
Wenn *Datum* ist [Smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md), werden Sekunden als 00 zurückgegeben.
  
## <a name="default-returned-for-a-datepart-that-is-not-in-the-date-argument"></a>Zurückgeben des Standardwerts für ein datepart-Argument, das nicht im date-Argument enthalten ist  
Wenn der Datentyp der *Datum* Argument weist nicht auf den angegebenen *Datepart*, der Standardwert für diese *Datepart* zurückgegeben, wenn ein Literal für angegebenwird*Datum*.
  
Beispielsweise die Standardeinstellung Jahr-Monat-Tag für eine beliebige **Datum** -Datentyp ist 1900-01-01. Die folgende Anweisung verfügt über DatePart-Argumente für *Datepart*, ein Time-Argument für *Datum*, und gibt `1900, January, 1, 1, Monday`.
  
```sql
SELECT DATENAME(year, '12:10:30.123')  
    ,DATENAME(month, '12:10:30.123')  
    ,DATENAME(day, '12:10:30.123')  
    ,DATENAME(dayofyear, '12:10:30.123')  
    ,DATENAME(weekday, '12:10:30.123');  
```  
  
Wenn *Datum* wird angegeben, wie eine Variable oder Tabellenspalte und die Daten geben, dass Variablen oder Spalte nicht dem angegebenen *Datepart*, Fehler 9810 zurückgegeben. Im folgenden Codebeispiel wird ein Fehler auftritt, weil das Year-Datumsteil kein gültiger für ist die **Zeit** -Datentyp, der für die Variable deklariert wird  *@t* .
  
```sql
DECLARE @t time = '12:10:30.123';   
SELECT DATENAME(year, @t);  
```  
  
## <a name="remarks"></a>Hinweise  
DATENAME kann in den Klauseln WHERE, HAVING, GROUP BY und ORDER BY der SELECT-Liste verwendet werden.
  
In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], DATENAME wandelt Zeichenfolgenliterale als implizit eine **datetime2** Typ. Daher unterstützt DATENAME das Format YDM nicht, wenn das Datum als Zeichenfolge übergeben wird. Sie müssen die Zeichenfolge, die explizit Umwandeln einer **"DateTime"** oder **Smalldatetime** Typ das YDM-Format verwendet.
  
## <a name="examples"></a>Beispiele  
Im folgenden Beispiel werden die Datumsteile für das angegebene Datum zurückgegeben.
  
`SELECT DATENAME(datepart,'2007-10-30 12:15:32.1234567 +05:10');`
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
|*datepart*|Rückgabewert|  
|---|---|
|**Jahr, JJJJ, JJ**|2007|  
|**Quartal, Qq, q**|4|  
|**Monat, mm, m**|October|  
|**DayOfYear dy, y**|303|  
|**Day "," Dd "," d**|30|  
|**Woche "," wk "," ww-**|44|  
|**Wochentag, dw**|Dienstag|  
|**Stunde, "hh"**|12|  
|**Minute, n**|15|  
|**Sekunde "," ss "," s**|32|  
|**Millisekunden, ms**|123|  
|**in Mikrosekunden, die mcs**|123456|  
|**Nanosekunden, ns**|123456700|  
|**TZoffset tz**|310|  
|**ISO_WEEK ISOWK, ISOWW**|44|  
  
[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

Im folgenden Beispiel werden die Datumsteile für das angegebene Datum zurückgegeben.
  
```sql
SELECT DATENAME(datepart,'2007-10-30 12:15:32.1234567 +05:10');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
|*datepart*|Rückgabewert|  
|---|---|
|**Jahr, JJJJ, JJ**|2007|  
|**Quartal, Qq, q**|4|  
|**Monat, mm, m**|October|  
|**DayOfYear dy, y**|303|  
|**Day "," Dd "," d**|30|  
|**Woche "," wk "," ww-**|44|  
|**Wochentag, dw**|Dienstag|  
|**Stunde, "hh"**|12|  
|**Minute, n**|15|  
|**Sekunde "," ss "," s**|32|  
|**Millisekunden, ms**|123|  
|**in Mikrosekunden, die mcs**|123456|  
|**Nanosekunden, ns**|123456700|  
|**TZoffset tz**|310|  
|**ISO_WEEK ISOWK, ISOWW**|44|  
  
## <a name="see-also"></a>Siehe auch
[CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  


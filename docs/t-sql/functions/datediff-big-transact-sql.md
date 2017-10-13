---
title: DATEDIFF_BIG (Transact-SQL) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
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
caps.latest.revision: 7
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 80c1228faeaaa4012afc0fd27992a2f5cf389f6e
ms.openlocfilehash: 08f27953aac5fa36f1b38e243d8465f57458dafe
ms.contentlocale: de-de
ms.lasthandoff: 10/12/2017

---
# <a name="datediffbig-transact-sql"></a>DATEDIFF_BIG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Gibt die Anzahl (große ganze Zahl mit Vorzeichen) der angegebenen *Datepart* Grenzen überschritten, zwischen dem angegebenen *"StartDate"* und *Enddate*.
  
Eine Übersicht über alle [!INCLUDE[tsql](../../includes/tsql-md.md)] Datums-und Uhrzeitdatentypen und Funktionen finden Sie unter [Datums- und Uhrzeitdatentypen und-Funktionen &#40; Transact-SQL &#41; ](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
  
DATEDIFF_BIG ( datepart , startdate , enddate )  
```  
  
## <a name="arguments"></a>Argumente  
*datepart*  
Ist der Teil des *"StartDate"* und *Enddate* , die den Typ der überschrittenen Begrenzung angibt. Die folgende Tabelle enthält alle gültigen *Datepart* Argumente. Benutzerdefinierte Variablenentsprechungen sind nicht gültig.
  
|*datepart*|Abkürzungen|  
|---|---|
|**Jahr**|**Yy, yyyy**|  
|**Quartal**|**Qq, q**|  
|**Monat**|**mm, m**|  
|**DayOfYear**|**dy, y**|  
|**Tag**|**tt, d**|  
|**Woche**|**wk weltweit**|  
|**Stunde**|**hh**|  
|**Minute**|**Mi, n**|  
|**Sekunde**|**ss, s**|  
|**Millisekunde**|**MS**|  
|**in Mikrosekunden**|**MCS**|  
|**Nanosekunden**|**Notification Services**|  
  
*startdate*  
Ist ein Ausdruck, der in aufgelöst werden kann ein **Zeit**, **Datum**, **Smalldatetime**, **"DateTime"**, **datetime2**, oder **"DateTimeOffset"** Wert. *Datum* kann ein Ausdruck, Spaltenausdruck, eine benutzerdefinierte Variable oder Zeichenfolge literal. *"StartDate"* abgezogen *Enddate*.  
Um Mehrdeutigkeiten zu vermeiden, sollten Sie vierstellige Jahreszahlen verwenden. Informationen zu zweistelligen Jahreszahlen finden Sie unter [konfigurieren two Digit Year cutoff Server Configuration Option](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md).
  
*EndDate*  
Finden Sie unter *"StartDate"*.
  
## <a name="return-type"></a>Rückgabetyp  
 Signiert   
        **bigint**  
  
## <a name="return-value"></a>Rückgabewert  
Gibt die Anzahl (mit Vorzeichen "bigint") der angegebenen Datepart-Begrenzungen gekreuzt zwischen den angegebenen Startdate und EndDate zurück.
-   Jede *Datepart* und zugehörigen Abkürzungen geben denselben Wert zurück.  
  
Wenn der Rückgabewert außerhalb des gültigen Bereichs für **"bigint"** (-9.223.372.036.854.775.808 bis 9.223.372.036.854.775.807), wird ein Fehler zurückgegeben. Für **Millisekunde**, der maximale Unterschied zwischen *"StartDate"* und *Enddate* beträgt 24 Tage, 20 Stunden, 31 Minuten und 23,647 Sekunden. Für **zweite**, der maximale Unterschied 68 Jahre liegt.
  
Wenn *"StartDate"* und *Enddate* sowohl nur einen Uhrzeitwert zugeordnet werden und die *Datepart* ist nicht *Datepart*, wird 0 zurückgegeben.
  
Ein Zeitzonenoffset Komponente des *"StartDate"* oder *Endate* wird bei der Berechnung des Rückgabewerts nicht verwendet.
  
Da [Smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md) wird nur auf die Minute, wenn eine **Smalldatetime** Wert wird zum *"StartDate"* oder *Enddate*, Sekunden und Millisekunden immer in der zurückgegebene Wert auf 0 festgelegt sind.
  
Wenn zu einer Variablen eines Datumsdatentyps nur ein Uhrzeitwert zugeordnet wird, wird für den Wert des fehlenden Datumsteils der Standardwert festgelegt: 1900-01-01. Wenn zu einer Variablen eines Uhrzeit- oder Datumsdatentyps nur ein Datumswert zugeordnet wird, wird für den Wert des fehlenden Uhrzeitteils der Standardwert festgelegt: 00-00-00. Wenn entweder *"StartDate"* oder *Enddate* haben nur einen Uhrzeitteil und der andere nur einen Date-Teil, die fehlenden Uhrzeit- und Datumsteile werden auf die Standardwerte festgelegt.
  
Wenn *"StartDate"* und *Enddate* sind von anderen Date-Datentypen und eine mehr Uhrzeitteile oder die Genauigkeit der Sekundenbruchteile als das andere ist, werden die fehlenden Teile des anderen auf 0 festgelegt.
  
## <a name="datepart-boundaries"></a>DatePart-Begrenzungen
Die folgenden Anweisungen verfügen über denselben *"StartDate"* und demselben *Endate*. Die Datumsangaben folgen aufeinander und unterscheiden sich in der Uhrzeit um 0,0000001 Sekunden. Der Unterschied zwischen der *"StartDate"* und *Endate* in jeder Anweisung überschreitet eine Kalender- oder uhrzeitbegrenzung des seine *Datepart*. Jede Anweisung gibt 1 zurück. Wenn für dieses Beispiel unterschiedliche Jahre verwendet werden, und wenn die beiden *"StartDate"* und *Endate* befinden sich in derselben Kalenderwoche, der Rückgabewert für **Woche** würde "0" sein.

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
  
## <a name="remarks"></a>Hinweise  
DATEDIFF_BIG kann verwendet werden, in der Auswahlliste BY und ORDER BY-Klauseln WHERE, HAVING, GROUP können.
  
DATEDIFF_BIG wandelt Zeichenfolgenliterale als implizit eine **datetime2** Typ. Dies bedeutet, dass DATEDIFF_BIG das Format YDM nicht unterstützt, wenn das Datum als Zeichenfolge übergeben wird. Sie müssen die Zeichenfolge, die explizit Umwandeln einer **"DateTime"** oder **Smalldatetime** Typ das YDM-Format verwendet.
  
Angeben von SET DATEFIRST hat keine Auswirkungen auf DATEDIFF_BIG. DATEDIFF_BIG verwendet immer Sonntag als erster Tag der Woche, um sicherzustellen, dass die Funktion deterministisch ist.
  
## <a name="examples"></a>Beispiele  
In den folgenden Beispielen wird mit verschiedenen Arten von Ausdrücken als Argumente für die *"StartDate"* und *Enddate* Parameter.
  
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
  
Viele weitere Beispiele finden Sie unter den eng verwandten Beispielen in [DATEDIFF &#40; Transact-SQL &#41; ](../../t-sql/functions/datediff-transact-sql.md).
  
## <a name="see-also"></a>Siehe auch
[CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[DATEDIFF &#40; Transact-SQL &#41;](../../t-sql/functions/datediff-transact-sql.md)
  
  


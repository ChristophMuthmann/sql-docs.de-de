---
title: ODBC-Skalarfunktionen (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
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
dev_langs:
- TSQL
helpviewer_keywords:
- CURDATE ODBC function
- DAYOFMONTH ODBC function
- WEEK ODBC function
- functions, ODBC CONCAT
- SECOND ODBC function
- functions, ODBC CURRENT_TIME
- functions, ODBC HOUR
- functions, ODBC QUARTER
- TRUNCATE ODBC function
- functions, ODBC SECOND
- DAYOFWEEK ODBC function
- CURRENT_DATE ODBC function
- DAYNAME ODBC function
- CURTIME ODBC function
- functions, ODBC CURRENT_DATE
- MINUTE ODBC function
- functions, ODBC BIT_LENGTH
- functions, ODBC OCTET_LENGTH
- CONCAT ODBC function
- MONTHNAME ODBC function
- functions, ODBC DAYOFYEAR
- OCTET_LENGTH ODBC function
- functions [SQL Server], ODBC scalar functions
- BIT_LENGTH ODBC function
- functions, ODBC DAYOFMONTH
- CURRENT_TIME ODBC function
- functions, ODBC CURDATE
- functions, ODBC CURTIME
- functions, ODBC TRUNCATE
- functions, ODBC MONTHNAME
- functions, ODBC DAYNAME
- ODBC scalar functions
- functions, ODBC MINUTE
- functions, ODBC DAYOFWEEK
- QUARTER ODBC function
- DAYOFYEAR ODBC function
- functions, ODBC WEEK
- HOUR ODBC function
ms.assetid: a0df1ac2-6699-4ac0-8f79-f362f23496f1
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b248e52c25e3c4a7cdbb0e52b1df50623e048189
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="odbc-scalar-functions-transact-sql"></a>ODBC-Skalarfunktionen (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Sie können [ODBC-Skalarfunktionen](http://go.microsoft.com/fwlink/?LinkID=88579) in [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisungen. Diese Anweisungen werden von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interpretiert. Sie können in gespeicherten Prozeduren und benutzerdefinierten Funktionen verwendet werden. Hierzu zählen Zeichenfolgen-, Uhrzeit-, Datums-, Intervall- und Systemfunktionen sowie numerische Funktionen.  
  
## <a name="usage"></a>Verwendung  
 `SELECT {fn <function_name> [ (<argument>,....n) ] }`  
  
## <a name="functions"></a>Funktionen  
 In den folgenden Tabellen sind ODBC-Skalarfunktionen aufgelistet, die nicht in [!INCLUDE[tsql](../../includes/tsql-md.md)] dupliziert werden.  
  
### <a name="string-functions"></a>Zeichenfolgenfunktionen  
  
|Funktion|Description|  
|--------------|-----------------|  
|BIT_LENGTH( string_exp ) (ODBC 3.0)|Gibt die Länge des Zeichenfolgenausdrucks in Bits zurück.<br /><br /> Kann nicht nur für string-Datentypen verwendet werden. Konvertiert daher string_exp nicht implizit in eine Zeichenfolge, sondern gibt die (interne) Größe des jeweiligen angegebenen Datentyps zurück.|  
|CONCAT( string_exp1,string_exp2) (ODBC 1.0)|Gibt eine Zeichenfolge zurück, die das Ergebnis der Verkettung von string_exp2 und string_exp1 darstellt. Die Ergebniszeichenfolge hängt vom DBMS ab. Wenn die durch string_exp1 dargestellte Spalte z. B. einen NULL-Wert enthält, wird DB2 NULL zurückgeben. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hingegen gibt eine Zeichenfolge ungleich NULL zurückgeben.|  
|OCTET_LENGTH( string_exp ) (ODBC 3.0)|Gibt die Länge des Zeichenfolgenausdrucks in Bytes zurück. Das Ergebnis ist die kleinste ganze Zahl, die nicht kleiner ist als die Anzahl der Bits dividiert durch 8.<br /><br /> Kann nicht nur für string-Datentypen verwendet werden. Konvertiert daher string_exp nicht implizit in eine Zeichenfolge, sondern gibt die (interne) Größe des jeweiligen angegebenen Datentyps zurück.|  
  
### <a name="numeric-function"></a>Numerische Funktion  
  
|Funktion|Description|  
|--------------|-----------------|  
|TRUNCATE( numeric_exp, integer_exp) (ODBC 2.0)|Gibt numeric_exp abgeschnitten auf integer_exp-Positionen rechts vom Dezimaltrennzeichen zurück. Wenn Integer_exp negativ ist, wird Numeric_exp abgeschnitten auf &#124; Integer_exp &#124; Positionen links vom Dezimaltrennzeichen an.|  
  
### <a name="time-date-and-interval-functions"></a>Uhrzeit-, Datums- und Intervallfunktionen  
  
|Funktion|Description|  
|--------------|-----------------|  
|CURRENT_DATE( ) (ODBC 3.0)|Gibt das aktuelle Datum zurück.|  
|CURDATE( ) (ODBC 3.0)|Gibt das aktuelle Datum zurück.|  
|AKTUELLE_ZEIT`[( time-precision )]` (ODBC 3.0)|Gibt die aktuelle lokale Zeit zurück. Das time-precision-Argument bestimmt die Genauigkeit des zurückgegebenen Werts bezüglich der Sekundenangaben.|  
|CURTIME() (ODBC 3.0)|Gibt die aktuelle lokale Zeit zurück.|  
|DAYNAME( date_exp ) (ODBC 2.0)|Gibt eine Zeichenfolge zurück, die den für die Datenquelle spezifischen Namen des Tages (z. B. Sonntag bis Samstag oder So. bis Sa. bei einer Datenquelle, die Deutsch verwendet, oder Sunday bis Saturday bei einer Datenquelle, die Englisch verwendet) für den Tagesteil von date_exp enthält.|  
|DAYOFMONTH( date_exp ) (ODBC 1.0)|Gibt den Tag des Monats basierend auf dem Monatsfeld in date_exp als ganze Zahl im Bereich von 1 bis 31 zurück.|  
|DAYOFWEEK( date_exp ) (ODBC 1.0)|Gibt den Wochentag basierend auf dem Wochenfeld in "date_exp" als ganze Zahl im Bereich von 1 bis 7 zurück, wobei 1 den Sonntag darstellt.|  
|HOUR( time_exp ) (ODBC 1.0)|Gibt die Stunde basierend auf dem Stundenfeld in "time_exp" als ganze Zahl im Bereich von 0 bis 23 zurück.|  
|MINUTE( time_exp ) (ODBC 1.0)|Gibt die Minute basierend auf dem Minutenfeld in "time_exp" als ganze Zahl im Bereich von 0 bis 59 zurück.|  
|SECOND( time_exp ) (ODBC 1.0)|Gibt die Sekunde basierend auf dem Sekundenfeld in "time_exp" als ganze Zahl im Bereich von 0 bis 59 zurück.|  
|MONTHNAME( date_exp ) (ODBC 2.0)|Gibt eine Zeichenfolge zurück, die den für die Datenquelle spezifischen Namen des Monats (z. B. January bis December bzw. Jan. bis Dec. für eine Datenquelle in englischer Sprache oder Januar bis Dezember für eine Datenquelle in deutscher Sprache) für den Monatsteil von "date_exp" enthält.|  
|QUARTER( date_exp ) (ODBC 1.0)|Gibt das Quartal in date_exp als ganze Zahl im Bereich von 1 bis 4 zurück, wobei 1 den Zeitraum vom 1. Januar bis 31. März darstellt.|  
|WEEK( date_exp ) (ODBC 1.0)|Gibt die Woche des Jahres basierend auf dem Wochenfeld in "date_exp" als ganze Zahl im Bereich von 1 bis 53 zurück.|  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-an-odbc-function-in-a-stored-procedure"></a>A. Verwenden einer ODBC-Funktion in einer gespeicherten Prozedur  
 Im folgenden Beispiel wird eine ODBC-Funktion in einer gespeicherten Prozedur verwendet:  
  
```  
CREATE PROCEDURE dbo.ODBCprocedure  
    (  
    @string_exp nvarchar(4000)  
    )  
AS  
SELECT {fn OCTET_LENGTH( @string_exp )};  
```  
  
### <a name="b-using-an-odbc-function-in-a-user-defined-function"></a>B. Verwenden einer ODBC-Funktion in einer benutzerdefinierten Funktion  
 Im folgenden Beispiel wird eine ODBC-Funktion in einer benutzerdefinierten Funktion verwendet:  
  
```  
CREATE FUNCTION dbo.ODBCudf  
    (  
    @string_exp nvarchar(4000)  
    )  
RETURNS int  
AS  
BEGIN  
DECLARE @len int  
SET @len = (SELECT {fn OCTET_LENGTH( @string_exp )})  
RETURN(@len)  
END ;  
  
SELECT dbo.ODBCudf('Returns the length.');  
--Returns 38  
  
```  
  
### <a name="c-using-an-odbc-functions-in-select-statements"></a>C. Verwenden von ODBC-Funktionen in SELECT-Anweisungen  
 In den folgenden SELECT-Anweisungen werden ODBC-Funktionen verwendet:  
  
```  
DECLARE @string_exp nvarchar(4000) = 'Returns the length.';  
SELECT {fn BIT_LENGTH( @string_exp )};  
-- Returns 304  
SELECT {fn OCTET_LENGTH( @string_exp )};  
-- Returns 38  
  
SELECT {fn CONCAT( 'CONCAT ','returns a character string')};  
-- Returns CONCAT returns a character string  
SELECT {fn TRUNCATE( 100.123456, 4)};  
-- Returns 100.123400  
SELECT {fn CURRENT_DATE( )};  
-- Returns 2007-04-20  
SELECT {fn CURRENT_TIME(6)};  
-- Returns 10:27:11.973000  
  
DECLARE @date_exp nvarchar(30) = '2007-04-21 01:01:01.1234567';  
SELECT {fn DAYNAME( @date_exp )};  
-- Returns Saturday  
SELECT {fn DAYOFMONTH( @date_exp )};  
-- Returns 21  
SELECT {fn DAYOFWEEK( @date_exp )};  
-- Returns 7  
SELECT {fn HOUR( @date_exp)};  
-- Returns 1   
SELECT {fn MINUTE( @date_exp )};  
-- Returns 1  
SELECT {fn SECOND( @date_exp )};  
-- Returns 1  
SELECT {fn MONTHNAME( @date_exp )};  
-- Returns April  
SELECT {fn QUARTER( @date_exp )};  
-- Returns 2  
SELECT {fn WEEK( @date_exp )};  
-- Returns 16  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-using-an-odbc-function-in-a-stored-procedure"></a>D. Verwenden einer ODBC-Funktion in einer gespeicherten Prozedur  
 Im folgenden Beispiel wird eine ODBC-Funktion in einer gespeicherten Prozedur verwendet:  
  
```  
CREATE PROCEDURE dbo.ODBCprocedure  
    (  
    @string_exp nvarchar(4000)  
    )  
AS  
SELECT {fn BIT_LENGTH( @string_exp )};  
```  
  
### <a name="e-using-an-odbc-function-in-a-user-defined-function"></a>E. Verwenden einer ODBC-Funktion in einer benutzerdefinierten Funktion  
 Im folgenden Beispiel wird eine ODBC-Funktion in einer benutzerdefinierten Funktion verwendet:  
  
```  
CREATE FUNCTION dbo.ODBCudf  
    (  
    @string_exp nvarchar(4000)  
    )  
RETURNS int  
AS  
BEGIN  
DECLARE @len int  
SET @len = (SELECT {fn BIT_LENGTH( @string_exp )})  
RETURN(@len)  
END ;  
  
SELECT dbo.ODBCudf('Returns the length in bits.');  
--Returns 432  
  
```  
  
### <a name="f-using-an-odbc-functions-in-select-statements"></a>F. Verwenden von ODBC-Funktionen in SELECT-Anweisungen  
 In den folgenden SELECT-Anweisungen werden ODBC-Funktionen verwendet:  
  
```  
DECLARE @string_exp nvarchar(4000) = 'Returns the length.';  
SELECT {fn BIT_LENGTH( @string_exp )};  
-- Returns 304  
  
SELECT {fn CONCAT( 'CONCAT ','returns a character string')};  
-- Returns CONCAT returns a character string  
SELECT {fn CURRENT_DATE( )};  
-- Returns todays date  
SELECT {fn CURRENT_TIME(6)};  
-- Returns the time  
  
DECLARE @date_exp nvarchar(30) = '2007-04-21 01:01:01.1234567';  
SELECT {fn DAYNAME( @date_exp )};  
-- Returns Saturday  
SELECT {fn DAYOFMONTH( @date_exp )};  
-- Returns 21  
SELECT {fn DAYOFWEEK( @date_exp )};  
-- Returns 7  
SELECT {fn HOUR( @date_exp)};  
-- Returns 1   
SELECT {fn MINUTE( @date_exp )};  
-- Returns 1  
SELECT {fn SECOND( @date_exp )};  
-- Returns 1  
SELECT {fn MONTHNAME( @date_exp )};  
-- Returns April  
SELECT {fn QUARTER( @date_exp )};  
-- Returns 2  
SELECT {fn WEEK( @date_exp )};  
-- Returns 16  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Integrierte Funktionen &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)  
  
  





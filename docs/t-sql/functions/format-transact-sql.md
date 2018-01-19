---
title: FORMAT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FORMAT_TSQL
- FORMAT
dev_langs: TSQL
helpviewer_keywords: FORMAT function
ms.assetid: dad6f24c-b8d9-4dbe-a561-9b167b8f20c8
caps.latest.revision: "21"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 46c7becb151b1942b411aefe337717172f207bb9
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="format-transact-sql"></a>FORMAT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Gibt ein Wert mit dem angegebenen Format und der optionalen Kultur in formatiert [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Verwenden Sie die FORMAT-Funktion für die gebietsschemabasierte Formatierung von Datums-/Uhrzeitwerten sowie numerischen Werten als Zeichenfolgen. Für allgemeine Datentypkonvertierungen verwenden Sie CAST oder CONVERT.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
FORMAT ( value, format [, culture ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *value*  
 Ausdruck eines unterstützten Datentyps, der formatiert werden soll. Eine Liste gültiger Typen finden Sie in der Tabelle im folgenden Abschnitt mit Hinweisen.  
  
 *format*  
 **Nvarchar** Formatmuster.  
  
 Das *format* -Argument muss eine gültige .NET Framework-Formatzeichenfolge enthalten, entweder als Standardformatzeichenfolge (z. B. "C" oder "D") oder als ein Muster aus benutzerdefinierten Zeichen für Datumsangaben und numerische Werte (z. B. "MMMM-DD, yyyy (dddd)"). Kombinierte Formatierung wird nicht unterstützt. Ausführliche erläuterungen zu diesen Formatierungsmustern können entnehmen Sie die .NET Framework-Dokumentation zur allgemeinen zeichenfolgenformatierung, benutzerdefinierte Datums- und Zeitformate und benutzerdefinierten Zahlenformaten. Ein guter Ausgangspunkt ist das Thema zu "[Formatierungstypen](http://go.microsoft.com/fwlink/?LinkId=211776)".  
  
 *culture*  
 Optionales **nvarchar** -Argument, das eine Kultur angibt.  
  
 Wenn das *culture* -Argument nicht angegeben wurde, wird die Sprache der aktuellen Sitzung verwendet. Diese Sprache ist entweder implizit definiert oder wird explizit mit der Anweisung SET LANGUAGE festgelegt. *Kultur* akzeptiert jede von .NET Framework als Argument unterstützte Kultur es gibt keine Beschränkung, die explizit von unterstützten Sprachen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Wenn das *culture* -Argument nicht gültig ist, löst FORMAT einen Fehler aus.  
  
## <a name="return-types"></a>Rückgabetypen  
 **nvarchar** oder NULL.  
  
 Die Länge des Rückgabewerts wird von *format*bestimmt.  
  
## <a name="remarks"></a>Hinweise  
 FORMAT gibt bei Fehlern, bei denen es sich nicht um eine *culture* handelt, die nicht *valid*ist, NULL zurück. NULL wird z. B. zurückgegeben, wenn der in *format* angegebene Wert nicht gültig ist.  
 
 Die FORMAT-Funktion ist nicht deterministisch.   
  
 FORMAT basiert auf dem Vorhandensein der .NET Framework Common Language Runtime (CLR).  
  
 Diese Funktion kann nicht remote ausgeführt, da sie die Existenz der CLR voraussetzt. Die Remoteausführung einer Funktion, die die CLR erfordert konnte dazu führen, dass einen Fehler auf dem Remoteserver.  
  
 FORMAT basiert auf CLR-Formatierungsregeln, der vorgibt, dass Doppelpunkte und Perioden mit Escapezeichen versehen werden müssen. Daher, wenn die Formatzeichenfolge (zweiten Parameter) enthält einen Doppelpunkt oder Zeitraum, den Doppelpunkt oder Zeitraum müssen mit Escapezeichen versehen werden mit umgekehrten Schrägstrich, wenn ein Eingabewert (erste Parameter) ist, der die **Zeit** -Datentyp. Finden Sie unter [D. FORMAT mit Time-Datentypen](#ExampleD).  
  
 In der folgenden Tabelle sind zulässige Datentypen für das *value* -Argument sowie die entsprechenden .NET Framework-Zuordnungstypen aufgeführt.  
  
|Kategorie|Typ|.NET-Typ|  
|--------------|----------|---------------|  
|Numerisch|bigint|Int64|  
|Numerisch|int|Int32|  
|Numerisch|smallint|Int16|  
|Numerisch|tinyint|Byte|  
|Numerisch|decimal|SqlDecimal|  
|Numerisch|Numerisch|SqlDecimal|  
|Numerisch|float|Double|  
|Numerisch|real|Single|  
|Numerisch|smallmoney|Decimal|  
|Numerisch|money|decimal|  
|Datum und Uhrzeit|Datum|datetime|  
|Datum und Uhrzeit|Uhrzeit|TimeSpan|  
|Datum und Uhrzeit|DateTime|DateTime|  
|Datum und Uhrzeit|smalldatetime|datetime|  
|Datum und Uhrzeit|datetime2|datetime|  
|Datum und Uhrzeit|datetimeoffset|datetimeoffset|  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-simple-format-example"></a>A. Einfaches Beispiel für FORMAT  
 Im folgenden Beispiel wird ein einfaches, für andere Kulturen formatiertes Datum zurückgegeben.  
  
```sql  
DECLARE @d DATETIME = '10/01/2011';  
SELECT FORMAT ( @d, 'd', 'en-US' ) AS 'US English Result'  
      ,FORMAT ( @d, 'd', 'en-gb' ) AS 'Great Britain English Result'  
      ,FORMAT ( @d, 'd', 'de-de' ) AS 'German Result'  
      ,FORMAT ( @d, 'd', 'zh-cn' ) AS 'Simplified Chinese (PRC) Result';   
  
SELECT FORMAT ( @d, 'D', 'en-US' ) AS 'US English Result'  
      ,FORMAT ( @d, 'D', 'en-gb' ) AS 'Great Britain English Result'  
      ,FORMAT ( @d, 'D', 'de-de' ) AS 'German Result'  
      ,FORMAT ( @d, 'D', 'zh-cn' ) AS 'Chinese (Simplified PRC) Result';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
US English Result Great Britain English Result  German Result Simplified Chinese (PRC) Result  
----------------  ----------------------------- ------------- -------------------------------------  
10/1/2011         01/10/2011                    01.10.2011    2011/10/1  
  
(1 row(s) affected)  
  
US English Result            Great Britain English Result  German Result                    Chinese (Simplified PRC) Result  
---------------------------- ----------------------------- -----------------------------  ---------------------------------------  
Saturday, October 01, 2011   01 October 2011               Samstag, 1. Oktober 2011        2011年10月1日  
  
(1 row(s) affected)  
```  
  
### <a name="b-format-with-custom-formatting-strings"></a>B. FORMAT mit benutzerdefinierten Formatierungszeichenfolgen  
 Im folgenden Beispiel ist das Formatieren von numerischen Werten durch Angeben eines benutzerdefinierten Formats dargestellt. Im Beispiel wird davon ausgegangen, dass das aktuelle Datum 27 September 2012 ist. Weitere Informationen zu diesen und anderen benutzerdefinierten Formaten finden Sie unter [Benutzerdefinierte Zahlenformatzeichenfolgen](http://msdn.microsoft.com/library/0c899ak8.aspx).  
  
```sql  
DECLARE @d DATETIME = GETDATE();  
SELECT FORMAT( @d, 'dd/MM/yyyy', 'en-US' ) AS 'DateTime Result'  
       ,FORMAT(123456789,'###-##-####') AS 'Custom Number Result';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
DateTime Result  Custom Number Result  
--------------   --------------------  
27/09/2012       123-45-6789  
  
(1 row(s) affected)  
```  
  
### <a name="c-format-with-numeric-types"></a>C. FORMAT mit numerischen Typen  
 Das folgende Beispiel gibt 5 Zeilen aus der **Sales.CurrencyRate** -Tabelle in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] Datenbank. Die Spalte **EndOfDateRate** wird als **money** -Typ in der Tabelle gespeichert. In diesem Beispiel wird die Spalte unformatiert zurückgegeben und wird dann durch Angeben der Typen für das .NET-Zahlenformat, das allgemeine Format und das Währungsformat formatiert. Weitere Informationen zu diesen und anderen Zahlenformaten finden Sie unter [Benutzerdefinierte Zahlenformatzeichenfolgen](http://msdn.microsoft.com/library/dwhawy9k.aspx).  
  
```sql  
SELECT TOP(5)CurrencyRateID, EndOfDayRate  
            ,FORMAT(EndOfDayRate, 'N', 'en-us') AS 'Number Format'  
            ,FORMAT(EndOfDayRate, 'G', 'en-us') AS 'General Format'  
            ,FORMAT(EndOfDayRate, 'C', 'en-us') AS 'Currency Format'  
FROM Sales.CurrencyRate  
ORDER BY CurrencyRateID;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
CurrencyRateID EndOfDayRate  Numeric Format  General Format  Currency Format  
-------------- ------------  --------------  --------------  ---------------  
1              1.0002        1.00            1.0002          $1.00  
2              1.55          1.55            1.5500          $1.55  
3              1.9419        1.94            1.9419          $1.94  
4              1.4683        1.47            1.4683          $1.47  
5              8.2784        8.28            8.2784          $8.28  
  
(5 row(s) affected)  
  
```  
  
 In diesem Beispiel wird die Kultur "Deutsch" (de-de) angegeben.  
  
```sql  
SELECT TOP(5)CurrencyRateID, EndOfDayRate  
      ,FORMAT(EndOfDayRate, 'N', 'de-de') AS 'Numeric Format'  
      ,FORMAT(EndOfDayRate, 'G', 'de-de') AS 'General Format'  
      ,FORMAT(EndOfDayRate, 'C', 'de-de') AS 'Currency Format'  
FROM Sales.CurrencyRate  
ORDER BY CurrencyRateID;  
```  
  
```  
CurrencyRateID EndOfDayRate  Numeric Format  General Format  Currency Format  
-------------- ------------  --------------  --------------  ---------------  
1              1.0002        1,00            1,0002          1,00 €  
2              1.55          1,55            1,5500          1,55 €  
3              1.9419        1,94            1,9419          1,94 €  
4              1.4683        1,47            1,4683          1,47 €  
5              8.2784        8,28            8,2784          8,28 €  
  
 (5 row(s) affected)  
```  
  
###  <a name="ExampleD"></a> D. FORMAT mit Time-Datentypen  
 Formatieren in diesen Fällen NULL zurückgegeben, da `.` und `:` kein Escapezeichen voransteht.  
  
```sql  
SELECT FORMAT(cast('07:35' as time), N'hh.mm');   --> returns NULL  
SELECT FORMAT(cast('07:35' as time), N'hh:mm');   --> returns NULL  
```  
  
 Format gibt eine formatierte Zeichenfolge zurück, da die `.` und `:` werden mit Escapezeichen versehen.  
  
```sql  
SELECT FORMAT(cast('07:35' as time), N'hh\.mm');  --> returns 07.35  
SELECT FORMAT(cast('07:35' as time), N'hh\:mm');  --> returns 07:35  
```  
  
## <a name="see-also"></a>Siehe auch  
 [CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
 [STR &#40;Transact-SQL&#41;](../../t-sql/functions/str-transact-sql.md)  
 [Zeichenfolgenfunktionen &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)   
  
  

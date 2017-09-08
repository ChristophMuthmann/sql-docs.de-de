---
title: CONCAT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CONCAT
- CONCAT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CONCAT function
ms.assetid: fce5a8d4-283b-4c47-95e5-4946402550d5
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2573d9f42b48205dab712ca401a1ac61ae4a17e2
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="concat-transact-sql"></a>CONCAT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all_md](../../includes/tsql-appliesto-ss2012-all-md.md)]

Gibt eine Zeichenfolge zurück, die das Ergebnis der Verkettung von zwei oder mehr Zeichenfolgenwerten darstellt. (Eine Trennung Wert während der Verkettung finden Sie unter [CONCAT_WS](../../t-sql/functions/concat-ws-transact-sql.md).)
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
CONCAT ( string_value1, string_value2 [, string_valueN ] )  
```  
  
## <a name="arguments"></a>Argumente  
*Zeichenfolgenwert*  
Ein Zeichenfolgenwert, der mit den anderen Werten verkettet werden soll.
  
## <a name="return-types"></a>Rückgabetypen
Zeichenfolge, deren Länge und Typ von der Eingabe abhängen.
  
## <a name="remarks"></a>Hinweise  
**CONCAT** nimmt eine Variable Anzahl von Argumenten und zu einer einzelnen Zeichenfolge verkettet. Es sind mindestens zwei Eingabewerte erforderlich. Andernfalls wird ein Fehler ausgelöst. Alle Argumente werden implizit in Zeichenfolgentypen konvertiert und dann verkettet. NULL-Werte werden implizit in eine leere Zeichenfolge konvertiert. Wenn alle Argumente null, eine leere Zeichenfolge vom Typ **Varchar**(1) wird zurückgegeben. Die implizite Konvertierung in Zeichenfolgen erfolgt basierend auf den vorhandenen Regeln für Datentypkonvertierungen. Weitere Informationen zu datentypkonvertierungen finden Sie unter [CAST und CONVERT &#40; Transact-SQL &#41; ](../../t-sql/functions/cast-and-convert-transact-sql.md).
  
Der Rückgabetyp hängt vom Typ der Argumente ab. In der folgenden Tabelle wird die Zuordnung veranschaulicht.
  
|Eingabetyp|Ausgabetyp und -länge|  
|---|---|
|Für ein Argument vom Typ SQL-CLR, SQL-CLR-UDT oder `nvarchar(max)`|**nvarchar(max)**|  
|Andernfalls, wenn eines der Argumente ist **varbinary(max)** oder **varchar(max)**|**varchar(max)** , wenn einer der Parameter ist ein **Nvarchar** mit beliebiger Länge. Wenn dies der Fall, klicken Sie dann das Ergebnis **nvarchar(max)**.|  
|Andernfalls, wenn eines der Argumente ist **Nvarchar**(< = 4000)|**Nvarchar**(< = 4000)|  
|Andernfalls, in allen anderen Fällen|**Varchar**(< = 8000), wenn einer der Parameter vom Typ Nvarchar mit beliebiger Länge ist. Wenn dies der Fall, klicken Sie dann das Ergebnis **nvarchar(max)**.|  
  
Wenn die Argumente sind < = 4000 für **Nvarchar**, oder < = 8000 für **Varchar**, können sich implizite Konvertierungen auf die Länge des Ergebnisses auswirken. Andere Datentypen haben andere Längen, wenn sie implizit in Zeichenfolgen konvertiert werden. Angenommen, ein **Int** (14) hat eine Zeichenfolgenlänge von 12, während eine **"float"** hat eine Länge von 32. Somit hat das Ergebnis aus der Verkettung von zwei ganzen Zahlen eine Länge von mindestens 24.
  
Wenn keines der Eingabeargumente einen unterstützten LOB-Typ aufweist, wird der Rückgabetyp unabhängig vom Rückgabetyp auf eine Lange von 8000 gekürzt. Durch diese Kürzung wird Speicherplatz eingespart und die Effizienz der Plangenerierung gesteigert.
  
CONCAT-Funktion kann remote ausgeführt werden, auf einem verknüpften Server, Version [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] und höher. Für ältere Verbindungsserver wird der CONCAT-Vorgang lokal ausgeführt werden, nachdem die Werte nicht verkettet vom Verbindungsserver zurückgegeben werden.
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-concat"></a>A. Verwenden von CONCAT  
  
```sql
SELECT CONCAT ( 'Happy ', 'Birthday ', 11, '/', '25' ) AS Result;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
-------------------------  
Happy Birthday 11/25  
  
(1 row(s) affected)  
```  
  
### <a name="b-using-concat-with-null-values"></a>B. Verwenden von CONCAT mit NULL-Werten  
  
```sql
CREATE TABLE #temp (  
    emp_name nvarchar(200) NOT NULL,  
    emp_middlename nvarchar(200) NULL,  
    emp_lastname nvarchar(200) NOT NULL  
);  
INSERT INTO #temp VALUES( 'Name', NULL, 'Lastname' );  
SELECT CONCAT( emp_name, emp_middlename, emp_lastname ) AS Result  
FROM #temp;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
------------------  
NameLastname  
  
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-concat"></a>C. Verwenden von CONCAT  
  
```sql
SELECT CONCAT ( 'Happy ', 'Birthday ', 11, '/', '25' ) AS Result;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
-------------------------  
Happy Birthday 11/25  
  
(1 row(s) affected)  
```  
## <a name="see-also"></a>Siehe auch
[Zeichenfolgenfunktionen (Transact-SQL)](../../t-sql/functions/string-functions-transact-sql.md)  
[CONCAT_WS (Transact-SQL)](../../t-sql/functions/concat-ws-transact-sql.md)   
  




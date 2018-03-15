---
title: CONCAT (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 07/24/2017
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
- CONCAT
- CONCAT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CONCAT function
ms.assetid: fce5a8d4-283b-4c47-95e5-4946402550d5
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 1f3a1ef2b55b2f67b6b2e01ceb1965a5076e8476
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="concat-transact-sql"></a>CONCAT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

Gibt eine Zeichenfolge zurück, die das Ergebnis der Verkettung von zwei oder mehr Zeichenfolgenwerten darstellt. (Informationen zum Hinzufügen eines Trennwerts beim Verkettungsvorgang finden Sie unter [CONCAT_WS](../../t-sql/functions/concat-ws-transact-sql.md).)
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
CONCAT ( string_value1, string_value2 [, string_valueN ] )  
```  
  
## <a name="arguments"></a>Argumente  
*string_value*  
Ein Zeichenfolgenwert, der mit den anderen Werten verkettet werden soll.
  
## <a name="return-types"></a>Rückgabetypen
Zeichenfolge, deren Länge und Typ von der Eingabe abhängen.
  
## <a name="remarks"></a>Remarks  
**CONCAT** lässt eine variable Anzahl von Zeichenfolgenargumenten zu und verkettet sie in einer einzelnen Zeichenfolge. Es sind mindestens zwei Eingabewerte erforderlich. Andernfalls wird ein Fehler ausgelöst. Alle Argumente werden implizit in Zeichenfolgentypen konvertiert und dann verkettet. NULL-Werte werden implizit in eine leere Zeichenfolge konvertiert. Wenn alle Argumente NULL sind, wird eine leere Zeichenfolge des Typs **varchar(1)** zurückgegeben. Die implizite Konvertierung in Zeichenfolgen erfolgt basierend auf den vorhandenen Regeln für Datentypkonvertierungen. Weitere Informationen zu Datentypkonvertierungen finden Sie unter [CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md).
  
Der Rückgabetyp hängt vom Typ der Argumente ab. In der folgenden Tabelle wird die Zuordnung veranschaulicht.
  
|Eingabetyp|Ausgabetyp und -länge|  
|---|---|
|Für ein Argument vom Typ SQL-CLR, SQL-CLR-UDT oder `nvarchar(max)`|**nvarchar(max)**|  
|Für ein Argument vom Typ **varbinary(max)** oder **varchar(max)**|**varchar(max)**, sofern keiner der Parameter vom Typ **nvarchar** mit beliebiger Länge ist. Ist dies der Fall, ist das Ergebnis vom Typ **nvarchar(max)**.|  
|Für ein Argument vom Typ **nvarchar**(<=4000)|**nvarchar**(<= 4000)|  
|Andernfalls, in allen anderen Fällen|**varchar**(<= 8000), sofern keiner der Parameter vom Typ nvarchar mit beliebiger Länge ist. Ist dies der Fall, ist das Ergebnis vom Typ **nvarchar(max)**.|  
  
Wenn die Argumente <=4000 für **nvarchar** oder <=8000 für **varchar** lauten, können sich implizite Konvertierungen auf die Länge des Ergebnisses auswirken. Andere Datentypen haben andere Längen, wenn sie implizit in Zeichenfolgen konvertiert werden. **int** (14) hat z.B. eine Zeichenfolgenlänge von 12, während **float** eine Länge von 32 hat. Somit hat das Ergebnis aus der Verkettung von zwei ganzen Zahlen eine Länge von mindestens 24.
  
Wenn keines der Eingabeargumente einen unterstützten LOB-Typ aufweist, wird der Rückgabetyp unabhängig vom Rückgabetyp auf eine Lange von 8000 gekürzt. Durch diese Kürzung wird Speicherplatz eingespart und die Effizienz der Plangenerierung gesteigert.
  
Die CONCAT-Funktion kann über eine Remoteverknüpfung auf einem Verbindungsserver der Version [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] und höher ausgeführt werden. Bei älteren Verbindungsservern wird der CONCAT-Vorgang lokal ausgeführt, nachdem die nicht verketteten Werte vom Verbindungsserver zurückgegeben wurden.
  
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
  
## <a name="see-also"></a>Siehe auch
 [CONCAT_WS &#40;Transact-SQL&#41;](../../t-sql/functions/concat-ws-transact-sql.md)   
 [FORMATMESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/formatmessage-transact-sql.md)  
 [QUOTENAME &#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)  
 [REPLACE &#40;Transact-SQL&#41;](../../t-sql/functions/replace-transact-sql.md)  
 [REVERSE &#40;Transact-SQL&#41;](../../t-sql/functions/reverse-transact-sql.md)  
 [STRING_AGG &#40;Transact-SQL&#41;](../../t-sql/functions/string-agg-transact-sql.md)  
 [STRING_ESCAPE &#40;Transact-SQL&#41;](../../t-sql/functions/string-escape-transact-sql.md)  
 [STUFF &#40;Transact-SQL&#41;](../../t-sql/functions/stuff-transact-sql.md)  
 [TRANSLATE &#40;Transact-SQL&#41;](../../t-sql/functions/translate-transact-sql.md)  
 [String Functions &#40;Transact-SQL&#41; (Zeichenfolgenfunktionen (Transact-SQL))](../../t-sql/functions/string-functions-transact-sql.md)  
  



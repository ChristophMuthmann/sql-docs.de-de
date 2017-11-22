---
title: ZWISCHEN (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/28/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- BETWEEN
- BETWEEN_TSQL
dev_langs: TSQL
helpviewer_keywords:
- inclusive ranges
- testing range
- exclusive ranges
- NOT BETWEEN operator
- BETWEEN operator
- range to test [SQL Server]
ms.assetid: a5d5b050-203e-4355-ac85-e08ef5ca7823
caps.latest.revision: "34"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 8ff77a998bba76af8a1fdfb728e613158a5c478b
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="between-transact-sql"></a>BETWEEN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt einen zu testenden Bereich an.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
test_expression [ NOT ] BETWEEN begin_expression AND end_expression  
```  
  
## <a name="arguments"></a>Argumente  
 *test_expression*  
 Ist die [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) So testen Sie im Bereich von definierten für *Begin_expression*und *End_expression*. *Test_expression* muss den gleichen Datentyp wie *Begin_expression* und *End_expression*.  
  
 NICHT  
 Gibt an, dass das Ergebnis des Prädikats negiert wird.  
  
 *begin_expression*  
 Ein gültiger Ausdruck. *Begin_expression* muss den gleichen Datentyp wie *Test_expression* und *End_expression*.  
  
 *end_expression*  
 Ein gültiger Ausdruck. *End_expression* muss den gleichen Datentyp wie *Test_expression*und *Begin_expression*.  
  
 AND  
 Fungiert als Platzhalter, der angibt, *Test_expression* muss innerhalb des Bereichs erkennbar *Begin_expression* und *End_expression*.  
  
## <a name="result-types"></a>Ergebnistypen  
 **Boolean**  
  
## <a name="result-value"></a>Ergebniswert  
 ZWISCHEN gibt **"true"** Wenn der Wert der *Test_expression* ist größer als oder gleich dem Wert der *Begin_expression* und kleiner oder gleich dem Wert des *End_expression*.  
  
 NOT BETWEEN gibt **"true"** Wenn der Wert der *Test_expression* ist kleiner als der Wert des *Begin_expression* oder größer als der Wert des *End_expression* .  
  
## <a name="remarks"></a>Hinweise  
 Verwenden Sie die Operatoren Größer-als (>) und Kleiner-als (<), um einen Exklusivbereich anzugeben. Ist einer der Eingabewerte für das BETWEEN- oder NOT BETWEEN-Prädikat NULL, lautet das Ergebnis UNKNOWN.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-between"></a>A. Verwenden von BETWEEN  
 Das folgende Beispiel gibt Informationen über die Datenbankrollen in einer Datenbank zurück. Die erste Abfrage gibt alle Rollen zurück. Im zweiten Beispiel wird die `BETWEEN` -Klausel können Sie die Rollen mit dem angegebenen beschränken `database_id` Werte.  
  
```sql  
SELECT principal_id, name 
FROM sys.database_principals
WHERE type = 'R';

SELECT principal_id, name 
FROM sys.database_principals
WHERE type = 'R'
AND principal_id BETWEEN 16385 AND 16390;
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]   
```  
principal_id    name
------------  ---- 
0               public
16384           db_owner
16385           db_accessadmin
16386           db_securityadmin
16387           db_ddladmin
16389           db_backupoperator
16390           db_datareader
16391           db_datawriter
16392           db_denydatareader
16393           db_denydatawriter
```  
```  
principal_id    name
------------  ---- 
16385           db_accessadmin
16386           db_securityadmin
16387           db_ddladmin
16389           db_backupoperator
16390           db_datareader
```  
  
### <a name="b-using--and--instead-of-between"></a>B. Verwenden von > und < anstelle von BETWEEN  
 Im folgenden Beispiel werden die Operatoren Größer-als (`>`) und Kleiner-als (`<`) verwendet. Da diese Operatoren die Bereichsgrenzen nicht einschließen, werden im Unterschied zu den zehn Zeilen des vorherigen Beispiels nur neun Zeilen zurückgegeben.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT e.FirstName, e.LastName, ep.Rate  
FROM HumanResources.vEmployee e   
JOIN HumanResources.EmployeePayHistory ep   
    ON e.BusinessEntityID = ep.BusinessEntityID  
WHERE ep.Rate > 27 AND ep.Rate < 30  
ORDER BY ep.Rate;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```  
 FirstName   LastName             Rate  
 ---------   -------------------  ---------  
 Paula       Barreto de Mattos    27.1394  
 Janaina     Bueno                27.4038  
 Dan         Bacon                27.4038  
 Ramesh      Meyyappan            27.4038  
 Karen       Berg                 27.4038  
 David       Bradley              28.7500  
 Hazem       Abolrous             28.8462  
 Ovidiu      Cracium              28.8462  
 Rob         Walters              29.8462  
 ```    
  
### <a name="c-using-not-between"></a>C. Verwenden von NOT BETWEEN  
 Im folgenden Beispiel werden alle Zeilen gesucht, die außerhalb des angegebenen Bereiches von `27` bis `30` liegen.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT e.FirstName, e.LastName, ep.Rate  
FROM HumanResources.vEmployee e   
JOIN HumanResources.EmployeePayHistory ep   
    ON e.BusinessEntityID = ep.BusinessEntityID  
WHERE ep.Rate NOT BETWEEN 27 AND 30  
ORDER BY ep.Rate;  
GO  
```  
  
### <a name="d-using-between-with-datetime-values"></a>D. Verwenden von BETWEEN mit datetime-Werten  
 Das folgende Beispiel ruft die Zeilen, in denen **"DateTime"** Werte liegen zwischen `'20011212'` und `'20020105'`(einschließlich).  
  
```sql  
-- Uses AdventureWorks  
  
SELECT BusinessEntityID, RateChangeDate  
FROM HumanResources.EmployeePayHistory  
WHERE RateChangeDate BETWEEN '20011212' AND '20020105';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```  
 BusinessEntityID RateChangeDate  
 ----------- -----------------------  
 3           2001-12-12 00:00:00.000  
 4           2002-01-05 00:00:00.000  
 ```  
 
 Die Abfrage die erwarteten Zeilen abgerufen, da das Datum in der Abfrage Werte und die **"DateTime"** in gespeicherten Werte der `RateChangeDate` Spalte ohne den Zeitteil des Datums angegeben wurden. Wenn der Zeitteil nicht angegeben wird, wird standardmäßig 0:00 Uhr verwendet. Beachten Sie, dass eine Zeile mit einen Zeitteil, der nach 0:00 Uhr am Datum 2002-01-05 liegt, von dieser Abfrage nicht zurückgegeben wird, da das Datum außerhalb des Bereichs liegt.  
  
  
## <a name="see-also"></a>Siehe auch  
 [&#62; &#40; Größer als &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/greater-than-transact-sql.md)   
 [&#60; &#40; Kleiner als &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/less-than-transact-sql.md)   
 [Ausdrücke &#40; Transact-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Integrierte Funktionen &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [Operatoren &#40; Transact-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [WOBEI &#40; Transact-SQL &#41;](../../t-sql/queries/where-transact-sql.md)  
  
  



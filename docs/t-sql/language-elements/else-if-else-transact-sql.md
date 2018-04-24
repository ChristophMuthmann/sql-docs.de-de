---
title: ELSE (IF...ELSE) (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|language-elements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ELSE
- ELSE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ELSE (IF...ELSE) keyword
- ELSE keyword
- IF keyword
ms.assetid: 6f2b4278-0dea-4603-bbd3-7cbad602a645
caps.latest.revision: 34
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: c90260f85a28f39c22848486aec0e7dc32ac6d37
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="else-ifelse-transact-sql"></a>ELSE (IF...ELSE) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Legt Bedingungen für die Ausführung einer [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung fest. Die [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung (*sql_statement*) nach dem *Boolean_expression*-Objekt wird ausgeführt, wenn das *Boolean_expression*-Objekt als TRUE ausgewertet wird. Die alternative [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung nach dem optionalen ELSE-Schlüsselwort wird ausgeführt, falls *Boolean_expression* als FALSE oder NULL ausgewertet wird.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
IF Boolean_expression   
     { sql_statement | statement_block }   
[ ELSE   
     { sql_statement | statement_block } ]   
```  
  
## <a name="arguments"></a>Argumente  
 *Boolean_expression*  
 Ein Ausdruck, der TRUE oder FALSE zurückgibt. Wenn das *Boolean_expression*-Objekt eine SELECT-Anweisung enthält, muss die SELECT-Anweisung in Klammern eingeschlossen werden.  
  
 { *sql_statement* | *statement_block* }  
 Eine beliebige gültige [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung oder -Anweisungsgruppierung, die als Anweisungsblock definiert ist. Um einen Anweisungsblock (Batch) zu definieren, verwenden Sie die Schlüsselwörter BEGIN und END aus den Sprachkonstrukten zur Ablaufsteuerung. Obwohl sämtliche [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen in einem BEGIN...END-Block gültig sind, sollten bestimmte [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen nicht in demselben Batch (Anweisungsblock) gruppiert werden.  
  
## <a name="result-types"></a>Ergebnistypen  
 **Boolean**  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-a-simple-boolean-expression"></a>A. Verwenden eines einfachen booleschen Ausdrucks  
 Das folgende Beispiel enthält einen einfachen booleschen Ausdruck (`1=1`), der TRUE ist, und daher wird die erste Anweisung ausgegeben.  
  
```  
IF 1 = 1 PRINT 'Boolean_expression is true.'  
ELSE PRINT 'Boolean_expression is false.' ;  
```  
  
 Das folgende Beispiel enthält einen einfachen booleschen Ausdruck (`1=2`), der FALSE ist, und daher wird die zweite Anweisung ausgegeben.  
  
```  
IF 1 = 2 PRINT 'Boolean_expression is true.'  
ELSE PRINT 'Boolean_expression is false.' ;  
GO  
```  
  
### <a name="b-using-a-query-as-part-of-a-boolean-expression"></a>B. Verwenden einer Abfrage als Teil eines booleschen Ausdrucks  
 Im folgenden Beispiel wird eine Abfrage als Teil des booleschen Ausdrucks ausgeführt. Da in der `Product`-Tabelle 10 Fahrräder vorhanden sind, die der `WHERE`-Klausel entsprechen, wird die erste Print-Anweisung ausgeführt. Ändern Sie `> 5` in `> 15`, um die mögliche Ausführung des zweiten Teils der Anweisung anzuzeigen.  
  
```  
USE AdventureWorks2012;  
GO  
IF   
(SELECT COUNT(*) FROM Production.Product WHERE Name LIKE 'Touring-3000%' ) > 5  
PRINT 'There are more than 5 Touring-3000 bicycles.'  
ELSE PRINT 'There are 5 or less Touring-3000 bicycles.' ;  
GO  
```  
  
### <a name="c-using-a-statement-block"></a>C. Verwenden eines Anweisungsblocks  
 Im folgenden Beispiel wird eine Abfrage als Teil des booleschen Ausdrucks ausgeführt, und anschließend werden auf der Grundlage der Ergebnisse des booleschen Ausdrucks leicht abweichende Anweisungsblöcke ausgeführt. Jeder Anweisungsblock beginnt mit `BEGIN`, und er wird mit `END` abgeschlossen.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @AvgWeight decimal(8,2), @BikeCount int  
IF   
(SELECT COUNT(*) FROM Production.Product WHERE Name LIKE 'Touring-3000%' ) > 5  
BEGIN  
   SET @BikeCount =   
        (SELECT COUNT(*)   
         FROM Production.Product   
         WHERE Name LIKE 'Touring-3000%');  
   SET @AvgWeight =   
        (SELECT AVG(Weight)   
         FROM Production.Product   
         WHERE Name LIKE 'Touring-3000%');  
   PRINT 'There are ' + CAST(@BikeCount AS varchar(3)) + ' Touring-3000 bikes.'  
   PRINT 'The average weight of the top 5 Touring-3000 bikes is ' + CAST(@AvgWeight AS varchar(8)) + '.';  
END  
ELSE   
BEGIN  
SET @AvgWeight =   
        (SELECT AVG(Weight)  
         FROM Production.Product   
         WHERE Name LIKE 'Touring-3000%' );  
   PRINT 'Average weight of the Touring-3000 bikes is ' + CAST(@AvgWeight AS varchar(8)) + '.' ;  
END ;  
GO  
```  
  
### <a name="d-using-nested-ifelse-statements"></a>D. Verwenden geschachtelter IF...ELSE-Anweisungen  
 Im folgenden Beispiel wird gezeigt, wie eine IF … ELSE-Anweisung in einer anderen geschachtelt werden kann. Legen Sie die `@Number`-Variable auf `5`, `50` und `500` fest, um die einzelnen Anweisungen zu testen.  
  
```  
DECLARE @Number int;  
SET @Number = 50;  
IF @Number > 100  
   PRINT 'The number is large.';  
ELSE   
   BEGIN  
      IF @Number < 10  
      PRINT 'The number is small.';  
   ELSE  
      PRINT 'The number is medium.';  
   END ;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
### <a name="e-using-a-query-as-part-of-a-boolean-expression"></a>E. Verwenden einer Abfrage als Teil eines booleschen Ausdrucks  
 Im folgenden Beispiel wird `IF…ELSE` verwendet, um basierend auf der Gewichtung eines Elements in der `DimProduct`-Tabelle festzulegen, welche Antwort von zwei Antworten dem Benutzer angezeigt wird.  
  
```  
-- Uses AdventureWorks  
  
DECLARE @maxWeight float, @productKey integer  
SET @maxWeight = 100.00  
SET @productKey = 424  
IF @maxWeight <= (SELECT Weight from DimProduct WHERE ProductKey=@productKey)   
    (SELECT @productKey, EnglishDescription, Weight, 'This product is too heavy to ship and is only available for pickup.' FROM DimProduct WHERE ProductKey=@productKey)  
ELSE  
    (SELECT @productKey, EnglishDescription, Weight, 'This product is available for shipping or pickup.' FROM DimProduct WHERE ProductKey=@productKey)  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [Control-of-Flow Language &#40;Transact-SQL&#41; (Sprachkonstrukte zur Ablaufsteuerung (Transact-SQL))](~/t-sql/language-elements/control-of-flow.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [IF...ELSE &#40;Transact-SQL&#41;](../../t-sql/language-elements/if-else-transact-sql.md)  
  
  



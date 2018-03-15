---
title: IF...ELSE (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 07/11/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- IF_TSQL
- IF
dev_langs:
- TSQL
helpviewer_keywords:
- IF...ELSE keyword
- ELSE (IF...ELSE) keyword
- ELSE keyword
- IF keyword
ms.assetid: 676c881f-dee1-417a-bc51-55da62398e81
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 34a14f617d5eed0b56d6ffb44134f03efa96d2c2
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="ifelse-transact-sql"></a>IF...ELSE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Legt Bedingungen für die Ausführung einer [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung fest. Die [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung nach dem IF-Schlüsselwort und der Bedingung wird nur ausgeführt, wenn die Bedingung erfüllt ist. Dies ist der Fall, wenn der boolesche Ausdruck TRUE zurückgibt. Das optionale ELSE-Schlüsselwort führt eine alternative [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung ein, die ausgeführt wird, wenn die IF-Bedingung nicht erfüllt ist. Dies ist der Fall., wenn der boolesche Ausdruck FALSE zurückgibt.  
  
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
 Ein Ausdruck, der TRUE oder FALSE zurückgibt. Wenn der boolesche Ausdruck eine SELECT-Anweisung enthält, muss die SELECT-Anweisung in Klammern eingeschlossen werden.  
  
 { *sql_statement*| *statement_block* }  
 Eine beliebige [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung oder -Anweisungsgruppe, die mithilfe eines Anweisungsblockes definiert wurde. Wenn kein Anweisungsblock angegeben wurde, steuert die IF- oder ELSE-Bedingung nur die Ausführung einer einzelnen [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung.  
  
 Um einen Anweisungsblock zu definieren, verwenden Sie die Schlüsselwörter zur Ablaufsteuerung BEGIN und END.  
  
## <a name="remarks"></a>Remarks  
 Ein IF...ELSE-Konstrukt kann in Batches, gespeicherten Prozeduren und Ad-hoc-Abfragen verwendet werden. Wenn dieses Konstrukt in einer gespeicherten Prozedur verwendet wird, wird damit das Vorhandensein bestimmter Parameter getestet.  
  
 IF-Tests können nach einem anderen IF oder auf ein ELSE folgend geschachtelt werden. Das Limit für die Anzahl geschachtelter Ebenen hängt vom verfügbaren Arbeitsspeicher ab.  
  
## <a name="example"></a>Beispiel  
  
```  
IF DATENAME(weekday, GETDATE()) IN (N'Saturday', N'Sunday')
       SELECT 'Weekend';
ELSE 
       SELECT 'Weekday';
```  
  
 Weitere Beispiele finden Sie unter [ELSE &#40;IF...ELSE&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/else-if-else-transact-sql.md).  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
 Im folgenden Beispiel wird `IF…ELSE` verwendet, um basierend auf der Gewichtung eines Elements in der `DimProduct`-Tabelle festzulegen, welche Antwort von zwei Antworten dem Benutzer angezeigt wird.  
  
```  
-- Uses AdventureWorksDW  
  
DECLARE @maxWeight float, @productKey integer  
SET @maxWeight = 100.00  
SET @productKey = 424  
IF @maxWeight <= (SELECT Weight from DimProduct 
                  WHERE ProductKey = @productKey)   
    (SELECT @productKey AS ProductKey, EnglishDescription, Weight, 
    'This product is too heavy to ship and is only available for pickup.' 
        AS ShippingStatus
    FROM DimProduct WHERE ProductKey = @productKey);  
ELSE  
    (SELECT @productKey AS ProductKey, EnglishDescription, Weight, 
    'This product is available for shipping or pickup.' 
        AS ShippingStatus
    FROM DimProduct WHERE ProductKey = @productKey);  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [BEGIN...END &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-end-transact-sql.md)   
 [END &#40;BEGIN...END&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/end-begin-end-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [WHILE &#40;Transact-SQL&#41;](../../t-sql/language-elements/while-transact-sql.md)   
 [CASE &#40;Transact-SQL&#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [Sprachkonstrukte zur Ablaufsteuerung &#40;Transact-SQL&#41;](~/t-sql/language-elements/control-of-flow.md) [ELSE &#40;IF...ELSE&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/else-if-else-transact-sql.md) 
  
  




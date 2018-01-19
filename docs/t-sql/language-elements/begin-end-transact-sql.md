---
title: GESTARTET... Ende (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
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
- BEGIN
- BEGIN_TSQL
dev_langs: TSQL
helpviewer_keywords:
- enclosing statements [SQL Server]
- BEGIN statement
- control-of-flow language [SQL Server], BEGIN...END statement
- BEGIN...END keyword
- grouping statements, BEGIN...END statement
- executing Transact-SQL statements together [SQL Server]
- statements [SQL Server], grouping
ms.assetid: fc2c7f76-f1f9-4f91-beef-bc8ef0da2feb
caps.latest.revision: "30"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 660e238a453c7438f726847c8c3ce0811c0731ea
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/19/2018
---
# <a name="beginend-transact-sql"></a>BEGIN...END (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Schließt eine Reihe von [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen ein, sodass eine Gruppe von [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen ausgeführt werden kann. Die Schlüsselwörter BEGIN und END gehören in die Gruppe der Sprachkonstrukte zur Ablaufsteuerung.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
BEGIN  
    { sql_statement | statement_block }   
END  
```  
  
## <a name="arguments"></a>Argumente  
 { *sql_statement* | *statement_block* }  
 Eine beliebige gültige [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung oder -Anweisungsgruppierung, die mithilfe eines Anweisungsblockes definiert ist.  
  
## <a name="remarks"></a>Hinweise  
 BEGIN...END-Blöcke können geschachtelt werden.  
  
 Obwohl sämtliche [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen in einem BEGIN...END-Block gültig sind, sollten bestimmte [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen nicht in demselben Batch oder Anweisungsblock gruppiert werden.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird durch `BEGIN` und `END` eine Reihe von [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen definiert, die gemeinsam ausgeführt werden. Wäre der `BEGIN...END`-Block nicht vorhanden, würden beide `ROLLBACK TRANSACTION`-Anweisungen ausgeführt, und beide `PRINT`-Meldungen würden zurückgegeben.  
  
```  
USE AdventureWorks2012;  
GO  
BEGIN TRANSACTION;  
GO  
IF @@TRANCOUNT = 0  
BEGIN  
    SELECT FirstName, MiddleName   
    FROM Person.Person WHERE LastName = 'Adams';  
    ROLLBACK TRANSACTION;  
    PRINT N'Rolling back the transaction two times would cause an error.';  
END;  
ROLLBACK TRANSACTION;  
PRINT N'Rolled back the transaction.';  
GO  
/*  
Rolled back the transaction.  
*/  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 Im folgenden Beispiel `BEGIN` und `END` definieren Sie eine Reihe von [!INCLUDE[DWsql](../../includes/dwsql-md.md)] -Anweisungen, die zusammen ausgeführt. Wenn die `BEGIN...END` Block sind nicht enthalten, die im folgende Beispiel werden in eine Endlosschleife.  
  
```  
-- Uses AdventureWorks  
  
DECLARE @Iteration Integer = 0  
WHILE @Iteration <10  
BEGIN  
    SELECT FirstName, MiddleName   
    FROM dbo.DimCustomer WHERE LastName = 'Adams';  
SET @Iteration += 1  
END;  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [Control-of-Flow-Sprache &#40; Transact-SQL &#41;](~/t-sql/language-elements/control-of-flow.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [END &#40;BEGIN...END&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/end-begin-end-transact-sql.md)  
  
  



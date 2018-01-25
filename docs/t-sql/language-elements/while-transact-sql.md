---
title: Beim (Transact-SQL) | Microsoft Docs
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
- WHILE_TSQL
- WHILE
dev_langs: TSQL
helpviewer_keywords:
- statements [SQL Server], repeated executions
- statement blocks [SQL Server]
- repeated statement executions
- nested WHILE loops
- WHILE keyword
ms.assetid: 52dd29ab-25d7-4fd3-a960-ac55c30c9ea9
caps.latest.revision: "40"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 62f346d7a32e6c1aa55e42666ad39f426e1ed8a5
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="while-transact-sql"></a>WHILE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Legt eine Bedingung für die wiederholte Ausführung einer SQL-Anweisung oder eines Anweisungsblockes fest. Die Anweisungen werden wiederholt ausgeführt, solange die angegebene Bedingung true ist. Sie können die Ausführung der Anweisungen in der WHILE-Schleife mithilfe der Schlüsselwörter BREAK und CONTINUE auch innerhalb der Schleife steuern.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
WHILE Boolean_expression   
     { sql_statement | statement_block | BREAK | CONTINUE }  
  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
WHILE Boolean_expression   
     { sql_statement | statement_block | BREAK }  
  
```  
  
## <a name="arguments"></a>Argumente  
 *Boolean_expression*  
 Ist ein [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) zurückgibt **"true"** oder **"false"**. Wenn der boolesche Ausdruck eine SELECT-Anweisung enthält, muss die SELECT-Anweisung in Klammern eingeschlossen werden.  
  
 {*sql_statement* | *statement_block*}  
 Ist eine beliebige [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung oder -Anweisungsgruppe, die als Anweisungsblock definiert wurde. Um einen Anweisungsblock zu definieren, verwenden Sie die Schlüsselwörter zur Ablaufsteuerung BEGIN und END.  
  
 BREAK  
 Bewirkt das Beenden der innersten WHILE-Schleife. Alle Anweisungen, die nach dem END-Schlüsselwort, markiert das Ende der Schleife auftreten, werden ausgeführt.  
  
 CONTINUE  
 Bewirkt, dass die WHILE-Schleife neu gestartet wird und alle Anweisungen nach dem CONTINUE-Schlüsselwort ignoriert werden.  
  
## <a name="remarks"></a>Hinweise  
 Wenn zwei oder mehr WHILE-Schleifen geschachtelt sind, wird mit der inneren BREAK-Anweisung zur nächsten äußersten Schleife gesprungen. Alle Anweisungen nach dem Ende der inneren Schleife werden zuerst ausgeführt, und dann wird die nächste äußerste Schleife neu gestartet.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-break-and-continue-with-nested-ifelse-and-while"></a>A. Verwenden von BREAK und CONTINUE mit geschachtelten IF...ELSE- und WHILE-Anweisungen  
 Im folgenden Beispiel verdoppelt die `$300`-Schleife die Preise und wählt dann den Höchstpreis aus, wenn der durchschnittliche Listenpreis eines Produkts unter `WHILE` liegt. Ist der Höchstpreis niedriger als oder gleich `$500`, wird die `WHILE`-Schleife erneut gestartet und der Preis erneut verdoppelt. Diese Schleife verdoppelt die Preise so lange, bis der Höchstpreis mehr als `$500` beträgt; dann wird die `WHILE`-Schleife beendet und eine Meldung ausgegeben.  
  
```  
USE AdventureWorks2012;  
GO  
WHILE (SELECT AVG(ListPrice) FROM Production.Product) < $300  
BEGIN  
   UPDATE Production.Product  
      SET ListPrice = ListPrice * 2  
   SELECT MAX(ListPrice) FROM Production.Product  
   IF (SELECT MAX(ListPrice) FROM Production.Product) > $500  
      BREAK  
   ELSE  
      CONTINUE  
END  
PRINT 'Too much for the market to bear';  
```  
  
### <a name="b-using-while-in-a-cursor"></a>B. Verwenden von WHILE in einem Cursor  
 Im folgenden Beispiel wird `@@FETCH_STATUS` zur Steuerung der Cursoraktivitäten in einer `WHILE`-Schleife verwendet.  
  
```  
DECLARE Employee_Cursor CURSOR FOR  
SELECT EmployeeID, Title   
FROM AdventureWorks2012.HumanResources.Employee  
WHERE JobTitle = 'Marketing Specialist';  
OPEN Employee_Cursor;  
FETCH NEXT FROM Employee_Cursor;  
WHILE @@FETCH_STATUS = 0  
   BEGIN  
      FETCH NEXT FROM Employee_Cursor;  
   END;  
CLOSE Employee_Cursor;  
DEALLOCATE Employee_Cursor;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-simple-while-loop"></a>"C:" einfache While-Schleife  
 Im folgenden Beispiel verdoppelt die `$300`-Schleife die Preise und wählt dann den Höchstpreis aus, wenn der durchschnittliche Listenpreis eines Produkts unter `WHILE` liegt. Ist der Höchstpreis niedriger als oder gleich `$500`, wird die `WHILE`-Schleife erneut gestartet und der Preis erneut verdoppelt. Diese Schleife verdoppelt die Preise, bis der Höchstpreis größer ist `$500`, und wird dann beendet die `WHILE` Schleife.  
  
```  
-- Uses AdventureWorks  
  
WHILE ( SELECT AVG(ListPrice) FROM dbo.DimProduct) < $300  
BEGIN  
    UPDATE dbo.DimProduct  
        SET ListPrice = ListPrice * 2;  
    SELECT MAX ( ListPrice) FROM dbo.DimProduct  
    IF ( SELECT MAX (ListPrice) FROM dbo.DimProduct) > $500  
        BREAK;  
END  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [Control-of-Flow-Sprache &#40; Transact-SQL &#41;](~/t-sql/language-elements/control-of-flow.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [Cursors &#40;Transact-SQL&#41;](../../t-sql/language-elements/cursors-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)  
  
  



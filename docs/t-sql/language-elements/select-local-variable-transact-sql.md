---
title: "Wählen Sie @local_variable (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 09/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- variable_TSQL
- '@loca_variable'
- '@local'
- variable
- '@loca_variable_TSQL'
- '@local_TSQL'
dev_langs: TSQL
helpviewer_keywords:
- variables [SQL Server], assigning
- SELECT statement [SQL Server], @local_variable
- '@local_variable'
- local variables [SQL Server]
ms.assetid: 8e1a9387-2c5d-4e51-a1fd-a2a95f026d6f
caps.latest.revision: "32"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 44fd55346e8a4a27f1d3301d6cb3c6bdf7bdf548
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="select-localvariable-transact-sql"></a>SELECT @local_variable (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Legt eine lokale Variable auf den Wert eines Ausdrucks.  
  
 Zum Zuweisen von Variablen, empfehlen wir die Verwendung [festgelegt @local_variable ](../../t-sql/language-elements/set-local-variable-transact-sql.md) anstelle von SELECT @*Local_variable*.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
SELECT { @local_variable { = | += | -= | *= | /= | %= | &= | ^= | |= } expression } 
    [ ,...n ] [ ; ]  
```  
  
## <a name="arguments"></a>Argumente  
@*local_variable*  
 Dies ist eine deklarierte Variable, der ein Wert zugewiesen wird.  
  
{= | += | -= | \*= | /= | %= | &= | ^= | |= }   
Den Wert auf der rechten Seite der Variablen auf der linken Seite zuweisen.  
  
Verbundzuweisungsoperator:  
  |Operator |action |   
  |-----|-----|  
  | = | Weist den Ausdruck, der folgt, der Variablen. |  
  | += | Hinzufügen und zuweisen |   
  | -= | Subtraktion und Zuweisung |  
  | \*= | "Multiply" und zuweisen |  
  | /= | Division und Zuweisung |  
  | %= | Modulo und zuweisen |  
  | &= | Bitweises AND und Zuweisung |  
  | ^= | Bitweises XOR und Zuweisung |  
  | \|= | Bitweises OR und Zuweisung |  
  
 *expression*  
 Ist ein beliebiger gültiger [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md). Er enthält eine skalare Unterabfrage.  
  
## <a name="remarks"></a>Hinweise  
 SELECT @*Local_variable* wird normalerweise verwendet, um einen einzelnen Wert in die Variable zurückzugeben. Jedoch wenn *Ausdruck* ist der Name einer Spalte können sie mehrere Werte zurückgeben. Falls die SELECT-Anweisung mehr als einen Wert zurückgibt, wird der Variablen der zuletzt zurückgegebene Wert zugewiesen.  
  
 Wenn die SELECT-Anweisung keine Zeilen zurückgibt, behält die Variable ihren derzeitigen Wert bei. Wenn *Ausdruck* eine skalare Unterabfrage, gibt keinen Wert, der die Variable auf NULL festgelegt ist.  
  
 Eine SELECT-Anweisung kann mehrere lokale Variablen initialisieren.  
  
> [!NOTE]  
>  Eine SELECT-Anweisung, die eine Variablenzuweisung enthält, kann nicht zugleich zur Durchführung der normalen Abrufvorgänge für Resultsets verwendet werden.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-use-select-localvariable-to-return-a-single-value"></a>A. SELECT-Anweisung @local_variable auf einen einzelnen Wert zurückgeben  
 Das folgende Beispiel weist der Variable `@var1` den Wert `Generic Name` zu. Die Abfrage der Tabelle `Store` gibt keine Zeilen zurück, da der für `CustomerID` angegebene Wert nicht in der Tabelle enthalten ist. Die Variable behält den Wert `Generic Name` bei.  
  
```sql  
-- Uses AdventureWorks    
  
DECLARE @var1 varchar(30);         
SELECT @var1 = 'Generic Name';         
SELECT @var1 = Name         
FROM Sales.Store         
WHERE CustomerID = 1000 ;        
SELECT @var1 AS 'Company Name';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```  
 Company Name  
 ------------------------------  
 Generic Name  
 ```  
  
### <a name="b-use-select-localvariable-to-return-null"></a>B. SELECT-Anweisung @local_variable null zurückgegeben.  
 Das folgende Beispiel weist der Variable `@var1` mithilfe einer Unterabfrage einen Wert zu. Da der für `CustomerID` angeforderte Wert nicht vorhanden ist, gibt die Unterabfrage keinen Wert zurück, und die Variable wird auf `NULL` gesetzt.  
  
```sql  
-- Uses AdventureWorks  
  
DECLARE @var1 varchar(30)   
SELECT @var1 = 'Generic Name'   
SELECT @var1 = (SELECT Name   
FROM Sales.Store   
WHERE CustomerID = 1000)   
SELECT @var1 AS 'Company Name' ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Company Name  
----------------------------  
NULL  
```  
  
## <a name="see-also"></a>Siehe auch  
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [Expressions &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Zusammengesetzte Operatoren &#40; Transact-SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)  
  
  

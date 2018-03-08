---
title: '% (Modulo) (Transact-SQL) | Microsoft Docs'
ms.custom: 
ms.date: 03/15/2017
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
- modulo
- modulus
- '% (Modulo)'
- '% (Modulus)'
- MOD_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- '% (modulo operator)'
- '% (modulus operator)'
- remainder of division operation
- modulo operator (%)
- modulus operator (%)
ms.assetid: f93c662e-f405-486e-bf23-a2d03907b5bd
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 927b993e2b93ef670633ae1594c86178662ebabb
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="-modulus-transact-sql"></a>% (Modulus) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt den Rest der Division einer Zahl durch eine andere zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
dividend % divisor  
```  
  
## <a name="arguments"></a>Argumente  
 *dividend*  
 Der zu dividierende numerische Ausdruck. *Dividend* muss ein gültiger [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) von einem der Datentypen monetären Datentypkategorien für ganze Zahlen und oder der **numerischen** -Datentyp.  
  
 *divisor*  
 Ist der numerische Ausdruck, durch den der Dividend geteilt werden soll. *Divisor* muss jeder gültiger Ausdruck eines beliebigen monetären Datentypkategorien für ganze Zahlen und die Datentypen oder **numerischen** -Datentyp.  
  
## <a name="result-types"></a>Ergebnistypen  
 Die Ergebnistypen werden von den Datentypen der beiden Argumente bestimmt.  
  
## <a name="remarks"></a>Hinweise  
 Können Sie den modulo arithmetischen Operator in der Auswahlliste der SELECT-Anweisung mit einer beliebigen Kombination von Spaltennamen, numerischen Konstanten oder ein gültiger Ausdruck eines ganze Zahlen und Währungen geben Kategorien oder die **numerischen** Daten Geben Sie ein.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-simple-example"></a>A. Einfaches Beispiel  
 Im folgenden Beispiel wird die Zahl 38 durch 5 geteilt. Dies führt zu 7 als der ganzzahlige Teil des Ergebnisses, und veranschaulicht, wie der Rest 3 modulo zurückgegeben.  
  
```  
SELECT 38 / 5 AS Integer, 38 % 5 AS Remainder ;  
  
```  
  
### <a name="b-example-using-columns-in-a-table"></a>B. Beispiel für Spalten in einer Tabelle  
 Das folgende Beispiel gibt die Product ID, den Einzelpreis des Produkts und den Modulo (Rest) aus der Division des Preises jedes Produkts, konvertiert in eine ganze Zahl, durch die Anzahl der bestellten Produkte zurück.  
  
```  
-- Uses AdventureWorks  
  
SELECT TOP(100)ProductID, UnitPrice, OrderQty,  
   CAST((UnitPrice) AS int) % OrderQty AS Modulo  
FROM Sales.SalesOrderDetail;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-simple-example"></a>"C:" einfaches Beispiel  
 Das folgende Beispiel zeigt die Ergebnisse für die `%` Operator nach der Division von 3 durch 2.  
  
```  
-- Uses AdventureWorks  
  
SELECT TOP(1) 3%2 FROM dimEmployee;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
---------   
1         
```  
  
## <a name="see-also"></a>Siehe auch  
 [Integrierte Funktionen &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [Operators &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [% = &#40; Modulozuweisung &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/modulo-equals-transact-sql.md)   
 [Zusammengesetzte Operatoren &#40; Transact-SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)  
  
  



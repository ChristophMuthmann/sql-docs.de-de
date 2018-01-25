---
title: "[] (Platzhalterzeichen – zu suchende(s) Zeichen) (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 12/06/2016
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
- Match
- wildcard
- '[ ]'
- '[_]_TSQL'
dev_langs: TSQL
helpviewer_keywords:
- wildcard characters [SQL Server]
- '[ ] (wildcard - character(s) to match)'
ms.assetid: 57817576-0bf1-49ed-b05d-fac27e8fed7a
caps.latest.revision: "32"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 04fcf0d9e76db380430bfbf4c4ed6e5fadf14afb
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="--wildcard---characters-to-match-transact-sql"></a>\[\] (Platzhalterzeichen - Zeichen zur Übereinstimmung) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Entspricht einem beliebigen einzelnes Zeichen innerhalb des angegebenen Bereichs oder Satzes, der zwischen Klammern angegeben ist `[ ]`. Diese Platzhalterzeichen können verwendet werden, in Zeichenfolgenvergleichen, bei denen Mustervergleiche, z. B. `LIKE` und `PATINDEX`.  
  
## <a name="examples"></a>Beispiele  
### <a name="a-simple-example"></a>A: einfaches Beispiel   
Im folgende Beispiel gibt die Namen der mit dem Buchstaben `m`. `[n-z]`Gibt an, dass der zweite Buchstaben an einer beliebigen Stelle im Bereich von muss `n` auf `z`. Prozent-Platzhalter `%` sind alle oder keine Zeichen beginnend mit 3 Zeichen zulässig. Die `model` und `msdb` Datenbanken, die diese Kriterien erfüllen. Die `master` Datenbank nicht und wird aus dem Resultset ausgeschlossen.
 
```sql
SELECT name FROM sys.databases
WHERE name LIKE 'm[n-z]%';
```
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]  

```
name
-----
model
msdb
```   
 Sie müssen möglicherweise zusätzliche qualifizierende installierte Datenbanken.


### <a name="b-more-complex-example"></a>B: Beispiel komplexere   
 Im folgenden Beispiel wird mithilfe des []-Operators nach den IDs und Namen aller [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)]-Mitarbeiter gesucht, deren Adressen eine vierstellige Postleitzahl enthalten.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT e.BusinessEntityID, p.FirstName, p.LastName, a.PostalCode  
FROM HumanResources.Employee AS e  
INNER JOIN Person.Person AS p ON e.BusinessEntityID = p.BusinessEntityID  
INNER JOIN Person.BusinessEntityAddress AS ea ON e.BusinessEntityID = ea.BusinessEntityID  
INNER JOIN Person.Address AS a ON a.AddressID = ea.AddressID  
WHERE a.PostalCode LIKE '[0-9][0-9][0-9][0-9]';  
```  
  
 Im Folgenden wird das Resultset aufgeführt:  
  
```  
EmployeeID      FirstName      LastName      PostalCode  
----------      ---------      ---------     ----------  
290             Lynn           Tsoflias      3000  
```  



  
## <a name="see-also"></a>Siehe auch  
 [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [PATINDEX &#40;Transact-SQL&#41;](../../t-sql/functions/patindex-transact-sql.md)   
  [% &#40; Platzhalter - Zeichen &#40; s &#41; Übereinstimmung &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/percent-character-wildcard-character-s-to-match-transact-sql.md)   
 [&#91; ^ &#93; &#40; Platzhalter - Zeichen &#40; s &#41; Nicht in Übereinstimmung &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)     
 [\_&#40; Platzhalterzeichen - einzelnes zu suchendes Zeichen &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)  
    
  

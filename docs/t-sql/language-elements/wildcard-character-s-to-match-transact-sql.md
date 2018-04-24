---
title: '[ ] (Platzhalterzeichen – zu suchende(s) Zeichen) (Transact-SQL) | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 12/06/2016
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
- Match
- wildcard
- '[ ]'
- '[_]_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- wildcard characters [SQL Server]
- '[ ] (wildcard - character(s) to match)'
ms.assetid: 57817576-0bf1-49ed-b05d-fac27e8fed7a
caps.latest.revision: 32
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 975848a7434badb238b91175cf29e5bfe09843cc
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="--wildcard---characters-to-match-transact-sql"></a>\[ \] (Platzhalterzeichen – zu suchende(s) Zeichen) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Entspricht jedem einzelnen Zeichen im Bereich oder der Menge, der bzw. die innerhalb der Klammern `[ ]` angegeben ist. Diese Platzhalterzeichen können in Zeichenfolgenvergleichen verwendet werden, bei denen Mustervergleiche wie `LIKE` und `PATINDEX` durchgeführt werden.  
  
## <a name="examples"></a>Beispiele  
### <a name="a-simple-example"></a>A: Einfaches Beispiel   
Im folgenden Beispiel werden Namen zurückgegeben, die mit dem Buchstaben `m` beginnen. `[n-z]` legt fest, dass der zweite Buchstaben zwischen `n` und `z` liegen muss. Durch das Prozent-Platzhalterzeichen `%` wird angegeben, dass auf das zweite Zeichen entweder kein weiteres Zeichen oder beliebige Zeichen folgen können. Die Datenbanken `model` und `msdb` erfüllen diese Kriterien. Die `master`-Datenbank erfüllt dieses Kriterium nicht und wird aus dem Resultset ausgeschlossen.
 
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
 Möglicherweise haben Sie aber zusätzliche qualifizierende Datenbanken installiert.


### <a name="b-more-complex-example"></a>B: Komplexeres Beispiel   
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



  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [PATINDEX &#40;Transact-SQL&#41;](../../t-sql/functions/patindex-transact-sql.md)   
  [% &#40;Wildcard - Character&#40;s&#41; to Match&#41; &#40;Transact-SQL&#41; (% (Platzhalterzeichen – zu suchende(s) Zeichen) (Transact-SQL))](../../t-sql/language-elements/percent-character-wildcard-character-s-to-match-transact-sql.md)   
 [&#91;^&#93; &#40;Wildcard - Character&#40;s&#41; Not to Match&#41; &#40;Transact-SQL&#41; ([^] (Platzhalterzeichen – nicht zu suchende(s) Zeichen) (Transact-SQL))](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)     
 [\_ &#40;Wildcard - Match One Character&#41; &#40;Transact-SQL&#41; (_ (Platzhalterzeichen – einzelnes zu suchendes Zeichen) (Transact-SQL))](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)  
    
  

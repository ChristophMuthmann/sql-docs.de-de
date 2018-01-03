---
title: _ (Platzhalterzeichen-einzelnes zu suchendes Zeichen) (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 12/06/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server (starting with 2008)
f1_keywords:
- Match
- wildcard
- _TSQL
- Match One
- _
dev_langs: TSQL
helpviewer_keywords:
- wildcard characters [SQL Server]
- _ (wildcard - match one character)
ms.assetid: 11a2ed36-9e21-4bdf-ae20-a31db1434b97
caps.latest.revision: "33"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 63f4d48f77556f04f1d9d2c3c381afd859a7c240
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/02/2018
---
# <a name="-wildcard---match-one-character-transact-sql"></a>_ (Platzhalterzeichen - einzelnes zu suchendes Zeichen) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Verwenden Sie den Unterstrich _ mit jedem beliebigen einzelnes Zeichen in einem Zeichenfolgenvergleich übereinstimmen, den Mustervergleich, z. B. umfasst `LIKE` und `PATINDEX`.  
  
## <a name="examples"></a>Beispiele  

## <a name="a-simple-example"></a>A: einfaches Beispiel   

Das folgende Beispiel gibt alle Datenbank-Name mit dem Buchstaben beginnt `m` und haben den Buchstaben `d` als dritten Buchstaben. Der Unterstrich gibt an, dass das zweite Zeichen des Namens beliebigen Buchstaben kann. Die `model` und `msdb` Datenbanken, die diese Kriterien erfüllen. Die `master` Datenbank nicht vorhanden.

```sql
SELECT name FROM sys.databases
WHERE name LIKE 'm_d%';
```   
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   
```
name
-----
model
msdb
```   
Sie müssen möglicherweise zusätzliche Datenbanken verbunden werden, die diese Kriterien erfüllen.

Mehrere Unterstriche können Sie mehrere Zeichen darstellen. Ändern der `LIKE` Kriterien zwei Unterstriche `'m__%` schließt den master-Datenbank in das Ergebnis.

### <a name="b-more-complex-example"></a>B: Beispiel komplexere
 Im folgenden Beispiel wird den Operator _ finden aller Personen in der `Person` -Tabelle verwendet, die einen drei Buchstaben bestehenden Vornamen haben, die mit enden `an`.  
  
```sql  
-- USE AdventureWorks2012
  
SELECT FirstName, LastName  
FROM Person.Person  
WHERE FirstName LIKE '_an'  
ORDER BY FirstName;  
```  
## <a name="c-escaping-the-underscore-character"></a>"C:" Escapezeichen Unterstrich   
Das folgende Beispiel gibt die Namen von festen Datenbankrollen wie `db_owner` und `db_ddladmin`, aber sie gibt überdies die `dbo` Benutzer. 

```sql
SELECT name FROM sys.database_principals
WHERE name LIKE 'db_%';
```

Der Unterstrich in der dritten Zeichenposition stammt als Platzhalter, und ist nicht für nur Prinzipale, die beginnend mit den Buchstaben gefiltert `db_`. Escapezeichen für der Unterstrich Einschließung in Klammern `[_]`. 

```sql
SELECT name FROM sys.database_principals
WHERE name LIKE 'db[_]%';
```   
Jetzt die `dbo` Benutzer ausgeschlossen wird.   
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   
```
name
-------------
db_owner
db_accessadmin
db_securityadmin
...
```

  
## <a name="see-also"></a>Siehe auch  
 [WIE &#40; Transact-SQL &#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [PATINDEX &#40; Transact-SQL &#41;](../../t-sql/functions/patindex-transact-sql.md)   
  [% (Platzhalterzeichen – zu suchende(s) Zeichen)](../../t-sql/language-elements/percent-character-wildcard-character-s-to-match-transact-sql.md)   
  [&#91; &#93; (Platzhalterzeichen – zu suchende(s) Zeichen)](../../t-sql/language-elements/wildcard-character-s-to-match-transact-sql.md)   
 [&#91; ^ &#93; (Platzhalterzeichen - nicht zu suchende(s) Zeichen)](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)     
  

---
title: _ (Platzhalterzeichen – einzelnes zu suchendes Zeichen) (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 12/06/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|language-elements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
dev_langs:
- TSQL
helpviewer_keywords:
- wildcard characters [SQL Server]
- _ (wildcard - match one character)
ms.assetid: 11a2ed36-9e21-4bdf-ae20-a31db1434b97
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: e978feab83e4be2f49281200d69a947320076eea
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="-wildcard---match-one-character-transact-sql"></a>_ (Platzhalterzeichen - einzelnes zu suchendes Zeichen) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Verwenden Sie den Unterstrich _ zum Abgleichen eines beliebigen einzelnen Zeichen bei einem Zeichenfolgenvergleich, der einen Mustervergleich wie `LIKE` oder `PATINDEX` umfasst.  
  
## <a name="examples"></a>Beispiele  

## <a name="a-simple-example"></a>A: Einfaches Beispiel   

Das folgende Beispiel gibt alle Datenbanknamen zurück, die mit dem Buchstaben `m` beginnen und `d` als dritten Buchstaben haben. Der Unterstrich gibt an, dass das zweite Zeichen ein beliebiger Buchstabe sein kann. Die Datenbanken `model` und `msdb` erfüllen diese Kriterien. Die Datenbank `master` erfüllt die Kriterien nicht.

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
Sie verfügen möglicherweise über zusätzliche Datenbanken, die diese Kriterien erfüllen.

Mehrere Unterstriche können mehrere Zeichen darstellen. Wenn Sie die `LIKE`-Kriterien ändern, um zwei Unterstriche einzuschließen, fügt `'m__%` dem Ergebnis die Masterdatenbank hinzu.

### <a name="b-more-complex-example"></a>B: Komplexeres Beispiel
 Im folgenden Beispiel wird der Operator _ zum Suchen aller Personen in der `Person`-Tabelle verwendet, die über einen aus drei Buchstaben bestehenden Vornamen verfügen, der auf `an` endet.  
  
```sql  
-- USE AdventureWorks2012
  
SELECT FirstName, LastName  
FROM Person.Person  
WHERE FirstName LIKE '_an'  
ORDER BY FirstName;  
```  
## <a name="c-escaping-the-underscore-character"></a>C: Versehen von Unterstrichen mit Escapezeichen   
Im folgenden Beispiel werden die Namen von festen Datenbankrollen wie `db_owner` und `db_ddladmin` zurückgegeben, aber auch der Benutzer `dbo`. 

```sql
SELECT name FROM sys.database_principals
WHERE name LIKE 'db_%';
```

Der Unterstrich an der dritten Zeichenposition wird als Platzhalter verwendet und filtert nicht nur nach Prinzipalen, die mit den Buchstaben `db_` beginnen. Setzen Sie den Unterstrich in Klammern (`[_]`), um ihn mit dem Escapezeichen zu versehen. 

```sql
SELECT name FROM sys.database_principals
WHERE name LIKE 'db[_]%';
```   
Jetzt wird der Benutzer `dbo` ausgeschlossen.   
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   
```
name
-------------
db_owner
db_accessadmin
db_securityadmin
...
```

  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [PATINDEX &#40;Transact-SQL&#41;](../../t-sql/functions/patindex-transact-sql.md)   
  [% (Platzhalterzeichen – zu suchende(s) Zeichen)](../../t-sql/language-elements/percent-character-wildcard-character-s-to-match-transact-sql.md)   
  [&#91; &#93; (Wildcard - Character(s) to Match) ([ ] (Platzhalterzeichen – zu suchende[s] Zeichen))](../../t-sql/language-elements/wildcard-character-s-to-match-transact-sql.md)   
 [&#91;^&#93; (Wildcard - Character(s) Not to Match) ([^] (Platzhalterzeichen – nicht zu suchende[s] Zeichen))](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)     
  

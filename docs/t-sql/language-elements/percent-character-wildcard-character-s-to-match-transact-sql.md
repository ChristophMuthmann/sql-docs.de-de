---
title: "Prozentzeichen (Platzhalterzeichen – zu suchende(s) Zeichen) (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 12/06/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- Azure SQL Data Warehouse
- Azure SQL Database
- SQL Server (starting with 2008)
f1_keywords:
- '%'
- '%_TSQL'
- wildcard
dev_langs:
- TSQL
helpviewer_keywords:
- conditions [SQL Server], wildcards
- '% (wildcard - character(s) to match)'
- matching conditions [SQL Server]
- wildcard characters [SQL Server]
- characters [SQL Server], wildcard
ms.assetid: d4cbc1a9-37e1-4101-97fb-e6ac30c1223e
caps.latest.revision: 23
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 63891f4f25781d1a4e7f169d42c4db779d5a9c12
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="percent-character-wildcard---characters-to-match-transact-sql"></a>Prozentzeichen (Platzhalterzeichen - zu suchende(s) Zeichen) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Entspricht einer Zeichenfolge aus null oder mehr Zeichen. Dieser Platzhalter kann entweder als Präfix oder Suffix verwendet werden.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden alle Vornamen der Personen in der `Person`-Tabelle von `AdventureWorks2012` zurückgegeben, die mit `Dan` beginnen.  
  
```  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName  
FROM Person.Person  
WHERE FirstName LIKE 'Dan%';  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [WIE &#40; Transact-SQL &#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [Operatoren &#40; Transact-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [Ausdrücke &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
 [&#91; &#93; (Platzhalterzeichen – zu suchende(s) Zeichen)](../../t-sql/language-elements/wildcard-character-s-to-match-transact-sql.md)   
  [&#91; ^ &#93; (Platzhalterzeichen - nicht zu suchende(s) Zeichen)](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)     
 [_ (Platzhalterzeichen-einzelnes zu suchendes Zeichen)](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)  
    
  


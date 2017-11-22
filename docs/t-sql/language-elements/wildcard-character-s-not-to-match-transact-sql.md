---
title: '[^] (Platzhalterzeichen - nicht zu suchende(s) Zeichen) (Transact-SQL) | Microsoft Docs'
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
- wildcard
- '[^]_TSQL'
- '[^]'
- Not Match
dev_langs: TSQL
helpviewer_keywords:
- wildcard characters [SQL Server]
- '[^] (wildcard - character(s) not to match)'
ms.assetid: b970038f-f4e7-4a5d-96f6-51e3248c6aef
caps.latest.revision: "36"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: d80ac01fe5fbfcfce5da1a60acc15ab1b76bda70
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="-wildcard---characters-not-to-match-transact-sql"></a>\[^\](Platzhalterzeichen - nicht zu suchende(s) Zeichen) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Entspricht einem einzelnen Zeichen, das nicht dem Bereich oder der Menge angehört, der bzw. die zwischen den eckigen Klammern angegeben ist.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird der [^]-Operator verwendet, um alle Personen in der `Contact`-Tabelle zu suchen, deren Vorname mit `Al` beginnt und als dritten Buchstaben nicht den Buchstaben `a` besitzt.  
  
```  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName  
FROM Person.Person  
WHERE FirstName LIKE 'Al[^a]%'  
ORDER BY FirstName;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [WIE &#40; Transact-SQL &#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [PATINDEX &#40; Transact-SQL &#41;](../../t-sql/functions/patindex-transact-sql.md)   
 [% &#40; Platzhalter - Zeichen &#40; s &#41; Übereinstimmung &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/percent-character-wildcard-character-s-to-match-transact-sql.md)   
  [&#91; &#93; &#40; Platzhalter - Zeichen &#40; s &#41; Übereinstimmung &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/wildcard-character-s-to-match-transact-sql.md)   
 [\_&#40; Platzhalterzeichen - einzelnes zu suchendes Zeichen &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)  
  
  

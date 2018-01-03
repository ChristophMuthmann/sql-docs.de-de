---
title: TRIM (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 01/20/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- TRIM
- TRIM_TSQL
dev_langs: TSQL
helpviewer_keywords: TRIM function
ms.assetid: a00245aa-32c7-4ad4-a0d1-64f3d6841153
caps.latest.revision: "4"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: b7ea9bb6828182ee0cbc5d0ebef1065564bf03df
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/02/2018
---
# <a name="trim-transact-sql"></a>TRIM (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

Entfernt das Leerzeichen `char(32)` oder andere angegebene Zeichen am Anfang oder Ende einer Zeichenfolge.  
 
## <a name="syntax"></a>Syntax   
```
TRIM ( [ characters FROM ] string ) 
```
[//]: # "[SOWOHL | FÜHRENDE | NACHFOLGENDE] nicht noch verfügbar."

## <a name="arguments"></a>Argumente   

Buchstaben   
Ist ein Literal, eine Variable oder ein Funktionsaufruf eines beliebigen Typs nicht-LOB-Zeichen (`nvarchar`, `varchar`, `nchar`, oder `char`), enthält Zeichen, die entfernt werden soll. `nvarchar(max)`und `varchar(max)` Typen sind nicht zulässig.

Zeichenfolge   
Ist ein Ausdruck eines beliebigen Typs Zeichen (`nvarchar`, `varchar`, `nchar`, oder `char`), in denen Zeichen entfernt werden soll.

## <a name="return-types"></a>Rückgabetypen   
Gibt einen Zeichenausdruck mit einem Zeichenfolgenargument zurück, in dem das Leerzeichen `char(32)` oder anderen angegebenen Zeichen werden auf beiden Seiten entfernt. Gibt `NULL` Wenn Eingabezeichenfolge `NULL`.

## <a name="remarks"></a>Hinweise   
Standardmäßig `TRIM` -Funktion entfernt das Leerzeichen `char(32)` auf beiden Seiten. Dieser entspricht `LTRIM(RTRIM(@string))`. Verhalten des `TRIM ` -Funktion mit dem angegebenen Zeichen ist identisch mit dem Verhalten der `REPLACE` Funktion, wobei die Zeichen vom Anfang oder Ende mit leeren Zeichenfolgen ersetzt werden.


## <a name="examples"></a>Beispiele
### <a name="a--removes-the-space-character-from-both-sides-of-string"></a>A.  Entfernt das Leerzeichen auf beiden Seiten der Zeichenfolge   
Im folgende Beispiel entfernt Leerzeichen vor und nach dem Wort `test`.   
```sql
SELECT TRIM( '     test    ') AS Result;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   

`test`


### <a name="b--removes-specified-characters-from-both-sides-of-string"></a>B.  Entfernt den angegebenen Zeichen auf beiden Seiten der Zeichenfolge   
Im folgende Beispiel werden Punkt und nachfolgende Leerzeichen entfernt.
```sql
SELECT TRIM( '.,! ' FROM  '#     test    .') AS Result;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   
`#     test`


## <a name="see-also"></a>Siehe auch
[Zeichenfolgenfunktionen (Transact-SQL)](../../t-sql/functions/string-functions-transact-sql.md)   
[LTRIM (Transact-SQL)](../../t-sql/functions/ltrim-transact-sql.md)   
[RTRIM (Transact-SQL)](../../t-sql/functions/rtrim-transact-sql.md)   
[REPLACE (Transact-SQL)](../../t-sql/functions/replace-transact-sql.md)   

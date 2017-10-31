---
title: Zeichenfolgenfunktionen (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/15/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- functions [SQL Server], strings
- strings [SQL Server], functions
- string functions
- strings [SQL Server]
ms.assetid: 6940a83d-5374-4af3-bb27-5d89c8af83ac
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 33df9a7082ee7e637b60e3a1ca7911e127040a08
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="string-functions-transact-sql"></a>Zeichenfolgenfunktionen (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Die folgenden Skalarfunktionen verarbeiten Zeichenfolgen-Eingabewerte und geben einen numerischen Wert oder eine Zeichenfolge zurück:  
  
||||  
|-|-|-| 
|[ASCII](../../t-sql/functions/ascii-transact-sql.md)|[CHAR](../../t-sql/functions/char-transact-sql.md)|[CHARINDEX](../../t-sql/functions/charindex-transact-sql.md)|
|[CONCAT](../../t-sql/functions/concat-transact-sql.md)|[CONCAT_WS](../../t-sql/functions/concat-ws-transact-sql.md)|[UNTERSCHIED](../../t-sql/functions/difference-transact-sql.md) |
|[FORMAT](../../t-sql/functions/format-transact-sql.md)|[LEFT](../../t-sql/functions/left-transact-sql.md)|[LEN](../../t-sql/functions/len-transact-sql.md) |
|[NIEDRIGERE](../../t-sql/functions/lower-transact-sql.md)|[LTRIM](../../t-sql/functions/ltrim-transact-sql.md)|[NCHAR](../../t-sql/functions/nchar-transact-sql.md) |
|[PATINDEX](../../t-sql/functions/patindex-transact-sql.md)|[QUOTENAME](../../t-sql/functions/quotename-transact-sql.md)|[REPLACE](../../t-sql/functions/replace-transact-sql.md) |
|[REPLIZIEREN](../../t-sql/functions/replicate-transact-sql.md)|[REVERSE](../../t-sql/functions/reverse-transact-sql.md) |[RIGHT](../../t-sql/functions/right-transact-sql.md) |
|[RTRIM](../../t-sql/functions/rtrim-transact-sql.md)|[SOUNDEX](../../t-sql/functions/soundex-transact-sql.md) |[SPEICHERPLATZ](../../t-sql/functions/space-transact-sql.md) |
|[STR](../../t-sql/functions/str-transact-sql.md)|[STRING_AGG](../../t-sql/functions/string-agg-transact-sql.md)|[STRING_ESCAPE](../../t-sql/functions/string-escape-transact-sql.md) |
|[STRING_SPLIT](../../t-sql/functions/string-split-transact-sql.md)|[STUFF](../../t-sql/functions/stuff-transact-sql.md)|[SUBSTRING](../../t-sql/functions/substring-transact-sql.md) |
|[ÜBERSETZEN](../../t-sql/functions/translate-transact-sql.md)|[ZUSCHNEIDEN](../../t-sql/functions/trim-transact-sql.md)|[UNICODE](../../t-sql/functions/unicode-transact-sql.md) |
|[OBERE](../../t-sql/functions/upper-transact-sql.md) | | |


  
 Alle integrierten Zeichenfolgenfunktionen außer `FORMAT` sind deterministisch. Das bedeutet, dass sie stets denselben Wert zurückgeben, wenn sie mit bestimmten Eingabewerten aufgerufen werden. Weitere Informationen zum Funktionsdeterminismus finden Sie unter [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
 Wenn an Zeichenfolgenfunktionen Argumente übergeben werden, die keine Zeichenfolgenwerte sind, wird der Eingabetyp implizit in einen Textdatentyp konvertiert. Weitere Informationen finden Sie unter [Datentypkonvertierung &#40; Datenbankmodul &#41;](../../t-sql/data-types/data-type-conversion-database-engine.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Integrierte Funktionen &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)  
  
  



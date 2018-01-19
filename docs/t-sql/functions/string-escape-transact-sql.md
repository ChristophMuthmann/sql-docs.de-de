---
title: STRING_ESCAPE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 02/25/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STRING_ESCAPE
- STRING_ESCAPE_TSQL
dev_langs: TSQL
helpviewer_keywords: STRING_ESCAPE function
ms.assetid: 2163bc7a-3816-4304-9c40-8954804f5465
caps.latest.revision: "11"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: f850839d54f5a1e4d58277524b1f2d35b56c7b4e
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="stringescape-transact-sql"></a>STRING_ESCAPE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Schützt Sonderzeichen in Texte und gibt Text mit Escapezeichen zurück. **STRING_ESCAPE** ist eine deterministische Funktion.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
STRING_ESCAPE( text , type )  
```  
  
## <a name="arguments"></a>Argumente  
 *text*  
 Ist eine **Nvarchar**[Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) Ausdruck, der das Objekt, das mit Escapezeichen versehen werden sollten darstellt.  
  
 *type*  
 Escape-Regeln, die angewendet werden. Derzeit wird ein Wert unterstützt `'json'`.  
  
## <a name="return-types"></a>Rückgabetypen  
 **nvarchar(max)** Text mit Escapezeichen besondere und Steuerzeichen. Derzeit **STRING_ESCAPE** können nur Escapesonderzeichen JSON in der folgenden Tabelle gezeigt.  
  
|Sonderzeichen|Codierte Sequenz|  
|-----------------------|----------------------|  
|Anführungszeichen (")|\\"|  
|umgekehrter Schrägstrich (\\)|\\\|  
|Schrägstrich (/)|\\/|  
|Rücktaste|\b|  
|Seitenvorschub|\f|  
|Neue Zeile|\n|  
|Wagenrücklauf|\r|  
|Horizontaler Tabstopp|\t|  
  
|Steuerzeichen|Codierte Sequenz|  
|-----------------------|----------------------|  
|CHAR(0)|\u0000|  
|CHAR(1)|\u0001|  
|...|...|  
|CHAR(31)|\u001f|  
  
## <a name="remarks"></a>Hinweise  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a--escape-text-according-to-the-json-formatting-rules"></a>A.  Escape-Text entsprechend der JSON-Formatierungsregeln  
 Die folgende Abfrage schützt Sonderzeichen, die mithilfe von JSON-Regeln und geschützter Text zurückgegeben.  
  
```  
SELECT STRING_ESCAPE('\   /  
\\    "     ', 'json') AS escapedText;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
escapedText  
-------------------------------------------------------------  
\\\t\/\n\\\\\t\"\t
```  
  
### <a name="b-format-json-object"></a>B. Format JSON-Objekt  
 Die folgende Abfrage erstellt ein JSON-Text aus der Variablen "Anzahl" und "Zeichenfolge und umgeht alle JSON Sonderzeichen in der Variablen.  
  
```  
SET @json = FORMATMESSAGE('{ "id": %d,"name": "%s", "surname": "%s" }',   
    17, STRING_ESCAPE(@name,'json'), STRING_ESCAPE(@surname,'json') );  
```  
  
## <a name="see-also"></a>Siehe auch  
 [CONCAT &#40;Transact-SQL&#41;](../../t-sql/functions/concat-transact-sql.md)  
 [CONCAT_WS &#40;Transact-SQL&#41;](../../t-sql/functions/concat-ws-transact-sql.md)  
 [FORMATMESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/formatmessage-transact-sql.md)  
 [QUOTENAME &#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)  
 [REPLACE &#40;Transact-SQL&#41;](../../t-sql/functions/replace-transact-sql.md)  
 [REVERSE &#40;Transact-SQL&#41;](../../t-sql/functions/reverse-transact-sql.md)  
 [STRING_AGG &#40;Transact-SQL&#41;](../../t-sql/functions/string-agg-transact-sql.md)  
 [STUFF &#40;Transact-SQL&#41;](../../t-sql/functions/stuff-transact-sql.md)  
 [TRANSLATE &#40;Transact-SQL&#41;](../../t-sql/functions/translate-transact-sql.md)  
 [Zeichenfolgenfunktionen &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)   
  
  

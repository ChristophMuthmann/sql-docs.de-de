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
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STRING_ESCAPE
- STRING_ESCAPE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STRING_ESCAPE function
ms.assetid: 2163bc7a-3816-4304-9c40-8954804f5465
caps.latest.revision: 11
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 41f969e292eff76c9a836ccd3177519d88e355ac
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

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
 [Zeichenfolgenfunktionen &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [TEILZEICHENFOLGE &#40; Transact-SQL &#41;](../../t-sql/functions/substring-transact-sql.md)  
  
  


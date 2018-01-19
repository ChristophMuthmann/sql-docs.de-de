---
title: QUOTENAME (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- QUOTENAME_TSQL
- QUOTENAME
dev_langs: TSQL
helpviewer_keywords:
- delimited identifiers [SQL Server]
- input strings [SQL Server]
- Unicode [SQL Server], delimited identifiers
- QUOTENAME function
- valid identifiers [SQL Server]
ms.assetid: 34d47f1e-2ac7-4890-8c9c-5f60f115e076
caps.latest.revision: "35"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 701d229ae745cee4a237f35b69cd00e899d5c6a5
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="quotename-transact-sql"></a>QUOTENAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt eine Unicode-Zeichenfolge mit hinzugefügten Trennzeichen zurück, sodass die Eingabezeichenfolge ein gültiger [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Begrenzungsbezeichner wird.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
QUOTENAME ( 'character_string' [ , 'quote_character' ] )   
```  
  
## <a name="arguments"></a>Argumente  
 '*character_string*'  
 Eine Zeichenfolge von Unicode-Zeichendaten. *Character_string* ist **Sysname** und ist auf 128 Zeichen beschränkt. Eingaben, die größer als 128 Zeichen sind, geben NULL zurück.  
  
 '*quote_character*'  
 Eine Zeichenfolge mit einem Zeichen, das als Trennzeichen verwendet wird. Kann ein einfaches Anführungszeichen ( **"** ), eine linke oder rechte Klammer ( **[]** ), oder ein doppeltes Anführungszeichen ( **"** ). Wenn *Quote_character* nicht angegeben ist, werden Klammern verwendet werden.  
  
## <a name="return-types"></a>Rückgabetypen  
 **nvarchar(258)**  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird mit der Zeichenfolge `abc[]def` und den Zeichen `[` und `]` ein gültiger [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Begrenzungsbezeichner erstellt.  
  
```  
SELECT QUOTENAME('abc[]def');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
[abc[]]def]  
  
(1 row(s) affected)  
```  
  
 Beachten Sie, dass die rechte Klammer in der Zeichenfolge `abc[]def` verdoppelt wurde, um ein Escapezeichen anzugeben.  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 Im folgenden Beispiel wird mit der Zeichenfolge `abc def` und den Zeichen `[` und `]` ein gültiger [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Begrenzungsbezeichner erstellt.  
  
```  
SELECT QUOTENAME('abc def');   
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
[abc def]  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Siehe auch  
 [PARSENAME &#40;Transact-SQL&#41;](../../t-sql/functions/parsename-transact-sql.md)  
 [CONCAT &#40;Transact-SQL&#41;](../../t-sql/functions/concat-transact-sql.md)  
 [CONCAT_WS &#40;Transact-SQL&#41;](../../t-sql/functions/concat-ws-transact-sql.md)  
 [FORMATMESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/formatmessage-transact-sql.md)  
 [REPLACE &#40;Transact-SQL&#41;](../../t-sql/functions/replace-transact-sql.md)  
 [REVERSE &#40;Transact-SQL&#41;](../../t-sql/functions/reverse-transact-sql.md)  
 [STRING_AGG &#40;Transact-SQL&#41;](../../t-sql/functions/string-agg-transact-sql.md)  
 [STRING_ESCAPE &#40;Transact-SQL&#41;](../../t-sql/functions/string-escape-transact-sql.md)  
 [STUFF &#40;Transact-SQL&#41;](../../t-sql/functions/stuff-transact-sql.md)  
 [TRANSLATE &#40;Transact-SQL&#41;](../../t-sql/functions/translate-transact-sql.md)  
 [Zeichenfolgenfunktionen &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  


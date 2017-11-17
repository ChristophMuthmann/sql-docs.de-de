---
title: REPLACE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/23/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- REPLACE_TSQL
- REPLACE
dev_langs:
- TSQL
helpviewer_keywords:
- first string expression [SQL Server]
- replacing string expression
- third string expressions [SQL Server]
- second string expressions [SQL Server]
- REPLACE function
ms.assetid: 8a7aaaf2-62e3-46c0-8e44-fa22290dd86b
caps.latest.revision: 39
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8340c1b3af3ad843a0e3080cbfdc771d7353c7b7
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="replace-transact-sql"></a>REPLACE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Ersetzt alle Vorkommen eines angegebenen Zeichenfolgenwerts durch einen anderen Zeichenfolgenwert.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
REPLACE ( string_expression , string_pattern , string_replacement )  
```  
  
## <a name="arguments"></a>Argumente  
 *string_expression*  
 Die Zeichenfolge [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) , gesucht werden soll. *String_expression* kann von einem Zeichen-oder Binärdatentyp sein.  
  
 *String_*Muster  
 Ist der zu suchende Teilzeichenfolge an. *String_pattern* kann von einem Zeichen-oder Binärdatentyp sein. *String_pattern* darf keine leere Zeichenfolge (") sein und darf nicht die maximale Anzahl von Bytes, die auf eine Seite passen.  
  
 *String_*Ersatz  
 Ist die Ersatzzeichenfolge. *String_replacement* kann von einem Zeichen-oder Binärdatentyp sein.  
  
## <a name="return-types"></a>Rückgabetypen  
 Gibt **Nvarchar** die Eingabeargumente des ist die **Nvarchar** Daten geben; andernfalls wird von REPLACE gibt **Varchar**.  
  
 Gibt NULL zurück, wenn eines der Argumente NULL ist.  
  
 Wenn *String_expression* ist nicht vom Typ **varchar(max)** oder **nvarchar(max) ersetzen** schneidet den Rückgabewert bei 8.000 Bytes ab. Zum Zurückgeben von Werten über 8.000 Bytes *String_expression* müssen explizit in einen Datentyp mit umfangreichen Werten umgewandelt werden.  
  
## <a name="remarks"></a>Hinweise  
 REPLACE führt Vergleiche auf der Basis der Sortierung der Eingabe durch. Um einen Vergleich in einer angegebenen Sortierung durchzuführen, können Sie [COLLATE](~/t-sql/statements/collations.md) eine ausdrückliche Sortierung auf die Eingabe anwenden.  
  
 0 x 0000 (**char(0) zurück**) ist ein nicht definiertes Zeichen in Windows-Sortierungen und kann nicht in REPLACE enthalten sein.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel ersetzt die Zeichenfolge `cde` in `abcdefghi` durch `xxx`.  
  
```sql  
SELECT REPLACE('abcdefghicde','cde','xxx');  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
------------  
abxxxfghixxx  
(1 row(s) affected)  
```  
  
 Das folgende Beispiel verwendet die `COLLATE`-Funktion.  
  
```sql  
SELECT REPLACE('This is a Test'  COLLATE Latin1_General_BIN,  
'Test', 'desk' );  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
------------  
This is a desk  
(1 row(s) affected)  
```  

  
## <a name="see-also"></a>Siehe auch  
 [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Zeichenfolgenfunktionen &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  


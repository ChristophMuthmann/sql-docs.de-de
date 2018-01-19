---
title: REVERSE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/13/2017
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
- REVERSE_TSQL
- REVERSE
dev_langs: TSQL
helpviewer_keywords:
- expressions [SQL Server], reverse
- REVERSE function
- reverse character expressions
ms.assetid: 555d8877-7cc7-4955-ae2c-6215aca313b7
caps.latest.revision: "46"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: c14fb9f1e0f6e7b3f0cb224036af37e6a7b19e23
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="reverse-transact-sql"></a>REVERSE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt einen Zeichenfolgenwert in umgekehrter Reihenfolge zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
REVERSE ( string_expression )  
```  
  
## <a name="arguments"></a>Argumente  
 *string_expression*  
 *String_expression* ist ein [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) eines Datentyps Zeichenfolgen- oder Binärdatentyps. *String_expression* kann eine Konstante, Variable oder Spalte mit Zeichen- oder Binärdaten sein.  
  
## <a name="return-types"></a>Rückgabetypen  
 **Varchar** oder **Nvarchar**  
  
## <a name="remarks"></a>Hinweise  
 *String_expression* muss einen Datentyp, der implizit in **Varchar**. Verwenden Sie andernfalls [Umwandlung](../../t-sql/functions/cast-and-convert-transact-sql.md) zur expliziten Konvertierung *String_expression*.  
  
## <a name="supplementary-characters-surrogate-pairs"></a>Ergänzende Zeichen (Ersatzpaare)  
 Wenn Sie SC-Sortierungen verwenden, kehrt die REVERSE-Funktion die Reihenfolge der beiden Hälften eines Ersatzzeichenpaars nicht um.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden die Vornamen aller Kontakte mit den Zeichen in umgekehrter Reihenfolge zurückgegeben. In diesem Beispiel wird die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank verwendet.  
  
```  
SELECT FirstName, REVERSE(FirstName) AS Reverse  
FROM Person.Person  
WHERE BusinessEntityID < 5  
ORDER BY FirstName;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
FirstName      Reverse
-------------- --------------
Ken            neK
Rob            boR
Roberto        otreboR
Terri          irreT

(4 row(s) affected)
```  
  
 Im folgenden Beispiel werden die Zeichen in einer Variablen umgekehrt.  
  
```  
DECLARE @myvar varchar(10);  
SET @myvar = 'sdrawkcaB';  
SELECT REVERSE(@myvar) AS Reversed ;  
GO  
```  
  
 Im folgenden Beispiel wird eine implizite Konvertierung von einer **Int** -Datentyp in **Varchar** -Datentyp, und klicken Sie dann das Ergebnis umgekehrt.  
  
```  
SELECT REVERSE(1234) AS Reversed ;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 Das folgende Beispiel gibt die Namen aller Datenbanken, und die Namen mit den Zeichen rückgängig gemacht.  
  
```  
SELECT name, REVERSE(name) FROM sys.databases;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [CONCAT &#40;Transact-SQL&#41;](../../t-sql/functions/concat-transact-sql.md)  
 [CONCAT_WS &#40;Transact-SQL&#41;](../../t-sql/functions/concat-ws-transact-sql.md)  
 [FORMATMESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/formatmessage-transact-sql.md)  
 [QUOTENAME &#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)  
 [REPLACE &#40;Transact-SQL&#41;](../../t-sql/functions/replace-transact-sql.md)  
 [STRING_AGG &#40;Transact-SQL&#41;](../../t-sql/functions/string-agg-transact-sql.md)  
 [STRING_ESCAPE &#40;Transact-SQL&#41;](../../t-sql/functions/string-escape-transact-sql.md)  
 [STUFF &#40;Transact-SQL&#41;](../../t-sql/functions/stuff-transact-sql.md)  
 [TRANSLATE &#40;Transact-SQL&#41;](../../t-sql/functions/translate-transact-sql.md)  
 [CAST und CONVERT &#40; Transact-SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Zeichenfolgenfunktionen &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  


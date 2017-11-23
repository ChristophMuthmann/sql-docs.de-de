---
title: STUFF (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 11/17/2017
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
- STUFF
- STUFF_TSQL
dev_langs: TSQL
helpviewer_keywords:
- deleting characters
- STUFF function
- length characters
- removing characters
- replacing characters
- characters [SQL Server], replacing
- inserting data
ms.assetid: abb0afa9-44f6-42a2-a871-5f471dfb222b
caps.latest.revision: "40"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: db5876abd95b4eb9b21d91deeeb6bc0f1a242303
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="stuff-transact-sql"></a>STUFF (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Die STUFF-Funktion fügt eine Zeichenfolge in eine andere Zeichenfolge ein. Sie löscht ab einer bestimmten Anfangsposition eine festgelegte Anzahl von Zeichen in der ersten Zeichenfolge und fügt dort die zweite Zeichenfolge ein.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
STUFF ( character_expression , start , length , replaceWith_expression )  
```  
  
## <a name="arguments"></a>Argumente  
 *character_expression*  
 Ist ein [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) von Zeichendaten. *Character_expression* kann eine Konstante, Variable oder Spalte mit Zeichen- oder Binärdaten sein.  
  
 *Starten*  
 Ein ganzzahliger Wert, der die Position angibt, ab der Zeichen gelöscht werden sollen und an der anschließend eine andere Zeichenfolge eingefügt werden soll. Wenn *starten* ist negativ oder 0 (null), eine null-Zeichenfolge zurückgegeben. Wenn *starten* ist länger als der erste *Character_expression*, eine null-Zeichenfolge zurückgegeben. *Starten Sie* kann vom Typ **"bigint"**.  
  
 *length*  
 Eine ganze Zahl, die festlegt, wie viele Zeichen gelöscht werden sollen. Wenn *Länge* ist negativ ist, wird eine Nullzeichenfolge zurückgegeben. Wenn *Länge* ist länger als der erste *Character_expression*, Löschung bis zum letzten Zeichen in den letzten *Character_expression*.  Wenn *Länge* ist 0 (null), Einfügen tritt auf, bevor Sie das erste Zeichen in der Zeichenfolge. *Länge* kann vom Typ **"bigint"**.

 *replaceWith_expression*  
 Ist ein [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) von Zeichendaten. *Character_expression* kann eine Konstante, Variable oder Spalte mit Zeichen- oder Binärdaten sein. Dieser Ausdruck ersetzt *Länge* Zeichen des *Character_expression* beginnend *starten*. Bereitstellen von `NULL` als die *ReplaceWith_expression*, werden Zeichen entfernt, ohne etwas einzufügen.   
  
## <a name="return-types"></a>Rückgabetypen  
 Gibt Zeichendaten zurück, wenn *Character_expression* ist einer der unterstützten Zeichendatentypen. Gibt Binärdaten zurück, wenn *Character_expression* eines der unterstützten Binärdatentypen ist.  
  
## <a name="remarks"></a>Hinweise  
 Falls die Startposition oder die Länge negativ oder die Startposition größer als die Länge der ersten Zeichenfolge ist, wird eine Nullzeichenfolge zurückgegeben. Wenn die Startposition 0 ist, wird ein NULL-Wert zurückgegeben. Wenn es sich um mehr zu löschende Zeichen handelt als die erste Zeichenfolge aufweist, wird die erste Zeichenfolge bis auf das erste Zeichen gelöscht.  

Wenn der Ergebniswert größer als der vom Rückgabetyp unterstützte Höchstwert ist, wird ein Fehler ausgegeben.  
  
## <a name="supplementary-characters-surrogate-pairs"></a>Ergänzende Zeichen (Ersatzpaare)  
 Bei Verwendung von SC-Sortierungen beide *Character_expression* und *ReplaceWith_expression* können auch Ersatzpaare enthalten. Der Length-Parameter zählt jedes Ersatzzeichen *Character_expression* als einzelnes Zeichen.  
  
## <a name="examples"></a>Beispiele  
 In diesem Beispiel wird eine neue Zeichenfolge zurückgegeben, indem zunächst drei Zeichen aus der ersten Zeichenfolge (`abcdef`) ab der Position `2`, (also bei `b`) gelöscht werden. Anschließend wird die zweite Zeichenfolge an der Löschposition eingefügt.  
  
```  
SELECT STUFF('abcdef', 2, 3, 'ijklmn');  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
---------   
aijklmnef   
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Zeichenfolgenfunktionen &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  

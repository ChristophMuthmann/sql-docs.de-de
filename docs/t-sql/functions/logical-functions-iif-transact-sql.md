---
title: IIF (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- IIF_TSQL
- IIF
dev_langs:
- TSQL
helpviewer_keywords:
- IIF function
ms.assetid: e3ccf8ed-1cec-43ac-90b7-d8597c24b050
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 86ff2683e1ee71a3d11baa024753e0f52e5b3ee9
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="logical-functions---iif-transact-sql"></a>Logische Funktionen - IIF (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Gibt einen von zwei Werten zurück, abhängig davon, ob der boolesche Ausdruck "true" oder "false" in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ergibt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
IIF ( boolean_expression, true_value, false_value )  
```  
  
## <a name="arguments"></a>Argumente  
 *boolean_expression*  
 Ein gültiger boolescher Ausdruck.  
  
 Wenn dieses Argument kein boolescher Ausdruck ist, wird ein Syntaxfehler ausgelöst.  
  
 *true_value*  
 Der Wert wird zurückgegeben, wenn *Boolean_expression* auf "true" ergibt.  
  
 *false_value*  
 Der Wert wird zurückgegeben, wenn *Boolean_expression* auf "false" ausgewertet wird.  
  
## <a name="return-types"></a>Rückgabetypen  
 Gibt den Datentyp mit der höchsten Rangfolge aus den Typen in *True_value* und *False_value*. Weitere Informationen finden Sie unter [Rangfolge der Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md).  
  
## <a name="remarks"></a>Hinweise  
 IIF ist eine schnelle Möglichkeit zum Schreiben eines CASE-Ausdrucks. Hierdurch wird der als erstes Argument übergebenen booleschen Ausdruck ausgewertet und eines der beiden anderen Argumente auf Grundlage des Ergebnisses der Auswertung zurückgegeben. D. h. die *True_value* wird zurückgegeben, wenn der boolesche Ausdruck "true" ist und die *False_value* wird zurückgegeben, wenn der boolesche Ausdruck false oder unknown. *True_value* und *False_value* kann einen beliebigen Typ sein. Die gleichen Regeln, die für den CASE-Ausdruck für boolesche Ausdrücke, NULL-Behandlung und Rückgabetypen gelten, sind auch für IIF gültig. Weitere Informationen finden Sie unter [Groß-/KLEINSCHREIBUNG &#40; Transact-SQL &#41; ](../../t-sql/language-elements/case-transact-sql.md).  
  
 Die Tatsache, dass IIF in CASE übersetzt wird, wirkt sich auch auf andere Aspekte des Verhaltens dieser Funktion aus. Da CASE-Ausdrücke nur bis zur Ebene 10 geschachtelt werden können, können auch IIF-Anweisungen nur bis zu einer maximalen Ebene von 10 geschachtelt werden. Außerdem wird IIF remote an andere Server als semantisch gleichwertiger CASE-Ausdruck übergeben, einschließlich aller Verhaltensweisen eines remote ausgeführten CASE-Ausdrucks.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-simple-iif-example"></a>A. Einfaches Beispiel für IIF  
  
```  
DECLARE @a int = 45, @b int = 40;  
SELECT IIF ( @a > @b, 'TRUE', 'FALSE' ) AS Result;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
--------  
TRUE  
  
(1 row(s) affected)  
```  
  
### <a name="b-iif-with-null-constants"></a>B. IIF mit NULL-Konstanten  
  
```  
SELECT IIF ( 45 > 30, NULL, NULL ) AS Result;  
```  
  
 Das Ergebnis dieser Anweisung ist ein Fehler.  
  
### <a name="c-iif-with-null-parameters"></a>C. IIF mit NULL-Parametern  
  
```  
DECLARE @P INT = NULL, @S INT = NULL;  
SELECT IIF ( 45 > 30, @p, @s ) AS Result;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
--------  
NULL  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Groß-/KLEINSCHREIBUNG &#40; Transact-SQL &#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [Wählen Sie &#40; Transact-SQL &#41;](../../t-sql/functions/logical-functions-choose-transact-sql.md)  
  
  

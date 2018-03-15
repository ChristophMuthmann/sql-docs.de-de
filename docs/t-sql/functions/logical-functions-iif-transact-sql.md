---
title: IIF (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
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
- IIF_TSQL
- IIF
dev_langs:
- TSQL
helpviewer_keywords:
- IIF function
ms.assetid: e3ccf8ed-1cec-43ac-90b7-d8597c24b050
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: a7b58233c958d8ca9dc6b0fea9f9e69290d13679
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="logical-functions---iif-transact-sql"></a>Logische Funktionen: IIF (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

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
 Der zurückzugebende Wert, wenn *boolean_expression* den Wert TRUE ergibt.  
  
 *false_value*  
 Der zurückzugebende Wert, wenn *boolean_expression* den Wert FALSE ergibt.  
  
## <a name="return-types"></a>Rückgabetypen  
 Gibt den Datentyp mit dem höchsten Rang unter den Typen in *true_value* und in *false_value* zurück. Weitere Informationen finden Sie unter [Rangfolge der Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md).  
  
## <a name="remarks"></a>Remarks  
 IIF ist eine schnelle Möglichkeit zum Schreiben eines CASE-Ausdrucks. Hierdurch wird der als erstes Argument übergebenen booleschen Ausdruck ausgewertet und eines der beiden anderen Argumente auf Grundlage des Ergebnisses der Auswertung zurückgegeben. Das heißt, dass bei einem zutreffenden (TRUE) booleschen Ausdruck *true_value* und bei einem unzutreffenden oder unbekannten (FALSE oder unbekannt) booleschen Ausdruck *false_value* zurückgegeben wird. *true_value* und *false_value* können einen beliebigen Typ aufweisen. Die gleichen Regeln, die für den CASE-Ausdruck für boolesche Ausdrücke, NULL-Behandlung und Rückgabetypen gelten, sind auch für IIF gültig. Weitere Informationen finden Sie unter [CASE &#40;Transact-SQL&#41;](../../t-sql/language-elements/case-transact-sql.md).  
  
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
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [CASE &#40;Transact-SQL&#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [CHOOSE &#40;Transact-SQL&#41;](../../t-sql/functions/logical-functions-choose-transact-sql.md)  
  
  

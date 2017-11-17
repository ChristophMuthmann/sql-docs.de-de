---
title: "+ (Unäres Plus) (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server (starting with 2008)
f1_keywords:
- + (positive)
- +
- positive
dev_langs:
- TSQL
helpviewer_keywords:
- + (positive operator)
- positive operator (+)
- positive values [SQL Server]
ms.assetid: 0f31c5cc-3078-4f6a-9870-7eb1a98053fb
caps.latest.revision: 33
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2a0e451cc1e4341d7e516733ab8d82efe09b1be7
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="unary-operators---positive"></a>Unäre Operatoren - positiv
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt den Wert eines numerischen Ausdrucks zurück (ein unärer Operator). Unäre Operatoren führen eine Operation mit nur einem Ausdruck eines beliebigen Datentyps der numerischen Datentypkategorie aus.   
  
|Operator|Bedeutung|  
|--------------|-------------|  
|[+ (Positive) (+ (Positiv))](../../t-sql/language-elements/unary-operators-positive.md)|Numerischer Wert ist positiv.|  
|[- (Negative) (- (Negativ))](../../t-sql/language-elements/unary-operators-negative.md)|Numerischer Wert ist negativ.|  
|[~ (Bitweises NOT)](../../t-sql/language-elements/bitwise-not-transact-sql.md)|Gibt das Einerkomplement der Zahl zurück.|  
  
 Die Operatoren + (Positiv) und - (Negativ) können für einen beliebigen Ausdruck eines jeden Datentyps der numerischen Datentypkategorie verwendet werden. Der Operator ~ (Bitweises NOT) kann nur für Ausdrücke eines Datentyps der ganzzahligen Datentypkategorie verwendet werden.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
+ numeric_expression  
```  
  
## <a name="arguments"></a>Argumente  
 *numeric_expression*  
 Ist ein beliebiger gültiger [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) eines beliebigen Datentyps Typen in der numerischen Datentypkategorie, mit Ausnahme der **"DateTime"** und **Smalldatetime** Datentypen.  
  
## <a name="result-types"></a>Ergebnistypen  
 Gibt den Datentyp von *numeric_expression*zurück.  
  
## <a name="remarks"></a>Hinweise  
 Obwohl ein unäres Plus vor jedem numerischen Ausdruck angezeigt werden kann, führt es keinen Vorgang mit dem Wert aus, der von dem Ausdruck zurückgegeben wird. Insbesondere gibt es nicht den positiven Wert eines negativen Ausdrucks zurück. Um positiven Wert eines negativen Ausdrucks zurückzugeben, verwenden die [ABS](../../t-sql/functions/abs-transact-sql.md) Funktion.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-setting-a-variable-to-a-positive-value"></a>A. Festlegen einer Variablen auf einen positiven Wert  
 Im folgenden Beispiel wird eine Variable auf einen positiven Wert festgelegt.  
  
```  
DECLARE @MyNumber decimal(10,2);  
SET @MyNumber = +123.45;  
SELECT @MyNumber;  
GO  
```  
  
 Im Folgenden wird das Resultset aufgeführt:  
  
```  
-----------   
123.45            
  
(1 row(s) affected)  
```  
  
### <a name="b-using-the-unary-plus-operator-with-a-negative-value"></a>B. Verwenden des unären Plus-Operators mit einem negativen Wert  
 Im folgenden Beispiel wird die Verwendung des unären Plus-Operators mit einem negativen Ausdruck und der ABS()-Funktion mit dem gleichen negativen Ausdruck gezeigt. Das unäre Plus hat keine Auswirkungen auf den Ausdruck, die ABS()-Funktion gibt jedoch den positiven Wert des Ausdrucks zurück.  
  
```  
USE tempdb;  
GO  
DECLARE @Num1 int;  
SET @Num1 = -5;  
SELECT +@Num1, ABS(@Num1);  
GO  
```  
  
 Im Folgenden wird das Resultset aufgeführt:  
  
```  
----------- -----------  
-5          5  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Ausdrücke &#40; Transact-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Operatoren &#40; Transact-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [ABS &#40; Transact-SQL &#41;](../../t-sql/functions/abs-transact-sql.md)  
  
  


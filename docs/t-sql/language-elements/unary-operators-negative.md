---
title: '- (Negativ) (Transact-SQL) | Microsoft Docs'
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: negative
dev_langs: TSQL
helpviewer_keywords:
- '- (negative)'
- negative operator (-)
- negative values
ms.assetid: d6c14d14-d379-403b-82db-c197ad58c896
caps.latest.revision: "30"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c2d561099b6208ad0057489efd27942e48882df9
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="unary-operators---negative"></a>Unäre Operatoren - Negative
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt den negativen Wert eines numerischen Ausdrucks zurück (einen unären Operator). Unäre Operatoren führen eine Operation mit nur einem Ausdruck eines beliebigen Datentyps der numerischen Datentypkategorie aus.   
  
|Operator|Bedeutung|  
|--------------|-------------|  
|[+ (Positive) (+ (Positiv))](../../t-sql/language-elements/unary-operators-positive.md)|Numerischer Wert ist positiv.|  
|[- (Negative) (- (Negativ))](../../t-sql/language-elements/unary-operators-negative.md)|Numerischer Wert ist negativ.|  
|[~ (bitweises NOT)](../../t-sql/language-elements/bitwise-not-transact-sql.md)|Gibt das Einerkomplement der Zahl zurück.|  
  
 Die Operatoren + (Positiv) und - (Negativ) können für einen beliebigen Ausdruck eines jeden Datentyps der numerischen Datentypkategorie verwendet werden. Der Operator ~ (Bitweises NOT) kann nur für Ausdrücke eines Datentyps der ganzzahligen Datentypkategorie verwendet werden. 
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
- numeric_expression  
```  
  
## <a name="arguments"></a>Argumente  
 *numeric_expression*  
 Ist ein beliebiger gültiger [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) von einem der Datentypen der numerischen Datentypkategorie, mit Ausnahme der Datum und Zeitkategorie.  
  
## <a name="result-types"></a>Ergebnistypen  
 Gibt den Datentyp der *numerischer_ausdruck*, außer dass unsignierten **"tinyint"** Ausdruck wird höher gestuft, um eine signierte **"smallint"** Ergebnis.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-setting-a-variable-to-a-negative-value"></a>A. Festlegen einer Variablen auf einen negativen Wert  
 Im folgenden Beispiel wird eine Variable auf einen negativen Wert festgelegt.  
  
```  
USE tempdb;  
GO  
DECLARE @MyNumber decimal(10,2);  
SET @MyNumber = -123.45;  
SELECT @MyNumber AS NegativeValue;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
NegativeValue  
---------------------------------------  
-123.45  
  
(1 row(s) affected)  
  
```  
  
### <a name="b-changing-a-variable-to-a-negative-value"></a>B. Ändern einer Variablen in einen negativen Wert  
 Im folgenden Beispiel wird eine Variable in einen negativen Wert geändert.  
  
```  
USE tempdb;  
GO  
DECLARE @Num1 int;  
SET @Num1 = 5;  
SELECT @Num1 AS VariableValue, -@Num1 AS NegativeValue;  
GO  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
VariableValue NegativeValue  
------------- -------------  
5             -5  
  
(1 row(s) affected)  
  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-returning-the-negative-of-a-positive-constant"></a>C. Zurückgeben von den negativen Wert des positive-Konstante  
 Das folgende Beispiel gibt den negativen Wert, der eine Konstante positive zurück.  
  
```  
USE ssawPDW;  
  
SELECT TOP (1) - 17 FROM DimEmployee;  
```  
  
 Rückgabewert  
  
```  
-17  
```  
  
### <a name="d-returning-the-positive-of-a-negative-constant"></a>D. Zurückgeben den positiven einer negativen-Konstante  
 Im folgende Beispiel gibt das Positive einer negativen Konstante zurück.  
  
```  
USE ssawPDW;  
  
SELECT TOP (1) – ( - 17) FROM DimEmployee;  
```  
  
 Rückgabewert  
  
```  
17  
```  
  
### <a name="e-returning-the-negative-of-a-column"></a>E. Zurückgeben von den negativen Wert einer Spalte  
 Das folgende Beispiel gibt den negativen Wert, der die `BaseRate` Wert für jeden Mitarbeiter in der `dimEmployee` Tabelle.  
  
```  
USE ssawPDW;  
  
SELECT - BaseRate FROM DimEmployee;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Expressions &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Operators &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  


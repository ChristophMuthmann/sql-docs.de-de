---
title: '- (Subtraktion) (Transact-SQL) | Microsoft Docs'
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- subtract
- '-'
- -_TSQL
dev_langs: TSQL
helpviewer_keywords:
- '- (subtract)'
- subtract operator (-)
- minus operator (-)
- subtracting numbers
ms.assetid: db23145f-f17d-4b90-be09-28a881cacd1a
caps.latest.revision: "48"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 28c59396887c146679c027e13607e5976740b873
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/19/2018
---
# <a name="--subtraction-transact-sql"></a>-(Subtraktion) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Subtrahiert zwei Zahlen (ein arithmetischer Subtraktionsoperator). Kann auch eine Zahl, in Tagen, von einem Datum subtrahieren.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
expression - expression  
```  
  
## <a name="arguments"></a>Argumente  
 *expression*  
 Ist ein beliebiger gültiger [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) von einem der Datentypen der numerischen Datentypkategorie, mit Ausnahme der **Bit** -Datentyp. Kann nicht verwendet werden, mit **Datum**, **Zeit**, **datetime2**, oder **"DateTimeOffset"** -Datentypen.  
  
## <a name="result-types"></a>Ergebnistypen  
 Gibt einen Wert vom Datentyp des Arguments zurück, das in der Rangfolge höher steht. Weitere Informationen finden Sie unter [Rangfolge der Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md).  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-subtraction-in-a-select-statement"></a>A. Verwenden der Subtraktion in einer SELECT-Anweisung  
 Im folgenden Beispiel wird der Unterschied im Steuersatz zwischen dem Staat bzw. der Provinz mit dem höchsten Steuersatz und dem Staat oder der Provinz mit dem niedrigsten Steuersatz berechnet.  
  
 **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
```  
-- Uses AdventureWorks  
  
SELECT MAX(TaxRate) - MIN(TaxRate) AS 'Tax Rate Difference'  
FROM Sales.SalesTaxRate  
WHERE StateProvinceID IS NOT NULL;  
GO  
```  
  
 Sie können die Reihenfolge der Ausführung ändern, indem Sie Klammern verwenden. Berechnungen innerhalb von Klammern werden zuerst ausgewertet. Bei geschachtelten Klammerausdrücken werden die innersten Bestandteile zuerst berechnet.  
  
### <a name="b-using-date-subtraction"></a>B. Verwenden der Subtraktion von Datumsangaben  
 Im folgenden Beispiel wird eine Anzahl von Tagen von einem `datetime`-Datum abgezogen.  
  
 Gilt für: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
```  
-- Uses AdventureWorks  
  
DECLARE @altstartdate datetime;  
SET @altstartdate = CONVERT(DATETIME, ''January 10, 1900 3:00 AM', 101);  
SELECT @altstartdate - 1.5 AS 'Subtract Date';  
```  
  
 Im Folgenden wird das Resultset aufgeführt:  
  
 ```
 Subtract Date  
 -----------------------  
 1900-01-08 15:00:00.000  

 (1 row(s) affected)
 ```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-subtraction-in-a-select-statement"></a>"C:" Verwenden der Subtraktion in einer SELECT-Anweisung  
 Das folgende Beispiel berechnet den Unterschied in einem Grundpreis zwischen den Mitarbeiter mit der höchsten Grundpreis und den Mitarbeiter mit dem niedrigsten Steuersatz aus der `dimEmployee` Tabelle.  
  
```  
-- Uses AdventureWorks  
  
SELECT MAX(BaseRate) - MIN(BaseRate) AS BaseRateDifference  
FROM DimEmployee;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [= &#40; Subtraktionszuweisung &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/subtract-equals-transact-sql.md)   
 [Zusammengesetzte Operatoren &#40; Transact-SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)  
 [Arithmetische Operatoren &#40; Transact-SQL &#41;](../../t-sql/language-elements/arithmetic-operators-transact-sql.md)   
 [- &#40;Negative&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/unary-operators-negative.md)   
 [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Expressions &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Integrierte Funktionen &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
  
  



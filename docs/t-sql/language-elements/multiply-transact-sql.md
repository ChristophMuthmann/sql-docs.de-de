---
title: '* (Multiplizieren) (Transact-SQL) | Microsoft Docs'
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '*_TSQL'
- '*'
dev_langs:
- TSQL
helpviewer_keywords:
- '* (multiply operator)'
- multiplication [SQL Server]
- multiply operator (*)
ms.assetid: 34beb660-db19-46ca-ac90-2218471457bf
caps.latest.revision: 43
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d86fa430d70b4e3f42f73f5a9f4e642034668401
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="-multiply-transact-sql"></a>* (Multiplikation) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Multiplikation zweier Ausdrücke (arithmetischer Operator für die Multiplikation).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
expression * expression  
```  
  
## <a name="arguments"></a>Argumente  
 *expression*  
 Ist ein beliebiger gültiger [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) von einem der Datentypen der numerischen Datentypkategorie, mit Ausnahme der **"DateTime"** und **Smalldatetime** Datentypen.  
  
## <a name="result-types"></a>Ergebnistypen  
 Gibt einen Wert vom Datentyp des Arguments zurück, das in der Rangfolge höher steht. Weitere Informationen finden Sie unter [Rangfolge der Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md).  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die Produkt-ID, der Name, der Listenpreis und der neue Listenpreis für alle Mountainbikes in der `Product`-Tabelle abgerufen. Mithilfe des arithmetischen Operators `*` wird der neue Listenpreis berechnet (`ListPrice` multipliziert mit `1.15`).  
  
```  
-- Uses AdventureWorks  
  
SELECT ProductID, Name, ListPrice, ListPrice * 1.15 AS NewPrice  
FROM Production.Product  
WHERE Name LIKE 'Mountain-%'  
ORDER BY ProductID ASC;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 Das folgende Beispiel ruft die vor- und Nachnamen der Mitarbeiter in der `dimEmployee` Tabelle, und berechnet die Bezahlung `VacationHours` für jede...  
  
```  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName, BaseRate * VacationHours AS VacationPay  
FROM DimEmployee  
ORDER BY lastName ASC;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Ausdrücke & #40; Transact-SQL & #41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Integrierte Funktionen &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [Operatoren & #40; Transact-SQL & #41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [WOBEI & #40; Transact-SQL & #41;](../../t-sql/queries/where-transact-sql.md)   
 [& #42; = & #40; Multiplizieren Sie gleich & #41; & #40; Transact-SQL & #41;](../../t-sql/language-elements/multiply-equals-transact-sql.md)   
 [Zusammengesetzte Operatoren & #40; Transact-SQL & #41;](../../t-sql/language-elements/compound-operators-transact-sql.md)  
  
  




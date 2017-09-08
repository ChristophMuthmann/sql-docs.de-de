---
title: ODER (Transact-SQL) | Microsoft Docs
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
- OR_TSQL
- OR
dev_langs:
- TSQL
helpviewer_keywords:
- conditions [SQL Server], combining
- combining conditions
- OR operator
ms.assetid: b730a256-4a63-4880-9906-65b05cd9caf2
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 590410dd84275f63bc610ac436410c7d323eb8e3
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="or-transact-sql"></a>OR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Kombiniert zwei Bedingungen. Werden in einem Ausdruck mehrere logische Operatoren verwendet, werden OR-Operatoren nach AND-Operatoren ausgewertet. Sie können jedoch die Reihenfolge der Auswertung ändern, indem Sie Klammern verwenden.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
boolean_expression OR boolean_expression  
```  
  
## <a name="arguments"></a>Argumente  
 *boolean_expression*  
 Ist ein beliebiger gültiger [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) , TRUE, FALSE oder UNKNOWN zurückgibt.  
  
## <a name="result-types"></a>Ergebnistypen  
 **Boolean**  
  
## <a name="result-value"></a>Ergebniswert  
 OR gibt TRUE zurück, falls der Wert für mindestens eine der Bedingungen TRUE ist.  
  
## <a name="remarks"></a>Hinweise  
 Die folgende Tabelle zeigt das Ergebnis des OR-Operators.  
  
||TRUE|FALSE|UNKNOWN|  
|------|----------|-----------|-------------|  
|**"TRUE"**|TRUE|TRUE|TRUE|  
|**"FALSE"**|TRUE|FALSE|UNKNOWN|  
|**UNBEKANNT**|TRUE|UNKNOWN|UNKNOWN|  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden mithilfe der `vEmployeeDepartmentHistory`-Sicht die Namen der `Quality Assurance`-Mitarbeiter abgerufen, die in der Abend- oder Nachtschicht arbeiten. Ohne die Angabe der Klammern gibt die Abfrage `Quality Assurance`-Mitarbeiter zurück, die in der Abendschicht arbeiten, und alle Mitarbeiter, die in der Nachtschicht arbeiten.  
  
```  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName, Shift   
FROM HumanResources.vEmployeeDepartmentHistory  
WHERE Department = 'Quality Assurance'  
   AND (Shift = 'Evening' OR Shift = 'Night');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `FirstName    LastName         Shift`  
  
 `------------ ---------------- -------`  
  
 `Andreas      Berglund         Evening`  
  
 `Sootha       Charncherngkha   Night`  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 Das folgende Beispiel ruft die Namen aller Mitarbeiter, die entweder verdienen eine `BaseRate` weniger als 20 oder über eine `HireDate` Januar 1, 2001 oder höher.  
  
```  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName, BaseRate, HireDate   
FROM DimEmployee  
WHERE BaseRate < 10 OR HireDate >= '2001-01-01';  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Ausdrücke &#40; Transact-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Integrierte Funktionen &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [Operatoren &#40; Transact-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [WOBEI &#40; Transact-SQL &#41;](../../t-sql/queries/where-transact-sql.md)  
  
  




---
title: IS NULL (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- NULL_TSQL
- IS_[NOT]_NULL_TSQL
- IS_NULL_TSQL
- NULL
- '[NOT]_TSQL'
- IS
- IS_TSQL
- IS NULL
- IS [NOT] NULL
- '[NOT]'
dev_langs:
- TSQL
helpviewer_keywords:
- verifying nullability
- IS NOT NULL clause
- null values [SQL Server], verifying
- null values [SQL Server], IS [NOT] NULL
- IS [NOT] NULL clause
- testing nullability
- checking nullability
ms.assetid: cdc45cd8-e9b6-4648-8417-892fbeab15af
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 9ee29ea552deb1c1164a8e1f206a94de46541638
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="is-null-transact-sql"></a>IS NULL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Bestimmt, ob ein angegebener Ausdruck NULL ist.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
expression IS [ NOT ] NULL  
```  
  
## <a name="arguments"></a>Argumente  
 *expression*  
 Ist ein beliebiger gültiger [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md).  
  
 NICHT  
 Gibt an, dass das boolesche Ergebnis negiert wird. Das Prädikat kehrt die Rückgabewerte um und gibt TRUE zurück, wenn der Wert ungleich NULL ist, und FALSE, wenn der Wert gleich NULL ist.  
  
## <a name="result-types"></a>Ergebnistypen  
 **Boolean**  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 Wenn der Wert für *expression* NULL ist, gibt IS NULL den Wert TRUE zurück; andernfalls wird FALSE zurückgegeben.  
  
 Wenn der Wert für *expression* NULL ist, gibt IS NOT NULL den Wert FALSE zurück; andernfalls wird TRUE zurückgegeben.  
  
## <a name="remarks"></a>Remarks  
 Um zu bestimmen, ob ein Ausdruck NULL ist, verwenden Sie IS NULL oder IS NOT NULL anstelle von Vergleichsoperatoren (z. B. = oder !=). Vergleichsoperatoren geben UNKNOWN zurück, auch wenn nur eines der Argumente NULL ist.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel gibt die Namen und die Gewichtung aller Produkte zurück, deren Gewichtung entweder unter `10` Pfund liegt oder deren Farbe nicht bekannt bzw. `NULL` ist.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT Name, Weight, Color  
FROM Production.Product  
WHERE Weight < 10.00 OR Color IS NULL  
ORDER BY Name;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
 Im folgenden Beispiel werden die vollständigen Namen aller Mitarbeiter mit den Initialen der Zweitnamen zurückgegeben.  
  
```  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName, MiddleName  
FROM DIMEmployee  
WHERE MiddleName IS NOT NULL  
ORDER BY LastName DESC;  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [CASE &#40;Transact-SQL&#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Ausdrücke &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [Operators &#40;Transact-SQL&#41; (Operatoren &#40;Transact-SQL&#41;)](../../t-sql/language-elements/operators-transact-sql.md)   
 [Logical Operators &#40;Transact-SQL&#41; (Logische Operatoren &#40;Transact-SQL&#41;)](../../t-sql/language-elements/logical-operators-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [UPDATE (Transact-SQL)](../../t-sql/queries/update-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)  
  
  


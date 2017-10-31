---
title: Monat (Transact-SQL) | Microsoft Docs
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
- MONTH_TSQL
- MONTH
dev_langs:
- TSQL
helpviewer_keywords:
- values [SQL Server], date and time
- dates [SQL Server], functions
- month of year [SQL Server]
- date and time [SQL Server], MONTH
- dateparts [SQL Server], month
- functions [SQL Server], date and time
- dates [SQL Server], MONTH
- MONTH function [SQL Server]
ms.assetid: 9dd8aff7-b0fc-45df-b316-ead14ee9b8b7
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5f3f25d694d7d9757b09d834e9844aad2b2defb3
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="month-transact-sql"></a>MONTH (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt eine ganze Zahl, die den Monat des angegebenen darstellt *Datum*.  
  
 Eine Übersicht über alle [!INCLUDE[tsql](../../includes/tsql-md.md)] Datums-und Uhrzeitdatentypen und Funktionen finden Sie unter[Datums- und Uhrzeitdatentypen und-Funktionen &#40; Transact-SQL &#41; ](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
MONTH ( date )  
```  
  
## <a name="arguments"></a>Argumente  
 *Datum*  
 Ist ein Ausdruck, der in aufgelöst werden kann ein **Zeit**, **Datum**, **Smalldatetime**, **"DateTime"**, **datetime2**, oder **"DateTimeOffset"** Wert. Die *Datum* Argument kann ein Ausdruck, Spaltenausdruck, eine benutzerdefinierte Variable oder Zeichenfolgenliteral sein.  
  
## <a name="return-type"></a>Rückgabetyp  
 **int**  
  
## <a name="return-value"></a>Rückgabewert  
 MONTH gibt den gleichen Wert wie [DATEPART](../../t-sql/functions/datepart-transact-sql.md) (**Monat**, *Datum*).  
  
 Wenn *Datum* enthält nur ein Uhrzeitteil, der Rückgabewert 1, den basismonat.  
  
## <a name="examples"></a>Beispiele  
 Die folgende Anweisung gibt `4` zurück. Dies ist die Monatszahl.  
  
```  
SELECT MONTH('2007-04-30T01:01:01.1234567 -07:00');  
```  
  
 Die folgende Anweisung gibt `1900, 1, 1` zurück. Das Argument für *Datum* ist die Anzahl `0`. `0` wird von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] als 1. Januar 1900 interpretiert.  
  
```  
SELECT YEAR(0), MONTH(0), DAY(0);  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 Das folgende Beispiel gibt `4`. Dies ist die Monatszahl.  
  
```  
-- Uses AdventureWorks  
  
SELECT TOP 1 MONTH('2007-04-30T01:01:01.1234')   
FROM dbo.DimCustomer;  
```  
  
 Das folgende Beispiel gibt `1900, 1, 1`. Das Argument für *Datum* ist die Anzahl `0`. `0` wird von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] als 1. Januar 1900 interpretiert.  
  
```  
-- Uses AdventureWorks  
  
SELECT TOP 1 YEAR(0), MONTH(0), DAY(0) FROM dbo.DimCustomer;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  



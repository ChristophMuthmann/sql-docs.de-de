---
title: Jahr (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- YEAR
- YEAR_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- dates [SQL Server], years
- date and time [SQL Server], YEAR
- functions [SQL Server], date and time
- YEAR function [SQL Server]
- dateparts [SQL Server], year
ms.assetid: 74aa7ccc-8575-4018-80cf-14aeca379687
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 48dad4b2e38d9e178213aa8ad5ebb9e7608032a2
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="year-transact-sql"></a>YEAR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt eine ganze Zahl, die das Jahr des angegebenen darstellt *Datum*.  
  
 Eine Übersicht über alle [!INCLUDE[tsql](../../includes/tsql-md.md)] Datums-und Uhrzeitdatentypen und Funktionen finden Sie unter [Datums- und Uhrzeitdatentypen und-Funktionen &#40; Transact-SQL &#41; ](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
YEAR ( date )  
```  
  
## <a name="arguments"></a>Argumente  
 *Datum*  
 Ist ein Ausdruck, der in aufgelöst werden kann ein **Zeit**, **Datum**, **Smalldatetime**, **"DateTime"**, **datetime2**, oder **"DateTimeOffset"** Wert. Die *Datum* -Argument einer ein Ausdruck, Spaltenausdruck, eine benutzerdefinierte Variable oder Zeichenfolgenliteral sein.  
  
## <a name="return-types"></a>Rückgabetypen  
 **int**  
  
## <a name="return-value"></a>Rückgabewert  
 YEAR gibt den gleichen Wert wie [DATEPART](../../t-sql/functions/datepart-transact-sql.md) (**Jahr**, *Datum*).  
  
 Wenn *Datum* nur einen Uhrzeitteil enthält der Rückgabewert ist 1900 das Basisjahr.  
  
## <a name="examples"></a>Beispiele  
 Die folgende Anweisung gibt `2010` zurück. Dies ist das Jahr.  
  
```  
SELECT YEAR('2010-04-30T01:01:01.1234567-07:00');  
```  
  
 Die folgende Anweisung gibt `1900, 1, 1` zurück. Das Argument für *Datum* ist die Anzahl `0`. `0` wird von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] als 1. Januar 1900 interpretiert.  
  
```  
SELECT YEAR(0), MONTH(0), DAY(0);  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 Die folgende Anweisung gibt `1900, 1, 1` zurück. Das Argument für *Datum* ist die Anzahl `0`. `0` wird von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] als 1. Januar 1900 interpretiert.  
  
```  
SELECT TOP 1 YEAR(0), MONTH(0), DAY(0);  
```  
  
## <a name="see-also"></a>Siehe auch  
 [CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  


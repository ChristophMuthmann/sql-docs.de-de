---
title: Tag (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/30/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DAY_TSQL
- DAY
dev_langs: TSQL
helpviewer_keywords:
- date and time [SQL Server], DAY
- dates [SQL Server], functions
- DAY function [SQL Server]
- dates [SQL Server], days
- functions [SQL Server], date and time
- dateparts [SQL Server], day
ms.assetid: 2f4410ea-fd3e-4d69-ac4b-3b0091a084bc
caps.latest.revision: "41"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 444df60a2cfe3adae045020b3db8d673946dccb1
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="day-transact-sql"></a>DAY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Gibt eine ganze Zahl, die den Tag (Tag des Monats) des angegebenen *Datum*.
  
Eine Übersicht über alle [!INCLUDE[tsql](../../includes/tsql-md.md)] Datums-und Uhrzeitdatentypen und Funktionen finden Sie unter [Datums- und Uhrzeitdatentypen und-Funktionen &#40; Transact-SQL &#41; ](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
DAY ( date )  
```  
  
## <a name="arguments"></a>Argumente  
*Datum*  
Ist ein Ausdruck, der in aufgelöst werden kann ein **Zeit**, **Datum**, **Smalldatetime**, **"DateTime"**, **datetime2**, oder **"DateTimeOffset"** Wert. Die *Datum* -Argument einer ein Ausdruck, Spaltenausdruck, eine benutzerdefinierte Variable oder Zeichenfolgenliteral sein.
  
## <a name="return-type"></a>Rückgabetyp  
**int**
  
## <a name="return-value"></a>Rückgabewert  
DAY gibt den gleichen Wert wie [DATEPART](../../t-sql/functions/datepart-transact-sql.md) (**Tag**, *Datum*).
  
Wenn *Datum* enthält nur ein Uhrzeitteil, der Rückgabewert 1, den basistag.
  
## <a name="examples"></a>Beispiele  
Die folgende Anweisung gibt `30` zurück. Dies ist der Tag.
  
```sql
SELECT DAY('2015-04-30 01:01:01.1234567');  
```  
  
Die folgende Anweisung gibt `1900, 1, 1` zurück. Das Argument für *Datum* ist die Anzahl `0`. `0` wird von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] als 1. Januar 1900 interpretiert.
  
```sql
SELECT YEAR(0), MONTH(0), DAY(0);  
```  
  
## <a name="see-also"></a>Siehe auch
[CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  



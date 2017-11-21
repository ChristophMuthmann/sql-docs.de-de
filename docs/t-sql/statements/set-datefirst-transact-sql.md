---
title: SET DATEFIRST (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET DATEFIRST
- SET_DATEFIRST_TSQL
- DATEFIRST_TSQL
- DATEFIRST
dev_langs:
- TSQL
helpviewer_keywords:
- first day of week [SQL Server]
- day of week [SQL Server]
- SET DATEFIRST option [SQL Server]
- DATEFIRST option [SQL Server]
- weekdays [SQL Server]
- options [SQL Server], date
ms.assetid: 6b0d0e52-8ac1-4f88-b091-f98d6fb8574a
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 36507bde94914d278c2dd932f2dbff3180c1b4a5
ms.contentlocale: de-de
ms.lasthandoff: 10/24/2017

---
# <a name="set-datefirst-transact-sql"></a>SET DATEFIRST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Legt den ersten Wochentag auf eine Zahl von 1 bis 7 fest.  
  
 Eine Übersicht über alle [!INCLUDE[tsql](../../includes/tsql-md.md)] Datums-und Uhrzeitdatentypen und Funktionen finden Sie unter [Datums- und Uhrzeitdatentypen und-Funktionen &#40; Transact-SQL &#41; ](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
SET DATEFIRST { number | @number_var }   
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
SET DATEFIRST 7 ;  
```  
  
## <a name="arguments"></a>Argumente  
 *Anzahl* | **@***Number_var*  
 Eine ganze Zahl, die den ersten Tag der Woche angibt. Dieses Argument einen der folgenden Werte annehmen.  
  
|Wert|Erster Tag der Woche ist.|  
|-----------|------------------------------|  
|**1**|Montag|  
|**2**|Dienstag|  
|**3**|Mittwoch|  
|**4**|Donnerstag|  
|**5**|Freitag|  
|**6**|Samstag|  
|**7** (Standard, USA (USA))|Sonntag|  
  
## <a name="remarks"></a>Hinweise  
 Um die aktuelle Einstellung von SET DATEFIRST anzuzeigen, verwenden Sie die [@@DATEFIRST ](../../t-sql/functions/datefirst-transact-sql.md) Funktion.  
  
 Die Einstellung von SET DATEFIRST wird zur Ausführungszeit und nicht zur Analysezeit festgelegt.  
  
 Das Angeben von SET DATEFIRST hat keine Auswirkungen auf DATEDIFF. DATEDIFF verwendet immer Sonntag als ersten Wochentag, um zu gewährleisten, dass die Funktion deterministisch ist.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **public** -Rolle.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird der Wochentag für einen Datumswert angezeigt, und es wird gezeigt, wie sich Änderungen der `DATEFIRST`-Einstellung auswirken.  
  
```  
-- SET DATEFIRST to U.S. English default value of 7.  
SET DATEFIRST 7;  
  
SELECT CAST('1999-1-1' AS datetime2) AS SelectDate  
    ,DATEPART(dw, '1999-1-1') AS DayOfWeek;  
-- January 1, 1999 is a Friday. Because the U.S. English default   
-- specifies Sunday as the first day of the week, DATEPART of 1999-1-1  
-- (Friday) yields a value of 6, because Friday is the sixth day of the   
-- week when you start with Sunday as day 1.  
  
SET DATEFIRST 3;  
-- Because Wednesday is now considered the first day of the week,  
-- DATEPART now shows that 1999-1-1 (a Friday) is the third day of the   
-- week. The following DATEPART function should return a value of 3.  
SELECT CAST('1999-1-1' AS datetime2) AS SelectDate  
    ,DATEPART(dw, '1999-1-1') AS DayOfWeek;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [SET-Anweisungen &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  



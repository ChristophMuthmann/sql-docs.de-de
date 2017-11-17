---
title: SYSDATETIME (Transact-SQL) | Microsoft Docs
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
- SYSDATETIME_TSQL
- SYSDATETIME
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- date and time [SQL Server], SYSDATETIME
- current date and time [SQL Server]
- functions [SQL Server], time
- system date and time [SQL Server]
- system time [SQL Server]
- SYSDATETIME function [SQL Server]
- functions [SQL Server], date and time
- time [SQL Server], functions
- dates [SQL Server], current date and time
- dates [SQL Server], system date and time
- time [SQL Server], system
ms.assetid: cba4999e-a9d4-4742-abc9-4a4f109206b6
caps.latest.revision: 37
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e199d8438ca39ead6e9c299925ba83edd6be7ef5
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="sysdatetime-transact-sql"></a>SYSDATETIME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt eine **datetime2(7)** -Wert enthält das Datum und die Uhrzeit des Computers, auf dem die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird.  
  
> [!NOTE]  
>  SYSDATETIME und SYSUTCDATETIME weisen eine höhere Genauigkeit bezüglich der Bruchteile von Sekunden auf als GETDATE und GETUTCDATE. SYSDATETIMEOFFSET schließt den Zeitzonenoffset des Systems ein. SYSDATETIME, SYSUTCDATETIME und SYSDATETIMEOFFSET können einer Variablen eines beliebigen Datums- und Zeittyps zugewiesen werden.  
  
 Eine Übersicht über alle [!INCLUDE[tsql](../../includes/tsql-md.md)] Datums-und Uhrzeitdatentypen und Funktionen finden Sie unter [Datums- und Uhrzeitdatentypen und-Funktionen &#40; Transact-SQL &#41; ](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
SYSDATETIME ( )  
```  
  
## <a name="return-type"></a>Rückgabetyp  
 **datetime2(7)**  
  
## <a name="remarks"></a>Hinweise  
 [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen können auf verweisen SYSDATETIME überall verweisen, kann eine **datetime2(7)** Ausdruck.  
  
 SYSDATETIME ist eine nicht deterministische Funktion. Sichten und Ausdrücke, die in einer Spalte auf diese Funktion verweisen, können nicht indiziert werden.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Ruft das Datum und Uhrzeit-Werte mithilfe der Windows-API für GetSystemTimeAsFileTime() ab. Die Genauigkeit hängt von der Computerhardware und der Windows-Version ab, unter der die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird. Die Genauigkeit dieser API liegt bei 100 Nanosekunden. Die Genauigkeit kann mithilfe der Windows-API für GetSystemTimeAdjustment() ermittelt werden.  
  
## <a name="examples"></a>Beispiele  
 In den folgenden Beispielen werden die sechs [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Systemfunktionen verwendet, die das aktuelle Datum und die aktuelle Uhrzeit wiedergeben, um das Datum, die Uhrzeit oder beides zurückzugeben. Die Werte werden der Reihe nach zurückgegeben und können sich daher in Bruchteilen von Sekunden unterscheiden.  
  
### <a name="a-getting-the-current-system-date-and-time"></a>A. Das aktuelle Systemdatum und die Uhrzeit abrufen  
  
```  
SELECT SYSDATETIME()  
    ,SYSDATETIMEOFFSET()  
    ,SYSUTCDATETIME()  
    ,CURRENT_TIMESTAMP  
    ,GETDATE()  
    ,GETUTCDATE();  
/* Returned:  
SYSDATETIME()      2007-04-30 13:10:02.0474381  
SYSDATETIMEOFFSET()2007-04-30 13:10:02.0474381 -07:00  
SYSUTCDATETIME()   2007-04-30 20:10:02.0474381  
CURRENT_TIMESTAMP  2007-04-30 13:10:02.047  
GETDATE()          2007-04-30 13:10:02.047  
GETUTCDATE()       2007-04-30 20:10:02.047  
*/
```    
  
### <a name="b-getting-the-current-system-date"></a>B. Abrufen des aktuellen Systemdatums  
  
```  
SELECT CONVERT (date, SYSDATETIME())  
    ,CONVERT (date, SYSDATETIMEOFFSET())  
    ,CONVERT (date, SYSUTCDATETIME())  
    ,CONVERT (date, CURRENT_TIMESTAMP)  
    ,CONVERT (date, GETDATE())  
    ,CONVERT (date, GETUTCDATE());  
  
/* All returned 2007-04-30 */  
```  
  
### <a name="c-getting-the-current-system-time"></a>C. Abrufen der aktuellen Systemzeit  
  
```  
SELECT CONVERT (time, SYSDATETIME())  
    ,CONVERT (time, SYSDATETIMEOFFSET())  
    ,CONVERT (time, SYSUTCDATETIME())  
    ,CONVERT (time, CURRENT_TIMESTAMP)  
    ,CONVERT (time, GETDATE())  
    ,CONVERT (time, GETUTCDATE());  
  
/* Returned  
SYSDATETIME()      13:18:45.3490361  
SYSDATETIMEOFFSET()13:18:45.3490361  
SYSUTCDATETIME()   20:18:45.3490361  
CURRENT_TIMESTAMP  13:18:45.3470000  
GETDATE()          13:18:45.3470000  
GETUTCDATE()       20:18:45.3470000  
*/  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-getting-the-current-system-date-and-time"></a>D: Abrufen, das aktuelle Systemdatum und die Uhrzeit  
  
```  
SELECT SYSDATETIME();  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
--------------------------  
7/20/2013 2:49:59 PM
```  
  
## <a name="see-also"></a>Siehe auch  
 [CAST und CONVERT &#40; Transact-SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [Datums- und Zeitdaten Typen und-Funktionen &#40; Transact-SQL &#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)  
  
  



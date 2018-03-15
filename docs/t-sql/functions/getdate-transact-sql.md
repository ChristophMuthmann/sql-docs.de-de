---
title: GETDATE (Transact-SQL) | Microsoft-Dokumentation
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
- GETDATE_TSQL
- GETDATE
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- GETDATE function [SQL Server]
- current date and time [SQL Server]
- time [SQL Server], current
- functions [SQL Server], time
- system date and time [SQL Server]
- system time [SQL Server]
- functions [SQL Server], date and time
- time [SQL Server], functions
- dates [SQL Server], current date and time
- date and time [SQL Server], GETDATE
- dates [SQL Server], system date and time
- time [SQL Server], system
ms.assetid: bebe3b65-2b3e-4c73-bf80-ff1132c680a7
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 5750024eea12dd90e9fdb8c69677ddd554e71bb8
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="getdate-transact-sql"></a>GETDATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt den aktuellen Zeitstempel des Datenbanksystems ohne den Zeitzonenoffset der Datenbank als **datetime**-Wert zurück. Dieser Wert wird aus dem Betriebssystem des Computers abgeleitet, auf dem die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird.  
  
> [!NOTE]  
>  SYSDATETIME und SYSUTCDATETIME weisen eine höhere Genauigkeit bezüglich der Bruchteile von Sekunden auf als GETDATE und GETUTCDATE. SYSDATETIMEOFFSET schließt den Zeitzonenoffset des Systems ein. SYSDATETIME, SYSUTCDATETIME und SYSDATETIMEOFFSET können einer Variablen eines beliebigen Datums- und Zeittyps zugewiesen werden.  
  
 Eine Übersicht über alle Datums- und Uhrzeitdatentypen und zugehörige Funktionen für [!INCLUDE[tsql](../../includes/tsql-md.md)] finden Sie unter [Datums- und Uhrzeitdatentypen und zugehörige Funktionen &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
GETDATE ( )  
```  
  
## <a name="return-type"></a>Rückgabetyp  
 **datetime**  
  
## <a name="remarks"></a>Remarks  
 [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen können auf eine beliebige Position von GETDATE verweisen, die auf einen **datetime**-Ausdruck verweisen kann.  
  
 GETDATE ist eine nicht deterministische Funktion. Sichten und Ausdrücke, die in einer Spalte auf diese Funktion verweisen, können nicht indiziert werden.  
  
 Wenn Sie SWITCHOFFSET mit der GETDATE()-Funktion verwenden, kann dies zu einer verlangsamten Abfrageausführung führen, da der Abfrageoptimierer keine genauen Kardinalitätsschätzungen für den GETDATE-Wert abrufen kann. Es wird empfohlen, den GETDATE-Wert vorab zu berechnen und den Wert dann wie im folgenden Beispiel in der Abfrage anzugeben. Verwenden Sie außerdem den OPTION (RECOMPILE)-Abfragehinweis, um vom Abfrageoptimierer zu erzwingen, dass ein Abfrageplan beim nächsten Ausführen derselben Abfrage erneut kompiliert wird. Dem Optimierer stehen daraufhin genaue Kardinalitätsschätzungen für GETDATE() zur Verfügung, und er erstellt einen effizienteren Abfrageplan.  
  
```  
DECLARE @dt datetimeoffset = switchoffset (CONVERT(datetimeoffset, GETDATE()), '-04:00');   
SELECT * FROM t    
WHERE c1 > @dt OPTION (RECOMPILE);  
  
```  
  
## <a name="examples"></a>Beispiele  
 In den folgenden Beispielen werden die sechs [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Systemfunktionen verwendet, die das aktuelle Datum, die aktuelle Uhrzeit oder beides zurückgeben. Die Werte werden der Reihe nach zurückgegeben und können sich daher in Bruchteilen von Sekunden unterscheiden.  
  
### <a name="a-getting-the-current-system-date-and-time"></a>A. Abrufen des aktuellen Systemdatums und der aktuellen Systemzeit  
  
```  
SELECT SYSDATETIME()  
    ,SYSDATETIMEOFFSET()  
    ,SYSUTCDATETIME()  
    ,CURRENT_TIMESTAMP  
    ,GETDATE()  
    ,GETUTCDATE();  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
SYSDATETIME()      2007-04-30 13:10:02.0474381
SYSDATETIMEOFFSET()2007-04-30 13:10:02.0474381 -07:00
SYSUTCDATETIME()   2007-04-30 20:10:02.0474381
CURRENT_TIMESTAMP  2007-04-30 13:10:02.047
GETDATE()          2007-04-30 13:10:02.047
GETUTCDATE()       2007-04-30 20:10:02.047
```  
  
### <a name="b-getting-the-current-system-date"></a>B. Abrufen des aktuellen Systemdatums  
  
```  
SELECT CONVERT (date, SYSDATETIME())  
    ,CONVERT (date, SYSDATETIMEOFFSET())  
    ,CONVERT (date, SYSUTCDATETIME())  
    ,CONVERT (date, CURRENT_TIMESTAMP)  
    ,CONVERT (date, GETDATE())  
    ,CONVERT (date, GETUTCDATE());  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
SYSDATETIME()          2007-05-03  
SYSDATETIMEOFFSET()    2007-05-03  
SYSUTCDATETIME()       2007-05-04  
CURRENT_TIMESTAMP      2007-05-03  
GETDATE()              2007-05-03  
GETUTCDATE()           2007-05-04
``` 
  
### <a name="c-getting-the-current-system-time"></a>C. Abrufen der aktuellen Systemzeit  
  
```  
SELECT CONVERT (time, SYSDATETIME())  
    ,CONVERT (time, SYSDATETIMEOFFSET())  
    ,CONVERT (time, SYSUTCDATETIME())  
    ,CONVERT (time, CURRENT_TIMESTAMP)  
    ,CONVERT (time, GETDATE())  
    ,CONVERT (time, GETUTCDATE());  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
SYSDATETIME()      13:18:45.3490361  
SYSDATETIMEOFFSET()13:18:45.3490361  
SYSUTCDATETIME()   20:18:45.3490361  
CURRENT_TIMESTAMP  13:18:45.3470000  
GETDATE()          13:18:45.3470000  
GETUTCDATE()       20:18:45.3470000  
```
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
 In den folgenden Beispielen werden die drei [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Systemfunktionen verwendet, die das aktuelle Datum, die aktuelle Uhrzeit oder beides zurückgeben. Die Werte werden der Reihe nach zurückgegeben und können sich daher in Bruchteilen von Sekunden unterscheiden.  
  
### <a name="d-getting-the-current-system-date-and-time"></a>D. Abrufen des aktuellen Systemdatums und der aktuellen Systemzeit  
  
```  
SELECT SYSDATETIME()  
    ,CURRENT_TIMESTAMP  
    ,GETDATE();  
```  
  
### <a name="e-getting-the-current-system-date"></a>E. Abrufen des aktuellen Systemdatums  
  
```  
SELECT CONVERT (date, SYSDATETIME())  
    ,CONVERT (date, CURRENT_TIMESTAMP)  
    ,CONVERT (date, GETDATE());  
  
```  
  
### <a name="f-getting-the-current-system-time"></a>F. Abrufen der aktuellen Systemzeit  
  
```  
SELECT CONVERT (time, SYSDATETIME())  
    ,CONVERT (time, CURRENT_TIMESTAMP)  
    ,CONVERT (time, GETDATE());  
  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  


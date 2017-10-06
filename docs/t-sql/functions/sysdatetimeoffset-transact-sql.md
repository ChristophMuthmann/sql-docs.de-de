---
title: SYSDATETIMEOFFSET (Transact-SQL) | Microsoft Docs
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
- SYSDATETIMEOFFSET_TSQL
- SYSDATETIMEOFFSET
dev_langs:
- TSQL
helpviewer_keywords:
- date and time [SQL Server], SYSDATETIMEOFFSET
- dates [SQL Server], functions
- current date and time [SQL Server]
- functions [SQL Server], time
- system date and time [SQL Server]
- system time [SQL Server]
- SYSDATETIMEOFFSET function [SQL Server]
- functions [SQL Server], date and time
- time [SQL Server], functions
- dates [SQL Server], current date and time
- dates [SQL Server], system date and time
- time zones [SQL Server]
- time [SQL Server], system
ms.assetid: 8423c753-cebe-4edd-871d-0138e092199f
caps.latest.revision: 43
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2497aa71cae4fa7cf5fecf6fe6bd1383d84680a1
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="sysdatetimeoffset-transact-sql"></a>SYSDATETIMEOFFSET (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt eine **datetimeoffset(7)** -Wert enthält das Datum und die Uhrzeit des Computers, auf dem die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird. Der Zeitzonenoffset wird einbezogen.  
  
 Eine Übersicht über alle [!INCLUDE[tsql](../../includes/tsql-md.md)] Datums-und Uhrzeitdatentypen und Funktionen finden Sie unter [Datums- und Uhrzeitdatentypen und-Funktionen &#40; Transact-SQL &#41; ](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
SYSDATETIMEOFFSET ( )  
```  
  
## <a name="return-type"></a>Rückgabetyp  
 **DateTimeOffset(7)**  
  
## <a name="remarks"></a>Hinweise  
 [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen können auf verweisen SYSDATETIMEOFFSET überall verweisen, kann eine **"DateTimeOffset"** Ausdruck.  
  
 SYSDATETIMEOFFSET ist eine nicht deterministische Funktion. Sichten und Ausdrücke, die in einer Spalte auf diese Funktion verweisen, können nicht indiziert werden.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Ruft das Datum und Uhrzeit-Werte mithilfe der Windows-API für GetSystemTimeAsFileTime() ab. Die Genauigkeit hängt von der Computerhardware und der Windows-Version ab, unter der die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird. Die Genauigkeit dieser API liegt bei 100 Nanosekunden. Die Genauigkeit kann mithilfe der Windows-API für GetSystemTimeAdjustment() ermittelt werden.  
  
## <a name="examples"></a>Beispiele  
 In den folgenden Beispielen werden die sechs [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Systemfunktionen verwendet, die das aktuelle Datum, die aktuelle Uhrzeit oder beides zurückgeben. Die Werte werden der Reihe nach zurückgegeben und können sich daher in Bruchteilen von Sekunden unterscheiden.  
  
### <a name="a-showing-the-formats-that-are-returned-by-the-date-and-time-functions"></a>A. Anzeigen der Formate, die von den Datums- und Uhrzeitfunktionen zurückgegeben werden  
 Das folgende Beispiel zeigt verschiedene Formatwerte, die von den Datums- und Zeitfunktionen zurückgegeben werden.  
  
```  
SELECT SYSDATETIME() AS SYSDATETIME  
    ,SYSDATETIMEOFFSET() AS SYSDATETIMEOFFSET  
    ,SYSUTCDATETIME() AS SYSUTCDATETIME  
    ,CURRENT_TIMESTAMP AS CURRENT_TIMESTAMP  
    ,GETDATE() AS GETDATE  
    ,GETUTCDATE() AS GETUTCDATE;  
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
  
### <a name="b-converting-date-and-time-to-date"></a>B. Konvertieren von Datums- und Uhrzeitwerten in date  
 Das folgende Beispiel zeigt, wie Sie Datums- und Uhrzeitwerte in `date` konvertieren.  
  
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
2007-04-30
2007-04-30
2007-04-30
2007-04-30
2007-04-30
2007-04-30
```  
  
### <a name="c-converting-date-and-time-to-times"></a>C. Konvertieren von Datums- und Uhrzeitwerten in Uhrzeitwerte  
 Das folgende Beispiel zeigt, wie Sie Datums- und Uhrzeitwerte in `time` konvertieren.  
  
```  
SELECT CONVERT (time, SYSDATETIME()) AS SYSDATETIME()  
    ,CONVERT (time, SYSDATETIMEOFFSET()) AS SYSDATETIMEOFFSET()  
    ,CONVERT (time, SYSUTCDATETIME()) AS SYSUTCDATETIME()  
    ,CONVERT (time, CURRENT_TIMESTAMP) AS CURRENT_TIMESTAMP  
    ,CONVERT (time, GETDATE()) AS GETDATE()  
    ,CONVERT (time, GETUTCDATE()) AS GETUTCDATE();  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 In den folgenden Beispielen werden die sechs [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Systemfunktionen verwendet, die das aktuelle Datum, die aktuelle Uhrzeit oder beides zurückgeben. Die Werte werden der Reihe nach zurückgegeben und können sich daher in Bruchteilen von Sekunden unterscheiden.  
  
### <a name="d-showing-the-formats-that-are-returned-by-the-date-and-time-functions"></a>D. Anzeigen der Formate, die von den Datums- und Uhrzeitfunktionen zurückgegeben werden  
 Das folgende Beispiel zeigt verschiedene Formatwerte, die von den Datums- und Zeitfunktionen zurückgegeben werden.  
  
```  
SELECT SYSDATETIME() AS SYSDATETIME  
    ,SYSDATETIMEOFFSET() AS SYSDATETIMEOFFSET  
    ,SYSUTCDATETIME() AS SYSUTCDATETIME  
    ,CURRENT_TIMESTAMP AS CURRENT_TIMESTAMP  
    ,GETDATE() AS GETDATE  
    ,GETUTCDATE() AS GETUTCDATE;  
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
  
### <a name="e-converting-date-and-time-to-date"></a>E. Konvertieren von Datums- und Uhrzeitwerten in date  
 Das folgende Beispiel zeigt, wie Sie Datums- und Uhrzeitwerte in `date` konvertieren.  
  
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
2007-04-30
2007-04-30
2007-04-30
2007-04-30
2007-04-30
2007-04-30
```  
  
### <a name="f-converting-date-and-time-to-times"></a>F. Konvertieren von Datums- und Uhrzeitwerten in Uhrzeitwerte  
 Das folgende Beispiel zeigt, wie Sie Datums- und Uhrzeitwerte in `time` konvertieren.  
  
```  
SELECT CONVERT (time, SYSDATETIME()) AS SYSDATETIME()  
    ,CONVERT (time, SYSDATETIMEOFFSET()) AS SYSDATETIMEOFFSET()  
    ,CONVERT (time, SYSUTCDATETIME()) AS SYSUTCDATETIME()  
    ,CONVERT (time, CURRENT_TIMESTAMP) AS CURRENT_TIMESTAMP  
    ,CONVERT (time, GETDATE()) AS GETDATE()  
    ,CONVERT (time, GETUTCDATE()) AS GETUTCDATE();  
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
  
## <a name="see-also"></a>Siehe auch  
 [CAST und CONVERT &#40; Transact-SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [Datums- und Zeitdaten Typen und-Funktionen &#40; Transact-SQL &#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)  
  
  



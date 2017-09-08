---
title: '@@DATEFIRST (Transact-SQL) | Microsoft Docs'
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DATE_FORMAT_TSQL
- DATE FORMAT
- '@@DATEFIRST_TSQL'
- '@@DATEFIRST'
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- date and time [SQL Server], SET DATEFIRST
- first day of week [SQL Server]
- dates [SQL Server], first day of week
- day of week [SQL Server]
- SET DATEFIRST option [SQL Server]
- date and time [SQL Server], DATEFIRST
- DATEFIRST option [SQL Server]
- date and time [SQL Server], @@DATEFIRST
- weekdays [SQL Server]
- '@@DATEFIRST function [SQL Server]'
- functions [SQL Server], date and time
- options [SQL Server], date
ms.assetid: a178868e-49d5-4bd5-a5e2-1283409c8ce6
caps.latest.revision: 46
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 951628293157784f522a262a1017b5b8b7f4bd83
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="datefirst-transact-sql"></a>@@DATEFIRST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Gibt den aktuellen Wert für eine Sitzung des [SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md).
  
Eine Übersicht über alle [!INCLUDE[tsql](../../includes/tsql-md.md)] Datums-und Uhrzeitdatentypen und Funktionen finden Sie unter [Datums- und Uhrzeitdatentypen und-Funktionen &#40; Transact-SQL &#41; ](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
@@DATEFIRST  
```  
  
## <a name="return-type"></a>Rückgabetyp  
**tinyint**
  
## <a name="remarks"></a>Hinweise  
SET DATEFIRST gibt den ersten Tag der Woche an. Der Standardparameter für Englisch (USA) ist 7 (Sonntag).
  
Diese Spracheinstellung wirkt sich nur auf die Interpretation von Zeichenfolgen bei der Konvertierung in Datumswerte zum Speichern in der Datenbank sowie auf die Anzeige von Datumswerten aus, die in der Datenbank gespeichert sind. Das Speicherformat der Datumsdaten beeinflusst diese Einstellung nicht. Im folgenden Beispiel wird zunächst die Sprache auf `Italian` festgelegt. Die `SELECT @@DATEFIRST;`-Anweisung gibt `1` zurück. Danach wird die Sprache auf `us_english` festgelegt. Die `SELECT @@DATEFIRST;`-Anweisung gibt `7` zurück.
  
```sql
SET LANGUAGE Italian;  
GO  
SELECT @@DATEFIRST;  
GO  
SET LANGUAGE us_english;  
GO  
SELECT @@DATEFIRST;  
```  
  
## <a name="examples"></a>Beispiele  
Dieses Beispiel legt den ersten Tag der Woche auf `5` (Freitag) fest und geht davon aus, dass der aktuelle Tag, `Today`, Samstag ist. Die `SELECT`-Anweisung gibt den `DATEFIRST`-Wert und die Zahl des aktuellen Tages der Woche zurück.
  
```sql
SET DATEFIRST 5;  
SELECT @@DATEFIRST AS 'First Day'  
    ,DATEPART(dw, SYSDATETIME()) AS 'Today';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
First Day         Today  
----------------  --------------  
5                 2  
```  
  
## <a name="example"></a>Beispiel
 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
```sql
SELECT @@DATEFIRST;  
```  
  
## <a name="see-also"></a>Siehe auch
[Konfigurationsfunktionen &#40; Transact-SQL &#41;](../../t-sql/functions/configuration-functions-transact-sql.md)
  
  



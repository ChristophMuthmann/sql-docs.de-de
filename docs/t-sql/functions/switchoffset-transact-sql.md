---
title: SWITCHOFFSET (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 12/02/2015
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
- SWITCHTZ
- SWITCHTZ_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- functions [SQL Server], time
- functions [SQL Server], date and time
- SWITCHOFFSET function [SQL Server]
- time [SQL Server], functions
- date and time [SQL Server], SWITCHOFFSET
- time zones [SQL Server]
ms.assetid: 32a48e36-0aa4-4260-9fe9-cae9197d16c5
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 56708a638f47aa926228d2d98e4fce5c3de7754b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="switchoffset-transact-sql"></a>SWITCHOFFSET (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt eine **"DateTimeOffset"** Wert, der von der gespeicherten Zeitzonenoffset in einen angegebenen neuen Zeitzonenoffset geändert wird.  
  
 Eine Übersicht über alle [!INCLUDE[tsql](../../includes/tsql-md.md)] Datums-und Uhrzeitdatentypen und Funktionen finden Sie unter [Datums- und Uhrzeitdatentypen und-Funktionen &#40; Transact-SQL &#41; ](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
SWITCHOFFSET ( DATETIMEOFFSET, time_zone )   
```  
  
## <a name="arguments"></a>Argumente  
 *"DATETIMEOFFSET"*  
 Ist ein Ausdruck, der in aufgelöst werden kann ein **DateTimeOffset (n)** Wert.  
  
 *time_zone*  
 Eine Zeichenfolge im Format [+|-]TZH:TZM oder eine ganze Zahl mit Vorzeichen (Minuten), die den Zeitzonenoffset darstellt und von der vorausgesetzt wird, dass sie die Sommerzeit berücksichtigt und entsprechend angepasst ist.  
  
## <a name="return-type"></a>Rückgabetyp  
 **"DateTimeOffset"** mit der Genauigkeit von Bruchteilen der *"DateTimeOffset"* Argument.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden Sie SWITCHOFFSET, Auswählen einer **"DateTimeOffset"** Wert in einem Zeitzonenoffset unterscheidet, die ursprünglich gespeicherten Zeitzonenoffset. SWITCHOFFSET nicht aktualisiert das gespeicherte *Time_zone* Wert.  
  
 SWITCHOFFSET kann verwendet werden, um Aktualisieren einer **"DateTimeOffset"** Spalte.  
  
 Bei Verwendung von SWITCHOFFSET mit der GETDATE()-Funktion wird die Abfrage u. U. langsam ausgeführt. Das liegt daran, dass der Abfrageoptimierer keine genauen Kardinalitätsschätzungen für den datetime-Wert abrufen kann. Um dieses Problem zu beheben, verwenden Sie den OPTION (RECOMPILE)-Abfragehinweis, um zu erzwingen, dass der Abfrageoptimierer einen Abfrageplan erneut kompiliert, sobald dieselbe Abfrage das nächste Mal ausgeführt wird. Auf diese Weise erhält der Optimierer exakte Kardinalitätsschätzungen und kann einen effizienteren Abfrageplan erzeugen. Weitere Informationen zu den RECOMPILE-Abfragehinweis, finden Sie unter [Abfragehinweise &#40; Transact-SQL &#41; ](../../t-sql/queries/hints-transact-sql-query.md).  
  
```  
DECLARE @dt datetimeoffset = switchoffset (CONVERT(datetimeoffset, GETDATE()), '-04:00');   
SELECT * FROM t    
WHERE c1 > @dt OPTION (RECOMPILE);  
  
```  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird `SWITCHOFFSET` verwendet, um einen anderen als den in der Datenbank gespeicherten Zeitzonenoffset-Wert anzuzeigen.  
  
```  
CREATE TABLE dbo.test   
    (  
    ColDatetimeoffset datetimeoffset  
    );  
GO  
INSERT INTO dbo.test   
VALUES ('1998-09-20 7:45:50.71345 -5:00');  
GO  
SELECT SWITCHOFFSET (ColDatetimeoffset, '-08:00')   
FROM dbo.test;  
GO  
--Returns: 1998-09-20 04:45:50.7134500 -08:00  
SELECT ColDatetimeoffset  
FROM dbo.test;  
--Returns: 1998-09-20 07:45:50.7134500 -05:00  
```  
  
## <a name="see-also"></a>Siehe auch  
 [CAST und CONVERT &#40; Transact-SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [ZEITZONE &#40; Transact-SQL &#41;](../../t-sql/queries/at-time-zone-transact-sql.md)  
  
  



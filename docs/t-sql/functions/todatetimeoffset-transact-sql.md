---
title: TODATETIMEOFFSET (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/13/2017
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
- TO_DATETIMEOFFSET_TSQL
- SWITCH_TZ_TSQL
- SWITCH_TZ
- TO_DATETIMEOFFSET
dev_langs:
- TSQL
helpviewer_keywords:
- date and time [SQL Server], TODATETIMEOFFSET
- TODATETIMEOFFSET function
- functions [SQL Server], time
- functions [SQL Server], date and time
- time [SQL Server], functions
ms.assetid: b5fafc08-efd4-4a3b-a0b3-068981a0a685
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: b6a8e329f2dc0db17bfb7e0e1a99657f7d436365
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="todatetimeoffset-transact-sql"></a>TODATETIMEOFFSET (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt einen **datetimeoffset**-Wert zurück, der von einem **datetime2**-Ausdruck übersetzt wird.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
TODATETIMEOFFSET ( expression , time_zone )  
```  
  
## <a name="arguments"></a>Argumente  
 *expression*  
 Ein [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md), der zu einem [datetime2](../../t-sql/data-types/datetime2-transact-sql.md)-Wert aufgelöst wird.  
  
> [!NOTE]  
>  Ein Ausdruck kann nicht vom Typ **text**, **ntext** oder **image** sein, da diese Typen nicht implizit in **varchar** oder **nvarchar** konvertiert werden können.  
  
 *time_zone*  
 Ein Ausdruck, der den Zeitzonenoffset in Minuten (bei einer ganzen Zahl), z. B. -120, oder in Stunden und Minuten (bei einer Zeichenfolge), z. B. '+13.00' darstellt. Der Bereich liegt zwischen +14 und -14 (in Stunden). Der Ausdruck wird in Ortszeit für die angegebene time_zone interpretiert.  
  
> [!NOTE]  
>  Wenn der Ausdruck eine Zeichenfolge ist, muss er folgendes Format aufweisen: {+ | -} TZH:THM.  
  
## <a name="return-type"></a>Rückgabetyp  
 **datetimeoffset**. Die Genauigkeit der Bruchteile entspricht der des *datetime*-Arguments.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-changing-the-time-zone-offset-of-the-current-date-and-time"></a>A. Ändern des Zeitzonenoffsets für das aktuelle Datum und die aktuelle Uhrzeit  
 Im folgenden Beispiel ändert sich der Zeitzonenoffset des aktuellen Datums und der aktuellen Uhrzeit zur Zeitzone `-07:00`.  
  
```  
DECLARE @todaysDateTime datetime2;  
SET @todaysDateTime = GETDATE();  
SELECT TODATETIMEOFFSET (@todaysDateTime, '-07:00');  
-- RETURNS 2007-08-30 15:51:34.7030000 -07:00  
```  
  
### <a name="b-changing-the-time-zone-offset-in-minutes"></a>B. Ändern des Zeitzonenoffsets zu Minuten  
 Im folgenden Beispiel ändert sich die aktuelle Zeitzone zu `-120` Minuten.  
  
```  
DECLARE @todaysDate datetime2;  
SET @todaysDate = GETDATE();  
SELECT TODATETIMEOFFSET (@todaysDate, -120);  
-- RETURNS 2007-08-30 15:52:37.8770000 -02:00  
```  
  
### <a name="c-adding-a-13-hour-time-zone-offset"></a>C. Hinzufügen eines 13-Stunden-Zeitzonenoffsets  
 Im folgenden Beispiel wird ein 13-Stunden-Zeitzonenoffset einem Datum und einer Uhrzeit hinzugefügt.  
  
```  
DECLARE @dateTime datetimeoffset(7)= '2007-08-28 18:00:30';  
SELECT TODATETIMEOFFSET (@dateTime, '+13:00');  
-- RETURNS 2007-08-28 18:00:30.0000000 +13:00  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [CAST and CONVERT &#40;Transact-SQL&#41; (CAST und CONVERT &#40;Transact-SQL&#41;)](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [Date and Time Data Types and Functions &#40;Transact-SQL&#41; (Datums- und Uhrzeitdatentypen und zugehörige Funktionen &#40;Transact-SQL&#41;)](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)   
 [AT TIME ZONE &#40;Transact-SQL&#41;](../../t-sql/queries/at-time-zone-transact-sql.md)  
  
  


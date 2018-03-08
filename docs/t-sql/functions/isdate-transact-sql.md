---
title: ISDATE (Transact-SQL) | Microsoft Docs
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
- ISDATETIME
- ISDATE_TSQL
- ISDATE
- ISDATETIME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- date and time [SQL Server], ISDATE
- validate dates times [SQL Server]
- formats [SQL Server], time
- dates [SQL Server], validate
- verify dates times [SQL Server]
- functions [SQL Server], time
- formats [SQL Server], dates
- functions [SQL Server], date and time
- time [SQL Server], functions
- time [SQL Server], validate
- ISDATE function [SQL Server]
ms.assetid: 8e2c9ee7-388a-432f-b2c9-7b398f26bf85
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: b9f17d829f3acf7c72a8599eb71b945c58d4cb0a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="isdate-transact-sql"></a>ISDATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt 1 zurück, wenn die *Ausdruck* ist ein gültiger **Datum**, **Zeit**, oder **"DateTime"** Wert; andernfalls 0.  
  
 ISDATE gibt 0 zurück, wenn die *Ausdruck* ist ein **datetime2** Wert.  
  
 Eine Übersicht über alle [!INCLUDE[tsql](../../includes/tsql-md.md)] Datums-und Uhrzeitdatentypen und Funktionen finden Sie unter [Datums- und Uhrzeitdatentypen und-Funktionen &#40; Transact-SQL &#41; ](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md). Beachten Sie, dass der Bereich für Datums-/Uhrzeitdaten zwischen 1753-01-01 und 9999-12-31 liegt, während der Bereich für Datumsdaten zwischen 0001-01-01 und 9999-12-31 liegt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
ISDATE ( expression )  
```  
  
## <a name="arguments"></a>Argumente  
 *expression*  
 Eine Zeichenfolge oder [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) in eine Zeichenfolge konvertiert werden kann. Der Ausdruck muss weniger als 4000 Zeichen umfassen. Datums- und Uhrzeitdatentypen, mit Ausnahme von datetime und smalldatetime, sind nicht als Argument für ISDATE zugelassen.  
  
## <a name="return-type"></a>Rückgabetyp  
 **int**  
  
## <a name="remarks"></a>Hinweise  
 ISDATE ist nur deterministisch bei Verwendung mit der [konvertieren](../../t-sql/functions/cast-and-convert-transact-sql.md) funktionieren, wenn der Style-Parameter von CONVERT angegeben ist, und Stil nicht gleich 0, 100, 9 oder 109 ist.  
  
 Der Rückgabewert von ISDATE hängt von den Einstellungen festlegen, indem [SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md), [SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md) und [Konfigurieren der Serverkonfigurationsoption Standardsprache](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md).  
  
## <a name="isdate-expression-formats"></a>Formate von ISDATE-Ausdrücken  
 Beispiele für gültige Formate für die ISDATE 1 zurück, finden Sie im Abschnitt "Unterstützte Formate der Zeichenfolgenliterale für Datetime" in der ["DateTime"](../../t-sql/data-types/datetime-transact-sql.md) und [Smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md) Themen. Weitere Beispiele auch finden Sie unter der Spalte Eingabe/Ausgabe des Abschnitts "Argumente" [CAST und CONVERT](../../t-sql/functions/cast-and-convert-transact-sql.md).  
  
 In der folgenden Tabelle werden ungültige Formate für Eingabeausdrücke zusammengefasst, die den Wert 0 oder einen Fehler zurückgeben.  
  
|ISDATE-Ausdruck|ISDATE-Rückgabewert|  
|-----------------------|-------------------------|  
|NULL|0|  
|Werte von Datentypen in aufgeführt [Datentypen](../../t-sql/data-types/data-types-transact-sql.md) in jeder beliebigen Datentypkategorie außer Zeichenfolgen, Unicode-Zeichenfolgen oder Datum und Uhrzeit.|0|  
|Werte des **Text**, **Ntext**, oder **Image** -Datentypen.|0|  
|Beliebiger Wert mit mehr als drei Dezimalstellen (.0000 bis .0000000... n) für die Genauigkeit bei Sekundenangaben. ISDATE gibt 0 zurück, wenn die *Ausdruck* ist ein **datetime2** , aber es gibt 1 zurück, wenn die *Ausdruck* ist ein gültiger **"DateTime"** Wert.|0|  
|Beliebiger Wert, der ein gültiges Datum mit einem ungültigen Wert kombiniert, z. B. 1995-10-1a.|0|  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-isdate-to-test-for-a-valid-datetime-expression"></a>A. Verwenden von ISDATE, um auf einen gültigen datetime-Ausdruck zu testen  
 Im folgenden Beispiel veranschaulicht das verwenden `ISDATE` zu prüfen, ob eine Zeichenfolge ein gültiger ist **"DateTime"**.  
  
```  
IF ISDATE('2009-05-12 10:19:41.177') = 1  
    PRINT 'VALID'  
ELSE  
    PRINT 'INVALID';  
```  
  
### <a name="b-showing-the-effects-of-the-set-dateformat-and-set-language-settings-on-return-values"></a>B. Anzeigen der Auswirkungen der SET DATEFORMAT-Einstellung und der SET LANGUAGE-Einstellung auf Rückgabewerte  
 Die folgenden Anweisungen zeigen die Werte, die als Ergebnis der Einstellungen von `SET DATEFORMAT` und `SET LANGUAGE` zurückgegeben werden.  
  
```  
/* Use these sessions settings. */  
SET LANGUAGE us_english;  
SET DATEFORMAT mdy;  
/* Expression in mdy dateformat */  
SELECT ISDATE('04/15/2008'); --Returns 1.  
/* Expression in mdy dateformat */  
SELECT ISDATE('04-15-2008'); --Returns 1.   
/* Expression in mdy dateformat */  
SELECT ISDATE('04.15.2008'); --Returns 1.   
/* Expression in myd  dateformat */  
SELECT ISDATE('04/2008/15'); --Returns 1.  
  
SET DATEFORMAT mdy;  
SELECT ISDATE('15/04/2008'); --Returns 0.  
SET DATEFORMAT mdy;  
SELECT ISDATE('15/2008/04'); --Returns 0.  
SET DATEFORMAT mdy;  
SELECT ISDATE('2008/15/04'); --Returns 0.  
SET DATEFORMAT mdy;  
SELECT ISDATE('2008/04/15'); --Returns 1.  
  
SET DATEFORMAT dmy;  
SELECT ISDATE('15/04/2008'); --Returns 1.  
SET DATEFORMAT dym;  
SELECT ISDATE('15/2008/04'); --Returns 1.  
SET DATEFORMAT ydm;  
SELECT ISDATE('2008/15/04'); --Returns 1.  
SET DATEFORMAT ymd;  
SELECT ISDATE('2008/04/15'); --Returns 1.  
  
SET LANGUAGE English;  
SELECT ISDATE('15/04/2008'); --Returns 0.  
SET LANGUAGE Hungarian;  
SELECT ISDATE('15/2008/04'); --Returns 0.  
SET LANGUAGE Swedish;  
SELECT ISDATE('2008/15/04'); --Returns 0.  
SET LANGUAGE Italian;  
SELECT ISDATE('2008/04/15'); --Returns 1.  
  
/* Return to these sessions settings. */  
SET LANGUAGE us_english;  
SET DATEFORMAT mdy;  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-isdate-to-test-for-a-valid-datetime-expression"></a>C. Verwenden von ISDATE, um auf einen gültigen datetime-Ausdruck zu testen  
 Im folgenden Beispiel veranschaulicht das verwenden `ISDATE` zu prüfen, ob eine Zeichenfolge ein gültiger ist **"DateTime"**.  
  
```  
IF ISDATE('2009-05-12 10:19:41.177') = 1  
    SELECT 'VALID';  
ELSE  
    SELECT 'INVALID';  
```  
  
## <a name="see-also"></a>Siehe auch  
 [CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  


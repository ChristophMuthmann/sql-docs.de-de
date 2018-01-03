---
title: EOMONTH (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
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
- EOMONTH
- EOMONTH_TSQL
dev_langs: TSQL
helpviewer_keywords: EOMONTH function
ms.assetid: 1d060d8e-3297-4244-afef-57df2f8f92e2
caps.latest.revision: "19"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: af048d17aadfece5e1deecf8a5aa4b008f1bd0fd
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/02/2018
---
# <a name="eomonth-transact-sql"></a>EOMONTH (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  Gibt den letzten Tag des Monats, der das angegebene Datum enthält, mit einem optionalen Versatz zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
EOMONTH ( start_date [, month_to_add ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *' Startdatum '.*  
 Datumsausdruck, der das Datum angibt, für das der letzte Tag des Monats zurückgegeben werden soll.  
  
 *month_to_add*  
 Angeben der Anzahl von Monaten für das Hinzufügen optionaler Ganzzahlausdruck *Start_date*.  
  
 Wenn dieses Argument, klicken Sie dann angegeben wird **EOMONTH** fügt die angegebene Anzahl von Monaten für das *Start_date*, und gibt dann den letzten Tag des Monats für das resultierende Datum zurück. Wenn durch das Hinzufügen der gültige Datumsbereich überschritten wird, wird ein Fehler ausgegeben.  
  
## <a name="return-type"></a>Rückgabetyp  
 **Datum**  
  
## <a name="remarks"></a>Hinweise  
 Diese Funktion kann remote auf Servern mit [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] oder einer höheren Version ausgeführt werden. Sie kann nicht remote mit einer Version vor [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ausgeführt werden.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-eomonth-with-explicit-datetime-type"></a>A. EOMONTH mit explizitem datetime-Typ  
  
```  
DECLARE @date DATETIME = '12/1/2011';  
SELECT EOMONTH ( @date ) AS Result;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
------------  
2011-12-31  
  
(1 row(s) affected)  
```  
  
### <a name="b-eomonth-with-string-parameter-and-implicit-conversion"></a>B. EOMONTH mit Zeichenfolgenparameter und impliziter Konvertierung  
  
```  
DECLARE @date VARCHAR(255) = '12/1/2011';  
SELECT EOMONTH ( @date ) AS Result;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
------------  
2011-12-31  
  
(1 row(s) affected)  
```  
  
### <a name="c-eomonth-with-and-without-the-monthtoadd-parameter"></a>C. EOMONTH mit und ohne den month_to_add-Parameter  
  
```sql  
DECLARE @date DATETIME = GETDATE();  
SELECT EOMONTH ( @date ) AS 'This Month';  
SELECT EOMONTH ( @date, 1 ) AS 'Next Month';  
SELECT EOMONTH ( @date, -1 ) AS 'Last Month';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
This Month  
-----------------------  
2011-12-31  
  
(1 row(s) affected)  
  
Next Month  
-----------------------  
2012-01-31  
  
(1 row(s) affected)  
  
Last Month  
-----------------------  
2011-11-30  
  
(1 row(s) affected)  
```  
  
  


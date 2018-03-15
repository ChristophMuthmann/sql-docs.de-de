---
title: TIMEFROMPARTS (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/04/2017
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
- TIMEFROMPARTS_TSQL
- TIMEFROMPARTS
dev_langs:
- TSQL
helpviewer_keywords:
- TIMEFROMPARTS function
ms.assetid: 786c65a1-2b3f-4e4b-82b6-4940d62f3801
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 5e046e203e7ebd5243cdfc6f10948dfd353b2dd3
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/02/2018
---
# <a name="timefromparts-transact-sql"></a>TIMEFROMPARTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  Gibt einen **time**-Wert für die angegebene Uhrzeit mit der angegebenen Genauigkeit zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
TIMEFROMPARTS ( hour, minute, seconds, fractions, precision )  
```  
  
## <a name="arguments"></a>Argumente  
 *hour*  
 Ganzzahliger Ausdruck, der die Stunden angibt.  
  
 *minute*  
 Ganzzahliger Ausdruck, der die Minuten angibt.  
  
 *Sekunden*  
 Ganzzahliger Ausdruck, der die Sekunden angibt.  
  
 *fractions*  
 Ganzzahliger Ausdruck, der die Sekundenbruchteile angibt.  
  
 *precision*  
 Ganzzahliges Literal, das die Genauigkeit des zurückzugebenden **time**-Werts angibt.  
  
## <a name="return-types"></a>Rückgabetypen  
 **time(** *precision* **)**  
  
## <a name="remarks"></a>Remarks  
 TIMEROMPARTS gibt einen vollständig initialisierten Uhrzeitwert zurück. Wenn die Argumente ungültig sind, wird ein Fehler ausgegeben. Wenn einer der Parameter einen NULL-Wert aufweist, wird NULL zurückgegeben. Wenn jedoch das *precision*-Argument NULL ist, wird ein Fehler ausgelöst.  
  
 Das *fractions*-Argument ist vom *precision*-Argument abhängig. Wenn beispielsweise *precision* den Wert 7 hat, stellt jeder Bruchteil 100 Nanosekunden dar. Ist *precision* jedoch 3, stellt jeder Bruchteil eine Millisekunde dar. Wenn der Wert von *precision* 0 (null) ist, muss auch der Wert von *fractions* 0 (null) sein; andernfalls wird ein Fehler ausgelöst.  
  
 Diese Funktion kann remote auf Servern mit [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] oder einer höheren Version ausgeführt werden. Sie kann nicht remote auf Servern mit einer Version vor [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ausgeführt werden.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-simple-example-without-fractions-of-a-second"></a>A. Einfaches Beispiel ohne Sekundenbruchteile  
  
```  
SELECT TIMEFROMPARTS ( 23, 59, 59, 0, 0 ) AS Result;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
--------------------  
23:59:59.0000000  
  
(1 row(s) affected)  
```  
  
### <a name="b-example-with-fractions-of-a-second"></a>B. Beispiel mit Sekundenbruchteilen  
 Das folgende Beispiel zeigt die Verwendung der Parameter *fractions* und *precision*:  
  
1.  Wenn *fractions* den Wert 5 und *precision* den Wert 1 hat, stellt der Wert von *fractions* 5/10 einer Sekunde dar.  
  
2.  Wenn *fractions* den Wert 50 und *precision* den Wert 2 hat, stellt der Wert von *fractions* 50/100 einer Sekunde dar.  
  
3.  Wenn *fractions* den Wert 500 und *precision* den Wert 3 hat, stellt der Wert von *fractions* 500/1000 einer Sekunde dar.  
  
```sql  
SELECT TIMEFROMPARTS ( 14, 23, 44, 5, 1 );  
SELECT TIMEFROMPARTS ( 14, 23, 44, 50, 2 );  
SELECT TIMEFROMPARTS ( 14, 23, 44, 500, 3 );  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----------------  
14:23:44.5  
  
(1 row(s) affected)  
  
----------------  
14:23:44.50  
  
(1 row(s) affected)  
  
----------------  
14:23:44.500  
  
(1 row(s) affected)  
```  
  


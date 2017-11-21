---
title: TIMEFROMPARTS (Transact-SQL) | Microsoft Docs
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
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: e7cb7497251a0a61cff9f71c07d3c5d9e9028d5d
ms.contentlocale: de-de
ms.lasthandoff: 10/17/2017

---
# <a name="timefromparts-transact-sql"></a>TIMEFROMPARTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  Gibt eine **Zeit** Wert für die angegebene Zeit und mit der angegebenen Genauigkeit.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
TIMEFROMPARTS ( hour, minute, seconds, fractions, precision )  
```  
  
## <a name="arguments"></a>Argumente  
 *Stunde*  
 Ganzzahliger Ausdruck, der die Stunden angibt.  
  
 *Minute*  
 Ganzzahliger Ausdruck, der die Minuten angibt.  
  
 *Sekunden*  
 Ganzzahliger Ausdruck, der die Sekunden angibt.  
  
 *Addieren von Brüchen*  
 Ganzzahliger Ausdruck, der die Sekundenbruchteile angibt.  
  
 *precision*  
 Ganzzahliges Literal, die angibt, die **Zeit** Wert, der zurückgegeben werden.  
  
## <a name="return-types"></a>Rückgabetypen  
 **Zeit (** *Genauigkeit* **)**  
  
## <a name="remarks"></a>Hinweise  
 TIMEROMPARTS gibt einen vollständig initialisierten Uhrzeitwert zurück. Wenn die Argumente ungültig sind, wird ein Fehler ausgegeben. Wenn einer der Parameter einen NULL-Wert aufweist, wird NULL zurückgegeben. Jedoch, wenn die *Genauigkeit* Argument null ist, wird ein Fehler ausgelöst.  
  
 Die *Brüche* Argument richtet sich nach der *Genauigkeit* Argument. Z. B. wenn *Genauigkeit* 7 ist, dann stellt jeder Bruchteil 100 Nanosekunden; dar, wenn *Genauigkeit* 3 ist, und klicken Sie dann jeder Bruchteil eine Millisekunde dar. Wenn der Wert der *Genauigkeit* ist 0 (null), und klicken Sie dann auf den Wert der *Brüche* muss auch werden 0 (null) ist; andernfalls ein Fehler ausgelöst.  
  
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
 Das folgende Beispiel veranschaulicht die Verwendung von der *Brüche* und *Genauigkeit* Parameter:  
  
1.  Wenn *Brüche* hat den Wert 5 und *Genauigkeit* hat den Wert 1, klicken Sie dann den Wert der *Brüche* 5/10 Sekunde darstellt.  
  
2.  Wenn *Brüche* verfügt über einen Wert von 50 und *Genauigkeit* hat den Wert 2, klicken Sie dann den Wert der *Brüche* 50/100 einer Sekunde darstellt.  
  
3.  Wenn *Brüche* hat den Wert 500 und *Genauigkeit* hat den Wert 3, klicken Sie dann den Wert der *Brüche* 500/1000 einer Sekunde darstellt.  
  
```tsql  
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
  



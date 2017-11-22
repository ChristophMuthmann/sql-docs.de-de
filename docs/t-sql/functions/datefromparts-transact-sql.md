---
title: DATEFROMPARTS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/29/2017
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
- DATEFROMPARTS_TSQL
- DATEFROMPARTS
dev_langs: TSQL
helpviewer_keywords: DATEFROMPARTS function
ms.assetid: 5b885376-87aa-41f1-9e18-04987aead250
caps.latest.revision: "16"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 73d2edfd6f0d19c4383b0bdbe1271d74a0ef2b6f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="datefromparts-transact-sql"></a>DATEFROMPARTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

Gibt eine **Datum** Wert für den angegebenen Werten für Jahr, Monat und Tag.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
DATEFROMPARTS ( year, month, day )  
```  
  
## <a name="arguments"></a>Argumente  
*Jahr*  
Ganzzahliger Ausdruck, der ein Jahr angibt.
  
*Monat*  
Ganzzahliger Ausdruck, der einen Monat angibt (von 1 bis 12).
  
*Tag*  
Ganzzahliger Ausdruck, der einen Tag angibt.
  
## <a name="return-types"></a>Rückgabetypen
**Datum**
  
## <a name="remarks"></a>Hinweise  
**DATEFROMPARTS** gibt eine **Datum** Wert mit den Datumsteil legen Sie auf den angegebenen Werten für Jahr, Monat und Tag und den Zeitbereich, der auf den Standardwert festgelegt. Wenn die Argumente nicht gültig sind, wird ein Fehler ausgelöst. Wenn erforderliche Argumente den Wert NULL haben, wird NULL zurückgegeben.
  
Diese Funktion kann remote auf [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]-Servern oder höher ausgeführt werden. Eine Remoteausführung auf Servern mit einer Version unter [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ist nicht möglich.
  
## <a name="examples"></a>Beispiele  
Das folgende Beispiel veranschaulicht die **DATEFROMPARTS** Funktion.
  
```sql
SELECT DATEFROMPARTS ( 2010, 12, 31 ) AS Result;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
----------------------------------  
2010-12-31  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Siehe auch
[date &#40;Transact-SQL&#41;](../../t-sql/data-types/date-transact-sql.md)
  
  


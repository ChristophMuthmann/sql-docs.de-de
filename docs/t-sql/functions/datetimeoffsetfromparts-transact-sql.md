---
title: DATETIMEOFFSETFROMPARTS (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DATETIMEOFFSETFROMPARTS_TSQL
- DATETIMEOFFSETFROMPARTS
dev_langs:
- TSQL
helpviewer_keywords:
- DATETIMEOFFSETFROMPARTS function
ms.assetid: 463da1f4-b4b6-45a3-9a95-ea1f99575542
caps.latest.revision: 19
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 2ad617b97020c23e0f3cfc2ea52da674ac380404
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="datetimeoffsetfromparts-transact-sql"></a>DATETIMEOFFSETFROMPARTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

Gibt einen **datetimeoffset**-Wert für das angegebene Datum und die angegebene Uhrzeit mit dem angegebenen Offset und der angegebenen Genauigkeit zurück.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
DATETIMEOFFSETFROMPARTS ( year, month, day, hour, minute, seconds, fractions, hour_offset, minute_offset, precision )  
```  
  
## <a name="arguments"></a>Argumente  
*year*  
Ganzzahliger Ausdruck, der ein Jahr angibt.
  
*month*  
Ganzzahliger Ausdruck, der einen Monat angibt.
  
*day*  
Ganzzahliger Ausdruck, der einen Tag angibt.
  
*hour*  
Ganzzahliger Ausdruck, der die Stunden angibt.
  
*minute*  
Ganzzahliger Ausdruck, der die Minuten angibt.
  
*Sekunden*  
Ganzzahliger Ausdruck, der die Sekunden angibt.
  
*fractions*  
Ganzzahliger Ausdruck, der die Sekundenbruchteile angibt.
  
*hour_offset*  
Ganzzahliger Ausdruck, der den Stundenteil des Zeitzonenoffsets angibt.
  
*minute_offset*  
Ganzzahliger Ausdruck, der den Minutenteil des Zeitzonenoffsets angibt.
  
*precision*  
Ganzzahliges Literal, der die Genauigkeit des zurückzugebenden **datetimeoffset**-Werts angibt.
  
## <a name="return-types"></a>Rückgabetypen
**datetimeoffset(** *Genauigkeit* **)**
  
## <a name="remarks"></a>Remarks  
**DATETIMEOFFSETFROMPARTS** gibt einen vollständig initialisierten **datetimeoffset**-Datentyp zurück. Die Offsetargumente werden verwendet, um den Zeitzonenoffset darzustellen. Werden die Offsetargumente nicht angegeben, wird als Zeitzonenoffset 00:00 angenommen, d. h. es gibt keinen Zeitzonenoffset. Wenn die Offsetargumente angegeben werden, dann müssen beide Argumente vorhanden und beide Argumente entweder positiv oder negativ sein. Wenn *minute_offset* ohne *hour_offset* angegeben wird, wird ein Fehler ausgelöst. Wenn andere Argumente ungültig sind, wird ein Fehler ausgegeben. Wenn erforderliche Argumente den Wert NULL haben, wird auch NULL zurückgegeben. Wenn jedoch das *precision*-Argument NULL ist, wird ein Fehler ausgelöst.
  
Das *fractions*-Argument ist vom *precision*-Argument abhängig. Wenn beispielsweise *precision* den Wert 7 hat, stellt jeder Bruchteil 100 Nanosekunden dar. Ist *precision* jedoch 3, stellt jeder Bruchteil eine Millisekunde dar. Wenn der Wert von *precision* 0 (null) ist, muss auch der Wert von *fractions* 0 (null) sein; andernfalls wird ein Fehler ausgelöst.
  
Diese Funktion kann remote auf [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]-Servern oder höher ausgeführt werden. Eine Remoteausführung auf Servern mit einer Version vor [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ist nicht möglich.
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-simple-example-without-fractions-of-a-second"></a>A. Einfaches Beispiel ohne Sekundenbruchteile  
  
```sql
SELECT DATETIMEOFFSETFROMPARTS ( 2010, 12, 31, 14, 23, 23, 0, 12, 0, 7 ) AS Result;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
-------------------------------------------  
2010-12-07 00:00:00.0000000 +00:00  
  
(1 row(s) affected)  
```  
  
### <a name="b-example-with-fractions-of-a-second"></a>B. Beispiel mit Sekundenbruchteilen  
Das folgende Beispiel zeigt die Verwendung der Parameter *fractions* und *precision*:
1.   Wenn *fractions* den Wert 5 und *precision* den Wert 1 hat, stellt der Wert von *fractions* 5/10 einer Sekunde dar.  
1.   Wenn *fractions* den Wert 50 und *precision* den Wert 2 hat, stellt der Wert von *fractions* 50/100 einer Sekunde dar.  
1.   Wenn *fractions* den Wert 500 und *precision* den Wert 3 hat, stellt der Wert von *fractions* 500/1000 einer Sekunde dar.  
  
```sql
SELECT DATETIMEOFFSETFROMPARTS ( 2011, 8, 15, 14, 30, 00, 5, 12, 30, 1 );  
SELECT DATETIMEOFFSETFROMPARTS ( 2011, 8, 15, 14, 30, 00, 50, 12, 30, 2 );  
SELECT DATETIMEOFFSETFROMPARTS ( 2011, 8, 15, 14, 30, 00, 500, 12, 30, 3 );  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
----------------------------------  
2011-08-15 14:30:00.5 +12:30  
  
(1 row(s) affected)  
  
----------------------------------  
2011-08-15 14:30:00.50 +12:30  
  
(1 row(s) affected)  
  
----------------------------------  
2011-08-15 14:30:00.500 +12:30  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Siehe auch
[datetimeoffset &#40;Transact-SQL&#41;](../../t-sql/data-types/datetimeoffset-transact-sql.md)  
[AT TIME ZONE &#40;Transact-SQL&#41;](../../t-sql/queries/at-time-zone-transact-sql.md)
  
  



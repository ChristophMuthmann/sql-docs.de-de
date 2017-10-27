---
title: DATETIMEOFFSETFROMPARTS (Transact-SQL) | Microsoft Docs
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
- DATETIMEOFFSETFROMPARTS_TSQL
- DATETIMEOFFSETFROMPARTS
dev_langs:
- TSQL
helpviewer_keywords:
- DATETIMEOFFSETFROMPARTS function
ms.assetid: 463da1f4-b4b6-45a3-9a95-ea1f99575542
caps.latest.revision: 19
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: 665607c3b6ea9411d90137fba416d96d3d46a4c1
ms.contentlocale: de-de
ms.lasthandoff: 10/17/2017

---
# <a name="datetimeoffsetfromparts-transact-sql"></a>DATETIMEOFFSETFROMPARTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all_md](../../includes/tsql-appliesto-ss2012-all-md.md)]

Gibt eine **"DateTimeOffset"** -Wert für das angegebene Datum und die Uhrzeit mit den angegebenen Offsets und die Genauigkeit.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
DATETIMEOFFSETFROMPARTS ( year, month, day, hour, minute, seconds, fractions, hour_offset, minute_offset, precision )  
```  
  
## <a name="arguments"></a>Argumente  
*Jahr*  
Ganzzahliger Ausdruck, der ein Jahr angibt.
  
*Monat*  
Ganzzahliger Ausdruck, der einen Monat angibt.
  
*Tag*  
Ganzzahliger Ausdruck, der einen Tag angibt.
  
*Stunde*  
Ganzzahliger Ausdruck, der die Stunden angibt.
  
*Minute*  
Ganzzahliger Ausdruck, der die Minuten angibt.
  
*Sekunden*  
Ganzzahliger Ausdruck, der die Sekunden angibt.
  
*Addieren von Brüchen*  
Ganzzahliger Ausdruck, der die Sekundenbruchteile angibt.
  
*hour_offset*  
Ganzzahliger Ausdruck, der den Stundenteil des Zeitzonenoffsets angibt.
  
*minute_offset*  
Ganzzahliger Ausdruck, der den Minutenteil des Zeitzonenoffsets angibt.
  
*precision*  
Ganzzahliges Literal, die angibt, die **"DateTimeOffset"** Wert, der zurückgegeben werden.
  
## <a name="return-types"></a>Rückgabetypen
**"DateTimeOffset" (** *Genauigkeit* **)**
  
## <a name="remarks"></a>Hinweise  
**DATETIMEOFFSETFROMPARTS** gibt einen vollständig initialisierten **"DateTimeOffset"** -Datentyp. Die Offsetargumente werden verwendet, um den Zeitzonenoffset darzustellen. Werden die Offsetargumente nicht angegeben, wird als Zeitzonenoffset 00:00 angenommen, d. h. es gibt keinen Zeitzonenoffset. Wenn die Offsetargumente angegeben werden, dann müssen beide Argumente vorhanden und beide Argumente entweder positiv oder negativ sein. Wenn *Minute_offset* wird angegeben, ohne *Hour_offset*, wird ein Fehler ausgelöst. Wenn andere Argumente ungültig sind, wird ein Fehler ausgegeben. Wenn erforderliche Argumente null sind, wird Null zurückgegeben. Jedoch, wenn die *Genauigkeit* Argument null ist, wird ein Fehler ausgelöst.
  
Die *Brüche* Argument richtet sich nach der *Genauigkeit* Argument. Z. B. wenn *Genauigkeit* 7 ist, dann stellt jeder Bruchteil 100 Nanosekunden; dar, wenn *Genauigkeit* 3 ist, und klicken Sie dann jeder Bruchteil eine Millisekunde dar. Wenn der Wert der *Genauigkeit* ist 0 (null), und klicken Sie dann auf den Wert der *Brüche* muss auch werden 0 (null) ist; andernfalls ein Fehler ausgelöst.
  
Diese Funktion kann remote auf [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]-Servern oder höher ausgeführt werden. Sie werden nicht in der Remoteausführung auf Servern, auf denen eine Version unter [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].
  
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
Das folgende Beispiel veranschaulicht die Verwendung von der *Brüche* und *Genauigkeit* Parameter:
1.   Wenn *Brüche* hat den Wert 5 und *Genauigkeit* hat den Wert 1, klicken Sie dann den Wert der *Brüche* 5/10 Sekunde darstellt.  
1.   Wenn *Brüche* verfügt über einen Wert von 50 und *Genauigkeit* hat den Wert 2, klicken Sie dann den Wert der *Brüche* 50/100 einer Sekunde darstellt.  
1.   Wenn *Brüche* hat den Wert 500 und *Genauigkeit* hat den Wert 3, klicken Sie dann den Wert der *Brüche* 500/1000 einer Sekunde darstellt.  
  
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
[ZEITZONE &AMP;#40; Transact-SQL &#41;](../../t-sql/queries/at-time-zone-transact-sql.md)
  
  




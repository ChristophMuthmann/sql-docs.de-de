---
title: DATETIME2FROMPARTS (Transact-SQL) | Microsoft Docs
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
- DATETIME2FROMPARTS_TSQL
- DATETIME2FROMPARTS
dev_langs:
- TSQL
helpviewer_keywords:
- DATETIME2FROMPARTS function
ms.assetid: 632b757d-d2d1-43a5-b870-792a779ae204
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c4ad800c684bcf69a52828969ca816a135901280
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="datetime2fromparts-transact-sql"></a>DATETIME2FROMPARTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all_md](../../includes/tsql-appliesto-ss2012-all-md.md)]

Gibt eine **datetime2** -Wert für das angegebene Datum und die Uhrzeit mit der angegebenen Genauigkeit.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
DATETIME2FROMPARTS ( year, month, day, hour, minute, seconds, fractions, precision )  
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
  
*Minute* Ganzzahlausdruck Minuten angeben.
  
*Sekunden*  
Ganzzahliger Ausdruck, der die Sekunden angibt.
  
*Addieren von Brüchen*  
Ganzzahliger Ausdruck, der die Sekundenbruchteile angibt.
  
*precision*  
Ganzzahliges Literal, die angibt, die **datetime2** Wert, der zurückgegeben werden.
  
## <a name="return-types"></a>Rückgabetypen
**datetime2 (** *Genauigkeit* **)**
  
## <a name="remarks"></a>Hinweise  
**DATETIME2FROMPARTS** gibt einen vollständig initialisierten **datetime2** Wert. Wenn die Argumente nicht gültig sind, wird ein Fehler ausgelöst. Wenn erforderliche Argumente den Wert NULL haben, wird NULL zurückgegeben. Jedoch, wenn die *Genauigkeit* Argument null ist, wird ein Fehler ausgelöst.
  
Die *Brüche* Argument richtet sich nach der *Genauigkeit* Argument. Z. B. wenn *Genauigkeit* 7 ist, dann stellt jeder Bruchteil 100 Nanosekunden; dar, wenn *Genauigkeit* 3 ist, und klicken Sie dann jeder Bruchteil eine Millisekunde dar. Wenn der Wert der *Genauigkeit* ist 0 (null), und klicken Sie dann auf den Wert der *Brüche* muss auch werden 0 (null) ist; andernfalls ein Fehler ausgelöst.
  
Diese Funktion kann remote auf [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]-Servern oder höher ausgeführt werden. Sie werden nicht in der Remoteausführung auf Servern, auf denen eine Version unter [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-simple-example-without-fractions-of-a-second"></a>A. Einfaches Beispiel ohne Sekundenbruchteile  
  
```sql
SELECT DATETIME2FROMPARTS ( 2010, 12, 31, 23, 59, 59, 0, 0 ) AS Result;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
---------------------------  
2010-12-31 23:59:59.0000000  
  
(1 row(s) affected)  
```  
  
### <a name="b-example-with-fractions-of-a-second"></a>B. Beispiel mit Sekundenbruchteilen  
Das folgende Beispiel veranschaulicht die Verwendung von der *Brüche* und *Genauigkeit* Parameter:
  
1.  Wenn *Brüche* hat den Wert 5 und *Genauigkeit* hat den Wert 1, klicken Sie dann den Wert der *Brüche* 5/10 Sekunde darstellt.  
  
2.  Wenn *Brüche* verfügt über einen Wert von 50 und *Genauigkeit* hat den Wert 2, klicken Sie dann den Wert der *Brüche* 50/100 einer Sekunde darstellt.  
  
3.  Wenn *Brüche* hat den Wert 500 und *Genauigkeit* hat den Wert 3, klicken Sie dann den Wert der *Brüche* 500/1000 einer Sekunde darstellt.  
  
```sql
SELECT DATETIME2FROMPARTS ( 2011, 8, 15, 14, 23, 44, 5, 1 );  
SELECT DATETIME2FROMPARTS ( 2011, 8, 15, 14, 23, 44, 50, 2 );  
SELECT DATETIME2FROMPARTS ( 2011, 8, 15, 14, 23, 44, 500, 3 );  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
----------------------  
2011-08-15 14:23:44.5  
  
(1 row(s) affected)  
  
----------------------  
2011-08-15 14:23:44.50  
  
(1 row(s) affected)  
  
----------------------  
2011-08-15 14:23:44.500  
  
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-simple-example-without-fractions-of-a-second"></a>C. Einfaches Beispiel ohne Sekundenbruchteile  
  
```sql
SELECT DATETIME2FROMPARTS ( 2010, 12, 31, 23, 59, 59, 0, 0 ) AS Result;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
---------------------------  
2010-12-31 23:59:59.0000000  
  
(1 row(s) affected)  
```  
  
### <a name="d-example-with-fractions-of-a-second"></a>D. Beispiel mit Sekundenbruchteilen  
Das folgende Beispiel veranschaulicht die Verwendung von der *Brüche* und *Genauigkeit* Parameter:
1.  Wenn *Brüche* hat den Wert 5 und *Genauigkeit* hat den Wert 1, klicken Sie dann den Wert der *Brüche* 5/10 Sekunde darstellt.  
1.   Wenn *Brüche* verfügt über einen Wert von 50 und *Genauigkeit* hat den Wert 2, klicken Sie dann den Wert der *Brüche* 50/100 einer Sekunde darstellt.  
1.   Wenn *Brüche* hat den Wert 500 und *Genauigkeit* hat den Wert 3, klicken Sie dann den Wert der *Brüche* 500/1000 einer Sekunde darstellt.  
  
```sql
SELECT DATETIME2FROMPARTS ( 2011, 8, 15, 14, 23, 44, 5, 1 );  
SELECT DATETIME2FROMPARTS ( 2011, 8, 15, 14, 23, 44, 50, 2 );  
SELECT DATETIME2FROMPARTS ( 2011, 8, 15, 14, 23, 44, 500, 3 );  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
----------------------  
2011-08-15 14:23:44.5  
  
(1 row(s) affected)  
  
----------------------  
2011-08-15 14:23:44.50  
  
(1 row(s) affected)  
  
----------------------  
2011-08-15 14:23:44.500  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Siehe auch
[datetime2 &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime2-transact-sql.md)
  
  



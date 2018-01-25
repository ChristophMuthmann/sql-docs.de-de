---
title: Bitweise Operatoren (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 09/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- operators [Transact-SQL], bitwise
- bitwise operators
- bit manipulations
ms.assetid: 2b994cf5-2daa-438a-b8c7-4bd8d451ac8d
caps.latest.revision: "29"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: b0706080c0a878987fab8d2cc5f0c1677f43309b
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="bitwise-operators-transact-sql"></a>Bitweise Operatoren (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Bitweise Operatoren bearbeiten Bits aus zwei Ausdrücken eines Datentyps der ganzzahligen Datentypkategorie.  
  Bitweise Operatoren konvertieren von zwei ganzzahligen Werten in binäre Bits, führen Sie AND, OR oder NOT-Operation auf jedes Bit, Erzeugen eines Ergebnisses. Das Ergebnis wird dann in eine ganze Zahl konvertiert.  
  
  Beispielsweise konvertiert die ganze Zahl 170 auf binäre 1010 1010.
Die Ganzzahl 75 konvertiert in binäre 0100 1011.

|Operator|bitweise mathematische Funktionen|
|---- |---- |
|AND <br> Wenn Bits an einer beliebigen Position 1 sind, ist das Ergebnis 1. |1010 1010 = 170 <br>0100 1011 =  75 <br>-----------------  <br> 0000 1010 =  10 |
|OR <br> Wenn jedes Bit an einer beliebigen Position 1 ist, ist das Ergebnis 1. |1010 1010 = 170 <br>0100 1011 =  75 <br>-----------------  <br> 1110 1011 = 235|
|NICHT  <br> Kehrt den Bitwert an jedem Standort Bit. |1010 1010 = 170 <br>----------------- <br>  0101 0101 =   85 |
  
Finden Sie unter den folgenden Themen:   
* [& &#40; Bitweises AND &#41;](../../t-sql/language-elements/bitwise-and-transact-sql.md)  
* [& = &#40; Bitweise AND-Zuweisung &#41;](../../t-sql/language-elements/bitwise-and-equals-transact-sql.md)   
* [&#124; &#40; Bitweises OR &#41;](../../t-sql/language-elements/bitwise-or-transact-sql.md)  
* [&#124; = &#40; Bitweise OR-Zuweisung &#41;](../../t-sql/language-elements/bitwise-or-equals-transact-sql.md)   
* [^ &#40; Bitweises exklusives OR &#41;](../../t-sql/language-elements/bitwise-exclusive-or-transact-sql.md)  
* [^ = &#40; Bitweises exklusives OR-Zuweisung &#41;](../../t-sql/language-elements/bitwise-exclusive-or-equals-transact-sql.md)  
* [~ &#40; Bitweises NOT &#41;](../../t-sql/language-elements/bitwise-not-transact-sql.md)  
  
 Die Operanden für bitweise Operatoren können eines der Datentypen der ganzzahligen oder Binärzeichenfolge Datentypkategorien werden (mit Ausnahme der **Image** -Datentyp), mit dem Unterschied, dass beide Operanden eines Datentyps der binären Zeichenfolgen sein können Datentypkategorie. In der folgenden Tabelle sind alle Datentypen aufgeführt, die für Operanden unterstützt werden.  
  
|Linker Operand|Rechter Operand|  
|------------------|-------------------|  
|[binary](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)|**Int**, **"smallint"**, oder **"tinyint"**|  
|[bit](../../t-sql/data-types/bit-transact-sql.md)|**Int**, **"smallint"**, **"tinyint"**, oder **Bit**|  
|[int](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|**Int**, **"smallint"**, **"tinyint"**, **binäre**, oder **Varbinary**|  
|[smallint](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|**Int**, **"smallint"**, **"tinyint"**, **binäre**, oder **Varbinary**|  
|[tinyint](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|**Int**, **"smallint"**, **"tinyint"**, **binäre**, oder **Varbinary**|  
|[varbinary](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)|**Int**, **"smallint"**, oder **"tinyint"**|  
  
## <a name="see-also"></a>Siehe auch  
 [Operators &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Zusammengesetzte Operatoren &#40; Transact-SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)   
  

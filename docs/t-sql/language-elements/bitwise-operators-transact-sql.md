---
title: Bitweise Operatoren (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 09/07/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- operators [Transact-SQL], bitwise
- bitwise operators
- bit manipulations
ms.assetid: 2b994cf5-2daa-438a-b8c7-4bd8d451ac8d
caps.latest.revision: 29
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 05976158e43d7dfafaf02289462d1537f5beeb36
ms.openlocfilehash: 5d04924a82578040f801864bb68905feebc53e94
ms.contentlocale: de-de
ms.lasthandoff: 09/08/2017

---
# <a name="bitwise-operators-transact-sql"></a>Bitweise Operatoren (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Bitweise Operatoren bearbeiten Bits aus zwei Ausdrücken eines Datentyps der ganzzahligen Datentypkategorie.  
  Bitweise Operatoren konvertieren von zwei ganzzahligen Werten in binäre Bits, führen Sie AND, OR oder NOT-Operation auf jedes Bit, Erzeugen eines Ergebnisses. Das Ergebnis wird dann in eine ganze Zahl konvertiert.  
  
  Beispielsweise konvertiert die ganze Zahl 170 auf binäre 1010 1010.
Die Ganzzahl 75 konvertiert in binäre 0100 1011.

|Operator|bitweise mathematische Funktionen|
|---- |---- |
|AND <br> Wenn Bits an einer beliebigen Position 1 sind, ist das Ergebnis 1. |1010 1010 = 170 <br>0100 1011 =  75 <br>-----------------  <br> 0000 1010 =  10 |
|oder <br> Wenn jedes Bit an einer beliebigen Position 1 ist, ist das Ergebnis 1. |1010 1010 = 170 <br>0100 1011 =  75 <br>-----------------  <br> 1110 1011 = 235|
|NICHT  <br> Kehrt den Bitwert an jedem Standort Bit. |1010 1010 = 170 <br>----------------- <br>  0101 0101 =   85 |
  
Finden Sie unter den folgenden Themen:   
* [& (Bitweises AND)](../../t-sql/language-elements/bitwise-and-transact-sql.md)  
* [& = (bitweises AND EQUALS)](../../t-sql/language-elements/bitwise-and-equals-transact-sql.md)   
* [&#124; (Bitweises OR)](../../t-sql/language-elements/bitwise-or-transact-sql.md)  
* [&#124; = (bitweises OR EQUALS)](../../t-sql/language-elements/bitwise-or-equals-transact-sql.md)   
* [^ (Bitweises exklusives OR)](../../t-sql/language-elements/bitwise-exclusive-or-transact-sql.md)  
* [^ = (Bitweises exklusives OR EQUALS)](../../t-sql/language-elements/bitwise-exclusive-or-equals-transact-sql.md)  
* [~ (Bitweises NOT)](../../t-sql/language-elements/bitwise-not-transact-sql.md)  
  
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
 [Operatoren &#40; Transact-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
  
  


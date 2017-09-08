---
title: '| (Bitweises OR) (Transact-SQL) | Microsoft Docs'
ms.custom: 
ms.date: 01/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '|'
- '|_TSQL'
- Bitwise OR
- bitwise
- OR
dev_langs:
- TSQL
helpviewer_keywords:
- OR operator
- bitwise OR (|)
- '| (bitwise OR operator)'
ms.assetid: 86a3b87f-9688-4eaf-a552-29f1b01d880a
caps.latest.revision: 43
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 932b8cc8997a2faec55e56786a80e511fa9c273a
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="-bitwise-or-transact-sql"></a>| (Bitweises OR) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Führt eine bitweise logische OR-Operation zwischen zwei gegebenen ganzzahligen Werten durch, die innerhalb von [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen in binäre Ausdrücke umgewandelt wurden.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```   
expression | expression  
```  
  
## <a name="arguments"></a>Argumente  
 *expression*  
 Ist ein beliebiger gültiger [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) der Datentypkategorie ' Integer ' oder die **Bit**, **binäre**, oder **Varbinary** Datentypen. *Ausdruck* wird als eine Binärzahl für die bitweise Operation behandelt.  
  
> [!NOTE]  
>  Nur ein *Ausdruck* sein **binäre** oder **Varbinary** -Datentyp in einer bitweisen Operation.  
  
## <a name="result-types"></a>Ergebnistypen  
 Gibt eine **Int** , wenn die Eingabewerte sind **Int**, **"smallint"** , wenn die Eingabewerte sind **"smallint"**, oder ein **"tinyint"** , wenn die Eingabewerte sind **"tinyint"**.  
  
## <a name="remarks"></a>Hinweise  
 Mit dem bitweisen |-Operator wird zwischen zwei Ausdrücken ein bitweises logisches OR ausgeführt, indem die jeweils entsprechenden Bits der beiden Ausdrücke verarbeitet werden. Ein Ergebnisbit wird dann auf den Wert 1 festgelegt, wenn mindestens eines der Bits (für das aktuell aufzulösende Bit) der Eingabeausdrücke den Wert 1 aufweist. Falls keines der Bits in den Eingabeausdrücken den Wert 1 hat, wird das entsprechende Bit im Ergebnis auf 0 festgelegt.  
  
 Wenn der linke und der rechte Ausdruck unterschiedliche ganzzahlige Datentypen aufweisen (z. B. Links *Ausdruck* ist **"smallint"** und das Recht *Ausdruck* ist  **Int**), wird das Argument des kleineren Datentyps in den größeren Datentyp konvertiert. In diesem Beispiel wird die **"smallint"***Ausdruck* konvertiert ein **Int**.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel erstellt eine Tabelle mit **Int** Datentypen, um die ursprünglichen Werte anzuzeigen und setzt die Tabelle in eine Zeile.  
  
```tsql  
CREATE TABLE bitwise  
(   
 a_int_value int NOT NULL,  
b_int_value int NOT NULL  
);  
GO  
INSERT bitwise VALUES (170, 75);  
GO  
```  
  
 Die folgende Abfrage führt ein bitweises OR auf die **A_int_value** und **B_int_value** Spalten.  
  
```  
SELECT a_int_value | b_int_value  
FROM bitwise;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
-----------   
235           
  
(1 row(s) affected)  
```  
  
 Die binäre Darstellung von 170 (**A_int_value** oder `A`, unten) wird `0000 0000 1010 1010`. Die binäre Darstellung von 75 (**B_int_value** oder `B`, unten) wird `0000 0000 0100 1011`. Die Anwendung einer bitweisen OR-Operation auf diese beiden Werte erzeugt das binäre Ergebnis `0000 0000 1110 1011`, was dem dezimalen Wert 235 entspricht.  
  
```  
(A | B)  
0000 0000 1010 1010  
0000 0000 0100 1011  
-------------------  
0000 0000 1110 1011  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Operatoren &#40; Transact-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [Bitweise Operatoren &#40; Transact-SQL &#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)   
 [&#124; = &#40; Bitweises OR EQUALS &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/bitwise-or-equals-transact-sql.md)   
 [Zusammengesetzte Operatoren &#40; Transact-SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)  
  
  




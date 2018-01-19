---
title: '&amp;(Bitweises AND) (Transact-SQL) | Microsoft Docs'
ms.custom: 
ms.date: 01/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- bitwise
- '&'
- '&_TSQL'
dev_langs: TSQL
helpviewer_keywords:
- AND, bitwise AND
- '& (bitwise AND)'
- bitwise AND (&)
ms.assetid: 20275755-4fa7-47b1-a9be-ac85606d63b0
caps.latest.revision: "42"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 0f81606a64480990a2f511a9820672c2cf1bb5c8
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/19/2018
---
# <a name="amp-bitwise-and-transact-sql"></a>&amp;(Bitweises AND) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Führt eine bitweise logische AND-Operation zwischen zwei ganzzahligen Werten aus.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
expression & expression  
```  
  
## <a name="arguments"></a>Argumente  
 *expression*  
 Ist ein beliebiger gültiger [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) aller die Datentypen der Datentypkategorie ' Integer ' oder die **Bit**, oder die **binäre** oder **Varbinary** Daten Typen. *Ausdruck* wird als eine Binärzahl für die bitweise Operation behandelt.  
  
> [!NOTE]  
>  In einer bitweisen Operation kann nur ein *Ausdruck* sein **binäre** oder **Varbinary** -Datentyp.  
  
## <a name="result-types"></a>Ergebnistypen  
 **Int** , wenn die Eingabewerte sind **Int**.  
  
 **"smallint"** , wenn die Eingabewerte sind **"smallint"**.  
  
 **"tinyint"** , wenn die Eingabewerte sind **"tinyint"** oder **Bit**.  
  
## <a name="remarks"></a>Hinweise  
 Die  **&**  -Operator führt eine bitweise logische AND-Operation zwischen den beiden Ausdrücken, indem die jeweils entsprechenden Bits für beide Ausdrücke. Ein Ergebnisbit wird genau dann auf den Wert 1 festgelegt, wenn beide Bits (für das aktuell aufzulösende Bit) der Eingabeausdrücke den Wert 1 aufweisen. Andernfalls wird das entsprechende Bit im Ergebnis auf 0 festgelegt.  
  
 Wenn der linke und der rechte Ausdruck unterschiedliche ganzzahlige Datentypen aufweisen (z. B. Links *Ausdruck* ist **"smallint"** und das Recht *Ausdruck* ist  **Int**), wird das Argument des kleineren Datentyps in den größeren Datentyp konvertiert. In diesem Fall die **"smallint" *** Ausdruck* konvertiert ein **Int**.  
  
## <a name="examples"></a>Beispiele  
 Im folgende Beispiel wird eine Tabelle mit den **Int** Daten geben, um die Werte zu speichern und fügt zwei Werte in eine Zeile.  
  
```  
CREATE TABLE bitwise  
(   
a_int_value int NOT NULL,  
b_int_value int NOT NULL  
);  
GO  
INSERT bitwise VALUES (170, 75);  
GO  
```  
  
 Diese Abfrage führt ein bitweises AND zwischen den Spalten `a_int_value` und `b_int_value` durch.  
  
```  
SELECT a_int_value & b_int_value  
FROM bitwise;  
GO  
```  
  
 Im Folgenden wird das Resultset aufgeführt:  
  
```  
-----------   
10            
  
(1 row(s) affected)  
```  
  
 Die binäre Darstellung von 170 (`a_int_value` oder `A`) ist `0000 0000 1010 1010`. Die binäre Darstellung von 75 (`b_int_value` oder `B`) ist `0000 0000 0100 1011`. Wird eine bitweise AND-Operation auf diese beiden Werte angewendet, resultiert daraus das binäre Ergebnis `0000 0000 0000 1010`, das dem Dezimalwert 10 entspricht.  
  
```  
(A & B)  
0000 0000 1010 1010  
0000 0000 0100 1011  
-------------------  
0000 0000 0000 1010  
```  
  
  
## <a name="see-also"></a>Siehe auch  
 [Expressions &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Operators &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [Bitweise Operatoren &#40; Transact-SQL &#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)   
 [& = &#40; Bitweise AND-Zuweisung &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/bitwise-and-equals-transact-sql.md)   
 [Zusammengesetzte Operatoren &#40; Transact-SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)  
  
  



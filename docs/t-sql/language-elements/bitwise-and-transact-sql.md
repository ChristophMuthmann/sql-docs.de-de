---
title: '&amp; (Bitweises UND) (Transact-SQL) | Microsoft-Dokumentation'
ms.custom: 
ms.date: 01/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- bitwise
- '&'
- '&_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- AND, bitwise AND
- '& (bitwise AND)'
- bitwise AND (&)
ms.assetid: 20275755-4fa7-47b1-a9be-ac85606d63b0
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 094c127434f2339a4a3e977c4455ca6ce904ab01
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="amp-bitwise-and-transact-sql"></a>&amp; (Bitweises UND) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Führt eine bitweise logische AND-Operation zwischen zwei ganzzahligen Werten aus.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
expression & expression  
```  
  
## <a name="arguments"></a>Argumente  
 *expression*  
 Ein beliebiger gültiger [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) eines beliebigen Datentyps der ganzzahligen Datentypkategorie oder des Datentyps **bit**, **binary** oder **varbinary**. *expression* wird in der bitweisen Operation als binäre Zahl behandelt.  
  
> [!NOTE]  
>  Nur eines der *expression*-Argumente kann in einer bitweisen Operation vom Datentyp **binary** oder **varbinary** sein.  
  
## <a name="result-types"></a>Ergebnistypen  
 **int**, wenn die Eingabewerte vom Typ **int** sind.  
  
 **smallint**, wenn die Eingabewerte vom Typ **smallint** sind.  
  
 **tinyint**, wenn die Eingabewerte vom Typ **tinyint** oder **bit** sind.  
  
## <a name="remarks"></a>Remarks  
 Der bitweise **&**-Operator führt eine bitweise logische UND-Operation zwischen den beiden Ausdrücken durch und verwendet die entsprechenden Bits für beide Ausdrücke. Ein Ergebnisbit wird genau dann auf den Wert 1 festgelegt, wenn beide Bits (für das aktuell aufzulösende Bit) der Eingabeausdrücke den Wert 1 aufweisen. Andernfalls wird das entsprechende Bit im Ergebnis auf 0 festgelegt.  
  
 Wenn der linke und der rechte Ausdruck unterschiedliche ganzzahlige Datentypen aufweisen (beispielsweise ist der linke *expression*-Ausdruck vom Datentyp **smallint** und der rechte *expression*-Ausdruck von Datentyp **int**), wird das Argument mit dem kleineren Datentyp in den größeren Datentyp konvertiert. In diesem Fall wird **smallint***expression* in einen **int**-Typ konvertiert.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine Tabelle mithilfe des **int**-Datentyps erstellt, um die Werte zu speichern. Zwei Werte werden in einer Zeile eingefügt.  
  
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
  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Ausdrücke &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Operators &#40;Transact-SQL&#41; (Operatoren &#40;Transact-SQL&#41;)](../../t-sql/language-elements/operators-transact-sql.md)   
 [Bitweise Operatoren &#40;Transact-SQL&#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)   
 [&= &#40;Bitwise AND Assignment&#41; &#40;Transact-SQL&#41; (&= (Bitweises UND und Zuweisung) &#40;Transact-SQL&#41;)](../../t-sql/language-elements/bitwise-and-equals-transact-sql.md)   
 [Verbundoperatoren &#40;Transact-SQL&#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)  
  
  



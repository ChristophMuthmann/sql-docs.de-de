---
title: '| (Bitweises OR) (Transact-SQL) | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 01/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|language-elements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 73a82e8d13e57aa4e14ea36c18a118431d6486b7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="-bitwise-or-transact-sql"></a>| (Bitweises OR) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Führt eine bitweise logische OR-Operation zwischen zwei gegebenen ganzzahligen Werten durch, die innerhalb von [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen in binäre Ausdrücke umgewandelt wurden.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```   
expression | expression  
```  
  
## <a name="arguments"></a>Argumente  
 *expression*  
 Ein beliebiger gültiger [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) der Datentypkategorie „integer“ oder vom Datentyp **bit**, **binary** oder **varbinary**. *expression* wird in der bitweisen Operation als binäre Zahl behandelt.  
  
> [!NOTE]  
>  Nur eines der *expression*-Argumente kann in einer bitweisen Operation vom Datentyp **binary** oder **varbinary** sein.  
  
## <a name="result-types"></a>Ergebnistypen  
 Gibt Folgendes zurück: ein **int**, wenn die Eingabewerte auch **int** sind, ein **smallint**, wenn die Eingabewerte **smallint** sind, oder ein **tinyint**, wenn die Eingabewerte **tinyint** sind.  
  
## <a name="remarks"></a>Remarks  
 Mit dem bitweisen |-Operator wird zwischen zwei Ausdrücken ein bitweises logisches OR ausgeführt, indem die jeweils entsprechenden Bits der beiden Ausdrücke verarbeitet werden. Ein Ergebnisbit wird dann auf den Wert 1 festgelegt, wenn mindestens eines der Bits (für das aktuell aufzulösende Bit) der Eingabeausdrücke den Wert 1 aufweist. Falls keines der Bits in den Eingabeausdrücken den Wert 1 hat, wird das entsprechende Bit im Ergebnis auf 0 festgelegt.  
  
 Wenn der linke und der rechte Ausdruck unterschiedliche ganzzahlige Datentypen aufweisen (beispielsweise ist der linke *expression*-Ausdruck vom Datentyp **smallint** und der rechte *expression*-Ausdruck von Datentyp **int**), wird das Argument mit dem kleineren Datentyp in den größeren Datentyp konvertiert. In diesem Beispiel wird **smallint***expression* in einen **int** konvertiert.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird zum Anzeigen der ursprünglichen Werte eine Tabelle mit Werten vom **int**-Datentyp und gibt der Tabelle die Form einer einzelnen Zeile.  
  
```sql  
CREATE TABLE bitwise  
(   
 a_int_value int NOT NULL,  
b_int_value int NOT NULL  
);  
GO  
INSERT bitwise VALUES (170, 75);  
GO  
```  
  
 Die folgende Abfrage führt ein bitweises OR zwischen den Spalten **a_int_value** und **b_int_value** durch.  
  
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
  
 Die binäre Darstellung von 170 (**a_int_value**, unten mit `A` bezeichnet) ist `0000 0000 1010 1010`. Die binäre Darstellung von 75 (**b_int_value**, unten mit `B` bezeichnet) ist `0000 0000 0100 1011`. Die Anwendung einer bitweisen OR-Operation auf diese beiden Werte erzeugt das binäre Ergebnis `0000 0000 1110 1011`, was dem dezimalen Wert 235 entspricht.  
  
```  
(A | B)  
0000 0000 1010 1010  
0000 0000 0100 1011  
-------------------  
0000 0000 1110 1011  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Operatoren &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [Bitweise Operatoren &#40;Transact-SQL&#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)   
 [&#124;= &#40;Bitwise OR Assignment&#41; &#40;Transact-SQL&#41; (Zuweisung mit bitweisem OR (Transact-SQL))](../../t-sql/language-elements/bitwise-or-equals-transact-sql.md)   
 [Verbundoperatoren &#40;Transact-SQL&#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)  
  
  



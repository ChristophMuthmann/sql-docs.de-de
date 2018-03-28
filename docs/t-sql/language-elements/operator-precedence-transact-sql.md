---
title: Operatorrangfolge (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|language-elements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- operators [Transact-SQL], precedence
- operator precedence [Transact-SQL]
- order of operator execution [Transact-SQL]
- precedence [SQL Server], operators
ms.assetid: f04d2439-6fff-4e4c-801f-cc62faef510a
caps.latest.revision: ''
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 8ea8f70ba88d8a9632e94d452c09612173cac83a
ms.sourcegitcommit: 6b1618aa3b24bf6759b00a820e09c52c4996ca10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/15/2018
---
# <a name="operator-precedence-transact-sql"></a>Operatorrangfolge (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Besitzt ein komplexer Ausdruck mehrere Operatoren, bestimmt die Operatorenrangfolge die Reihenfolge, in der die einzelnen Operationen durchgeführt werden. Die Ausführungsreihenfolge kann sich entscheidend auf das Ergebnis auswirken.  
  
 Operatoren besitzen die in der folgenden Tabelle dargestellte Rangfolge. Ein Operator, der höher in der Rangfolge steht, wird vor einem Operator niedrigeren Ranges ausgewertet.  
  
|Ebene|Operatoren|  
|-----------|---------------|  
|1|~ (Bitweises NOT)|  
|2|* (Multiplikation) / (Division), % (Modulo)|  
|3|+ (Positiv), - (Negativ), + (Addition), + (Verkettung), - (Subtraktion), & (bitweises UND), ^ (bitweises exklusives ODER), &#124; (bitweises ODER)|  
|4|=, >, \<, >=, <=, <>, !=, !>, !< (Vergleichsoperatoren)|  
|5|NICHT|  
|6|AND|  
|7|ALL, ANY, BETWEEN, IN, LIKE, OR, SOME|  
|8|= (Zuweisung)|  
  
 Besitzen zwei Operatoren in einem Ausdruck die gleiche Ebene in der Rangfolge, werden sie von links nach rechts, ausgehend von ihrer Position innerhalb des Ausdrucks, ausgewertet. So wird in dem Ausdruck, der in der folgenden `SET`-Anweisung verwendet wird, der Subtraktionsoperator vor dem Additionsoperator ausgewertet.  
  
```  
DECLARE @MyNumber int;  
SET @MyNumber = 4 - 2 + 27;  
-- Evaluates to 2 + 27 which yields an expression result of 29.  
SELECT @MyNumber;  
```  
  
 Mit Klammern kann die definierte Rangfolge von Operatoren in einem Ausdruck überschrieben werden. Die Operatoren innerhalb der Klammern werden zuerst ausgewertet, bevor der sich ergebende einzelne Wert von den Operatoren außerhalb der Klammern verwendet wird.  
  
 In dem Ausdruck, der in der folgenden `SET`-Anweisung verwendet wird, besitzt der Multiplikationsoperator Vorrang vor dem Additionsoperator. Er wird daher zuerst ausgewertet; das Ergebnis des Ausdrucks lautet `13`.  
  
```  
DECLARE @MyNumber int;  
SET @MyNumber = 2 * 4 + 5;  
-- Evaluates to 8 + 5 which yields an expression result of 13.  
SELECT @MyNumber;  
```  
  
 In dem Ausdruck, der in der folgenden `SET`-Anweisung verwendet wird, bewirken die Klammern, dass die Addition zuerst durchgeführt wird. Das Ergebnis des Ausdrucks lautet `18`.  
  
```  
DECLARE @MyNumber int;  
SET @MyNumber = 2 * (4 + 5);  
-- Evaluates to 2 * 9 which yields an expression result of 18.  
SELECT @MyNumber;  
```  
  
 In einem Ausdruck mit geschachtelten Klammern wird der Ausdruck der höchsten Schachtelungstiefe zuerst ausgewertet. Das folgende Beispiel enthält geschachtelte Klammern, und der Ausdruck `5 - 3` ist der Ausdruck mit der höchsten Schachtelungstiefe. Dieser Ausdruck ergibt den Wert `2`. Danach wird mit dem Additionsoperator (`+`) dieses Ergebnis zu `4` addiert. Dies ergibt den Wert `6`. Schließlich wird `6` mit `2` multipliziert, sodass sich als Ergebnis des Ausdrucks `12` ergibt.  
  
```  
DECLARE @MyNumber int;  
SET @MyNumber = 2 * (4 + (5 - 3) );  
-- Evaluates to 2 * (4 + 2) which then evaluates to 2 * 6, and   
-- yields an expression result of 12.  
SELECT @MyNumber;  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Logische Operatoren &#40;Transact-SQL&#41;](../../t-sql/language-elements/logical-operators-transact-sql.md)   
 [Operatoren &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [Integrierte Funktionen &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)  
  
  

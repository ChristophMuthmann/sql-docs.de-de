---
title: COUNT_BIG (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- COUNT_BIG_TSQL
- COUNT_BIG
dev_langs: TSQL
helpviewer_keywords:
- totals [SQL Server], COUNT_BIG function
- counting items in group
- groups [SQL Server], number of items in
- number of group items
- COUNT_BIG function
ms.assetid: f2e3601f-487e-4917-bb01-47b1047908cd
caps.latest.revision: "44"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: ad2b7e5343547bb65c6d81de8c6586ef5209e52a
ms.sourcegitcommit: 0e305dce04dcd1aa83c39328397524b352c96386
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/22/2017
---
# <a name="countbig--sql"></a>COUNT_BIG (-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Gibt die Anzahl von Elementen in einer Gruppe zurück. COUNT_BIG funktioniert wie die COUNT-Funktion. Der einzige Unterschied zwischen den beiden Funktionen sind die Rückgabewerte. COUNT_BIG gibt immer eine **"bigint"** -Datentypwert. COUNT gibt immer zurück ein **Int** -Datentypwert.
  
![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
-- Syntax for SQL Server and Azure SQL Database  
  
COUNT_BIG ( { [ ALL | DISTINCT ] expression } | * )  
   [ OVER ( [ partition_by_clause ] [ order_by_clause ] ) ]  
```  
  
```sql
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  

-- Aggregation Function Syntax  
COUNT_BIG ( { [ [ ALL | DISTINCT ] expression ] | * } )  
  
-- Analytic Function Syntax  
COUNT_BIG ( { expression | * } ) OVER ( [ <partition_by_clause> ] )  
```  
  
## <a name="arguments"></a>Argumente  
ALL  
Wendet die Aggregatfunktion auf alle Werte an. ALL ist die Standardeinstellung.
  
DISTINCT  
Gibt an, dass COUNT_BIG die Anzahl von eindeutigen Werten, die ungleich NULL sind, zurückgibt.
  
*expression*  
Ist ein [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) eines beliebigen Typs. Aggregatfunktionen und Unterabfragen sind nicht zulässig.
  
*\**  
Gibt an, dass alle Zeilen gezählt werden müssen, um die Gesamtzahl der Zeilen einer Tabelle zurückzugeben. COUNT_BIG (*\**) besitzt keine Parameter und kann nicht zusammen mit DISTINCT verwendet werden. COUNT_BIG (*\**) erfordert kein *Ausdruck* Parameter, da definitionsgemäß keine Informationen zu einer bestimmten Spalte verwendet wird. COUNT_BIG (*\**) gibt die Anzahl der Zeilen in einer angegebenen Tabelle ohne Duplikate zu entfernen. Dabei werden alle Zeilen einzeln gezählt. Dies schließt Zeilen mit NULL-Werten ein.
  
ALL  
Wendet die Aggregatfunktion auf alle Werte an. ALL ist die Standardeinstellung.
  
DISTINCT  
Gibt an, dass AVG nur für jede eindeutige Instanz eines Werts ausgeführt werden soll, unabhängig davon, wie oft der Wert vorkommt.
  
*expression*  
Ist ein [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) der genauen numerischen oder ungefähren numerischen Datentypkategorie, mit Ausnahme der **Bit** -Datentyp. Aggregatfunktionen und Unterabfragen sind nicht zulässig.
  
ÜBER **(** [ *Partition_by_clause* ] [ *Order_by_clause* ] **)**  
*Partition_by_clause* teilt das Resultset, das von der FROM-Klausel erstellt wird, in Partitionen, die auf die die Funktion angewendet wird. Wird dies nicht angegeben, verarbeitet die Funktion alle Zeilen des Abfrageresultsets als einzelne Gruppe. *Order_by_clause* bestimmt die logische Reihenfolge, in dem der Vorgang ausgeführt wird. Weitere Informationen finden Sie unter [Klausel "OVER" &#40; Transact-SQL &#41; ](../../t-sql/queries/select-over-clause-transact-sql.md).
  
## <a name="return-types"></a>Rückgabetypen
**bigint**
  
## <a name="remarks"></a>Hinweise  
COUNT_BIG(*) gibt die Anzahl von Elementen in einer Gruppe zurück. Dies schließt NULL-Werte und Duplikate ein.
  
COUNT_BIG (alle *Ausdruck*) ergibt *Ausdruck* für jede Zeile in einer Gruppe und die Anzahl der Werte ungleich NULL zurückgegeben.
  
COUNT_BIG (DISTINCT *Ausdruck*) ergibt *Ausdruck* für jede Zeile in einer Gruppe und die Anzahl der eindeutigen Werte ungleich NULL zurückgegeben.
  
COUNT_BIG ist eine deterministische Funktion, wenn sie ohne die OVER- und ORDER BY-Klauseln angegeben wird. Sie ist nicht deterministisch, wenn sie mit den OVER- und ORDER BY-Klauseln angegeben wird. Weitere Informationen finden Sie unter [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).
  
## <a name="examples"></a>Beispiele  
Beispiele finden Sie unter [Anzahl &#40; Transact-SQL &#41; ](../../t-sql/functions/count-transact-sql.md).
  
## <a name="see-also"></a>Siehe auch
[Aggregatfunktionen &#40; Transact-SQL &#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)  
[Anzahl &#40; Transact-SQL &#41;](../../t-sql/functions/count-transact-sql.md)  
[Int, Bigint, Smallint und Tinyint &#40; Transact-SQL &#41;](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)  
[Failover-Klausel &#40; Transact-SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md)
  
  

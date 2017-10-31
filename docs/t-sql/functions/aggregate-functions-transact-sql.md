---
title: Aggregatfunktionen (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
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
- functions [SQL Server], aggregate
- aggregate functions [SQL Server], about aggregate functions
- summarizing functions
- aggregate functions [SQL Server]
ms.assetid: 0c06ae42-eb0a-4d77-9d74-aa1e7f344009
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5a97d68c641d2a3deb1d3fd3a674f65cafc3854c
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="aggregate-functions-transact-sql"></a>Aggregatfunktionen (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Aggregatfunktionen führen Berechnungen für eine Wertemenge durch und geben einen einzelnen Wert zurück. Alle Aggregatfunktionen, außer COUNT, ignorieren NULL-Werte. Aggregatfunktionen werden häufig mit der GROUP BY-Klausel der SELECT-Anweisung verwendet.
  
Alle Aggregatfunktionen sind deterministisch. Dies bedeutet, dass Aggregatfunktionen bei jedem Aufrufen mit bestimmten Eingabewerten immer das gleiche Ergebnis zurückgeben. Weitere Informationen zum Funktionsdeterminismus finden Sie unter [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md). Die [OVER-Klausel](../../t-sql/queries/select-over-clause-transact-sql.md) kann alle Aggregatfunktionen außer GROUPING und GROUPING_ID folgen.
  
Aggregatfunktionen können nur in folgenden Fällen als Ausdrücke verwendet werden:
-   In der Auswahlliste einer SELECT-Anweisung (Unterabfrage oder äußere Abfrage)  
-   In einer HAVING-Klausel  
  
[!INCLUDE[tsql](../../includes/tsql-md.md)] stellt die folgenden Aggregatfunktionen bereit:
  
|||  
|-|-|  
|[AVG](../../t-sql/functions/avg-transact-sql.md)|[MIN.](../../t-sql/functions/min-transact-sql.md)|  
|[CHECKSUM_AGG](../../t-sql/functions/checksum-agg-transact-sql.md)|[SUMME](../../t-sql/functions/sum-transact-sql.md)|  
|[ANZAHL](../../t-sql/functions/count-transact-sql.md)|[STDEV](../../t-sql/functions/stdev-transact-sql.md)|  
|[COUNT_BIG](../../t-sql/functions/count-big-transact-sql.md)|[STDEVP](../../t-sql/functions/stdevp-transact-sql.md)|  
|[GRUPPIEREN VON](../../t-sql/functions/grouping-transact-sql.md)|[VAR](../../t-sql/functions/var-transact-sql.md)|  
|[GROUPING_ID](../../t-sql/functions/grouping-id-transact-sql.md)|[VARP](../../t-sql/functions/varp-transact-sql.md)|  
|[MAX](../../t-sql/functions/max-transact-sql.md)||  
  
## <a name="see-also"></a>Siehe auch
[Integrierte Funktionen &#40;Transact-SQL&#41;](../../t-sql/functions/functions.md)  
[Failover-Klausel &#40; Transact-SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md)
  
  


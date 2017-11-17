---
title: Hinweise (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- query optimizer [SQL Server], hints
- hints [SQL Server], about hints
- SELECT statement [SQL Server], hints
- hints [SQL Server]
- INSERT statement [SQL Server], hints
- UPDATE statement [SQL Server], hints
- DELETE statement [SQL Server], hints
ms.assetid: 99412475-b0df-4264-9938-33a0b302b41a
caps.latest.revision: 27
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6d2d8b50a38299162677b1f7d5bbff501fba9881
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="hints-transact-sql"></a>Hinweise (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Hinweise sind Optionen oder Strategien, die angegeben werden, um bei Bedarf durch den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Abfrageoptimierer für SELECT-, INSERT-, UPDATE- oder DELETE-Anweisungen erzwungen werden zu können. Diese Hinweise überschreiben jeden Ausführungsplan, den der Abfrageoptimierer möglicherweise für eine Abfrage auswählt.  
  
> [!CAUTION]  
>  Da die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Abfrageoptimierer in der Regel den optimalen Ausführungsplan für eine Abfrage auswählt, wird empfohlen, die \<Join_hint >, \<Query_hint >, und \<Table_hint > nur als letzte Möglichkeit verwendet werden, die von erfahrenen Entwickler und Datenbankadministratoren.
  
 In diesem Abschnitt werden die folgenden Hinweise beschrieben:  
  
-   [Joinhinweise](../../t-sql/queries/hints-transact-sql-join.md)  
  
-   [Abfragehinweise](../../t-sql/queries/hints-transact-sql-query.md)  
  
-   [Tabellenhinweis](../../t-sql/queries/hints-transact-sql-table.md)  
  
  


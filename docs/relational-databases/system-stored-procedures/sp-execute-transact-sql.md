---
title: Sp_execute (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_cursor_execute
- sp_cursor_execute_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_execute
ms.assetid: 2009acd3-0d92-435a-a8fb-057e50dc7146
caps.latest.revision: "11"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 2b40bd51a730cf902068aa0ba8bc40411f002f3b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spexecute-transact-sql"></a>sp_execute (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Führt eine vorbereitete [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung mithilfe eines angegebenen Handles und optionalen Parameterwerts. Sp_execute wird aufgerufen, indem ID = 12 in einem tabular Data Stream (TDS)-Paket.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
sp_execute handle OUTPUT  
    [,bound_param  ]  [,...n ]  ]  
```  
  
## <a name="arguments"></a>Argumente  
 *Handle*  
 Ist die *behandeln* von Sp_prepare zurückgegebene Wert. *behandeln* ist ein erforderlicher Parameter, der erfordert **Int** Eingabewert.  
  
 *bound_param*  
 Gibt die Verwendung zusätzlicher Parameter an. *Bound_param* ist ein erforderlicher Parameter, der Eingabewerte eines beliebigen Datentyps, um zusätzliche Parameter für die Prozedur anzugeben.  
  
> [!NOTE]  
>  *Bound_param* übereinstimmen die Deklarationen von Sp_prepare*Params* Wert und kann in der Form  *@name = Value* oder *Wert*.  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Sp_prepare &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-prepare-transact-sql.md)  
  
  

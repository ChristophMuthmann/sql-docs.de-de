---
title: GOTO (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- GOTO
- GOTO_TSQL
dev_langs: TSQL
helpviewer_keywords:
- skipping statements
- Transact-SQL statements, skipping
- labels [SQL Server]
- statements [SQL Server], skipping
- GOTO statement
ms.assetid: 589b6f8e-dc80-416f-9e74-48bed5337f58
caps.latest.revision: "33"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 9dbabcc0fe5f9573554384549023ab8395b87762
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="goto-transact-sql"></a>GOTO (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Verändert den Kontrollfluss, sodass die Ausführung an einer Marke fortgesetzt wird. Die [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung oder -Anweisungen, die GOTO folgen, werden ausgelassen, und die Verarbeitung wird an der Marke fortgesetzt. Sie können GOTO-Anweisungen und Marken überall in einer Prozedur, in einem Batch oder einem Anweisungsblock verwenden. GOTO-Anweisungen können geschachtelt werden.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Define the label:   
label:   
Alter the execution:  
GOTO label   
```  
  
## <a name="arguments"></a>Argumente  
 *Bezeichnung*  
 Ist der Punkt, an dem die Ausführung beginnt, wenn GOTO auf diese Marke zielt. Bezeichnungen müssen den Regeln für [Bezeichner](../../relational-databases/databases/database-identifiers.md). Sie können Marken auch als Kommentarmethode verwenden, unabhängig davon, ob GOTO verwendet wird.  
  
## <a name="remarks"></a>Hinweise  
 GOTO kann innerhalb von bedingten Anweisungen zur Ablaufsteuerung, Anweisungsblöcken oder Prozeduren vorhanden sein, nicht aber an Marken außerhalb des Batches. Sie können mit GOTO zu einer Marke verzweigen, die vor oder nach GOTO definiert ist.  
  
## <a name="permissions"></a>Berechtigungen  
 GOTO-Berechtigungen erhalten standardmäßig alle gültigen Benutzer.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird gezeigt, wie Sie `GOTO` als Verzweigungsmechanismus verwenden können.  
  
```  
DECLARE @Counter int;  
SET @Counter = 1;  
WHILE @Counter < 10  
BEGIN   
    SELECT @Counter  
    SET @Counter = @Counter + 1  
    IF @Counter = 4 GOTO Branch_One --Jumps to the first branch.  
    IF @Counter = 5 GOTO Branch_Two  --This will never execute.  
END  
Branch_One:  
    SELECT 'Jumping To Branch One.'  
    GOTO Branch_Three; --This will prevent Branch_Two from executing.  
Branch_Two:  
    SELECT 'Jumping To Branch Two.'  
Branch_Three:  
    SELECT 'Jumping To Branch Three.';  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Control-of-Flow-Sprache &#40; Transact-SQL &#41;](~/t-sql/language-elements/control-of-flow.md)   
 [GESTARTET... END &#40; Transact-SQL &#41;](../../t-sql/language-elements/begin-end-transact-sql.md)   
 [BREAK &#40; Transact-SQL &#41;](../../t-sql/language-elements/break-transact-sql.md)   
 [WEITERHIN &#40; Transact-SQL &#41;](../../t-sql/language-elements/continue-transact-sql.md)   
 [IF... ELSE &#40; Transact-SQL &#41;](../../t-sql/language-elements/if-else-transact-sql.md)   
 [WAITFOR &#40; Transact-SQL &#41;](../../t-sql/language-elements/waitfor-transact-sql.md)   
 [WHILE &#40;Transact-SQL&#41;](../../t-sql/language-elements/while-transact-sql.md)  
  
  

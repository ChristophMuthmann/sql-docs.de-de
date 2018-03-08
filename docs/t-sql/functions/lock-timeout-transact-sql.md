---
title: '@@LOCK_TIMEOUT (Transact-SQL) | Microsoft Docs'
ms.custom: 
ms.date: 09/19/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@LOCK_TIMEOUT'
- '@@LOCK_TIMEOUT_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- timeout options [SQL Server], locks
- '@@LOCK_TIMEOUT function'
- current lock time-out setting
- locking [SQL Server], time-outs
ms.assetid: 6bf8bf97-60b8-40c1-b89d-8f5a00bcae2e
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 84b885d21e5d940e3c532eef43040ba29c2b45ea
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="x40x40locktimeout-transact-sql"></a>&#x40;&#x40;LOCK_TIMEOUT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt die aktuelle Einstellung für das Sperrtimeout für die aktuelle Sitzung in Millisekunden zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
@@LOCK_TIMEOUT  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 **integer**  
  
## <a name="remarks"></a>Hinweise  
 SET LOCK_TIMEOUT ermöglicht einer Anwendung das Festlegen der maximalen Zeit, die eine Anweisung auf eine blockierte Ressource wartet. Wenn eine Anweisung länger als die Einstellung für LOCK_TIMEOUT gewartet hat, wird die blockierte Anweisung automatisch abgebrochen und eine Fehlermeldung an die Anwendung zurückgegeben.  
  
 @@LOCK_TIMEOUT gibt einen Wert von-1 zurück, wenn SET LOCK_TIMEOUT noch nicht in der aktuellen Sitzung ausgeführt wurde.  
  
## <a name="examples"></a>Beispiele  
 In diesem Beispiel wird das Resultset dargestellt, wenn kein Wert für LOCK_TIMEOUT festgelegt wurde.  
  
```  
SELECT @@LOCK_TIMEOUT AS [Lock Timeout];  
GO  
```  
  
 Im Folgenden wird das Resultset aufgeführt:  
  
```  
Lock Timeout  
------------  
-1  
```  
  
 In diesem Beispiel wird LOCK_TIMEOUT auf 1800 Millisekunden und ruft dann@LOCK_TIMEOUT .  
  
```  
SET LOCK_TIMEOUT 1800;  
SELECT @@LOCK_TIMEOUT AS [Lock Timeout];  
GO  
```  
  
 Im Folgenden wird das Resultset aufgeführt:  
  
```  
Lock Timeout  
------------  
1800          
```  
  
## <a name="see-also"></a>Siehe auch  
 [Konfigurationsfunktionen (Transact-SQL)](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [SET LOCK_TIMEOUT &#40; Transact-SQL &#41;](../../t-sql/statements/set-lock-timeout-transact-sql.md)  
  
  

---
title: '@@LOCK_TIMEOUT (Transact-SQL) | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 09/19/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 4bcd7703d4e03a6b41320d3b539bb7cade1907b8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
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
  
## <a name="remarks"></a>Remarks  
 SET LOCK_TIMEOUT ermöglicht einer Anwendung das Festlegen der maximalen Zeit, die eine Anweisung auf eine blockierte Ressource wartet. Wenn eine Anweisung länger als die Einstellung für LOCK_TIMEOUT gewartet hat, wird die blockierte Anweisung automatisch abgebrochen und eine Fehlermeldung an die Anwendung zurückgegeben.  
  
 @@LOCK_TIMEOUT gibt den Wert –1 zurück, wenn SET LOCK_TIMEOUT noch nicht in der aktuellen Sitzung ausgeführt wurde.  
  
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
  
 In diesem Beispiel wird LOCK_TIMEOUT auf 1800 Millisekunden festgelegt und dann @@LOCK_TIMEOUT aufgerufen.  
  
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
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Konfigurationsfunktionen (Transact-SQL)](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [SET LOCK_TIMEOUT &#40;Transact-SQL&#41;](../../t-sql/statements/set-lock-timeout-transact-sql.md)  
  
  

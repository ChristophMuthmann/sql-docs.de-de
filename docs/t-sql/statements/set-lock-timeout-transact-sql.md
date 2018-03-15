---
title: SET LOCK_TIMEOUT (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 09/11/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- LOCK_TIMEOUT_TSQL
- SET_LOCK_TIMEOUT_TSQL
- SET LOCK_TIMEOUT
- LOCK_TIMEOUT
dev_langs:
- TSQL
helpviewer_keywords:
- timeout options [SQL Server], locks
- releasing locks
- LOCK_TIMEOUT option
- SET LOCK_TIMEOUT statement
- locking [SQL Server], time-outs
- wait time for lock releases [SQL Server]
ms.assetid: dd0c389e-956d-435e-bf71-e16624a0a215
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 0e19a9acd7378615433364ac1b30db31a1a84b3a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="set-locktimeout-transact-sql"></a>SET LOCK_TIMEOUT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt an, wie viele Millisekunden eine Anweisung auf die Aufhebung einer Sperre wartet.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
SET LOCK_TIMEOUT timeout_period  
```  
  
## <a name="arguments"></a>Argumente  
 *timeout_period*  
 Anzahl der Millisekunden, die vergehen, bevor [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen Sperrfehler zurückgibt. Der Wert -1 (Standardwert) gibt an, dass keine Wartezeit festgelegt ist (d. h., es wird ewig gewartet).  
  
 Wenn die Wartezeit auf eine Sperre den Timeoutwert überschreitet, wird ein Fehler zurückgegeben. Der Wert 0 gibt an, dass nicht gewartet und eine Meldung zurückgegeben wird, sobald eine Sperre auftritt.  
  
## <a name="remarks"></a>Remarks  
 Zu Beginn einer Verbindung besitzt diese Einstellung den Wert -1. Nach einer Änderung bleibt die neue Einstellung für die restliche Verbindungsdauer bestehen.  
  
 Die Einstellung von SET LOCK_TIMEOUT wird zur Ausführungszeit und nicht zur Analysezeit festgelegt.  
  
 Der READPAST-Sperrhinweis stellt eine Alternative zu dieser SET-Option dar.  
  
 CREATE DATABASE-, ALTER DATABASE- und DROP DATABASE-Anweisungen erkennen die SET LOCK_TIMEOUT-Einstellung nicht an.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **public** -Rolle.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-set-the-lock-timeout-to-1800-milliseconds"></a>A: Festlegen des Sperrtimeout auf 1800 Millisekunden  
 Im folgenden Beispiel wird der Sperrtimeout auf `1800` Millisekunden festgelegt.  
  
```sql  
SET LOCK_TIMEOUT 1800;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
### <a name="b-set-the-lock-timeout-to-wait-forever-for-a-lock-to-be-released"></a>B. Festlegen des Sperrtimeouts, sodass dieses für immer darauf wartet, dass eine Sperre aufgehoben wird.  
 Im folgenden Beispiel wird festgelegt, dass das Sperrtimeout für immer wartet und nie abläuft. Dabei handelt es sich um das Standardverhalten, das bereits zu Beginn jeder Verbindung festgelegt wird.  
  
```sql  
SET LOCK_TIMEOUT -1;  
```  
  
 Im folgenden Beispiel wird der Sperrtimeout auf `1800` Millisekunden festgelegt. In diesem Release analysiert [!INCLUDE[ssDW](../../includes/ssdw-md.md)] die Anweisung zwar erfolgreich, ignoriert dabei aber den Wert 1800 und verwendet weiterhin das Standardverhalten.  
  
```sql  
SET LOCK_TIMEOUT 1800;  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [@@LOCK_TIMEOUT &#40;Transact-SQL&#41;](../../t-sql/functions/lock-timeout-transact-sql.md)   
 [SET-Anweisungen &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  


---
title: SET LOCK_TIMEOUT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 09/11/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
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
caps.latest.revision: 26
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 754242a86367b07b98caa9f70f457b70d0840075
ms.openlocfilehash: 3de86c7f33afd6e708ad8e773470ec650e092d2c
ms.contentlocale: de-de
ms.lasthandoff: 09/12/2017

---
# <a name="set-locktimeout-transact-sql"></a>SET LOCK_TIMEOUT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt die Anzahl der Millisekunden, die eine Anweisung wartet, eine Sperre aufgehoben wird.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
SET LOCK_TIMEOUT timeout_period  
```  
  
## <a name="arguments"></a>Argumente  
 *timeout_period*  
 Ist die Anzahl der Millisekunden, die vergehen, bevor [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen Sperrfehler zurückgibt. Der Wert -1 (Standardwert) gibt an, dass keine Wartezeit festgelegt ist (d. h., es wird ewig gewartet).  
  
 Wenn die Wartezeit auf eine Sperre den Timeoutwert überschreitet, wird ein Fehler zurückgegeben. Der Wert 0 gibt, dass nicht gewartet und eine Meldung zurückgegeben, sobald eine Sperre auftritt.  
  
## <a name="remarks"></a>Hinweise  
 Zu Beginn einer Verbindung besitzt diese Einstellung den Wert -1. Nach einer Änderung bleibt die neue Einstellung für die restliche Verbindungsdauer bestehen.  
  
 Die Einstellung von SET LOCK_TIMEOUT wird zur Ausführungszeit und nicht zur Analysezeit festgelegt.  
  
 Der READPAST-Sperrhinweis stellt eine Alternative zu dieser SET-Option dar.  
  
 CREATE DATABASE-, ALTER DATABASE- und DROP DATABASE-Anweisungen erkennen die SET LOCK_TIMEOUT-Einstellung nicht an.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **public** -Rolle.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-set-the-lock-timeout-to-1800-milliseconds"></a>A: das Sperrtimeout auf 1800 Millisekunden festgelegt  
 Im folgenden Beispiel wird der Sperrtimeout auf `1800` Millisekunden festgelegt.  
  
```sql  
SET LOCK_TIMEOUT 1800;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-set-the-lock-timeout-to-wait-forever-for-a-lock-to-be-released"></a>B. Legen Sie das Sperrungstimeout ewig warten, bis eine Sperre aufgehoben wird.  
 Im folgenden Beispiel wird der Sperrtimeout ewig warten und laufen nie ab. Dies ist das Standardverhalten, das am Anfang jeder Verbindung bereits festgelegt ist.  
  
```sql  
SET LOCK_TIMEOUT -1;  
```  
  
 Im folgenden Beispiel wird der Sperrtimeout auf `1800` Millisekunden festgelegt. In dieser Version [!INCLUDE[ssDW](../../includes/ssdw-md.md)] analysieren Sie die Anweisung erfolgreich, aber werden ignoriert den Wert 1800 und weiterhin das Standardverhalten zu verwenden.  
  
```sql  
SET LOCK_TIMEOUT 1800;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [@@LOCK_TIMEOUT &#40;Transact-SQL&#41;](../../t-sql/functions/lock-timeout-transact-sql.md)   
 [SET-Anweisungen &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  



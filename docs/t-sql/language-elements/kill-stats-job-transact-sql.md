---
title: KILL STATS JOB (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/27/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- KILL STATS JOB
- KILL_STATS_JOB_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ending statistics update jobs [SQL Server]
- stopping statistics update jobs
- terminating statistics update jobs
- asynchronous statistics updates [SQL Server]
- KILL STATS JOB statement
- statistics update jobs [SQL Server]
ms.assetid: 55a8f9f1-3259-45c0-8ab9-60b9c088b4b4
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7f1738c96709d2eb1489c9ec25c598459842e3ab
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="kill-stats-job-transact-sql"></a>KILL STATS JOB (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Beendet einen asynchronen statistikupdateauftrag in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
KILL STATS JOB job_id   
```  
  
## <a name="arguments"></a>Argumente  
 *job_id*  
 Ist das job_id-Feld, das von der dynamischen Verwaltungssicht sys.dm_exec_background_job_queue für den Auftrag zurückgegeben wird.  
  
## <a name="remarks"></a>Hinweise  
 job_id hängt nicht mit session_id oder der in anderen Formen der KILL-Anweisung verwendeten Arbeitseinheit zusammen.  
  
## <a name="permissions"></a>Berechtigungen  
 Benutzer benötigen die VIEW SERVER STATE-Berechtigung, um auf Informationen in der dynamischen Verwaltungssicht sys.dm_exec_background_job_queue zuzugreifen.  
  
 KILL STATS JOB-Berechtigungen erhalten standardmäßig die Mitglieder der festen Datenbankrollen sysadmin und processadmin; sie sind nicht übertragbar.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel zeigt, wie das Update der Statistik mit einem Auftrag verknüpften beendet, in dem die *Job_id* = `53`.  
  
```  
KILL STATS JOB 53;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [KILL &#40; Transact-SQL &#41;](../../t-sql/language-elements/kill-transact-sql.md)   
 [KILL QUERY NOTIFICATION SUBSCRIPTION &#40; Transact-SQL &#41;](../../t-sql/language-elements/kill-query-notification-subscription-transact-sql.md)   
 [dm_exec_background_job_queue &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-background-job-queue-transact-sql.md)   
 [Statistik](../../relational-databases/statistics/statistics.md)  
  
  


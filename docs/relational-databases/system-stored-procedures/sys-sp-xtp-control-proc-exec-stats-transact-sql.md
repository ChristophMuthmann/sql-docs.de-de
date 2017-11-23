---
title: Sys. sp_xtp_control_proc_exec_stats (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.sp_xtp_control_proc_exec_stats
- sys.sp_xtp_control_proc_exec_stats_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.sp_xtp_control_proc_exec_stats
ms.assetid: f5119808-76a1-4522-8529-9e02ee39adcb
caps.latest.revision: "15"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 721c120c200bb3142b36e06beb6e45cab1ca0805
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysspxtpcontrolprocexecstats-transact-sql"></a>sys.sp_xtp_control_proc_exec_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  Aktiviert die Statistiksammlung für systemintern kompilierte gespeicherte Prozeduren für die Instanz.  
  
 Zum Aktivieren der Statistiksammlung auf der abfragenebene für systemintern kompilierte gespeicherte Prozeduren finden Sie unter [Sys. sp_xtp_control_query_exec_stats &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql.md).  
  
## <a name="syntax"></a>Syntax  
  
```  
sp_xtp_control_proc_exec_stats [ [ @new_collection_value = ] collection_value ], [ @old_collection_value]  
```  
  
## <a name="arguments"></a>Argumente  
 @new_collection_value= *Wert*  
 Bestimmt, ob die Statistiksammlung auf Prozedurebene aktiviert (1) oder deaktiviert (0) ist.  
  
 @new_collection_valuewird auf 0 (null) festgelegt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oder die Datenbank gestartet wird.  
  
 @old_collection_value= *Wert*  
 Gibt den aktuellen Status zurück.  
  
## <a name="return-code"></a>Rückgabecode  
 0 für Erfolg. Ungleich 0 für Fehler.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der festen sysadmin-Rolle.  
  
## <a name="code-samples"></a>Codebeispiele  
 Festzulegende @new_collection_value und Fragen den Wert von@new_collection_value:  
  
```  
exec [sys].[sp_xtp_control_proc_exec_stats] @new_collection_value = 1  
declare @c bit  
exec sp_xtp_control_proc_exec_stats @old_collection_value=@c output  
select @c as 'collection status'  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [In-Memory-OLTP &#40;Arbeitsspeicheroptimierung&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  

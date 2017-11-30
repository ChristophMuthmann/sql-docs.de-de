---
title: Sys. sp_xtp_control_query_exec_stats (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 10/13/2015
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
- sys.sp_xtp_control_query_exec_stats_TSQL
- sys.sp_xtp_control_query_exec_stats
dev_langs: TSQL
helpviewer_keywords: sys.sp_xtp_control_query_exec_stats
ms.assetid: 4838125d-ad1e-479e-b7d2-42655e8f4f02
caps.latest.revision: "16"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f4bcc1bb453783a38c4b23e6526de1a804bde8f1
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="sysspxtpcontrolqueryexecstats-transact-sql"></a>sys.sp_xtp_control_query_exec_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  Aktiviert die Statistiksammlung pro Abfrage für alle systemintern kompilierten gespeicherten Prozeduren der Instanz oder für bestimmte systemintern kompilierte gespeicherte Prozeduren.  
  
 Die Leistung nimmt ab, wenn Sie die Statistiksammlung aktivieren. Wenn Sie eine Problembehandlung nur für eine bzw. einige wenige systemintern kompilierte gespeicherte Prozeduren durchführen möchten, können Sie die Statistiksammlung nur für diese bestimmten systemintern kompilierten gespeicherten Prozeduren aktivieren.  
  
 Zum Aktivieren der Statistiksammlung auf Prozedurebene für alle systemintern kompilierten gespeicherten Prozeduren finden Sie unter [sp_xtp_control_proc_exec_stats &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-proc-exec-stats-transact-sql.md).  
  
## <a name="syntax"></a>Syntax  
  
```  
sp_xtp_control_query_exec_stats [ [ @new_collection_value = ] collection_value ],  
[ [ @database_id = ] database_id   
[ , [ @xtp_object_id = ] procedure_id ] ,   
[ @old_collection_value] ]  
```  
  
## <a name="arguments"></a>Argumente  
 @new_collection_value= *Wert*  
 Bestimmt, ob die Statistiksammlung auf Prozedurebene aktiviert (1) oder deaktiviert (0) ist.  
  
 @new_collection_valuewird auf 0 (null) festgelegt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gestartet wird.  
  
 @database_id== *Database_id*, @xtp_object_id = *Procedure_id*  
 Die Datenbank-ID und Objekt-ID der systemintern kompilierten gespeicherten Prozedur. Wenn die Statistiksammlung für die Instanz aktiviert ist ([sp_xtp_control_proc_exec_stats &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-proc-exec-stats-transact-sql.md)), werden Statistiken für eine systemintern kompilierte gespeicherte Prozedur gesammelt. Wenn Sie die Statistiksammlung auf der Instanz deaktivieren, wird die Statistiksammlung für die einzelnen systemintern kompilierten gespeicherten Prozeduren nicht deaktiviert.  
  
 Verwendung [sys.databases &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md), [sys.procedures &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-procedures-transact-sql.md), [DB_ID &#40; Transact-SQL &#41; ](../../t-sql/functions/db-id-transact-sql.md), oder [OBJECT_ID &#40; Transact-SQL &#41; ](../../t-sql/functions/object-id-transact-sql.md) um IDs für eine Datenbank und die gespeicherte Prozedur abzurufen.  
  
 @old_collection_value= *Wert*  
 Gibt den aktuellen Status zurück.  
  
## <a name="return-code"></a>Rückgabecode  
 0 für Erfolg. Ungleich 0 für Fehler.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der festen sysadmin-Rolle.  
  
## <a name="code-sample"></a>Codebeispiel  
 Im folgenden Codebeispiel wird gezeigt, wie die Statistiksammlung für alle systemintern kompilierten gespeicherten Prozeduren für die Instanz und dann für eine bestimmte systemintern kompilierte gespeicherte Prozedur aktiviert wird.  
  
```tsql   
DECLARE @c bit  
  
EXEC [sys].[sp_xtp_control_query_exec_stats] @new_collection_value = 1;  
  
EXEC sp_xtp_control_query_exec_stats @old_collection_value=@c output;  
SELECT @c AS 'collection status';  
  
EXEC [sys].[sp_xtp_control_query_exec_stats] @new_collection_value = 1,   
@database_id = 5, @xtp_object_id = 341576255;  
  
EXEC sp_xtp_control_query_exec_stats @database_id = 5,   
@xtp_object_id = 341576255, @old_collection_value=@c output;  
  
SELECT @c AS 'collection status';  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [In-Memory-OLTP &#40;Arbeitsspeicheroptimierung&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  

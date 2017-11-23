---
title: Sys.dm_exec_compute_node_errors (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SYS.DM_EXEC_COMPUTE_NODE_ERRORS_TSQL
- DM_EXEC_COMPUTE_NODE_ERRORS
- DM_EXEC_COMPUTE_NODE_ERRORS_TSQL
dev_langs: TSQL
helpviewer_keywords:
- PolyBase
- PolyBase, views
- dm_exec_compute_node_errors
- sys.dm_exec_compute_node_errors management view
ms.assetid: 9a03c039-70e4-4974-95d8-d3fa45984ffb
caps.latest.revision: "8"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 15d64d6e93258fca7245df90c429321b8ed45675
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmexeccomputenodeerrors-transact-sql"></a>Sys.dm_exec_compute_node_errors (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Gibt für PolyBase auftretenden Serverknoten an.  
  
|Spaltenname|Datentyp|Description|Bereich|  
|-----------------|---------------|-----------------|-----------|  
|error_id|**nvarchar(36)**|Eindeutige numerische Id des Fehlers.|Eindeutig für alle Abfragefehlern im system|  
|Quelle|**nvarchar(255)**|Datenquellenbeschreibung Prozess oder thread||  
|Typ|**nvarchar(255)**|Fehlertyp.||  
|create_time|**datetime**|Die Uhrzeit des Auftretens Fehler||  
|compute_node_id|**int**|Bezeichner des bestimmten Serverknoten|Finden Sie unter der Compute_node_id [dm_exec_compute_nodes &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md)|  
|rexecution_id|**nvarchar(36)**|Der Bezeichner der PolyBase-Abfrage, sofern vorhanden.||  
|spid|**int**|ID der SQL Server-Sitzung||  
|thread_id|**int**|Numerischer Bezeichner des Threads, die auf dem der Fehler aufgetreten ist.||  
|Details|nvarchar(4000)|Vollständige Beschreibung der Details des Fehlers.||  
  
## <a name="see-also"></a>Siehe auch  
 [PolyBase, Problembehandlung mit dynamischen Verwaltungssichten](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Datenbank verbundene dynamische Verwaltungssichten &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  

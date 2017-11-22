---
title: Sys.dm_exec_external_operations (Transact-SQL) | Microsoft Docs
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
- DM_EXEC_EXTERNAL_OPERATIONS_TSQL
- DM_EXEC_EXTERNAL_OPERATIONS
- SYS.DM_EXEC_EXTERNAL_OPERATIONS_TSQL
dev_langs: TSQL
helpviewer_keywords:
- PolyBase,views
- PolyBase
- sys.dm_exec_external_operations management view
- dm_exec_external_operations management view
ms.assetid: d268217a-85b8-4b7f-9cd1-87865eba2be1
caps.latest.revision: "8"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 90f2793ddb2c2059e2b279b53f7261d3b583e469
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmexecexternaloperations-transact-sql"></a>Sys.dm_exec_external_operations (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Erfasst Informationen zu externen PolyBase-Vorgänge.  
  
|Spaltenname|Datentyp|Description|Bereich|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|**nvarchar(32)**|Eindeutige abfragebezeichners PolyBase Abfrage zugeordnet|Finden Sie unter-ID in [Sys. dm_exec_requests &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)|  
|step_index|**int**|Der Index des Abfrage-Schritts|Finden Sie unter Step_index in [sys.dm_exec_distributed_request_steps &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-request-steps-transact-sql.md)|  
|Operation_-Typ|**vom Datentyp nvarchar(128)**|Beschreibt einen Hadoop-Vorgang oder einen anderen externen Vorgang|"Externe Hadoop Operation"|  
|Operation_ name|**nvarchar(4000)**|Gibt an, wie der Status des Auftrags in Prozent (wie viel die Eingabe verwendet wird)|0-1 – multipliziert, um den Faktor 100 (abgeschlossen)|  
|Map_-Status|**float**|Zeigt an wie der Status der reduzieren Sie einen Auftrag in Prozent, falls vorhanden|0-1 – multipliziert, um den Faktor 100 (abgeschlossen)|  
  
## <a name="see-also"></a>Siehe auch  
 [PolyBase, Problembehandlung mit dynamischen Verwaltungssichten](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Datenbank verbundene dynamische Verwaltungssichten &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  

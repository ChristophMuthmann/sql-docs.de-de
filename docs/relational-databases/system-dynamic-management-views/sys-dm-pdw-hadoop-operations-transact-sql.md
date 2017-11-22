---
title: Sys.dm_pdw_hadoop_operations (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: 5d2337d4-e2c7-48de-9c26-cdc7e6eb5d55
caps.latest.revision: "5"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9b735d4759d3164ae61da717ec18d54ab8661441
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmpdwhadoopoperations-transact-sql"></a>Sys.dm_pdw_hadoop_operations (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Enthält eine Zeile für jedes map-reduce-Auftrags, der im Rahmen der Ausführung an Hadoop weitergegeben wird eine [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] -Abfrage auf eine externe Hadoop-Tabelle. Jeder map-reduce-Auftrag stellt eine von den Prädikaten in der Abfrage dar. Dies wird nur verwendet, wenn die prädikatweitergabe für Abfragen in externen Tabellen für Hadoop aktiviert ist.  
  
|Spaltenname|Datentyp|Description|Bereich|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|Die ID für diesen externen Hadoop-Vorgang.|Identisch mit der ID in [sys.dm_pdw_exec_requests &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|step_index|**int**|Der Index des Schritts Abfrage, die auf diesen Hadoop-Vorgang verweist.|Identisch mit Step_index in [sys.dm_pdw_request_steps &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|operation_type|**nvarchar(255)**|Beschreibt den Typ des externen Vorgang.|"Externe Hadoop Operation"|  
|operation_name|**nvarchar(4000)**|Die Auftrags-ID für einen map-reduce-Auftrag. Rückgabewert von Hadoop nach [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] übermitteln des Auftrags.||  
|map_progress|**float**|Der Prozentsatz der Eingabedaten, die bisher durch die Zuordnung-Auftrag verbraucht wurde.|Eine Gleitkommazahl zwischen und einschließlich 0 und 100.|  
|reduce_progress|**int**|Der Anteil der Reduce-Auftrag abgeschlossen ist...|Eine Gleitkommazahl zwischen und einschließlich 0 und 100.|  
  
## <a name="see-also"></a>Siehe auch  
 [Systemsichten &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)  
  
  

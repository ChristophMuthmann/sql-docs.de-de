---
title: Sys.dm_pdw_hadoop_operations (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 5d2337d4-e2c7-48de-9c26-cdc7e6eb5d55
caps.latest.revision: 5
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 7c7da3f36c73a2b724c3b6709983d5c3ae611ce4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmpdwhadoopoperations-transact-sql"></a>Sys.dm_pdw_hadoop_operations (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Enthält eine Zeile für jedes map-reduce-Auftrags, der im Rahmen der Ausführung an Hadoop weitergegeben wird eine [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] -Abfrage auf eine externe Hadoop-Tabelle. Jeder map-reduce-Auftrag stellt eine von den Prädikaten in der Abfrage dar. Dies wird nur verwendet, wenn die prädikatweitergabe für Abfragen in externen Tabellen für Hadoop aktiviert ist.  
  
|Spaltenname|Datentyp|Description|Bereich|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|Die ID für diesen externen Hadoop-Vorgang.|Identisch mit der ID in [sys.dm_pdw_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|step_index|**int**|Der Index des Schritts Abfrage, die auf diesen Hadoop-Vorgang verweist.|Identisch mit Step_index in [sys.dm_pdw_request_steps &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|operation_type|**nvarchar(255)**|Beschreibt den Typ des externen Vorgang.|"Externe Hadoop Operation"|  
|operation_name|**nvarchar(4000)**|Die Auftrags-ID für einen map-reduce-Auftrag. Rückgabewert von Hadoop nach [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] übermitteln des Auftrags.||  
|map_progress|**float**|Der Prozentsatz der Eingabedaten, die bisher durch die Zuordnung-Auftrag verbraucht wurde.|Eine Gleitkommazahl zwischen und einschließlich 0 und 100.|  
|reduce_progress|**int**|Der Anteil der Reduce-Auftrag abgeschlossen ist...|Eine Gleitkommazahl zwischen und einschließlich 0 und 100.|  
  
## <a name="see-also"></a>Siehe auch  
 [Systemsichten &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)  
  
  

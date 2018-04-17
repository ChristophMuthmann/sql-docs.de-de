---
title: Sys.dm_exec_external_work (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DM_EXEC_EXTERNAL_WORK
- DM_EXEC_EXTERNAL_WORK_TSQL
- SYS.DM_EXEC_EXTERNAL_WORK_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_external_work management view
- dm_exec_external_work management view
- PolyBase,views
- PolyBase
ms.assetid: 7597d97b-1fde-4135-ac35-4af12968f300
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: cc5c37ce63dda93ca251856648150b22aa9bea97
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmexecexternalwork-transact-sql"></a>Sys.dm_exec_external_work (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Informationen über die Arbeitslast pro-Worker auf jedem Computeknoten zurückgegeben.  
  
 Fragen Sie sys.dm_exec_external_work, um die Arbeit erstellt, für die Kommunikation mit der externen Datenquelle (z. B. Hadoop oder externe SQL Server) zu identifizieren.  
  
|Spaltenname|Datentyp|Description|Bereich|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|**nvarchar(32)**|Eindeutiger Bezeichner für die PolyBase-Abfrage zugeordnet.|Finden Sie unter *Request_ID* in [Sys. dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md).|  
|step_index|**int**|Dieser Worker die Anforderung ausführt.|Finden Sie unter *Step_index* in [Sys. dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md).|  
|dms_step_index|**int**|Der Schritt in der DMS-Plan, den dieser Arbeitsthread ausgeführt wird.|Finden Sie unter [sys.dm_exec_dms_workers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-workers-transact-sql.md).|  
|compute_node_id|**int**|Der Knoten der Arbeitsthread ausgeführt wird.|Finden Sie unter [sys.dm_exec_compute_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md).|  
|Typ|**nvarchar(60)**|Der Typ des externen Ressourcen.|'Datei teilen'|  
|work_id|**int**|Die ID der tatsächlichen Aufteilung.|Größer als oder gleich 0.|  
|input_name|**nvarchar(4000)**|Name der Eingabe gelesen werden|Name der Datei bei Verwendung von Hadoop.|  
|read_location|**bigint**|Offset oder Speicherort lesen.|Offset der die zu lesende Datei.|  
|bytes_processed|**bigint**|Gesamtzahl der Bytes von diesem Arbeitsthread verarbeitet werden.|Größer als oder gleich 0.|  
|length|**bigint**|Länge der Teilung oder HDFS-Block bei Hadoop|Benutzerdefinierbare. Der Standardwert ist 64M|  
|status|**nvarchar(32)**|Status des Arbeitsthreads|Wartet auf und Verarbeiten von Arbeit, Fehler, abgebrochen|  
|start_time|**datetime**|Beginn der Arbeit||  
|end_time|**datetime**|Ende der Arbeit||  
|total_elapsed_time|**int**|Gesamtzeit in Millisekunden||  
  
## <a name="see-also"></a>Siehe auch  
 [PolyBase, Problembehandlung mit dynamischen Verwaltungssichten](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Datenbank verbundene dynamische Verwaltungssichten &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  

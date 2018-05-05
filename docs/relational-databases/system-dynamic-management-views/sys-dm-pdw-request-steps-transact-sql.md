---
title: Sys.dm_pdw_request_steps (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/01/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.service: sql-data-warehouse
ms.component: dmv's
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: cc563e88-0d34-436e-b914-b60d6ee0d50b
caps.latest.revision: 10
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: a6aa4428090cdb9965de19116fbbd0a9d493a73d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmpdwrequeststeps-transact-sql"></a>sys.dm_pdw_request_steps (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Enthält Informationen über alle Schritte, die eine bestimmte Anforderung erstellen oder Abfragen [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]. Eine Zeile pro abfrageschritt aufgeführt.  
  
|Spaltenname|Datentyp|Description|Bereich|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|Request_id und Step_index bilden zusammen den Schlüssel für diese Ansicht.<br /><br /> Eindeutige numerische Id der Anforderung zugeordnet ist.|Finden Sie unter Request_id in [sys.dm_pdw_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|step_index|**int**|Request_id und Step_index bilden zusammen den Schlüssel für diese Ansicht.<br /><br /> Die Position dieses Schritts in der Abfolge von Schritten, die die Anforderung bilden.|0 bis (n-1) für eine Anforderung mit n Schritten.|  
|operation_type|**nvarchar(35)**|Der Typ des Vorgangs, die durch diesen Schritt dargestellt.|**DMS-Plan Abfrageoperationen:** "ReturnOperation" "PartitionMoveOperation" "MoveOperation" "BroadcastMoveOperation" "ShuffleMoveOperation" "TrimMoveOperation" "CopyOperation", "DistributeReplicatedTableMoveOperation"<br /><br /> **SQL-Abfrage-Plan-Vorgänge:** "OnOperation", "RemoteOperation"<br /><br /> **Andere Plan Abfrageoperationen:** "MetaDataCreateOperation", "RandomIDOperation"<br /><br /> **Externe Vorgänge für Lesevorgänge:** "HadoopShuffleOperation", "HadoopRoundRobinOperation", "HadoopBroadcastOperation"<br /><br /> **Externe Vorgänge für MapReduce:** "HadoopJobOperation", "HdfsDeleteOperation"<br /><br /> **Externe Vorgänge für Schreibvorgänge:** "ExternalExportDistributedOperation", "ExternalExportReplicatedOperation", "ExternalExportControlOperation"<br /><br /> Weitere Informationen finden Sie unter "Grundlegendes zu Abfragepläne" in der [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].|  
|distribution_type|**nvarchar(32)**|Die Art der Verteilung, die diesen Schritt unterzogen wird.|"AllNodes", "AllDistributions", "AllComputeNodes", 'ComputeNode', 'Distribution', 'SubsetNodes', 'SubsetDistributions","Nicht angegeben"|  
|location_type|**nvarchar(32)**|Gibt an, in dem der Schritt ausgeführt wird.|"Compute", "Control", "DMS"|  
|status|**nvarchar(32)**|Der Status dieses Schritts.|Ausstehend "," ausgeführt wird, abgeschlossen, fehlgeschlagen, UndoFailed, PendingCancel abgebrochen, rückgängig gemacht, abgebrochen|  
|error_id|**nvarchar(36)**|Eindeutige Id des Fehlers bei diesem Schritt verknüpft sind, sofern vorhanden.|Finden Sie unter Fehler-ID des [sys.dm_pdw_errors &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md). NULL, wenn kein Fehler aufgetreten ist.|  
|start_time|**datetime**|Zeitpunkt, zu dem der Schritt Ausführung begonnen hat.|Kleiner oder gleich der aktuellen Uhrzeit und größer oder gleich End_compile_time der Abfrage zu der dieser Schritt gehört. Weitere Informationen zu Abfragen finden Sie unter [sys.dm_pdw_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|end_time|**datetime**|Zeitpunkt, zu dem dieser Schritt hat die Ausführung abgeschlossen, wurde abgebrochen oder fehlerhaft.|Kleiner oder gleich der aktuellen Uhrzeit und größer oder gleich Start_time. Schritte bei der Ausführung auf NULL festgelegt oder in die Warteschlange eingereiht.|  
|total_elapsed_time|**int**|Gesamtdauer der abfrageschritt, in Millisekunden ausgeführt wurde.|Zwischen 0 und der Unterschied zwischen End_time und Start_time. 0 für Schritte in Warteschlange.<br /><br /> Wenn Total_elapsed_time den maximalen Wert für eine ganze Zahl überschreitet, weiterhin Total_elapsed_time der maximale Wert sein. Diese Bedingung generiert die Warnung "der maximale Wert überschritten wurde."<br /><br /> Der maximale Wert in Millisekunden entspricht 24.8 Tage.|  
|row_count|**bigint**|Gesamtanzahl der Zeilen geändert oder von dieser Anforderung zurückgegeben.|0 für Schritte, die nicht ändern oder Daten zurückgeben. Andernfalls, Anzahl der betroffenen Zeilen.|  
|Befehl|**nvarchar(4000)**|Enthält den vollständigen Text des Befehls dieses Schritts an.|Eine beliebige gültige Anforderungszeichenfolge für einen Schritt. NULL, wenn der Vorgang des Typs MetaDataCreateOperation ist. Bei mehr als 4000 Zeichen abgeschnitten.|  
  
 Informationen über die maximale Zeilenanzahl, die von dieser Ansicht beibehalten werden, finden Sie im Abschnitt "maximale Systemwerte anzeigen" in die "minimale und Maximalwerte" in der [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Datawarehouse und Parallel Data Warehouse-dynamische Verwaltungssichten &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  

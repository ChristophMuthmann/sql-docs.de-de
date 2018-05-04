---
title: Sys.dm_pdw_dms_workers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
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
ms.assetid: 0a284d18-3c46-4ffa-bcc9-689e660ee8b4
caps.latest.revision: 7
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: ad9e41d1092f17d2fb5c37b7f16d2f6be056506b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmpdwdmsworkers-transact-sql"></a>Sys.dm_pdw_dms_workers (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Enthält Informationen zu allen Workern DMS-Schritte.  
  
|Spaltenname|Datentyp|Description|Bereich|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|Abfrage, die dieser Arbeitsthread DMS gehört.<br /><br /> Request_id Step_index und Dms_step_index bilden den Schlüssel für diese Ansicht ein.|Finden Sie unter Request_id in [sys.dm_pdw_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|step_index|**int**|Fragen Sie Schritt, mit dem dieser Arbeitsthread DMS gehört.<br /><br /> Request_id Step_index und Dms_step_index bilden den Schlüssel für diese Ansicht ein.|Finden Sie unter Step_index in [sys.dm_pdw_request_steps &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|dms_step_index|**int**|Der Schritt in der DMS-Plan, den dieser Arbeitsthread ausgeführt wird.<br /><br /> Request_id Step_index und Dms_step_index bilden den Schlüssel für diese Ansicht ein.||  
|pdw_node_id|**int**|Knoten, der der Arbeitsthread ausgeführt wird.|Finden Sie unter "node_id" in [sys.dm_pdw_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md).|  
|distribution_id|**Int**|Verteilung, die der Arbeitsthread ggf. ausgeführt wird.|Finden Sie unter Distribution_id in [sys.pdw_distributions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-distributions-transact-sql.md).|  
|Typ|**nvarchar(32)**|Typ des DMS-Arbeitsthread, diesen Eintrag darstellt.|"DIRECT_CONVERTER", "DIRECT_READER", "FILE_READER", "HASH_CONVERTER", "HASH_READER", "ROUNDROBIN_CONVERTER", "EXPORT_READER", "EXTERNAL_READER", "EXTERNAL_WRITER", "PARALLEL_COPY_READER", "REJECT_WRITER", "WRITER"|  
|status|**nvarchar(32)**|Status des DMS-Arbeitsthreads.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|bytes_per_sec|**bigint**|Durchsatz von Lese- oder Schreibvorgang in der letzten Sekunde.|Größer als oder gleich 0. NULL, wenn die Abfrage wurde abgebrochen oder Fehler, bevor der Arbeitsthread ausgeführt werden konnte.|  
|bytes_processed|**bigint**|Gesamtzahl der Bytes von diesem Arbeitsthread verarbeitet werden.|Größer als oder gleich 0. NULL, wenn die Abfrage wurde abgebrochen oder Fehler, bevor der Arbeitsthread ausgeführt werden konnte.|  
|rows_processed|**bigint**|Anzahl der Zeilen gelesen bzw. geschrieben werden für diesen Arbeitsthread.|Größer als oder gleich 0. NULL, wenn die Abfrage wurde abgebrochen oder Fehler, bevor der Arbeitsthread ausgeführt werden konnte.|  
|start_time|**datetime**|Zeitpunkt, zu dem Ausführung dieses Arbeitsthreads begonnen hat.|Größer als oder gleich der Startzeit des Schritts Abfrage wird dieser Arbeitsthread angehört. Finden Sie unter [sys.dm_pdw_request_steps &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|end_time|**datetime**|Uhrzeit der Ausführung beendet wurde, ist fehlgeschlagen, oder wurde abgebrochen.|NULL für laufende oder in der Warteschlange Worker. Andernfalls, Start_time größer.|  
|total_elapsed_time|**int**|Gesamtzeit für die Ausführung in Millisekunden.|Größer als oder gleich 0.<br /><br /> Insgesamt verstrichene Zeit seit System gestartet oder neu gestartet. Wenn Total_elapsed_time den maximalen Wert für eine ganze Zahl (24.8 Tage in Millisekunden) überschreitet, führt es Materialisierung Fehler aufgrund einer dazu, dass "Überlauf".<br /><br /> Der maximale Wert in Millisekunden entspricht 24.8 Tage.|  
|cpu_time|**bigint**|CPU-Zeit verbraucht, die von diesem Arbeitsthread, in Millisekunden.|Größer als oder gleich 0.|  
|query_time|**int**|Zeitspanne vor SQL startet wiederkehrender Zeilen für den Thread, in Millisekunden.|Größer als oder gleich 0.|  
|buffers_available|**int**|Anzahl der nicht verwendeten Puffer.| NULL, wenn die Abfrage wurde abgebrochen oder Fehler, bevor der Arbeitsthread ausgeführt werden konnte.|  
|sql_spid|**int**|Sitzungs-Id für die SQL Server-Instanz, die der Arbeiten für diesen Arbeitsthread DMS ausführen.||  
|dms_cpid|**int**|Prozess-ID des aktuellen Threads ausgeführt.||  
|error_id|**nvarchar(36)**|Eindeutiger Bezeichner des aufgetretenen Fehlers während der Ausführung dieses Arbeitsthreads, sofern vorhanden.|Finden Sie unter Fehler-ID in [sys.dm_pdw_request_steps &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|source_info|**nvarchar(4000)**|Für einen Reader, die Spezifikation der Datenquelltabellen und Spalten.||  
|destination_info|**nvarchar(4000)**|Für einen Writer Spezifikation der Zieltabellen.||  
  
 Informationen über die maximale Zeilenanzahl, die von dieser Ansicht beibehalten werden, finden Sie unter [maximale Systemwerte Ansicht](http://msdn.microsoft.com/en-us/5243f018-2713-45e3-9b61-39b2a57401b9).  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Datawarehouse und Parallel Data Warehouse-dynamische Verwaltungssichten &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  

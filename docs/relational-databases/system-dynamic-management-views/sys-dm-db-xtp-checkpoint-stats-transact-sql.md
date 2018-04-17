---
title: dm_db_xtp_checkpoint_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_db_xtp_checkpoint_stats
- dm_db_xtp_checkpoint_stats_TSQL
- sys.dm_db_xtp_checkpoint_stats
- sys.dm_db_xtp_checkpoint_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_checkpoint_stats dynamic management view
ms.assetid: 8d0b18ca-db4d-4376-9905-3e4457727c46
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 3fe44cb92654807147c96cd4becc1a3489ae3081
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmdbxtpcheckpointstats-transact-sql"></a>sys.dm_db_xtp_checkpoint_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  Gibt Statistiken zu den In-Memory OLTP-Prüfpunktvorgängen in der aktuellen Datenbank zurück. Wenn für die Datenbank keine In-Memory OLTP-Objekte vorhanden sind, wird ein leeres Resultset zurückgegeben.  
  
 Weitere Informationen finden Sie unter [In-Memory OLTP &#40;Arbeitsspeicheroptimierung&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
```  
SELECT * FROM db.sys.dm_db_xtp_checkpoint_stats;  
```  
  
**[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] unterscheidet sich deutlich von neueren Versionen und wird unten im Thema zur erläutert [SQL Server 2014](#bkmk_2014).**
  
## <a name="includesssql15includessssql15-mdmd-and-later"></a>[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] und höher  
 Die folgende Tabelle beschreibt die Spalten in `sys.dm_db_xtp_checkpoint_stats`ab **[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]**.  
  
|Spaltenname|Typ|Description|  
|-----------------|----------|-----------------|  
|last_lsn_processed|**bigint**|Letzte LSN, die vom Controller angezeigt werden.|  
|end_of_log_lsn|**numeric(38)**|Die LSN der das Ende des Protokolls.|  
|bytes_to_end_of_log|**bigint**|Protokollbytes, die nicht verarbeitet, durch den Controller, auf die Bytes zwischen entsprechenden `last_lsn_processed` und `end_of_log_lsn`.|  
|log_consumption_rate|**bigint**|Rate der Transaktion Protokoll Auslastung durch den Controller (in KB/s).|  
|active_scan_time_in_ms|**bigint**|Von der Controller aktiv Scannen des Transaktionsprotokolls benötigte Zeit.|  
|total_wait_time_in_ms|**bigint**|Kumulierte Wartezeit für den Controller bei der Suche nach nicht das Protokoll.|  
|waits_for_io|**bigint**|Anzahl von Wartevorgängen für Protokoll-e/a durch die controllerthread verursacht wird.|  
|io_wait_time_in_ms|**bigint**|Kumulierte Zeit für die Wartezeit für Protokoll-e/a durch den controllerthread.|  
|waits_for_new_log_count|**bigint**|Anzahl der Wartevorgänge werden, die den controllerthread für ein neues Protokoll generiert werden soll.|  
|new_log_wait_time_in_ms|**bigint**|Kumulierte Wartezeit auf ein neues Protokoll vom controllerthread.|  
|idle_attempts_count|**bigint**|Anzahl der Wiederholungen, die der Controller in den Leerlauf gewechselt hat.|  
|tx_segments_dispatched|**bigint**|Die Anzahl der Segmente, die von der Controller und die Serialisierungsprogramme weitergeleitet. -Segment ist ein zusammenhängender Bereich des Protokolls, die der Serialisierung bildet. Er ist derzeit auf 1MB großen allerdings in Zukunft ändern kann.|  
|segment_bytes_dispatched|**bigint**|Gesamtzahl der Byte-Anzahl von Bytes, die vom Controller für Serialisierungsprogramme, verteilt werden, da die Datenbank neu starten.|  
|bytes_serialized|**bigint**|Gesamtanzahl der Bytes, die serialisiert werden, da die Datenbank erneut zu starten.|  
|serializer_user_time_in_ms|**bigint**|Zeit im Benutzermodus Serialisierungsprogramme.|  
|serializer_kernel_time_in_ms|**bigint**|Zeit im Kernelmodus Serialisierungsprogramme.|  
|xtp_log_bytes_consumed|**bigint**|Gesamtanzahl der Protokollbytes, die seit der die Datenbank neu starten.|  
|checkpoints_closed|**bigint**|Die Anzahl der Prüfpunkte geschlossen, da die Datenbank neu starten.|  
|last_closed_checkpoint_ts|**bigint**|Der Zeitstempel des letzten Prüfpunkts geschlossen.|  
|hardened_recovery_lsn|**numeric(38)**|Wiederherstellung wird aus dieser LSN gestartet.|  
|hardened_root_file_guid|**uniqueidentifier**|Die GUID der Stammdatei, die als Ergebnis der letzten abgeschlossenen Prüfpunkt festgeschrieben.|  
|hardened_root_file_watermark|**bigint**|**Interne nur**. Wie weit an die Stammdatei bis zu gelesen werden (Dies ist ein intern relevanten Typ nur – BSN bezeichnet).|  
|hardened_truncation_lsn|**numeric(38)**|LSN des den Protokollkürzungspunkt.|  
|log_bytes_since_last_close|**bigint**|Bytes vom letzten Schließen, um das aktuelle Ende des Protokolls.|  
|time_since_last_close_in_ms|**bigint**|Zeit seit der letzten Schließen des Prüfpunkts.|  
|current_checkpoint_id|**bigint**|Derzeit neue Segmente werden auf diesen Prüfpunkt zugewiesen wird. Prüfpunkt-Systems handelt es sich um eine Pipeline. Der aktuelle Prüfpunkt wird die Segmente aus dem Protokoll zugewiesen werden. Einen Grenzwert erreicht wurde, wird der Prüfpunkt durch den Controller und ein neues Konto erstellt, die als aktuell freigegeben.|  
|current_checkpoint_segment_count|**bigint**|Die Anzahl der Segmente in der aktuellen Prüfpunkt.|  
|recovery_lsn_candidate|**bigint**|**Intern nur**. Mögliche als Recoverylsn entnommen werden, wenn Current_checkpoint_id geschlossen wird.|  
|outstanding_checkpoint_count|**bigint**|Die Anzahl der Prüfpunkte in der Pipeline, die darauf warten, geschlossen werden.|  
|closing_checkpoint_id|**bigint**|Die ID des Prüfpunkts schließen.<br /><br /> Serialisierungsprogramme arbeiten parallel, also, sobald sie fertig sind. Klicken Sie dann der Prüfpunkt ein Kandidat zum Schließen Thread geschlossen werden. Aber schließende Thread kann nur jeweils einzeln schließen, und muss er in der Reihenfolge, damit das schließende Prüfpunkt ist, an der der Thread schließende arbeitet.|  
|recovery_checkpoint_id|**bigint**|Die ID des Prüfpunkts in Recovery verwendet werden.|  
|recovery_checkpoint_ts|**bigint**|Der Zeitstempel des Prüfpunkts wiederherstellen.|  
|bootstrap_recovery_lsn|**numeric(38)**|Wiederherstellungs-LSN für den Bootstrap.|  
|bootstrap_root_file_guid|**uniqueidentifier**|GUID der für den Bootstrap-Stammdatei.|  
|internal_error_code|**bigint**|Fehler, die mithilfe einer der Controller, Serialisierungsprogramm geschlossen wurden, und der Merge-Threads angezeigt werden.|
|bytes_of_large_data_serialized|**bigint**|Die Datenmenge, die serialisiert wurde. |  
  
##  <a name="bkmk_2014"></a> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
 Die folgende Tabelle beschreibt die Spalten in `sys.dm_db_xtp_checkpoint_stats`, für **[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]**.  
  
|Spaltenname|Typ|Description|  
|-----------------|----------|-----------------|  
|log_to_process_in_bytes|**bigint**|Die Anzahl von Protokollbytes zwischen der aktuellen Protokollfolgenummer (LSN) und dem Protokollende des Threads.|  
|total_log_blocks_processed|**bigint**|Gesamtzahl der Protokollblöcke, die seit dem Start des Servers verarbeitet wurden.|  
|total_log_records_processed|**bigint**|Gesamtzahl der Protokolldatensätze, die seit dem Start des Servers verarbeitet wurden.|  
|xtp_log_records_processed|**bigint**|Gesamtzahl der In-Memory OLTP-Protokolldatensätze, die seit dem Start des Servers verarbeitet wurden.|  
|total_wait_time_in_ms|**bigint**|Kumulierte Wartezeit (ms).|  
|waits_for_io|**bigint**|Anzahl von Wartevorgängen für Protokoll-EAs.|  
|io_wait_time_in_ms|**bigint**|Kumulierte Wartezeit für Protokoll-EA.|  
|waits_for_new_log|**bigint**|Anzahl der Wartevorgänge für neu zu erstellendes Protokoll.|  
|new_log_wait_time_in_ms|**bigint**|Kumulierte Wartezeit für neues Protokoll.|  
|log_generated_since_last_checkpoint_in_bytes|**bigint**|Umfang des seit dem letzten In-Memory OLTP-Prüfpunkt generierten Protokolls.|  
|ms_since_last_checkpoint|**bigint**|Zeit in Millisekunden seit dem letzten In-Memory OLTP-Prüfpunkt.|  
|checkpoint_lsn|**numeric (38)**|Die Protokollfolgenummer (LSN) der Wiederherstellung, die dem zuletzt abgeschlossenen OLTP-Prüfpunkt im Arbeitsspeicher zugeordnet ist.|  
|current_lsn|**numeric (38)**|Die LSN des Protokolldatensatzes, der gerade verarbeitet wird.|  
|end_of_log_lsn|**numeric (38)**|Die LSN des Protokollendes.|  
|task_address|**varbinary(8)**|Die Adresse von SOS_Task. Stellen Sie einen Join mit sys.dm_os_tasks her, um weitere Informationen zu suchen.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die `VIEW DATABASE STATE`-Berechtigung auf dem Server.  
  
## <a name="see-also"></a>Siehe auch  
 [Eine Speicheroptimierte Tabelle dynamische Verwaltungssichten &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  

---
title: dm_xtp_transaction_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_xtp_transaction_stats_TSQL
- dm_xtp_transaction_stats
- sys.dm_xtp_transaction_stats_TSQL
- sys.dm_xtp_transaction_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_xtp_transaction_stats dynamic management view
ms.assetid: 9389f48d-0de5-47bd-9821-4db8f04504e4
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 83d2a1cfde20eaba1cbf3d01203f3ce88f2b0eed
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmxtptransactionstats-transact-sql"></a>sys.dm_xtp_transaction_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Zeigt Statistiken zu Transaktionen, die ausgeführt wurden, seit der Server gestartet wurde.  
  
 Weitere Informationen finden Sie unter [In-Memory OLTP &#40;Arbeitsspeicheroptimierung&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|total_count|**bigint**|Die Gesamtanzahl der Transaktionen, die im In-Memory OLTP-Datenbankmodul ausgeführt wurden.|  
|read_only_count|**bigint**|Die Anzahl der schreibgeschützten Transaktionen.|  
|total_aborts|**bigint**|Die Gesamtanzahl der Transaktionen, die durch den Benutzer oder das System abgebrochen wurden.|  
|user_aborts|**bigint**|Die Anzahl der vom System initiierten Abbrüche. Mögliche Ursachen: Schreibkonflikte, Überprüfungsfehler oder Abhängigkeitsfehler.|  
|validation_failures|**bigint**|Die Häufigkeit, mit der eine Transaktion aufgrund eines Überprüfungsfehlers abgebrochen wurde.|  
|dependencies_taken|**bigint**|Nur interne Verwendung.|  
|dependencies_failed|**bigint**|Die Häufigkeit, mit der eine Transaktion aufgrund des Abbruchs einer anderen Transaktion, von der diese abhängig war, abgebrochen wurde.|  
|savepoint_create|**bigint**|Die Anzahl der erstellten Sicherungspunkte. Für jeden atomaren Block wird ein neuer Sicherungspunkt erstellt.|  
|savepoint_rollbacks|**bigint**|Die Anzahl der Rollbacks zu einem vorherigen Sicherungspunkt.|  
|savepoint_refreshes|**bigint**|Nur interne Verwendung.|  
|log_bytes_written|**bigint**|Die Gesamtanzahl von Bytes, die in die In-Memory OLTP-Protokolldatensätze geschrieben werden.|  
|log_IO_count|**bigint**|Die Gesamtzahl der Transaktionen, die Protokoll-EAs erfordern. Berücksichtigt nur Transaktionen für permanente Tabellen.|  
|phantom_scans_started|**bigint**|Nur interne Verwendung.|  
|phantom_scans_retries|**bigint**|Nur interne Verwendung.|  
|phantom_rows_touched|**bigint**|Nur interne Verwendung.|  
|phantom_rows_expiring|**bigint**|Nur interne Verwendung.|  
|phantom_rows_expired|**bigint**|Nur interne Verwendung.|  
|phantom_rows_expired_removed|**bigint**|Nur interne Verwendung.|  
|scans_started|**bigint**|Nur interne Verwendung.|  
|scans_retried|**bigint**|Nur interne Verwendung.|  
|rows_returned|**bigint**|Nur interne Verwendung.|  
|rows_touched|**bigint**|Nur interne Verwendung.|  
|rows_expiring|**bigint**|Nur interne Verwendung.|  
|rows_expired|**bigint**|Nur interne Verwendung.|  
|rows_expired_removed|**bigint**|Nur interne Verwendung.|  
|rows_inserted|**bigint**|Nur interne Verwendung.|  
|rows_updated|**bigint**|Nur interne Verwendung.|  
|rows_deleted|**bigint**|Nur interne Verwendung.|  
|write_conflicts|**bigint**|Nur interne Verwendung.|  
|unique_constraint_violations|**bigint**|Die Gesamtzahl von UNIQUE-Einschränkungsverletzungen.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW SERVER STATE-Berechtigung auf dem Server.  
  
## <a name="see-also"></a>Siehe auch  
 [Eine Speicheroptimierte Tabelle dynamische Verwaltungssichten &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  

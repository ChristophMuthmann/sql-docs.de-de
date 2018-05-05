---
title: Sys. dm_tran_database_transactions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/09/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_tran_database_transactions
- sys.dm_tran_database_transactions_TSQL
- dm_tran_database_transactions_TSQL
- sys.dm_tran_database_transactions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_database_transactions dynamic management view
ms.assetid: 82a44295-4cbc-4a5b-891a-8ebaf307b8f5
caps.latest.revision: 33
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: ca4f720028a1877a98a84e2df2fb20d20c67010b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmtrandatabasetransactions-transact-sql"></a>sys.dm_tran_database_transactions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt Informationen zu Transaktionen auf Datenbankebene zurück.  
  
> [!NOTE]  
>  Diese DMV aus aufrufen [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] oder [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], verwenden Sie den Namen **sys.dm_pdw_nodes_tran_database_transactions**.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|transaction_id|**bigint**|ID der Transaktion auf Instanzebene, nicht auf Datenbankebene. Diese ist nur in allen Datenbanken innerhalb einer Instanz eindeutig, nicht jedoch innerhalb aller Serverinstanzen.|  
|database_id|**int**|ID der Datenbank, die der Transaktion zugeordnet ist.|  
|database_transaction_begin_time|**datetime**|Zeitpunkt, zu dem die Datenbank in die Transaktion aufgenommen wurde. Genauer gesagt: Dies ist die Zeit des ersten Protokolldatensatzes in der Datenbank für die Transaktion.|  
|database_transaction_type|**int**|1 = Lese-/Schreibtransaktion<br /><br /> 2 = Schreibgeschützte Transaktion<br /><br /> 3 = Systemtransaktion|  
|database_transaction_state|**int**|1 = Die Transaktion wurde nicht initialisiert.<br /><br /> 3 = Die Transaktion wurde initialisiert, hat jedoch keine Protokolldatensätze generiert.<br /><br /> 4 = Die Transaktion hat Protokolldatensätze generiert.<br /><br /> 5 = Die Transaktion wurde vorbereitet.<br /><br /> 10 = Für die Transaktion wurde ein Commit ausgeführt.<br /><br /> 11 = Für die Transaktion wurde ein Rollback ausgeführt.<br /><br /> 12 = Für die Transaktion wird ein Commit ausgeführt. (Der Protokolldatensatz generiert wird, jedoch nicht materialisiert oder permanent gespeichert.)|  
|database_transaction_status|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|database_transaction_status2|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|database_transaction_log_record_count|**bigint**|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Anzahl der Protokolldatensätze, die in der Datenbank für die Transaktion generiert wurden.|  
|database_transaction_replicate_record_count|**int**|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Die Anzahl der Protokolldatensätze, die in der Datenbank für die Transaktion, die repliziert wird generiert.|  
|database_transaction_log_bytes_used|**bigint**|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Anzahl von Bytes, die bisher im Datenbankprotokoll für die Transaktion verwendet wurden.|  
|database_transaction_log_bytes_reserved|**bigint**|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Anzahl von Bytes, die zur Verwendung im Datenbankprotokoll für die Transaktion reserviert wurden.|  
|database_transaction_log_bytes_used_system|**int**|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Anzahl von Bytes, die im Datenbankprotokoll für Systemtransaktionen bisher für diese Transaktion verwendet wurden.|  
|database_transaction_log_bytes_reserved_system|**int**|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Anzahl von Bytes, die im Datenbankprotokoll für Systemtransaktionen zur Verwendung für diese Transaktion reserviert wurden.|  
|database_transaction_begin_lsn|**numeric(25,0)**|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Protokollfolgenummer (Log Sequence Number, LSN) des ersten Datensatzes für die Transaktion im Datenbankprotokoll.|  
|database_transaction_last_lsn|**numeric(25,0)**|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> LSN des zuletzt protokollierten Datensatzes für die Transaktion im Datenbankprotokoll.|  
|database_transaction_most_recent_savepoint_lsn|**numeric(25,0)**|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> LSN des letzten Sicherungspunktes für die Transaktion im Datenbankprotokoll.|  
|database_transaction_commit_lsn|**numeric(25,0)**|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> LSN des Protokolldatensatzes für den Commit der Transaktion im Datenbankprotokoll.|  
|database_transaction_last_rollback_lsn|**numeric(25,0)**|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> LSN, zu der das letzte Rollback ausgeführt wurde. Wenn kein Rollback stattgefunden hat, ist der Wert MaxLSN.|  
|database_transaction_next_undo_lsn|**numeric(25,0)**|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> LSN des nächsten Datensatzes, der rückgängig gemacht werden soll.|  
|pdw_node_id|**int**|**Gilt für**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Der Bezeichner für den Knoten, dem auf diesem Verteilungspunkt befindet.|  
  
## <a name="permissions"></a>Berechtigungen

Auf [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], erfordert `VIEW SERVER STATE` Berechtigung.   
Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], erfordert die `VIEW DATABASE STATE` Berechtigung in der Datenbank.   

## <a name="see-also"></a>Siehe auch  
 [sys.dm_tran_active_transactions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-active-transactions-transact-sql.md)   
 [sys.dm_tran_session_transactions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-session-transactions-transact-sql.md)   
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Dynamische Verwaltungssichten und Funktionen in Verbindung mit Transaktionen &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  



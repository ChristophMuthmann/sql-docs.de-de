---
title: sys.dm_tran_active_transactions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2017
ms.prod: sql-non-specified
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
- sys.dm_tran_active_transactions
- sys.dm_tran_active_transactions_TSQL
- dm_tran_active_transactions_TSQL
- dm_tran_active_transactions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_active_transactions dynamic management view
ms.assetid: 154ad6ae-5455-4ed2-b014-e443abe2c6ee
caps.latest.revision: 39
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 5aedf9cc79bb389d6920cc736c3f30b319368b07
ms.sourcegitcommit: 8b332c12850c283ae413e0b04b2b290ac2edb672
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/05/2018
---
# <a name="sysdmtranactivetransactions-transact-sql"></a>sys.dm_tran_active_transactions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt Informationen zu Transaktionen für die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zurück.  
  
> [!NOTE]  
>  Aufrufen von [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] oder [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], verwenden Sie den Namen **sys.dm_pdw_nodes_tran_active_transactions**.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|transaction_id|**bigint**|ID der Transaktion auf Instanzebene, nicht auf Datenbankebene. Die ID ist nur für alle Datenbanken in einer Instanz eindeutig, jedoch nicht für alle Serverinstanzen.|  
|name|**nvarchar(32)**|Transaktionsname. Bei Markierung der Transaktion wird der Transaktionsname überschrieben und durch den markierten Namen ersetzt.|  
|transaction_begin_time|**datetime**|Uhrzeit des Transaktionsbeginns.|  
|transaction_type|**int**|Transaktionstyp.<br /><br /> 1 = Lese-/Schreibtransaktion<br /><br /> 2 = Schreibgeschützte Transaktion<br /><br /> 3 = Systemtransaktion<br /><br /> 4 = Verteilte Transaktion|  
|transaction_uow|**uniqueidentifier**|Arbeitseinheits-Bezeichner (Unit of Work, UOW) für verteilte Transaktionen. MS DTC verwendet den UOW-Bezeichner zum Bearbeiten der verteilten Transaktion.|  
|transaction_state|**int**|0 = Die Transaktion wurde noch nicht vollständig initialisiert.<br /><br /> 1 = Die Transaktion wurde initialisiert, aber noch nicht gestartet.<br /><br /> 2 = Die Transaktion ist aktiv.<br /><br /> 3 = Die Transaktion wurde beendet. Diese Einstellung wird für schreibgeschützte Transaktionen verwendet.<br /><br /> 4 = Der Commitprozess wurde für die verteilte Transaktion initiiert. Diese Einstellung wird nur für verteilte Transaktionen verwendet. Die verteilte Transaktion ist noch aktiv, doch ist keine weitere Verarbeitung möglich.<br /><br /> 5 = Die Transaktion hat den Status 'Vorbereitet' und wartet auf Auflösung.<br /><br /> 6 = die Transaktion ein Commit ausgeführt wurde.<br /><br /> 7 = Es wird ein Rollback für die Transaktion durchgeführt.<br /><br /> 8 = die Transaktion wurde ein Rollback.|  
|transaction_status|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|transaction_status2|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|dtc_state|**int**|**Gilt für**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] (ursprüngliche Version bis [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299659)).<br /><br /> 1 = ACTIVE<br /><br /> 2 = PREPARED<br /><br /> 3 = COMMITTED<br /><br /> 4 = ABORTED<br /><br /> 5 = RECOVERED|  
|dtc_status|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|dtc_isolation_level|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|filestream_transaction_id|**varbinary(128)**|**Gilt für**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] (ursprüngliche Version bis [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299659)).<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|pdw_node_id|**int**|**Gilt für**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Der Bezeichner für den Knoten, dem auf diesem Verteilungspunkt befindet.|  
  
## <a name="permissions"></a>Berechtigungen

Auf [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], erfordert `VIEW SERVER STATE` Berechtigung.   
Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], erfordert die `VIEW DATABASE STATE` Berechtigung in der Datenbank.   
  
## <a name="see-also"></a>Siehe auch  
 [sys.dm_tran_session_transactions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-session-transactions-transact-sql.md)   
 [sys.dm_tran_database_transactions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-database-transactions-transact-sql.md)   
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Dynamische Verwaltungssichten und Funktionen in Verbindung mit Transaktionen &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  



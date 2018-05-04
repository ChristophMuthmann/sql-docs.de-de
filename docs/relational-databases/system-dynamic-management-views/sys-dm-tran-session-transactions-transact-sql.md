---
title: dm_tran_session_transactions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2017
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
- dm_tran_session_transactions
- sys.dm_tran_session_transactions
- sys.dm_tran_session_transactions_TSQL
- dm_tran_session_transactions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_session_transactions dynamic management view
ms.assetid: c7157491-58c2-49fe-87d7-0c9723113adf
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 33f46110017b80cf066cbb1726ce4793759a7484
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmtransessiontransactions-transact-sql"></a>sys.dm_tran_session_transactions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt Korrelationsinformationen für zugehörige Transaktionen und Sitzungen zurück.  
  
> [!NOTE]  
>  Aufrufen von [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] oder [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], verwenden Sie den Namen **sys.dm_pdw_nodes_tran_session_transactions**.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|session_id|**int**|ID der Sitzung, unter der die Transaktion ausgeführt wird.|  
|transaction_id|**bigint**|ID der Transaktion.|  
|transaction_descriptor|**binary(8)**|Die Transaktions-ID, die von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] für die Kommunikation mit dem Clienttreiber verwendet wird.|  
|enlist_count|**int**|Anzahl der aktiven Anforderungen in der Sitzung für die Transaktion.|  
|is_user_transaction|**bit**|1 = Die Transaktion wurde von einer Benutzeranforderung initiiert.<br /><br /> 0 = Systemtransaktion.|  
|is_local|**bit**|1 = Lokale Transaktion.<br /><br /> 0 = Verteilte Transaktion oder eine eingetragene gebundene Sitzungstransaktion.|  
|is_enlisted|**bit**|1 = Eingetragene verteilte Transaktion.<br /><br /> 0 = Keine eingetragene verteilte Transaktion.|  
|is_bound|**bit**|1 = Die Transaktion ist in der Sitzung über gebundene Sitzungen aktiv.<br /><br /> 0 = Die Transaktion ist in der Sitzung nicht über gebundene Sitzungen aktiv.|  
|open_transaction_count||Die Anzahl der offenen Transaktionen für jede Sitzung.|  
|pdw_node_id|**int**|**Gilt für**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Der Bezeichner für den Knoten, dem auf diesem Verteilungspunkt befindet.|  
  
## <a name="permissions"></a>Berechtigungen

Auf [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], erfordert `VIEW SERVER STATE` Berechtigung.   
Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], erfordert die `VIEW DATABASE STATE` Berechtigung in der Datenbank.   

## <a name="remarks"></a>Hinweise  
 Über gebundene Sitzungen und verteilte Transaktionen kann eine Transaktion unter mehreren Sitzungen ausgeführt werden. In diesen Fällen zeigt sys.dm_tran_session_transactions mehrere Zeilen für dieselbe transaction_id an, und zwar eine pro Sitzung, unter der die Transaktion ausgeführt wird.  
  
 Durch Ausführen mehrerer Anforderungen im Autocommitmodus mithilfe mehrerer aktiver Resultsets (MARS) ist mehr als eine aktive Transaktion in einer einzigen Sitzung möglich. In diesen Fällen zeigt sys.dm_tran_session_transactions mehrere Zeilen für dieselbe session_id an, und zwar eine pro Transaktion, die unter dieser Sitzung ausgeführt wird.  
  
## <a name="see-also"></a>Siehe auch  
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Dynamische Verwaltungssichten und Funktionen in Verbindung mit Transaktionen &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  



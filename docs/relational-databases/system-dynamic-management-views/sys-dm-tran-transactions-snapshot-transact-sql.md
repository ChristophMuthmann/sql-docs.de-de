---
title: Sys. dm_tran_transactions_snapshot (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_tran_transactions_snapshot
- dm_tran_transactions_snapshot
- sys.dm_tran_transactions_snapshot_TSQL
- dm_tran_transactions_snapshot_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_transactions_snapshot dynamic management view
ms.assetid: 03f64883-07ad-4092-8be0-31973348c647
caps.latest.revision: 37
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 9fffba5bd1015e33b49b5779c6320249aa72dc79
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmtrantransactionssnapshot-transact-sql"></a>sys.dm_tran_transactions_snapshot (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt eine virtuelle Tabelle für die **sequence_number** von Transaktionen zurück, die beim Starten der einzelnen Momentaufnahmetransaktionen aktiv sind. Die von dieser Sicht zurückgegebenen Informationen können Ihnen bei folgenden Aufgaben helfen:  
  
-   Finden der Anzahl derzeit aktiver Momentaufnahmetransaktionen.  
  
-   Identifizieren von Datenänderungen, die von einer bestimmten Momentaufnahmetransaktion ignoriert werden. Für eine Transaktion, die beim Start einer Momentaufnahmetransaktion aktiviert ist, werden alle Datenänderungen durch diese Transaktion, selbst nach dem Commit dieser Transaktion, von der Momentaufnahmetransaktion ignoriert.  
  
 Betrachten Sie beispielsweise die folgende Ausgabe von **sys.dm_tran_transactions_snapshot**:  
  
```  
transaction_sequence_num snapshot_id snapshot_sequence_num  
------------------------ ----------- ---------------------  
59                       0           57  
59                       0           58  
60                       0           57  
60                       0           58  
60                       0           59  
60                       3           57  
60                       3           58  
60                       3           59  
60                       3           60  
```  
  
 Die `transaction_sequence_num` -Spalte identifiziert die Transaktionssequenznummer (XSN) der aktuellen Momentaufnahmetransaktionen. Die Ausgabe zeigt zwei Transaktionssequenznummern: `59` und `60`. Die `snapshot_sequence_num` -Spalte identifiziert die Transaktionssequenznummer der Transaktionen, die beim Start jeder Momentaufnahmetransaktion aktiviert sind.  
  
 Die Ausgabe zeigt, dass Momentaufnahmetransaktion XSN-59 startet, während zwei aktive Transaktionen, XSN-57 und XSN-58, ausgeführt werden. Wenn XSN-57 oder XSN-58 Datenänderungen ausführt, ignoriert XSN-59 die Änderungen und verwendet die Zeilenversionsverwaltung, um eine hinsichtlich der Transaktion konsistente Sicht der Datenbank bereitzustellen.  
  
 Momentaufnahmetransaktion XSN-60 ignoriert Datenänderungen, die von XSN-57 und XSN-58 sowie XSN 59 ausgeführt werden.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
dm_tran_transactions_snapshot  
```  
  
## <a name="table-returned"></a>Zurückgegebene Tabelle  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**transaction_sequence_num**|**bigint**|Transaktionssequenznummer (XSN) einer Momentaufnahmetransaktion.|  
|**snapshot_id**|**int**|Momentaufnahme-ID für die einzelnen [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung gestartet wird, unter der Read committed mit zeilenversionsverwaltung. Mit diesem Wert wird eine im Hinblick auf Transaktionen konsistente Sicht der Datenbank generiert, die jede Abfrage unterstützt, die unter der Snapshotoption READ COMMITTED mit Zeilenversionsverwaltung ausgeführt wird.|  
|**snapshot_sequence_num**|**bigint**|Die Transaktionssequenznummer einer Transaktion, die beim Starten der Momentaufnahmetransaktion aktiviert war.|  
  
## <a name="permissions"></a>Berechtigungen

Auf [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], erfordert `VIEW SERVER STATE` Berechtigung.   
Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], erfordert die `VIEW DATABASE STATE` Berechtigung in der Datenbank.   
  
## <a name="remarks"></a>Hinweise  
 Wenn eine Snapshot-Transaktion gestartet wird, die [!INCLUDE[ssDE](../../includes/ssde-md.md)] zeichnet alle Transaktionen, die zu diesem Zeitpunkt aktiv sind. **sys.dm_tran_transactions_snapshot** erfasst diese Informationen für alle derzeit aktiven Momentaufnahmetransaktionen.  
  
 Jede Transaktion wird durch eine Transaktionssequenznummer identifiziert, die zu Transaktionsbeginn zugewiesen wird. Transaktionen starten zu dem Zeitpunkt, zu dem eine BEGIN TRANSACTION- oder BEGIN WORK-Anweisung ausgeführt wird. [!INCLUDE[ssDE](../../includes/ssde-md.md)] ordnet hingegen die Transaktionssequenznummer mit der Ausführung der ersten [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung zu, die nach der BEGIN TRANSACTION- oder BEGIN WORK-Anweisung auf Daten zugreift. Transaktionssequenznummern werden um eins erhöht.  
  
## <a name="see-also"></a>Siehe auch  
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Dynamische Verwaltungssichten und Funktionen in Verbindung mit Transaktionen &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


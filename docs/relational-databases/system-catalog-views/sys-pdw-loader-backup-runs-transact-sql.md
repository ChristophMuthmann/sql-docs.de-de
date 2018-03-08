---
title: Sys.pdw_loader_backup_runs (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 2b72034c-6a11-46b9-a76c-7a88b2bea360
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2bc42a27de363d0c1f3e62a4b3f69b8b9fbb95de
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="syspdwloaderbackupruns-transact-sql"></a>sys.pdw_loader_backup_runs (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Enthält Informationen zu laufenden und abgeschlossenen sicherungs- und Wiederherstellungsvorgänge in [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], und zum laufenden und abgeschlossenen Sicherung, Wiederherstellung und Ladevorgänge in [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]. Die Informationen, die über Systemneustarts weiterhin besteht.  
  
|Spaltenname|Datentyp|Description|Bereich|  
|-----------------|---------------|-----------------|-----------|  
|run_id|**int**|Eindeutiger Bezeichner für eine bestimmte Sicherung, Wiederherstellung oder für Auslastungstests.<br /><br /> Der Schlüssel für diese Ansicht.||  
|name|**nvarchar(255)**|NULL für den Auslastungstest. Optionalen Namen für die Sicherung oder Wiederherstellung.||  
|submit_time|**datetime**|Zeitpunkt, zu die Anforderung übermittelt wurde.||  
|start_time|**datetime**|Zeit, zu der der Vorgang gestartet wurde.||  
|end_time|**datetime**|Zeitpunkt der Vorgang abgeschlossen, fehlgeschlagen oder wurde abgebrochen.||  
|total_elapsed_time|**int**|Insgesamt verstrichene Zeit zwischen Start_time und aktuelle Uhrzeit oder zwischen Start_time und End_time nach einem abgeschlossenen, abgebrochenen oder fehlgeschlagenen ausgeführt wird.|Wenn Total_elapsed_time den maximalen Wert für eine ganze Zahl (24.8 Tage in Millisekunden) überschreitet, führt es Materialisierung Fehler aufgrund einer dazu, dass "Überlauf".<br /><br /> Der maximale Wert in Millisekunden entspricht 24.8 Tage.|  
|operation_type|**nvarchar(16)**|Der Typ der arbeitsauslastung.|"BACKUP", "LAST", "WIEDERHERSTELLEN"|  
|mode|**nvarchar(16)**|Der Modus in den Typ ausführen.|Für Operation_type = **Sicherung**<br />**DIFFERENTIAL**<br />**FULL**<br /><br /> Für Operation_type = **laden**<br />**ANFÜGEN**<br />**ZUM ERNEUTEN LADEN**<br />**UPSERT**<br /><br /> Für Operation_type = **wiederherstellen**<br />**DATABASE**<br />**HEADER_ONLY**|  
|database_name|**nvarchar(255)**|Name der Datenbank, die im Rahmen dieses Vorgangs ist.||  
|table_name|**nvarchar(255)**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|Principal_id|**int**|ID des Benutzers, der den Vorgang anfordert.||  
|session_id|**nvarchar(32)**|Die ID der Sitzung Ausführen des Vorgangs.|Finden Sie unter Session_id in [sys.dm_pdw_exec_sessions &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md).|  
|request_id|**nvarchar(32)**|Die ID der Anforderung, die den Vorgang ausführt. Für das Laden ist dies der aktuellen oder letzten Anforderung, diese Last zugeordnet...|Finden Sie unter Request_id in [sys.dm_pdw_exec_requests &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|status|**nvarchar(16)**|Status der Ausführung.|'CANCELLED','COMPLETED','FAILED','QUEUED','RUNNING'|  
|Status|**int**|Prozentsatz der Fertigstellung.|0 bis 100|  
|Befehl|**nvarchar(4000)**|Vollständige Text des Befehls vom Benutzer übermittelt.|Wird Wenn mehr als 4000 Zeichen (Zählung von Leerzeichen) abgeschnitten.|  
|rows_processed|**bigint**|Anzahl der Zeilen, die als Teil dieses Vorgangs verarbeitet.||  
|rows_rejected|**bigint**|Anzahl der Zeilen, die als Teil dieses Vorgangs abgelehnt.||  
|rows_inserted|**bigint**|Anzahl der Zeilen, die in den Tabellen der Datenbank eingefügt werden, im Rahmen dieses Vorgangs.||  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Datawarehouse und Parallel Datawarehouse-Katalogsichten](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  

---
title: Sys. dm_continuous_copy_status (Azure SQL-Datenbank) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: dmv's
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_continuous_copy_status_TSQL
- dm_continuous_copy_status_TSQL
- dm_continuous_copy_status
- sys.dm_continuous_copy_status
dev_langs:
- TSQL
helpviewer_keywords:
- dm_continuous_copy_status
- sys.dm_continuous_copy_status
ms.assetid: 411b2e71-4421-4ef5-900d-5af068750899
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: d94787cd01bc93f6ae49da39a717a389225940ab
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="sysdmcontinuouscopystatus-azure-sql-database"></a>Sys. dm_continuous_copy_status (Azure SQL-Datenbank)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Gibt eine Zeile für jede Benutzerdatenbank (V11), die derzeit in einer Beziehung mit kontinuierlichem kopieren geografische Replikation beteiligt ist. Wenn für eine bestimmte primäre Datenbank mehr als eine Beziehung mit kontinuierlichem Kopieren initiiert wird, enthält diese Tabelle für jede aktive sekundäre Datenbank eine Zeile.  
  
Bei Verwendung von SQL-Datenbank V12 sollten Sie verwenden [sys.dm_geo_replication_link_status](../../relational-databases/system-dynamic-management-views/sys-dm-geo-replication-link-status-azure-sql-database.md) (da *Sys. dm_continuous_copy_status* gilt nur für Version 11).

  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**copy_guid**|**uniqueidentifier**|Eindeutige ID der Replikatdatenbank.|  
|**partner_server**|**sysname**|Der Name des SQL-Datenbankverbindungsservers.|  
|**partner_database**|**sysname**|Name der Verbindungsdatenbank auf dem SQL-Datenbankverbindungsserver.|  
|**last_replication**|**datetimeoffset**|Der Zeitstempel der zuletzt durchgeführten replizierten Transaktion.|  
|**replication_lag_sec**|**int**|Der Zeitunterschied in Sekunden zwischen der aktuellen Zeit und dem Zeitstempel der letzten Transaktion in der primären Datenbank, für die erfolgreich ein Commit ausgeführt wurde und die von der aktiven sekundären Datenbank nicht bestätigt wurde.|  
|**replication_state**|**tinyint**|Der Status der fortlaufenden kopierbeziehung für diese Datenbank. Im folgenden sind die möglichen Werte und deren Beschreibungen.<br /><br /> 1: seeding. Für das Replikationsziel, das einen inkonsistenten Transaktionsstatus aufweist, wird ein Seeding durchgeführt. Solange das Seeding noch nicht abgeschlossen wurde, können Sie keine Verbindung mit der aktiven sekundären Datenbank herstellen. <br />2: aufholen. Die aktive sekundäre Datenbank holt derzeit den Rückstand zur primären Datenbank auf und weist hinsichtlich der Transaktionen einen konsistenten Status auf.<br />3: Erneutes seeding. Für die aktive sekundäre Datenbank wird aufgrund eines nicht behebbaren Replikationsfehlers automatisch ein erneutes Seeding durchgeführt.<br />4: angehalten. Dies ist keine aktive Beziehung mit kontinuierlichem Kopieren. Dieser Status gibt normalerweise an, dass die Bandbreite, die für den Interlink verfügbar ist, für die Ebene der Transaktionsaktivität in der primären Datenbank nicht ausreicht. Die Beziehung mit kontinuierlichem Kopieren ist jedoch nach wie vor intakt.|  
|**replication_state_desc**|**nvarchar(256)**|Beschreibung von replication_state. Folgende Werte sind möglich:<br /><br /> SEEDING<br /><br /> CATCH_UP<br /><br /> RE_SEEDING<br /><br /> SUSPENDED|  
|**is_rpo_limit_reached**|**bit**|Wird immer auf 0 festgelegt.|  
|**is_target_role**|**bit**|0 = Quelle der Kopienbeziehung<br /><br /> 1 = Ziel der Kopienbeziehung|  
|**is_interlink_connected**|**bit**|1 = Interlink ist verbunden.<br /><br /> 0 = Interlink-Verbindung ist getrennt.|  
  
## <a name="permissions"></a>Berechtigungen  
 Zum Abrufen von Daten, erfordert die Mitgliedschaft in der **Db_owner** -Datenbankrolle. Die Dbo-Benutzer, der Mitglied der **Dbmanager** Datenbankrolle und Anmeldenamens "sa" können alle Abfragen in dieser Ansicht auch.  
  
## <a name="remarks"></a>Hinweise  
 Die **Sys. dm_continuous_copy_status** Sicht wird erstellt, der **Ressource** -Datenbank und in allen Datenbanken, einschließlich der logischen Masterdatenbank sichtbar ist. Wenn aber diese Sicht in der logischen master-Datenbank abgerufen wird, wird ein leeres Set zurückgegeben.  
  
 Wenn die fortlaufende kopierbeziehung, in einer Datenbank, die Zeile für diese Datenbank in beendet wird der **Sys. dm_continuous_copy_status** -Sicht nicht mehr angezeigt.  
  
 Wie die **dm_database_copies** Ansicht **Sys. dm_continuous_copy_status** zeigt den Status der fortlaufenden kopierbeziehung in dem die Datenbank entweder eine primäre oder aktive sekundäre Datenbank ist . Im Gegensatz zu **dm_database_copies**, **Sys. dm_continuous_copy_status** enthält mehrere Spalten, die Details zu Vorgängen und Leistung bereitstellen. Diese Spalten enthalten **Last_replication**, und **Replication_lag_sec**...  
  
## <a name="see-also"></a>Siehe auch  
 [Sys. dm_database_copies &#40;Azure SQL-Datenbank&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-database-copies-azure-sql-database.md)   
 [Aktive geografische Replikation gespeicherten Prozeduren &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/81658ee4-4422-4d73-bf7a-86a07422cb0d)  
  
  

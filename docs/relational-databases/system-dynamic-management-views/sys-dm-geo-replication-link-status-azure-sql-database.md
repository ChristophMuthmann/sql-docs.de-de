---
title: Sys.dm_geo_replication_link_status (Azure SQL-Datenbank) | Microsoft Docs
ms.custom: 
ms.date: 10/13/2016
ms.prod: 
ms.prod_service: sql-database
ms.reviewer: 
ms.service: sql-database
ms.component: dmv's
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- dm_geo_replication_link_status
- dm_geo_replication_link_status_TSQL
- sys.dm_geo_replication_link_status
- sys.dm_geo_replication_link_status_TSQL
helpviewer_keywords:
- dm_geo_replication_link_status dynamic management view
- sys.dm_geo_replication_link_status dynamic management view
ms.assetid: d763d679-470a-4c21-86ab-dfe98d37e9fd
caps.latest.revision: "15"
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0399e0ef7587a7a7cb8a7ef32419518f1b95d53e
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmgeoreplicationlinkstatus-azure-sql-database"></a>Sys.dm_geo_replication_link_status (Azure SQL-Datenbank)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Enthält eine Zeile für jeden Replikationslink zwischen primären und sekundären Datenbanken in einer Partnerschaft geografische Replikation. Dies schließt primäre und sekundäre Datenbanken. Wenn mehr als einen Link für die fortlaufende Replikation für eine bestimmte primäre Datenbank vorhanden ist, enthält diese Tabelle eine Zeile für jede der Beziehungen. Die Ansicht ist in allen Datenbanken, einschließlich der logischen Masterdatenbank erstellt. Wenn aber diese Sicht in der logischen master-Datenbank abgerufen wird, wird ein leeres Set zurückgegeben.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|link_guid|**uniqueidentifier**|Eindeutige ID des Replikationslinks.|  
|partner_server|**sysname**|Der Name des logischen Servers, auf die verknüpfte Datenbank.|  
|partner_database|**sysname**|Name der Verbindungsdatenbank auf dem logischen Verbindungsserver.|  
|last_replication|**datetimeoffset**|Der Zeitstempel der letzten Transaktion Bestätigung vom sekundären basierend auf der primären Datenbank Uhr. Dieser Wert ist auf nur die primäre Datenbank verfügbar.|  
|replication_lag_sec|**int**|Der Zeitunterschied in Sekunden zwischen dem Last_replication-Wert und den Zeitstempel der Commit dieser Transaktion, auf dem primären basierend auf der primären Datenbank Uhr.  Dieser Wert ist auf nur die primäre Datenbank verfügbar.|  
|replication_state|**tinyint**|Der Status der geografischen Replikation für diese Datenbank, eines:.<br /><br /> 1 = Seeding. Das Ziel für die geografische Replikation wird ein Seeding, aber die beiden Datenbanken noch nicht synchronisiert. Bis zum Abschluss des Seedings herstellen nicht Sie die sekundäre Datenbank. Entfernen der sekundären Datenbank vom primären Server werden den Seedingvorgang abzubrechen.<br /><br /> 2 = aufholen. Die sekundäre Datenbank befindet sich in einem transaktionskonsistenten Zustand und wird ständig mit der primären Datenbank synchronisiert.<br /><br /> 4 = angehalten. Dies ist keine aktive Beziehung mit kontinuierlichem Kopieren. Dieser Status gibt normalerweise an, dass die Bandbreite, die für den Interlink verfügbar ist, für die Ebene der Transaktionsaktivität in der primären Datenbank nicht ausreicht. Die Beziehung mit kontinuierlichem Kopieren ist jedoch nach wie vor intakt.|  
|replication_state_desc|**nvarchar(256)**|PENDING<br /><br /> SEEDING<br /><br /> CATCH_UP|  
|Rolle (role)|**tinyint**|Geografische Replikation-Rolle, eine von:<br /><br /> 0 = Primary. Die Database_id bezieht sich auf die primäre Datenbank in der Partnerschaft geografische Replikation.<br /><br /> 1 = der sekundären Datenbank.  Die Database_id bezieht sich auf die primäre Datenbank in der Partnerschaft geografische Replikation.|  
|role_desc|**nvarchar(256)**|PRIMARY<br /><br /> SECONDARY|  
|secondary_allow_connections|**tinyint**|Sekundären Typs, einer der:<br /><br /> 0 = keine direkten Verbindungen zugelassen werden, in der sekundären Datenbank und die Datenbank ist nicht für Lesezugriff verfügbar.<br /><br /> 2 = alle Verbindungen sind zulässig, in der Datenbank in die sekundäre Repl; Ication für schreibgeschützten Zugriff.|  
|secondary_allow_connections_desc|**nvarchar(256)**|Nein<br /><br /> Alle|  
|last_commit|**datetimeoffset**|Der Zeitpunkt der letzten Transaktion, die an die Datenbank übergeben. In der sekundären Datenbank abgerufen, wenn das primäre des Replikationslinks ausgefallen ist, weist dies darauf hin bis was zeigen Sie die sekundäre Datenbank aufgeholt hat.|
  
> [!NOTE]  
>  Wenn die replikationsbeziehung beendet wird, durch das Entfernen der sekundären Datenbank (im Abschnitt 4.2.), die Zeile für diese Datenbank in der **sys.dm_geo_replication_link_status** -Sicht nicht mehr angezeigt.  
  
## <a name="permissions"></a>Berechtigungen  
 Jedes Konto mit Berechtigung View_database_state kann Abfragen **sys.dm_geo_replication_link_status**.  
  
## <a name="example"></a>Beispiel  
 Replikation Verzögerungen und Zeitpunkt der letzten Replikation meinem sekundären Datenbanken anzeigen.  
  
```  
SELECT   
     link_guid  
   , partner_server  
   , last_replication  
   , replication_lag_sec   
FROM sys.dm_geo_replication_link_status;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER DATABASE &#40; Azure SQL-Datenbank &#41;](../../t-sql/statements/alter-database-azure-sql-database.md)   
 [Sys.geo_replication_links &#40; Azure SQL-Datenbank &#41;](../../relational-databases/system-dynamic-management-views/sys-geo-replication-links-azure-sql-database.md)   
 [Sys. dm_operation_status &#40; Azure SQL-Datenbank &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md)  
  
  

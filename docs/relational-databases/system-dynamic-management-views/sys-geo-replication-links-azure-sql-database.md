---
title: Sys.geo_replication_links (Azure SQL-Datenbank) | Microsoft Docs
ms.custom: 
ms.date: 10/18/2016
ms.prod: 
ms.prod_service: sql-database
ms.reviewer: 
ms.service: sql-database
ms.component: dmv's
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- dm_geo_replication_links_TSQL
- dm_geo_replication_links
- sys.dm_geo_replication_links
- sys.dm_geo_replication_links_TSQL
helpviewer_keywords:
- sys.dm_geo_replication_links dynamic management view
- dm_geo_replication_links dynamic management view
ms.assetid: 58911798-1d60-4f28-87ab-2def2bfc3de7
caps.latest.revision: 
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5eb8f74023e90966200aca7603b82f685e0eb9db
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="sysgeoreplicationlinks-azure-sql-database"></a>Sys.geo_replication_links (Azure SQL-Datenbank)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Enthält eine Zeile für jeden Replikationslink zwischen primären und sekundären Datenbanken in einer Partnerschaft geografische Replikation. Diese Ansicht befindet sich in der logischen master-Datenbank.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|database_id|**int**|Die ID der aktuellen Datenbank in der sys.databases-Sicht.|  
|start_date|**datetimeoffset**|UTC-Zeit in einem regionalen SQL-Datenbank-Datencenter, die Datenbankreplikation initiiert wurde|  
|modify_date|**datetimeoffset**|UTC-Zeit im regionalen SQL-Datenbank-Datencenter, zu der die Datenbank Geo-Replikation abgeschlossen wurde. Die neue Datenbank wird mit der primären Datenbank ab diesem Zeitpunkt synchronisiert. aus.|  
|link_guid|**uniqueidentifier**|Eindeutige ID des Links geografische Replikation.|  
|partner_server|**sysname**|Der Name des logischen Servers mit der Datenbank geografisch repliziert.|  
|partner_database|**sysname**|Name der Datenbank auf dem Verbindungsserver logischen geografisch repliziert.|  
|replication_state|**tinyint**|Der Status der geografischen Replikation für diese Datenbank, eines:.<br /><br /> 0 = ausstehend. Erstellung der aktiven sekundären Datenbank geplant ist, aber die notwendigen Vorbereitungsschritte sind noch nicht abgeschlossen.<br /><br /> 1 = Seeding. Das Ziel für die geografische Replikation wird ein Seeding, aber die beiden Datenbanken noch nicht synchronisiert. Bis zum Abschluss des Seedings herstellen nicht Sie die sekundäre Datenbank. Entfernen der sekundären Datenbank vom primären Server werden den Seedingvorgang abzubrechen.<br /><br /> 2 = aufholen. Die sekundäre Datenbank befindet sich in einem transaktionskonsistenten Zustand und wird ständig mit der primären Datenbank synchronisiert.|  
|replication_state_desc|**nvarchar(256)**|PENDING<br /><br /> SEEDING<br /><br /> CATCH_UP|  
|Rolle (role)|**tinyint**|Geografische Replikation-Rolle, eine von:<br /><br /> 0 = Primary. Die Database_id bezieht sich auf die primäre Datenbank in der Partnerschaft geografische Replikation.<br /><br /> 1 = der sekundären Datenbank.  Die Database_id bezieht sich auf die primäre Datenbank in der Partnerschaft geografische Replikation.|  
|role_desc|**nvarchar(256)**|PRIMARY<br /><br /> SECONDARY|  
|secondary_allow_connections|**tinyint**|Sekundären Typs, einer der:<br /><br /> 0 = Nein. Die sekundäre Datenbank ist nicht verfügbar, bis ein Failover erfolgt.<br /><br /> 1 = ReadOnly. Die sekundäre Datenbank ist nur für Clientverbindungen mit ApplicationIntent = ReadOnly.<br /><br /> 2 = Alle. Die sekundäre Datenbank ist für jede Clientverbindung zugänglich.|  
|secondary_allow_connections _desc|**nvarchar(256)**|nein<br /><br /> Alle<br /><br /> Schreibgeschützt|  
  
## <a name="permissions"></a>Berechtigungen  
 Diese Sicht ist nur verfügbar, in der **master** Datenbank der prinzipalanmeldung auf Serverebene.  
  
## <a name="example"></a>Beispiel  
 Zeigen Sie alle Datenbanken mit geografische Replikation Links.  
  
```  
SELECT   
     database_id  
   , start_date  
   , partner_server  
   , partner_database  
   , replication_state  
   , role_desc  
   , secondary_allow_connections_desc   
FROM sys.geo_replication_links;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER DATABASE (Azure SQL-Datenbank)](../../t-sql/statements/alter-database-azure-sql-database.md)   
 [Sys.dm_geo_replication_link_status &#40; Azure SQL-Datenbank &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-geo-replication-link-status-azure-sql-database.md)   
 [Sys. dm_operation_status &#40; Azure SQL-Datenbank &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md)  
  
  

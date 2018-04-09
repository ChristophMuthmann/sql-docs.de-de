---
title: Sys.elastic_pool_resource_stats (Azure SQL-Datenbank) | Microsoft Docs
ms.custom: ''
ms.date: 04/06/2018
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: system-catalog-views
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- Azure SQL Database
f1_keywords:
- sys.elastic_pool_resource_stats catalog view
helpviewer_keywords:
- sys.elastic_pool_resource_stats_TSQL
- sys.elastic_pool_resource_stats
- elastic_pool_resource_stats_TSQL
- elastic_pool_resource_stats
ms.assetid: f242c1bd-3cc8-4c8b-8aaf-c79b6a8a0329
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c1e77bcfcfd4e27981f63fd2802fd6b76c18fe1f
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2018
---
# <a name="syselasticpoolresourcestats-azure-sql-database"></a>Sys.elastic_pool_resource_stats (Azure SQL-Datenbank)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Gibt ressourcenauslastungsstatistiken für alle Pools für elastische Datenbanken in einem logischen Server zurück. Für jeden Pool für elastische Datenbanken wird eine Zeile für jedes Fenster (vier Zeilen pro Minute) reporting von 15 Sekunden. Dies umfasst CPU, e/a-, Log, Speicherverbrauch und gleichzeitige Anforderung/Sitzung Auslastung durch alle Datenbanken im Pool. Diese Daten werden 14 Tage lang beibehalten. 
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssSDS](../../includes/sssds-md.md)] V12.|  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**start_time**|**datetime2**|UTC-Zeit, die den Anfang des Berichtsintervalls von 15 Sekunden.|  
|**end_time**|**datetime2**|UTC-Zeit, die das Ende des Berichtsintervalls von 15 Sekunden.|  
|**elastic_pool_name**|**nvarchar(128)**|Der Name des elastischen Pools.|  
|**avg_cpu_percent**|**decimal(5,2)**|Durchschnittliche servernutzung als Prozentwert der maximalen Kapazität des Pools.|  
|**avg_data_io_percent**|**decimal(5,2)**|Durchschnittliche e/a-Auslastung in Prozent basierend auf den Grenzwert des Pools.|  
|**avg_log_write_percent**|**decimal(5,2)**|Durchschnittliche schreibressourcenauslastung in Prozent des Grenzwerts des Pools.|  
|**avg_storage_percent**|**decimal(5,2)**|Durchschnittliche speicherauslastung in Prozent, der die Speicherkapazität des Pools an.|  
|**max_worker_percent**|**decimal(5,2)**|Maximale gleichzeitige Arbeitsthreads (Anforderungen) als Prozentwert der maximalen Kapazität des Pools für.|  
|**max_session_percent**|**decimal(5,2)**|Maximaler gleichzeitiger Sitzungen als Prozentwert der maximalen Kapazität des Pools für.|  
|**elastic_pool_dtu_limit**|**int**|Aktuelle max elastischen Pool-dtu-Einstellung für diesen elastischen Pool während dieses Intervalls.|  
|**elastic_pool_storage_limit_mb**|**bigint**|Aktuelle max elastischen Pool Speicherobergrenze für diesen elastischen Pool in Megabyte während dieses Intervalls festlegen.|  
  
## <a name="remarks"></a>Hinweise  
 Diese Sicht ist in der master-Datenbank des logischen Servers vorhanden. Sie müssen verbunden sein, mit der Masterdatenbank abzufragende **sys.elastic_pool_resource_stats**.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **Dbmanager** Rolle.  
  
## <a name="examples"></a>Beispiele  
 Im folgende Beispiel gibt die ressourcennutzungsdaten sortiert nach der letzten Zeit für die elastische datenbankpools auf dem aktuellen logischen Server zurück.  
  
```  
SELECT * FROM sys.elastic_pool_resource_stats   
ORDER BY end_time DESC;  
```  
  
 Im folgende Beispiel wird die durchschnittliche DTU-Verbrauch in Prozent für einen bestimmten Pool berechnet.  
  
```  
SELECT start_time, end_time,      
  (SELECT Max(v)      
FROM (VALUES (avg_cpu_percent), (avg_data_io_percent), (avg_log_write_percent)) AS value(v)) AS [avg_DTU_percent]    
FROM sys.elastic_pool_resource_stats   
WHERE elastic_pool_name = '<your pool name>'   
ORDER BY end_time DESC;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Tame dramatisch für elastische Datenbanken](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool/)   
 [Erstellen Sie und verwalten Sie einen Pool für elastische Datenbanken SQL-Datenbank (Vorschau)](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool-portal/)   
 [Sys. resource_stats &#40;Azure SQL-Datenbank&#41;](../../relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database.md)   
 [Sys. dm_db_resource_stats &#40;Azure SQL-Datenbank&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-resource-stats-azure-sql-database.md)  
  
  

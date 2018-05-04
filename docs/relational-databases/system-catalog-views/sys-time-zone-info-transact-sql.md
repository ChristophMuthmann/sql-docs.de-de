---
title: Sys. time_zone_info (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/27/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Data Warehouse
- SQL Server (starting with 2016)
f1_keywords:
- sys.time_zone_info
- sys.time_zone_info_TSQL
- time_zone_info
- time_zone_info_TSQL
helpviewer_keywords:
- sys.time_zone_info system table
ms.assetid: 3f51a9a4-75f8-4a11-9552-8bf6118b68da
caps.latest.revision: 7
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 6c652ad6e9db451d490d8803f9689e9e82b1c231
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="systimezoneinfo-transact-sql"></a>Sys. time_zone_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  Gibt Informationen zu unterstützten Zeitzonen zurück. Alle Zeitzonen, die auf dem Computer installiert werden in der folgenden Registrierungsstruktur gespeichert:  
`KEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Time Zones`installiert haben.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Der Name der Zeitzone im Windows-Standardformat. Beispielsweise **"CEN" Ostaustralische Normalzeit** oder **Mitteleuropäische Zeit**.|  
|**current_utc_offset**|**nvarchar(12)**|Die aktuelle offset zur UTC. Beispielsweise **+ 01:00** oder **-07: 00**.|  
|**is_currently_dst**|**bit**|"True", wenn die Sommerzeit derzeit zu beobachten.|  
  
## <a name="see-also"></a>Siehe auch  
 [GETUTCDATE &#40;Transact-SQL&#41;](../../t-sql/functions/getutcdate-transact-sql.md)   
 [AT TIME ZONE &#40;Transact-SQL&#41;](../../t-sql/queries/at-time-zone-transact-sql.md)   
 [Date and Time Data Types and Functions &#40;Transact-SQL&#41; (Datums- und Uhrzeitdatentypen und zugehörige Funktionen &#40;Transact-SQL&#41;)](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)   
 [Katalogsichten für die serverweite Konfiguration &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/server-wide-configuration-catalog-views-transact-sql.md)  

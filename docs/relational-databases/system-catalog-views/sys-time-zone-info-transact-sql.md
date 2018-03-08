---
title: Sys. time_zone_info (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 09/12/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
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
helpviewer_keywords: sys.time_zone_info system table
ms.assetid: 3f51a9a4-75f8-4a11-9552-8bf6118b68da
caps.latest.revision: "7"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: b4d893e468c2d9820506bb4be18de8c8fbb6dd28
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="systimezoneinfo-transact-sql"></a>Sys. time_zone_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Gibt Informationen zu unterstützten Zeitzonen zurück. Alle Zeitzonen, die auf dem Computer installiert werden in der folgenden Registrierungsstruktur gespeichert:  
`KEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Time Zones`.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Der Name der Zeitzone im Windows-Standardformat. Beispielsweise **"CEN" Ostaustralische Normalzeit** oder **Mitteleuropäische Zeit**.|  
|**current_utc_offset**|**nvarchar(12)**|Die aktuelle offset zur UTC. Beispielsweise **+ 01:00** oder **-07: 00**.|  
|**is_currently_dst**|**bit**|"True", wenn die Sommerzeit derzeit zu beobachten.|  
  
## <a name="see-also"></a>Siehe auch  
 [GETUTCDATE &#40; Transact-SQL &#41;](../../t-sql/functions/getutcdate-transact-sql.md)   
 [ZEITZONE &AMP;#40; Transact-SQL &#41;](../../t-sql/queries/at-time-zone-transact-sql.md)   
 [Datums- und Zeitdaten Typen und-Funktionen &#40; Transact-SQL &#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)   
 [Serverweite Konfiguration-Katalogsichten &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/server-wide-configuration-catalog-views-transact-sql.md)  
  
  

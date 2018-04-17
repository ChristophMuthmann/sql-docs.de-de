---
title: Sys.dm_xe_database_session_targets (Azure SQL-Datenbank) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
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
ms.assetid: 7f353e2a-f8fc-4366-97e4-aa1c49eadaf4
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 7284d59668742f2ad8821ebfb435de469ed31c4e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmxedatabasesessiontargets-azure-sql-database"></a>Sys.dm_xe_database_session_targets (Azure SQL-Datenbank)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Gibt Informationen über Sitzungsziele zurück.  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 und alle zukünftigen Versionen.|  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary(8)**|Die Speicheradresse der Ereignissitzung. Verfügt über eine viele-zu-eins-Beziehung mit sys.dm_xe_database_sessions.address aus. Lässt keine NULL-Werte zu.|  
|target_name|**nvarchar(60)**|Der Name des Ziels innerhalb einer Sitzung. Lässt keine NULL-Werte zu.|  
|target_package_guid|**uniqueidentifier**|Die GUID des Pakets, das das Ziel enthält Lässt keine NULL-Werte zu.|  
|execution_count|**bigint**|Die Häufigkeit, mit der das Ziel für die Sitzung ausgeführt wurde. Lässt keine NULL-Werte zu.|  
|execution_duration_ms|**bigint**|Die gesamte Zeit in Millisekunden, für die das Ziel ausgeführt wurde. Lässt keine NULL-Werte zu.|  
|target_data|**nvarchar(max)**|Die Daten, die das Ziel beibehält, z. B. Ereignisaggregationsinformationen. Lässt NULL-Werte zu.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW DATABASE STATE-Berechtigung.  
  
### <a name="relationship-cardinalities"></a>Kardinalität der Beziehungen  
  
|Von|Aktion|Beziehung|  
|----------|--------|------------------|  
|Sys.dm_xe_database_session_targets.event_session_address|sys.dm_xe_database_sessions.address|n:1|  
  
  

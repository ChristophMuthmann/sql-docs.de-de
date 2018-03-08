---
title: Sys.dm_xe_database_session_object_columns (Azure SQL-Datenbank) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: 
ms.prod_service: sql-database
ms.reviewer: 
ms.service: sql-database
ms.component: dmv's
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 0e6adc54-4d97-4ef0-bf4f-b4538d69f136
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c0799d00819bade1e0f87fceb916aa649aef150a
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmxedatabasesessionobjectcolumns-azure-sql-database"></a>Sys.dm_xe_database_session_object_columns (Azure SQL-Datenbank)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Zeigt die Konfigurationswerte für Objekte an, die an eine Sitzung gebunden sind.  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 und alle späteren Versionen.|  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary(8)**|Die Speicheradresse der Ereignissitzung. Verfügt über eine viele-zu-eins-Beziehung mit sys.dm_xe_database_sessions.address aus. Lässt keine NULL-Werte zu.|  
|column_name|**nvarchar(60)**|Der Name des Konfigurationswerts. Lässt keine NULL-Werte zu.|  
|column_id|**int**|Die ID der Spalte. Ist eindeutig innerhalb des Objekts. Lässt keine NULL-Werte zu.|  
|column_value|**nvarchar(2048)**|Der konfigurierte Wert der Spalte. Lässt NULL-Werte zu.|  
|object_type|**nvarchar(60)**|Der Typ des Objekts.  Ist keine nullable.object_type eines:<br /><br /> Ereignis<br /><br /> target|  
|object_name|**nvarchar(60)**|Der Name des Objekts, zu dem diese Spalte gehört. Lässt keine NULL-Werte zu.|  
|object_package_guid|**uniqueidentifier**|Die GUID des Pakets, das das Objekt enthält. Lässt keine NULL-Werte zu.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW DATABASE STATE-Berechtigung.  
  
### <a name="relationship-cardinalities"></a>Kardinalität der Beziehungen  
  
|Von|Aktion|Beziehung|  
|----------|--------|------------------|  
|dm_xe_database_session_object_columns.object_name<br /><br /> dm_xe_database_session_object_columns.object_package_guid|sys.dm_xe_objects.package_guid<br /><br /> sys.dm_xe_objects.name|n:1|  
|dm_xe_database_session_object_columns.column_name<br /><br /> dm_xe_database_session_object_columns.column_id|sys.dm_xe_object_columns.name<br /><br /> sys.dm_xe_object_columns.column_id|n:1|  
  
## <a name="see-also"></a>Siehe auch  
 [Erweiterte Ereignisse](../../relational-databases/extended-events/extended-events.md)  
  
  

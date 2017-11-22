---
title: Sys.dm_pdw_nodes (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: 93966909-d758-4d50-950b-f5066d104fa6
caps.latest.revision: "7"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 95748ae75cedb219d2a0948d3d1e55586c6861e4
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmpdwnodes-transact-sql"></a>Sys.dm_pdw_nodes (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Enthält Informationen zu allen Knoten im [!INCLUDE[ssAPS](../../includes/ssaps-md.md)]. Sie enthält eine Zeile pro Knoten in der Einheit.  
  
|Spaltenname|Datentyp|Description|Bereich|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|Eindeutige numerische Id, die dem Knoten zugeordnet.<br /><br /> Der Schlüssel für diese Ansicht.|Für die Appliance, unabhängig vom Typ eindeutig.|  
|Typ|**nvarchar(32)**|Der Typ des Knotens.|"COMPUTE", "CONTROL", "VERWALTUNG"|  
|name|**nvarchar(32)**|Logischer Name des Knotens.|Eine beliebige Zeichenfolge entsprechenden Länge.|  
|address|**nvarchar(32)**|IP-Adresse dieses Knotens.|Im Format [0-255]. [0-255]. [0-255]. [0-255].|  
|is_passive|**int**|Gibt an, ob der virtuelle Computer mit dem Knoten, die auf dem zugeordneten Server ausgeführt wird oder ein auf dem Ersatzserver Failover wurde.|0 – hauptknotencomputer wird auf dem ursprünglichen Server ausgeführt werden.<br /><br /> 1 – hauptknotencomputer wird auf dem Ersatzserver ausgeführt.|  
|Bereich|**nvarchar(32)**|Die Region, in dem der Knoten ausgeführt wird.|"PDW', 'HDINSIGHT'|  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Datawarehouse und dynamische Verwaltungssichten für Parallel Datawarehouse &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  

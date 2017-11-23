---
title: Sys.dm_pdw_component_health_status (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 68cc3f7a-693c-4d5d-a76b-455352af8d7f
caps.latest.revision: "6"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d87c8ef38185e3194da1d13f8a9732991023f0ab
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmpdwcomponenthealthstatus-transact-sql"></a>Sys.dm_pdw_component_health_status (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Enthält Informationen zu den aktuellen Zustand der Anwendung Komponenten.  
  
|Spaltenname|Datentyp|Description|Bereich|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**||NOT NULL|  
|component_id|int|Die ID der Komponente. Finden Sie unter [sys.pdw_health_components &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).<br /><br /> Pdw_node_id, Component_id Property_id und Component_instance_id bilden den Schlüssel für diese Ansicht ein.|NOT NULL|  
|property_id|**int**|Die ID der Eigenschaft. Finden Sie unter [sys.pdw_health_component_properties &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-pdw-health-component-properties-transact-sql.md).|NOT NULL|  
|component_instance_id|**nvarchar(255)**|Gibt eine Instanz einer Komponente. Beispielsweise kann eine Instanz von der CPU-Auslastung von Component_instance_id identifiziert werden = CPU "1".<br /><br /> Pdw_node_id, Component_id Property_id und Component_instance_id bilden den Schlüssel für diese Ansicht ein.|NOT NULL|  
|property_value|**nvarchar(255)**|Der aktuelle Eigenschaftswert.|NULL|  
|update_time|**datetime**|Zuletzt aktualisiert wurde die Metrik.|NOT NULL|  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Datawarehouse und dynamische Verwaltungssichten für Parallel Datawarehouse &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  

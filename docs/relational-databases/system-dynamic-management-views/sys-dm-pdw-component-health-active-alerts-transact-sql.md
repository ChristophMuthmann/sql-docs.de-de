---
title: Sys.dm_pdw_component_health_active_alerts (Transact-SQL) | Microsoft Docs
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
ms.assetid: c53e4a36-b841-424a-b8e2-255b1878deb6
caps.latest.revision: "8"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c88fd88a8545e5fa375732377f0afdbf92b70f96
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmpdwcomponenthealthactivealerts-transact-sql"></a>Sys.dm_pdw_component_health_active_alerts (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Aktive Warnungen speichert [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] Komponenten.  
  
|Spaltenname|Datentyp|Description|Bereich|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|Der eindeutige Bezeichner einer [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] Knoten.<br /><br /> Pdw_node_id, Component_id Component_instance_id, Alert_id und Alert_instance_id bilden den Schlüssel für diese Ansicht ein.|NOT NULL|  
|component_id|**int**|Die ID der Komponente. Finden Sie unter [sys.pdw_health_components &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).<br /><br /> Pdw_node_id, Component_id Component_instance_id, Alert_id und Alert_instance_id bilden den Schlüssel für diese Ansicht ein.|NOT NULL|  
|component_instance_id|**nvarchar(255)**|Pdw_node_id, Component_id Component_instance_id, Alert_id und Alert_instance_id bilden den Schlüssel für diese Ansicht ein.|NOT NULL|  
|alert_id|**int**|Die ID für den Warnungstyp aus. Finden Sie unter [sys.pdw_health_alerts &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md).<br /><br /> Pdw_node_id, Component_id Component_instance_id, Alert_id und Alert_instance_id bilden den Schlüssel für diese Ansicht ein.|NOT NULL|  
|alert_instance_id|**nvarchar(36)**|Gibt eine Instanz einer bestimmten Warnung.<br /><br /> Pdw_node_id, Component_id Component_instance_id, Alert_id und Alert_instance_id bilden den Schlüssel für diese Ansicht ein.|NOT NULL|  
|current_value|**nvarchar(255)**|Verwendet, wenn die Warnung vom Typ StatusChange ist. Dies ist der aktuelle Komponentenstatus. Wert ist NULL für Warnungen vom Typ Schwellenwert. Finden Sie unter [sys.pdw_health_alerts &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md) eine Liste der Warnungstypen.|NULL|  
|previous_value|**nvarchar(255)**|Verwendet, wenn die Warnung vom Typ StatusChange ist. Dies ist der vorherige Komponentenstatus. Wert ist NULL für Warnungen vom Typ Schwellenwert. Finden Sie unter [sys.pdw_health_alerts &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md) eine Liste der Warnungstypen.|NULL|  
|create_time|**datetime**|Uhrzeit und Datum, wenn die Warnung generiert wurde.|NOT NULL|  
  
 Informationen über die maximale Zeilenanzahl, die von dieser Ansicht beibehalten werden, finden Sie unter "Minimale und Maximalwerte" in der [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Datawarehouse und dynamische Verwaltungssichten für Parallel Datawarehouse &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  

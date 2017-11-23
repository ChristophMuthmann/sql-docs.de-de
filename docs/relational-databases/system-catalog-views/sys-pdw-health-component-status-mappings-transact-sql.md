---
title: Sys.pdw_health_component_status_mappings (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4272cfad-5ad7-493d-9edd-d9111619bda0
caps.latest.revision: "7"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bdce6d1bf58727b78282ebdf46c71974cfaafc94
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="syspdwhealthcomponentstatusmappings-transact-sql"></a>Sys.pdw_health_component_status_mappings (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Definiert die Zuordnung zwischen der [!INCLUDE[ssDW](../../includes/ssdw-md.md)] Komponentenstatus und den Hersteller definierte Komponentennamen.  
  
|Spaltenname|Datentyp|Description|Bereich|  
|-----------------|---------------|-----------------|-----------|  
|property_id|**int**|Eindeutiger Bezeichner der Eigenschaft.<br /><br /> Property_id und Component_id Physical_name bilden den Schlüssel für diese Ansicht ein.|NOT NULL|  
|component_id|**int**|Die ID der Komponente. Finden Sie unter [sys.pdw_health_components &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).<br /><br /> Property_id und Component_id Physical_name bilden den Schlüssel für diese Ansicht ein.|NOT NULL|  
|physical_name|**nvarchar(32)**|Eigenschaftenname, wie vom Hersteller definiert.<br /><br /> Property_id und Component_id Physical_name bilden den Schlüssel für diese Ansicht ein.|NOT NULL|  
|logical_name|**nvarchar(255)**|Eigenschaftsnamen gemäß der Definition von [!INCLUDE[ssDW](../../includes/ssdw-md.md)].|NOT NULL<br /><br /> 0 – Geräteinstanz ist eindeutig.<br /><br /> 1 - Geräteinstanz ist nicht eindeutig.|  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Datawarehouse und Parallel Datawarehouse-Katalogsichten](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  

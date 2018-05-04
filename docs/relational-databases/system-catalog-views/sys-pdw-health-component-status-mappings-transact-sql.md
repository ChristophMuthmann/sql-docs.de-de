---
title: Sys.pdw_health_component_status_mappings (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: pdw
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4272cfad-5ad7-493d-9edd-d9111619bda0
caps.latest.revision: 7
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: be811802c8c49a58eb55b7724863be86a3fa0ace
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="syspdwhealthcomponentstatusmappings-transact-sql"></a>Sys.pdw_health_component_status_mappings (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Definiert die Zuordnung zwischen der [!INCLUDE[ssDW](../../includes/ssdw-md.md)] Komponentenstatus und den Hersteller definierte Komponentennamen.  
  
|Spaltenname|Datentyp|Description|Bereich|  
|-----------------|---------------|-----------------|-----------|  
|property_id|**int**|Eindeutiger Bezeichner der Eigenschaft.<br /><br /> Property_id und Component_id Physical_name bilden den Schlüssel für diese Ansicht ein.|NOT NULL|  
|component_id|**int**|Die ID der Komponente. Finden Sie unter [sys.pdw_health_components &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).<br /><br /> Property_id und Component_id Physical_name bilden den Schlüssel für diese Ansicht ein.|NOT NULL|  
|physical_name|**nvarchar(32)**|Eigenschaftenname, wie vom Hersteller definiert.<br /><br /> Property_id und Component_id Physical_name bilden den Schlüssel für diese Ansicht ein.|NOT NULL|  
|logical_name|**nvarchar(255)**|Eigenschaftsnamen gemäß der Definition von [!INCLUDE[ssDW](../../includes/ssdw-md.md)].|NOT NULL<br /><br /> 0 – Geräteinstanz ist eindeutig.<br /><br /> 1 - Geräteinstanz ist nicht eindeutig.|  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Datawarehouse und Parallel Datawarehouse-Katalogsichten](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  

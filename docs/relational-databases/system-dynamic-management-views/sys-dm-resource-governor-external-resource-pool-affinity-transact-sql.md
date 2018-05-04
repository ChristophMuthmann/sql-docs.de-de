---
title: Sys. dm_resource_governor_external_resource_pool_affinity (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/13/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_resource_governor_external_resource_pool_affinity
- sys.dm_resource_governor_external_resource_pool_affinity_TSQL
- dm_resource_governor_external_resource_pool_affinity
- dm_resource_governor_external_resource_pool_affinity_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_resource_governor_external_resource_pool_affinity
- dm_resource_governor_external_resource_pool_affinity
ms.assetid: e32fac49-5161-47c0-8540-af3fe730c00c
caps.latest.revision: 8
author: jeannt
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 11a7ff1947d3c7cf53370a912bcba9368fb4302d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmresourcegovernorexternalresourcepoolaffinity-transact-sql"></a>Sys. dm_resource_governor_external_resource_pool_affinity (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]
**Gilt für :** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)] und [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

CPU-affinitätsinformationen über die aktuelle Konfiguration der externen Ressourcenpools zurück.
  
|Spaltenname|Datentyp|Description|
|----------------|---------------|-----------------|
|pool_id|**int**|Die ID des externen Ressourcenpools. Lässt keine NULL-Werte zu.|
|processor_group|**smallint**|Die ID der logischen Windows-Prozessorgruppe. Lässt keine NULL-Werte zu.|
|cpu_mask|**bigint**|Die binäre Maske, die diesem Pool zugeordnete CPUs darstellt. Lässt keine NULL-Werte zu.|
  
## <a name="remarks"></a>Hinweise

Pools, die mit der Affinität erstellt werden `AUTO` werden nicht in dieser Ansicht angezeigt, da sie keine Affinität besitzen. Weitere Informationen finden Sie unter der [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41; ](../../t-sql/statements/create-external-resource-pool-transact-sql.md) und [ALTER EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41; ](../../t-sql/statements/alter-external-resource-pool-transact-sql.md) Anweisungen.

## <a name="permissions"></a>Berechtigungen

Erfordert die `VIEW SERVER STATE`-Berechtigung.

## <a name="see-also"></a>Siehe auch

[Resource governance for machine learning in SQL Server (Ressourcenkontrolle für Machine Learning in SQL Server)](../../advanced-analytics/r/resource-governance-for-r-services.md)

[sys.dm_resource_governor_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pool-affinity-transact-sql.md)

[Externe Skripts aktiviert (Serverkonfigurationsoption)](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)

[ALTER EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)

---
title: Sys.pdw_database_mappings (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 10/17/2017
ms.prod: sql-non-specified
ms.prod_service: pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: 4ae2c71e-dd56-41ea-a16b-64936175b459
caps.latest.revision: "9"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5a08d9b0fdb770918c1bb7c8b08e253af58be314
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="syspdwdatabasemappings-transact-sql"></a>Sys.pdw_database_mappings (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Zuordnungen der **Database_id**s der Datenbanken auf dem physischen Namen für Serverknoten verwendet und stellt die **Prinzipal-Id** des Datenbankbesitzers auf dem System. Join **sys.pdw_database_mappings** auf **sys.databases** und **sys.pdw_nodes_pdw_physical_databases**.  
  
|Spaltenname|Datentyp|Description|Bereich|  
|-----------------|---------------|-----------------|-----------|  
|physical_name|**nvarchar(36)**|Der physische Name für die Datenbank auf den Serverknoten.<br /><br /> **Physical_name** und **Database_id** bilden den Schlüssel für diese Ansicht.||  
|database_id|**int**|Die Objekt-ID für die Datenbank. Finden Sie unter [sys.databases &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).<br /><br /> **Physical_name** und **Database_id** bilden den Schlüssel für diese Ansicht.||  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>Beispiele:[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 Im folgenden Beispiel verknüpft sys.pdw_database_mappings mit anderen Systemtabellen, um anzuzeigen, wie Datenbanken zugeordnet werden.  
  
```  
SELECT DB.database_id, DB.name, Map.*, Phys.*   
FROM sys.databases AS DB  
JOIN sys.pdw_database_mappings AS Map  
    ON DB.database_id = Map.database_id  
JOIN sys.pdw_nodes_pdw_physical_databases AS Phys  
    ON Map.physical_name = Phys.physical_name  
ORDER BY DB.database_id, Phys.pdw_node_id;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Datawarehouse und Parallel Datawarehouse-Katalogsichten](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [Sys.pdw_index_mappings &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-index-mappings-transact-sql.md)   
 [Sys.pdw_table_mappings &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-table-mappings-transact-sql.md)   
 [Sys.pdw_nodes_pdw_physical_databases &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-pdw-physical-databases-transact-sql.md)  
  
  


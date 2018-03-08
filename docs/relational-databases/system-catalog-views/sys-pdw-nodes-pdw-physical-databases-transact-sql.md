---
title: sys.pdw_nodes_pdw_physical_databases (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/09/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 70e0939d-4d97-4ae0-ba16-934e0a80e718
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 61ffd5ddd2c246b3bcd8910591393779368081b5
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="syspdwnodespdwphysicaldatabases-transact-sql"></a>sys.pdw_nodes_pdw_physical_databases (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Enthält eine Zeile für jede physische Datenbank auf einem Serverknoten. Aggregieren Sie die physische Datenbankinformationen, um ausführliche Informationen zu Datenbanken abzurufen. Informationen zu kombinieren, verknüpfen die `sys.pdw_nodes_pdw_physical_databases` auf die `sys.pdw_database_mappings` und `sys.databases` Tabellen.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|database_id|**int**|Die Objekt-ID für die Datenbank. Beachten Sie, dass dieser Wert nicht identisch mit einem Database_id in die [sys.databases &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) anzeigen.|  
|physical_name|**sysname**|Der physische Name für die Datenbank auf die Shell/Serverknoten. Dieser Wert ist identisch mit einem Wert in der Spalte Physical_name der [sys.pdw_database_mappings &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-pdw-database-mappings-transact-sql.md) anzeigen.|  
|pdw_node_id|**int**|Eindeutige numerische Id, die dem Knoten zugeordnet.|  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-returning"></a>A. Zurückgeben von  
 Die folgende Abfrage gibt den Namen und die ID der einzelnen Datenbanken in Master und den entsprechenden Datenbanknamen auf jedem Computeknoten zurück.  
  
```  
SELECT D.database_id AS DBID_in_master, D.name AS UserDatabaseName,   
PD.pdw_node_id AS NodeID, DM.physical_name AS PhysDBName   
FROM sys.databases AS D  
JOIN sys.pdw_database_mappings AS DM  
    ON D.database_id = DM.database_id  
JOIN sys.pdw_nodes_pdw_physical_databases AS PD  
    ON DM.physical_name = PD.physical_name  
ORDER BY D.database_id, PD.pdw_node_ID;  
```  
  
### <a name="b-using-syspdwnodespdwphysicaldatabases-to-gather-detailed-object-information"></a>B. Verwenden zum Sammeln von ausführlichen Objektinformationen sys.pdw_nodes_pdw_physical_databases  
 Die folgende Abfrage zeigt Informationen zu Indizes und enthält nützliche Informationen über die Datenbank an, dass die Objekte auf Objekte in der Datenbank gehören.  
  
```  
SELECT D.name AS UserDatabaseName, D.database_id AS DBIDinMaster,  
DM.physical_name AS PhysDBName, PD.pdw_node_id AS NodeID,   
IU.object_id, IU.index_id, IU.user_seeks, IU.user_scans, IU.user_lookups, IU.user_updates  
FROM sys.databases AS D  
JOIN sys.pdw_database_mappings AS DM  
    ON D.database_id = DM.database_id  
JOIN sys.pdw_nodes_pdw_physical_databases AS PD  
    ON DM.physical_name = PD.physical_name  
JOIN sys.dm_pdw_nodes_db_index_usage_stats AS IU  
    ON PD.database_id = IU.database_id  
ORDER BY D.database_id, IU.object_id, IU.index_id, PD.pdw_node_ID;  
```  
  
### <a name="c-using-syspdwnodespdwphysicaldatabases-to-determine-the-encryption-state"></a>C. Verwenden zum Ermitteln des Verschlüsselungsstatus sys.pdw_nodes_pdw_physical_databases  
 Die folgende Abfrage stellt Verschlüsselungsstatus der Datenbank AdventureWorksPDW2012.  
  
```  
WITH dek_encryption_state AS   
(  
    SELECT ISNULL(db_map.database_id, dek.database_id) AS database_id, encryption_state  
    FROM sys.dm_pdw_nodes_database_encryption_keys AS dek  
        INNER JOIN sys.pdw_nodes_pdw_physical_databases AS node_db_map  
            ON dek.database_id = node_db_map.database_id AND dek.pdw_node_id = node_db_map.pdw_node_id  
        LEFT JOIN sys.pdw_database_mappings AS db_map  
            ON node_db_map .physical_name = db_map.physical_name  
        INNER JOIN sys.dm_pdw_nodes AS nodes  
            ON nodes.pdw_node_id = dek.pdw_node_id  
    WHERE dek.encryptor_thumbprint <> 0x  
)  
SELECT TOP 1 encryption_state  
       FROM  dek_encryption_state  
       WHERE dek_encryption_state.database_id = DB_ID('AdventureWorksPDW2012 ')  
       ORDER BY (CASE encryption_state WHEN 3 THEN -1 ELSE encryption_state END) DESC;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Datawarehouse und Parallel Datawarehouse-Katalogsichten](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.pdw_database_mappings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-database-mappings-transact-sql.md)  
  
  


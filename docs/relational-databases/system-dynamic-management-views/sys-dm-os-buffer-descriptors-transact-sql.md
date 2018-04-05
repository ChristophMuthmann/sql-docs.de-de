---
title: Sys. dm_os_buffer_descriptors (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_os_buffer_descriptors_TSQL
- dm_os_buffer_descriptors_TSQL
- sys.dm_os_buffer_descriptors
- dm_os_buffer_descriptors
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_buffer_descriptors dynamic management view
ms.assetid: 012aab95-8888-4f35-9ea3-b5dff6e3f60f
caps.latest.revision: 48
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d64627b7d232503494a3aff308eb24273df98313
ms.sourcegitcommit: 8b332c12850c283ae413e0b04b2b290ac2edb672
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/05/2018
---
# <a name="sysdmosbufferdescriptors-transact-sql"></a>sys.dm_os_buffer_descriptors (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt Informationen zu allen Datenseiten zurück, die derzeit im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Pufferpool sind. Die Ausgabe dieser Sicht kann verwendet werden, um die Verteilung der Datenbankseiten im Pufferpool gemäß der Datenbank, des Objekts oder des Typs zu bestimmen. In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] gibt diese dynamische Verwaltungssicht auch Informationen über die Datenseiten in der Pufferpoolerweiterungsdatei zurück. Weitere Informationen finden Sie unter [Buffer Pool Extension](../../database-engine/configure-windows/buffer-pool-extension.md).  
  
 Beim Lesen einer Datenseite vom Datenträger wird die Seite in den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Pufferpool kopiert und für die Wiederverwendung zwischengespeichert. Jede zwischengespeicherte Datenseite verfügt über einen Pufferdeskriptor. Pufferdeskriptoren identifizieren jede Datenseite eindeutig, die derzeit in einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zwischengespeichert ist. sys.dm_os_buffer_descriptors gibt zwischengespeicherte Seiten für alle Benutzer- und Systemdatenbanken zurück. Dazu zählen auch Seiten, die der Ressourcendatenbank zugeordnet sind.  
  
> **Hinweis:** von Aufrufen [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] oder [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], verwenden Sie den Namen **sys.dm_pdw_nodes_os_buffer_descriptors**.  

|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|database_id|**int**|ID der Datenbank, die der Seite im Pufferpool zugeordnet ist. Lässt NULL-Werte zu.|  
|file_id|**int**|ID der Datei, die das persistente Image der Seite speichert. Lässt NULL-Werte zu.|  
|page_id|**int**|ID der Seite innerhalb der Datei. Lässt NULL-Werte zu.|  
|page_level|**int**|Indexebene der Seite. Lässt NULL-Werte zu.|  
|allocation_unit_id|**bigint**|ID der Zuordnungseinheit der Seite. Dieser Wert kann für den Join mit sys.allocation_units verwendet werden. Lässt NULL-Werte zu.|  
|page_type|**nvarchar(60)**|Typ der Seite, z. B. Datenseite oder Indexseite. Lässt NULL-Werte zu.|  
|row_count|**int**|Anzahl der Zeilen auf der Seite. Lässt NULL-Werte zu.|  
|free_space_in_bytes|**int**|Umfang des verfügbaren Speicherplatzes auf der Seite (in Byte). Lässt NULL-Werte zu.|  
|is_modified|**bit**|1 = Seite wurde nach dem Lesen vom Datenträger geändert. Lässt NULL-Werte zu.|  
|numa_node|**int**|NUMA-Knoten (Non-Uniform Memory Access) für den Puffer. Lässt NULL-Werte zu.|  
|read_microsec|**bigint**|Die tatsächliche Zeit (in Mikrosekunden), die erforderlich ist, um die Seite in den Puffer einzulesen. Diese Zahl wird zurückgesetzt, wenn der Puffer wiederverwendet wird. Lässt NULL-Werte zu.|  
|is_in_bpool_extension|**bit**|1 = Seite befindet sich in der pufferpoolerweiterung. Lässt NULL-Werte zu.|  
|pdw_node_id|**int**|**Gilt für**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Der Bezeichner für den Knoten, dem auf diesem Verteilungspunkt befindet.|  
  
## <a name="permissions"></a>Berechtigungen  

Auf [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], erfordert `VIEW SERVER STATE` Berechtigung.   
Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], erfordert die `VIEW DATABASE STATE` Berechtigung in der Datenbank.   
   
## <a name="remarks"></a>Hinweise  
 Sys. dm_os_buffer_descriptors gibt Seiten, die von der Resource-Datenbank verwendet werden. Sys. dm_os_buffer_descriptors gibt keine Informationen über freie oder gestohlene Seite oder zu Seiten, die beim Lesen Fehler enthielten zurück.  
  
|Von|Aktion|On|Beziehung|  
|----------|--------|--------|------------------|  
|sys.dm_os_buffer_descriptors|sys.databases|database_id|Viele-zu-eins|  
|sys.dm_os_buffer_descriptors|\<userdb>.sys.allocation_units|allocation_unit_id|Viele-zu-eins|  
|sys.dm_os_buffer_descriptors|\<userdb>.sys.database_files|file_id|Viele-zu-eins|  
|sys.dm_os_buffer_descriptors|sys.dm_os_buffer_pool_extension_configuration|file_id|Viele-zu-eins|  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-returning-cached-page-count-for-each-database"></a>A. Zurückgeben der zwischengespeicherten Seitenanzahl für jede Datenbank  
 Im folgenden Beispiel wird die für jede Datenbank geladene Seitenanzahl zurückgegeben.  
  
```  
SELECT COUNT(*)AS cached_pages_count  
    ,CASE database_id   
        WHEN 32767 THEN 'ResourceDb'   
        ELSE db_name(database_id)   
        END AS database_name  
FROM sys.dm_os_buffer_descriptors  
GROUP BY DB_NAME(database_id) ,database_id  
ORDER BY cached_pages_count DESC;  
```  
  
### <a name="b-returning-cached-page-count-for-each-object-in-the-current-database"></a>B. Zurückgeben der zwischengespeicherten Seitenanzahl für jedes Objekt in der aktuellen Datenbank  
 Im folgenden Beispiel wird die für jedes Objekt in der aktuellen Datenbank geladene Seitenanzahl zurückgegeben.  
  
```  
SELECT COUNT(*)AS cached_pages_count   
    ,name ,index_id   
FROM sys.dm_os_buffer_descriptors AS bd   
    INNER JOIN   
    (  
        SELECT object_name(object_id) AS name   
            ,index_id ,allocation_unit_id  
        FROM sys.allocation_units AS au  
            INNER JOIN sys.partitions AS p   
                ON au.container_id = p.hobt_id   
                    AND (au.type = 1 OR au.type = 3)  
        UNION ALL  
        SELECT object_name(object_id) AS name     
            ,index_id, allocation_unit_id  
        FROM sys.allocation_units AS au  
            INNER JOIN sys.partitions AS p   
                ON au.container_id = p.partition_id   
                    AND au.type = 2  
    ) AS obj   
        ON bd.allocation_unit_id = obj.allocation_unit_id  
WHERE database_id = DB_ID()  
GROUP BY name, index_id   
ORDER BY cached_pages_count DESC;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sys.allocation_units &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)   
 
 [SQL Server-Betriebssystem verbundene dynamische Verwaltungssichten &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [Ressourcendatenbank](../../relational-databases/databases/resource-database.md)   
 [Sys.dm_os_buffer_pool_extension_configuration &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-buffer-pool-extension-configuration-transact-sql.md)  
  
  



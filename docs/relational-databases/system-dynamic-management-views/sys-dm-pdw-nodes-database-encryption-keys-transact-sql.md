---
title: Sys.dm_pdw_nodes_database_encryption_keys (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: e7fd02b2-5d7e-4816-a0af-b58ae2ac3f7a
caps.latest.revision: 9
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: d497f9e6fb2e9fcf8a9c383243d82389f3348dcf
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmpdwnodesdatabaseencryptionkeys-transact-sql"></a>Sys.dm_pdw_nodes_database_encryption_keys (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Gibt Informationen über den Verschlüsselungsstatus einer Datenbank und die ihr zugeordneten Verschlüsselungsschlüssel für die Datenbank zurück. **sys.dm_pdw_nodes_database_encryption_keys** provides this information for each node. Weitere Informationen über die datenbankverschlüsselung finden Sie unter [Transparent Data Encryption (SQL Server PDW)](http://msdn.microsoft.com/en-us/b82ad21d-09dd-43dd-8fab-bcf2c8c3ac6d).  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|database_id|**int**|Die ID der physischen Datenbank auf jedem Knoten.|  
|encryption_state|**int**|Gibt an, ob die Datenbank auf diesem Knoten verschlüsselt oder nicht verschlüsselt.<br /><br /> 0 = Kein Verschlüsselungsschlüssel für die Datenbank vorhanden, keine Verschlüsselung<br /><br /> 1 = Unverschlüsselt<br /><br /> 2 = Verschlüsselung wird ausgeführt<br /><br /> 3 = Verschlüsselt.<br /><br /> 4 = Schlüsseländerung wird ausgeführt<br /><br /> 5 = Entschlüsselung wird ausgeführt<br /><br /> 6 = schutzänderung ausgeführt (das Zertifikat, das Verschlüsseln des Verschlüsselungsschlüssels wird geändert wird.)|  
|create_date|**datetime**|Zeigt das Datum der Erstellung des Verschlüsselungsschlüssels an.|  
|regenerate_date|**datetime**|Zeigt das Datum der Neugenerierung des Verschlüsselungsschlüssels an.|  
|modify_date|**datetime**|Zeigt das Datum der Änderung des Verschlüsselungsschlüssels an.|  
|set_date|**datetime**|Zeigt das Datum der Anwendung des Verschlüsselungsschlüssels auf die Datenbank an.|  
|opened_date|**datetime**|Zeigt das Datum an, an dem der Datenbankschlüssel zuletzt geöffnet wurde.|  
|key_algorithm|**varchar(?)**|Zeigt den Algorithmus an, der für den Schlüssel verwendet wird.|  
|key_length|**int**|Zeigt die Länge des Schlüssels an.|  
|encryptor_thumbprint|**varbin**|Zeigt den Fingerabdruck der Verschlüsselung an.|  
|percent_complete|**real**|Prozentualer Anteil der bereits abgeschlossenen Änderung des Verschlüsselungsstatus einer Datenbank. Dieser Wert ist 0, wenn es keine Statusänderung gibt.|  
|node_id|**int**|Eindeutige numerische Id, die dem Knoten zugeordnet.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW SERVER STATE-Berechtigung auf dem Server.  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
 Das folgende Beispiel verknüpft `sys.dm_pdw_nodes_database_encryption_keys` mit anderen Systemtabellen an den Verschlüsselungsstatus für jeden Knoten von der TDE eine Datenbank geschützt.  
  
```  
SELECT D.database_id AS DBIDinMaster, D.name AS UserDatabaseName,   
PD.pdw_node_id AS NodeID, DM.physical_name AS PhysDBName,   
keys.encryption_state  
FROM sys.dm_pdw_nodes_database_encryption_keys AS keys  
JOIN sys.pdw_nodes_pdw_physical_databases AS PD  
    ON keys.database_id = PD.database_id AND keys.pdw_node_id = PD.pdw_node_id  
JOIN sys.pdw_database_mappings AS DM  
    ON DM.physical_name = PD.physical_name  
JOIN sys.databases AS D  
    ON D.database_id = DM.database_id  
ORDER BY D.database_id, PD.pdw_node_ID;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Datawarehouse und Parallel Data Warehouse-dynamische Verwaltungssichten &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)   
 [CREATE DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-encryption-key-transact-sql.md)   
 [ALTER DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-encryption-key-transact-sql.md)   
 [DROP DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-encryption-key-transact-sql.md)  
  
  


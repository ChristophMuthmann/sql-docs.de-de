---
title: Sys. dm_db_missing_index_columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
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
- dm_db_missing_index_columns_TSQL
- sys.dm_db_missing_index_columns_TSQL
- sys.dm_db_missing_index_columns
- dm_db_missing_index_columns
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_missing_index_columns dynamic management function
- missing indexes feature [SQL Server], sys.dm_db_missing_index_columns dynamic management function
ms.assetid: 3b24e5ed-0c79-47e5-805c-a0902d0aeb86
caps.latest.revision: 40
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: da062527194387dbfbc2c2516722bbbad8faf304
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmdbmissingindexcolumns-transact-sql"></a>sys.dm_db_missing_index_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt Informationen zu Spalten von Datenbanktabellen zurück, für die kein Index vorhanden ist, mit Ausnahme von räumlichen Indizes. **Sys. dm_db_missing_index_columns** ist eine dynamische Verwaltungsfunktion.  

## <a name="syntax"></a>Syntax  
  
```  
  
sys.dm_db_missing_index_columns(index_handle)  
```  
  
## <a name="arguments"></a>Argumente  
 *index_handle*  
 Eine ganze Zahl, die einen fehlenden Index eindeutig identifiziert. Sie kann aus den folgenden dynamischen Verwaltungsobjekten abgerufen werden:  
  
 [sys.dm_db_missing_index_details &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)  
  
 [sys.dm_db_missing_index_groups &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-groups-transact-sql.md)  
  
## <a name="table-returned"></a>Zurückgegebene Tabelle  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**column_id**|**int**|ID der Spalte.|  
|**column_name**|**sysname**|Name der Tabellenspalte.|  
|**column_usage**|**varchar(20)**|Art der Verwendung der Spalte durch die Abfrage. Die möglichen Werte und deren Beschreibungen sind:<br /><br /> Gleichheit: Spalte wird in ein Prädikat, das Gleichheit, von dem Formular drückt einbezogen: <br />                        *table.column* = *constant_value*<br /><br /> UNGLEICHHEITSOPERATOR: Spalte trägt zur ein Prädikat, das Ungleichheit, z. B. ausdrückt ein Prädikat im Format: *table.column* > *für Constant_value*. Jeder Vergleichsoperator außer "=" drückt Ungleichheit aus.<br /><br /> INCLUDE: Spalte wird nicht verwendet werden, um die Auswertung eines Prädikats, aber er ist einem anderen Grund verwendet, z. B. zum Abdecken einer Abfrage.|  
  
## <a name="remarks"></a>Hinweise  
 Zurückgegebene Informationen **dm_db_missing_index_columns** wird aktualisiert, wenn eine Abfrage vom Abfrageoptimierer optimiert wird, und wird nicht beibehalten. Informationen zu fehlenden Indizes werden nur bis zum Neustart von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aufbewahrt. Datenbankadministratoren sollten regelmäßig Sicherungskopien der Informationen zu fehlenden Indizes erstellen, wenn Sie sie nach dem Wiederverwenden des Servers beibehalten möchten.  
  
## <a name="transaction-consistency"></a>Transaktionskonsistenz  
 Wenn durch eine Transaktion eine Tabelle erstellt oder gelöscht wird, werden die Zeilen mit Informationen zu fehlenden Indizes bezüglich der gelöschten Objekte aus diesem dynamischen Verwaltungsobjekt entfernt, damit die Transaktionskonsistenz erhalten bleibt.  
  
## <a name="permissions"></a>Berechtigungen  
 Benutzern muss die VIEW SERVER STATE-Berechtigung oder eine Berechtigung, die die VIEW SERVER STATE-Berechtigung impliziert, erteilt werden, damit sie diese dynamische Verwaltungsfunktion abfragen können.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine Abfrage für die `Address`-Tabelle und anschließend eine Abfrage mithilfe der dynamischen Verwaltungssicht `sys.dm_db_missing_index_columns` ausgeführt, um die Tabellenspalten zurückzugeben, die keinen Index aufweisen.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT City, StateProvinceID, PostalCode  
FROM Person.Address  
WHERE StateProvinceID = 9;  
GO  
SELECT mig.*, statement AS table_name,  
    column_id, column_name, column_usage  
FROM sys.dm_db_missing_index_details AS mid  
CROSS APPLY sys.dm_db_missing_index_columns (mid.index_handle)  
INNER JOIN sys.dm_db_missing_index_groups AS mig ON mig.index_handle = mid.index_handle  
ORDER BY mig.index_group_handle, mig.index_handle, column_id;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sys.dm_db_missing_index_details &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)   
 [sys.dm_db_missing_index_groups &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-groups-transact-sql.md)   
 [sys.dm_db_missing_index_group_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-group-stats-transact-sql.md)  
  
  

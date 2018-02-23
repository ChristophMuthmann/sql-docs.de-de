---
title: sys.dm_tran_version_store_space_usage (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 04/30/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_tran_version_store_space_usage_TSQL
- sys.dm_tran_version_store_space_usage
- dm_tran_version_store_space_usage
- dm_tran_version_store_space_usage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_version_store_space_usage dynamic management view
ms.assetid: 7ab44517-0351-4f91-bdd9-7cf940f03c51
caps.latest.revision: 
author: savjani
ms.author: pariks
manager: ajayj
ms.workload: Inactive
ms.openlocfilehash: 3108394b7848047bac97ece004bf9c168b0e045c
ms.sourcegitcommit: 7ed8c61fb54e3963e451bfb7f80c6a3899d93322
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/20/2018
---
# <a name="sysdmtranversionstorespaceusage-transact-sql"></a>sys.dm_tran_version_store_space_usage (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Gibt eine Tabelle, in dem Gesamtspeicherplatz in Tempdb verwendeten Speicher Versionsdatensätze für jede Datenbank angezeigt. **sys.dm_tran_version_store_space_usage** is efficient and not expensive to run, as it does not navigate through individual version store records, and returns aggregated version store space consumed in tempdb per database.
  
Jeder Versionsdatensatz wird als Binärdaten zusammen mit protokollierungs- oder Statusinformationen gespeichert. Ähnlich wie Datensätze in Datenbanktabellen werden die Versionsspeicherdatensätze in 8192 Bytes umfassenden Seiten gespeichert. Falls ein Datensatz größer ist als 8192 Bytes, wird er in zwei unterschiedliche Datensätze geteilt.  
  
Da der Versionsdatensatz als Binärdaten gespeichert wird, treten keine Probleme mit unterschiedlichen Sortierungen aus unterschiedlichen Datenbanken auf. Verwendung **sys.dm_tran_version_store_space_usage** zu überwachen und Planen der Tempdb-Größe, die basierend auf der Version Store speicherplatznutzung von Datenbanken in einer SQL Server-Instanz.
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|Datenbank-ID der Datenbank.|  
|**reserved_page_count**|**bigint**|Gesamtanzahl der Seiten, reservierten in ' tempdb ', Version Datensätze in der Datenbank zu speichern.|  
|**reserved_space_kb**|**bigint**|In Kilobyte in ' tempdb ' für Version belegter Gesamtspeicherplatz speichern Datensätze in der Datenbank.|  
  
## <a name="permissions"></a>Berechtigungen  
Auf [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], erfordert `VIEW SERVER STATE` Berechtigung.   

## <a name="examples"></a>Beispiele  
 Die folgende Abfrage kann in Tempdb verwendeter Speicherplatz ermitteln verwendet werden, vom Versionsspeicher für jede Datenbank in eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instanz. 
  
```sql  
SELECT 
  DB_NAME(database_id) as 'Database Name',
  reserved_page_count,
  reserved_space_kb 
FROM sys.dm_tran_version_store_space_usage;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Database Name            reserved_page_count reserved_space_kb  
------------------------ -------------------- -----------  
msdb                      0                    0             
AdventureWorks2016        10                   80             
AdventureWorks2016DW      0                    0             
WideWorldImporters        20                   160             
```
 
## <a name="see-also"></a>Siehe auch  
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Dynamische Verwaltungssichten und Funktionen in Verbindung mit Transaktionen &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  

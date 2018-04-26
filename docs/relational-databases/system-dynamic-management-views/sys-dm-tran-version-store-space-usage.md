---
title: Sys.dm_tran_version_store_space_usage (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/24/2018
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
- sys.dm_tran_version_store_space_usage_TSQL
- sys.dm_tran_version_store_space_usage
- dm_tran_version_store_space_usage
- dm_tran_version_store_space_usage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_version_store_space_usage dynamic management view
ms.assetid: 7ab44517-0351-4f91-bdd9-7cf940f03c51
caps.latest.revision: 10
author: savjani
ms.author: pariks
manager: ajayj
ms.workload: Inactive
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 1459dd2b98ed9579bc1939c60c1e74e14157d0b6
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="sysdmtranversionstorespaceusage-transact-sql"></a>Sys.dm_tran_version_store_space_usage (Transact-SQL)
[!INCLUDE[tsql-appliesto-2016sp2-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-2016sp2-asdb-xxxx-xxx-md.md)]

Gibt eine Tabelle, in dem Gesamtspeicherplatz in Tempdb verwendeten Speicher Versionsdatensätze für jede Datenbank angezeigt. **Sys.dm_tran_version_store_space_usage** ist effizient und nicht über einzelne Version Store Datensätze navigieren, und gibt die aggregierten Version Store Speicherplatz in ' tempdb ' pro Datenbank ausgeführt wird, nicht aufwändig.
  
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
  

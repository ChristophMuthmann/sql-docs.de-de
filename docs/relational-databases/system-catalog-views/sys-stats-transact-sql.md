---
title: Sys.Stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.stats
- stats_TSQL
- sys.stats_TSQL
- stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.stats catalog view
ms.assetid: 42605c80-126f-460a-befb-a0b7482fae6a
caps.latest.revision: 41
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 82a5133ee5c5f8146264d14d1800dc8f500ac644
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysstats-transact-sql"></a>sys.stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Enthält eine Zeile für jedes Statistikobjekt, das für die Tabellen, Indizes und indizierte Sichten in der Datenbank vorhanden ist [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Jeder Index verfügt über eine entsprechende Statistikzeile mit dem gleichen Namen und der gleichen ID (**index_id** = **stats_id**), doch verfügt nicht jede Statistikzeile über einen entsprechenden Index.  
  
 Die Katalogsicht [stats_columns](../../relational-databases/system-catalog-views/sys-stats-columns-transact-sql.md) stellt Statistikinformationen für jede Spalte in der Datenbank bereit. Weitere Informationen zu Statistiken finden Sie unter [Statistiken](../../relational-databases/statistics/statistics.md).  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID des Objekts, zu dem diese Statistik gehört.|  
|**name**|**sysname**|Der Name der Statistik. Ist eindeutig innerhalb des Objekts.|  
|**stats_id**|**int**|Die ID der Statistik. Ist eindeutig innerhalb des Objekts.<br /><br />Wenn Statistiken einem Index entsprechen den *Stats_id* Wert ist identisch mit der *Index_id* Wert in der [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) -Katalogsicht angezeigt.|  
|**auto_created**|**bit**|Gibt an, ob die Statistik von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] automatisch erstellt wurde.<br /><br /> 0 = Statistik wurde nicht von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] automatisch erstellt.<br /><br /> 1 = Statistik wurde von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] automatisch erstellt.|  
|**user_created**|**bit**|Gibt an, ob die Statistik von einem Benutzer erstellt wurde.<br /><br /> 0 = Statistik wurde nicht von einem Benutzer erstellt.<br /><br /> 1 = Statistik wurde von einem Benutzer erstellt.|  
|**no_recompute**|**bit**|Gibt an, ob die Statistik mit der **NORECOMPUTE** -Option erstellt wurde.<br /><br /> 0 = Statistik wurde nicht mithilfe der **NORECOMPUTE** -Option erstellt.<br /><br /> 1 = Statistik wurde mithilfe der **NORECOMPUTE** -Option erstellt.|  
|**has_filter**|**bit**|0 = Statistik hat keinen Filter und wird für alle Zeilen berechnet.<br /><br /> 1 = Statistik hat einen Filter und wird nur für Zeilen berechnet, die der Filterdefinition entsprechen.|  
|**filter_definition**|**nvarchar(max)**|Ausdruck für die Teilmenge von Zeilen, die in der gefilterten Statistik enthalten sind.<br /><br /> NULL = Nicht gefilterte Statistik.|  
|**is_temporary**|**bit**|**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Geben Sie an, ob die Statistik temporär ist. Temporäre Statistik unterstützt [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] sekundären Datenbanken, die für nur-Lese-Zugriff aktiviert sind.<br /><br /> 0 = Statistik ist nicht temporär.<br /><br /> 1 = Statistik ist temporär.|  
|**is_incremental**|**bit**|**Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Gibt an, ob die Statistiken als inkrementelle Statistiken erstellt werden.<br /><br /> 0 = Die Statistiken sind nicht inkrementell.<br /><br /> 1 = Die Statistiken sind inkrementell.|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Beispiele  
 In den folgenden Beispielen werden alle Statistiken und Statistikspalten für die Tabelle `HumanResources.Employee` zurückgegeben.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT s.name AS statistics_name  
      ,c.name AS column_name  
      ,sc.stats_column_id  
FROM sys.stats AS s  
INNER JOIN sys.stats_columns AS sc   
    ON s.object_id = sc.object_id AND s.stats_id = sc.stats_id  
INNER JOIN sys.columns AS c   
    ON sc.object_id = c.object_id AND c.column_id = sc.column_id  
WHERE s.object_id = OBJECT_ID('HumanResources.Employee');  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten für Objekte &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Abfragen von SQL Server-Systemkatalogs – häufig gestellte Fragen](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [Statistiken](../../relational-databases/statistics/statistics.md)    
 [sys.dm_db_stats_properties (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md)   
 [Sys.dm_db_stats_histogram &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md)   
 [sys.stats_columns (Transact-SQL)](../../relational-databases/system-catalog-views/sys-stats-columns-transact-sql.md)
 

 

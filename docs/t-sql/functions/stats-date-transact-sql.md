---
title: STATS_DATE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 12/18/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STATS_DATE_TSQL
- STATS_DATE
dev_langs:
- TSQL
helpviewer_keywords:
- statistical information [SQL Server], last time updated
- STATS_DATE function
- query optimization statistics [SQL Server], last time updated
- last time statistics updated
- stats update date
ms.assetid: f9ec3101-1e41-489d-b519-496a0d6089fb
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: de308046d069b6efa6115cf1efae33af7c07128c
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/02/2018
---
# <a name="statsdate-transact-sql"></a>STATS_DATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt das Datum des letzten Updates für die Statistik einer Tabelle oder indizierten Sicht zurück.  
  
 Weitere Informationen zum Aktualisieren von Statistiken finden Sie unter [Statistiken](../../relational-databases/statistics/statistics.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
STATS_DATE ( object_id , stats_id )  
```  
  
## <a name="arguments"></a>Argumente  
 *object_id*  
 Die ID der Tabelle oder der indizierten Sicht, die die Statistik beinhaltet.  
  
 *stats_id*  
 Die ID des Statistikobjekts.  
  
## <a name="return-types"></a>Rückgabetypen  
 Gibt **"DateTime"** bei Erfolg. Gibt **NULL** ein Statistik-Blob nicht erstellt wurde.  
  
## <a name="remarks"></a>Hinweise  
 Systemfunktionen können in der Auswahlliste, in der WHERE-Klausel und überall dort verwendet werden, wo ein Ausdruck verwendet werden kann.  
 
 Statistiken Aktualisierungsdatum befindet sich in der [Statistik-Blob-Objekt](../../relational-databases/statistics/statistics.md#DefinitionQOStatistics) zusammen mit den [Histogramm](../../relational-databases/statistics/statistics.md#histogram) und [dichtevektor](../../relational-databases/statistics/statistics.md#density), nicht in den Metadaten. Wenn keine Daten gelesen werden, um statistische Daten zu generieren, die Statistik-Blob nicht erstellt, und das Datum ist nicht verfügbar. Dies ist der Fall für gefilterte Statistiken für die das Prädikat keine Zeilen zurückgibt, oder für neue, leere Tabellen.
 
 Wenn Statistiken einem Index entsprechen den *Stats_id* Wert in der [sys.stats](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md) -Katalogsicht ist identisch mit der *Index_id* Wert in der [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) -Katalogsicht angezeigt.
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der festen Datenbankrolle db_owner oder die Berechtigung, Metadaten für die Tabelle oder indizierte Sicht anzuzeigen.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-return-the-dates-of-the-most-recent-statistics-for-a-table"></a>A. Zurückgeben der Datumsangaben der letzten Statistik für eine Tabelle  
 Im folgenden Beispiel wird das Datum des letzten Updates für jedes Statistikobjekt in der `Person.Address`-Tabelle zurückgegeben.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT name AS stats_name,   
    STATS_DATE(object_id, stats_id) AS statistics_update_date  
FROM sys.stats   
WHERE object_id = OBJECT_ID('Person.Address');  
GO  
```  
  
 Wenn Statistiken einem Index entsprechen den *Stats_id* Wert in der [sys.stats](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md) -Katalogsicht ist identisch mit der *Index_id* Wert in der [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) -Katalogsicht, und die folgende Abfrage gibt die gleichen Ergebnisse wie die vorherige Abfrage. Wenn Statistiken keinem Index entsprechen, kommen sie in den sys.stats-Ergebnissen, nicht jedoch in den sys.indexes-Ergebnissen vor.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT name AS index_name,   
    STATS_DATE(object_id, index_id) AS statistics_update_date  
FROM sys.indexes   
WHERE object_id = OBJECT_ID('Person.Address');  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-learn-when-a-named-statistics-was-last-updated"></a>B. Erfahren Sie, wann eine benannte Statistik zuletzt aktualisiert wurde  
 Das folgende Beispiel erstellt Statistiken für die Spalte LastName der DimCustomer-Tabelle. Anschließend wird eine Abfrage aus, um das Datum der Statistik anzeigen ausgeführt. Klicken Sie dann es wurden Updates der Statistiken und führt die Abfrage erneut aus, um das aktualisierte Datum angezeigt.  
  
```sql
--First, create a statistics object  
USE AdventureWorksPDW2012;  
GO  
CREATE STATISTICS Customer_LastName_Stats  
ON AdventureWorksPDW2012.dbo.DimCustomer (LastName)  
WITH SAMPLE 50 PERCENT;  
GO  
  
--Return the date when Customer_LastName_Stats was last updated  
USE AdventureWorksPDW2012;  
GO  
SELECT stats_id, name AS stats_name,   
    STATS_DATE(object_id, stats_id) AS statistics_date  
FROM sys.stats s  
WHERE s.object_id = OBJECT_ID('dbo.DimCustomer')  
    AND s.name = 'Customer_LastName_Stats';  
GO  
  
--Update Customer_LastName_Stats so it will have a different timestamp in the next query  
GO  
UPDATE STATISTICS dbo.dimCustomer (Customer_LastName_Stats);  
  
--Return the date when Customer_LastName_Stats was last updated.  
SELECT stats_id, name AS stats_name,   
    STATS_DATE(object_id, stats_id) AS statistics_date  
FROM sys.stats s  
WHERE s.object_id = OBJECT_ID('dbo.DimCustomer')  
    AND s.name = 'Customer_LastName_Stats';  
GO    
```  
  
### <a name="c-view-the-date-of-the-last-update-for-all-statistics-on-a-table"></a>C. Das Datum der letzten Aktualisierung für alle Statistiken für eine Tabelle anzeigen  
 In diesem Beispiel gibt das Datum für zurück, wenn jede Statistikobjekt für die DimCustomer-Tabelle zuletzt aktualisiert wurde.  
  
```sql  
--Return the dates all statistics on the table were last updated.  
SELECT stats_id, name AS stats_name,   
    STATS_DATE(object_id, stats_id) AS statistics_date  
FROM sys.stats s  
WHERE s.object_id = OBJECT_ID('dbo.DimCustomer');  
GO  
```  
  
 Wenn Statistiken einem Index entsprechen den *Stats_id* Wert in der [sys.stats](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md) -Katalogsicht ist identisch mit der *Index_id* Wert in der [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) -Katalogsicht, und die folgende Abfrage gibt die gleichen Ergebnisse wie die vorherige Abfrage. Wenn Statistiken keinem Index entsprechen, kommen sie in den sys.stats-Ergebnissen, nicht jedoch in den sys.indexes-Ergebnissen vor.  
  
```sql  
USE AdventureWorksPDW2012;  
GO  
SELECT name AS index_name,   
    STATS_DATE(object_id, index_id) AS statistics_update_date  
FROM sys.indexes   
WHERE object_id = OBJECT_ID('dbo.DimCustomer');  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Systemfunktionen &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)   
 [Sp_autostats &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-autostats-transact-sql.md)   
 [Statistiken](../../relational-databases/statistics/statistics.md)    
 [sys.dm_db_stats_properties (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md)   
 [sys.stats](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)   
  
  


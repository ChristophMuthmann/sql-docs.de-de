---
title: Sys. fulltext_indexes (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- fulltext_indexes
- fulltext_indexes_TSQL
- sys.fulltext_indexes_TSQL
- sys.fulltext_indexes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fulltext_indexes catalog view
- full-text indexes [SQL Server], properties
ms.assetid: 7fc10fdc-370f-4927-bba0-b76108a7508e
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c6f19f05239629553594f52f30fe2eb4ef0854cb
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="sysfulltextindexes-transact-sql"></a>sys.fulltext_indexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Enthält eine Zeile pro Volltextindex eines Tabellenobjekts.  

|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID des Objekts, zu dem dieser Volltextindex gehört|  
|**unique_index_id**|**int**|ID des entsprechenden eindeutigen Volltextindexes, mit der der Volltextindex den Zeilen zugeordnet wird|  
|**fulltext_catalog_id**|**int**|ID des Volltextkatalogs, in dem der Volltextindex gespeichert ist|  
|**is_enabled**|**bit**|1 = Volltext ist derzeit aktiviert|  
|**change_tracking_state**|**char(1)**|Status der Änderungsnachverfolgung<br /><br /> M = Manual<br /><br /> A = Auto<br /><br /> O = Off|  
|**change_tracking_state_desc**|**nvarchar(60)**|Beschreibung des Status der Änderungsnachverfolgung<br /><br /> MANUAL<br /><br /> AUTO<br /><br /> OFF|  
|**has_crawl_completed**|**bit**|Der letzte Durchforstungsvorgang (Auffüllen), den der Volltextindex abgeschlossen hat.|  
|**crawl_type**|**char(1)**|Typ der aktuellen oder letzten Durchforstung<br /><br /> F = Vollständige Durchforstung<br /><br /> I = Inkrementeller, auf Timestamps basierende Durchforstung<br /><br /> U = Update-Durchforstung auf der Basis von Benachrichtigungen<br /><br /> P = Vollständige Durchforstung ist angehalten|  
|**crawl_type_desc**|**nvarchar(60)**|Beschreibung des aktuellen oder letzten Durchforstungstyps<br /><br /> FULL_CRAWL<br /><br /> INCREMENTAL_CRAWL<br /><br /> UPDATE_CRAWL<br /><br /> PAUSED_FULL_CRAWL|  
|**crawl_start_date**|**datetime**|Start der aktuellen oder letzten Durchforstung<br /><br /> NULL = Kein.|  
|**crawl_end_date**|**datetime**|Ende der aktuellen oder letzten Durchforstung<br /><br /> NULL = Kein.|  
|**incremental_timestamp**|**binary(8)**|Timestampwert, der für die nächste inkrementelle Durchforstung verwendet wird<br /><br /> NULL = Kein.|  
|**stoplist_id**|**int**|ID der [Stoppliste](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md) , dieser Volltextindex zugeordnet ist.|  
|**data_space_id**|**int**|Dateigruppe, in der sich dieser Volltextindex befindet.|  
|**property_list_id**|**int**|ID der diesem Volltextindex zugeordneten Sucheigenschaftenliste. NULL gibt an, dass dem Volltextindex keine Sucheigenschaftenliste zugeordnet ist. Um weitere Informationen zu dieser sucheigenschaftenliste abzurufen, verwenden die [Sys. registered_search_property_lists &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md) -Katalogsicht angezeigt.|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird ein Volltextindex für die `HumanResources.JobCandidate`-Tabelle der `AdventureWorks2012`-Beispieldatenbank verwendet. Im Beispiel werden die für den Volltextindex verwendete Objekt-ID der Tabelle, die Sucheigenschaftenlisten-ID und die Stopplisten-ID der Stoppliste zurückgegeben.  
  
> [!NOTE]  
>  Für das Codebeispiel, das diesem Volltextindex erstellt wird, finden Sie im Abschnitt "Beispiele" von [CREATE FULLTEXT INDEX &#40; Transact-SQL &#41; ](../../t-sql/statements/create-fulltext-index-transact-sql.md).  
  
```  
USE AdventureWorks2012;  
GO  
SELECT object_id, property_list_id, stoplist_id FROM sys.fulltext_indexes  
    where object_id = object_id('HumanResources.JobCandidate');   
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sys.fulltext_index_fragments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-fragments-transact-sql.md)   
 [sys.fulltext_index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)   
 [sys.fulltext_index_catalog_usages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-catalog-usages-transact-sql.md)   
 [Katalogsichten für Objekte &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Erstellen und Verwalten von Volltextindizes](../../relational-databases/search/create-and-manage-full-text-indexes.md)   
 [DROP FULLTEXT INDEX &#40; Transact-SQL &#41;](../../t-sql/statements/drop-fulltext-index-transact-sql.md)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)  
  
  

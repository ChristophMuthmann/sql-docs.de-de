---
title: fulltext_index_columns (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.fulltext_index_columns
- fulltext_index_columns
- sys.fulltext_index_columns_TSQL
- fulltext_index_columns_TSQL
dev_langs: TSQL
helpviewer_keywords:
- full-text indexes [SQL Server], columns
- sys.fulltext_index_columns catalog view
- full-text indexes [SQL Server], properties
ms.assetid: c34b8625-e53c-4281-ace6-d46230d5cb84
caps.latest.revision: "27"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ea0b235c347f9d06f0ea87462c62e5d02629ccd7
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysfulltextindexcolumns-transact-sql"></a>sys.fulltext_index_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Enthält eine Zeile für jede Spalte, die Teil eines Volltextindexes ist.    
 
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID des Objekts, dessen Teil dies ist.|  
|**column_id**|**int**|ID der Spalte, die Teil des Volltextindexes ist.|  
|**type_column_id**|**int**|ID der Typspalte, in der die vom Benutzer angegebene Dokumentdateierweiterung – ".doc", ".xls" usw. – des Dokuments in einer gegebenen Zeile gespeichert wird. Die Typspalte wird nur für Spalten angegeben, deren Daten während der Volltextindizierung eine Filterung erfordern. Dieser Wert ist NULL, falls dies nicht verfügbar ist. Weitere Informationen finden Sie unter [Konfigurieren und Verwalten von Filtern für die Suche](../../relational-databases/search/configure-and-manage-filters-for-search.md).|  
|**language_id**|**int**|LCID der Sprache, deren Wörtertrennung zum Indizieren dieser Volltextspalte verwendet wird.<br /><br /> 0 = Neutral.<br /><br /> Weitere Informationen finden Sie unter [Sys. fulltext_languages &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md).|  
|**statistical_semantics**|**int**|1 = Für diese Spalte ist die statistische Semantik zusätzlich zur Volltextindizierung aktiviert.|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten für Objekte &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  

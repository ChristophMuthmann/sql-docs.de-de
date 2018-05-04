---
title: Sys.pdw_column_distribution_properties (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 46b74f99-2e22-4dbd-872a-533fce0e239c
caps.latest.revision: 5
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: cdd674a663b8e5e6e18ef68c91fb07d2a59ac44e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="syspdwcolumndistributionproperties-transact-sql"></a>Sys.pdw_column_distribution_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Enthält Verteilungsinformationen zur für Spalten.  
  
|Spaltenname|Datentyp|Description|Bereich|  
|-----------------|---------------|-----------------|-----------|  
|**object_id**|**int**|Die ID des Objekts, zu dem die Spalte gehört.||  
|**column_id**|**int**|ID der Spalte.||  
|**distribution_ordinal**|**tinyint**|Ordinalzahl (1-basiert) innerhalb einer Gruppe der Verteilung.|0 = keine verteilungsspalte. 1 = [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] ist diese Spalte verwenden, um die übergeordnete Tabelle zu verteilen.|  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Datawarehouse und Parallel Datawarehouse-Katalogsichten](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  

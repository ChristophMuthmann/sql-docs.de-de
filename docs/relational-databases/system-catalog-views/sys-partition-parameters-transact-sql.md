---
title: Sys. partition_parameters (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- partition_parameters_TSQL
- partition_parameters
- sys.partition_parameters_TSQL
- sys.partition_parameters
dev_langs: TSQL
helpviewer_keywords: sys.partition_parameters catalog view
ms.assetid: 2012ed9d-3ea3-4c29-9b78-dfa54a392dce
caps.latest.revision: "23"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ea75798552d0521204e063663566b08b36a5797b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="syspartitionparameters-transact-sql"></a>sys.partition_parameters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  Enthält eine Zeile für jeden Parameter einer Partitionsfunktion.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**function_id**|**int**|ID der Partitionsfunktion, zu der dieser Parameter gehört|  
|**parameter_id**|**int**|ID des Parameters. Ist innerhalb der Partitionsfunktion eindeutig und beginnt mit 1.|  
|**system_type_id**|**tinyint**|ID des Systemtyps des Parameters. Entspricht der Spalte **system_type_id** der Katalogsicht **sys.types** .|  
|**max_length**|**smallint**|Die maximale Länge des Parameters in Byte.|  
|**Genauigkeit**|**tinyint**|Genauigkeit des Parameters, wenn dieser numerisch ist. Andernfalls ist der Wert 0.|  
|**Skalierung**|**tinyint**|Dezimalstellen des Parameters, wenn dieser numerisch ist. Andernfalls ist der Wert 0.|  
|**Sortierungsname**|**sysname**|Name der Sortierung des Parameters, wenn dieser auf Zeichen basiert. Andernfalls ist der Wert NULL.|  
|**user_type_id**|**int**|Die ID des Typs. Ist in der Datenbank eindeutig. Für Systemdatentypen gilt **user_type_id** = **system_type_id**.|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten für Partitionsfunktionen &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/partition-function-catalog-views-transact-sql.md)   
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Sys. partition_functions &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-partition-functions-transact-sql.md)   
 [Sys. partition_range_values &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-partition-range-values-transact-sql.md)  
  
  

---
title: Sys.pdw_nodes_indexes (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 261bcb7f-a906-4979-b274-bc5f1aa66426
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 77d90e50801abe9a8d9bd6c9ed67223486630b9e
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="syspdwnodesindexes-transact-sql"></a>sys.pdw_nodes_indexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Gibt die Indizes für [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].  
  
|Spaltenname|Datentyp|Description|Bereich|  
|-----------------|---------------|-----------------|-----------|  
|object_id|**int**|die ID des Objekts, zu dem dieser Index gehört.||  
|name|**sysname**|Der Name des Indexes. Der Name ist nur innerhalb des Objekts eindeutig. NULL = Heap||  
|index_id|**int**|die ID des Indexes. Index_id ist nur innerhalb des Objekts eindeutig.<br /><br /> 0 = Heap<br /><br /> 1 = Gruppierter Index<br /><br /> > 1 = nicht gruppierter Index||  
|Typ|**tinyint**|Typ des Index:<br /><br /> 0 = Heap<br /><br /> 1 = In einem Cluster gruppiert<br /><br /> 2 = nicht gruppiert<br /><br /> 5 = gruppierter xVelocity-Arbeitsspeicher optimierter columnstore-Index|  
|type_desc|**nvarchar(60)**|Beschreibung des Typs des Index:<br /><br /> HEAP<br /><br /> CLUSTERED<br /><br /> NONCLUSTERED<br /><br /> GRUPPIERTE COLUMNSTORE||  
|is_unique|**bit**|0 = Der Index ist nicht eindeutig.|Immer 0.|  
|data_space_id|**int**|die ID des Datenspeicherplatzes für diesen Index. Der Datenspeicherplatz ist entweder eine Dateigruppe oder ein Partitionsschema.<br /><br /> 0 = Object_id ist eine Funktion mit Tabellenrückgabe.||  
|ignore_dup_key|**bit**|0 = IGNORE_DUP_KEY ist OFF.|Immer 0.|  
|is_primary_key|**bit**|1 = Der Index ist Teil einer PRIMARY KEY-Einschränkung.|Immer 0.|  
|is_unique_constraint|**bit**|1 = Der Index ist Teil einer UNIQUE-Einschränkung.|Immer 0.|  
|fill_factor|**tinyint**|> 0 = FILLFACTOR-Prozentsatz, der beim Erstellen oder Neuerstellen des Index verwendet wurde.<br /><br /> 0 = Standardwert|Immer 0.|  
|is_padded|**bit**|0 = PADINDEX ist OFF.|Immer 0.|  
|is_disabled|**bit**|1 = Der Index ist deaktiviert.<br /><br /> 0 = Der Index ist nicht deaktiviert.||  
|is_hypothetical|**bit**|0 = Der Index ist nicht hypothetisch.|Immer 0.|  
|allow_row_locks|**bit**|1 = Der Index lässt Zeilensperren zu.|Immer 1.|  
|allow_page_locks|**bit**|1 = Der Index lässt Seitensperren zu.|Immer 1.|  
|has_filter|**bit**|0 = Index hat keinen Filter.|Immer 0.|  
|filter_definition|**nvarchar(max)**|Ausdruck für die Teilmenge von Zeilen, die im gefilterten Index enthalten sind.|Immer NULL.|  
|pdw_node_id|**int**|Der eindeutige Bezeichner einer [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] Knoten.|NOT NULL|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CONTROL SERVER-Berechtigung.  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Datawarehouse und Parallel Datawarehouse-Katalogsichten](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  

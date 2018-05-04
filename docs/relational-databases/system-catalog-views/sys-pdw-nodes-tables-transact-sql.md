---
title: Sys.pdw_nodes_tables (Transact-SQL) | Microsoft Docs
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
ms.assetid: 473b5d14-171b-4a16-9195-acf36d3f786c
caps.latest.revision: 8
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: d07f675a8352159386bde71899d6f59ea748acda
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="syspdwnodestables-transact-sql"></a>Sys.pdw_nodes_tables (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Enthält eine Zeile für jedes Tabellenobjekt, das ein Prinzipals entweder der Besitzer ist oder auf dem der Prinzipal eine Berechtigung erteilt wurde.  
  
|Spaltenname|Datentyp|Description|Bereich|  
|-----------------|---------------|-----------------|-----------|  
|\<geerbte Spalten >||Eine Liste der Spalten, die diese Sicht erbt, finden Sie unter [sys.objects](http://msdn.microsoft.com/en-us/c36fa71e-549a-4533-a6cd-1314d26f533f).||  
|lob_data_space_id|**int**||Immer 0.|  
|filestream_data_space_id|**int**|ID des Datenspeicherplatzes für eine FILESTREAM-Dateigruppe oder [!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|NULL|  
|max_column_id_used|**int**|Höchste Spalten-ID, die von dieser Tabelle verwendet.||  
|lock_on_bulk_load|**bit**|Die Tabelle wird bei Massenladevorgängen gesperrt.|TBD|  
|uses_ansi_nulls|**bit**|Beim Erstellen der Tabelle war die Datenbankoption SET ANSI_NULLS auf ON festgelegt.|1|  
|is_replicated|**bit**|1 = Tabelle mittels Replikation veröffentlicht wird.|0; Replikation wird nicht unterstützt.|  
|has_replication_filter|**bit**|1 = Die Tabelle hat einen Replikationsfilter.|0|  
|is_merge_published|**bit**|1 = Die Tabelle wird mithilfe der Mergereplikation veröffentlicht.|0; wird nicht unterstützt.|  
|is_sync_tran_subscribed|**bit**|1 = Die Tabelle wird mithilfe eines Abonnements mit sofortigem Update abonniert.|0; wird nicht unterstützt.|  
|has_unchecked_assembly_data|**bit**|1 = Die Tabelle enthält persistente Daten, die von einer Assembly abhängen, deren Definition bei der letzten ALTER ASSEMBLY-Anweisung geändert wurde. Der Wert wird nach der nächsten erfolgreichen Ausführung von DBCC CHECKDB oder DBCC CHECKTABLE auf 0 zurückgesetzt.|0; keine CLR-Unterstützung.|  
|text_in_row_limit|**int**|0 = Text in Zeile Option nicht festgelegt ist.|Immer 0.|  
|large_value_types_out_of_row|**bit**|1 = Umfangreiche Werttypen werden außerhalb der Zeile gespeichert.|Immer 0.|  
|is_tracked_by_cdc|**bit**|1 = Tabelle für Change Data Capture aktiviert ist|Immer 0; CDC werden nicht unterstützt.|  
|lock_escalation|**tinyint**|Der Wert der LOCK_ESCALATION-Option für die Tabelle: 2 = AUTO|Immer 2.|  
|lock_escalation_desc|**nvarchar(60)**|Eine textbeschreibung der Lock_escalation-Option.|Immer ꞌAUTOꞌ.|  
|pdw_node_id|**int**|Der eindeutige Bezeichner einer [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] Knoten.|NOT NULL|  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Datawarehouse und Parallel Datawarehouse-Katalogsichten](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  

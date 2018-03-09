---
title: ddl_history (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- cdc.ddl_history_TSQL
- cdc.ddl_history
dev_langs:
- TSQL
helpviewer_keywords:
- cdc.ddl_history
ms.assetid: cb97ea71-da2f-441a-bbd2-db1f5f48ab49
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 26ce592636c837f74cbbc8980b5d7cbd8742f78a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="cdcddlhistory-transact-sql"></a>cdc.ddl_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt eine Zeile für jede Änderung an der Datendefinitionssprache (DDL) zurück, die an Tabellen vorgenommen wurde, die für Change Data Capture aktiviert wurden. Mithilfe dieser Tabelle können Sie bestimmen, wann eine DDL-Änderung in einer Quelltabelle aufgetreten ist und was der Gegenstand dieser Änderung war. Für Quelltabellen ohne DDL-Änderungen sind in dieser Tabelle keine Einträge vorhanden.  
  
 Es wird empfohlen, die Systemtabellen nicht direkt abzufragen. Führen Sie stattdessen die [sp_cdc_get_ddl_history](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-ddl-history-transact-sql.md) gespeicherte Prozedur.  
   
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**source_object_id**|**int**|ID der Quelltabelle, auf die die DDL-Änderung angewendet wurde.|  
|**object_id**|**int**|ID der Änderungstabelle, die einer Aufzeichnungsinstanz für die Quelltabelle zugeordnet wurde.|  
|**required_column_update**|**bit**|Gibt an, dass der Datentyp einer aufgezeichneten Spalte in der Quelltabelle geändert wurde. Durch diese Änderung wurde die Spalte in der Änderungstabelle geändert.|  
|**ddl_command**|**nvarchar(max)**|DDL-Anweisung, die auf die Quelltabelle angewendet wurde.|  
|**ddl_lsn**|**binary(10)**|Protokollfolgenummer (Log Sequence Number, LSN), die dem Commit der DDL-Änderung zugeordnete wurde.|  
|**ddl_time**|**datetime**|Datum und Uhrzeit der DDL-Änderung an der Quelltabelle.|  
  
## <a name="see-also"></a>Siehe auch  
 [sp_cdc_help_change_data_capture &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)   
 [CDC. fn_cdc_get_all_changes_ &#60; Capture_instance &#62;  &#40; Transact-SQL &#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)  
  
  

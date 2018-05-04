---
title: CDC. change_tables (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- cdc.change_tables
- cdc.change_tables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- cdc.change_tables
ms.assetid: 3525a5f5-8d8b-46a8-b334-4b7cd9fb7c21
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 82549b60622ac4ae6e0107f73da5e8a336d2a3b2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="cdcchangetables-transact-sql"></a>cdc.change_tables (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt eine Zeile pro Änderungstabelle in der Datenbank zurück. Eine Änderungstabelle wird erstellt, wenn Change Data Capture für eine Quelltabelle aktiviert ist. Es wird empfohlen, die Systemtabellen nicht direkt abzufragen. Führen Sie stattdessen die [sp_cdc_help_change_data_capture](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md) gespeicherte Prozedur.  
  |Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID der Änderungstabelle. Ist innerhalb einer Datenbank eindeutig.|  
|**version**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> In [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] gibt diese Spalte immer den Wert 0 zurück.|  
|**source_object_id**|**int**|ID der Quelltabelle, für die Change Data Capture aktiviert ist.|  
|**capture_instance**|**sysname**|Name der Aufzeichnungsinstanz, der zur Benennung von instanzspezifischen Nachverfolgungsobjekten verwendet wird. Standardmäßig ist der Name aus dem quellschemanamen und dem Quelltabellennamen im Format abgeleitet *Schemaname_sourcename*.|  
|**start_lsn**|**binary(10)**|Protokollfolgenummer (Log Sequence Number, LSN), die den unteren Endpunkt zum Abfragen der in der Änderungstabelle enthaltenen Änderungsdaten darstellt.<br /><br /> NULL = Der untere Endpunkt wurde nicht erstellt.|  
|**end_lsn**|**binary(10)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> Für [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] gibt diese Spalte immer NULL zurück.|  
|**supports_net_changes**|**bit**|Unterstützung zum Abfragen von Nettoänderungen ist für die Änderungstabelle aktiviert.|  
|**has_drop_pending**|**bit**|Der Aufzeichnungsprozess hat die Benachrichtigung erhalten, dass die Quelltabelle gelöscht wurde.|  
|**role_name**|**sysname**|Der Name der Datenbankrolle zum Sperren des Zugriffs auf Änderungsdaten.<br /><br /> NULL = Eine Rolle wird nicht verwendet.|  
|**index_name**|**sysname**|Name des Indexes, mit dessen Hilfe Zeilen in der Quelltabelle eindeutig identifiziert werden. **Index_name** ist entweder der Name des Primärschlüsselindexes der Quelltabelle oder der Name eines eindeutigen Indexes angegeben, wenn Change Data Capture für die Quelltabelle aktiviert wurde.<br /><br /> NULL = Bei der Aktivierung von Change Data Capture verfügte die Quelltabelle über keinen Primärschlüssel, und es wurde auch kein eindeutiger Index angegeben.<br /><br /> Hinweis: Wenn Change Data Capture für eine Tabelle aktiviert ist, in dem ein Primärschlüssel vorhanden ist, verwendet die Change Data Capture-Funktion den Index, gleichgültig, ob nettoänderungen aktiviert ist oder nicht. Nachdem Change Data Capture aktiviert wurde, kann der Primärschlüssel nicht mehr geändert werden. Besitzt die Tabelle keinen Primärschlüssel, können Sie immer noch Change Data Capture aktivieren, jedoch nur dann, wenn Nettoänderungen auf false festgelegt wurden. Nachdem Change Data Capture aktiviert wurde, können Sie einen Primärschlüssel erstellen. Sie können den Primärschlüssel auch ändern, denn Change Data Capture verwendet den Primärschlüssel nicht.|  
|**filegroup_name**|**sysname**|Name der Dateigruppe, in der sich die Änderungstabelle befindet.<br /><br /> NULL = Die Änderungstabelle befindet sich in der Standarddateigruppe der Datenbank.|  
|**create_date**|**datetime**|Datum, an dem die Quelltabelle aktiviert wurde.|  
|**partition_switch**|**bit**|Gibt an, ob die **SWITCH PARTITION** -Befehl des **ALTER TABLE** ausgeführt werden kann, für eine Tabelle, die für Change Data Capture aktiviert ist. 0 bedeutet, dass der Partitionswechsel blockiert wird. Für nicht partitionierte Tabellen wird stets 1 zurückgegeben.|  
  
## <a name="see-also"></a>Siehe auch  
 [sp_cdc_help_change_data_capture &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)  
  
  

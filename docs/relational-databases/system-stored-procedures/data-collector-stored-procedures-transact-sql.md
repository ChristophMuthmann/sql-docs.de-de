---
title: "Gespeicherte Prozeduren (Transact-SQL) für den Datensammler | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- stored procedures [SQL Server], data collector
- system stored procedures [SQL Server], data collector
- data collector [SQL Server], stored procedures
ms.assetid: 9dd2824f-ea55-439b-8cd5-3a81fedb1432
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b9230680af9f7e0457f6c4c8379937c992db03dd
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="data-collector-stored-procedures-transact-sql"></a>Gespeicherte Prozeduren für den Datensammler (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  SQL Server unterstützt die folgenden gespeicherten Systemprozeduren, die verwendet werden, zum Arbeiten mit dem Datensammler und die folgenden Komponenten: Sammlungssätze, auflistelemente und Auflistungstypen.  
  
> [!IMPORTANT]  
>  Im Gegensatz zu regulären gespeicherten Prozeduren werden die Parameter für die gespeicherten Prozeduren des Datensammlers genau eingegeben und unterstützen die automatische Datentypkonvertierung nicht. Wenn diese Parameter nicht mit den richtigen Datentypen für Eingabeparameter aufgerufen werden, wie in der Argumentbeschreibung angegeben, gibt die gespeicherte Prozedur einen Fehler zurück.  
  
|||  
|-|-|  
|[sp_syscollector_create_collection_item](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-item-transact-sql.md)|[sp_syscollector_set_cache_window](../../relational-databases/system-stored-procedures/sp-syscollector-set-cache-window-transact-sql.md)|  
|[sp_syscollector_create_collection_set](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql.md)|[sp_syscollector_set_warehouse_database_name](../../relational-databases/system-stored-procedures/sp-syscollector-set-warehouse-database-name-transact-sql.md)|  
|[sp_syscollector_create_collector_type](../../relational-databases/system-stored-procedures/sp-syscollector-create-collector-type-transact-sql.md)|[sp_syscollector_set_warehouse_instance_name](../../relational-databases/system-stored-procedures/sp-syscollector-set-warehouse-instance-name-transact-sql.md)|  
|[sp_syscollector_delete_collection_item](../../relational-databases/system-stored-procedures/sp-syscollector-delete-collection-item-transact-sql.md)|[sp_syscollector_start_collection_set](../../relational-databases/system-stored-procedures/sp-syscollector-start-collection-set-transact-sql.md)|  
|[sp_syscollector_delete_collection_set](../../relational-databases/system-stored-procedures/sp-syscollector-delete-collection-set-transact-sql.md)|[sp_syscollector_stop_collection_set](../../relational-databases/system-stored-procedures/sp-syscollector-stop-collection-set-transact-sql.md)|  
|[sp_syscollector_delete_collector_type](../../relational-databases/system-stored-procedures/sp-syscollector-delete-collector-type-transact-sql.md)|[sp_syscollector_run_collection_set](../../relational-databases/system-stored-procedures/sp-syscollector-run-collection-set-transact-sql.md)|  
|[sp_syscollector_delete_execution_log_tree](../../relational-databases/system-stored-procedures/sp-syscollector-delete-execution-log-tree-transact-sql.md)|[sp_syscollector_update_collection_item](../../relational-databases/system-stored-procedures/sp-syscollector-update-collection-item-transact-sql.md)|  
|[sp_syscollector_disable_collector](../../relational-databases/system-stored-procedures/sp-syscollector-disable-collector-transact-sql.md)|[sp_syscollector_update_collection_set](../../relational-databases/system-stored-procedures/sp-syscollector-update-collection-set-transact-sql.md)|  
|[sp_syscollector_enable_collector](../../relational-databases/system-stored-procedures/sp-syscollector-enable-collector-transact-sql.md)|[sp_syscollector_update_collector_type](../../relational-databases/system-stored-procedures/sp-syscollector-update-collector-type-transact-sql.md)|  
|[sp_syscollector_set_cache_directory](../../relational-databases/system-stored-procedures/sp-syscollector-set-cache-directory-transact-sql.md)|[sp_syscollector_upload_collection_set](../../relational-databases/system-stored-procedures/sp-syscollector-upload-collection-set-transact-sql.md)|  
  
 Folgende gespeicherte Prozeduren dienen nur zur internen Verwendung:  
  
-   sp_syscollector_get_warehouse_connection_string  
  
-   sp_syscollector_set_warehouse_connection_password  
  
-   sp_syscollector_set_warehouse_connection_user  
  
-   sp_syscollector_event_oncollectionbegin  
  
-   sp_syscollector_event_oncollectionend  
  
-   sp_syscollector_event_onpackagebegin  
  
-   sp_syscollector_event_onpackageend  
  
-   sp_syscollector_event_onpackageupdate  
  
-   sp_syscollector_event_onerror  
  
-   sp_syscollector_event_onstatsupdate  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

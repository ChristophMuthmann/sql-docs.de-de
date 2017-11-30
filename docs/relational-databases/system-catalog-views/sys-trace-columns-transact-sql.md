---
title: trace_columns (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.trace_columns
- trace_columns
- trace_columns_TSQL
- sys.trace_columns_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.trace_columns catalog view
ms.assetid: 5c48eb09-9e9b-45dd-b151-ca39b026ece5
caps.latest.revision: "23"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7405b51d9071238a237a11ef7c0ceef78e2e7119
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="systracecolumns-transact-sql"></a>sys.trace_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die **trace_columns** -Katalogsicht enthält eine Liste von Spalten für alle Ablaufverfolgungsereignisse. Diese Spalten ändern sich für eine bestimmte Version von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] nicht.  
  
 Eine vollständige Liste der unterstützten Ablaufverfolgungsereignisse finden Sie unter [SQL Server Event Class Reference](../../relational-databases/event-classes/sql-server-event-class-reference.md).  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Verwenden Sie stattdessen die Katalogsichten für erweiterte Ereignisse.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**trace_event_id**|**smallint**|Eindeutige ID dieser Spalte.|  
|**name**|**vom Datentyp nvarchar(128)**|Eindeutiger Name dieser Spalte. Dieser Parameter ist nicht lokalisiert.|  
|**TYPE_NAME**|**vom Datentyp nvarchar(128)**|Datentypname dieser Spalte.|  
|**max_size**|**int**|Maximale Datengröße dieser Spalte in Bytes.|  
|**is_filterable**|**bit**|Gibt an, ob die Spalte in einer Filterdefinition verwendet werden kann.<br /><br /> 0 = "false"<br /><br /> 1 = TRUE|  
|**is_repeatable**|**bit**|Gibt an, ob in den Daten für wiederholte Spalten auf diese Spalte verwiesen werden kann.<br /><br /> 0 = "false"<br /><br /> 1 = TRUE|  
|**is_repeated_base**|**bit**|Gibt an, ob diese Spalte als eindeutiger Schlüssel für den Verweis auf wiederholte Daten verwendet werden kann.<br /><br /> 0 = "false"<br /><br /> 1 = TRUE|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten für Objekte &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Sys.Traces &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-traces-transact-sql.md)   
 [Sys. trace_categories &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-trace-categories-transact-sql.md)   
 [trace_events &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-trace-events-transact-sql.md)   
 [Sys. trace_event_bindings &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-trace-event-bindings-transact-sql.md)   
 [trace_subclass_values &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-trace-subclass-values-transact-sql.md)  
  
  

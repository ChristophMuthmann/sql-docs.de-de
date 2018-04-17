---
title: "\"trace_xe_action_map\" (Transact-SQL) | Microsoft Docs"
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
- trace_xe_action_map_TSQL
- trace_xe_action_map
dev_langs:
- TSQL
helpviewer_keywords:
- extended events [SQL Server], tables
- trace_xe_action_map
ms.assetid: 208a1413-ce7f-4521-b765-d74723627302
caps.latest.revision: 11
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d75ed8bd81491e7095f13a794a818d4b2532f176
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="extended-events-tables---tracexeactionmap"></a>Tabellen für erweiterte Ereignisse - "trace_xe_action_map"
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Enthält eine Zeile für jede Aktion für erweiterte Ereignisse, die der Spalten-ID für eine SQL-Ablaufverfolgung zugeordnet ist. Diese Tabelle wird in der master-Datenbank im Sys-Schema gespeichert.  
  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|trace_event_id|**smallint**|Die ID der Spalte für die SQL-Ablaufverfolgung, die zugeordnet wird.|  
|package_name|**nvarchar(60)**|Der Name des Pakets für erweiterte Ereignisse, in dem sich die zugeordnete Aktion befindet.|  
|xe_action_name|**nvarchar(60)**|Der Name der Aktion für erweiterte Ereignisse, die der Spalte für die SQL-Ablaufverfolgung zugeordnet ist.|  
  
## <a name="remarks"></a>Hinweise  
 Mit der folgenden Abfrage können Sie Aktionen für erweiterte Ereignisse identifizieren, die Spalten für die SQL-Ablaufverfolgung entsprechen:  
  
```  
SELECT tc.name AS trace_column, am.package_name, am.xe_action_name  
FROM sys.trace_columns AS tc  
INNER JOIN sys.trace_xe_action_map AS am  
   ON tc.trace_column_id = am.trace_column_id  
```  
  
 Spalten für die SQL-Ablaufverfolgung, die keinen Aktionen zugeordnet sind, sind nicht in der Tabelle enthalten.  
  
## <a name="see-also"></a>Siehe auch  
 [trace_xe_event_map &#40;Transact-SQL&#41;](../../relational-databases/system-tables/extended-events-tables-trace-xe-event-map.md)  
  
  

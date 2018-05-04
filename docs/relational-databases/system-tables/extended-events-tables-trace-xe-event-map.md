---
title: "\"trace_xe_event_map\" (Transact-SQL) | Microsoft Docs"
ms.custom: ''
ms.date: 03/14/2017
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
- trace_xe_event_map_TSQL
- trace_xe_event_map
dev_langs:
- TSQL
helpviewer_keywords:
- trace_xe_event_map
- extended events [SQL Server], tables
ms.assetid: 537aa292-3540-47e8-be28-56dc01abc343
caps.latest.revision: 10
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a8822d39f4a1743981224cd607cf830db526f697
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="extended-events-tables---tracexeeventmap"></a>Tabellen für erweiterte Ereignisse - "trace_xe_event_map"
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Enthält eine Zeile für jedes einer SQL-Ablaufverfolgungs-Ereignisklasse zugeordnete Ereignis für erweiterte Ereignisse. Diese Tabelle wird in der master-Datenbank im Sys-Schema gespeichert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|trace_column_id|**smallint**|Die ID der zuzuordnenden SQL-Ablaufverfolgungs-Ereignisklasse.|  
|package_name|**nvarchar(60)**|Der Name des Pakets für erweiterte Ereignisse, in dem sich das zugeordnete Ereignis befindet.|  
|xe_event_name|**nvarchar(60)**|Der Name des der SQL-Ablaufverfolgungs-Ereignisklasse zugeordneten Ereignisses für erweiterte Ereignisse.|  
  
## <a name="remarks"></a>Hinweise  
 Mit der folgenden Abfrage können Sie Ereignisse für erweiterte Ereignisse identifizieren, die Spalten für die SQL-Ereignisklassen entsprechen:  
  
```  
SELECT te.name, xe.package_name, xe.xe_event_name  
FROM sys.trace_events AS te  
LEFT JOIN sys.trace_xe_event_map AS xe  
   ON te.trace_event_id = xe.trace_event_id  
WHERE xe.trace_event_id IS NOT NULL  
```  
  
 Nicht alle Ereignisklassen verfügen über entsprechende Ereignisse für erweiterte Ereignisse. Sie können die Ereignisklassen, die über keine Entsprechung in erweiterten Ereignissen verfügen, mithilfe der folgenden Abfrage auflisten:  
  
```  
SELECT te.trace_event_id, te.name  
FROM sys.trace_events AS te  
LEFT JOIN sys.trace_xe_event_map AS xe  
   ON te.trace_event_id = xe.trace_event_id  
WHERE xe.trace_event_id IS NULL  
```  
  
 In der vorherigen Abfrage beziehen sich die meisten zurückgegebenen Ereignisklassen auf die Überwachung. Es wird empfohlen, für die Überwachung [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Audit verwenden. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Audit verwendet erweiterte Ereignisse, um eine Überwachung zu erstellen. Weitere Informationen finden Sie unter [SQL Server Audit &#40;Datenbankmodul&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  
  
## <a name="see-also"></a>Siehe auch  
 [trace_xe_action_map &#40;Transact-SQL&#41;](../../relational-databases/system-tables/extended-events-tables-trace-xe-action-map.md)  
  
  

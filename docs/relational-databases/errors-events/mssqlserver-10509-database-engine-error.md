---
title: MSSQLSERVER_10509 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 10509 (Database Engine error)
ms.assetid: e9dd5357-ee3d-420a-9a89-d12ab5404e73
caps.latest.revision: "9"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1f20d57d41659acbead6597dc10324fedd5410b6
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver10509"></a>MSSQLSERVER_10509
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|10509|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|PG_INVALID_STMT|  
|Meldungstext|Die Planhinweisliste „%.\*ls“ kann nicht erstellt werden, weil die mit **@stmt** oder **@statement_start_offset** angegebene Anweisung einen Syntaxfehler enthält oder für die Planhinweisliste nicht verwendet werden kann. Geben Sie nur eine gültige [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung oder eine gültige Startposition der Anweisung im Batch an. Fragen Sie die Spalte statement_start_offset in der dynamischen sys.dm_exec_query_stats-Verwaltungsfunktion ab, um eine gültige Startposition zu erhalten.|  
  
## <a name="explanation"></a>Erklärung  
Die mit **@stmt** oder **@statement_start_offset** angegebene Anweisung enthält einen Syntaxfehler oder kann für die Planhinweisliste nicht verwendet werden.  
  
## <a name="user-action"></a>Benutzeraktion  
Geben Sie nur eine gültige [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung oder eine gültige Startposition der Anweisung im Batch an. Fragen Sie die Spalte statement_start_offset in der dynamischen sys.dm_exec_query_stats-Verwaltungsfunktion ab, um eine gültige Startposition zu erhalten.  
  
## <a name="see-also"></a>Siehe auch  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[Planhinweislisten](~/relational-databases/performance/plan-guides.md)  
[sys.dm_exec_query_stats &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  

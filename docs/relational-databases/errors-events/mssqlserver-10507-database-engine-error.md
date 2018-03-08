---
title: MSSQLSERVER_10507 | Microsoft-Dokumentation
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
helpviewer_keywords: 10507 (Database Engine error)
ms.assetid: cd83fa81-ac37-4eda-a3c3-17610b051de2
caps.latest.revision: "9"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3bad7ac89e53fb1de9c814cc64618f966e328b66
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver10507"></a>MSSQLSERVER_10507
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|10507|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|PG_STMT_DOES_NOT_MATCH|  
|Meldungstext|Die Planhinweisliste „%.\*ls“ kann nicht erstellt werden, weil die mit **@stmt** und **@module_or_batch** oder mit **@plan_handle** und **@statement_start_offset** angegebene Anweisung keiner Anweisung im festgelegten Modul oder Batch entspricht. Ändern Sie die Werte, um eine Übereinstimmung mit einer Anweisung im Modul oder Batch herzustellen.|  
  
## <a name="explanation"></a>Erklärung  
Eine Anweisung im festgelegten Modul oder Batch konnte nicht der angegebenen Anweisung bzw. dem Offsetwert der Anweisung zugeordnet werden.  
  
## <a name="user-action"></a>Benutzeraktion  
Ändern Sie die angegebenen Parameterwerte, um eine Übereinstimmung mit einer Anweisung im Modul oder Batch herzustellen.  
  
## <a name="see-also"></a>Siehe auch  
[Planhinweislisten](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  

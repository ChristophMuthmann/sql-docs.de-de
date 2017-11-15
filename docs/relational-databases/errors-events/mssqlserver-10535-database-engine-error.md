---
title: MSSQLSERVER_10535 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 10535 (Database Engine error)
ms.assetid: 478fd978-11d9-4155-8329-f599fdbec14b
caps.latest.revision: "9"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: d5c5cda49e791ada03e8069d4892d72b664cb13e
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver10535"></a>MSSQLSERVER_10535
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|10535|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|PG_NO_PLAN|  
|Meldungstext|Die Planhinweisliste '%.*ls' kann nicht erstellt werden, weil kein Plan im entsprechenden Plancache für das Planhandle gefunden wurde. Geben Sie ein zwischengespeichertes Planhandle an. Fragen Sie die dynamische sys.dm_exec_query_stats-Verwaltungssicht ab, um eine Liste der zwischengespeicherten Planhandles zu erhalten.|  
  
## <a name="explanation"></a>Erklärung  
Es wurde kein Plan im Plancache gefunden, der dem angegebenen Planhandle entspricht.  
  
## <a name="user-action"></a>Benutzeraktion  
Geben Sie ein zwischengespeichertes Planhandle an. Fragen Sie die dynamische sys.dm_exec_query_stats-Verwaltungssicht ab, um eine Liste der zwischengespeicherten Planhandles zu erhalten.  
  
## <a name="see-also"></a>Siehe auch  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
[sys.dm_exec_query_stats &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
  

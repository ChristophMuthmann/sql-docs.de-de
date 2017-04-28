---
title: MSSQLSERVER_10535 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 10535 (Database Engine error)
ms.assetid: 478fd978-11d9-4155-8329-f599fdbec14b
caps.latest.revision: 9
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4ba53cf6d726ee80d2a3604ccc66f36212d48f47
ms.lasthandoff: 04/11/2017

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
  


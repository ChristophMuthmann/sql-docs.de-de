---
title: MSSQLSERVER_17300 | Microsoft-Dokumentation
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 17300 (Database Engine error)
ms.assetid: c1d6bfb6-28af-4df6-8087-25807602d282
caps.latest.revision: 18
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3df70ddeff20cc79efd3736b3507a285c2d0b8b6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver17300"></a>MSSQLSERVER_17300
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|17300|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|PROC_OUT_OF_SYSTASK_SESSIONS|  
|Meldungstext|Der SQL Server war nicht in der Lage, einen neuen Systemtask auszuführen, entweder aufgrund von unzureichendem Speicher oder weil die Anzahl der konfigurierten Sitzungen die maximale Anzahl der auf dem Server zulässigen Sitzungen übersteigt. Überprüfen Sie, ob der Server über ausreichenden Arbeitsspeicher verfügt. Sie können mithilfe von sp_configure und der Option ‚Benutzerverbindungen’ die maximale Anzahl der zulässigen Benutzerverbindungen überprüfen. Verwenden Sie sys.dm_exec_sessions, um die aktuelle Anzahl von Sitzungen einschließlich der Benutzerprozesse zu überprüfen.|  
  
## <a name="explanation"></a>Erklärung  
Die Ausführung eines neuen Systemtasks ist aufgrund von unzureichendem Speicher oder weil die Anzahl der konfigurierten Sitzungen auf dem Server überschritten wurde, fehlgeschlagen.  
  
## <a name="user-action"></a>Benutzeraktion  
Überprüfen Sie, ob der Server über ausreichenden Arbeitsspeicher verfügt. Überprüfen Sie die aktuelle Anzahl von Systemtasks mit sys.dm_exec_sessions und überprüfen Sie den konfigurierten Wert der maximalen Anzahl von Benutzerverbindungen mit sp_configure.  
  
Führen Sie die folgenden Tasks entsprechend aus:  
  
-   Fügen Sie dem Server mehr Arbeitsspeicher hinzu.  
  
-   Beenden Sie eine oder mehrere Sitzungen.  
  
-   Erhöhen Sie die maximal zulässige Anzahl von Benutzerverbindungen auf dem Server.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[sp_configure &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
[Serverkonfigurationsoptionen &#40;Transact-SQL&#41;](~/database-engine/configure-windows/server-configuration-options-sql-server.md)  
[sys.dm_exec_sessions &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
[Konfigurieren der Serverkonfigurationsoption Benutzerverbindungen](~/database-engine/configure-windows/configure-the-user-connections-server-configuration-option.md)  
[KILL &#40;Transact-SQL&#41;](~/t-sql/language-elements/kill-transact-sql.md)  
  

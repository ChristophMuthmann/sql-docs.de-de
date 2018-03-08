---
title: MSSQLSERVER_41301 | Microsoft-Dokumentation
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
helpviewer_keywords: 41301 (Database Engine error)
ms.assetid: c6127e1e-2846-4ee9-bc42-2d896ea9730e
caps.latest.revision: "10"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ac85372b238cb049398979a710cde0d4c75f41c0
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver41301"></a>MSSQLSERVER_41301
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Ereignis-ID|41301|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|COMMIT_DEPENDENCY_FAILURE|  
|Meldungstext|Eine vorherige Transaktion, zu der die aktuelle Transaktion eine Abhängigkeit eingegangen war, wurde abgebrochen. Die aktuelle Transaktion kann keinen Commit mehr ausführen.|  
  
## <a name="explanation"></a>Erklärung  
Bei der Transaktion trat ein Abhängigkeitsfehler auf, sie kann nicht abgeschlossen werden.  
  
Dieser Fehler kann auch durch zu viele abhängige Transaktionen verursacht werden. Jede Schreibtransaktion kann über eine begrenzte Anzahl abhängiger Transaktionen verfügen. Dieser Fehler kann beispielsweise auftreten, wenn zu viele Lesetransaktionen versuchen, eine Abhängigkeit von der Updatetransaktion herzustellen.  
  
## <a name="user-action"></a>Benutzeraktion  
Erledigen Sie keine Bearbeitung der Transaktion. Rufen Sie ROLLBACK TRAN auf, um ein Rollback für die Transaktion auszuführen. Weitere Informationen finden Sie unter [In-Memory OLTP &#40;Arbeitsspeicheroptimierung&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
## <a name="see-also"></a>Siehe auch  
[Aktivieren und Deaktivieren von Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](~/database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)  
  

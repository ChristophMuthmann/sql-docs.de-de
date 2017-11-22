---
title: MSSQLSERVER_1401 | Microsoft-Dokumentation
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
helpviewer_keywords: 1401 (Database Engine error)
ms.assetid: 02928770-aa63-4509-8713-406c73e4cedc
caps.latest.revision: "15"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c8f23f441da3e1cb597f0749152a95eb4386905a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver1401"></a>MSSQLSERVER_1401
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|1401|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|DBM_MASTERSTARTUP|  
|Meldungstext|Fehler beim Starten der Masterthreadroutine für die Datenbankspiegelung mit folgender Ursache: %ls. Beheben Sie die Fehlerursache, und starten Sie den SQL Server-Dienst erneut.|  
  
## <a name="explanation"></a>Erklärung  
Beim Starten des Spiegelungssteuerungsthreads ist ein Fehler aufgetreten.  
  
## <a name="user-action"></a>Benutzeraktion  
Suchen Sie im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Fehlerprotokoll nach dem entsprechenden Fehler, der vor dieser Meldung angezeigt wurde. Beheben Sie die Fehlerursache, und starten Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Dienst (MSSQLSERVER) anschließend erneut.  
  
## <a name="see-also"></a>Siehe auch  
[Starten, Beenden, Anhalten, Fortsetzen und Neustarten des Datenbankmoduls, SQL Server-Agent oder des SQL Server-Browsers](~/database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)  
  

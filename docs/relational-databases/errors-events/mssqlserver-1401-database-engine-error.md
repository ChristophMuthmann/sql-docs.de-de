---
title: MSSQLSERVER_1401 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 1401 (Database Engine error)
ms.assetid: 02928770-aa63-4509-8713-406c73e4cedc
caps.latest.revision: "15"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: fdae41b3011a31be94777a9ffc05dd9304d0f315
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver1401"></a>MSSQLSERVER_1401
  
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
  

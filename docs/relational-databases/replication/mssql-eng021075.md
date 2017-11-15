---
title: MSSQL_ENG021075 | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: MSSQL_ENG021075 error
ms.assetid: c8c29543-d1f6-49d5-b6c8-e8c3aa373090
caps.latest.revision: "14"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b18878ed0b8d1bf3de1216f54daafac690fa6d71
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="mssqleng021075"></a>MSSQL_ENG021075
    
## <a name="message-details"></a>Meldungsdetails  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|21075|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Symbolischer Name||  
|Meldungstext|Die Anfangsmomentaufnahme für die %1!s!-Veröffentlichung ist noch nicht verfügbar.|  
  
## <a name="explanation"></a>Erklärung  
 Der Fehler MSSQL_ENG021075 wird ausgelöst, wenn der Verteilungs-Agent oder der Merge-Agent gestartet wird, bevor der Momentaufnahme-Agent mit dem Generieren der Momentaufnahme fertig ist.  
  
## <a name="user-action"></a>Benutzeraktion  
 Wenn der Momentaufnahme-Agent für die Veröffentlichung seit der Erstellung des Abonnements oder seit dem letzten erneuten Initialisieren des Abonnements nicht mehr gestartet wurde, starten Sie den Momentaufnahme-Agent, und lassen Sie ihn die Momentaufnahme fertig generieren, bevor Sie den Verteilungs-Agent oder den Merge-Agent starten. Weitere Informationen finden Sie unter [Erstellen und Anwenden der Momentaufnahme](../../relational-databases/replication/create-and-apply-the-snapshot.md).  
  
 Wenn der Momentaufnahme-Agent die Momentaufnahme nicht fertig generiert, überprüfen Sie den Verlauf des Momentaufnahme-Agents auf Fehler, und sorgen Sie für deren Behebung. Informationen zum Anzeigen des Agentstatus und der Fehlerinformationen im Replikationsmonitor finden Sie unter [Anzeigen von Informationen und Ausführen von Aufgaben für die einer Veröffentlichung zugeordneten Agents &#40;Replikationsmonitor&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-publication-agents.md).  
  
 Wenn der Fehler weiterhin auftritt, erhöhen Sie die Protokollierungsstufe des Agents, und geben Sie eine Ausgabedatei für das Protokoll an. Je nach Zusammenhang, in dem der Fehler auftritt, finden Sie hier möglicherweise die Schritte, die zum Fehler führen, und/oder weitere Fehlermeldungen.  
  
## <a name="see-also"></a>Siehe auch  
 [Fehler- und Ereignisreferenz &#40;Replikation&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  

---
title: MSSQL_ENG021076 | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- MSSQL_ENG021076 error
ms.assetid: 612e5c59-ba3e-49c3-a3df-56bac3d850a2
caps.latest.revision: 15
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b4a4a884022b36bb2e0c819c234724b4335170c2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="mssqleng021076"></a>MSSQL_ENG021076
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>Meldungsdetails  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|21076|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Symbolischer Name||  
|Meldungstext|Die Anfangsmomentaufnahme für den %1!s!-Artikel ist noch nicht verfügbar.|  
  
## <a name="explanation"></a>Erklärung  
 Der Fehler MSSQL_ENG021076 wird ausgelöst, wenn der Verteilungs-Agent gestartet wird, bevor der Momentaufnahme-Agent mit dem Generieren der Momentaufnahmen fertig ist. Dieser Fehler wird nur ausgelöst, wenn die Veröffentlichung einen einzigen Artikel enthält. Wenn die Veröffentlichung mehr als einen Artikel enthält, wird stattdessen der Fehler MSSQL_ENG021075 ausgelöst. Weitere Informationen finden Sie unter [MSSQL_ENG021075](../../relational-databases/replication/mssql-eng021075.md).  
  
## <a name="user-action"></a>Benutzeraktion  
 Wenn der Momentaufnahme-Agent für die Veröffentlichung seit der Erstellung des Abonnements oder seit dem letzten erneuten Initialisieren des Abonnements nicht mehr gestartet wurde, starten Sie den Momentaufnahme-Agent, und lassen Sie ihn die Momentaufnahme fertig generieren, bevor Sie den Verteilungs-Agent starten. Weitere Informationen finden Sie unter [Erstellen und Anwenden der Momentaufnahme](../../relational-databases/replication/create-and-apply-the-snapshot.md).  
  
 Wenn der Momentaufnahme-Agent die Momentaufnahme nicht fertig generiert, überprüfen Sie den Verlauf des Momentaufnahme-Agents auf Fehler, und sorgen Sie für deren Behebung. Informationen zum Anzeigen des Agentstatus und der Fehlerinformationen im Replikationsmonitor finden Sie unter [Anzeigen von Informationen und Ausführen von Aufgaben für die einer Veröffentlichung zugeordneten Agents &#40;Replikationsmonitor&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-publication-agents.md).  
  
 Wenn der Fehler weiterhin auftritt, erhöhen Sie die Protokollierungsstufe des Agents, und geben Sie eine Ausgabedatei für das Protokoll an. Je nach Zusammenhang, in dem der Fehler auftritt, finden Sie hier möglicherweise die Schritte, die zum Fehler führen, und/oder weitere Fehlermeldungen.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Fehler- und Ereignisreferenz &#40;Replikation&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  

---
title: MSSQL_ENG020554 | Microsoft-Dokumentation
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
- MSSQL_ENG020554 error
ms.assetid: ef1a1b88-b2ab-43e8-99cd-163a973262d6
caps.latest.revision: 16
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 48abf8d981154d166bfe9539747b0a2a6e554b4c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="mssqleng020554"></a>MSSQL_ENG020554
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>Meldungsdetails  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|20554|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Symbolischer Name||  
|Meldungstext|Vom Replikations-Agent wurde in %ld Minuten keine Statusmeldung protokolliert. Möglicherweise reagiert der Agent nicht mehr, oder das System ist stark ausgelastet. Überprüfen Sie, ob Datensätze an das Ziel repliziert werden und ob die Verbindungen mit dem Abonnenten, Verleger und Verteiler noch aktiv sind.|  
  
## <a name="explanation"></a>Erklärung  
 Der **Überprüfung des Replikations-Agents** -Auftrag wird nach Ablauf einer angegebenen Zeitspanne (standardmäßig alle 10 Minuten) ausgeführt, um den Status der einzelnen Replikations-Agents zu überprüfen. Wenn ein Agent keine Statusmeldungen protokolliert hat, seitdem der Agentüberprüfungsauftrag zum letzten Mal ausgeführt wurde, wird der Fehler MSSQL_ENG020554 ausgelöst. Vom Agent wird erwartet, dass er zumindest Verlaufsmeldungen protokolliert, auch wenn keinerlei Replikationsaktivität stattgefunden hat. Dass der Replikations-Agent nicht wie erwartet reagiert, heißt nicht unbedingt, dass er beendet wurde oder ausgefallen ist (bei Ausfall eines Agents wird der Fehler MSSQL_ENG020536 ausgelöst).  
  
 Für das Auslösen des Fehlers MSSQL_ENG020554 kann es folgende Gründe geben:  
  
-   Der Agent ist ausgelastet.  
  
     Wenn der Agent so ausgelastet ist, dass er auf den Abruf durch den Agentüberprüfungsauftrag nicht reagieren kann, kann der Agentüberprüfungsauftrag auch nicht berichten, ob der Replikations-Agent ordnungsgemäß funktioniert. Für die Auslastung des Replikations-Agents kann es mehrere Gründe geben. So ist es z. B. möglich, dass viele Daten repliziert werden müssen, oder es gibt Probleme im Anwendungsentwurf bzw. in der Konfiguration, die dazu führen, dass bestimmte Prozesse sehr lange brauchen.  
  
-   Der Agent kann sich auf einem der Computer in der Topologie nicht anmelden.  
  
     Alle Agents besitzen einen **-LoginTimeOut** -Parameter (Standardwert: 15 Sekunden), der bestimmt, wie lange ein Agent versucht, sich bei einem Replikationsknoten anzumelden. Dies gilt auch für Merge-Agents, die sich beim Verleger anmelden. Wenn der Wert für den **-LoginTimeOut** -Parameter höher ist als das Zeitintervall, in dem der Replikations-Agent den Überprüfungsauftrag ausführt, kann das eigentliche Problem für die Ausgabe dieses Fehlers ein Anmeldungsproblem sein: Der MSSQL_ENG020554-Fehler wird ausgelöst, bevor der Agent in der Lage ist, einen spezifischeren Fehler auszulösen.  
  
## <a name="user-action"></a>Benutzeraktion  
 Die notwendige Aktion hängt von der Ursache des Fehlers ab:  
  
-   Für alle Fälle, in denen dieser Fehler ausgegeben wird, gilt Folgendes:  
  
     Überprüfen Sie die Fehlerdetails im Replikationsmonitor, und starten Sie den Replikationsmonitor neu, falls er beendet wurde. Den Fehlerdetails ist vielleicht genauer zu entnehmen, warum der Agent nicht ordnungsgemäß ausgeführt wurde. Wenn der Agent ausgeführt wird, sollten Sie ihn auch nicht beenden und wieder starten, weil sich dadurch das Problem verschlimmern kann. Informationen zum Anzeigen des Agentstatus und der Fehlerdetails im Replikationsmonitor finden Sie in den folgenden Themen:  
  
    -   Informationen zum Momentaufnahme-Agent, Protokolllese-Agent und Warteschlangenlese-Agent finden Sie unter [Anzeigen von Informationen und Ausführen von Aufgaben für die einer Veröffentlichung zugeordneten Agents &#40;Replikationsmonitor&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-publication-agents.md).  
  
    -   Informationen zum Verteilungs-Agent und zum Merge-Agent finden Sie unter [Anzeigen von Informationen und Ausführen von Aufgaben für die einem Abonnement zugeordneten Agents &#40;Replikationsmonitor&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md).  
  
-   Wenn der Fehler häufig ausgelöst wird, weil der Agent ausgelastet ist, haben Sie folgende Möglichkeiten:  
  
     Ändern Sie Ihre Anwendung so, dass der Agent weniger Zeit für die Verarbeitung benötigt.  
  
     Erhöhen Sie im Dialogfeld **Auftragseigenschaften** das Zeitintervall, in dem der Agentstatus geprüft wird. Informationen zum Zugreifen auf dieses Dialogfeld für Replikationsaufträge finden Sie unter [Anzeigen von Informationen und Ausführen von Aufgaben für einen Verleger &#40;Replikationsmonitor&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publisher-replication-monitor.md).  
  
-   Wenn ein Agent sich nicht bei einem der Computer in der Topologie anmelden kann, haben Sie folgende Möglichkeiten:  
  
     Es wird empfohlen, den Wert für den **-LoginTimeOut** -Parameter auf einen niedrigeren Wert festzulegen als das Intervall, in dem der Auftrag zur Überprüfung des Replikations-Agents ausgeführt wird. Mitunter wird der Wert für **-LoginTimeOut** aufgrund von Netzwerkproblemen, die zu einem Timeout bei Anmeldungen führen können, relativ hoch angesetzt. Wenn der Wert für **-LoginTimeOut** niedriger festgelegt wird, kann die Replikation spezifischere Informationen zu Fehlern melden, sodass Sie Anmeldeprobleme diagnostizieren können, die durch Probleme bei den Berechtigungen, durch Netzwerkprobleme oder durch andere Probleme hervorgerufen werden. Agentparameter können in den Agentprofilen und in der Befehlszeile angegeben werden. Weitere Informationen finden Sie in den folgenden Themen:  
  
    -   [Arbeiten mit Replikations-Agent-Profilen](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
    -   [Anzeigen und Ändern von Befehlszeilenparametern des Replikations-Agents &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
  
    -   [Replication Agent Executables Concepts](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)zugeordnet ist.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Replikations-Agentverwaltung](../../relational-databases/replication/agents/replication-agent-administration.md)   
 [Fehler- und Ereignisreferenz &#40;Replikation&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [Replikationsverteilungs Agent](../../relational-databases/replication/agents/replication-distribution-agent.md)   
 [Replikationsprotokolllese-Agent](../../relational-databases/replication/agents/replication-log-reader-agent.md)   
 [Replikationsmerge-Agent](../../relational-databases/replication/agents/replication-merge-agent.md)   
 [Warteschlangenlese-Agent](../../relational-databases/replication/agents/replication-queue-reader-agent.md)   
 [Replication Snapshot Agent](../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
  

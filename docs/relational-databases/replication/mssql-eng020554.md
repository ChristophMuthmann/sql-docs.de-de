---
title: "MSSQL_ENG020554 | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "MSSQL_ENG020554 (Fehler)"
ms.assetid: ef1a1b88-b2ab-43e8-99cd-163a973262d6
caps.latest.revision: 16
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 16
---
# MSSQL_ENG020554
    
## Meldungsdetails  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|20554|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Symbolischer Name||  
|Meldungstext|Vom Replikations-Agent wurde in %ld Minuten keine Statusmeldung protokolliert. Möglicherweise reagiert der Agent nicht mehr, oder das System ist stark ausgelastet. Überprüfen Sie, ob Datensätze an das Ziel repliziert werden und ob die Verbindungen mit dem Abonnenten, Verleger und Verteiler noch aktiv sind.|  
  
## Erklärung  
 Die **Replikations-Agents** Auftrag in einem angegebenen Intervall (standardmäßig 10 Minuten) ausgeführt wird, um den Status der einzelnen Replikations-Agents zu überprüfen. Wenn ein Agent keine Statusmeldungen protokolliert hat, seitdem der Agentüberprüfungsauftrag zum letzten Mal ausgeführt wurde, wird der Fehler MSSQL_ENG020554 ausgelöst. Vom Agent wird erwartet, dass er zumindest Verlaufsmeldungen protokolliert, auch wenn keinerlei Replikationsaktivität stattgefunden hat. Dass der Replikations-Agent nicht wie erwartet reagiert, heißt nicht unbedingt, dass er beendet wurde oder ausgefallen ist (bei Ausfall eines Agents wird der Fehler MSSQL_ENG020536 ausgelöst).  
  
 Für das Auslösen des Fehlers MSSQL_ENG020554 kann es folgende Gründe geben:  
  
-   Der Agent ist ausgelastet.  
  
     Wenn der Agent so ausgelastet ist, dass er auf den Abruf durch den Agentüberprüfungsauftrag nicht reagieren kann, kann der Agentüberprüfungsauftrag auch nicht berichten, ob der Replikations-Agent ordnungsgemäß funktioniert. Für die Auslastung des Replikations-Agents kann es mehrere Gründe geben. So ist es z. B. möglich, dass viele Daten repliziert werden müssen, oder es gibt Probleme im Anwendungsentwurf bzw. in der Konfiguration, die dazu führen, dass bestimmte Prozesse sehr lange brauchen.  
  
-   Der Agent kann sich auf einem der Computer in der Topologie nicht anmelden.  
  
     Alle Agents besitzen einen Parameter **- LoginTimeout-Parameter** (festgelegt auf 15 Sekunden, in der Standardeinstellung), die steuert, wie langen eines Agents versucht, die Anmeldung bei einem Replikationsknoten eine Merge-Agents mit dem Verleger. Wenn die **- LoginTimeOut** Wert höher ist als das Intervall, in dem der Replikations-Agent den Überprüfungsauftrag ausgeführt wird, eine Anmeldung Problem ist möglicherweise die Ursache des Fehlers: Fehler MSSQL_ENG020554 wird ausgelöst, bevor der Agent möglich ist, einen spezifischeren Fehler auszulösen.  
  
## Benutzeraktion  
 Die notwendige Aktion hängt von der Ursache des Fehlers ab:  
  
-   Für alle Fälle, in denen dieser Fehler ausgegeben wird, gilt Folgendes:  
  
     Überprüfen Sie die Fehlerdetails im Replikationsmonitor, und starten Sie den Replikationsmonitor neu, falls er beendet wurde. Den Fehlerdetails ist vielleicht genauer zu entnehmen, warum der Agent nicht ordnungsgemäß ausgeführt wurde. Wenn der Agent ausgeführt wird, sollten Sie ihn auch nicht beenden und wieder starten, weil sich dadurch das Problem verschlimmern kann. Informationen zum Anzeigen des Agentstatus und der Fehlerdetails im Replikationsmonitor finden Sie in den folgenden Themen:  
  
    -   Der Snapshot-Agent, Protokolllese-Agent und Warteschlangenlese-Agent, finden Sie unter [Anzeigen von Informationen und Ausführen von Aufgaben für die Agents verknüpft sind mit einer Publikation & #40; Der Replikationsmonitor & #41;](../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md).  
  
    -   Der Snapshot-Agent und Merge-Agent finden Sie unter [Anzeigen von Informationen und Ausführen von Aufgaben für die Agents einem Abonnement zugeordneten & #40; Der Replikationsmonitor & #41;](../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md).  
  
-   Wenn der Fehler häufig ausgelöst wird, weil der Agent ausgelastet ist, haben Sie folgende Möglichkeiten:  
  
     Ändern Sie Ihre Anwendung so, dass der Agent weniger Zeit für die Verarbeitung benötigt.  
  
     Sie können das Intervall, in dem der Agent Status wird geprüft, erhöhen die **Auftragseigenschaften** (Dialogfeld). Informationen zum Zugreifen auf dieses Dialogfeld für Replikationsaufträge finden Sie unter [Anzeigen von Informationen und Ausführen von Aufgaben für einen Verleger & #40; Der Replikationsmonitor & #41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publisher-replication-monitor.md).  
  
-   Wenn ein Agent sich nicht bei einem der Computer in der Topologie anmelden kann, haben Sie folgende Möglichkeiten:  
  
     Es wird empfohlen, die **- LoginTimeOut** Wert festgelegt werden, niedriger als das Intervall, in dem der Replikations-Agent den Überprüfungsauftrag ausgeführt wird. In einigen Fällen den Wert der **- LoginTimeOut** angesetzt aufgrund von Netzwerkproblemen, die Anmeldungen zu einem Timeout führen. Wenn die **- LoginTimeOut** niedriger festgelegt wird, Replikation kann mehr Fehler, und Sie können die Login-Problemen, die von den Berechtigungen, Netzwerkprobleme oder durch andere Probleme verursacht werden. Agentparameter können in den Agentprofilen und in der Befehlszeile angegeben werden. Weitere Informationen finden Sie in den folgenden Themen:  
  
    -   [Arbeiten mit Replikations-Agent-Profilen](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
    -   [Anzeigen und Ändern von Replikations-Agent-Befehlszeilenparameter & #40; SQL Server Management Studio & #41;](../../relational-databases/replication/agents/view and modify replication agent command prompt parameters.md)  
  
    -   [Replikations-Agent ausführbare Konzepte](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
## Siehe auch  
 [Replikations-Agent-Verwaltung](../../relational-databases/replication/agents/replication-agent-administration.md)   
 [Fehler und Ereignisreferenz & #40; Replikation & #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [Replikationsverteilungs-Agent](../../relational-databases/replication/agents/replication-distribution-agent.md)   
 [Replikationsprotokolllese-Agent](../../relational-databases/replication/agents/replication-log-reader-agent.md)   
 [Replikationsmerge-Agent](../../relational-databases/replication/agents/replication-merge-agent.md)   
 [Warteschlangenlese-Agent der Microsoft SQL Server-Replikation](../../relational-databases/replication/agents/replication-queue-reader-agent.md)   
 [Replikationsmomentaufnahme-Agent](../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
  
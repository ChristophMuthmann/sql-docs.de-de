---
title: "Replikations-Agents (&#220;bersicht) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Verteilungs-Agent"
  - "Agents [SQL Server-Replikation]"
  - "Warteschlangenlese-Agent, Informationen zum Warteschlangenlese-Agent"
  - "Warteschlangenlese-Agent"
  - "Merge-Agent, Informationen zum Merge-Agent"
  - "Protokolllese-Agent, Informationen zum Protokolllese-Agent"
  - "Replikation [SQL Server], Agents und Profile"
  - "Protokolllese-Agent"
  - "Verteilungs-Agent, Informationen zum Verteilungs-Agent"
  - "Agents [SQL Server-Replikation], Informationen zu Agents"
  - "Merge-Agent"
  - "Momentaufnahme-Agent, Informationen zum Momentaufnahme-Agent"
  - "Momentaufnahme-Agent"
ms.assetid: a35ecd7d-f130-483c-87e3-ddc8927bb91b
caps.latest.revision: 42
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 42
---
# Replikations-Agents (&#220;bersicht)
  Von der Replikation werden eine Reihe eigenständiger Programme verwendet, die Agents genannt werden. Diese Agents führen die mit dem Nachverfolgen von Änderungen und Verteilen von Daten verbundenen Aufgaben aus. Standardmäßig werden Replikations-Agents als Aufträge ausgeführt, die unter dem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Agent geplant werden. Zum Ausführen dieser Aufträge muss der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Agent ausgeführt werden. Replikations-Agents können auch in der Befehlszeile und von Anwendungen ausgeführt werden, die Replikationsverwaltungsobjekte (RMO) verwenden. Replikations-Agents können im [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Replikationsmonitor und in [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]verwaltet werden.  
  
## SQL Server-Agent  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Agent beinhaltet und plant die Agents, die bei der Replikation verwendet werden, und bietet so eine einfache Möglichkeit, die Replikations-Agents auszuführen. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Agent steuert und überwacht auch Vorgänge, die nicht im Rahmen der Replikation erfolgen. Weitere Informationen finden Sie unter [Configure SQL Server Agent](../../../ssms/agent/configure-sql-server-agent.md).  
  
> [!IMPORTANT]  
>  Standardmäßig ist der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Agent-Dienst bei der Installation von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] deaktiviert, es sei denn, Sie haben den automatischen Start des Diensts während der Installation explizit ausgewählt. Weitere Informationen zum Starten der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Agent-Dienst finden Sie unter [starten, beenden oder Anhalten der SQL Server-Agent-Dienst](../../../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md).  
  
## Momentaufnahme-Agent  
 Der Momentaufnahme-Agent wird in der Regel bei allen Replikationstypen verwendet. Er bereitet Schema und Anfangsdatendateien der veröffentlichten Tabellen und anderer Objekte vor, speichert die Momentaufnahmedateien und zeichnet Informationen zur Synchronisierung in der Verteilungsdatenbank auf. Der Momentaufnahme-Agent wird auf dem Verteiler ausgeführt. Weitere Informationen finden Sie unter [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md).  
  
## Protokolllese-Agent  
 Der Protokolllese-Agent wird mit der Transaktionsreplikation verwendet. Er verschiebt Transaktionen, die für die Replikation markiert wurden, vom Transaktionsprotokoll auf dem Verleger zur Verteilungsdatenbank. Jede Datenbank, die mithilfe der Transaktionsreplikation veröffentlicht wird, verfügt über einen eigenen Protokolllese-Agent. Dieser Agent wird auf dem Verteiler ausgeführt und stellt die Verbindung mit dem Verleger her (der Verteiler kann sich auf demselben Computer befinden wie der Verleger). Weitere Informationen finden Sie unter [Replication Log Reader Agent](../../../relational-databases/replication/agents/replication-log-reader-agent.md).  
  
## Verteilungs-Agent  
 Der Verteilungs-Agent wird mit der Momentaufnahmereplikation und Transaktionsreplikation verwendet. Er wendet die Anfangsmomentaufnahme auf den Abonnenten an und verschiebt Transaktionen aus der Verteilungsdatenbank auf die Abonnenten. Der Verteilungs-Agent wird für Pushabonnements auf dem Verteiler und für Pullabonnements auf dem Abonnenten ausgeführt. Weitere Informationen finden Sie unter [Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md).  
  
## Merge-Agent  
 Der Merge-Agent wird mit der Mergereplikation verwendet. Er wendet die Anfangsmomentaufnahme auf den Abonnenten an, verschiebt auftretende inkrementelle Datenänderungen und stimmt sie ab. Jedes Mergeabonnement besitzt einen Merge-Agent, der eine Verbindung sowohl zum Verleger als auch zum Abonnenten herstellt und beide aktualisiert. Der Merge-Agent wird für Pushabonnements auf dem Verteiler und für Pullabonnements auf dem Abonnenten ausgeführt. Der Merge-Agent ladet standardmäßig Änderungen vom Abonnenten auf den Verleger hoch und ladet dann die Änderungen vom Verleger auf den Abonnenten herunter. Weitere Informationen finden Sie unter [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md).  
  
## Warteschlangenlese-Agent  
 Der Warteschlangenlese-Agent wird beim verzögerten Update über eine Warteschlange mit der Transaktionsreplikation verwendet. Der Agent wird auf dem Verteiler ausgeführt und verschiebt auf dem Abonnenten vorgenommene Änderungen zurück auf den Verleger. Im Gegensatz zum Verteilungs-Agent und dem Merge-Agent ist nur eine Instanz des Warteschlangenlese-Agents vorhanden, um alle Verleger und Veröffentlichungen für einen bestimmten Verteiler zu bedienen. Weitere Informationen zum Warteschlangenlese-Agent finden Sie unter [Replication Queue Reader Agent](../../../relational-databases/replication/agents/replication-queue-reader-agent.md). Weitere Informationen zu aktualisierbaren Abonnements finden Sie unter [Updatable Subscriptions for Transactional Replication](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md).  
  
## Aufträge zur Replikationswartung  
 Die Replikation schließt eine Reihe von Wartungsaufträgen ein, mit denen geplante und bedarfsgesteuerte Wartungen ausgeführt werden. Weitere Informationen finden Sie unter [Replikations-Agent-Verwaltung](../../../relational-databases/replication/agents/replication-agent-administration.md).  
  
## Siehe auch  
 [Starten Sie und beenden Sie eines Replikations-Agents & #40. SQL Server Management Studio & #41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)   
 [Führen Sie Replikationswartungsaufträge & #40. SQL Server Management Studio & #41;](../../../relational-databases/replication/administration/run-replication-maintenance-jobs-sql-server-management-studio.md)   
 [Ausführbare Konzepte für die Programmierung von Replikations-Agents](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)   
 [Replikations-Agent-Verwaltung](../../../relational-databases/replication/agents/replication-agent-administration.md)  
  
  
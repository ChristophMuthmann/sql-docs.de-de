---
title: Replikations-Agents (Übersicht) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
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
- Distribution Agent
- agents [SQL Server replication]
- Queue Reader Agent, about Queue Reader Agent
- Queue Reader Agent
- Merge Agent, about Merge Agent
- Log Reader Agent, about Log Reader Agent
- replication [SQL Server], agents and profiles
- Log Reader Agent
- Distribution Agent, about Distribution Agent
- agents [SQL Server replication], about agents
- Merge Agent
- Snapshot Agent, about Snapshot Agent
- Snapshot Agent
ms.assetid: a35ecd7d-f130-483c-87e3-ddc8927bb91b
caps.latest.revision: 42
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 84365e80f664a15e1257a02f60d7e7b9e62e5364
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="replication-agents-overview"></a>Replikations-Agents (Übersicht)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Von der Replikation werden eine Reihe eigenständiger Programme verwendet, die Agents genannt werden. Diese Agents führen die mit dem Nachverfolgen von Änderungen und Verteilen von Daten verbundenen Aufgaben aus. Standardmäßig werden Replikations-Agents als Aufträge ausgeführt, die unter dem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Agent geplant werden. Zum Ausführen dieser Aufträge muss der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Agent ausgeführt werden. Replikations-Agents können auch in der Befehlszeile und von Anwendungen ausgeführt werden, die Replikationsverwaltungsobjekte (RMO) verwenden. Replikations-Agents können im [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Replikationsmonitor und in [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]verwaltet werden.  
  
## <a name="sql-server-agent"></a>SQL Server-Agent  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Agent beinhaltet und plant die Agents, die bei der Replikation verwendet werden, und bietet so eine einfache Möglichkeit, die Replikations-Agents auszuführen. Der[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Agent steuert und überwacht auch Vorgänge, die nicht im Rahmen der Replikation erfolgen. Weitere Informationen finden Sie unter [Configure SQL Server Agent](http://msdn.microsoft.com/library/2e361a62-9e92-4fcd-80d7-d6960f127900).  
  
> [!IMPORTANT]  
>  Standardmäßig ist der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Agent-Dienst bei der Installation von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] deaktiviert, es sei denn, Sie haben den automatischen Start des Diensts während der Installation explizit ausgewählt. Weitere Informationen zum Starten des [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Agent-Dienstes finden Sie unter [Start, Stop, or Pause the SQL Server Agent Service](http://msdn.microsoft.com/library/c95a9759-dd30-4ab6-9ab0-087bb3bfb97c)verwaltet werden.  
  
## <a name="snapshot-agent"></a>Momentaufnahme-Agent  
 Der Momentaufnahme-Agent wird in der Regel bei allen Replikationstypen verwendet. Er bereitet Schema und Anfangsdatendateien der veröffentlichten Tabellen und anderer Objekte vor, speichert die Momentaufnahmedateien und zeichnet Informationen zur Synchronisierung in der Verteilungsdatenbank auf. Der Momentaufnahme-Agent wird auf dem Verteiler ausgeführt. Weitere Informationen finden Sie unter [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md).  
  
## <a name="log-reader-agent"></a>Protokolllese-Agent  
 Der Protokolllese-Agent wird mit der Transaktionsreplikation verwendet. Er verschiebt Transaktionen, die für die Replikation markiert wurden, vom Transaktionsprotokoll auf dem Verleger zur Verteilungsdatenbank. Jede Datenbank, die mithilfe der Transaktionsreplikation veröffentlicht wird, verfügt über einen eigenen Protokolllese-Agent. Dieser Agent wird auf dem Verteiler ausgeführt und stellt die Verbindung mit dem Verleger her (der Verteiler kann sich auf demselben Computer befinden wie der Verleger). Weitere Informationen finden Sie unter [Replication Log Reader Agent](../../../relational-databases/replication/agents/replication-log-reader-agent.md).  
  
## <a name="distribution-agent"></a>Verteilungs-Agent  
 Der Verteilungs-Agent wird mit der Momentaufnahmereplikation und Transaktionsreplikation verwendet. Er wendet die Anfangsmomentaufnahme auf den Abonnenten an und verschiebt Transaktionen aus der Verteilungsdatenbank auf die Abonnenten. Der Verteilungs-Agent wird für Pushabonnements auf dem Verteiler und für Pullabonnements auf dem Abonnenten ausgeführt. Weitere Informationen finden Sie unter [Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md).  
  
## <a name="merge-agent"></a>Merge-Agent  
 Der Merge-Agent wird mit der Mergereplikation verwendet. Er wendet die Anfangsmomentaufnahme auf den Abonnenten an, verschiebt auftretende inkrementelle Datenänderungen und stimmt sie ab. Jedes Mergeabonnement besitzt einen Merge-Agent, der eine Verbindung sowohl zum Verleger als auch zum Abonnenten herstellt und beide aktualisiert. Der Merge-Agent wird für Pushabonnements auf dem Verteiler und für Pullabonnements auf dem Abonnenten ausgeführt. Der Merge-Agent ladet standardmäßig Änderungen vom Abonnenten auf den Verleger hoch und ladet dann die Änderungen vom Verleger auf den Abonnenten herunter. Weitere Informationen finden Sie unter [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md).  
  
## <a name="queue-reader-agent"></a>Warteschlangenlese-Agent  
 Der Warteschlangenlese-Agent wird beim verzögerten Update über eine Warteschlange mit der Transaktionsreplikation verwendet. Der Agent wird auf dem Verteiler ausgeführt und verschiebt auf dem Abonnenten vorgenommene Änderungen zurück auf den Verleger. Im Gegensatz zum Verteilungs-Agent und dem Merge-Agent ist nur eine Instanz des Warteschlangenlese-Agents vorhanden, um alle Verleger und Veröffentlichungen für einen bestimmten Verteiler zu bedienen. Weitere Informationen zum Warteschlangenlese-Agent finden Sie unter [Replication Queue Reader Agent](../../../relational-databases/replication/agents/replication-queue-reader-agent.md). Weitere Informationen zu aktualisierbaren Abonnements finden Sie unter [Updatable Subscriptions for Transactional Replication](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md).  
  
## <a name="replication-maintenance-jobs"></a>Aufträge zur Replikationswartung  
 Die Replikation schließt eine Reihe von Wartungsaufträgen ein, mit denen geplante und bedarfsgesteuerte Wartungen ausgeführt werden. Weitere Informationen finden Sie unter [Replikations-Agent-Verwaltung](../../../relational-databases/replication/agents/replication-agent-administration.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Starten und Beenden eines Replikations-Agents &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)   
 [Ausführen von Aufträgen zur Replikationswartung &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/administration/run-replication-maintenance-jobs-sql-server-management-studio.md)   
 [Ausführbare Konzepte für die Programmierung von Replikations-Agents](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)   
 [Replikations-Agent-Verwaltung](../../../relational-databases/replication/agents/replication-agent-administration.md)  
  
  

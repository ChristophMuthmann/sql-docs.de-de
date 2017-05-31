---
title: Replikations-Agent-Verwaltung | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/24/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Snapshot Agent, administering
- Log Reader Agent, administering
- Queue Reader Agent, administering
- shared agents [SQL Server replication]
- Merge Agent, administering
- Distribution Agent, administering
- agents [SQL Server replication], administering
- replication cleanup jobs [SQL Server]
- administering replication, agents
- replication [SQL Server], administering
- independent agents [SQL Server replication]
ms.assetid: f27186b8-b1b2-4da0-8b2b-91f632c2ab7e
caps.latest.revision: 48
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ee0ddd687702068508c54ea60a533fc3c5c75b10
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="replication-agent-administration"></a>Replikations-Agent-Verwaltung
  Die Replikations-Agents führen viele der der Replikation zugeordneten Aufgaben aus. Zu diesen Aufgaben gehören das Erstellen von Kopien des Schemas und der Daten, das Ermitteln von Aktualisierungen auf dem Verleger oder dem Abonnenten und das Weitergeben von Änderungen zwischen Servern. Standardmäßig werden die Replikations-Agents unter [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Agentauftragsschritten ausgeführt. Bei den Agents handelt es sich einfach nur um ausführbare Dateien, d. h., sie können auch direkt von der Befehlszeile und von Batchskripts aus aufgerufen werden. Jeder Replikations-Agent unterstützt einen Satz von Laufzeitparametern, mit denen gesteuert wird, wie der Agent ausgeführt wird. Diese Parameter werden in einem Agentprofil oder auf der Befehlszeile angegeben.  
  
> [!IMPORTANT]  
>  Standardmäßig ist der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Agent-Dienst bei der Installation von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] deaktiviert, es sei denn, Sie haben den automatischen Start des Diensts während der Installation explizit ausgewählt.  
  
 Die Replikations-Agentdateien befinden sich unter [!INCLUDE[ssInstallPathVar](../../../includes/ssinstallpathvar-md.md)]\COM. Die folgende Tabelle enthält eine Aufstellung der Namen der ausführbaren Replikationsdateien und der Dateien. Klicken Sie auf den Link für einen Agent, um sich die zugehörige Parameterreferenz anzeigen zu lassen.  
  
|Ausführbare Agent-Dateien|Dateiname|  
|----------------------|---------------|  
|[Replikationsmomentaufnahme-Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)|snapshot.exe|  
|[Replikationsverteilungs-Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)|distrib.exe|  
|[Replikationsprotokolllese-Agent](../../../relational-databases/replication/agents/replication-log-reader-agent.md)|logread.exe|  
|[Warteschlangenlese-Agent](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)|qrdrsvc.exe|  
|[Replikationsmerge-Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)|replmerg.exe|  
  
 Zusätzlich zu den Replikations-Agents besitzt die Replikation eine Reihe von Aufträgen, die geplante und Bedarfswartungen ausführen.  
  
 **So führen Sie Agents und Wartungsaufträge aus**  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] und Replikationsmonitor: [Starten und Beenden eines Replikations-Agents &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)  
  
-   Replikationsprogrammierung: [Ausführbare Konzepte für die Programmierung von Replikations-Agents](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)  
  
## <a name="agent-profiles"></a>Agentprofile  
 Wenn die Replikation konfiguriert wird, wird ein Satz Agentprofile auf dem Verteiler installiert. Ein Agentprofil enthält eine Reihe Parameter, die bei jeder Ausführung des Agents zur Anwendung kommen: Jeder Agent meldet sich während seines Startprozesses beim Verteiler an und fragt die Parameter in seinem Profil ab. Die Replikation stellt ein Standardprofil für jeden Agent und zusätzliche vordefinierte Profile für den Protokolllese-Agent, den Verteilungs-Agent und den Merge-Agent bereit. Neben den bereitgestellten Profilen können Sie Profile erstellen, die sich für Ihre Anwendungsanforderungen eignen. Weitere Informationen finden Sie unter [Replication Agent Profiles](../../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
 Informationen zum direkten Angeben von Befehlszeilenparametern finden Sie unter [ Ausführbare Konzepte für die Programmierung von Replikations-Agents](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
## <a name="monitoring-replication-agents"></a>Überwachen der Replikations-Agents  
 Im Replikationsmonitor können Sie Informationen zu den einzelnen Replikations-Agents anzeigen und agentbezogene Aufgaben ausführen. Die folgende Liste enthält alle Agents, die Registerkarten im Replikationsmonitor, auf denen die Agents zu finden sind, und einen Verweis darauf, wo Sie Informationen zum Zugreifen auf die jeweilige Registerkarte finden:  
  
-   Die folgenden Agents sind Veröffentlichungen im Replikationsmonitor zugeordnet:  
  
    -   Momentaufnahme-Agent  
  
    -   Protokolllese-Agent  
  
    -   Warteschlangenlese-Agent  
  
     Auf die Informationen und Aufgaben zu diesen Agents können Sie über die Registerkarte **Agents** zugreifen. Weitere Informationen finden Sie unter [Anzeigen von Informationen und Ausführen von Aufgaben für die einer Veröffentlichung zugeordneten Agents &#40;Replikationsmonitor&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-publication-agents.md).  
  
-   Die folgenden Agents sind Abonnements im Replikationsmonitor zugeordnet:  
  
    -   Verteilungs-Agent  
  
    -   Merge-Agent  
  
     Auf die Informationen und Aufgaben im Zusammenhang mit diesen Agents kann über die folgenden Registerkarten zugegriffen werden: **Überwachungsliste für Abonnements** (verfügbar für jeden Verleger) bzw. **Alle Abonnements** (verfügbar für jede Veröffentlichung). Weitere Informationen finden Sie unter [Anzeigen von Informationen und Ausführen von Aufgaben für die einem Abonnement zugeordneten Agents &#40;Replikationsmonitor&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md).  
  
## <a name="independent-and-shared-agents"></a>Unabhängige und freigegebene Agents  
 Ein unabhängiger Agent ist ein Agent, der ein Abonnement bedient. Ein freigegebener Agent bedient mehrere Abonnements. Wenn mehrere Abonnements, die denselben freigegebenen Agent verwenden, synchronisiert werden müssen, warten sie standardmäßig in einer Warteschlange. Der freigegebene Agent bedient die Abonnements einzeln nacheinander. Die Latenzzeit wird reduziert, wenn unabhängige Agents verwendet werden, da der Agent immer dann bereitsteht, wenn das Abonnement synchronisiert werden muss. Die Mergereplikation verwendet grundsätzlich unabhängige Agents, während die Transaktionsreplikation standardmäßig unabhängige Agents nur für Veröffentlichungen verwendet, die im Assistenten für neue Veröffentlichung erstellt wurden (in früheren [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Versionen hat die Transaktionsreplikation standardmäßig freigegebene Agents verwendet).  
  
## <a name="replication-maintenance-jobs"></a>Aufträge zur Replikationswartung  
 Die Replikation verwendet die folgenden Aufträge zum Ausführen von geplanten und Bedarfswartungen.  
  
|Cleanupauftrag|Beschreibung|Standardzeitplan|  
|------------------|-----------------|----------------------|  
|Agentverlaufscleanup: Verteilung|Entfernt Verlaufseinträge des Replikations-Agents aus der Verteilungsdatenbank.|Wird alle zehn Minuten ausgeführt.|  
|Verteilungscleanup: Verteilung|Entfernt replizierte Transaktionen aus der Verteilungsdatenbank. Deaktiviert Abonnements, die innerhalb der maximalen Beibehaltungsdauer für Verteilung nicht synchronisiert wurden.|Wird alle zehn Minuten ausgeführt.|  
|Cleanup abgelaufener Abonnements|Ermittelt und entfernt abgelaufene Abonnements aus Veröffentlichungsdatenbanken.|Wird täglich um 1:00 Uhr nachts ausgeführt.|  
|Abonnements mit Datenüberprüfungsfehlern erneut initialisieren|Ermittelt alle Abonnements mit Datenüberprüfungsfehlern und kennzeichnet diese für eine erneute Initialisierung. Bei der nächsten Ausführung des Merge-Agents oder Verteilungs-Agents wird auf die Abonnenten eine neue Momentaufnahme angewendet.|Kein Standardzeitplan (nicht standardmäßig aktiviert).|  
|Überprüfung des Replikations-Agents|Ermittelt Replikations-Agents, die keinen Verlauf protokollieren. Schreibt in das [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows-Ereignisprotokoll, wenn ein Auftragsschritt einen Fehler erzeugt.|Wird alle zehn Minuten ausgeführt.|  
|Aktualisierung für die Replikationsüberwachung für die Verteilung|Aktualisiert die vom Replikationsmonitor verwendeten zwischengespeicherten Abfragen.|Wird fortlaufend ausgeführt.|  
  
## <a name="see-also"></a>Siehe auch  
 [Überwachen der Replikation](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  


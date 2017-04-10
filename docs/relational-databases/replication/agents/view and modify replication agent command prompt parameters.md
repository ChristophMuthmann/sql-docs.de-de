---
title: "Anzeigen und &#196;ndern von Befehlszeilenparametern des Replikations-Agents (SQL Server Management Studio) | Microsoft Docs"
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
  - "Agents [SQL Server-Replikation], Eingabeaufforderungsparameter"
ms.assetid: 45f2e781-c21d-4b44-8992-89f60fb3d022
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Anzeigen und &#196;ndern von Befehlszeilenparametern des Replikations-Agents (SQL Server Management Studio)
  Replikations-Agents sind ausführbare Dateien, die Befehlszeilenparameter akzeptieren. Standardmäßig werden Agents unter ausgeführt [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent-Auftragsschritten, damit diese Parameter angezeigt können und geändert werden mithilfe der **Auftragseigenschaften - \< Auftrag>** (Dialogfeld). Dieses Dialogfeld steht über den Ordner **Aufträge** in [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] sowie über die Registerkarte **Agents** im Replikationsmonitor zur Verfügung. Informationen zum Starten des Replikationsmonitors finden Sie unter [Starten des Replikationsmonitors](../../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
> [!NOTE]  
>  Die Änderungen der Agentparameter treten in Kraft, wenn der Agent das nächste Mal gestartet wird. Wenn der Agent ständig ausgeführt wird, müssen Sie den Agent beenden und neu starten.  
  
 Parameter können zwar direkt geändert werden, aber es ist eher üblich, sie über ein Agentprofil zu ändern. Weitere Informationen finden Sie unter [Replication Agent Profiles](../../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
 Wenn Sie über den Ordner **Aufträge** auf Agentaufträge zugreifen, ermitteln Sie mithilfe der folgenden Tabelle den Namen des Agentauftrags und die jeweils für den Agent verfügbaren Parameter.  
  
|Agent|Auftragsname|Eine Liste der Parameter finden Sie unter|  
|-----------|--------------|------------------------------------|  
|Momentaufnahme-Agent|**\< Publisher>-\< PublicationDatabase>-\< Veröffentlichung>-\< Integer>**|[Replikationsmomentaufnahme-Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)|  
|Momentaufnahme-Agent für eine Mergeveröffentlichungspartition|**Dyn_ \< Publisher>-\< PublicationDatabase>-\< Veröffentlichung>-\< GUID>**|[Replikationsmomentaufnahme-Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)|  
|Protokolllese-Agent|**\< Publisher>-\< PublicationDatabase>-\< Integer>**|[Replikationsprotokolllese-Agent](../../../relational-databases/replication/agents/replication-log-reader-agent.md)|  
|Merge-Agent für Pullabonnements|**\< Publisher>-\< PublicationDatabase>-\< Veröffentlichung>-\< Abonnent>-\< SubscriptionDatabase>-\< Integer>**|[Replikationsmerge-Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)|  
|Merge-Agent für Pushabonnements|**\< Publisher>-\< PublicationDatabase>-\< Veröffentlichung>-\< Abonnent>-\< Integer>**|[Replikationsmerge-Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)|  
|Verteilungs-Agent für Pushabonnements|**\< Publisher>-\< PublicationDatabase>-\< Veröffentlichung>-\< Abonnent>-\< Integer>***|[Replikationsverteilungs-Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)|  
|Verteilungs-Agent für Pullabonnements|**\< Publisher>-\< PublicationDatabase>-\< Veröffentlichung>-\< Abonnent>-\< SubscriptionDatabase>-\< GUID>***\*|[Replikationsverteilungs-Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)|  
|Verteilungs-Agent für Pushabonnements für Nicht-SQL Server-Abonnenten|**\< Publisher>-\< PublicationDatabase>-\< Veröffentlichung>-\< Abonnent>-\< Integer>**|[Replikationsverteilungs-Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)|  
|Warteschlangenlese-Agent|**[\< Verteiler>]. \< ganze Zahl>**|[Warteschlangenlese-Agent der Microsoft SQL Server-Replikation](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)|  
  
 \*Bei Pushabonnements für Oracle-Veröffentlichungen lautet **\< Publisher>-\< Publisher**> statt **\< Publisher>-\< PublicationDatabase>**  
  
 \*\*Bei Pullabonnements für Oracle-Veröffentlichungen lautet **\< Publisher>-\< DistributionDatabase**> statt **\< Publisher>-\< PublicationDatabase>**  
  
### So zeigen Sie Befehlszeilenparameter des Replikations-Agents in SQL Server Management Studio an und ändern Sie die Parameter  
  
1.  Stellen Sie in [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]eine Verbindung mit dem entsprechenden Computer her, und erweitern Sie dann den Serverknoten:  
  
    -   Beim Verteilungs-Agent und Merge-Agent für Pullabonnements stellen Sie eine Verbindung mit dem Abonnenten her.  
  
    -   Bei allen anderen Agents stellen Sie eine Verbindung mit dem Verteiler her.  
  
2.  Erweitern Sie den Ordner **SQL Server-Agent** und anschließend den Ordner **Aufträge** .  
  
3.  Maustaste auf einen Auftrag, und klicken Sie dann auf **Eigenschaften**.  
  
4.  Auf der **Schritte** auf der Seite der **Auftragseigenschaften - \< Auftrag>** Dialogfeld Wählen Sie den Schritt **Agent ausführen**, und klicken Sie dann auf **Bearbeiten**.  
  
5.  In der **Auftragsschritt-Eigenschaften - Agent ausführen** Dialogfeld Bearbeiten der **Befehl** Feld.  
  
6.  Klicken Sie in beiden Dialogfeldern auf **OK** .  
  
### So zeigen Sie Befehlszeilenparameter des Verteilungs- und des Merge-Agents in Replikationsmonitor an und ändern Sie die Parameter  
  
1.  Erweitern Sie im linken Bereich des Replikationsmonitors eine Verlegergruppe, erweitern Sie einen Verleger, und klicken Sie dann auf eine Veröffentlichung.  
  
2.  Klicken Sie auf die Registerkarte **Alle Abonnements** .  
  
3.  Mit der rechten Maustaste ein Abonnement, und klicken Sie dann auf **Details zum**.  
  
4.  In der **Abonnement \< SubscriptionName >** Fenster, klicken Sie auf **Aktion**, und klicken Sie dann auf **\< AgentName> Auftragseigenschaften**.  
  
5.  Auf der **Schritte** auf der Seite der **Auftragseigenschaften - \< Auftrag>** Dialogfeld Wählen Sie den Schritt **Agent ausführen**, und klicken Sie dann auf **Bearbeiten**.  
  
6.  In der **Auftragsschritt-Eigenschaften - Agent ausführen** Dialogfeld Bearbeiten der **Befehl** Feld.  
  
7.  Klicken Sie in beiden Dialogfeldern auf **OK** .  
  
### So zeigen Sie Befehlszeilenparameter des Momentaufnahme-, des Protolllese- und des Warteschlangenlese-Agents im Replikationsmonitor an und ändern Sie die Parameter  
  
1.  Erweitern Sie im linken Bereich des Replikationsmonitors eine Verlegergruppe, erweitern Sie einen Verleger, und klicken Sie dann auf eine Veröffentlichung.  
  
2.  Klicken Sie auf die Registerkarte **Agents** .  
  
3.  Mit der rechten Maustaste eines Agents im Raster, und klicken Sie dann auf **Eigenschaften**.  
  
4.  Auf der **Schritte** auf der Seite der **Auftragseigenschaften - \< Auftrag>** Dialogfeld Wählen Sie den Schritt **Agent ausführen**, und klicken Sie dann auf **Bearbeiten**.  
  
5.  In der **Auftragsschritt-Eigenschaften - Agent ausführen** Dialogfeld Bearbeiten der **Befehl** Feld.  
  
6.  Klicken Sie in beiden Dialogfeldern auf **OK** .  
  
## Siehe auch  
 [Replikations-Agent-Verwaltung](../../../relational-databases/replication/agents/replication-agent-administration.md)   
 [Ausführbare Konzepte für die Programmierung von Replikations-Agents](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)   
 [Replikations-Agents (Übersicht)](../../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
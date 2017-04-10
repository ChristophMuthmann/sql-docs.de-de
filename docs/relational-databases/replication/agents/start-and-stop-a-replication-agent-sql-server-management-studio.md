---
title: "Starten und Beenden eines Replikations-Agents (SQL Server Management Studio) | Microsoft Docs"
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
  - "Agents [SQL Server-Replikation], beenden"
  - "Agents [SQL Server-Replikation], starten"
ms.assetid: 97977c4a-8c7c-4a22-9480-69aa812bd1e5
caps.latest.revision: 42
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 42
---
# Starten und Beenden eines Replikations-Agents (SQL Server Management Studio)
  Starten oder beenden Sie Agents in **** oder im Replikationsmonitor über den Ordner **Aufträge** oder den Ordner [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] and from Aufträge Monitor. Starten oder beenden Sie die folgenden Agents und Aufträge:  
  
-   Momentaufnahme-Agent, der von allen Veröffentlichungen verwendet wird.  
  
-   Protokolllese-Agent, der von allen Transaktionsveröffentlichungen verwendet wird.  
  
-   Warteschlangenlese-Agent, der von Transaktionsveröffentlichungen verwendet wird, die für Abonnements mit verzögertem Update über eine Warteschlange aktiviert wurden.  
  
-   Verteilungs-Agent, der Abonnements für Transaktions- und Momentaufnahmeveröffentlichungen synchronisiert.  
  
-   Merge-Agent, der Abonnements für Mergeveröffentlichungen synchronisiert.  
  
-   Aufträge zur Replikationswartung.  
  
 Weitere Informationen zum Starten der Merge-Agent und der Verteilungsagent, finden Sie unter [Synchronisieren eines Abonnements Push](../../../relational-databases/replication/synchronize-a-push-subscription.md) und [synchronisieren Sie ein Pullabonnement](../../../relational-databases/replication/synchronize-a-pull-subscription.md). Weitere Informationen zu Wartungsaufträgen finden Sie unter [Replikationswartungsaufträge ausführen & #40; SQL Server Management Studio & #41;](../../../relational-databases/replication/administration/run-replication-maintenance-jobs-sql-server-management-studio.md).  
  
 Informationen zum Starten des Replikationsmonitors finden Sie unter [Starten des Replikationsmonitors](../../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
### So starten oder beenden Sie einen Momentaufnahme-Agent oder Protokolllese-Agent in Management Studio  
  
1.  Stellen Sie in [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]eine Verbindung mit dem Verleger her, und erweitern Sie dann den Serverknoten und den Ordner **Replikation** .  
  
2.  Erweitern Sie die **lokale Publikationen** Ordner, und klicken Sie dann mit der rechten Maustaste eine Veröffentlichung.  
  
3.  Klicken Sie auf **Status des Momentaufnahme-Agents anzeigen** oder **Status des Protokolllese-Agents anzeigen**.  
  
4.  Klicken Sie auf **Starten** oder **Beenden**.  
  
### So starten oder beenden Sie einen Warteschlangenlese-Agent in Management Studio  
  
1.  Stellen Sie in [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]eine Verbindung mit dem Verteiler her, und erweitern Sie dann den Serverknoten.  
  
2.  Erweitern Sie den Ordner **SQL Server-Agent** und anschließend den Ordner **Aufträge** .  
  
3.  Maustaste auf den Auftrag für den Agent, und klicken Sie dann auf **Auftrag starten** oder **Auftrag zum Beenden des**. Der Name des Auftrags, für den Warteschlangenlese-Agent wird in der Form **[\< Verteiler>]. \< ganze Zahl>**.  
  
### So starten oder beenden Sie einen Momentaufnahme-Agent, Protokolllese-Agent oder Warteschlangenlese-Agent im Replikations-Monitor  
  
1.  Erweitern Sie im linken Bereich eine Verlegergruppe, erweitern Sie einen Verleger, und klicken Sie dann auf eine Veröffentlichung.  
  
2.  Klicken Sie auf die Registerkarte **Agents** .  
  
3.  Maustaste auf einen Agent, und klicken Sie dann auf **Agent starten** oder **Agent beenden**.  
  
## Siehe auch  
 [Überwachen der Replikation](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)   
 [Ausführbare Konzepte für die Programmierung von Replikations-Agents](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)   
 [Replikations-Agents (Übersicht)](../../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
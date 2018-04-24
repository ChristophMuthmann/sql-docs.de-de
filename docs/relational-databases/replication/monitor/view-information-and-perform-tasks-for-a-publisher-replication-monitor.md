---
title: Anzeigen von Informationen und Ausführen von Aufgaben für einen Verleger (Replikationsmonitor) | Microsoft-Dokumentation
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
- Publishers [SQL Server replication], Replication Monitor tasks
- viewing Publisher information
- Publishers [SQL Server replication], viewing information
ms.assetid: 1e777e95-377a-4de3-b965-867464aadaaf
caps.latest.revision: 37
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0084f2e6288cb2a09810499c38a8c5e1a346fa7f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="view-information-and-perform-tasks-for-a-publisher-replication-monitor"></a>Anzeigen von Informationen und Ausführen von Aufgaben für einen Verleger (Replikationsmonitor)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Der Replikationsmonitor bietet folgende Registerkarten, auf denen Informationen zu dem ausgewählten Verleger angezeigt werden:  
  
-   **Veröffentlichungen**  
  
     Diese Registerkarte enthält Informationen zu allen Veröffentlichungen auf dem ausgewählten Verleger.  
  
-   **Überwachungsliste für Abonnements**  
  
     Auf dieser Registerkarte werden Informationen zu Abonnements von allen auf dem ausgewählten Verleger vorhandenen Veröffentlichungen angezeigt, für die Fehlermeldungen oder Warnungen ausgegeben wurden bzw. bei denen Leistungsprobleme aufgetreten sind. Bei Verteilern, auf denen Versionen vor [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]ausgeführt werden, wird diese Registerkarte nicht angezeigt.  
  
-   Registerkarte**Agents**   
  
     Diese Registerkarte zeigt ausführliche Informationen zu den Agents und Aufträgen an, die von allen Replikationstypen verwendet werden. Über diese Registerkarte können Sie zudem alle Agents und Aufträge starten und beenden.  
  
 Wenn Sie weitere Informationen zu den Optionen auf den einzelnen Registerkarten anzeigen möchten, klicken Sie im rechten Bereich auf die Registerkarte, und klicken Sie anschließend auf der Menüleiste auf **Hilfe** . Informationen zum Starten des Replikationsmonitors finden Sie unter [Starten des Replikationsmonitors](../../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
### <a name="to-view-information-and-perform-tasks-for-a-publisher"></a>So zeigen Sie Informationen für einen Verleger an und führen Aufgaben aus  
  
1.  Erweitern Sie im linken Bereich eine Verlegergruppe, und klicken Sie dann auf einen Verleger.  
  
2.  Um Informationen zu allen Veröffentlichungen anzuzeigen, klicken Sie auf die Registerkarte **Veröffentlichungen** .  
  
3.  Um Informationen zu Abonnements anzuzeigen, klicken Sie auf die Registerkarte **Überwachungsliste für Abonnements** . Über diese Registerkarte können Sie auch auf ausführliche Informationen zugreifen und Aufgaben ausführen:  
  
    -   Wenn Sie detaillierte Informationen zum Agent angezeigt bekommen möchten, der dem jeweiligen Abonnement zugeordnet ist, klicken Sie mit der rechten Maustaste auf das Abonnement, und klicken Sie dann auf **Details anzeigen**.  
  
    -   Wenn Sie die Eigenschaften eines Abonnements anzeigen möchten, klicken Sie mit der rechten Maustaste auf das Abonnement, und klicken Sie anschließend auf **Eigenschaften**.  
  
    -   Wenn Sie ein Pushabonnement synchronisieren möchten, klicken Sie mit der rechten Maustaste auf das betreffende Abonnement, und klicken Sie dann auf **Synchronisierung starten**.  
  
    -   Wenn Sie ein Abonnement erneut initialisieren möchten, klicken Sie mit der rechten Maustaste auf das betreffende Abonnement, und klicken Sie dann auf **Abonnement erneut initialisieren**.  
  
4.  Um Informationen zu Agents anzuzeigen, klicken Sie auf die Registerkarte **Agents** . Sie können von dieser Registerkarte aus auch auf detailliertere Informationen zugreifen und Aufgaben ausführen:  
  
    -   Wenn Sie ausführliche Informationen zu einem Agent (z. B. Informationsmeldungen und Fehlermeldungen) anzeigen möchten, klicken Sie mit der rechten Maustaste auf den Agent, und klicken Sie dann auf **Details anzeigen**.  
  
    -   Wenn Sie detaillierte Informationen zu dem Auftrag anzeigen möchten, durch den der Agent ausgeführt wird (z. B. Zeitplan, Details zu den Auftragsschritten usw.), klicken Sie mit der rechten Maustaste auf den Agent, und klicken Sie anschließend auf **Eigenschaften**.  
  
    -   Wenn Sie die Profile für den Agent verwalten möchten, klicken Sie mit der rechten Maustaste auf den Agent, und klicken Sie dann auf **Agentprofil**. Weitere Informationen finden Sie unter [Arbeiten mit Replikations-Agent-Profilen](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md).  
  
    -   Um einen Agent zu starten, der nicht ausgeführt wird, klicken Sie mit der rechten Maustaste auf den Agent, und klicken Sie dann auf **Agent starten**.  
  
    -   Um einen Agent zu beenden, der ausgeführt wird, klicken Sie mit der rechten Maustaste auf den Agent, und klicken Sie dann auf **Agent beenden**.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Anzeigen und Ändern der Verteiler- und Verlegereigenschaften](../../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [Überwachen der Replikation](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  

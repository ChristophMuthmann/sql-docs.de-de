---
title: Anzeigen von Informationen und Ausführen von Aufgaben für eine Veröffentlichung (Replikationsmonitor) | Microsoft-Dokumentation
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
- viewing publication information
- publications [SQL Server replication], viewing information
- publications [SQL Server replication], Replication Monitor tasks
ms.assetid: 92e28a07-d6a7-461b-a0b3-bd9bc6afcbe5
caps.latest.revision: 39
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5ce5de4bf5315dabe1bd8c2671fc366475a203d6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="view-information-and-perform-tasks-for-a-publication-replication-monitor"></a>Anzeigen von Informationen und Ausführen von Aufgaben für eine Veröffentlichung (Replikationsmonitor)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Der Replikationsmonitor stellt die folgenden Registerkarten mit Informationen zur ausgewählten Veröffentlichung bereit:  
  
-   **Alle Abonnements**  
  
     Auf dieser Registerkarte werden Informationen zu allen Abonnements für die ausgewählte Veröffentlichung angezeigt.  
  
-   **Agents**  
  
     Diese Registerkarte zeigt Informationen zu allen Agents an, die von einer Veröffentlichung verwendet werden.  
  
    -   Momentaufnahme-Agent, der von allen Veröffentlichungen verwendet wird.  
  
    -   Protokolllese-Agent, der von allen Transaktionsveröffentlichungen verwendet wird.  
  
    -   Dem Warteschlangenlese-Agent, der von Transaktionsveröffentlichungen verwendet wird, die Abonnements mit verzögertem Update über eine Warteschlange aufweisen.  
  
-   **Warnungen** (bei Verteilern, auf denen [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] oder höher ausgeführt wird)  
  
    -   Auf dieser Registerkarte können Sie Warnungen für Agents angeben.  
  
-   **Überwachungstoken** (nur bei der Transaktionsreplikation für Verteiler, auf denen [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] oder höher ausgeführt wird)  
  
     Über diese Registerkarte können Sie die Latenzzeit messen, d. h. die Zeitspanne zwischen dem Ausführen des Commit für eine Transaktion auf dem Verleger und dem Ausführen des Commit für die entsprechende Aktion auf dem Abonnenten.  
  
 Weitere Informationen zu den Optionen der einzelnen Registerkarten finden Sie, wenn Sie auf die Registerkarte im rechten Bereich und dann auf **Hilfe** auf der Menüleiste klicken. Informationen zum Starten des Replikationsmonitors finden Sie unter [Starten des Replikationsmonitors](../../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
### <a name="to-view-information-and-perform-tasks-for-a-publication"></a>So zeigen Sie für eine Veröffentlichung Informationen an und führen Sie Aufgaben aus  
  
1.  Erweitern Sie im linken Bereich eine Verlegergruppe, erweitern Sie einen Verleger, und klicken Sie dann auf eine Veröffentlichung.  
  
2.  Zum Anzeigen und Ändern von Veröffentlichungseigenschaften klicken Sie mit der rechten Maustaste auf die Veröffentlichung, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Um Informationen zu Abonnements anzuzeigen, klicken Sie auf die Registerkarte **Alle Abonnements** .  
  
     Zum Anzeigen und Ändern von Abonnementeigenschaften klicken Sie mit der rechten Maustaste auf das Abonnement, und klicken Sie dann auf **Eigenschaften**. Sie können auf dieser Registerkarte auch auf detailliertere Informationen zugreifen und Aufgaben ausführen. Weitere Informationen finden Sie unter [Anzeigen von Informationen und Ausführen von Aufgaben für die einem Abonnement zugeordneten Agent &#40;Replikationsmonitor &#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md).  
  
4.  Um Informationen zu Agents anzuzeigen, klicken Sie auf die Registerkarte **Agents** . Sie können auf dieser Registerkarte auch auf detailliertere Informationen zugreifen und Aufgaben ausführen. Weitere Informationen finden Sie unter [Anzeigen von Informationen und Ausführen von Aufgaben für die einer Veröffentlichung zugeordneten Agents &#40;Replikationsmonitor&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-publication-agents.md).  
  
5.  Um Informationen zu Agentwarnungen und Schwellenwerten anzuzeigen, klicken Sie auf die Registerkarte **Warnungen** . Weitere Informationen finden Sie unter [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md).  
  
6.  Um Informationen zu Überwachungstoken anzuzeigen, klicken Sie auf die Registerkarte **Überwachungstoken** . Weitere Informationen zu Überwachungstoken finden Sie unter [Measure Latency and Validate Connections for Transactional Replication](../../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Anzeigen und Ändern von Veröffentlichungseigenschaften](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Überwachen der Replikation](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
